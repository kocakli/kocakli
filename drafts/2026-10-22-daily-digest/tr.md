---
title: "DeepSeek DeepInfer üretim motorunu GitHub'a koydu"
slug: "deepseek-deepinfer-eagle-4-muse-glimmer-yerel-model"
excerpt: "DeepSeek DeepInfer, V4.1-Flash için açılan Apache 2.0 inference çatısı. Sürüm çevrimdışı. EAGLE-4 source-available bir drafter. Muse Glimmer raporu 30B modeli tek GPU'da anlatıyor. Viggle 3D sahneyi sentlerle fiyatlıyor."
focuskw: "DeepSeek DeepInfer"
yoast_title: "DeepSeek DeepInfer servis katmanını açtı"
yoast_metadesc: "DeepSeek DeepInfer, V4.1-Flash için Apache 2.0 çevrimdışı inference. EAGLE-4 source-available. Muse Glimmer tek GPU. Viggle 3D sahneyi sentle fiyatlıyor."
---

DeepSeek DeepInfer 20 Ekim 2026'da, saat 09:30 UTC'de (İstanbul'da 12:30) GitHub'a çıktı. DeepSeek-V4.1-Flash'i üretimde taşıyan inference çatısı bu, lisans Apache 2.0, inen dosyalar çevrimdışı inference. Aynı iki günde Eagle'ın EAGLE-4'ü, Meta'nın 30B Muse Glimmer raporu ve Viggle'ın bir 3D sahneyi bir sentin altında compute ile kurduğu iddiası da vardı. Repoları, makaleleri, blogları ve fiyat sayfalarını okudum, kurmadım, çalıştırmadım, ölçmedim.

## 🧰 DeepSeek DeepInfer: servis katmanı GitHub'da
<!-- INLINE: deepinfer-serving-stack -->

DeepSeek'in [dağıtım notlarına](https://github.com/deepseek-ai/DeepInfer/blob/main/doc/inference_deployment_qa.md) göre tek küme günde 155 trilyon token işliyor. Genel gelir, notun ifadesiyle vadi fiyatında, GPU-saat başına 38 dolar. KV cache 72 saatten uzun tutuluyor. Verimli en küçük birim 64 GPU prefill artı 64 GPU decode, decode için EP64 ve üzeri. Depolama GPU başına yaklaşık 14,4 TB, mantıksal boy.

[README](https://github.com/deepseek-ai/DeepInfer): DeepInfer, büyük ölçekli üretimi çalıştıran inference çatısı. Bu sürüm çevrimdışı inference. Lisans Apache 2.0. Tek model DeepSeek-V4.1-Flash, varsayılan checkpoint deepseek-ai/DeepSeek-V4.1-Flash-1017. Ağırlıklar [19 Ekim notunda](https://www.oguzhan.co/tr/openai-misalignment-raporlari-claude-ecdsa-tohumlari/) var. Donanım: NVIDIA SM100 GPU, Huawei Ascend 950 NPU. Linux, Python 3.12, NVIDIA'da CUDA 13, Ascend'de CANN 9.2.

[X duyurusu](https://x.com/deepseek_ai/status/2112476496283775135) çatıyı "artık tamamen açık kaynak" diye tanıtıyor. V4.1-Flash'i ölçekte bu motor taşıyor. Amaç: işlem maliyetini, enerjiyi ve fiyatı düşürmek.

Listede optimize çekirdekler, attention DP / balanced CP, EPLB ile MoE expert parallelism, speculative decoding için DSpark ve confidence-scheduled verification, SWA bounded replay, asenkron zero-overhead batch zamanlayıcı, batch-invariant inference, deterministic sampling ve structured outputs. Motor notu, kodun vLLM'den türediğini ve DeepSeek'in değiştirdiğini söylüyor.

Olmayanlar: KV cache sistemi, prefill ile decode ayrıştırması, replikalar arası load balancing. Dağıtım notu, KV cache yönetimi ile load balancing'in iç altyapıya sıkı bağlı olduğunu ve o kodun henüz tamamen açılmadığını yazıyor. Çevrimiçi servis sarmalayıcısı yok.

[deepseek-recipe](https://github.com/deepseek-ai/deepseek-recipe) yanında, GitHub lisansı MIT. Ana akım LLM API protokollerini token dizisine çeviriyor, resmi API ile hizalı. Sonraki modellerin inference kodu da DeepInfer'e inecek.

128 GPU, sağlayıcı ve kendi kümesini kuran ekip için taban. KV cache ile load balancer içeride.

## 🦅 EAGLE-4 kuyruk dolunca da hızlı kalıyor mu?
<!-- INLINE: eagle-4-draft-tree -->

Küçük drafter birkaç sonraki token kestirir, hedef model tek geçişte doğrular. [EAGLE-4 reposu](https://github.com/eagle-hq/EAGLE-4) çıktı dağılımının hedef modelde kaldığını yazıyor. Drafter hedef başına bir tane. Ağaç, ölçülen drafting ve verification maliyetine göre kuruluyor (batch, donanım, iş yükü). Isınma turu EAGLE-Harness tablosuna yazıyor. [Eagle blogu](https://blog.eagle.ai/blog/introducing-eagle-4) (20 Ekim 2026): düşük eşzamanlılıkta işe yarayan ağaç, yük altında pahalıya dönebiliyor.

Aynı yazı, aynı motor, Qwen3.8-27B, 4x NVIDIA B300, TP4, T=0. Tek istek, sonra 512 toplamı: vanilla 240,5 tok/s ve 21.203, DSpark 618,6 ve 14.229, DFlash 2 672,6 ve 16.641, EAGLE-4 863,8 ve 28.340. 512 istekte DSpark ile DFlash 2 vanilla'nın altında, EAGLE-4 üstünde. Tek istekte 961,6 tok/s TokenSpeed'e ait, SGLang referansı 837,6. Nemotron 3.5 Super VL, 4x B300: 647 tok/s ve 33.480, katlar 2,74 ve 1,69.

Eklenti: SGLang, vLLM, deneysel TokenSpeed (yamalı wheel ve imaj, stok motorda kanca yok). [AMD'ye göre](https://x.com/AIatAMD/status/2112659635295404176) ilk gün Instinct MI355X'te, Qwen3.8-27B BF16, tek GPU, yaklaşık 300 tok/s, yerleşik MTP'den 1,6 kat. Rakam AMD'nin.

Repostlar açık kaynak demiş. Repo source-available diyor: kaynak incelenebiliyor, OSI onaylı açık kaynak lisansı taşımıyor. Ticari kullanım, 12 aylık ciro 20 milyon doların altındayken serbest. Rakip ürün kullanımı ayrı lisans istiyor, ciroya bakılmaksızın.

## 💻 Muse Glimmer: tek tüketici GPU'suna sığan 30B agent

Ağırlıklar Ağustos 2026, [model kartında](https://huggingface.co/meta-models/Muse-Glimmer-30B). Rapor yeni.

19 Ekim 2026'da [AI at Meta](https://x.com/AIatMeta/status/2112265822274302066) raporu duyurdu. Kendi ifadesiyle Muse Glimmer, tüketici donanımında agent işleri için kurulmuş 30B open-weight bir model. 4-bit hassasiyette, tek tüketici GPU'su olan Mac ya da PC'de pratik hızlarda çalışıyor. Ağırlıklar [15 Ekim yazısında](https://www.oguzhan.co/tr/muse-wonder-gemini-4-argon-frontier-ajanlar/) bir satır geçmişti. Alexandr Wang, Axios'a Meta'nın bu ağırlıkları kısa süre önce açık ağırlık olarak paylaştığını söylemişti.

[Teknik rapor](https://arxiv.org/abs/2610.24628) (20 Ekim 2026, v2) ve [araştırma sayfası](https://ai.meta.com/research/publications/muse-glimmer-30b-an-on-device-agentic-model/): yoğun causal transformer, yaklaşık 29,6 milyar parametre, yaklaşık 1,8 milyarı perception encoder. Giriş metin ve görsel, çıkış metin. Bağlam 128K ve üzeri, kartta 131.072 ve üzeri. Yaklaşık 140 dil. Apache 2.0. Muse Spark'tan damıtılmış. Rapor ona Meta'nın [frontier-class modeli](https://www.oguzhan.co/tr/frontier-model-ne-demek/) diyor. Hedef 32 GB ayrılmış bellek, yaklaşık 4-bit ve bir DFlash speculative decoding başı. Rapordaki cümle: tek RTX 5090'da, kalite kaybı az, pratik hız. Tok/s yok.

Agent eğitimi simüle dijital hayatlarla yapılmış: bir persona, 10 ila 14 kişilik çevre, haftalarca yazışma, takvim, belge ve mesaj geçmişi, araçlar da gerçek argüman ve JSON biçimini taklit ediyor.

Sayılar Meta'nın [teknik raporundan](https://arxiv.org/abs/2610.24628). Muse Glimmer high reasoning, yanında Gemma4-31B thinking ve Qwen3.6-27B thinking.

| Benchmark | Muse Glimmer | Gemma4-31B | Qwen3.6-27B |
|---|---|---|---|
| MCPAtlas (tool use) | 75.5 | 54.2 | 62.5 |
| SWE-Bench Pro | 51.2 | 36.9 | 50.2 |
| SWE-Bench Verified | 76.0 | 66.6 | 77.2 |
| OSWorld-Verified | 65.9 | 58.5 | 75.6 |

Araç kullanımında Glimmer önde. OSWorld-Verified ile SWE-Bench Verified satırlarını Qwen3.6-27B alıyor.

## 🌍 3D sahne artık kaça geliyor?

[Viggle'ın 19 Ekim 2026 notu](https://viggle.ai/jst2) JST-2'yi (Joint Space-and-Time, ikinci nesil) fiziği içinden kurulmuş bir dünya temel modeli diye tanıtıyor. Atomlar 3B uzayda, xyz açık, piksel ve video uzayının dışında. Çıktı 3D Gaussian splat, tarayıcıda çiziliyor. Viggle grafiği: NVIDIA B200'de yaklaşık bir saniye, 0,01 doların altında. World Labs Marble 5 ila 6 dakika, Viggle'ın kıyası. Mekânsal girdi 64 görüntüye kadar. Tek görsel riglenmiş karaktere dönebiliyor. Beden hareketi metinden ya da videodan.

[API fiyat sayfası](https://viggle.ai/developers): prompt sahnesi 0,06 dolar (6 kredi, önce panorama), diğer işler 0,01 dolar, 100 ücretsiz kredi. PINOC'ta denemek ücretsiz. API ve MCP açık, Viggle'a göre Codex ve Claude Code ile çalışıyor. Duyuru [Viggle'ın X gönderisinde](https://x.com/ViggleAI/status/2112202242048528540).

Çarpışma ve nesne etkileşimi kural tabanlı fizik. JST-3 geliştirmede ve bu dinamikleri öğrenmeyi amaçlıyor. JST-1 meme uygulamasını taşımış, Viggle kullanıcıyı 50 milyonun üstünde veriyor.

Dört not, hepsi tesisat. İndirimi servis katmanında izliyorum. EAGLE-4'ün lisans satırı da tablonun yanında.

## Kaynaklar

[DeepInfer deposu](https://github.com/deepseek-ai/DeepInfer)
[DeepInfer dağıtım notları](https://github.com/deepseek-ai/DeepInfer/blob/main/doc/inference_deployment_qa.md)
[deepseek-recipe](https://github.com/deepseek-ai/deepseek-recipe)
[DeepSeek X gönderisi](https://x.com/deepseek_ai/status/2112476496283775135)
[Eagle blogu](https://blog.eagle.ai/blog/introducing-eagle-4)
[EAGLE-4 deposu](https://github.com/eagle-hq/EAGLE-4)
[AMD X gönderisi](https://x.com/AIatAMD/status/2112659635295404176)
[Muse Glimmer araştırma sayfası](https://ai.meta.com/research/publications/muse-glimmer-30b-an-on-device-agentic-model/)
[Muse Glimmer teknik raporu](https://arxiv.org/abs/2610.24628)
[Muse Glimmer model kartı](https://huggingface.co/meta-models/Muse-Glimmer-30B)
[AI at Meta X gönderisi](https://x.com/AIatMeta/status/2112265822274302066)
[Viggle JST-2](https://viggle.ai/jst2)
[Viggle API fiyatları](https://viggle.ai/developers)
[Viggle X gönderisi](https://x.com/ViggleAI/status/2112202242048528540)
