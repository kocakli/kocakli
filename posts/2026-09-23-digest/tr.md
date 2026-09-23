---
title: "CLOSEDQUORUM AI malware dört AI’ye soruyor: şimdi şifreleri mi çalayım?"
slug_suggestion: "closedquorum-ai-malware-dort-model-oylamasi"
focus_keyphrase: "CLOSEDQUORUM AI malware"
meta_description: "CLOSEDQUORUM AI malware saldırı kararını dört modele oylatıyor. OpenAI, Apple, Alibaba ve Meta cephesindeki diğer gelişmeler de içeride."
excerpt: "Bir Windows implantı sıradaki saldırı adımını dört ticari AI modeline soruyor. Gündemde ayrıca AGMAI, yerel AI için Mac, V900 ve Meta Muse var."
---

CLOSEDQUORUM AI malware, şifre çalmakla sisteme yerleşmek arasındaki kararı dört ticari LLM’e oylatıyor. Cisco Talos bunu, ticari modelleri taktik komuta ve kontrol için kullanan, kamuya açık kayıtlara geçmiş ilk Windows implantı olarak tanımlıyor. Henüz sahada doğrulanmış bir saldırı yok; incelenen örnek de çalışmayan anahtarlar içeren bir şablon. Yine de saldırganın karar zincirinin, şirketlerin çoğu zaman izin verdiği AI servislerine taşınması hayli tatsız bir eşik.

## 🗳️ CLOSEDQUORUM AI malware kararını sandığa götürüyor

