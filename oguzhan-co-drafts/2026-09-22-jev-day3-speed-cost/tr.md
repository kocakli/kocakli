---
title: Jev hızı ve maliyeti: 70–500ms karar, token akışı yok
slug: jev-hiz-maliyet-paralel-ornekleyici
yoast_title: Jev hız: 70–500ms System One kararlar | oguzhan.co
yoast_metadesc: TypeSafe Jev 70–500ms uçtan uca gecikme ve $0.042/MTok girdi ücreti ile geliyor. Paralel örnekleme ve soru demetleme, Pareto gerçekliğiyle.
focus_keyphrase: Jev hız
lang: tr
word_count_target: 800-1200
---

TypeSafe [Jev](https://www.oguzhan.co/tr/typesafe-jev-system-one-karar-modeli/) bir System One kararını 70–500 milisaniyede veriyor. TypeSafe'in lansmanında açıkladığı gecikme aralığı bu, genellikle ABD Batı Kıyısı sunucularından ölçülmüş. Aynı System One sorularına frontier LLM'ler 3 ila 329 saniye harcıyor. [The Register'ın yan yana demosu](https://www.theregister.com/ai-and-ml/2026/09/16/typesafe-ai-debuts-model-for-machines-that-plays-doom/5296711) Jev'i ~0.114 saniyede, GPT-5.6 Terra'yı ~8.566 saniyede çalışırken göstermiş. Aynı karar için.

Bu bir kıyaslama hilesi değil. Mimari fark.

## ⚡ Paralel örnekleme: bir sorgu, çok cevap

Jev hızının kaynağı örnekleyici. LLM'ler token'ları sırayla üretiyor, her token bir sonrakini bekliyor. Bir soru soruyorsunuz, bir string alıyorsunuz, model o string'i karakter karakter inşa ederek zaman harcıyor.

Jev string üretmiyor. Bütün soruları tek bir forward pass'te değerlendiriyor. Durum ve tipli sorular (Choice, Score, Noul) gönderdiğinizde Jev her cevap adayı için olasılıkları paralel hesaplıyor. İsteğinize on soru daha eklediğinizde yanıt süresi neredeyse değişmiyor. [TypeSafe dökümanları](https://docs.typesafe.ai/) açık: "Her soru paralel değerlendiriliyor… Soru eklemek yanıt süresini neredeyse değiştirmiyor."

Bu temel bir ayrım. Otoregresif token üretimi artık hızlı, ama yine de sıralı. Paralel örnekleme tasarımdan eşzamanlı. Tüketiciniz açıklamalar akıtan bir sohbet arayüzü değil de çalışma zamanında karar veren kod olduğunda, bu eşzamanlılık gecikme bütçeniz oluyor.

Trafik yönlendiriyorsanız, cache anahtarı seçiyorsanız, ya da şüpheli bir isteği tırmandırmaya karar veriyorsanız, size bir paragraf gerekmiyor. Choice A ya da Choice B gerekiyor. Jev size o seçimi bir olasılık ve [güven aralığıyla](https://www.oguzhan.co/tr/jev-confidence-rlcd-kalibre-suphe/) veriyor, hem de onlarca ya da yüzlerce milisaniyede.

## 💵 Fiyat kartı: milyon token başına $0.042 girdi, çıktı ücretsiz

TypeSafe Jev'i **milyon girdi token'ı başına $0.042** fiyatla listeliyor. Çıktı **ücretsiz**. [OpenRouter'ın Jev-1.13 sayfası](https://openrouter.ai/typesafe/jev-1.13) aynı fiyatı yansıtıyor: 1M başına $0.042 / $0. [Vercel AI Gateway](https://vercel.com/changelog/typesafe-ai-jev-now-available-on-ai-gateway) da milyon girdi başına $0.042 listeliyor, Gateway üzerinde 25 Eylül 2026'ya kadar süreli bir promosyonla ücretsiz.

Gönderdiğiniz için ödüyorsunuz. Durum token'ları, soru metni. Cevaplar saymayacak kadar ucuz.

Frontier LLM'lerle kıyaslayalım. Girdi fiyatları genellikle milyon token başına $0.20'den başlıyor, en büyük modellerde $10 ve üzerine çıkıyor. Çıktı kabaca girdinin beş katı. Paragraflar dolusu akıl yürütme ürettiğinizde o çıktı token'ları birikim yapıyor. Tipli kararlar ürettiğinizde var olmuyorlar.

TypeSafe sürdürülebilirlik konusunda açık. Fiyatın sübvanse olmadığını henüz kanıtlayamıyorlar. Beklentileri: fiyatlar zamanla düşecek, yükselmeyecek. Ama yayınlanan liste fiyatı milyon girdi token'ı başına $0.042, bugün buna göre planlayabilirsiniz.

Bağlam için: System One iş akışınız günde 10 milyon girdi token'ı Jev üzerinden işliyorsa, $420 edecek. Aynı iş akışı üst düzey bir LLM sarmalayıcısından, hem girdi hem çıktıya 10× ila 100× fiyatla faturalandırıldığında, binlerce ya da on binlerce dolara mal olacak.

## 📦 Demetleme: çok soruyu bir kez sorun

Paralel değerlendirmenin pratik bir maliyet kolu var. Durum istek başına bir kez alınıyor. Birçok bağımsız soru o durumu paylaşabiliyor.

TypeSafe'in yemek kitabı tarzı testleri aynı durum üzerinde yaklaşık 13 soruyu demetlemiş. Ayrı sıralı çağrılar her soru için durumu yeniden faturalandıracaktı. Demetlenmiş yaklaşım kabaca **11.5–12.2× daha ucuz** ve **9.6–10× daha hızlı** çıkmış ayrı çağrılara kıyasla. Bu rakamlar TypeSafe'in yayınladığı özetlerde hafifçe değişiyor, ama büyüklük mertebesi tutuyor.

İki uyarı. Birincisi, istemciniz istekleri paralel ateşleyebiliyorsa eşzamanlı çağrılar gecikme farkını küçültebilir. Maliyet farkını küçültmezler. Hala durumu her seferinde yeniden faturalıyorsunuz. İkincisi, ~11× / ~10× yemek kitabı sayıları TypeSafe kaynaklı. Kendi iş akışlarınızda bunu yeniden üretmeden bütçe kurmayın.

Durumunuz birkaç kilobaytlık bağlam ve tek soru soruyorsanız, demetleme ibre oynatmayacak. Durumunuz 20.000 token'lık bir döküman ve onunla ilgili on karar sorusu soruyorsanız, tasarruflar hızla birikiyor.

Demetleme sihirli çarpan değil. Problem şekliniz uyduğunda yapısal bir avantaj: paylaşılan bağlam, çok bağımsız karar.

## 📉 Pareto gerçekliği: 193.6× ve 444.6× tavan iddiaları

TypeSafe'in ana sayfası ve iş akışı değerlendirmeleri LLM System One sarmalayıcılarına karşı **193.6× daha hızlı** ve **444.6× daha ucuz** diyor. Bu sayılar TypeSafe'in kendi yetenek ekibinin frontier modellerin (Astra ve Fable ortalaması) etrafındaki yapılandırılmış sarmalayıcılara karşı Jev üzerinde koşturduğu iş akışlarından geliyor.

Lansmanı yazısı bu sonuçların gerçek dünya kazançlarının **üst ucu** olduğunu söylüyor. Neden? İş akışlarını Jev'in güçlü yönlerini bilen TypeSafe mühendisleri tasarlamış. Referans modeller yapılandırılmış çıktı sarmalayıcılarından zorlanmış, bu da ek yük ekliyor. Ve temel, yığını kontrol ediyor olsaydınız seçebileceğiniz en hızlı ya da en ucuz seçenek değil, büyük harici modellerin ortalaması.

Bunlar geçerli iş akışı değerlendirmeleri. Garanti değiller. Kilometreniz sorunun karmaşıklığına, durum boyutuna, bölgenizden ağ gecikmesine ve probleminizin Choice / Score / Noul ilkelerine ne kadar iyi eşlendiğine bağlı olarak değişecek.

Register demosu tek bir anlık görüntü: bir soru, bir durum, bir ağ yolu. GPT-5.6 Terra'ya karşı ~75× hız avantajı göstermiş. OpenRouter pazar yeri verileri Jev'in P50 gecikmesini ~0.26 saniye civarında listeliyor, ama bu bir sağlayıcı anlık görüntüsü, TypeSafe SLA'sı değil.

Jev'i değerlendiriyorsanız, kendiniz ölçün. 193.6× ve 444.6× tavan iddiaları TypeSafe'in kendi iş akışlarında ideal koşullarda neyin mümkün olduğunu anlatıyor. Üretim tavanınız yığınınıza, durum boyutunuza ve gecikme toleransınıza bağlı olacak.

Dürüst Pareto çerçevesi: Jev, System One iş yüklerinde LLM sarmalayıcılarından daha hızlı ve daha ucuz, çoğu zaman dramatik şekilde. Kesin katlar kurulumunuza bağlı. Kullanıcılarınıza UI SLA'ları vaat etmeden önce test edin.

## System One yönlendirme için ne anlama geliyor

Hız ve maliyet karar sınırını sıkıştırıyor. Bir System One sorgusu milyon girdi token'ı başına $0.042'ye mal olup 70–500 milisaniyede dönüyorsa, daha yavaş, daha pahalı bir modele tırmandırmadan önce daha çok trafiği buradan geçirebilirsiniz.

[2. Gün güven aralıklarını ve RLCD eğitimini anlattı](https://www.oguzhan.co/tr/jev-confidence-rlcd-kalibre-suphe/). Jev geniş belirsizlikle bir Choice döndürdüğünde, tırmandırıyorsunuz. Dar bir güven aralığıyla döndürdüğünde, hareket ediyorsunuz. Hız ve maliyet rakamları bu tırmanma hiyerarşisini ölçekte pratik kılıyor.

Sırada: 4. Gün agentları ve korkulukları kapsayacak. System One kararlarının çok adımlı iş akışlarına nasıl oturduğunu ve Jev'in diğer araçlara nerede devrettiğini. [Jev merkezinde](https://www.oguzhan.co/tr/typesafe-jev-system-one-karar-modeli/) devamı.
