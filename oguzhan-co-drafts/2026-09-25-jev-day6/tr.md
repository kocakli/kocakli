---
title: "Jev Gerçek Zamanlı Döngülerde: Doom, Wikiracing ve Tarayıcı Ajanları Piksel Olmadan"
slug: "jev-gercek-zamanli-doom-wikiracing-tarayici"
yoast_title: "Jev Gerçek Zamanlı Demolar: Doom, Wikiracing ve Tarayıcı Döngüleri | TypeSafe"
yoast_metadesc: "TypeSafe'in Doom ve Wikiracing demoları Jev'i oyun hızında çalıştırıyor. Tarayıcı ve mobil araçlar aynı deseni takip ediyor: yapılandırılmış durum, piksel değil."
focus_keyphrase: "Jev real-time"
---

## Jev Döngü Hızında: Yapılandırılmış Durum, Piksel Değil

TypeSafe'in [Jev lansmanı](https://typesafe.ai/blog/introducing-system-one-models-and-jev) bir karar modelini saniyede 10 sorgu hızına soktu. Doom oyunu ~10 qps ile dönüyor, Wikiracing her adımda yüzlerce Wikipedia bağlantısını tarayıp seçiyor, tarayıcı ajanları DOM hedeflerini sekiz saniyenin altında işaretliyor. İşin sırrı yapılandırılmış metin girişi; ekran görüntüsü veya piksel tanıma yok. Doom'da oyun durumu satır satır gelir: can, mermi, konum, yapılabilecek hareketler. Wikiracing'de sayfadaki bağlantı listeleri. Tarayıcı araçlarında A11Y ağacı veya indekslenmiş DOM tablosu. Her döngü bir [Choice çağrısıyla](https://www.oguzhan.co/tr/jev-primitives-choice-score-noul-karar/) bitiyor ve milisaniyeler içinde yanıt dönüyor.

