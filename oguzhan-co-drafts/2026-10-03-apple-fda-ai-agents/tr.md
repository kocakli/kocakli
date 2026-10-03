---
title: "Apple Full Disk Access: AI ajanları Mac gizlilik ayarını neden zorladı"
slug: "apple-full-disk-access-ai-ajanlari"
yoast_title: "Apple Full Disk Access ve AI ajanları | Oğuzhan"
yoast_metadesc: "Apple, AI ajanları yüzünden Full Disk Access denetimini sıkılaştırıyor. Muse tartışması, yerel erişim riski ve bilinmeyenler burada."
focus_keyphrase: "Full Disk Access"
excerpt: "Yedekleme uygulamaları için açılan Full Disk Access kapısı artık AI ajanlarının dosya, posta ve mesajlara erişim yolu. Apple denetimi değiştireceğini açıkladı; asıl ayrıntılar henüz yok."
---

Mac’te yıllardır duran **Full Disk Access**, yani tam disk erişimi, yedekleme uygulamaları çalışabilsin diye tasarlanmıştı. 2 Ekim’de [Apple bu iznin AI ajanları için fazla tehlikeli hale geldiğini açıkladı](https://developer.apple.com/news/): Bundan sonra bu “olağanüstü” erişimi vermek isteyen kişinin çok açık bir işlem yapması gerekecek. Ne zaman ve nasıl olacağını ise söylemedi.

Kısa duyurunun asıl ağırlığı burada. Apple, eski izin düzeninin kendi başına hareket eden yazılımlara dar geldiğini kabul ediyor. Ortada henüz sınayabileceğimiz yeni bir güvenlik özelliği yok.

## 🍎 Apple’ın Full Disk Access itirafı

<!-- INLINE: fda-permission-gate -->

Apple’ın Developer News sayfasındaki metni birkaç dakikada okuyabilirsiniz. Ancak şirketin kullandığı ifadeler, alıştığımız cilalı güvenlik duyurularından daha açık.

Full Disk Access, macOS’un gizlilik denetimlerini “büyük ölçüde devre dışı bırakıyor.” Bu bilinçli bir tercih. Yedekleme uygulamasının her klasör için ayrı ayrı izin istemesi, korunan verileri atlayıp eksik yedek çıkarması kimsenin işine yaramazdı. Apple da bunun için geniş bir geçiş kapısı bıraktı.

Fakat aynı izin bugün dosyaları, e-postaları, mesajları ve tarama geçmişini kullanıcının “tam bilgisi ve anlayışı” olmadan açığa çıkarabiliyor. Apple’ın ifadesi bu. Üstelik bir iletişim uygulaması söz konusuysa, konuşmanın karşı tarafındaki kişinin mahremiyeti de gidiyor. O kişi herhangi bir izin ekranı görmedi.

Şirket ek denetimler getirecek. Full Disk Access vermek isteyen kullanıcı bunu ancak “çok açık bir işlemle” yapabilecek. Ardından sebebini tek cümlede koyuyor: AI ajanları daha yetenekli ve otonom hale geldikçe bu erişimden doğan risk ciddi biçimde büyüyecek.

Hepsi bu kadar. Tarih yok. Yeni ekranın nasıl görüneceği, mevcut izinlerin yeniden sorulup sorulmayacağı, erişimin parçalara ayrılıp ayrılmayacağı da belli değil. [TechCrunch’ın aktardığına göre](https://techcrunch.com/2026/10/02/apple-says-its-tightening-macos-full-disk-access-controls-due-to-new-risks-from-ai-agents/) Apple, değişikliğin zamanına ilişkin soruyu yanıtlamadı.

Bir ayrıntı daha: Duyuruda Muse, Meta, OpenAI ya da Dots isimleri geçmiyor. Apple sınıfın tamamına bakıyor.

## 💾 Yedekleme izninden ajanın çalışma alanına

Yedekleme yazılımının işi kolay anlatılır. Mac’teki verileri bulur, kopyalar, gerektiğinde geri getirir. Diskin tamamını görme talebi geniştir ama ürünün vaadiyle uyuşur.

AI ajanında iş değişiyor. Bugün bir belgeyi bulmasını istersiniz, yarın o belgeden özet çıkarıp e-postayla ilişkilendirmesini, ertesi gün tarayıcıdaki bilgiyle birleştirip işlem yapmasını. Kurulum sırasında çıkan “disk erişimi” sorusu, henüz aklınıza gelmemiş bütün bu görevleri anlatamaz.

Üstelik Full Disk Access epey kaba bir izin. Tek klasör seçmekten ya da aç penceresinden tek dosya göstermekten farklı. İşletim sistemi geniş kararı bir defa veriyor; bundan sonraki ince sınırların önemli kısmı uygulamanın sözüne kalıyor.

Sorun da tam burada başlıyor. İzin ekranları bugüne kadar çoğunlukla uygulamanın hangi veriye ulaşacağını anlattı. Ajanlarda buna yazılımın kendi başına hangi adımları atabileceğini, hangi connector’ların sonradan ekleneceğini ve güvenilen ajanı başka bir sürecin yönlendirip yönlendiremeyeceğini de katmak gerekiyor.

Eski kapı gerçek bir ihtiyacı çözüyordu. Kapıdan geçen şey değişti.

## 💬 Muse mesajlarımı nereden gördü?

<!-- INLINE: muse-messages-dispute -->

Tartışmayı alevlendiren olay hayli kişisel. Inc. yazarı Jason Aten, Meta’nın Muse adlı ajanının bir iş arkadaşıyla yaptığı özel Apple Messages yazışmasına atıfta bulunduğunu söyledi. Kendisine göre buna izin vermemişti ve mesajların erişim dışında kaldığını sanıyordu.

Meta’nın yanıtı net: Messages erişimi tümüyle isteğe bağlı. Şirket sözcüsü Andy Stone, X’te hem Full Disk Access’in hem de Messages connector’ının açılması gerektiğini, erişimin geri alınabildiğini yazdı. Meta CTO’su David Singleton da Threads’te aynı iki izinli düzeni anlattı.

Burada boşluğu hikâyeyle doldurmamak gerek. Aten’ın Mac’inde Full Disk Access açık mıydı, kapalı mıydı; elimizde kesin bilgi yok. Dolayısıyla “Muse izinsiz biçimde mesajları okudu” hükmü çıkaramayız. Meta’nın savunmasındaki iki ayrı onay da dipnot değil, meselenin ana parçası.

Yine de Patrick Wardle’ın işaret ettiği teknik gerçek tatsız. Full Disk Access verildiğinde root’a ait olmayan dosyalar; tarama geçmişi, cookie’ler ve sohbet kayıtları dahil okunabilir hale gelebiliyor. [Ars Technica’nın haberindeki](https://arstechnica.com/security/2026/10/apple-changes-full-disk-access-permissions-to-curb-abuse-from-ai-agents/) soru şu: İşletim sistemi bu geniş izni verdikten sonra Messages connector’ı tek gerçek kapı mı, yoksa Muse içinde uygulanan ikinci bir ürün kuralı mı?

Apple ertesi günlerde Meta’nın adını anmadan benzer noktaya bastı: Bazı geliştiriciler mesajları, e-postaları ve geçmişi kullanıcı ne olduğunu tam kavramadan açığa çıkarıyor.

Meta “iki izin var” diyor. Apple ise izinlerin toplam sonucunun anlaşılmadığını söylüyor. İkisi aynı anda doğru olabilir.

Bir onay kurulum sırasında, diğeri connector ekranında verildiğinde kullanıcı bunları tek yetki paketi gibi görmeyebilir. Sonra sevimli bir asistan, özel bir konuşmadan bildiği ayrıntıyı ortaya döker. Güvenin koptuğu an budur. İki düğme, sonunda tek kapı açıyor.

## 🧨 Ajan erişime değil, erişim ajana dönüşünce

<!-- INLINE: agent-local-attack-surface -->

Apple’ın açıklamasından yaklaşık 11 gün önce Wardle, Muse ile ilgili daha ciddi bir yapılandırma sorununu duyurdu. Mac’te çalışan başka uygulamalar ya da kodlar, ClickFix yöntemiyle kullanıcıya çalıştırılan komutlar dahil, asistanın denetimini ele geçirip Muse’un yetkilerini kullanabiliyordu.

Bu kez “Ajan mesajları okumalı mı?” sorusu yetmiyor. “Kullanıcı ajana güvendikten sonra ajanı kim yönlendirebilir?” diye sormak gerekiyor.

Geniş yerel erişimi olan asistan, pek çok izni tek yerde topluyor. Zararlı kod her macOS engelini ayrı ayrı aşmak zorunda kalmayabilir; kullanıcının önceden içeri aldığı yazılımı yönlendirmesi yeterli olabilir. İzinler olduğu yerde durur, komut veren değişir.

Hayli ekonomik bir saldırı yolu.

Apple’ın daha açık bir onay istemesi bu yüzden iyi ama tek başına yeterli değil. Yeni ekran, gelişigüzel verilen izinleri azaltabilir. Buna karşılık erişim verildikten sonra ajanın nasıl sınırlandırılacağını, hangi dosyaya baktığının nasıl görüleceğini, kullanıcının komutuyla dışarıdan gelen yönlendirmenin nasıl ayrılacağını henüz bilmiyoruz.

Daha önce [OpenAI’ın agent hata türlerini incelerken](https://www.oguzhan.co/tr/ai-ajan-hata-turleri-openai-incelemesi/) benzer bir sonuca varmıştım: Sorun çoğu zaman tek model yanıtında değil, araçlar ve izinlerle kurulan sistemin tamamında çıkıyor. Yerel makine erişimi bunun üzerine kişisel veri arşivini de ekliyor.

Amazon’ın tepkisi başka bir sınırı gösteriyor. Ars Technica’ya göre Amazon, Muse’u platformundan engelledi ve bu uygulamaların açık biçimde çalışıp hizmet sağlayıcının katılma kararına saygı göstermesi gerektiğini söyledi. Demek ki yalnız Mac sahibinin onayıyla bitmiyor. Yazıştığı insanlar, uygulama geliştiricisi ve erişilen hizmet de bu denklemde.

Tek kutucuk hepsinin rızasını taşıyamaz.

## 🤖 Dots, ChatGPT Mac ve aynı yerel erişim sorusu

OpenAI Dots farklı bir ürün, fakat sınır tanıdık. Aylık 100 dolarlık Pro+ ajanı bir VM içinde çalışıyor; isteğe bağlı olarak masaüstü bilgisayara ChatGPT uygulaması üzerinden erişebiliyor. İzole çalışma ortamından kişisel Mac’e geçildiği anda eski macOS izinleri ajanın araç çantasına ekleniyor.

Dots’un fiyatını ve DevDay duyurusunu [önceki yazıda ayrıntılı ele aldım](https://www.oguzhan.co/tr/openai-devday-2026-dots-sol-pro-500-degerlendirme/). Burada yeniden lansman özeti çıkarmaya gerek yok. Önemli nokta, VM’in ajanın bir bölümünü sınırlarken cihaz erişiminin kalıcı kimlik bilgileri, yazışmalar ve tarayıcı verileriyle dolu yeni bir alan açması.

Muse kişisel bilgileri düzenleyebilir, Dots uzun görevleri üstlenebilir, ChatGPT Mac ise tanıdık sohbet uygulaması gibi görünebilir. Ürün anlatıları ayrı. İşletim sisteminin çözmesi gereken soru aynı: Her süreç neyi okuyacak ve o sürecin denetimi ele geçirilirse ne olacak?

Bu kaygı varsayımdan ibaret değil. TechCrunch, Wired’ın ChatGPT Mac uygulamasındaki bir açığın saldırganların hassas verilere erişmesine imkân verebileceği yönündeki haberini hatırlatıyor. Kaynakta olmayan CVE numarası ya da saldırı ayrıntısı eklemeye lüzum yok. Büyük bir markanın yerel erişimi kendiliğinden güvenli hale getirmediğini göstermesi yeterli.

Uygulamaların connector düzeyindeki denetimleri değerli. Fakat bunlar ikinci savunma hattı. Altındaki işletim sistemi izni, kullanıcının zihninde canlandırabileceğinden çok daha genişse bütün yükü ürün içindeki düğmelere bırakamayız.

## ⏱️ Saldırganın süresi 24 saatten kısa

Microsoft’un 1 Ekim’de yayımladığı [2026 Digital Defense Report](https://www.microsoft.com/en-us/security/blog/2026/10/01/insights-from-the-2026-microsoft-digital-defense-report/) zaman baskısını sayılara döküyor. Sahada bulunan bir açığın saldırı aracına dönüşme süresinin ortancası 24 saatin hayli altında. Kurumların internete açık kritik açıkları kapatmasıysa çoğu kez 30 ila 60 gün sürüyor.

Aradaki fark pek iç açıcı değil.

2026’nın ilk yarısında yaklaşık 40 bin CVE kayda geçti. Microsoft, yılın yaklaşık 72 bin CVE ile kapanma yolunda olduğunu söylüyor. Şubat ile mayıs başı arasında 1,1 milyondan fazla benzersiz cihazda ClickFix tipi komut görüldü; Microsoft Defender verisindeki artış yaklaşık sekiz kat.

ClickFix, insanı kandırıp komut çalıştırmaya dayanıyor. Wardle’ın Muse bulgusu da o komutların geniş yetkili yerel bir ajanı yönlendirebildiği köprüyü gösteriyor. Bu sayılar belirli bir AI ürününe karşı doğrulanmış saldırı kanıtı değil. Fakat Apple’ın neden izin ekranını ağırdan alamayacağını gayet iyi anlatıyor.

Microsoft ayrıca AI kullanımını keşif, phishing, zararlı yazılım ve exploit hazırlığından sistem ele geçirildikten sonraki adımlara kadar görüyor. Agentic sistemler zincirin daha büyük bölümünü otomatikleştirmeye başlamış durumda. Saldırgan bir günden kısa sürede harekete geçerken savunmanın aylar sürmesi, yerel yetkide yapılacak hatayı pahalı hale getiriyor.

## 🛠️ Yeni ayar gelene kadar ne yapacağız?

Apple şimdilik niyet açıkladı. Teknik tasarım ve tarih gelene kadar yapılabilecekler sıkıcı ama etkili.

Mac kullananlar, Sistem Ayarları’nda Full Disk Access verilen uygulamalara yeniden bakabilir. Artık açık bir sebebi olmayan izinleri kaldırmak iyi başlangıç. macOS izniyle uygulama içindeki connector’ı iki ayrı kutu gibi değil, birleştiğinde ortaya çıkan tek yetki gibi düşünmek gerek. Ajan bir VM içinde ya da cihaz erişimi olmadan işi bitirebiliyorsa, gerçekten gerekene kadar dar seçenekte kalmak daha makul.

Geliştirici tarafında işletim sistemi onayı, kullanıcının sonraki bütün veri kaynaklarını anladığının kanıtı sayılmamalı. Hassas connector gerektiği anda yeniden sormak, erişimi geri almayı görünür kılmak, ajanın hangi kaynağa neden baktığını göstermek gerekiyor. Geniş izin, yeni eklenen her özelliğin sessizce miras aldığı sınırsız yetkiye dönüşmemeli.

Wardle’ın bulgusu komut yolunu da tasarımın merkezine koyuyor. Güvenilmeyen içerikle talimatları ayırmak, çalıştırılabilecek komutları sınırlandırmak ve başka yerel süreçlerin ajanı yönlendirmeye çalışacağını varsaymak şart. Güzel hazırlanmış onay ekranı, tıklamadan sonra ele geçirilen bir asistanı kurtarmaz.

Apple’ın önündeki zor seçim ayrıntı seviyesi. Her adımda soru çıkarsa kullanıcı okumayı bırakır. Az soru çıkarsa bugünkü açık çek korunur. Şirketin dengeyi nereye kuracağını bilmiyoruz.

[Model ve agent dağıtımında safety case ihtiyacını](https://www.oguzhan.co/tr/gpt-6-1-astra-iptal-safety-case/) daha önce yazmıştım. Mac tarafındaki sınırlar daha elle tutulur: özel konuşmalar, e-posta arşivi, tarayıcı geçmişi ve AI ürününe hiç onay vermemiş başka insanların verileri.

Full Disk Access gerçek bir yedekleme sorununu çözdü. Ajanlar kapı açıldıktan sonra yapılabilecekleri değiştirdi. Apple kilidi yenileyeceğini söylüyor. Şimdi ayrıntıları bekliyoruz.

## 📚 Kaynaklar

- Apple Developer News, “Updates to Full Disk Access in macOS”, 2 Ekim 2026: https://developer.apple.com/news/
- TechCrunch, Apple’ın Full Disk Access denetimi haberi, 2 Ekim 2026: https://techcrunch.com/2026/10/02/apple-says-its-tightening-macos-full-disk-access-controls-due-to-new-risks-from-ai-agents/
- Ars Technica, Apple, Muse ve Patrick Wardle bulguları: https://arstechnica.com/security/2026/10/apple-changes-full-disk-access-permissions-to-curb-abuse-from-ai-agents/
- The Verge, Apple ve Mac disk erişimi haberi: https://www.theverge.com/tech/1004295/apple-limit-mac-disk-access-ai-agents
- Microsoft, “Insights from the 2026 Microsoft Digital Defense Report”, 1 Ekim 2026: https://www.microsoft.com/en-us/security/blog/2026/10/01/insights-from-the-2026-microsoft-digital-defense-report/
