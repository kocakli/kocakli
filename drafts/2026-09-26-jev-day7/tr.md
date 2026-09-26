---
title: "Jev'e hangi kapıdan girilir, nerede kapıdan çevrilir?"
slug: "jev-ekosistem-openrouter-vercel-cloudflare"
focus_keyphrase: "Jev ekosistemi"
yoast_title: "Jev ekosistemi ve kullanım sınırları"
yoast_metadesc: "OpenRouter, Vercel, Cloudflare ve TanStack üzerinden Jev kullanımı; açık replikalar ve Jev yerine LLM seçmeniz gereken işler."
excerpt: "Jev artık üç büyük platformdan çağrılabiliyor, TanStack ile sağlayıcı değiştirmek de kolay. Asıl mesele erişmek değil, hangi kararı ona bırakacağınızı bilmek."
---

Bir hafta boyunca Jev'in nasıl karar verdiğine baktık. Son günün sorusu daha dünyevi: Nereden çağıracağız?

Cevap bol seçenekli. OpenRouter, Vercel AI Gateway ve Cloudflare Workers AI hazır. TanStack AI bunların üstüne ortak bir `decide()` katmanı koyuyor. Üstelik LitJev, openjev, Kev ve NanoJev gibi açık denemeler de var. Fakat kapıların çoğalması her işin Jev'e uygun olduğu anlamına gelmiyor.

