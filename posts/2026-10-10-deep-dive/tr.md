---
title: "Claude Managed Agents: dinamik iş akışı sunucuya taşındı"
slug: "claude-managed-agents-dinamik-is-akislari"
focus_keyphrase: "Claude Managed Agents"
yoast_title: "Claude Managed Agents: Dinamik İş Akışları"
meta_description: "Claude Managed Agents dinamik iş akışları açık betada. Maliyetleri, sınırları, riskleri ve ilk canlı kullanım öncesi kontrol listesini okuyun."
excerpt: "Anthropic, agent tarafından yazılan iş akışlarını Managed Agents sunucularına taşıdı. Çok sayıda agent artık aşamalar halinde çalışabiliyor. Fakat bütçe, izinler ve tamamlanma durumuna dair önemli ayrıntılar var."
---

## Anthropic'in 9 Ekim duyurusu

Anthropic, Claude Managed Agents için dinamik iş akışlarını 9 Ekim 2026'da açık betaya aldı. Başroldeki agent artık bir program yazabiliyor; bu program çok sayıda agent'ı aşamalar halinde çalıştırıyor, sonuçları kodla birleştiriyor ve bütün işi Anthropic sunucularında sürdürüyor. Üst sınırlar hayli geniş: aynı anda 64 çalışan thread, bir run boyunca toplam 1.000 agent.

Fakat sayıların cazibesine fazla kapılmamak gerek. Bu sistem, birbirinden ayrılabilen iş parçaları ve bunları yeniden bir araya getirecek açık bir kural varsa anlamlı. Üstelik `completed` ibaresi bütün işlerin başarıyla bittiğini söylemiyor, konuşmayı yarıda kesmek run'ı durdurmuyor ve çalışan workflow programını o sırada göremiyorsunuz.

