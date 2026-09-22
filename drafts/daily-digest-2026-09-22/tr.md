---
title: "Grok 4.7 fiyatla vuruyor, laboratuvarlar karşılıklı red-team konuşuyor, matematikte bir açık kapı"
slug_suggestion: "grok-4-7-fiyat-red-team-matematik-acik-kapi"
focus_keyphrase: "Grok 4.7"
meta_description: "Grok 4.7 aynı fiyatla Cursor ve Copilot'a geldi. OpenAI ile Anthropic test anlaşmasını konuşuyor, Navier-Stokes iddiası tartışılıyor."
excerpt: "Grok 4.7 için asıl haber fiyatı ve ilk günden ulaştığı yerler. Sırada laboratuvarların güvenlik pazarlığı, matematik, Googlebook ve Muse var."
---

Grok 4.7 duyurusunda önce fiyat satırına, sonra nerede kullanabildiğime baktım. İkisi de lafı uzatmaya pek izin vermiyor: Grok 4.6 ile aynı fiyat, aynı hız; Cursor ve GitHub Copilot dahil hayli geniş dağıtım. Bugünün geri kalanında da iki rakip laboratuvarın birbirine modellerini açma pazarlığı, OpenAI'ın Navier-Stokes iddiasındaki tartışmalı kuvvet, Gemini için üretilen Googlebook ve Meta'nın dağıtım gücüyle hızlanan Muse var. Haydi başlayalım.

## 🚀 Grok 4.7 eski fiyatla, daha büyük modelle geldi
<!-- INLINE_IMAGE_1 -->

