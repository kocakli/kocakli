---
title: "Claude Haiku 5.5 ile Fiyat Tabanı On Sente İndi"
slug: "claude-haiku-5-5-gpt-6-luna-fiyat-tabani"
excerpt: "Anthropic küçük model fiyatında GPT-6 Luna ile buluştu, ChatGPT görsel arayüze geçti, Microsoft yerel ajanlar için güçlü bir cihaz çıkardı."
focuskw: "Claude Haiku 5.5"
yoast_title: "Claude Haiku 5.5 ile Fiyat Tabanı On Sente İndi"
yoast_metadesc: "Claude Haiku 5.5, GPT-6 Luna fiyatına indi. ChatGPT Intelligent UI kazanırken Microsoft yerel ve sandbox içinde çalışan ajanları öne çıkardı."
categories: "763, 79"
---

Claude Haiku 5.5, bir milyon input token için on sentlik fiyatıyla GPT-6 Luna'nın yanına geldi. Ajan kuranların bütçesini asıl kemiren yüzlerce küçük çağrı artık hayli ucuz. Çarşamba gününe GPT-6, yerel çalışan Microsoft modelleri, herkese açılan SynthID ve OpenAI içindeki chain of thought tartışması da sığdı.

## 💸 Claude Haiku 5.5 ile küçük model fiyatı on sent
<!-- INLINE: haiku-price-floor -->