Bu yazı, [yedi günlük Jev dosyasının](https://www.oguzhan.co/tr/typesafe-jev-system-one-karar-modeli/) son halkası. Ekosistemi toparlayıp modeli nerede kapıdan çevirmek gerektiğine bakalım.

## OpenRouter, Vercel ve Cloudflare

OpenRouter tarafındaki ilk ayrıntı küçük görünse de entegrasyonu doğrudan etkiliyor: Jev bir chat modeli değil. `typesafe/jev-1.13` ya da hareketli alias olan `~typesafe/jev-latest`, chat completions endpoint'inden çağrılmıyor. Adres, `POST /api/alpha/decisions`. İstekte `model`, `state` ve `questions` var. `@openrouter/sdk` kullananlar için karşılığı `openrouter.alpha.decisions.create()`.

Mevcut bir OpenRouter anahtarı yeterli; ayrıca TypeSafe hesabı açmak gerekmiyor. [Model sayfasında](https://openrouter.ai/typesafe/jev-1.13) 32K context, milyon girdi token'ı başına 0,042 dolar, sıfır çıktı ücreti ve 0,23 saniye P50 latency görünüyor. Tekrarlanabilir test için sürümü sabitlemek, `latest` alias'ını üretim kolaylığı uğruna bilinçli seçmek gerek.

Vercel, AI SDK kullananlara daha tanıdık bir yol sunuyor. AI SDK 7.0.105 ile gelen `experimental_evaluate`, `typesafe-ai/jev` modelini çağırıyor. Choice ve Score aynı adla dururken TypeSafe'in Noul tipi burada Boolean olarak geçiyor. Çıktı yine metin değil; olasılıklarıyla birlikte tipli karar.

AI Gateway'in asıl payı modelden ziyade işletme tarafında. [Vercel'in duyurusuna göre](https://vercel.com/changelog/typesafe-ai-jev-now-available-on-ai-gateway) Zero Data Retention ve No Training seçenekleri istek bazında açılabiliyor. Çağrılar log, rapor ve bütçe takibine de giriyor. TypeSafe client kullananlar `baseURL` değerini `https://ai-gateway.vercel.sh/typesafe` yapıp mevcut `systemOne` çağrılarını koruyabiliyor. SDK istemeyenler için [`POST /v1/evaluate`](https://vercel.com/changelog/ai-gateway-now-supports-typesafe-clients-and-http-api-for-jev) yolu var.

Uygulama zaten Cloudflare Worker üstündeyse en kısa satır orada:

`env.AI.run('typesafe/jev', { state, questions })`

[Workers AI dokümanı](https://developers.cloudflare.com/ai/models/typesafe/jev/) Noul, Choice ve Score örnekleri veriyor; örnek cevaplarda `jev-1.13.0` yazıyor. REST çağrısında aynı gövde `input` içine alınıyor. Cloudflare maliyetini başka sağlayıcının fiyatından türetmemek gerek; güncel tutar dashboard'dan kontrol edilmeli.

Üç kapının arkasında aynı tür karar modeli var. Fakat model adı, auth, istek zarfı, loglama ve sürüm kontrolü aynı değil. “Jev'i denedik” cümlesi bu ayrıntılar yazılmadıysa pek az şey anlatıyor.

<!-- INLINE_IMAGE_1 -->

## Sağlayıcı değiştirmenin kısa yolu

[TanStack AI Evaluate](https://tanstack.com/ai/latest/docs/evaluate/evaluate), aynı `decide()` çağrısını dört adapter ile çalıştırıyor: doğrudan TypeSafe için `typesafeDecider('jev-latest')`, OpenRouter için `openRouterDecider('~typesafe/jev-latest')`, Vercel için `vercelGatewayDecider('typesafe-ai/jev')`, Cloudflare için `cloudflareDecider('typesafe/jev')`.

`state` ve soru haritası yerinde kalıyor, adapter değişiyor. Anahtarlar da beklenen yerlerden geliyor: `TYPESAFE_API_KEY`, `OPENROUTER_API_KEY`, `AI_GATEWAY_API_KEY` ya da Vercel OIDC; Cloudflare tarafında Worker binding veya hesap ile token ikilisi. Sağlayıcı karşılaştırırken güzel kolaylık. Yine de ortak fonksiyon imzası, dört kurulumun aynı sonucu vereceğinin garantisi değil. Alias'ın hangi model sürümüne karşılık geldiğini ve yanıt metadata'sını kaydetmek şart.

## Açık replikaların anlattığı

Bu projeleri “açık kaynak Jev” diye tek sepete atmak cazip. Doğru değil. TypeSafe'in private weight'lerini ya da şirketin RLCD eğitim sistemini yayımlamıyorlar. Aynı ürün biçimini farklı yöntemlerle yeniden kurmaya çalışıyorlar.

[LitJev](https://github.com/zhengxuyu/LitJev), hazır Qwen Hugging Face checkpoint'lerini eğitim yapmadan Jev benzeri bir karar modeline sarıyor. Choice ve olasılık dağılımı dönüyor, cevap metni üretilmiyor. Apache-2.0 lisanslı projenin kendi README'si de açık: Bu, kamuya açık bilgilerden kurulmuş varsayımsal bir replika ve olasılıklar varsayılan halde kalibre değil.

[openjev](https://github.com/daseinlabs/open-jev), Gemma 3 4B ile tek geçişte seçenek puanlıyor. Ortak prefix bir kez işleniyor, KV cache seçenek batch'ine yayılıyor. Apple silicon için MLX, diğer sistemler için PyTorch yolu; `/v1/systemone` ve `/score` sunan FastAPI servisi ile Doom demosu var. MIT lisanslı yerel scorer ve araştırma seti demek daha doğru.

[Kev](https://github.com/jaredpalmer/kev), Qwen tabanlı ailesi ve System One uyumlu servisiyle drop-in kullanıma en çok yaklaşan proje. `python -m kev.serve` ile çalışıyor; TypeSafe Python SDK yerel sunucuya yöneltilebiliyor. Ama Kev, Jev değil. İlk 0.5B checkpoint'i kendi model kartında üretimde kullanılmaması gereken, artık aşılmış bir araştırma prototipi olarak tanımlanıyor. Yeni checkpoint'ler bu ilk denemenin yerini aldı.

[NanoJev](https://github.com/TianyuCodings/NanoJev) yaklaşık 0.6B parametreli, baştan sona eğitilmiş küçük bir replika. Paralel karar, 2 ile 255 arasında dinamik Choice adayı, Boolean ve sıralı Score destekliyor. Hugging Face adresi `C-Tianyu/NanoJev`; seçilmiş oyun checkpoint'i `unified-games-v1` etiketiyle duruyor. İncelenebilir olması kıymetli; hâlâ küçük ölçekli, deneysel bir araştırma projesi.

Bu dört proje yerel çalıştırma, seçenek sırasına hassasiyet ve küçük model davranışı gibi iyi sorular açıyor. Hiçbiri, adında Jev geçtiği için TypeSafe'in kalibrasyon iddiasını miras almıyor. Her birinin kendi etiketli eval setine ihtiyacı var.

<!-- INLINE_IMAGE_2 -->

## Jev'e verilmeyecek işler

E-posta, kod, sohbet cevabı, rapor ya da açık uçlu plan üretecekseniz LLM kullanın. Jev serbest metin yazmıyor. Cevap uzayı baştan tarif edilemiyorsa iş zaten System Two tarafına kaymış demektir.

Choice en fazla 255 seçenek kabul ediyor. Daha kalabalık listede önce adayları daraltmak ya da [Doom ve Wikiracing yazısındaki](https://www.oguzhan.co/tr/jev-gercek-zamanli-doom-wikiracing-tarayici/) iki aşamalı puanla-seç yöntemine dönmek gerekiyor. Doğru cevap listede olmayabilir. Bu yüzden `abstain`, insan incelemesi veya başka bir kaçış yolu tasarlanmadan kapalı seçenek kullanmak, düzenli görünen yanlış cevap üretir.

Şemaya uyan cevap güvenli cevap da değil. İzin verilen tool'lardan yanlış olanı seçmek hâlâ mümkün. Ödeme, silme, yetki değişikliği ve dışarı mesaj gönderme gibi işlerde deterministik kontroller kalmalı. [Guardrail bölümünde](https://www.oguzhan.co/tr/jev-ajan-guardrail-sema-gecerli-guvenli-degil/) gördüğümüz sınır buydu.

Fiyat ve latency rakamları sık karar döngülerinde iştah açıyor; [hız ve maliyet yazısı](https://www.oguzhan.co/tr/jev-hiz-maliyet-paralel-ornekleyici/) bunu ayrıntılı ele aldı. Yine de erken erişim limitleri, alias değişimleri, sağlayıcı farkları ve yanlış kararın bedeli hesabı bozabilir. Eşiği demo üstünde değil, kendi etiketli trafiğinizde belirleyin.

## Dosyanın sonunda kalan

Seri [Choice, Score ve Noul](https://www.oguzhan.co/tr/jev-primitives-choice-score-noul-karar/) ile başladı. Geldiğimiz yerde en işe yarar tarif hâlâ sade: LLM'in yanına hızlı, tipli ve ölçülebilir bir karar katmanı koy; politikayı uygulama kodunda tut.

LLM arasın, düşünsün, yazsın ve anlatsın. Jev ise `state` belli, soru dar, seçenekler tanımlı ve olasılıkların ölçülmüş bir karar eşiğine bağlanabildiği yerde çalışsın. OpenRouter, Vercel, Cloudflare ve TanStack erişim sorununu büyük ölçüde çözdü. Açık replikalar da mekanizmayı kurcalanabilir hale getirdi.

Karar vermenin kendisi hâlâ bize kaldı. Böylesi daha iyi.