Gösterişli mi? Kesinlikle. En iyi oyuncu mu? Hayır. [TypeSafe ekibi açıkça söylüyor](https://typesafe.ai/blog/introducing-system-one-models-and-jev): AI olmayan bir Doom botu kendi ajanlarından daha iyi oynar. Amaç döngü hızında reaktif talimat takibi. Hız sınırları ve Choice'ın 255 seçenek tavanı gerçek tasarımları şekillendiriyor. Topluluk tarayıcı ve mobil projeleri de aynı kısıtları taşıyor.

## Doom: Metin Durumu, Saatte ~$7 Maliyet

TypeSafe'in Doom ajanı Jev'e saniyede yaklaşık 10 kez soruyor. Oyun durumu yapılandırılmış metin olarak geliyor: oyuncu konumu, yakındaki düşmanlar, can, mermi, dört yönlü hareket, ateş, yatay kaçış. Model bir aksiyon seçiyor, döngü tekrarlıyor. Erken erişim fiyatlaması milyon girdi token başına ~$0.042; çıktı ücretsiz. Sürekli oyun saatte kabaca $7 tutuyor.

<!-- INLINE_IMAGE_1 -->

Ekip bunu zaman baskısı altında talimat takibi olarak çerçeveliyor, optimal oyun değil. Elle kodlanmış bir pathfinding botu odaları daha hızlı temizler. Ama Jev sorgu başına 70–500 milisaniye arasında yanıt veriyor ([Gün 3'ün hız makalesi](https://www.oguzhan.co/tr/jev-hiz-maliyet-paralel-ornekleyici/) detayları kapsıyor), insan izleyici açısından yeterince reaktif hissettiriyor. Mimari basit: yapılandırılmış durumu gözlemle, tiplenmiş bir soru sor (Choice), harekete geç. Piksel kod çözme yok, OCR gecikmesi yok.

Hız matematiği önemli. Erken erişim sınırları saniyede ~250.000 token işleme ve dakikada 1.200 istek (saniyede 20). Bir 10 Hz ajan rpm bütçesinin yarısını kullanıyor. Birden fazla ajan veya eşzamanlı istek hemen tavana çarpıyor. Bu kısıt gerçek tasarımları host tarafı timeout'lara ve Jev geç kaldığında yedek aksiyonlara itiyor.

## Wikiracing ve Choice-255 Tavanı

Wikiracing yüksek kardinaliteli kararlar için daha temiz bir stres testi. Başlangıç makalesi, hedef makale, sadece sayfadaki bağlantılar izin veriliyor. Her adım yüzlerce hatta binlerce Wikipedia çapasını sunabiliyor. Oyun Choice'ı URL icat etmeden veya serbest tahmin yapmadan ölçekte gösteriyor.

Sorun şu: [Choice maksimum 255 seçeneği destekliyor](https://www.oguzhan.co/tr/jev-primitives-choice-score-noul-karar/). Bunun üstünde iki aşamalı bir desen lazım. Önce Score veya kısaltma listesiyle bağımsız filtreleme (48 veya 60 güçlü adaya kadar), sonra alt küme üzerinde Choice. TypeSafe kısaltma adımı çalıştığında ara sıra yavaşlama kaydediyor. [jev-agent.com/wikirace](https://jev-agent.com/wikirace) gibi topluluk uygulamaları filtrelemeden sonra adım başına ~48 bağlantı bildiriyor, Choice'ı tavanın altında tutuyor.

Ders Wikipedia'nın ötesine geçer. Tarayıcı DOM ağaçları, uygulama menüleri, otomatik tamamlama açılır listeleri hepsi 255 seçeneği taşırıyor. İki aşamalı desen standart oluyor: en üst katmana budama, sonra karar.

<!-- INLINE_IMAGE_2 -->

## Tarayıcı ve Mobil Araçlar: DOM Tabloları, Ekran Görüntüsü Yok

Topluluk tarayıcı ajanları aynı yapılandırılmış durum stratejisini takip etti. [jev-ultrafast](https://github.com/cobanov/awesome-jev) DOM'u bir aksiyon alanına indeksliyor: tıklanabilir öğeler, metin alanları, gezinme hedefleri. Bir Jev isteği operasyon ve hedefi seçiyor (12 numaralı düğmeye tıkla, aşağı kaydır, sekmeye git). TYPE_TEXT aksiyonları Jev yerine küçük bir LLM'e gidiyor. Yazar Zürih'ten Londra'ya uçuş aramalarını rezervasyon ekranına kadar ~7.1 saniyede bildiriyor.

[jev-browser-use](https://awesomejev.vercel.app/c/browser-and-computer-use/) döngüyü farklı böldü. Jev gezinme, tıklama ve kaydırmayı hallediyor. Codex skill yazma ve doğrulama mantığını tutuyor. Hibrit saf üretken yaklaşımlara göre tarayıcı adımlarında ~5–10× hız iddia ediyor, tam kıyaslamalar göreve göre değişiyor.

Mobil Android A11Y ağacını takip ediyor, ekran görüntüsü yok. [mobile-jev](https://github.com/cobanov/awesome-jev) ve xinwang-nwpu'nun jev-mobile gibi benzerleri A11Y hiyerarşisini tabloya serileştiriyor: düğmeler, metin alanları, kaydırma kapları. Bir istek aksiyon ve öğeyi seçiyor. Yazar dokuz Uber aksiyonunu ~21 saniyede (mobile-jev) ve bir Bilibili görevini ~18 saniyede (jev-mobile) bildiriyor. Bunları yazar tarafından bildirilen zamanlama olarak değerlendirin; çoğaltma cihaza, ağa ve hız sınırlarına bağlı.

Diğer araçlar deseni özel bağlamlara uyguluyor. jkudish/jev-browser Playwright'i MCP sunucusuyla sarıyor. imanshu03'ün jev-browser-use Chrome DevTools Protocol üstüne güven kapısı ekliyor. typesafe-computer-use (jev-use olarak da biliniyor) macOS A11Y API'lerini hedefliyor, yine piksel kullanmadan. Ortak iplik: arayüz durumunu yapılandırılmış bir soruya serileştir, Jev'den tiplenmiş karar iste, çalıştır.

## Demolar En İyi Oyuncu Değil

Gerçek zamanlı Jev durum serileştirme artı döngüdeki tiplenmiş sorular demek. Model hızlı yanıt veriyor. Host kodu timeout'ları, yanıt geç kaldığında varsayılanları ve kardinalite 255'i taşınca kısaltma listelerini sahipleniyor.

Bu mimari çarpıcı demolar üretiyor. Doom oyunu akıcı görünüyor. Wikiracing bulmacaları saniyeler içinde çözüyor. Tarayıcı ajanları insanın tıklayabileceğinden hızlı uçuş rezervasyonu yapıyor. Ama bu demoların hiçbiri sınıfının en iyisi performansı optimize etmiyor. Bir Doom speedrunner veya arama sezgiseli kazanır. Takas döngü hızında talimat takibi: hedefinizi anlatıyorsunuz, ajan reaksiyon gösteriyor, döngü sıkı kalıyor.

Hız sınırları ve maliyet gerçek dağıtımları çerçeveliyor. Doom için saatte $7 demo için sürdürülebilir, 7/24 hizmet için pahalı. Dakikada 1.200 istek bir avuç eşzamanlı ajanı destekler, bin tanesini değil. Üretim tasarımları Jev'in etrafında host mantığını katmanlıyor: kısaltma listeleri, önbellekleme, yedek sezgiseller, daha küçük modellere kısmi araç çağrıları. Karar modeli hızlı kalıyor; iskele bütçe yakmadan veya sınırlara çarpmadan ilerlemesini sağlıyor.

Tarayıcı ve mobil araçlar desenin oyunların ötesine ölçeklendiğini kanıtlıyor. DOM ve A11Y ağaçları sadece başka yapılandırılmış durum. Jev'in hızı ve tiplenmiş çıktıları ortamın kendini serileştirebileceği ve 255 seçeneğin çoğu kararı kapsadığı her döngüye oturuyor. Kapsamadığında iki aşamalı Score-sonra-Choice boşluğu dolduruyor.

Gün 6'nın dersi bu. Gerçek zamanlı Jev çalışıyor çünkü ortam zor serileştirmeyi yapıyor, model tiplenmiş menüden seçiyor ve host uç durumları hallediyor. Piksel isteğe bağlı.
