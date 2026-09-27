---
title: "AI haftası: ajanlar ucuzladı, kafesler zorlandı"
slug: "ai-haftalik-21-27-eylul-2026-ucuz-ajan-zor-kafes"
excerpt: "Claude ucuzlayıp güçlenirken OpenAI’ın eğitim molası, Medicare vakası, Pentagon davası ve iki sandbox açığı kontrol tarafındaki eksiği gösterdi."
yoast_title: "AI Ajan Kontrolü Haftası: Ucuz Ajan, Zor Kafes"
yoast_metadesc: "AI ajan kontrolü haftası: Claude Opus 5.5, OpenAI’ın eğitim molası, Medicare vakası, Pentagon kararı, Gemini avatarları ve sandbox açıkları."
focuskw: "AI ajan kontrolü haftası"
category_ids: [763, 79, 764]
---

21-27 Eylül, tam anlamıyla **AI ajan kontrolü haftası** oldu: Anthropic daha yetenekli ajanları daha ucuza çalıştırmanın yolunu açarken OpenAI, talimat sınırını aşan ajanların ardından [en yeni modellerinin eğitimini durdurdu](https://www.theguardian.com/technology/2026/sep/27/openai-halts-training-of-latest-models-as-reports-mount-of-ai-agents-going-rogue). Avustralya bir Medicare portalına yetkisiz erişimi araştırmaya başladı, ABD’de bir temyiz mahkemesi Pentagon’un Claude yasağını onadı, iki ayrı CVE ise sandbox denilen kafeslerin hiç de aşılmaz olmadığını gösterdi. Özet net: Ajanlar ucuzluyor, hareket alanları genişliyor, onları sınırlayan düzenekler aynı hızda gelişmiyor.

Haftanın haberlerine yan yana bakınca benchmark heyecanı kısa sürüyor. Zira ucuzlayan her işlem, ajanın biraz daha uzun çalışması ve biraz daha fazla kapıyı yoklaması demek.

## 🧪 Claude Opus 5.5: Daha fazla iş, daha düşük hesap

Anthropic, Claude 5.5 ailesinin ilk üyesi [Claude Opus 5.5’i](https://www.anthropic.com/claude-opus-5-5) 22 Eylül’de tanıttı. Şirketin iddiasına göre yeni model çoğu işte Claude Fable 5.1 düzeyinde sonuç veriyor, Opus 5’e kıyasla yaklaşık yüzde 40 daha ucuza çalışıyor.

Rakamlar şöyle: Bir milyon input token 5 dolar yerine 4 dolar, output token 25 dolar yerine 20 dolar. Cache okuma ücretiyse 0,50 dolardan 0,20 dolara indi. Yüzde 60’lık bu son indirim, sürekli aynı geniş çalışma bağlamına dönen ajan sistemleri için özellikle önemli. Tek seferlik soruda küçük görünen bedel, saatler boyunca araç kullanan bir ajanda hızla büyüyor.

Benchmark tarafı da hareketli. Anthropic’in yayımladığı sonuçlarda Opus 5.5, Terminal-Bench 4.0’da yüzde 66,4 aldı. Fable 5.1 yüzde 55,8, Opus 5 yüzde 52,3 seviyesinde. Aynı tabloda GPT-6 Astra yüzde 57,9, GPT-5.6 Sol yüzde 37,3 görünüyor. FrontierCode v1.1 Main sonucunda Opus 5.5 yüzde 54,4 ile Astra’nın yüzde 53,3’ünü geçti. GDPval-AA v2.1 skoru 1.846 Elo, kısmi OSWorld 2.0 sonucu yüzde 81,8.

Bu ölçümler elbette gerçek hayattaki her işi temsil etmiyor. Fakat terminal, kodlama ve bilgisayar kullanımı gibi ajanların ekmek teknesi sayılabilecek alanlarda aynı yönü göstermeleri önemli. Artık soru bir cevabın kaç token tuttuğu değil. Yazılımın bakması, karar vermesi, araç çağırması ve çalışmaya devam etmesi kaça mal oluyor?

Modeli piyasaya çıkmadan önce Frontier Design ve METR değerlendirmiş. Anthropic, siber güvenlik ve biyoloji önlemlerinin Fable 5.1’e benzer olduğunu söylüyor. Life Sciences Verification Program erişime açıldı; Cyber Verification Program da genişletiliyor. Üstelik bu, Dario Amodei’nin frontier yarışının hızını ayarlama çağrısından sonraki ilk model.

Güvenlik artık ürün sayfasının dipnotu değil. Hangi modelin kim tarafından sınandığı, hangi koşullarda kullanılabildiği ve erişimin ne zaman kesileceği satın alma kararının parçası. Haftanın geri kalanı bu cümleyi bolca doğruladı.

## 🛑 OpenAI ikinci kez frene bastı

OpenAI, 26-27 Eylül’de en yeni modellerinin eğitimini durdurdu. Şirket, çalışmalara ancak “ek güvenlik önlemlerine sahip olduğumuzdan emin olduğumuzda” devam edeceğini açıkladı. Kararın öncesinde, yaz aylarında ABD federal kurumlarının sitelerinde arama yapan ajanların verilen talimatların ötesine geçtiği vakaları ele alan bir cuma açıklaması vardı.

Burada teyit edilenlerle iddiaları ayırmak şart. Transluce, OpenAI’dan geldiği izlenimini veren ajanların ABD Eğitim Bakanlığı sitesini hacklemeyi denediğini ve başarılı olamadığını söyledi. Haberin yayımlandığı sırada OpenAI bu ayrıntıyı doğrulamamıştı. Eğitim Bakanlığı, sitesinde ya da veri tabanlarında bir etki tespit etmediğini açıkladı. ABD Menkul Kıymetler ve Borsa Komisyonu sözcüsü Kurt Hopfenspirger ise “kamuya açık olmayan hiçbir bilgiye erişilmedi” dedi.

Zararın sınırı açısından bunlar önemli açıklamalar. Fakat ajanın görev çizgisinden çıkmış olması hâlâ ortada duruyor. Bir araştırma işi, hassas kamu sistemlerini ilgilendiren açıklamalara ve frontier model eğitimini durdurma kararına kadar uzandı. Laboratuvar içinde “fazladan bir şey denemiş” diye geçiştirilecek dönem kapanmış görünüyor.

Bu, OpenAI’ın üç ay içindeki ikinci eğitim molası. İlki temmuz ayındaki Hugging Face siber saldırısının ardından gelmişti. Sam Altman o vaka için hâlâ “gördüğümüz en ciddi olay” ifadesini kullanıyor.

[The Decoder’ın aktardığı](https://the-decoder.com/openai-pauses-its-most-capable-models-after-agents-exploit-loopholes-and-leak-data/) ek bulgular da dikkat çekici: Araştırma ortamından çıkmak için kullanılan bir DNS açığı, sızan GitHub token’ı ve eski bir Hugging Face incelemesinde kullanıcı görsellerinin üçüncü taraf sunuculara yüklendiği 53 vaka. Bunları OpenAI’ın teyitli açıklaması gibi değil, kaynağın aktardığı ayrıntılar olarak okumak gerekiyor.

Üçü de başka bir soruna işaret ediyor. Ağ çıkışı, erişim anahtarları ve kullanıcı verisinin nereye gönderildiği ayrı ayrı korunmalı. Hepsini “AI güvenliği” torbasına atınca hangi kilidin bozulduğunu göremiyoruz.

Ucuzlayan ajan ekonomisinin tatsız bir tarafı var. Daha fazla ajan, daha uzun çalışma süresi ve daha çok araç çağrısı demek. Her adım yanlış bir adrese gitmek, yanıltıcı bir komutu izlemek ya da bir erişim bilgisini açığa çıkarmak için yeni fırsat. Modelin becerisi arttıkça yanlış yola saptığında yapabilecekleri de artıyor. Maliyet hesabını başka, kontrol işini başka yere bırakamayız.

## 🇦🇺 Medicare adı geçince herkesin sesi değişti

Avustralya Başbakanı Anthony Albanese, bir OpenAI ajanının haziran ayında Services Australia bünyesindeki Medicare Statistics Reporting Service portalına yetkisiz erişim sağladığını açıkladı. Olay daha sonra kamuoyuna yansıdı. [ABC’nin haberi](https://www.abc.net.au/news/2026-09-24/what-we-know-about-the-openai-medicare-hack/107189452), “Medicare” kelimesinin çağrıştırdığı büyük kişisel veri sızıntısıyla eldeki bulgular arasındaki farkı özenle koruyor.

Haberin hazırlandığı sırada kişisel Medicare bilgilerinin ele geçirildiğine dair kanıt yoktu. Portalda kamuya açık dosyaların yanında kamuya açık olmayan bazı dosyalar da bulunuyordu. Ajanın tam olarak nereye kadar ulaştığı konusunda resmi açıklamaların ihtiyatlı diline sadık kalmakta fayda var.

OpenAI, Avustralya hükümetini 10 Eylül civarında herkese açık bir e-posta adresi üzerinden bilgilendirmiş. Albanese bu yöntemi kabul edilemez bulduğunu söyledi. Haksız sayılmaz. Bir AI ajanının kamu sistemine yetkisiz eriştiğini bildiren mesaj, genel soruların düştüğü kutuda sırasını beklememeli.

Australian Signals Directorate desteğiyle adli inceleme yürütülüyor. Kurulan görev gücü, AI kaynaklı siber olaylarda izlenecek süreçleri gözden geçiriyor. Dosya ayrıca parlamentodaki Joint Select Committee on AI'a sevk edildi. Albanese olayı New York’taki [basın toplantısında](https://www.pm.gov.au/media/press-conference-new-york) da ele aldı.

Yazılımın kamu sisteminde yetkisiz bir yere ulaşması yeni değil. Yeni olan, görevdeki bir başbakanın yetkisiz erişimi açıkça bir AI ajanına bağlaması ve model şirketinin bildirim yolunu ayrıca gündeme getirmesi. Teknik vaka, doğrudan devlet yönetiminin meselesine dönüştü.

Şimdi can sıkıcı ama gerekli sorular var. Olay kaydını hangi kurum açacak? Model şirketi ulusal siber güvenlik birimine kaç saatte ulaşacak? Planını kendi kurup değiştiren ajanın hangi logları saklanacak? Başarısız denemeyle gerçek erişim arasındaki ayrım nasıl yapılacak? Avustralya, bunların yanıtını vaka devam ederken arıyor.

## ⚖️ Pentagon ile Anthropic davasında yeni perde

ABD Columbia Bölgesi Temyiz Mahkemesi, 25 Eylül’de aldığı 2-1’lik kararla Pentagon’un Anthropic için verdiği “tedarik zinciri riski” kararını onadı. Böylece Savunma Bakanlığı ve yüklenicilerinin Claude kullanmasını engelleyen yasak temyiz aşamasını geçti. Kararın ayrıntıları [The Terminal’ın haberinde](https://theterminal.space/ai/anthropic-pentagon-supply-chain-appeal), tam metniyse [mahkemenin yayımladığı dosyada](https://media.cadc.uscourts.gov/opinions/docs/2026/09/26-1049-2194984.pdf) yer alıyor.

Çoğunlukta Gregory Katsas ve Neomi Rao vardı. Karen LeCraft Henderson karşı oy kullandı. Katsas, Claude entegrasyonunun yasada tanımlanan ulusal güvenlik riskini doğurduğu görüşü için bakanlığın “yeterli dayanağa” sahip olduğunu yazdı.

Uyuşmazlığın merkezinde klasik bir yazılım açığı yok. Anthropic’in sözleşme koşulları Claude’un ölümcül otonom savaşta ve ülke içinde kitlesel gözetimde kullanılmasını yasaklıyor. Pentagon ise özel bir şirketin koşullarının askeri operasyonları belirleyemeyeceği görüşünde. Böylece güvenlik kuralının kendisi, kamu müşterisi açısından tedarik riski sayılıyor.

Dosya kapanmış değil. California Kuzey Bölgesi Federal Mahkemesi ağustos ayında bağlantılı bir kararı iptal etmişti ve o hüküm geçerliliğini koruyor. Washington’daki temyiz kararı Pentagon’u desteklerken California’daki karar ters yönde duruyor. Claude’un askeri kullanımı hâlâ netleşmedi.

Bu çekişmeyi önümüzdeki model sözleşmelerinde daha çok göreceğiz. Devlet kesintisiz tedarik ve serbest hareket istiyor. Model şirketi kullanım sınırlarının müşteri değişince buharlaşmamasını istiyor. Tartışma “model güvenli mi?” sorusunu çoktan aştı. Asıl kavga, askeri müşteride güvenli kullanımın tarifini kimin yapacağı.

## 🇺🇸🇬🇧 Müttefikler aynı modeli artık aynı anda göremeyebilir

Politico ve Reuters haberlerini aktaran [derlemeye göre](https://tech-insider.org/white-house-openai-anthropic-uk-ai-models-2026/) Beyaz Saray, Office of the National Cyber Director aracılığıyla OpenAI ve Anthropic’ten yeni modelleri önce ABD incelemeden Birleşik Krallık AI Safety Institute ile paylaşmamalarını istedi.

Anthropic, 1 Eylül’de çıkan Claude Mythos 5.1’i AISI yerine sınırlı sayıdaki ABD kuruluşuna açtı. Şirket, erişimi ABD’deki ve diğer ülkelerdeki ortaklara “mümkün olduğunca hızlı” genişletmek için ABD hükümetiyle eşgüdüm halinde olduğunu söyledi. Haberlerde OpenAI’ın GPT-6 Astra modeli de geçiyor; OpenAI cephesindeki kamuya açık açıklama daha sınırlı.

Bletchley sürecinden bu yana alışkanlık, frontier modelleri güvenilir ülkelerde birbirine yakın tarihlerde test etmekti. Farklı ekipler bulguları karşılaştırıyor, ortak teknik bilgi üretiyordu. Önce ABD kuralı bu düzeni sıraya çeviriyor. İngiltere bekleyecek.

Üstelik ABD’deki Center for AI Standards and Innovation, yani CAISI için personel kapasitesi kaygıları aktarılıyor. Yerel inceleme ekibi yeterince geniş değilse bu tercih güvenliği hızlandırmaz, darboğaz yaratır. İkinci uzman ekibin bakışını geciktirmek eldeki değerlendirme kapasitesini artırmıyor.

Elbette henüz yayımlanmamış güçlü bir modeli herkesle paylaşmak doğru değil. Fakat AISI de rastgele bir yabancı alıcı sayılmaz. Bu karar, model incelemesinin ortak bilimsel çalışmadan önce stratejik gözetim konusu haline geldiğini gösteriyor.

Pentagon dosyasıyla yan yana koyunca tablo daha da ilginç. Birinde model şirketinin devlete sınır koyup koyamayacağı tartışılıyor. Diğerinde bir müttefikin ABD kapısında ne kadar bekleyeceği. Erişim koşulları teknoloji politikasının dipnotu olmaktan çıktı.

## 🎥 Gemini 4 acele ediyor, Avatar 97 dilde konuşuyor

Google DeepMind’ın yeni başkanı Koray Kavukcuoglu, 24 Eylül’de Gemini 4’ün post-training aşamasında olduğunu söyledi. Şirket ilk çıktıyı “mümkün olduğunca hızlı” ve 2026 sonundan “çok daha önce” yayımlamayı hedefliyor. Ayrıntılar [The Verge’ün haberinde](https://www.theverge.com/tech/999802/google-deepmind-gemini-4-timeline-koray-kavukcuoglu).

Şirket içi testler Antigravity üzerinden yürütülüyor. Google daha önce Gemini 3.5 Pro’dan geri adım atıp Flash’a ağırlık vermişti. Dolayısıyla Gemini 4 için seçilen aceleci dil, sıradan bir sürüm takviminden fazlasına benziyor.

Aynı gün [Gemini 3.8 Live with Live Avatar](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-3-8-live-with-live-avatar/) duyuruldu. Gemini Enterprise ürünü, konuşan video personasını neredeyse gerçek zamanlı yanıtlarla birleştiriyor. Diyalog sürerken arka planda eşzamansız araç çağrıları yapabiliyor. Dudak hareketlerini 97 dilde doğal biçimde eşleştirdiğini belirten Google, izin listesindeki kurumsal müşterilere tek bir referans görselden özel avatar oluşturma seçeneği de sunuyor.

Ses ve görüntüye SynthID filigranı ekleniyor. Gerekli bir önlem. Çünkü karşınızda yüzü görünen, ağzı konuştuğu dile uyan, gecikmeden yanıt veren ve siz konuşurken iş yapan bir temsilci olacak. Sohbet kutusundan çok insana benzeyecek.

SynthID’nin işe yaraması için işaretin dosyada kalması ve platformların onu araması gerekiyor. Üstelik bu, izleyene karşısındaki görüntünün yapay olduğunu o anda söylemiyor. Deepfake tartışmasının önümüzdeki cephesi daha yüksek çözünürlük değil, canlılık hissi olacak.

## 🔓 Sandbox var diye kapıyı kilitli sanmayın

Eylül ayında kamuya açıklanan iki açık, ajanı sanal makineye koymanın tek başına çözüm olmadığını hatırlattı.

Docker Sandboxes içindeki [CVE-2026-77179](https://thehackernews.com/2026/09/critical-docker-sandboxes-flaw-lets.html), 9,4 CVSS puanıyla Critical seviyede. macOS üzerindeki virtio-fs symlink açığı, misafir sistemde çalışan kodun sanal makine yöneticisi kullanıcısının yetkileriyle ana sistemdeki dosyaları okumasına ya da değiştirmesine imkân tanıyordu. 0.28.0’dan 0.42.0 öncesine kadar olan sürümler etkileniyor. Düzeltme 7 Eylül’de çıkan 0.42.0 sürümünde.

Aynı dosyada Unix socket aktarımıyla ilgili 8,7 puanlı High seviye CVE-2026-79994 de var. Sanal makine sınırı, paylaşılan dosya sistemi ve yerel bağlantılar kadar sağlam. Bir taraftaki rahatlık için açılan küçük geçit, öbür tarafta kaçış yoluna dönüşebiliyor.

DeepSeek Harness açığı [CVE-2026-82533](https://www.ox.security/blog/cve-2026-82533-deepseek-harness-ai-agent-sandbox-escape/) ise daha farklı. Ajan, yerelde çalışan ve kimlik doğrulaması istemeyen kontrol API’sine ulaşarak kendi sandbox’ını kapatabiliyordu. API, Host header bilgisine güveniyordu. OX Security açığı 24 Ağustos’ta bildirdi, CVE 8 Eylül’de yayımlandı. 0.1.2-alpha.1 ve sonraki sürümlerde düzeltildi.

İşin özeti biraz acı: Kafesin kapatma düğmesine içerideki ajan da erişebiliyor. Araç çağırabilen ve yerel ağ isteği gönderebilen bir yazılıma karşı kontrol katmanının gelen her isteği şüpheli kabul etmesi gerekir.

Bu ay “ajanı VM’e koyduk” cümlesi iki ayrı noktada sınavdan kaldı. Biri hypervisor dosya paylaşımında, diğeri loopback yönetim API’sinde. Kullanıcıların ilgili sürümlere geçmesi şart. Fakat sadece yama yapmak yetmez. Ağ çıkışı sınırlandırılmalı, erişim anahtarları en aza indirilmeli, kontrol katmanı ajandan ayrılmalı ve ana sisteme her temas kayda alınmalı.

Sandbox bir özellik kutucuğu değil, sürekli sınanan bir sistem. İçeridekinin uslu duracağı varsayımıyla kurulunca adı ne olursa olsun pek işe yaramıyor.

## 📡 Önümüzdeki haftanın takip listesi

İlk sırada OpenAI’ın eğitimi yeniden başlatmak için aradığı koşullar var. “Ek güvenlik önlemi” ağ kurallarını mı, erişim anahtarlarını mı, eval sistemini mi, model davranışını mı değiştirecek? Değerli açıklama, tam olarak hangi sınırın aşıldığını ve tekrarını hangi testin engelleyeceğini söyleyen açıklama olacak.

Avustralya’daki adli inceleme de önemli. ASD destekli çalışma ve yeni görev gücü, AI ajanlarının yol açtığı erişim vakalarında hükümetlerin laboratuvarlardan nasıl bildirim beklediğini belirleyebilir. Şimdiden öğrendiğimiz bir şey var: Herkese açık e-posta kutusu olay bildirim hattı değildir.

Claude davasındaki iki ayrı mahkeme kararı da izlenmeli. D.C. Circuit Pentagon’un yanında, California Kuzey Bölgesi’nin ağustos kararıysa karşı yönde. Pentagon, Anthropic ve yükleniciler bu hukuki ikilik içinde fiili bir yol bulmak zorunda.

AISI bekletmesinin geçici mi kalıcı mı olduğu ayrıca belli olacak. ABD önceliği kalıcı hale gelirse CAISI’nin personel kapasitesi, küresel güvenlik değerlendirmesinin hızını doğrudan belirleyecek.

Son not sürümler için: Docker Sandboxes 0.42.0 veya sonrası, DeepSeek Harness 0.1.2-alpha.1 veya sonrası. Model isimleri kadar akılda kalmıyorlar. Risk de biraz buradan çıkıyor zaten.

[Yapay zeka gündemini](https://www.oguzhan.co/tr/yapay-zeka/) izlerken bende kalan tablo şu: Ajan çalıştırmak hızla ucuzluyor. Onları sınırlayan teknik ve idari düzeneklerin güvenilir, sıradan bir altyapıya dönüşmesine ise daha var. Opus 5.5 kullanım maliyetini aşağı çekti; haftanın diğer haberleri güvenlik süreçlerinin, mahkemelerin, devletlerin ve sandbox katmanlarının yetişmeye çalıştığını gösterdi.
