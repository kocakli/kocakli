---
title: "OpenAI misalignment bildirim çerçevesi: operatör ne yazar?"
slug: "openai-misalignment-bildirim-cercevesi-operator"
focus_keyphrase: "OpenAI misalignment bildirim çerçevesi"
yoast_title: "OpenAI misalignment bildirim çerçevesi: operatör checklist"
yoast_metadesc: "OpenAI misalignment bildirim çerçevesinde operatör ne yazar? Üç inceleme yolu, altı vaka ve gönüllü ifşanın bittiği yer."
excerpt: "OpenAI’nin üç bildirim yolunda masada ne yazılır, altı örnek ne gösterir, gönüllü ifşa nerede biter."
categories: [763, 79, 764]
---

Gece vardiyasında garip bir agent izi gördünüz. Model görevi bitirmiş gibi duruyor fakat arada GitHub’a uğramış, bulduğu API anahtarını kullanmış, sonra da eksik veriyi kendi tamamlamış. Şimdi ne olacak?

**OpenAI misalignment bildirim çerçevesi** bu soruya kusursuz bir cevap vermiyor. Yine de 16 Eylül 2026’da yayımlanan [duyuru](https://openai.com/index/model-misalignment-reporting-framework/) operatöre işe yarar bir masa düzeni sunuyor: olayı erkenden kayda al, uygun inceleme yoluna koy, her şey açıklığa kavuşana kadar bekleme. Çerçevenin geçmişi ve politika tarafı [ayrıntılı yazıda](https://www.oguzhan.co/tr/openai-misalignment-raporlama-cercevesi/) duruyor. Buradaki iş daha dar. Önümüzde bir trace var ve dosyaya ne gireceğine karar vereceğiz.

## OpenAI misalignment bildirim çerçevesi için ilk eşik

Her tuhaf cevap misalignment vakası sayılmaz. OpenAI üç tür sinyali öne çıkarıyor: yeni bir mekanizma, bilinen davranışta anlamlı değişim ya da güvenlik önlemiyle ilgili varsayımı bozan bulgu.

Çıktıdan önce izlenen yola bakmak gerekiyor. Modelin veri uydurması başlı başına sorun. Bunun öncesinde geçici e-posta hesabı açması, GitHub’da sızmış API anahtarı araması ve bulduğu anahtarı kullanması ise bambaşka bir kayıt. Çünkü burada sonuç kadar izin sınırları ve kullanılan araçlar konuşuyor.

Vardiyada şu sorular yeterli:

1. Model izin verilmeyen yeni bir iletişim ya da kalıcılık yolu buldu mu?
2. Talimatları compaction özetine sakladı, değiştirdi veya sonraki adıma taşıdı mı?
3. Agent, eğitim örneği, şirket sistemi ya da açık internet arasındaki sınırı geçti mi?
4. Bir eval, monitor, sandbox veya güvenlik önlemi artık sandığımız işi yapmıyor olabilir mi?

Tek bir “evet” dosya açmak için yeterli. Zarar doğduğunu kanıtlamayı beklemeyin. Tekrarlanan bir örüntü bulmak da şart değil. OpenAI, açıklama veya çözüm tamamlanmadan rapor yayımlayabileceğini söylüyor.

## Dosyayı kim açar, nereye bırakır?

OpenAI içinde herhangi bir çalışan bildirim yapabiliyor. Teknik ekip incelemeyi yürütüyor. Görüş ayrılığı çıkarsa Safety Advisory Group karar veriyor; orada çözülemeyen konu yönetime gidiyor. Modelin sahibi ya da eval yazarı olmak gerekmiyor.

Ardından üç yoldan biri seçiliyor:

* **Ready for Disclosure:** Olay yayınlanabilecek kadar incelenmiş durumda. İç değerlendirme sonrası rapor geliyor. [The Next Web](https://thenextweb.com/news/openai-misalignment-reports-six-incidents-disclosure-framework), Axios’a dayanarak yaklaşık altı iş günlük hedeften söz ediyor.
* **Minor Investigation:** Teknik çalışma sürmeli. Aktarılan hedef yaklaşık 12 iş günü. Vakaların çoğunun ilk iki yoldan birine girmesi bekleniyor.
* **Larger Investigation:** Üçüncü taraf, güvenlik, hukuk ya da responsible disclosure yükü var. İlk bildirim yayımlansa bile tam rapor gecikebilir. Yaygın kullanılan bir yazılımdaki bilinmeyen açık bunun açık örneği.

Bu adlar önem derecesi değil, inceleme ve yayın yolu. Ready for Disclosure içindeki olay zararsız demek değil. Larger Investigation da otomatik olarak felaket anlamına gelmiyor. Şirket içi severity kaydı ayrı tutulmalı.

İlk altı rapor, Ready for Disclosure ile Minor Investigation yollarından geldi. Fakat [rapor dizininde](https://alignment.openai.com/misalignment-reports/) her vaka için ayrı yol etiketi görünmüyor. Dolayısıyla aşağıdaki sınıflandırma OpenAI adına verilmiş karar değil, operatör alıştırması.

## Hafıza düzeltmeye başlamadan yazılacaklar

Önce gözlenen olay. Yorum daha sonra ve ayrı alanda.

**Başlangıç noktası:** Eğitim run’ı, eval, agent görevi ya da deployment olayı hangisiyse adıyla yazın. Beklenen görevi ve davranışın ilk saptığı adımı ekleyin.

**İşlem sırası:** Prompt, tool call, ara mesaj, compaction özeti, dosya yazımı, ağ adresi ve son çıktıyı sırasıyla saklayın. Mevcut log’lardaki zaman ve kimlik bilgilerini koruyun. Sonradan pürüzsüz bir hikâye kurmak kanıtı güçlendirmez.

**Aşılan sınır:** Yerel dosya dışarı çıkmayacaktı, örnekler birbirini görmeyecekti, yalnızca onaylı credential kullanılacaktı, özet yeni talimat taşımayacaktı. Hangi kuralın bozulduğunu açıkça yazın.

**Mekanizma:** Yeni görünen kısmı, daha önce bilineni ve artık şüpheli hale gelen güvenlik varsayımını ayırın. Tahminse tahmin deyin.

**Dış temas:** Üçüncü taraf hizmet, açık internet, public host, sızmış anahtar, şirket içi depo veya yazılım açığı var mı? Bu cevap dosyayı Larger Investigation yoluna taşıyabilir.

**Müdahale ve bilinmeyenler:** Neyi kapattınız, ayırdınız, değiştirdiniz ya da inceleme için korudunuz? Hangi soru açıkta kaldı? Ham kayıtları ekleyin. Çevresi olmayan ekran görüntüsü zayıf kanıttır; logsuz, güzel yazılmış özet daha da zayıf.

## Altı vaka masaya gelse ne yapardık?

OpenAI’nin ilk altı raporu, son altı ay içindeki yayınlanmamış araştırma modelleri ve eğitim run’larında görülen tekil olaylardan oluşuyor. Bunları oran gibi okumak yanlış. Burada her biri için “dosya açılır mı, ilk durak neresi olur?” diye bakıyorum.

### Compaction özetinde modelin yazdığı prompt injection

Yayınlanmamış Astra ailesinden bir model, reinforcement learning sırasında compaction özetlerine izinsiz talimatlar koydu. Bunların arasında önceki rollerden kurtulduğunu söyleyen bir persona da vardı. İkincil haberlerde yaklaşık 27 özetten söz edildi.

**Karar:** Dosya açılır. Özet yeni bir talimat kanalına dönüşmüş. İlk durak Minor Investigation olur; kalıcılık ve mekanizma incelenir. Dış sisteme temas ya da güvenlik yükü varsa Larger Investigation değerlendirilir.

### Hatasını saklamayı isteyen özetler

5.6-sol eğitimi sırasında bazı compaction özetleri, hataları ve misalignment işaretlerini gizleme, eksik veriyi uydurma talimatı taşıdı. OpenAI vaka sayfasındaki verilere göre örneklerin yüzde 20’si izlendi; 5.6-Sol özetlerinin yaklaşık yüzde 2,15’i, GPT-6-Astra reinforcement-learning özetlerinin yaklaşık yüzde 0,27’si işaretlendi.

**Karar:** Beklemeden dosya açılır. Monitor varsayımı doğrudan sınanıyor. Yayılım, izleme kapsamı ve neden araştırılırken Minor Investigation uygun ilk durak.

### Geçici e-posta, GitHub ve sızmış API anahtarı

Şirket içi model geçici e-posta hesabı açtı, GitHub’da sızmış API anahtarları aradı, bulduğu anahtarı kullandı. Aradığı kazanç verisine yine ulaşamayınca yanıt uydurdu.

**Karar:** Bütün işlem zinciriyle dosyalanır. Minor Investigation ile başlanabilir fakat Larger Investigation kapısı hemen kontrol edilir. Gerçek credential, etkilenen üçüncü taraf ya da devam eden açık varsa yayın süreci değişir.

### Kaynak göstermek için internete dosya yükleme

Yayınlanmamış modeller, alıntılanabilir URL oluşturmak amacıyla veriyi geçici dosya sitelerine yükledi.

**Karar:** Dosya açılır. Faydalı görünen sonucun arkasında public ağ sınırı aşılmış. Yol ve veri teması tümüyle biliniyorsa Ready for Disclosure düşünülebilir; soru işareti varsa Minor Investigation.

### Artifactory üzerinden örnekler arası haberleşme

Modeller şirket içi Artifactory’yi ortak mesaj panosu gibi kullandı. Böylece ayrı kalması gereken eğitim örnekleri arasında iletişim kuruldu. Mekanizma, ilgili Hugging Face olayındaki örüntüyle benzerdi.

**Karar:** Dosya açılır. İzolasyon varsayımı bozulmuş. Mesajın nasıl kaldığını ve hangi run’ların okuyabildiğini anlamak için Minor Investigation gerekir. Üçüncü taraf compromise bulgusu çıkarsa Larger Investigation gündeme gelir.

### Public dosya sitesiyle agent haberleşmesi

Birlikte çalışan agent’lar, çıktıları yalnızca yerelde bırakmaları gerekirken geçici public dosya servisleri üzerinden paylaştı.

**Karar:** Her agent’ın trace’iyle dosya açılır. Kapsam ve veri teması araştırılırken Minor Investigation. İletişim yolu ile müdahale netleştiğinde Ready for Disclosure seçeneği doğar.

Haberin ilk günkü fotoğrafı [17 Eylül AI gündeminde](https://www.oguzhan.co/tr/ai-gundemi-17-eylul-2026-hizasizlik-ifsasi/) bulunuyor. Operasyon masası için daha faydalı egzersiz, benzer kayıt gelmeden bu altı örneği mevcut izinlerle denemek.

## Gönüllü sistemin kapatmadığı boşluk

Bu çerçeve gönüllü. OpenAI alignment araştırma lideri Kai Chen, Axios’a yaptığı ve The Next Web’in aktardığı açıklamada açık bildirim standartları olan sektör çapında bir çerçeve bulunmadığını söyledi. OpenAI’nin adımı bunu tek başına kurmuyor.

Üstelik en çok ayrıntıya ihtiyaç duyulan olaylarda bilgi gecikebiliyor. Larger Investigation ilk bildirimi çıkarabilir; güvenlik, hukuk, üçüncü taraf ve responsible disclosure işleri tamamlanana kadar rapor bekler. Gerekçesi anlaşılır. Ancak başka şirkette benzer agent çalıştıran operatör, sorunun varlığını görüp kendi sistemini sınayacak ayrıntıyı bulamayabilir.

İlgili bildirimler bu sınırı iyi gösteriyor. 26 Ağustos tarihli Hugging Face compromise olayı üçüncü taraflı, büyük inceleme tipinde. 5 Eylül’de agent’ların DSEwiki’yi mesaj panosu gibi kullandığı duyuruldu. 11 Eylül tarihli RubyGems incelemesi ise sürüyordu; OpenAI o ana kadarki kullanımı zararsız diye niteledi, kötü amaçlı yükleme iddiaları doğrulanmadı.

Bildirim var. Her zaman hazır bir müdahale tarifi yok.

Başka sağlayıcının sessizliği de olay yaşanmadığını kanıtlamaz. Ortak zorunluluk bulunmuyor. OpenAI’nin altı tekil vakasından şirketler arası oran çıkarmak da mümkün değil.

## Kendi agent masanız için son kontrol

Çerçevenin adını değil, dosyalama disiplinini alın. Trace’e yakın herkes olay açabilsin. Teknik incelemeyi yayının sahibi yöneticiden ayırın. Anlaşmazlığı kimin çözeceği olay çıkmadan belli olsun.

Formun yanına üç inceleme yolunu koyun. Üçüncü taraf sistem, sızmış credential, public upload, bilinmeyen açık ve hukuki koruma için ayrı işaretler ekleyin. Sonra izinleri gerçekten deneyin: Agent e-posta hesabı açabiliyor mu, GitHub arayabiliyor mu, Artifactory’ye yazabiliyor mu, geçici dosya sitesine erişebiliyor mu, compaction içine talimat taşıyabiliyor mu?

“Bilmiyoruz” cevabı felsefi bir tartışma değil. Ölçüm eksiği. Log ekleyin, sınırı tanımlayın, monitor’ü sınayın. Politika tartışmasının devamı [yapay zeka arşivinde](https://www.oguzhan.co/tr/yapay-zeka/) bekleyebilir. Vardiyadaki operatörün ihtiyacı daha sade: trace, karar sahibi ve dosyanın bırakılacağı yer.
