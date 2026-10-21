---
title: "MiniMax M3.1 Flash: Space Bunny'nin maskesi düştü, token ucuzladı"
slug: "minimax-m3-1-flash-space-bunny-fiyat"
focus_keyphrase: "MiniMax M3.1 Flash"
yoast_title: "MiniMax M3.1 Flash: Fiyatı, Özellikleri, Space Bunny Bağı"
meta_description: "MiniMax M3.1 Flash milyon tokene $0.15 girdi ve $0.60 çıktı ile açıldı. Space Bunny erken sürümdü. Düşünme kapanmayınca görev faturası yine büyüyebilir."
excerpt: "19 Ekim 2026'da MiniMax, MiniMax M3.1 Flash'i açtı ve Space Bunny'yi erken sürüm diye yazdı. Liste fiyatı milyon tokende $0.15 girdi, $0.60 çıktı. Düşünme varsayılan olarak açık kalıyor."
---

## Space Bunny sahibini buldu

19 Ekim 2026'da [MiniMax](https://www.minimax.io/blog/minimax-m31f), MiniMax M3.1 Flash'i açtı ve [OpenRouter](https://openrouter.ai/stealth/space-bunny-alpha) üzerinde 23 Eylül'den beri Space Bunny Alpha adıyla duran isimsiz modelin bunun erken sürümü olduğunu yazdı. [Fiyat sayfası](https://platform.minimax.io/docs/guides/pricing-paygo) milyon token için $0.15 girdi, $0.60 çıktı ve $0.015 önbellekten okunan girdi gösteriyor. [Model kılavuzu](https://platform.minimax.io/docs/guides/text-generation) MiniMax-M3.1-Flash'e 1.000.000 tokenlik bağlam penceresi veriyor, girdi metin, görüntü ve video. Çağrı MiniMax API, M Plan ve MiniMax Code masaüstü uygulamasından gidiyor, ağırlıklar ise duyuruya göre daha sonra yayımlanacak.

## 23 Eylül'den 19 Ekim'e adsız kaldı

Duyuruyu, API belgelerini, fiyat sayfasını, OpenRouter'ın stealth sayfasını ve Plotly'nin yazısını okudum. Modeli çalıştırmadım, kimseyle de konuşmadım. Alttaki skorlar ya MiniMax'in kendi iddiası ya da Plotly'nin tek testi.

OpenRouter'ın stealth sayfası, adın bir süre gizlendiği liste. Space Bunny Alpha orada anonim: çıkarımı hızlı, kodu güçlü, reasoning effort ayarlanabilir, bağlam 1 milyon token. Girdi baştan çoklu modal, metin, görüntü ve video. Dışarı metin çıkıyor. Listelenme tarihi 23 Eylül 2026. Sayfa, modeli MiniMax M3.1 Flash olarak açıklıyor. Ücretsiz stealth dönemi bitmiş. İstemler ve tamamlamalar sağlayıcıda tutulmuş olabilir, eğitime kullanılmıyor.

Tutulma ihtimalini eğitim yasağından ayrı okudum. Eğitim yasağı, kaydın silindiği anlamına gelmiyor.

[MiniMax](https://www.minimax.io/blog/minimax-m31f), anonim çalışırken 200 trilyondan fazla token işlendiğini söylüyor. [TokenPost](https://www.tokenpost.com/news/technology/34757) 19 Ekim tarihli haberinde önizlemenin 23 Eylül'de OpenRouter'a geldiğini, 24 Eylül'de OpenCode'un günlük token sıralamasında zirveye oturduğunu yazıyor. [OpenCode veri sayfası](https://opencode.ai/data/minimax/minimax-m3-1-flash) ise adlandırılmış modeli geçen hafta, OpenCode genelinde token hacminde ikinci sıraya koyuyor. Son iki aydaki tokenlerin yüzde 16'sı da burada görünüyor.

Ad konmadan önceki sessiz trafik, laboratuvarlarda gördüğüm bir alışkanlık. Bunu görüş olarak yazıyorum. MiniMax'in yayımladığı olgu token sayısı.

## MiniMax M3.1 Flash için duyurulan sayılar
<!-- INLINE_IMAGE_1 -->

[MiniMax duyurusuna](https://www.minimax.io/blog/minimax-m31f) göre ajan görevlerinde, kodlamada, Computer Use'ta ve siber güvenlikte nesil sıçraması var. Çevrimiçi çıkarım neredeyse üç kat hızlı. Ajan görevlerinde toplam kullanım maliyeti, önceki modele göre yüzde 70 daha düşük. Hız cümlesinin kıyas tabanı yok. "Önceki" MiniMax'in kelimesi. MiniMax-M3'ün fiyatını kendi kartından okuyorum.

Aynı yazıdaki benchmark satırları MiniMax'in iddiası:

- DeepSWE v1.1 yüzde 73,7
- OSWorld V2 61,7
- Agents' Last Exam 29,6. MiniMax, hem OSWorld V2'de hem ALE'de Çin modelleri arasında birinci olduğunu söylüyor
- BankerToolBench 76,2
- CyberGym yüzde 82, zafiyet bulma ve doğrulama diye çerçevelenmiş
- AutomationBench-AA'da en iyi performans gösterenler arasında. MiniMax bunu satış, pazarlama, operasyon, müşteri hizmeti, finans ve insan kaynaklarındaki kurumsal SaaS akışları için yazıyor

MiniMax, iç güvenlik uzmanlarının modeli kod denetiminde, zafiyet yamalamada, sızma testinde, zararlı yazılım analizinde ve tersine mühendislikte güçlü bulduğunu da ekliyor. Bu cümle onların tarifi.

Hız da aynı duyurudan. Daha agresif sparsity, yani hesabı daha seyrek tutmak. Çıktı saniyede 200 tokenin üstüne çıkabiliyor. Medyan (P50) saniyede 170 tokenin üstü.

Bu yüzdeler satıcı skoru. Aşağıdaki 43 soru ayrı test. Bu yüzdelerle genel bir Claude ya da GPT sıralaması kurmuyorum.

[Model kılavuzu](https://platform.minimax.io/docs/guides/text-generation) MiniMax-M3.1-Flash'i, 1 milyon token bağlamlı ve düşünme derinliği ayarlanabilen frontier coding modeli diye tanıtıyor. Ajan muhakemesi, araç kullanımı, kod ve yapılandırılmış görev için tasarlanmış. Frontier etiketini [ayrı notta](https://www.oguzhan.co/tr/frontier-model-ne-demek/) açıyorum. Aynı kılavuz "gündelik iş için ultra verimli, açık ağırlıklı model" de diyor. Duyuru ağırlıkları sonraya bırakıyor.

MiniMax-M3 de kılavuzda duruyor, o da 1 milyon token bağlamla.

Dosya sınırları [OpenAI SDK sayfasında](https://platform.minimax.io/docs/api-reference/text-openai-api). Görüntü JPEG, PNG, GIF ya da WEBP, tavan 10 MB. Video MP4, AVI, MOV ya da MKV. Varsayılan örnekleme saniyede 1 kare, izin verilen aralık 0,2 ile 5. Adres ya da base64 ile giden video 50 MB'a kadar. Files API üzerinden video 512 MB'a kadar. Ses girdisi yok.

## Fiyat listesinde ne yazıyor?

Rakamlar 1 milyon token için ABD doları. Flash ve M3 satırları [MiniMax'in kullandıkça öde sayfasından](https://platform.minimax.io/docs/guides/pricing-paygo). DeepSeek satırı [DeepSeek fiyat sayfasından](https://api-docs.deepseek.com/quick_start/pricing). Orada deepseek-flash, DeepSeek-V4.1-Flash-1017 demek ve bağlam yine 1 milyon token.

| Model | Girdi | Çıktı | Önbellekten okunan girdi |
|---|---|---|---|
| MiniMax M3.1 Flash | $0.15 | $0.60 | $0.015 |
| MiniMax M3 (standart, ≤512k girdi) | $0.30 | $1.20 | $0.06 |
| DeepSeek V4.1 Flash (sakin saat / yoğun saat) | $0.15 / $0.30 | $0.60 / $1.20 | $0.003 / $0.006 |

Girdi ve çıktıda MiniMax M3.1 Flash, girdi 512k ve altındayken MiniMax-M3'ün standart ücretinin yarısı. Önbellekten okunan girdi $0.015. Bu, Flash'in kendi $0.15 girdi fiyatının onda biri. Aynı kademedeki M3 önbellek fiyatı $0.06 olduğu için o sütunda oran çeyrek.

512k üstü girdide M3'ün kartı $0.60, $2.40 ve $0.12. Sayfada M3 için 1,5 kat öncelik kademesi de var. Flash'in yayımlanan satırı düz: $0.15 / $0.60 / $0.015.

MiniMax, ajan görevlerinde toplam kullanım maliyetinin önceki modele göre yüzde 70 düştüğünü söylüyor. Tabela, token hacmi, çağrı sayısı ve önbellek payı bilinince faturaya dönüşüyor.

Sakin saatte DeepSeek, girdi ve çıktıda Flash ile aynı yerde: $0.15 ve $0.60. DeepSeek'in yoğun saatleri pazartesiden cumaya, UTC ile 01:00-04:00 ve 06:00-10:00. O aralıkta girdi ve çıktı ikiye katlanıp $0.30 ve $1.20 oluyor. Önbellek isabeti iki pencerede de Flash'in altında: sakin saatte $0.003, yoğun saatte $0.006, Flash'te $0.015. 19 Ekim özetinde DeepSeek-V4.1-Flash-1017, [üç açık ağırlık yayını arasında](https://www.oguzhan.co/tr/openai-misalignment-raporlari-claude-ecdsa-tohumlari/) duruyordu. Bu satır ücret kıyası. Flash'in ağırlıkları hâlâ yayımlanmadı. $0.15 / $0.60 çifti, [Haiku 5.5 ve GPT-6 Luna notundaki](https://www.oguzhan.co/tr/claude-haiku-5-5-gpt-6-luna-fiyat-tabani/) ucuz kademenin de komşusu. Flash'e eklenen kural tabelada görünmüyor: düşünme açık kalıyor.

Türkiye'den bakan geliştirici bu satırlara zaten dolarla bakıyor. İşin faturası, biten çağrıdan ve harcanan tokenden çıkıyor.

## Uzun düşünme ucuz tokeni pahalı işe çeviriyor
<!-- INLINE_IMAGE_2 -->

[Sohbet tamamlama belgesi](https://platform.minimax.io/docs/api-reference/text-chat-openai) M3.1 Flash'in her zaman düşündüğünü yazıyor. `thinking` alanını `disabled` göndermek HTTP 400 döndürüyor. Düşünme izi ayrı geliyor, alanın adı `reasoning_content`. Derinlik ayarı bu sayfada `reasoning_effort`, model kılavuzunda `effort`. İkisi de `low`, `medium`, `high`, `xhigh` ve `max` kabul ediyor. Varsayılan `max`.

Aynı sayfada MiniMax-M3 uyarlanabilir düşünüyor. `disabled`, M3'te düşünmeyi atlıyor. Flash ucuz tokeni satıp sessiz çağrıyı reddediyor. M3 sessizliği hâlâ kabul ediyor, daha yüksek ücretle. M3 gövdesinden kopyalanıp düşünmesi kapatılmış bir istek, Flash'te HTTP 400 yer.

[Plotly'nin 20 Ekim yazısı](https://plotly.com/blog/minimax-m3-1-flash-plotly-data-analytics-bench/) okuduğum tek bağımsız test. 43 soruluk veri analizi. Eylülde Space Bunny, ekimde MiniMax M3.1 Flash. Soruları koşturmadım. Effort kademesi yazıda yok.

Önce eylül, sonra ekim:

- Skor: 43'te 38, sonra 43'te 41
- Bulunan gizli örüntü: 5'te 2, sonra 5'te 5
- Soru başına model çağrısı: 15, sonra 45
- Soru başına okunan token: 0,7 milyon, sonra 4,2 milyon
- Soru başına yazılan token: 8.500, sonra 32.000
- Soru başına medyan süre: 36 saniye, sonra 3 dakika
- MiniMax liste fiyatıyla tam koşu: $0.82, sonra $4.09

Plotly, girdinin yüzde 98'inin önbellekten geldiğini de söylüyor ve bu payı bir kez veriyor. Çağrı 15'ten 45'e çıkmış, üç kat. Yazılan token 8.500'den 32.000'e gelmiş, dört kata yakın. Okunan token 0,7 milyondan 4,2 milyona çıkmış. OpenRouter o sırada MiniMax M3.1 Flash'i şimdilik ücretsiz sunuyormuş. Plotly ekim koşusunu liste fiyatından hesaplamış ve soru başına yaklaşık 10 sent demiş.

Skorda 43'te 41, Plotly sıralamasında Claude Opus 5.5, Gemini 4 Argon, Muse Wonder ve GPT-6 Sol ile berabere. Plotly buna, bir Çin laboratuvarından gördükleri en iyi skor diyor. Sıradaki isimler GLM 5.3 Flash ve Qwen 3.8 27B, ikisi de 38'de. Eylüldeki Space Bunny 43'te 38 ile, Plotly'nin cümlesiyle, o ana kadar denedikleri açık ağırlıklı modellerin herhangi biri kadar iyiymiş.

Plotly, bu 43'te 41'i aynı skor için Claude Opus 5.5 ve Gemini 4 Argon maliyetinin yaklaşık üçte biri diye koyuyor. GPT-6 Sol 41 skoru $2.61'a yapmış. GPT-6.1 Sol aynı $2.61'a 43'te 43 yapmış. İki kıyası da bu tek setin içinde bırakıyorum.

3 dakikalık medyan, Plotly sıralamasının en yavaşı. Çağrı başına yaklaşık 150 token/saniye görmüşler. MiniMax P50'yi 170'in, tepeyi 200'ün üstünde veriyor. Plotly, satıcının medyanını hacme vuruyor: saniyede 170 tokende bile 32.000 token yazmak yaklaşık üç dakika sürüyor. Arka planda yürüyen analiz için idare eder, yanıt bekleyen biri için yavaş.

Bütçeyi effort ayarına göre kurardım. Varsayılan `max`, `disabled` reddediliyor. `low` ile `max` arasındaki token farkını ölçmedim. Plotly'nin ekim modeli aynı sorularda eylül önizlemesinden daha çok çağrı yapmış, daha çok token yazmış.

OpenRouter'ın stealth sayfası ücretsiz dönemin bittiğini söylüyor. Plotly'nin "şimdilik"i 20 Ekim'e ait, ücretsiz ucu liste fiyatıyla çarpmalarının sebebi de bu. O tarihten sonrasına ücretsiz OpenRouter ücreti yazmam.

## M2.5 ve M2.7 kullanan ne yapacak?

[Model listesi](https://platform.minimax.io/docs/faq/models) M2.5 ve M2.7 ailelerine iki tarih koyuyor. 19 Ekim 2026'dan beri yeni kullanıcıya açılmıyorlar. 18 Kasım 2026'da emekliye ayrılıyorlar, API istekleri çalışmaz oluyor.

Kullandıkça ödeyen ve erişimi zaten olan müşteri 18 Kasım'a kadar devam ediyor. M Plan ve Token Plan başka yoldan gidiyor. 19 Ekim'den itibaren M2.5 ya da M2.7'ye giden istekler kendiliğinden MiniMax M3.1 Flash'e yönleniyor. Eski model adları çalışmayı sürdürüyor. Plan hakları değişmiyor.

Plan kullanıcısı tek satır kod değiştirmeden model değiştirmiş oluyor. Çıktı, gecikme ve görev başına token yine kayabilir, çünkü eski adın arkasındaki model artık her zaman düşünüyor ve düşünmeyi kapatmak HTTP 400 getiriyor. Hak sütunundaki sayı yerinde duruyor. O hakkın kaç göreve yeteceği, görev başına tokene bağlı. Kendi işimin eval'lerini yeniden koştururdum. Eski M2.7 kayıtlarını başka modelin günlüğü sayardım.

Notlarımızda bulunsun: fişin çekildiği gün 18 Kasım. MiniMax-M3 duruyor. Düşünmeyi atlayan anahtar onda, ücreti de M3'ün yüksek tarifesinde.

## Ağırlık dosyası henüz yok
<!-- INLINE_IMAGE_3 -->

Duyurudaki cümle kısa: "Model ağırlıkları daha sonra yayımlanacak." MiniMax'in "zekânın sınırını zorlayan" dediği Pro da daha sonra gelecek. Okuduğum sayfalarda tarih yok, parametre sayısı yok, lisans metni yok.

Model kılavuzu MiniMax M3.1 Flash'e "ultra verimli, açık ağırlıklı model" diyor, duyuru sonrayı işaret ediyor, [OpenCode](https://opencode.ai/data/minimax/minimax-m3-1-flash) açık ağırlığı Hayır diye listeliyor. 21 Ekim 2026 itibarıyla indirilecek ağırlık dosyası yok, lisans da yok.

Çin'in 16 Ekim taslağı ayrı izlek. [İhracat kontrolleri ve model ağırlıkları notunda](https://www.oguzhan.co/tr/cin-yapay-zeka-ihracat-kontrolu-model-agirliklari/) duruyor. Halihazırda yayımlanmış açık ağırlıklar taslağın dışında. Yeni açık kaynak yayımları otomatik lisanslanıyor. Taslak kesinleşirse ilerideki bir MiniMax M3.1 Flash ağırlık yayını o yoldan geçer. Parametre sayısı yayımlanmadı. Not, yalnız bu yolu anlatıyor.

## Geçmeden önce kontrol listesi

- Aynı görevleri iki ya da üç effort kademesinde çalıştırıp çağrıyı, tokeni ve süreyi not ederdim. Varsayılan `max`. Kademeyi bilerek seçerdim.
- Girdinin ne kadarının önbellekten geldiğine bakardım. Önbellekten gelen $0.015, gelmeyen $0.15. Bu pay girdinin tarafını oynatır. Çıktı tokeni ve ek çağrı faturada durur.
- Çağrının hangi uçtan gittiğine bakardım. MiniMax Code, MiniMax API ve OpenRouter yönlendirmesi aynı markayı taşıyıp ayrı istek olabilir.
- Üretimde hâlâ M2.5 ya da M2.7 adı geçiyorsa 18 Kasım'ı işaretlerdim. Plan trafiği çoktan yönlendi. Kullandıkça öde çağrıları o gün o adlarda duruyor.
- Yerel makinede çalıştırmadan önce ağırlığı ve lisansı beklerdim.

Tabelayı okumak kolay. Faturayı düşünme süresi dolduruyor.

## Kaynaklar

- [MiniMax duyurusu, 19 Ekim 2026](https://www.minimax.io/blog/minimax-m31f)
- [MiniMax model çağırma kılavuzu](https://platform.minimax.io/docs/guides/text-generation)
- [MiniMax sohbet tamamlama](https://platform.minimax.io/docs/api-reference/text-chat-openai)
- [MiniMax OpenAI SDK sayfası](https://platform.minimax.io/docs/api-reference/text-openai-api)
- [MiniMax model listesi ve emeklilik notu](https://platform.minimax.io/docs/faq/models)
- [MiniMax kullandıkça öde fiyatı](https://platform.minimax.io/docs/guides/pricing-paygo)
- [OpenRouter, Space Bunny Alpha stealth sayfası](https://openrouter.ai/stealth/space-bunny-alpha)
- [TokenPost, 19 Ekim 2026](https://www.tokenpost.com/news/technology/34757)
- [OpenCode, MiniMax M3.1 Flash veri sayfası](https://opencode.ai/data/minimax/minimax-m3-1-flash)
- [Plotly veri analizi yazısı, 20 Ekim 2026](https://plotly.com/blog/minimax-m3-1-flash-plotly-data-analytics-bench/)
- [DeepSeek API fiyatı](https://api-docs.deepseek.com/quick_start/pricing)
