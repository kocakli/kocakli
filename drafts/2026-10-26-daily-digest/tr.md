---
title: "LiteLLM tedarik zinciri saldırısı, Block Dessa ve iki küçük model"
slug: litellm-tedarik-zinciri-saldirisi-block-dessa-nanbeige
excerpt: "PyPI, 21 Ekim'de zehirli bir LiteLLM 1.107.0 paketini yaklaşık iki saat tuttu. 23 Ekim kök neden yazısı, işaretlenip döndürülmemiş Agent Platform anahtarını gösteriyor."
focuskw: "LiteLLM tedarik zinciri saldırısı"
yoast_title: "LiteLLM tedarik zinciri saldırısı: dönmeyen anahtar"
yoast_metadesc: "LiteLLM tedarik zinciri saldırısı, dönmeyen bir anahtardan çıktı. Zehirli 1.107.0 yaklaşık iki saat PyPI'de kaldı. Yanında Block Dessa ve iki model var."
---

PyPI, 21 Ekim'de zehirli bir `litellm==1.107.0` paketini yaklaşık iki saat tuttu. LiteLLM tedarik zinciri saldırısı, [kök neden yazısına](https://docs.litellm.ai/blog/security-incident-oct-21-2026-attack-chain) göre, Mayıs 2026'da işaretlenip hiç döndürülmemiş bir Agent Platform master key'inden çıkmış. Hafta sonu o yazıyı, olay notunu, Dessa sayfasını, iki kartı ve İsveç haberlerini okudum. İlk not, ilk token'ın yerini yanlış vermiş.

## 🔐 LiteLLM tedarik zinciri saldırısı, hiç dönmeyen bir anahtardan çıktı
<!-- INLINE: litellm-attack-chain -->

