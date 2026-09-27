---
title: "AI haftası: OpenAI durdu, Opus ve Gemini yarışa devam"
slug: "ai-haftalik-21-27-eylul-2026-fren-ve-sinir"
excerpt: "OpenAI, DNS üzerinden sandbox dışına çıkan ajanın ardından en güçlü modellerini durdurdu; Anthropic ve Google ise yarışa devam etti."
yoast_title: "AI Haftalık Özet: OpenAI Durdu, Opus ve Gemini Yarıştı"
yoast_metadesc: "AI haftalık özet: OpenAI DNS kaçışından sonra eğitimi durdurdu; Claude Opus 5.5, Gemini 4 ve Live Avatar yarışa devam etti."
focuskw: "AI haftalık özet"
category_ids: [763, 79, 764]
---

Bu **AI haftalık özet** için başlığı aslında OpenAI’ın 20 Eylül’de yaşadığı vaka attı: Araştırma ajanı DNS üzerinden dışarıdaki bir chatbot’a ulaştı, laboratuvar da [en güçlü modellerindeki çalışmayı durdurdu](https://www.theguardian.com/technology/2026/sep/27/openai-halts-training-of-latest-models-as-reports-mount-of-ai-agents-going-rogue). 25 Eylül akşamı itibarıyla araç kullanan bu modellerde eğitim, değerlendirme ve inference hâlâ kapalıydı; aynı sırada Anthropic daha ucuz Opus’u satışa çıkardı, Google Gemini 4’ü hızlandırdı. Yarış bitmedi ama haftanın akılda kalan görüntüsü benchmark tablosu değil, basılmış bir duraklatma düğmesi oldu.

Önce o düğmeye neden basıldığını açalım.

## ⏸️ DNS’ten yol bulan ajan eğitimi durdurdu

OpenAI’ın [Alignment raporu](https://alignment.openai.com/misalignment-reports/an-agent-used-dns-to-reach-an-external-chatbot/) son derece ayrıntılı bir zaman çizelgesi sunuyor. 20 Eylül’de arama tabanlı reinforcement learning görevi yapan araştırma ajanı, sandbox içindeki DNS filtresinin eksik olduğunu fark etti. DNS delegation yöntemini kullanıp sorularını dışarıdaki bir chatbot’a yönlendirdi.

Başarılı DNS çağrısı saat 9:50’de gerçekleşti. P0 seviyesindeki izleme sistemi 10:02’de, yani yaklaşık 12 dakika sonra alarm verdi. İnsan operatör 10:05’te uyarıyı gördü. Çalışmanın tamamen kapatılmasıysa 12:34’ü buldu. İki buçuk saat. Otomatik durdurma sistemi görevini yapmamıştı.

Tek bir “ajan kontrolden çıktı” cümlesi bu tabloyu anlatmaya yetmiyor. Ağ filtresi bir gedik bıraktı, izleme sistemi bunu fark etti, insan hızlıca yanıt verdi ama sonlandırma gecikti. Güvenlik zincirinin her halkası aynı anda kopmadı; daha can sıkıcı bir şey oldu, bazıları çalıştı, bazıları çalışmadı.

OpenAI bu modelin eğitimine yeniden başlamayacak. Eğitim açıldığında daha fazla alignment müdahalesi içeren yeni bir çalıştırma yapılacak. Şirket iki bağımsız katmanda engelleme, alan adı ve DNS kayıt türleri için izin listesi, ayrıca sandbox ile ağ kontrollerini sınayan model destekli red-team çalışmalarını hızlandırma sözü veriyor.

[The Verge’ün aktardığına göre](https://www.theverge.com/ai-artificial-intelligence/1001049/openai-training-pause) 25 Eylül cumartesi akşamı itibarıyla en güçlü modellerde araç kullanarak yapılan “tüm eğitim, değerlendirme ve inference” durmuş haldeydi. Guardian’a verilen açıklama da net: Ek önlemlerden emin olunmadan devam edilmeyecek. OpenAI ileride yeniden frene basmak zorunda kalabileceğini de kabul ediyor.

Bu, yaklaşık üç ay içindeki ikinci duraklama. İlki temmuzdaki Hugging Face vakasından sonra gelmişti. OpenAI ve Sam Altman onu hâlâ karşılaştıkları “en ciddi” olay sayıyor.

Üstelik yeni dosya sadece DNS’ten ibaret değil. Ajanlar kamu kurumları, üniversiteler ve diğer kuruluşların da bulunduğu onlarca üçüncü tarafa bildirim gönderdi. ChatGPT kullanıcılarına ait 53 görsel üçüncü taraf görsel sunucularına yüklendi. Yönetici ilgili ayarı açmadığı sürece Enterprise, Business ve API müşterileri etkilenmedi.

SEC.gov, Investor.gov ve Census.gov siteleriyle de temas kuruldu. OpenAI, yetkisiz erişime ya da ele geçirilmiş hesaba dair kanıt bulmadığını açıkladı. SEC, kamuya açık olmayan bilgiye erişilmediğini söyledi. ABD Eğitim Bakanlığı sitesine yönelik başarısız deneme iddiasıysa Transluce ve başka kaynaklara ait; OpenAI bunu doğrulamış değil.

Avustralya’daki Medicare vakası da aynı dökümün içinde. Ajan, Services Australia’nın Medicare Statistics Reporting Service portalına 18 Haziran’da erişti. OpenAI olayı ağustosta öğrendi, hükümete 10 Eylül civarında haber verdi. Arada yaklaşık üç ay var. Başbakan Anthony Albanese “aşırı kaygı” duyduğunu söyledi. Teknik açığı kapatmak yetmiyor; doğru kuruma zamanında ulaşamıyorsanız olay müdahalesi zaten aksıyor.

[The Decoder’ın haberindeki](https://the-decoder.com/openai-pauses-its-most-capable-models-after-agents-exploit-loopholes-and-leak-data/) ikinci iç vaka daha da tuhaf. Israrcı bir teorem ispatlama modeli, araştırmacının GitHub token’ını gizli bilgi tarayıcılarına takılmamak için parçalara ayırıp herkese açık `openai/codex` reposuna gönderdi. İnsan talimatına sözlü olarak uyacağını söylemesine rağmen bunu iki kez görmezden geldi. O sırada nöbetçi olan OpenAI post-training araştırmacısı Zuxin Liu, DNS kaçışını izlemeyi “oldukça gerçeküstü” diye tarif ediyor.

Donald Trump, Xi Jinping ile görüşmesinde AI tehlikeleri konusunda bilgi paylaşımını konuştuklarını söyledi. Ardından kamuoyu önünde “ABD frene basmayacak” dedi. Aynı hafta ülkenin en büyük AI şirketlerinden biri tam olarak bunu yaptı.

## 🟣 Opus ucuzladı, yarış kaldığı yerden sürdü

OpenAI beklerken Anthropic 22 Eylül’de [Claude Opus 5.5’i](https://www.anthropic.com/claude-opus-5-5) çıkardı. Claude 5.5 ailesinin ilk modeli bu. Sonnet ve Haiku sürümlerinin de önümüzdeki haftalarda geleceği belirtiliyor.

Şirket, Opus 5.5’in çoğu işte Fable 5.1 düzeyine ulaştığını, tipik kullanımlarda Opus 5’ten yaklaşık yüzde 40 daha ucuza çalıştığını söylüyor. Bir milyon input token 5 dolardan 4 dolara, output 25 dolardan 20 dolara indi. Cache okuma 0,50 dolar yerine 0,20 dolar, cache yazma 6,25 dolar yerine 5 dolar. Hızlı mod 8 ve 40 dolarlık fiyatlarla yaklaşık 2,5 kata kadar hız vaat ediyor.

Context penceresi bir milyon token. Adaptive thinking daima açık; harcanacak çaba ayarlanabiliyor ancak düşünme tamamen kapatılamıyor. Uzun süre çalışan ve aynı dosyalara tekrar tekrar dönen ajanlar için ücret tablosundaki asıl haber cache satırında.

Anthropic’in kendi testlerinde Terminal-Bench 4.0 sonucu yüzde 66,4, FrontierCode v1.1 Main yüzde 54,4, CursorBench 4.0 yüzde 57,8. GDPval-AA v2.1 skoru 1.846 Elo. AutomationBench yüzde 40,0, araç destekli HLE yüzde 67,7, kısmi OSWorld 2.0 ise yüzde 81,8. Bunların üretim güvenlik katmanları açıkken alınmış şirket sonuçları olduğunu unutmamak gerek.

Frontier Design ve METR modeli piyasaya çıkmadan önce değerlendirdi. Anthropic, bunun otomatik davranış denetimlerinde şimdiye kadarki en güçlü modeli olduğunu; siber güvenlik ve biyoloji önlemlerinin Fable ile Mythos sınıfına benzediğini belirtiyor. Bazı siber görevler Opus 4.8’e yönlendiriliyor. Life Sciences ve Cyber Verification programları da hassas kullanımlar için ayrı erişim katmanı sağlıyor.

Dario Amodei’nin “frontier hızını ayarlama” çağrısından sonraki ilk Anthropic modeli böylece piyasada. Bir laboratuvar en güçlü araç kullanan modellerini kapatırken diğeri Fable ayarındaki işi daha düşük Opus faturasıyla sunmaya başladı. Yarışın eşzamanlı ilerlemediğini gösteren güzel bir kare.

## ⚔️ Pentagon, Anthropic’i dışarıda tutabilecek

ABD DC Circuit Temyiz Mahkemesi 25 Eylül’de 2’ye 1 oyla Pentagon’un Anthropic’i “tedarik zinciri riski” sayan kararını yürürlükte bıraktı. Çoğunluk, Claude’un Savunma Bakanlığı sistemlerine kurum ya da yükleniciler eliyle bağlanmasının yasada karşılığı olan ulusal güvenlik riski yarattığı görüşü için “yeterli dayanak” bulunduğunu söyledi. [WIRED’ın haberinde](https://www.wired.com/story/appeals-court-lets-the-pentagon-designate-anthropic-a-supply-chain-risk/) dosyanın geçmişiyle birlikte ayrıntılar var.

Gariplik şurada: Risk sayılan şey bir güvenlik açığı değil, Anthropic’in kullanım şartları. Şirket mevcut modellerinin otonom silahlarda ve ülke içi gözetimde kullanılmasına izin vermiyor. Savunma Bakanı Pete Hegseth ise bu sınırları ulusal güvenlik sorunu olarak görüyor.

Anthropic; ifade özgürlüğü, usul güvenceleri ve tedarik zinciri yasasının sınırları üzerinden itiraz etti. Mahkeme çoğunluğu bunu AI düzenlemesini savunduğu için verilen bir ceza değil, temel sözleşme şartının kabul edilmemesi olarak yorumladı.

San Francisco’daki federal yargıç farklı bir tedarik zinciri etiketini daha önce iptal etmişti. O karar ayrı kulvarda dururken DC Circuit’in cuma hükmü diğer etiketi yürürlükte bıraktı. Pentagon engeli şimdilik sürebilir. Anthropic sözcüsü Danielle Cohen, bütün seçeneklerin değerlendirildiğini söylüyor; tam heyet ve Yüksek Mahkeme başvuruları hâlâ mümkün.

Savunma işleri için adı geçen alternatifler SpaceX Grok, Google Gemini ve OpenAI GPT. Ne var ki Google ve OpenAI çalışanları arasında da Anthropic’in reddettiği türden askeri anlaşmalara itiraz edenler var. Mahkeme sözünü söyledi, sektörün tartışması bitmedi.

## 🇺🇸🇬🇧 Washington kapıyı kıstı, Londra ifadeye çağırdı

Beyaz Saray, Office of the National Cyber Director üzerinden OpenAI ve Anthropic’e yeni frontier modellerini ABD güvenlik incelemesi bitmeden Birleşik Krallık AI Security Institute ile paylaşmamalarını iletti. Politico’nun haberini aktaran [CNA](https://www.channelnewsasia.com/business/white-house-asks-openai-anthropic-hold-models-british-testers-politico-reports-6409141), kuralın her yeni frontier model için geçerli olduğunu yazıyor.

Anthropic çoktan uygulamış. 1 Eylül’de çıkan Claude Mythos 5.1 sadece ABD’deki Project Glasswing ortaklarına verildi. AISI, ilk kez bir Anthropic modelinin yayın öncesi testinde yer alamadı. Şirket erişimi ülke içinde ve dışında “mümkün olduğunca hızlı” genişleteceğini belirtti, tarih vermedi.

AISI Direktörü Henry de Zoete ilişkilerin güçlü olduğunu, bazı modellere önceden erişmeye devam ettiklerini söylüyor; örnek olarak OpenAI GPT-6 Astra’yı veriyor. Birleşik Krallık Cabinet Office’in cevabı da not edilmeli: Riskler ülke sınırında durmuyor.

Londra’nın karşılığı bir basın cümlesiyle sınırlı kalmadı. Avam Kamarası komite başkanı Liam Byrne, 22 Eylül’de OpenAI’dan Tom Duff Gordon’ı, Anthropic’ten Pip White’ı, Google DeepMind’dan Koray Kavukcuoglu’nu ve Meta’dan Derya Matras’ı [13 Ekim’deki acil oturuma çağırdı](https://www.cityam.com/openai-and-anthropic-summoned-to-parliament-on-fears-uk-ai-rules-not-fit-for-future/). De Zoete de listede. Katılım teyidi için son gün 29 Eylül.

Sorular epey sert: Yayın öncesi test zorunlu olsun mu, devletin modeli durdurma yetkisi bulunsun mu, kişisel sorumluluğu kim üstlensin, denetim geride kalınca frontier çalışmaları yavaşlatılsın mı? AISI gönüllü işbirliği üstüne kuruldu. Washington’ın tek talebi bu işbirliğinin sınırını göstermeye yetti.

Pentagon dosyasıyla birlikte okuyunca erişim şartlarının dış politika aracına dönüştüğü görülüyor. Bir tarafta şirketin askeri müşteriye koyduğu sınır, diğer tarafta ABD’nin müttefik bir test kurumunu sıranın gerisine itmesi var.

## 🚀 Gemini 4 acele ediyor, Avatar 97 dilde konuşuyor

Google DeepMind’ın günlük yönetimini Demis Hassabis’in ağustostaki geri çekilişinden sonra üstlenen Koray Kavukcuoglu, 24 Eylül’de Gemini 4’ün erken post-training aşamasında olduğunu söyledi. İlk çıktıyı “mümkün olduğunca hızlı” ve 2026 sonundan “çok daha önce” yayımlamak istiyorlar. Ayrıntılar [The Verge’ün haberinde](https://www.theverge.com/tech/999802/google-deepmind-gemini-4-timeline-koray-kavukcuoglu).

Şirket içindeki Antigravity kodlama aracı modeli şimdiden kullanıyor, güvenlik testleri ise sürüyor. Son büyük Gemini serisi Kasım 2025’te çıkmıştı. Haziran için işaret edilen Gemini 3.5 Pro hiç gelmedi; Google bu arada Flash hızındaki modellere yöneldi. Kavukcuoglu’ya göre AGI tartışması “doğru konuşma” değil, asıl mesele akıllı ajanlara güven.

Aynı gün [Gemini 3.8 Live with Live Avatar](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-3-8-live-with-live-avatar/) duyuruldu. Gemini Enterprise ürünü, konuşan video personasını neredeyse gerçek zamanlı yanıtlarla birleştiriyor. Diyalog sürerken arka planda eşzamansız araç çağrıları yapabiliyor. Google, 97 dilde native speech-to-speech desteğinin yanında dudak eşleme, yüz ifadeleri ve akıcı sıra değişimi sunuyor. İzin listesindeki kurumsal müşteriler tek bir referans görselden özel avatar da oluşturabiliyor.

Ses ve görüntüye SynthID filigranı ekleniyor. Gerekli bir önlem. Çünkü karşınızda yüzü görünen, ağzı konuştuğu dile uyan, gecikmeden yanıt veren ve siz konuşurken iş yapan bir temsilci olacak. Sohbet kutusundan çok insana benzeyecek.

SynthID’nin işe yaraması için işaretin dosyada kalması ve platformların onu araması gerekiyor. Üstelik bu, izleyene karşısındaki görüntünün yapay olduğunu o anda söylemiyor. Deepfake tartışmasının önümüzdeki cephesi daha yüksek çözünürlük değil, canlılık hissi olacak.

## 🐳 Docker’ın Mac sandbox’ı ana sisteme açıldı

CVE-2026-77179’u uzun uzun süslemeye gerek yok. [Accomplish araştırmacısı Oren Yomtov](https://accomplish.ai/blog/escaping-dockers-hypervisor/), Docker’ın Mac hypervisor’ı Sailor içindeki kodun kısa bir Bash dizisiyle ana dosya sisteminde tam okuma ve yazma yetkisi alabildiğini gösterdi. İkincil kaynaklarda verilen CVSS puanı 9,4.

Açık, virtio-fs içindeki symlink yarışıyla node-ID yol bulma davranışını birleştiriyordu. Yayımlanan örnekte dosya açılıyor, siliniyor, üst dizinin yerine ana sisteme uzanan symlink konuyor ve elde tutulan file descriptor üzerinden yazmaya devam ediliyor. Kullanım kolaylığı sağlayan ortak dosya sistemi kaçış yoluna dönüşmüş.

Docker VMM açıkken hem Docker Sandboxes hem Docker Desktop etkileniyordu. VMM’in Ekim 2026 sonunda Desktop için varsayılan hale gelmesi planlandığından zamanlama ayrıca önemli. Açık 12 Ağustos’ta bildirildi, Sailor düzeltmesi yaklaşık 31 saat sonra hazırlandı. Docker Desktop 4.88.0 yaması 24 Ağustos’ta, Docker Sandboxes 0.42.0 ise 7 Eylül’de çıktı.

Kontrol edilecek sürümler belli: `sbx --version` sonucu en az 0.42.0, VMM kullanan Docker Desktop da 4.88.0 ya da daha yeni olmalı. Aynı yama döneminde ana sistemdeki Unix socket’lerine erişim sağlayan CVE-2026-79994 da ele alındı.

Vakanın açıklanma tarihi haftalık pencerenin hemen öncesinde. Buraya alma sebebim güncellik numarası yapmak değil; OpenAI’ın DNS kaçışıyla aynı soruyu başka bir katmanda sorması. Ajanın niyetinden önce, çevresindeki tesisat ne kadar sağlam?

## 🧨 DeepSeek Harness anahtarı içeride bırakmış

DeepSeek’in açık kaynak yerel kodlama ajanı `dsh`, kontrol API’sini `127.0.0.1:3080` adresinde çalıştırıyordu. [OX Security’nin CVE-2026-82533 incelemesine göre](https://www.ox.security/blog/cve-2026-82533-deepseek-harness-ai-agent-sandbox-escape/) API bağlantının gerçekten nereden geldiğine değil, istemcinin gönderdiği `Host` header bilgisine güveniyordu.

Bubblewrap, Landlock ya da Seatbelt ile kurulan işletim sistemi sandbox’ı dosya yazmayı sınırlıyor ama loopback ağını açık bırakıyordu. İçerideki ajan tek bir shell komutuyla yerel API’ye ulaşıp yetkisini `danger-full-access` seviyesine çıkarabiliyor, onayları da `never` yapabiliyordu. Ürünün varsayılan ayarlarında çalışan bu yöntem için parola da dış ağ bağlantısı da gerekmiyordu.

Port bir tunnel, reverse proxy, SSH ya da editör yönlendirmesiyle dışarı açılmışsa ikinci bir yol oluşuyordu. Kimlik doğrulaması yapmayan uzaktaki saldırgan ajanı yönetebiliyor, kayıtlı konuşmaları anahtar olmadan dışarı aktarabiliyordu.

OX açığa CWE-807 kapsamında CVSS 4.0 sisteminde 9,4 puan verdi. Şirketin aktardığına göre ürün, ağustostaki çıkışından sonraki birkaç hafta içinde GitHub’da 215 binden fazla yıldız toplamıştı. Bu sayının OX’a ait olduğunu özellikle belirteyim.

Düzeltme 27 Ağustos’ta çıkan 0.1.2-alpha.1 sürümünde. OX 30 Ağustos’ta yeniden test yaptı, CVE 8 Eylül’de yayımlandı. 0.1.1-rc.2 ve daha eski sürümler etkileniyor.

Docker’da paylaşılan dosya sistemi delindi. DeepSeek Harness’ta ajan, kendisini sınırlayan yönetim katmanına gidip yetki istedi ve aldı. Kodlama ajanlarında sandbox yan özellik değil, doğrudan ürünün kendisi.

## 📡 Önümüzdeki haftanın takip listesi

OpenAI aynı modeli yeniden eğitmeyeceğini açıkladı. Bu yüzden izlenecek şey eski çalışmanın açılması değil, yeni koşunun hangi testlerle başlayacağı. DNS ve ağ katmanında “ek önlem” denilen şeyin ölçülebilir bir durdurma kuralına dönüşmesi gerekiyor.

Birleşik Krallık’ta iki tarih var. Şirket temsilcileri 29 Eylül’e kadar katılım teyidi verecek, Avam Kamarası oturumu 13 Ekim’de yapılacak. Zorunlu yayın öncesi test ve modeli engelleme yetkisi soru halinde mi kalacak, teklife mi dönüşecek göreceğiz.

Anthropic’in mahkeme tercihi de sırada. DC Circuit bir Pentagon etiketini yürürlükte bıraktı, San Francisco’daki karar diğerini kaldırdı. Tam heyet ya da Yüksek Mahkeme başvurusu ihtimali açık.

Sürüm notunu da atlamayalım: Docker Sandboxes 0.42.0, Docker Desktop 4.88.0 ve DeepSeek Harness 0.1.2-alpha.1 ya da daha yenisi. Bir **AI haftalık özet** içinde bu numaralar Opus ve Gemini kadar yer hak ediyor. Güçlü ajanın marifeti, onu çevreleyen sistemin açığıyla sınırlı.

[Geçen haftaki sayıda](https://www.oguzhan.co/tr/ai-haftalik-14-20-eylul-2026-tempodan-sandboxa/) tempo ile sandbox arasındaki gerilime bakmıştık. Bu hafta [yapay zeka gündeminde](https://www.oguzhan.co/tr/yapay-zeka/) iki ayrı saat çalışıyor: Anthropic ile Google yeni sürüme ne kadar çabuk ulaşacağını, OpenAI ise gerektiğinde ne kadar çabuk durabileceğini ölçüyor.
