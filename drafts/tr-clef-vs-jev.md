---
title: "Cloudflare Clef ve TypeSafe Jev: aynı API, farklı tercihler"
slug: clef-ve-jev-karar-modelleri-karsilastirma
lang: tr
polylang_pair: drafts/en-clef-vs-jev.md
status: draft (yayımlanmayacak)
format: B deep dive
hub: https://www.oguzhan.co/tr/yapay-zeka/
focus_keyphrase: "Clef ve Jev"
yoast_seo_title: "Clef ve Jev karşılaştırması: fiyat, latency ve testler"
yoast_meta_description: "Clef ve Jev karşılaştırması: Cloudflare'in open-weight decision model'leri ile TypeSafe Jev 1.13; fiyat, latency iddiaları, küçük testler ve bağımlılık."
excerpt: "Cloudflare'in Clef ve Clef-flash modelleri Jev'in API'sini konuşuyor ve ağırlıkları açık. Üreticiler ne diyor, küçük bağımsız testler ne buldu, hangisi nerede işe yarar?"
featured_image: clef-vs-jev-decision-models-cover.webp
---

[[IMAGE: cover | clef-vs-jev-decision-models-cover.webp; alt: Yan yana iki karar makinesi: biri kapalı siyah kutu, diğeri dişlileri görünen cam kasa, ikisine de aynı kartlar giriyor | Aynı girdi, iki farklı yol: biri kapalı ve barındırılan bir API, diğeri indirip kendi sunucunuzda çalıştırabileceğiniz açık ağırlıklar.]]