[Claude Platform sürüm notlarına](https://platform.claude.com/docs/en/release-notes/overview) göre özellik `managed-agents-2026-04-01` beta başlığıyla kullanılıyor. Ayarı ise `{"type": "multiagent_20261001", "workflows": {"type": "enabled"}}`. Sistem prompt'uyla ne zaman devreye gireceğini tarif etmek, gelişmeleri `workflow_run.*` event'leri üzerinden izlemek gerekiyor. Run başlatmak için ayrı bir API çağrısı yok.

## Üç farklı devir yolu
<!-- INLINE_IMAGE_1 -->

"Multi-agent" tek yöntemmiş gibi duruyor. Değil. Anthropic üç ayrı yol sunuyor ve aralarındaki fark, kaç agent çalıştırdığınızdan daha önemli.

**Subagent**, doğrudan yardımcı gibi çalışıyor. Ana agent görevi bir child thread'e veriyor, yanıtını alıyor, gerekirse devam sorusu gönderiyor. Sınır 25 child thread ve yalnızca tek seviye. Ara sonuç üzerinde konuşmak, düzeltme istemek ya da yön değiştirmek gerekiyorsa doğal seçenek bu.

**Dinamik workflow**, agent'ın yazdığı ve arka planda çalışan program. Program aşamaları kuruyor, thread'leri çalıştırıyor, gelen çıktıları işliyor. Bir thread'in sonucu sohbeti yürüten agent'a değil, doğrudan programa dönüyor. Ana agent sonradan o thread'e "şurayı bir daha kontrol et" diyemiyor. Üstelik run'ı yalnızca primary thread başlatabildiği için iç içe workflow kurulamıyor.

Karşılığında ana sohbet boşta kalmıyor. Program sunucuda işini sürdürürken agent kullanıcıyla konuşabiliyor. Anthropic'in [multi-agent orchestration rehberi](https://platform.claude.com/docs/en/managed-agents/multiagent-orchestration) bu yolu denetim, migration, derin araştırma ve çapraz kontrol için öneriyor. Hepsinde ortak bir özellik var: iş bölünebiliyor ve parçaların nasıl birleşeceği önceden tarif edilebiliyor.

**Advisor** ise daha hafif bir danışma hattı. Agent, aynı turn içinde başka bir agent'ın fikrini alıyor; arka planda kapsamlı bir program kurmuyor. `multiagent_20261001` ayarında subagent ve workflow varsayılan olarak açık. Advisor ise ayrıca etkinleştirilene kadar kapalı.

İki ayrıntı daha var. Inline agent'lar session agent'ıyla aynı modeli kullanıyor. Önceden tanımlanmış subagent ve workflow listelerinin her birinde en fazla 20 agent tanımı bulunabiliyor. Toplu aşamalarda daha ucuz model seçmek isteyenler için predefined agents bu yüzden önemli. Küçük modellerdeki maliyet yarışının geldiği yeri daha önce [Haiku 5.5 ve GPT-6 Luna fiyatları](https://www.oguzhan.co/tr/claude-haiku-5-5-gpt-6-luna-fiyat-tabani/) vesilesiyle aktarmıştım.

## Claude Managed Agents workflow düzeni
<!-- INLINE_IMAGE_2 -->

Her şey bir `user.message` ile başlıyor. Ana agent mesajı değerlendiriyor, workflow yazıp başlatmaya kendisi karar veriyor. Uygulamanın "şimdi workflow başlat" diye çağıracağı ayrı bir endpoint bulunmuyor. Yazılan program Anthropic'in sunucusunda arka plana geçiyor.

Programı, kod haline getirilmiş iş planı gibi düşünün. İlk aşama bir kod deposunu ya da belge grubunu bağımsız parçalara ayırabilir. Thread'ler paylarına düşeni inceler, sonuçlar programa döner. Sonraki aşama bunları eleyebilir, karşılaştırabilir veya tek çıktıda toplayabilir. Yirmi agent'a aynı genel soruyu sorup çoğunluğun doğruyu bulmasını ummaktan daha düzenli bir yapı.

Bu sırada ana agent sohbete devam edebiliyor. Uygulama da `workflow_run.*` event'leriyle run'ın gidişini izliyor. Ancak çalışan thread'ler sohbetin parçası değil. Yanıtlarını programa teslim ediyorlar ve yoldayken ek talimat alamıyorlar.

Claude Code tarafında dinamik workflow 28 Mayıs'tan beri var ve artık genel kullanıma açık. Aradaki fark basit fakat önemli. Claude Code yerel makinede okunabilen, değiştirilebilen bir script üretiyor. Managed Agents ise agent'ın başlattığı sunucu taraflı bir program çalıştırıyor. Bütçe koyabilir, event'leri izleyebilir, agent'tan run'ı durdurmasını isteyebilirsiniz; fakat çalışan kodu göremezsiniz. Sonradan agent'a programı yazdırmak mümkün. Bu, çalışmadan önce denetim değil, bittikten sonra kayıt sağlar.

Yerel script daha çok ön kontrol sunuyor. Managed Agents ise orchestration yükünü sunucuya bırakıyor ve programın arka planda sürmesini sağlıyor. Kolaylık arttı. Kontrolün bir kısmı da yer değiştirdi.

## Bir workflow run ne kadar tutuyor?

Run için ayrıca kesilen sabit bir ücret yok. İki kalem ödeniyor: seçilen modelin token ücreti ve session `running` durumunda kaldığı sürece saatlik Managed Agents bedeli. Hiçbir thread çalışmıyor olsa bile arka plandaki run session'ı açık tutuyor.

Rakamları yan yana koyalım:

- Aynı anda en fazla 64 thread çalışabiliyor; API bu concurrency seviyesini garanti etmiyor.
- Tek run ömrü boyunca en fazla 1.000 agent oluşturulabiliyor. Sınır aşılırsa `thread_limit_error` geliyor.
- Bir run'ın varsayılan ömrü 24 saat.
- Her session için varsayılan açık run sınırı 10.
- Session, `running` durumundayken saat başına 0,08 dolar.
- 24 saatin yalnızca session bedeli yaklaşık 1,92 dolar. Token ücretleri buna dahil değil.
- Anthropic'in 2025 verisinde multi-agent sistemler sohbetlerin yaklaşık 15 katı token kullandı.
- Ocak 2026'da eşdeğer işler için tek agent'a kıyasla 3 ila 10 katlık aralık verildi.
- Batch API indirimi Managed Agents session'larında geçmiyor.

Saatlik ücret küçük görünebilir. Asıl hesabı token tarafı belirliyor. Altmış dört thread indirim anlamına gelmiyor; kısa sürede model isteği gönderebilecek 64 ayrı çalışma hattı demek.

Bütçeyi session oluşturulurken koymak şart, sonradan eklenemiyor. Sınıra gelindiğinde run duraklıyor. Ne var ki o anda çalışan her thread bir istek kadar taşma yaratabiliyor. Çok sayıda thread aynı anda iş başındaysa belirlenen bütçe ile son tutar arasında hissedilir fark oluşabilir. Sistem bozulmuş sayılmıyor; tarif edildiği gibi çalışıyor.

Bu yüzden run'dan önce şu iki cümleyi kurabilmek iyi bir ölçü: İş hangi bağımsız parçalara ayrılacak? Sonuçlar hangi kuralla birleşecek? Yanıt bulanıksa, birkaç kat token harcayıp aynı belirsizliğin farklı sürümlerini toplamak işten bile değil.

## Can sıkabilecek ayrıntılar
<!-- INLINE_IMAGE_3 -->

İlk tuzak durum etiketinde. `completed`, workflow programının tamamlandığını söylüyor. Her thread'in başarılı olduğunu ya da çıkan sonucun kalite kontrolünden geçtiğini değil. Uygulama thread sonuçlarını ayrıca incelemeli, kendi kabul testini çalıştırmalı. Yeşil renkli bir rozet için erken.

İkinci tuzak durdurma davranışı. Agent'ın turn'ünü yarıda kesmek workflow run'ı durdurmuyor. Ekrandaki yanıt kesilmişken sunucuda token ve zaman harcanmaya devam edebilir. Run'ı durdurmak için ayrıca tanımlanmış bir işletim adımı gerekiyor.

Üçüncüsü görünürlük. Event akışı hareketi gösteriyor ama o sırada karar veren programın kaynak kodunu sunmuyor. Claude Code'daki düzenlenebilir yerel script ile Managed Agents arasındaki en sert fark burada. Programı sonradan istemek hata incelemesine yardım eder; önceden onay sağlamaz.

Dördüncü konu izinler. Permission policy, agent'ların çağırdığı araçlara uygulanıyor. Workflow başlatma kararını engellemiyor. Yüksek sayıda agent çalıştıran bir run için ayrıca onay gerekiyorsa bu kontrolü tool izinlerinin dışında kurmak şart. [AI agent hata türlerinde](https://www.oguzhan.co/tr/ai-ajan-hata-turleri-openai-incelemesi/) gördüğümüz eski bir ders burada da geçerli: tek tek eylemleri sınırlamak, onları sıraya koyan süreci otomatik olarak sınırlamıyor.

Migration sırasında da varsayımlara güvenmemek gerek. `coordinator` ayarından açık tercihler belirtilmeden `multiagent_20261001` sürümüne geçilirse workflow ve inline agents varsayılan olarak açılıyor. Prompt aynı kalsa bile davranış alanı genişleyebilir. Ayarları tek tek yazmak en doğrusu.

Son olarak bütün worker'lar aynı sandbox'ı paylaşıyor ve aynı iş iki defa çalışabiliyor. Mümkün olan araç çağrıları idempotent olmalı, her worker ayrı çıktı yolu kullanmalı. Aksi halde tekrar edilen bir çağrı dış sistemde çift işlem yaratabilir; iki doğru worker birbirinin dosyasını silebilir. Sandbox erişiminin neden başlı başına tasarım meselesi olduğunu [Full Disk Access ve AI agent'lar](https://www.oguzhan.co/tr/apple-full-disk-access-ai-ajanlari/) yazısında başka bir örnek üzerinden anlatmıştım.

## Çok agent harcadığı token'ı ne zaman hak eder?

Anthropic'in saydığı örnekler denetim, migration, derin araştırma ve çapraz kontrol. Bunları uygun kılan yalnızca büyük olmaları değil; bölünebilmeleri.

Dosyalar ayrı ayrı taranabilir, kayıtlar gruplar halinde taşınabilir, kaynaklar bağımsız araştırılabilir, bulgular başka thread'lere doğrulatılabilir. Ardından yinelenenleri silmek, migration sonuçlarını aşamalar halinde uygulamak, kaynakları karşılaştırmak veya bir iddiayı kabul etmek için mutabakat aramak mümkün. Parçalar ve birleştirme kuralı yoksa concurrency, sonradan bir insanın ayıklayacağı metni daha hızlı üretir.

[The Decoder'ın aktardığı](https://the-decoder.com/anthropics-claude-can-now-orchestrate-up-to-1000-ai-agents-in-parallel-through-dynamic-workflows/) Anthropic testi bu farkı çarpıcı bir sayıyla gösteriyor. 116.000 satırlık kod tabanına 70 hata saklanmış. Tek agent her run'da 14 ila 27 hata bulurken dinamik workflow düzenli olarak 66 hataya ulaşmış. Bu bağımsız bir benchmark değil, Anthropic'in testi. Sonucun başka iş türlerinde tekrarlanıp tekrarlanmayacağı da bilinmiyor. Kendi iş yükünde sınamadan genellemek doğru olmaz.

Aynı haberde adı verilmeyen kıdemli bir OpenAI mühendisi, agent sürülerini devasa token israfı diye nitelendiriyor. İki tespit birbiriyle çelişmek zorunda değil. Kapsama alanı önemliyse ve arama sahası temizce bölünebiliyorsa paralellik işe yarar. [Chatbot zaten yeterliyse](https://www.oguzhan.co/tr/ajan-yapay-zeka-nedir-chatbot-ne-zaman-yeter/), worker'lar birbirinin ara sonucunu bekliyorsa ya da iyi birleşim ile akıcı görünen birleşimi ayıracak test yoksa para hızla erir.

Benim ölçüm sade: bağımsız iş parçalarını ve birleştirme kuralını ayrı ayrı tek cümlede yazın. Cümlelerden biri bulanık kalıyorsa küçük başlayın veya subagent kullanın. Agent sayısı kalite ölçüsü değil.

## İlk canlı run öncesi

- `multiagent_20261001` ayarını açıkça yazın; workflow, subagent ve advisor durumlarını tek tek belirtin.
- Workflow'un ne zaman kurulacağını system prompt içinde tarif edin.
- Session bütçesini oluşturma anında koyun; çalışan her thread için bir istek taşma payını hesaba katın.
- 64 thread tavanından uzakta başlayın, gerçek iş yükünü sınayın.
- Başarı ölçüsünü `completed` etiketinden ayrı tanımlayın.
- `workflow_run.*` event'lerini işleyin, run durumunu operatöre gösterin.
- Ortak sandbox içinde her worker'a ayrı çıktı yolu verin.
- Tekrarlanabilecek dış sistem işlemlerini idempotent kurun.
- Run'ı durdurmak için açık bir adım belirleyin. Turn'ü kesmek yetmiyor.
- Görünmeyen sunucu programının denetim ihtiyacına uyup uymadığına karar verin. Düzenlenebilir yerel script gerekiyorsa Claude Code'u değerlendirin.
- İlk denemeden sonra yazdırılan workflow'u, thread hatalarını, token tüketimini, session süresini ve çıktı kalitesini incelemeden sınırları yükseltmeyin.

"Açık beta" yerinde bir tanım. Doğru bölünmüş işi arka planda düzenli bir programa çevirebilen güçlü bir mekanizma var. Onu canlı sistemde güvenilir kılacak şey ise 1.000 agent vaadi değil; baştan konan bütçe, doğru anlaşılan izinler, ayrılmış çıktılar ve gerçekten kontrol edilen sonuçlar.

## Kaynaklar

- [Anthropic, Claude Platform sürüm notları](https://platform.claude.com/docs/en/release-notes/overview)
- [Anthropic, Multi-agent orchestration](https://platform.claude.com/docs/en/managed-agents/multiagent-orchestration)
- [Vanja Petreski, Managed Agents dynamic workflows](https://vanja.io/managed-agents-dynamic-workflows/)
- [The Decoder, Claude ile 1.000 agent'a kadar orchestration](https://the-decoder.com/anthropics-claude-can-now-orchestrate-up-to-1000-ai-agents-in-parallel-through-dynamic-workflows/)