LiteLLM, çağrıları birçok LLM sağlayıcısına ileten, yaygın kullanılan açık kaynaklı bir Python geçidi. [Olay yazısına](https://docs.litellm.ai/blog/security-incident-oct-21-2026) göre 21 Ekim'de `litellm==1.107.0` PyPI'ye yedi wheel olarak yayımlanmış, 11:39:51 ile 11:40:13 UTC. Docker Hub ve GHCR 11:46:56 UTC. Derleme, kimlik bilgisi çalan ve uzaktan kod çalıştırma araçları yükleyen bir zararlı taşıyor. PyPI 13:23 UTC'de karantinaya almış. Docker Hub'da `v1.107.0`, `latest`, `main-latest` ve `main-stable` 14:20 UTC'ye kadar durmuş. GHCR etiketleri 13:51 UTC'de inmiş. Resmi v1.107.0 kaynak etiketinde zararlı dosya yok. Derleme `Berri-AI/litellm` taklitinden. Asıl organizasyon `BerriAI`.

Oliver Jensen ve Mateo Wang metni 23 Ekim 21:00 UTC'de yayımlamış. LiteLLM bunu asıl kaynak sayıyor. 27 Mayıs 2026'da `opencode.json`, `LiteLLM-Labs/lite-harness` açık deposuna girmiş. İçinde Agent Platform master key'i var. Platform, pull request açan self-hosted cloud agent'lar için içerideki deneysel servis. Commit force-push ile ezilmiş, anahtar iptale işaretlenmiş, döndürülmemiş.

10 Ekim'de anahtar `GET /api/v1/managed_agents/agents?limit=100` ile bütün agent ayarlarını almış. Birinde, iki GitHub organizasyon sahibinden birinin GitHub CLI OAuth token'ı duruyor. Servis hesabı scope'u yok. LiteLLM'e göre bu token'lar 2FA sonrası üretiliyor ve GitHub'ın sudo tarzı yeniden doğrulamasını atlıyor. O gece kısa ömürlü CI branch'leri sırları webhook.site'a POST etmiş. İki bakımcı token'ı daha çıkmış. 12 Ekim'de özel depolardan başka sırlar da gitmiş.

21 Ekim'de release deposuna push, branch protection'a takılmış. Beş saniye sonra sahip token'ı korumayı aşıp workflow'u taklit fork'a bağlamış. İkinci bakımcının çalınan token'ı üretim kapısını onaylamış. Kapı normalde ofisteki fiziksel cihaza kilitli özel hesap ister. O hafta daha erken, herhangi iki mühendis hem tetikleyip hem onaylayabilir olmuş. Gerekçe, hızlı bugfix backport. Onay kapısını 24 Ekim [Claude Duet yazısında](https://www.oguzhan.co/tr/claude-duet-proaktif-agent-onay-sinirlar/) anlatmıştım. Üçüncü token workflow kayıtlarını silmiş. `main` force-push ile temizlenmiş.

LidorMachluf 12:06 UTC'de #47826'yı açmış. LiteLLM, yakalamanın yayımdan sonraki 20 dakika içinde olduğunu söylüyor. Müdahale 13:02 UTC. Özel kayıt defterindeki kurumsal müşteriler etkilenmemiş. LiteLLM'in deyişiyle: "Bu olay, açığa çıkmış olabilecek bir anahtarı döndürmemenin risklerini güçlü biçimde gösterdi." 21 Ekim notu ilk token'ları iç LiteLLM kurulumunun loglarına bağlamış. Kök neden yazısı bunu bırakıyor. İlk token Agent Platform API'sinden gelmiş.

Olay yazısının çizgisi: 21 Ekim 11:39 ile 13:23 UTC arasında sabitlenmemiş pip, ya da 11:46 ile 14:20 UTC arasında o Docker etiketleri. Pip'i önce çalıştırmayın. Her Python açılışı `cook.pth` ve `sitecustomize.py` dosyalarını yeniden işletiyor.

- İkisini kabuktan, Python'dan önce silin.
- `litellm==1.106.2` sürümüne sabitleyin. Sıfırdan kurmak daha iyi.
- Ulaşılabilen anahtarları döndürün: proxy veritabanındaki sağlayıcı anahtarları, master ve sanal anahtarlar, `DATABASE_URL` parolası, bulut rolü.

## 🎙️ Dessa neden yazıya uğramadan konuşuyor?
<!-- INLINE: dessa-full-duplex -->

Block, Dessa'yı 23 Ekim cuma duyurdu. [Sayfa](https://block.xyz/dessa) full-duplex speech-to-speech diyor. Ses girer, ses çıkar, dinlerken konuşur. Araya girer, "evet" ya da "anladım" diye kısa onay verir. Sayfayı okudum.

Block'a göre eğitim sıfırdan, yalnızca insan konuşması, metin yok, hazır model yok. Block, bildiği kadarıyla, bunu yalnızca konuşmadan eğitilmiş ilk gerçekçi canlı sohbet yapay zekası sayıyor. Inference gerçek zamandan hızlı. Yerel makine MacBook Pro M4 Max ya da daha güçlüsü. Eğitim tek NVIDIA GB200 NVL72. Laboratuvar Block'un içinde, küçük. Kuranlar Toronto'daki Dessa girişiminin eski üyeleri. Doğrudan Jack Dorsey'ye bağlı. Lider Ragavan Thurairatnam.

Ürün yok. Herkese açık API yok. Open-weight yok. Erken erişim, Block'un öngörmediği riskler için küçük bir AI safety grubunda. Block'un cümlesi: "Ciddi bir acı içindeyken bir ses yapay zekasının bunun farkında olmamasını ve konuşmayı sürdürmesini düşünün." Open-weight olmayınca ilk davet safety araştırmacılarına gidiyor. Klipte Dessa, OpenAI GPT-Live-1 ile konuşuyor. İkisi de yapay ses. [The Verge](https://www.theverge.com/ai-artificial-intelligence/1017906/jack-dorsey-block-dessa-ai-voice-speech) 23 Ekim'de bazı sohbetleri biraz tuhaf ve tekinsiz bulmuş. Model bir konuşmacıyı Ronaldo sanmış.

## 🧩 Biri öğretmen, öteki cihaza sığmak istiyor

İki Hugging Face kartını da okudum. Makineleri ayrı.

[Nanbeige4.3-33B](https://huggingface.co/Nanbeige/Nanbeige4.3-33B), Nanbeige ekibinin asıl öğretmen modeli. Kart, en yüksek thinking effort ve aynı harness ile Terminal-Bench 2.1'de 80.9 diyor. Her benchmark'ı kazanmıyor. SWE-Bench Pro 60.3 (Qwen3.8-27B 61.7). GDPval 84.8, yanındaki sayı 86.4. GPQA Diamond 89.5 (Gemma4-31B 91.3). Serving için SGLang ve vLLM'de 4 yollu tensor parallelism var. BF16 hali dizüstü bilgisayar modeli değil. Satırdaki Muse Glimmer, [22 Ekim özetindeki](https://www.oguzhan.co/tr/deepseek-deepinfer-eagle-4-muse-glimmer-yerel-model/) tüketici GPU modeli.

NVIDIA, [Nemotron 3.5 Bolt E4B](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Bolt-E4B-BF16) modelini Gemma-4-E4B-it üstünden post-train etmiş. Metin girer, metin çıkar. NVIDIA, OpenMDW-1.1 ağırlıkların ticari kullanıma hazır olduğunu söylüyor. Gemma 4 tabanı Apache 2.0. Karttaki Tau2-Bench 55.10, taban Gemma 4 E4B-it 38.50. Aynı kıyasta Qwen3.5 4B, 75.06. Bolt orada önde değil. Tablodaki IFBench de bu kartın iddiası.

| | Nanbeige4.3-33B | Nemotron 3.5 Bolt E4B |
|---|---|---|
| Parameters | 33B | 8B (4B effective) |
| License | Apache 2.0 | OpenMDW-1.1 |
| Context | 512K tokens | 64K in, 64K out |
| Built for | Coding and office agents | Local voice and device assistants |
| Headline claim | Terminal-Bench 2.1: 80.9 | IFBench: 63.79 (base Gemma 4 E4B: 42.84) |
| Released | 24 to 25 Oct (Hugging Face) | 23 Oct (Hugging Face, build.nvidia.com) |

## 🇸🇪 İsveç hangi sohbet penceresini kapattı?

Bugün, 26 Ekim pazartesi, Regeringskansliet iş bilgisayarlarında ChatGPT ve Claude web arayüzünü kapatıyor. İsveç'in hükümet ofisleri. [SVT](https://www.svt.se/nyheter/inrikes/ai-tjanster-sparras-pa-regeringskansliet) 23 Ekim'de yazmış, 24 Ekim'de güncellemiş. Kaynak [Sveriges Radio Ekot](https://www.sverigesradio.se/artikel/chat-gpt-och-claude-forbjuder-regeringskansliet). Personel, onaylı Microsoft Copilot'a gidiyor. Güvenliği bir incelemeden sonra yükseltilmiş. Modeller Intric üzerinden açık. SVT'ye giden e-posta bunu söylüyor. Kapanan yer tarayıcı penceresi.

LiteLLM çizelgesinden sonra agent araçlarındaki kendi token'larıma bakacağım. Henüz bakmadım.

## Kaynaklar

[LiteLLM kök neden yazısı](https://docs.litellm.ai/blog/security-incident-oct-21-2026-attack-chain)
[LiteLLM olay yazısı](https://docs.litellm.ai/blog/security-incident-oct-21-2026)
[Block Dessa](https://block.xyz/dessa)
[The Verge](https://www.theverge.com/ai-artificial-intelligence/1017906/jack-dorsey-block-dessa-ai-voice-speech)
[Nanbeige4.3-33B](https://huggingface.co/Nanbeige/Nanbeige4.3-33B)
[Nemotron 3.5 Bolt E4B](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Bolt-E4B-BF16)
[SVT](https://www.svt.se/nyheter/inrikes/ai-tjanster-sparras-pa-regeringskansliet)
[Sveriges Radio](https://www.sverigesradio.se/artikel/chat-gpt-och-claude-forbjuder-regeringskansliet)