TypeSafe'in Jev'i çıkalı iki hafta olmuştu ki rakibi geldi. Cloudflare 1 Ekim 2026'da Clef ve Clef-flash adında iki decision model yayımladı ve bunları açıkça Jev'in karşısına koydu. Clef ve Jev aynı işi yapıyor: serbest metin yazmıyor, tipli sorulara her olası cevap için bir olasılık döndürüyor. [Cloudflare'in duyurusuna göre](https://blog.cloudflare.com/clef-decision-models/) yeni modeller Jev'in System One API'siyle tamamen uyumlu, üstelik ağırlıkları açık.

Baştan bir not: Jev bu blogda en sık yazdığım konulardan (eski yazılar [yapay zeka sayfasında](https://www.oguzhan.co/tr/yapay-zeka/)), yorumlarımı bu bilgiyle okuyun. İki modeli de çalıştırmadım; her rakam ya üreticinin sayfasından ya da bağlantısını verdiğim küçük testlerden.

## Cloudflare'in çıkardığı iki model

[Cloudflare bloguna](https://blog.cloudflare.com/clef-decision-models/) ve [Hugging Face kartına](https://huggingface.co/Cloudflare/clef) göre büyüğü Clef 27B, dondurulmuş Qwen3.8-27B üzerine eğitilmiş. Küçüğü Clef-flash 9B, tabanı Qwen3.5-9B. [Changelog'daki](https://developers.cloudflare.com/changelog/post/2026-10-01-clef-workers-ai/) ifadeyle bunlar Workers AI ekibinin eğittiği ilk modeller.

Model bir `state` ve en fazla 64 tipli soru okuyor: evet/hayır için `noul`, seçeneklerden biri için `choice`, sıralı puanlama için `score`. Karşılığında her izinli cevaba bir olasılık geliyor, düzyazı yok. Workers AI, REST ya da AI Gateway ile çağrılıyor; OpenRouter'da da listelenmiş.

## İki model nasıl çalışıyor

[[IMAGE: inline-1 | decision-model-state-questions-diagram.webp; alt: Şema: state ile choice, score ve noul soruları decision model'e giriyor, her soru için olasılık çubukları çıkıyor | İki model de aynı isteği okuyor: bir state, tipli sorular ve her olası cevap için bir olasılık.]]

İstek formatı aynı; arkasını ise yalnızca bir taraf anlatıyor.

Cloudflare'in anlatımına göre Clef'te Qwen backbone'u tek bir prefill geçişi yapıyor, küçük bir "joint schema head" de bütün geçerli seçenekleri paralel puanlıyor. Eğitimde ikincil hedef olarak "Reinforcement Learning for Calibrated Decisions (RLCD)" var. İsim tanıdık gelebilir: [TypeSafe'in lansman yazısı](https://typesafe.ai/blog/introducing-system-one-models-and-jev) Jev'in eğitim yöntemine de aynı adı veriyor.

Jev'in mimarisi ise sır; [The Register'ın](https://www.theregister.com/ai-and-ml/2026/10/01/cloudflare-tries-to-outplay-jev-with-open-weight-clef-models/5300649) deyişiyle "TypeSafe has kept that a secret." TypeSafe, Jev için "can't hallucinate" diyor ama kastettiği dar: çıktı şeması garanti, tip hatası çıkmıyor.

Asıl fark girdide. [TypeSafe'in dokümanlarına](https://docs.typesafe.ai/models) göre Jev yalnızca metin alıyor. Clef'te vision encoder var ve [Workers AI model sayfası](https://developers.cloudflare.com/workers-ai/models/clef/) istek başına 4 görsele izin veriyor. Hugging Face kartı videoyu da sayıyor ama Workers AI parametre listesinde yalnızca görsel geçiyor; videoyu şimdilik açık ağırlıkların özelliği diye not ediyorum.

İkisinin context penceresi 64K. TypeSafe İngilizce dışındaki diller için "handled but not equally well" diyor. Türkçe metinle çalışacaklar bu satırı atlamasın. Clef için kaynaklarda benzer bir bilgi yok.

## Açık ağırlık, kapalı kutu

[[IMAGE: inline-2 | hosted-vs-self-hosted-fork.webp; alt: Devre yolu ikiye ayrılıyor: bir kol kilitli bulut binasına, diğeri açık kilitli küçük bir sunucuya gidiyor | Jev'e yalnızca barındırılan API üzerinden ulaşılıyor. Clef ise Workers AI'da ya da kendi GPU'nuzda çalışıyor; 27B model için yaklaşık 85 GB VRAM gerekiyor.]]

Jev kapalı. TypeSafe'in dokümanlarına göre her hesap aynı ağırlıkları kullanıyor, müşteri verisiyle fine-tune ya da LoRA yapılmıyor. Servis "şimdilik" ABD Batı Kıyısı'nda; OpenRouter, Vercel AI Gateway ve Workers AI üzerinden de ulaşılıyor (bu yolları [Jev ekosistemi yazısında](https://www.oguzhan.co/tr/jev-ekosistem-openrouter-vercel-cloudflare/) anlatmıştım). Kurumsal müşterilere zero data retention var.

Clef'in ağırlıkları Apache-2.0 lisansıyla Hugging Face'te, eğitim verisi ise ortada yok. Cloudflare'den Michelle Chen bunu The Register'a doğruladı. [Hacker News'teki](https://news.ycombinator.com/item?id=49923692) başlık da "Open weights, not open source." gibi itirazlardan sonra "open-weight" olarak değişti.

Self-host mümkün ama ağır: Chen'e göre Clef-flash en az 41 GB, Clef 85 GB VRAM istiyor, hem de tek eşzamanlı istekte. Cloudflare ayrıca RL fine-tuning servisi açıyor; önce kendi mühendisleri ve design partner'larla elden, ileride self-serve. Jev'de bunun karşılığı yok.

Benim okumam şu: Jev'de tek bir şirketin API'sine bağlısınız. Clef'te de Cloudflare'e bağlanabilirsiniz, ama ağırlıkları alıp gitme seçeneği elinizde kalıyor.

## Clef ve Jev ne kadar tutuyor?

[Workers AI fiyat sayfasında](https://developers.cloudflare.com/workers-ai/platform/pricing/) Clef milyon input token başına 0,24 dolar, Clef-flash 0,09 dolar; output için fiyat yazmıyor. TypeSafe'in dokümanlarında Jev 0,042 dolar, output ücretsiz. The Register'a göre fark "nearly six times", yani altı kata yakın. Clef-flash ise liste fiyatında Jev'in iki katını biraz aşıyor.

Bağımsız testlerin karar başı maliyeti de aynı yönü gösteriyor. [Startrise](https://www.startrise.io/blog/jev-vs-clef/) milyon karar için Clef'te yaklaşık 63, Jev'de yaklaşık 17 dolar hesapladı. [Construct'ın](https://construct.computer/blog/clef-vs-jev-benchmark/) rakamları Jev için 23, Clef-flash için 35, Clef için 93 dolar.

Jev tarafına da bir not: TypeSafe, fiyatın sübvansiyonlu olmadığını kanıtlayamayacağını lansman yazısında kendisi söylüyor. Rate limit'ler de sabit değil; saniyede 100K token ve 80 istek, haber vermeden değişebiliyor. Hız ve maliyet hesabını [şu yazıda](https://www.oguzhan.co/tr/jev-hiz-maliyet-paralel-ornekleyici/) ayrıntılı anlatmıştım.

## Yan yana bakınca

| | TypeSafe Jev 1.13 | Cloudflare Clef | Cloudflare Clef-flash |
|---|---|---|---|
| Çıkış | 15 Eylül 2026 (early access) | 1 Ekim 2026 | 1 Ekim 2026 |
| Ağırlıklar | Kapalı | Açık, Apache-2.0 | Açık, Apache-2.0 |
| Boyut / taban | Açıklanmadı | 27B, Qwen3.8-27B | 9B, Qwen3.5-9B |
| API | System One | System One uyumlu (Cloudflare'e göre) | Aynı |
| Girdi | Yalnızca metin | Metin, JSON, en fazla 4 görsel | Aynı |
| Context | 64k (state ve en uzun soru için 32k) | 64K | 64K |
| Milyon input token | 0,042 $ | 0,24 $ | 0,09 $ |
| Output token | Ücretsiz | Ücret listelenmemiş | Ücret listelenmemiş |
| Barındırma | TypeSafe API, OpenRouter, Vercel, Workers AI | Workers AI, OpenRouter, self-host (~85 GB VRAM) | Workers AI, OpenRouter, self-host (~41 GB VRAM) |
| Fine-tuning | Yok | RL fine-tuning (design partner'lar) | Aynı |
| Üreticinin latency iddiası | 70-500 ms (TypeSafe) | 209,3 ms medyan (Cloudflare) | 38,8 ms medyan (Cloudflare) |

Son satıra dikkat, nedeni aşağıda.

## Cloudflare'in rakamları, bağımsız testlerin rakamları

[[IMAGE: inline-3 | vendor-benchmarks-vs-independent-tests.webp; alt: Sahnede spot ışığı altında kupa biçimli bir grafik, yanında karışık sonuçlu defterler, kronometreler ve soru işaretleri | Cloudflare'in tabloları kendi ölçümü. Startrise, Construct ve başkalarının küçük testleri ise karışık sonuçlar verdi.]]

[Changelog'a göre](https://developers.cloudflare.com/changelog/post/2026-10-01-clef-workers-ai/) 43 ölçümün medyanında Clef 209,3 ms, Clef-flash 38,8 ms, Jev 524,1 ms. Cloudflare bunu Clef için 2,5 kat, Clef-flash için 13 kat hız farkı diye özetliyor.

### Latency rakamları neden kıyaslanamaz

Bu 13 kata temkinli bakın. [Flavio Copes](https://flaviocopes.com/clef/), leaderboard'un metodoloji notlarına dayanarak Clef'in süresinin Cloudflare'in kendi serving altyapısında ölçüldüğünü yazıyor. Jev'in 524 ms'si ise Cloudflare'in laboratuvarından TypeSafe'in API'sine internet üzerinden gidip gelen bir istek. Biri ağın içinde ölçülmüş, öteki internetin üzerinden. TypeSafe, Batı Kıyısı'ndan çağrıların çoğu için yaklaşık 100 ms veriyor.

Her modeli internet üzerinden çağıran testlerde sıralama değişiyor. Startrise'ta karar başına süre Jev için 320, Clef-flash için 316, Clef için 655 ms. Construct'ın laptop'tan aldığı medyanlar aynı sırayla 454, 449 ve 654 ms. [DEV Community'deki testte](https://dev.to/therabbithole/cloudflare-just-shipped-two-decision-models-i-raced-them-against-jev-on-openrouter-3fdm) Jev her görevde en hızlısı.

Doğrulukta Cloudflare, 10 decision benchmark'ın 7'sinde birinciliği bir Clef modeline veriyor; BANKING77'de Clef 94,20, Jev 79,74 gibi. Model kartının tamamında tablo karışıyor: akıl yürütme ağırlıklı satırlarda Jev açık ara önde, GPQA Diamond'da 78,3'e 48,0. The Register'ın hatırlattığı gibi bu skorlar Cloudflare'in kendi ölçümü ve resmi Decision Index'te henüz tekrarlanmadı.

Bağımsız doğruluk sonuçları birbirine yakın:

- **Startrise:** 10 görev, model başına 168 karar. YZ ile sonradan incelenmiş referanslarla uyum Jev'de yüzde 89,2, Clef'te yüzde 89,8, Clef-flash'ta yüzde 82,6.
- **Construct:** 117 etiketli sentetik vaka. Drop-in doğruluk Clef'te yüzde 92,3, Jev'de yüzde 88,6, Clef-flash'ta yüzde 82,1. Construct'a göre fark istatistiksel olarak anlamlı değil.
- **DEV Community:** 40, 30 ve 12 maddelik elle hazırlanmış setler. Jev ile Clef aşağı yukarı başa baş; Clef her görevde bir kez HTTP 429 "Capacity temporarily exceeded" hatası vermiş.

[Hacker News](https://news.ycombinator.com/item?id=49923692) ve [X](https://x.com/search?q=Clef%20Jev) tarafında anekdotlar iki yöne de dağılıyor.

### Testler küçük, herkesin bir çıkarı var

Bu testlerin hepsi küçük ve lansmandan birkaç gün sonra yapılmış; Startrise bile pilotlarının genel doğruluk hakkında hüküm vermediğini yazıyor. Üstelik Startrise ilgili hizmetler satan bir danışmanlık şirketi, Construct da Cloudflare üzerinde çalışıyor. Cloudflare kendi modelini rakibin API'siyle kıyasladı. TypeSafe ise Copes'a göre Jev için kamuya açık benchmark yayımlamıyor ve kendi "193.6x faster" iddiası için "some bias could exist" diyor.

TypeSafe'in kurucusu Diogo Almeida, [GIGAZINE'in aktardığına göre](https://gigazine.net/gsc_news/en/20261005-clef-cloudflare-decision-model/) X'te "benchmaxxed" modellerle güvenilirliği önemseyenlerin modelleri arasında benchmark'ta görünmeyen bir fark olduğunu yazdı; [daily.dev podcast'inde](https://daily.dev/posts/jev-system-one-models-for-prod-not-god-with-diogo-almeida-ceo-typesafe-ai-1c6lthxm7) de benchmark'lar için "extremely gameable" dedi. Haksız sayılmaz. Öte yandan bu tavır Jev'in iddialarını dışarıdan sınamayı da zorlaştırıyor.

## Clef, Jev'in yerine doğrudan geçer mi?

[[IMAGE: inline-4 | threshold-dial-two-models.webp; alt: Aynı girdi kartını okuyan iki gösterge, 0 ile 1 arasındaki eşik çubuğunun üstünde farklı noktaları gösteriyor | API aynı, olasılıklar farklı. Construct'ın testinde Jev için ayarlanan threshold'lar Clef'te yeniden ayar istedi.]]

API düzeyinde büyük ölçüde evet. Kararlarınız için test etmeden hayır.

Construct'ın en net bulgusu, threshold'ların modelden modele taşınmaması. Jev'in olasılıklarına göre ayarlanmış bir eşik Clef'e oturmuyor. Her model kendi threshold'unu alınca üçü de yüzde 90,6 ile 93,2 arasına geliyor.

Confidence değerleri de farklı davranıyor. Startrise'ta Jev doğru cevaplarda ortalama 0,86, yanlışlarda 0,69 vermiş; Clef'te bu ikili 0,94 ve 0,84, yani ara daha dar. Düşük confidence'lı vakaları insana yönlendiriyorsanız o kuralı yeniden sınayın. Jev'in confidence tarafını [RLCD yazısında](https://www.oguzhan.co/tr/jev-confidence-rlcd-kalibre-suphe/) konuşmuştuk.

Tekrarlanabilirlikte durum tersine dönüyor. Construct'ta Clef ve Clef-flash, 351 tekrar çağrının hepsinde aynı olasılıkları döndürmüş. Jev'de karara esas olan olasılık 0,10'a kadar oynamış, iki vaka taraf değiştirmiş. Üç kalibrasyon sorusundaki skorlar da 20 Eylül ile 4 Ekim arasında, aynı `jev-1.13.0` sürümü altında kaymış.

## İki tarafın da zayıf noktaları

İkisi de yeni. Jev early access'te ve `jev-latest` ile `jev-preview` aynı `1.13.0`'ı gösteriyor. Clef'e beta etiketi konmamış, ama Cloudflare'in blogunda "We're still early here." cümlesi duruyor. [InfoQ'nun haberine göre](https://www.infoq.com/news/2026/10/typesafe-ai-jev-released/) TypeSafe'in "jaggedness" sayfası Jev'in sayma, aritmetik ve tarih karşılaştırmasında güvenilmez olduğunu yazıyor, hesabı kodda tutmayı ve sürüm sabitlemeyi öneriyor. Açık sözlü bir dokümantasyon; yine de gerçek eksiklerin listesi.

**Jev:** ağırlıklar ve mimari kapalı, fine-tuning yok; yalnızca metin; servis ABD Batı Kıyısı'nda; rate limit'ler dinamik; belgelenmiş jaggedness; Construct'a göre aynı sürüm adı altında kayma; kamuya açık benchmark yok.

**Clef ve Clef-flash:** Clef'in liste fiyatı Jev'in altı katına yakın; benchmark'lar Cloudflare'in kendi ölçümü; manşetteki latency farkını internet üzerinden yapılan testler tekrarlayamadı; bir testte 429 kapasite hatası; akıl yürütme satırlarında Cloudflare'in kendi kartında bile Jev'in gerisinde; eğitim verisi kapalı; self-host için 41 ile 85 GB VRAM.

## Hangi durumda hangisi

Kazanan ilan etmeyeceğim; aşağıdakiler kendi eval'iniz için birer çıkış noktası.

- **Yalnızca metin, yüksek hacim:** Jev'in liste fiyatı en düşük, iki maliyet testinde de karar başına en ucuzu çıktı. Doğruluk yakın; sürüm kaymasına tahammülünüz belirleyici.
- **State'te görsel varsa:** Clef ya da Clef-flash. Jev yalnızca metin alıyor.
- **Self-host, verinin nerede durduğu, sürüm sabitleme:** Clef'in ağırlıklarıyla modeli dondurup istediğiniz yerde çalıştırabilirsiniz, GPU'nuz yetiyorsa. Jev'de TypeSafe'in servisine bağlısınız.
- **Kendi kararlarınızla fine-tune:** Clef, ama program hâlâ design partner aşamasında.
- **Zaten Cloudflare Workers üzerindeyseniz:** İkisi de Workers AI'da (Jev `typesafe/jev` adıyla); yan yana denemek kolay.
- **Latency'nin kritik olduğu hot path:** Kodunuzun çalıştığı yerden ölçün. Startrise ve Construct'ta Jev ile Clef-flash yakın, Clef en yavaş.
- **Akıl yürütme ağırlıklı sorular:** Cloudflare'in kendi kartında bile Jev önde. İkisinde de aritmetiği ve tarihleri kodda tutun.

Bana sorarsanız Clef, Jev kullananlara bir çıkış kapısı ve görsel desteği getiriyor. Metin tarafında Jev hâlâ daha ucuz görünüyor. Eldeki kanıt ikisi için de, kendi iş yükünüzde denemeden karar vermeye yetecek kadar güçlü değil.

## Kaynaklar

- Cloudflare blogu, "Introducing Clef" (2026-10-01): https://blog.cloudflare.com/clef-decision-models/
- Cloudflare changelog (2026-10-01): https://developers.cloudflare.com/changelog/post/2026-10-01-clef-workers-ai/
- Workers AI model sayfası, Clef: https://developers.cloudflare.com/workers-ai/models/clef/
- Workers AI fiyatlandırma (2026-10-01 güncellemesi): https://developers.cloudflare.com/workers-ai/platform/pricing/
- Hugging Face model kartı, Cloudflare/clef: https://huggingface.co/Cloudflare/clef
- The Register (2026-10-01): https://www.theregister.com/ai-and-ml/2026/10/01/cloudflare-tries-to-outplay-jev-with-open-weight-clef-models/5300649
- Hacker News tartışması: https://news.ycombinator.com/item?id=49923692
- Startrise (2026-10-06): https://www.startrise.io/blog/jev-vs-clef/
- Construct (2026-10-05): https://construct.computer/blog/clef-vs-jev-benchmark/
- DEV Community, TheRabbitHole (2026-10-08): https://dev.to/therabbithole/cloudflare-just-shipped-two-decision-models-i-raced-them-against-jev-on-openrouter-3fdm
- Flavio Copes, Clef incelemesi: https://flaviocopes.com/clef/
- GIGAZINE (2026-10-05): https://gigazine.net/gsc_news/en/20261005-clef-cloudflare-decision-model/
- daily.dev podcast özeti, Diogo Almeida: https://daily.dev/posts/jev-system-one-models-for-prod-not-god-with-diogo-almeida-ceo-typesafe-ai-1c6lthxm7
- TypeSafe lansman yazısı (2026-09-15): https://typesafe.ai/blog/introducing-system-one-models-and-jev
- TypeSafe dokümanları, Models: https://docs.typesafe.ai/models
- InfoQ (Ekim 2026): https://www.infoq.com/news/2026/10/typesafe-ai-jev-released/
- X paylaşımları, 3-8 Ekim 2026 (@Lonely__MH, @samsillva, @_mantaroh_): https://x.com/search?q=Clef%20Jev