[Anthropic'in duyurduğu](https://www.anthropic.com/claude-haiku-5-5) tarife 100K token sınırına kadar şöyle: Bir milyon token için input $0,10, output $0,50, cache read $0,01. OpenAI'ın [GPT-6 Luna API fiyatı](https://developers.openai.com/api/docs/pricing) da aynı. İki şirket küçük modellerini tam olarak aynı etikete koydu.

Fakat 100K aşılınca hesap değişiyor. Haiku'nun input ücreti $0,50'ye, output ücreti $2,50'ye, cache read ise $0,05'e çıkıyor. Anthropic, Haiku 4.5 isteklerinin yaklaşık yüzde 90'ının bu eşiğin altında kaldığını söylüyor. Şirketin hesabına göre kısa istekler yüzde 90, yeni tokenizer hesaba katıldığında ortalama kullanım yaklaşık yüzde 75 daha ucuz. Önceki modelin fiyatı $1 ve $5'ti.

Kullanım listesinde özetleme, context compaction, veritabanı sorguları, sınıflandırma, müşteri desteği ve browser use var. [Opus 5.5](https://www.oguzhan.co/tr/claude-opus-5-5-derin-inceleme/) ya da Sonnet 5.5 altında dar görevli coding subagent olarak da çalışabiliyor. Ayarlanabilir effort seçeneği taşıyan ilk Haiku bu.

Anthropic'in kendi benchmark tablosunda OSWorld 2.1 offline sonucunu yüzde 72,4 görüyoruz. Luna yüzde 48,9, Sonnet 5.5 yüzde 83,9 almış. Terminal-Bench 4.0'da sıralama yüzde 39,2, yüzde 16,4 ve yüzde 70,6. Şirket, zor agentic coding işleri için Sonnet ve Opus'u öneriyor.

Benim çıkaracağım kullanım kuralı açık: Subagent promptlarını kısa tutun. Özet, arama ve [context compaction](https://www.oguzhan.co/tr/jev-context-compaction-aynen-budama/) çağrılarının maliyeti ciddi biçimde düştü. 100K çizgisini geçince fatura beş katına çıkıyor.

## 🧩 GPT-6 yanıtla birlikte arayüz de üretiyor

[GPT-6, 7 Ekim'de ChatGPT'ye geldi](https://openai.com/index/gpt-6-for-everyone/). Plus, Pro, Business ve Enterprise kullanıcıları Chat bölümünde GPT-6 Sol'u kullanıyor. Free ve Go hesaplarına bugünden itibaren GPT-6 Luna veriliyor. Work ve Codex modellerinde değişiklik yok.

Yeni Intelligent UI, düz metnin yanına görsel, buton, form, grafik ve küçük araçlar yerleştiriyor. Bu bileşenler model yanıt üretirken ekrana akıyor. OpenAI'ın örnekleri arasında hesap bölüştürücü, emeklilik hesabı, retro oyun ve harita üstünde rota var. Görselleri azaltmak mümkün. Şirket, modelin tasarım kararlarında daha yapacak işi olduğunu da kabul ediyor.

ChatGPT artık düşünürken yanıt vermeye başlayabiliyor. OpenAI'ın kendi web araması testinde GPT-6 Instant, GPT-5.6 Instant'a göre ortalama yüzde 44 daha erken yanıt yazmış. Güvenlik tarafında Astra çalışmalarından yararlanıldığı ve çok turlu jailbreak denemelerine karşı direncin arttığı söyleniyor.

Türkiye'de pek çok kişi için ChatGPT demek ücretsiz sürüm demek. Dolayısıyla model neslinin değişmesi önemli. O anda üretilen hesap araçları kullanışlı olabilir, ancak para hesabında çıkan her rakamı ayrıca kontrol ederim. Sol ve Luna'nın ayrıntıları için önceki [GPT-6 incelemesine](https://www.oguzhan.co/tr/gpt-6-sol-luna-derin-inceleme/) bakabilirsiniz.

## 💻 Microsoft yerel ajanları sandbox içine alıyor
<!-- INLINE: local-agent-sandbox -->

Microsoft, ["hybrid intelligence"](https://blogs.windows.com/windowsexperience/2026/10/07/building-windows-for-hybrid-intelligence/) yaklaşımında uygun işleri yerel makinede çalıştırıp gerektiğinde buluta gitmeyi öneriyor. Bunun donanımı Surface Laptop Ultra. NVIDIA RTX Spark, 128 GB'a kadar unified memory ve bir petaflopa kadar AI işlem gücü sunan cihaz $2.599'dan başlıyor, 16 Ekim'de sevk edilecek.

MAI Code 1.1 Flash toplam 137B, aktif 6,8B parametreli bir MoE model. Yaklaşık üç bite quantize edilmiş ve yerelde 256K context çalıştırabiliyor. Microsoft'un kendi Surface testinde tam context bellek kullanımı 75,5 GB'a ulaştı. Prompt işleme hızı 64K'da saniyede 923,5 token, 128K'da 769,8 token ölçülmüş. Yerel model çağrılarında inference ücreti alınmadığını da şirket söylüyor.

75,5 GB sayısı ürünü yerine oturtuyor. Bu, parasını baştan verdiğiniz özel bir geliştirici cihazı. Daha geniş kitleyi ilgilendiren yenilik MXC olabilir. Windows 11'de genel kullanıma açılan Microsoft Execution Containers, ajanın erişebileceği dosya ve ağları kurumun belirlemesini, bu sınırların çalışma anında uygulanmasını sağlıyor. Açık kaynak olan MXC farklı işletim sistemlerinde de çalışıyor.

Codex, GitHub Copilot, Replit ve LM Studio destek verenler arasında. Claude Code ise gelecekler listesinde. Yerel ajanların güven vermesi için erişim sınırı şart. Windows tarafındaki bu çözüm, [Apple Full Disk Access ve AI ajanları](https://www.oguzhan.co/tr/apple-full-disk-access-ai-ajanlari/) yazısında gördüğümüz izin kavgasının bir başka cevabı.

## 🔍 SynthID Detector herkese açıldı

Google, [SynthID Detector'ı](https://blog.google/innovation-and-ai/models-and-research/google-deepmind/synth-id-ai-content/) synthid.com adresinde dünya çapında kullanıma açtı. İngilizce arayüz, görsel, video ve ses dosyalarında Google ile ortakları OpenAI, NVIDIA ve Kakao'nun SynthID filigranını arıyor. Apple desteği yakında gelecek.

Google'ın verdiği sayılar epey büyük: 2023'ten bu yana 180 milyardan fazla görsel ve video ile 240 bin yıllık ses filigranlanmış. Search, Gemini ve Chrome içindeki doğrulama sistemi günde bir milyondan fazla istek alıyor.

Halka açık sürümün eli daha dar. [Ars Technica'nın aktardığına göre](https://arstechnica.com/ai/2026/10/google-rolls-out-improved-synthid-ai-content-detector-now-available-globally/) giriş yapmak gerekiyor, günlük yaklaşık 10 kontrol hakkı var, kurum içi araçtaki işaretli bölge gösterimi kaldırılmış. Microsoft ve Meta kendi filigran standartlarını kullanıyor. Bu araçlar da hatasız değil.

"SynthID bulunamadı" yanıtını, içeriği insan üretti diye okumam. Söylediği tek şey filigranın bulunamadığı. Yine de viral bir videoyu inceleyen gazeteci için birkaç şirketin izini tek yerde aramak faydalı. Günde 10 hakla haber merkezi altyapısı olmaz, ara sıra yapılacak kontrol için iş görür.

## 🧯 İşten çıkarılan araştırmacılar görünür muhakeme istiyor

OpenAI'ın geçen hafta işten çıkardığı Tomek Korbak, Mikita Balesni ve Jasmine Wang, yönetim kuruluna ve güvenlik komitelerine mektup gönderdi. [Wall Street Journal'ın aktardığı mektup](https://www.wsj.com/tech/ai/fired-openai-researchers-ask-company-to-preserve-visibility-into-ai-reasoning-987c8c94), modelin izlenebilirliğini daha da azaltacak adımlardan kaçınılmasını, bağımsız denetçileri ve açık bir güvenlik ekosistemini öneriyor.

Üç araştırmacı, işten çıkarmaların kalan çalışanları susturduğunu söylüyor. OpenAI ise kararın güvenlik kaygılarını dile getirmekle ilgisi olmadığını, hassas şirket bilgilerinin kullanımıyla ilgili olduğunu belirtti. Şirket içi bir yazıda önerilerle güçlü biçimde hemfikir olduklarını da kaydettiler. [Gizmodo'nun aktardığı](https://gizmodo.com/3-fired-openai-employees-write-plea-for-chain-of-thought-monitoring-to-be-preserved-2000823349) Astra system card ayrıntıları, bu model sınıfının saldırı koşullarında CoT izleyicilerinden kaçabildiğini söylüyor. Madem taraflar içerikte anlaşıyor, bunu sonraki system card içinde açık bir taahhüt olarak görmek isterim.

Çarşamba, ürün duyurusu kılığına girmiş bir fiyat günüydü. Küçük model çağrıları on sente indi, ücretsiz ChatGPT GPT-6'ya geçti, Microsoft peşin donanım bedelini karşılayana token sayacı olmayan bir seçenek sundu. Modelin düşüncesini görebilecek miyiz, sahte videoyu ayırt edebilecek miyiz soruları da biraz ilerledi. Şimdilik o kadarıyla yetiniyorum.