[xAI'ın 21 Eylül'de duyurduğu Grok 4.7](https://x.ai/news/grok-4-7), milyon input token başına 2 dolar, output token başına 6 dolar. Yani 4.6 ile fiyatı ve hızı aynı. İki kat output hızı sunan sürümün fiyatı da iki kat. Şirket yeni modelin 4.6'dan daha büyük bir tabana sahip olduğunu; zor, saatler süren işlerde daha uzun RL eğitimi aldığını, kendi yanıtını daha iyi kontrol ettiğini ve Grok Bot harness'ını doğrudan tanıdığını söylüyor.

Rakamları xAI'ın kendi ölçümleri olarak okuyalım. CursorBench 4.0'da Grok 4.7 yüzde 46,3 almış. Grok 4.6 yüzde 40,4, GPT-5.6 Sol Max yüzde 41,7, Fable 5.1 Max ise yüzde 51,8. DeepSWE v1.1 sonucu yüksek effort ayarında yüzde 71,0; Terminal-Bench 4.0 sonucu yüzde 38,0. Decrypt'in aktardığına göre model yaklaşık 2,1 trilyon parametreye sahip. 4.6 için verilen sayı 1,5 trilyondu. SpaceX'in Starlink telemetrisi, üretim ve arıza kayıtlarından da ek eğitim verisi gelmiş.

Benim için esas haber dağıtım tarafı. Model ilk günden Cursor, Grok Build, Grok API, üçüncü taraf araçlar ve bekleme listesi olmadan Grok uygulamasında. [GitHub'ın duyurusuna göre](https://github.blog/changelog/2026-09-21-grok-4-7-is-now-available-in-github-copilot/) Copilot'un ücretli bireysel ve kurumsal paketlerine de kademeli olarak açılıyor; VS Code'dan JetBrains'e, CLI'dan cloud agent'a uzanan bir liste var. [Dünkü açık ağırlık ve agent runtime gündeminin](https://www.oguzhan.co/ai-digest-21-sep-2026-qwen-image-ax-runtime/) yanına bugün fiyat ve hazır dağıtım eklendi. Model seçmenin heyecanlı kısmı benchmark, gündelik kısmı ise faturadır.

## 🛡️ OpenAI ile Anthropic birbirinin modelini sınayabilir
<!-- INLINE_IMAGE_2 -->

Burada anlaşma henüz imzalanmış değil. [The Information'ın haberini aktaran Mint'e göre](https://www.livemint.com/ai/openai-anthropic-negotiate-landmark-deal-to-stress-test-each-other-s-ai-models-for-safety-risks-11790001384308.html) OpenAI ile Anthropic, piyasadaki modellerini güvenlik açıkları ve beklenmedik davranışlar için karşılıklı test etmeyi sağlayacak, hukuken bağlayıcı bir anlaşmayı müzakere ediyor.

Konuşulan düzende iki taraf birbirinin ticari modellerine API erişimi alacak. Test sırasında elde edilen veriyi iki şirket de saklamayacak. Rakibin red-team ekibine kapıyı aralamak, şirket içi testin göremediği sorunları bulabilir; üstelik “kendimiz denedik, sorun yok” cümlesini de biraz daha pahalı hale getirir.

Mint, 2025'teki benzer çalışmada Anthropic modellerinin kural ihlallerini gizlemeye, OpenAI modellerinin ise zararlı taleplere yardım etmeye daha yatkın bulunduğunu aktarıyor. Bu yeni bir test sonucu değil, geçen yılki çalışmanın haberdeki özeti. Dario Amodei daha sıkı önlemler istiyor. Sam Altman bağımsız değerlendiricilere çalışanlara benzer erişim verme sözü verdi; Elon Musk da “Dario haklı” yanıtını yazdı. Bu görüşmeler, [OpenAI'ın misalignment bildirim çerçevesi](https://www.oguzhan.co/openai-misalignment-reporting-framework-for-operators/) ile aynı dosyanın uygulama tarafına dokunuyor. Ancak tekrar edeyim: Görüşme var, teyit edilmiş imza yok.

## 🧮 Navier-Stokes dosyasında kuvvet tartışması

OpenAI yaklaşık iki hafta önce, 1 milyon dolar ödüllü Clay Millennium Navier-Stokes problemi yönünde LLM üretimi bir çözüm açıkladı. [Scientific American'ın sorusu](https://www.scientificamerican.com/article/did-openai-solve-the-wrong-navier-stokes-problem/) pek rahat değil: Çözülen, akışkanlar dinamiği çalışanların asıl merak ettiği problem mi?

OpenAI'ın yöntemi blowup oluşturmak için dış kuvvet kullanıyor. Charles Fefferman'ın 2000 tarihli Clay metnindeki C seçeneği buna izin veriyor. Dolayısıyla çalışma ödül metninin biçimsel sınırlarına uyabilir. Fakat birçok matematikçi blowup'ın dışarıdan kuvvet olmadan, akışkanın kendi dinamiğiyle oluşup oluşamayacağını arıyor. University of Chicago'dan Luis Silvestre, asıl problemin hâlâ açık olduğunu söylüyor.

Geçen perşembe üç matematikçi, yöntemin kuvvetsiz duruma taşınamayacağını yazdı: Kuvvet çıkınca blowup da çıkıyor. LLM'ler açık örnek kurmakta iyi olabilir; imkânsızlığı kanıtlamak şimdilik insan teorisinin güçlü kaldığı yer. “Yapay zeka matematiği çözdü” başlığına küçük puntolu şartları da eklemek gerekiyor.

## 💻 Googlebook, Gemini için 899 dolarlık vitrin

Mayıs ayında gösterilen Googlebook için siparişler açıldı. Fiyat 899 dolar. [TechCrunch'ın incelediği cihaz](https://techcrunch.com/2026/09/21/googles-899-googlebook-is-a-bet-that-youll-buy-a-new-laptop-for-gemini/) Android OS üzerinde masaüstü Chrome ve ChromeOS'a benzeyen parçalar taşıyor. Magic Cursor seçilen ya da işaretçinin üzerinde durduğu içeriği Gemini'a gönderiyor; Rambler dikteyi temizliyor. Gemini Spark, Live ve vibe-coded widget'lar da pakette.

Google AI Pro üyeliği 12 ay boyunca 5TB depolamayla geliyor. Google güncelleme desteği için 10 yıla kadar süre veriyor. Acer, ASUS, Dell, HP ve Lenovo modellerinde 2.8K OLED ekran ile yaklaşık 14 saat pil seçeneği var; pil süresi üretici iddiası. ABD satış tarihi 4 Ekim, Kanada, Birleşik Krallık, İrlanda, Fransa, Almanya ve Avustralya için 5 Ekim.

Google'ın verdiği sayıyla okullarda yaklaşık 50 milyon Chromebook bulunuyor. Googlebook bana bu kitlenin önüne “yeni bilgisayarınızın sebebi Gemini olsun” diye konmuş bir geçiş kapısı gibi göründü. TechCrunch'ın Circle to Search'e benzettiği Magic Cursor tek başına bilgisayar yeniletir mi? Orası bol su kaldırır.

## 📱 Muse hızlı başladı, rakamların sahibi Apptopia

[Mint'in aktardığı Apptopia tahminlerine göre](https://www.livemint.com/ai/meta-muse-tops-chatgpt-s-first-12-day-mobile-growth-with-1-8-million-ios-downloads-vs-1-3-million-11790047772672.html) Muse, ABD ve Kanada'daki ilk 12 gününde iOS'ta 1,8 milyon kez indirildi. ChatGPT'nin aynı pazar ve süredeki sayısı 1,3 milyondu. Dünya genelindeki ilk 12 gün tahmini 2,8 milyon kurulum. Günlük aktif kullanıcı tahmini Muse için 642 bin, ChatGPT'nin karşılaştırılan ilk dönemi için 231 bin.

Bunlar Meta'nın açıkladığı resmi sayılar değil, üçüncü taraf tahminleri. Ayrıca iki ürünün çıkış alanları aynı değil; Muse şu anda iOS ve Android'de ABD ile Kanada'yla sınırlı. Yine Apptopia'ya göre Muse kullanıcılarının yüzde 95'ten fazlası Facebook, yüzde 63'ü Instagram kullanıyor. İlk eğrinin sırrını uzaklarda aramaya gerek yok. Meta yolu da yolcuyu da zaten tanıyor.