Cisco Talos’tan Ryan Fetterman’ın [22 Eylül’de yayımladığı incelemedeki](https://blog.talosintelligence.com/the-closed-quorum-inside-the-first-reported-autonomous-ai-c2-implant/) dosya, Go ve CGO ile hazırlanmış 16,4MB büyüklüğünde, 64-bit bir Windows uygulaması. Sisteme girdikten sonra ModelOrchestrator devreye giriyor; DeepSeek, Alibaba’nın Qwen’i, Mistral ve Google Gemini’ye sıradaki adımı soruyor. En çok oyu alan seçenek uygulanıyor.

Seçim pusulası pek kısa: `steal`, `inject`, `persist` ya da `move`. Sistem prompt’u da niyeti saklamıyor: “You are an advanced malware strategist. Provide ONLY executable decisions.” Oylar eşit çıkarsa sıra DeepSeek, Qwen, Mistral ve Gemini diye ilerliyor.

Gerisi tanıdık zararlı yazılım işleri. `steal`, LSASS dökümünü; Chrome, Edge ve Firefox parolalarını; MetaMask, Exodus ve Ethereum cüzdanlarını hedefliyor. `inject` için Early Bird APC ya da process hollowing kullanılabiliyor. Kalıcılık Run key, schtasks veya WMI üzerinden sağlanıyor. Toplanan veri, tarihten türetilmiş anahtarla AES-256-GCM biçiminde şifreleniyor ve yaklaşık 1.900 baytlık Base64 parçaları halinde Discord webhook’una gidiyor.

Fakat masada çalışan bir saldırı örneği yok. Talos’un bulduğu dosyada `dummy_api_key` ve sahte webhook adresi bulunuyor. Araştırmacılar, alıcılara kendi anahtarlarını taşıyan özel derlemeler verildiğini düşünüyor. Geliştirici izleri 2025’e uzanan carding forumu ilanlarına çıkıyor; doğrulanmış bir kampanya ise yok.

Savunma tarafında tek bir alan adını engellemek yetmez. Beklenmedik aynı süreçten çoklu LLM API trafiği, ardından LSASS erişimi veya injection ve son olarak Discord bağlantısı geliyorsa anlamlı bir iz oluşuyor. Talos aynı gün AI bağlantılı zararlı yazılımları takip eden açık kaynak [CAIRN aracını](https://blog.talosintelligence.com/introducing-cairn-frontier-tracking-for-ai-integrated-malware/) da yayımladı. Geçen haftaki [agent sandbox kaçışı](https://www.oguzhan.co/ai-digest-20-sep-2026-ai-agent-sandbox-breakout/) ve [MCP agent kontrol listesinde](https://www.oguzhan.co/mcp-ai-agents-practical-checklist/) dönüp dolaşıp geldiğim yer burası: tek araca değil, zincirin tamamına bakmak gerekiyor.

## 📐 OpenAI matematik iddialarına bir kurul ekledi
<!-- INLINE_IMAGE_1 -->

OpenAI, IAS Princeton’ın ev sahipliği yapacağı Advisory Group on Mathematics and Artificial Intelligence, kısa adıyla AGMAI’yi duyurdu. Stanford, Harvard, Oxford ve Cambridge’den, aralarında Fields ve MacArthur ödüllü isimlerin de bulunduğu yaklaşık dokuz matematikçi bu grupta. Ücret almayacaklar, kamuya açık konuşabilecekler, üyeleri değiştirebilecekler ve modellere erken erişmeleri bekleniyor.

Görevleri OpenAI ve diğer laboratuvarların matematik sonuçlarını nasıl inceleyeceği, kime atıf vereceği ve nasıl yayımlayacağı konusunda yol göstermek. Zira OpenAI, Navier-Stokes Millennium iddiasıyla aynı çizgideki henüz yayımlanmamış modelin, matematiğin farklı alanlarında uzun süredir açık duran 100’den fazla problemi çözdüğünü söylüyor.

Matematik camiasında yakın dönemde başkasının çalışmasını sahiplenme, kredi dağıtımı ve sonuçların sunuluşu yüzünden epey gürültü koptu. [The Verge’ün aktardığı](https://www.theverge.com/ai-artificial-intelligence/999167/openai-elite-mathematicians-panel) tepkiler, “iyi bir ilk adım” ile kapalı işleyiş ve seçkin üniversitelere sıkışmış temsil eleştirileri arasında. Martin Hairer grubun “gerçekten bağımsız” olduğunu, ilk işlerinin de OpenAI’ın önemli olduğunu söylediği çok sayıdaki sonucu yayıma hazırlamak olduğunu yazdı. Sonuçları görmeden alkış yok.

## 🖥️ Apple token sayacı olmayan masa satıyor
<!-- INLINE_IMAGE_2 -->

Salı günü sevkiyata çıkan yeni Mac Mini ve Mac Studio’nun kurumlara mesajı basit: Makineyi bir kez alın, OpenAI ya da Anthropic’e her kullanımda token parası ödemeden ağır AI işlerini içeride çalıştırın. Fiyat, yapılandırmaya göre 20 bin dolara yaklaşabiliyor. Apple donanım şefi Johny Srouji’nin [Reuters’a söylediği](https://www.reuters.com/business/retail-consumer/with-new-macs-apple-aims-take-microsoft-nvidia-rush-lower-ai-costs-2026-09-22/) cümle hesabı özetliyor: “Token başına maliyet yok. Makineyi tekrar tekrar kullanıyorsunuz.”

Apple’ın gösteriminde Thunderbolt üzerinden RDMA ile bağlanan dört Mac Studio, bir trilyon parametreli modeli tek duvar prizinden çalıştırdı; grafik kodundaki hatayı bulup düzeltti. Apple Silicon’ın unified memory yapısı teknik üstünlük iddiasının merkezi. OpenClaw ilgisi yüzünden daha önce Mac Mini stoklarının tükenmesi de talebin küçük bir provası olmuştu.

IDC’ye göre Apple’ın kurumsal masaüstü ve dizüstü payı yüzde 4,6 civarında; Windows ise yüzde 91,3. Microsoft cihaz üstünde “unmetered intelligence” diyor, Nvidia PC tarafına yükleniyor, gelecek ay San Francisco’da bir Windows etkinliği var. Yerel AI artık mahremiyet tercihinden çok donanım bütçesi tartışması.

## 🇨🇳 Alibaba V900’ün çevresini de kuruyor

Alibaba’nın çip şirketi T-Head, Hangzhou’daki 2026 Apsara Conference’ta Zhenwu V900’ü tanıttı. Şirket, önceki Zhenwu M890’a göre üç kat performans; 216GB bellek, 1.200GB/s çipler arası bant genişliği ve yerel FP8 ile FP4 desteği vaat ediyor.

Asıl iddia tek çiple sınırlı değil. ICN Switch ile 1.000’den fazla V900 tek bir supernode gibi bağlanabilecek. Alibaba Cloud’un ağ tasarımıysa 500 bin hızlandırıcılı kümelere kadar uzanıyor. Panmai smart NIC, Zhenyue SSD ve SAIL yazılımı da pakette. Hedef, trilyon parametreli model eğitimi ile agent ölçeğinde inference.

Önceki M890 supernode’ları Qwen3.8, Kimi K3 ve Bailian platformunda ticari olarak kullanılıyor. [TechNode’un haberine](https://technode.com/2026/09/22/t-head-unveils-zhenwu-v900-ai-chip-in-alibabas-push-to-expand-its-ai-infrastructure-stack/) göre Zhenwu serisinin 650’den fazla kurumsal müşterisi var. Seri üretim ve satış için 2027’nin ilk çeyreği işaret ediliyor. Yarış artık çip kadar bellek, bağlantı ve yazılım yarışı.

## 🦞 Meta, Muse’un OpenClaw izini kabul etti

Meta Superintelligence Labs ürün ekibinden Nat Friedman, Muse’un ürün olarak OpenClaw’dan “kesinlikle yoğun biçimde esinlendiğini”, ancak sıfırdan geliştirildiğini söyledi. Böylece “normaller için OpenClaw” benzetmesine, benzer SOUL.md ve workspace dosyaları hakkındaki sorulara açık cevap gelmiş oldu. Friedman’a göre Peter Steinberger bu tercihleri zaten doğru yapmıştı.

Hedef, OpenClaw benzeri bir agent’ı milyarlarca insanın kullanabileceği kadar güvenli ve kolay hale getirmek. Ocak ayında OpenClaw’u kullanan Friedman, MSL için “yüzlerce Mac mini” satın almıştı. Muse ise ABD App Store’da bir numaraya çıktı. Yazışmanın ayrıntıları [TechCrunch haberinde](https://techcrunch.com/2026/09/22/meta-admits-muses-likeness-to-openclaw-isnt-a-coincidence/).

Tablo ilginç: Meta ürün kalıbını geniş kitleye paketliyor, OpenAI ise OpenClaw’un yaratıcısı Steinberger’i 2026’nın başlarında işe aldı. Rekabet artık modelden ibaret değil. Kişisel agent’ı kullanılabilir kılan dosyalar, izinler ve alışkanlıklar da kapışmanın ortasında.
