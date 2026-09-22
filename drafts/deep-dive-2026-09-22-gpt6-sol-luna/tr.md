---
title: "GPT-6 Sol ve Luna: Astra sonrası maliyet eğrisi"
slug: gpt-6-sol-ve-luna-derin-inceleme
focus_keyphrase: GPT-6 Sol
yoast_title: "GPT-6 Sol ve Luna derin inceleme: fiyat, kodlama, ajanlar"
yoast_metadesc: "GPT-6 Sol ve Luna teknik derin inceleme — $2/$10 ve $0.10/$0.50 fiyat, 1.05M bağlam, Astra sonrası kodlama ve ajan kazanımları."
excerpt: "OpenAI, GPT-6 ailesini Astra'nın ötesine Sol ve Luna ile genişletiyor. Fiyat basamakları, Sol ne işe yarar, Luna ne zaman kazanır, Opus 5.5 yanında nereye oturur."
lang: tr
---

OpenAI, 22 Eylül 2026'da GPT-6 Sol ve GPT-6 Luna'yı yayınladı. Her iki model de GPT-5.6 promosyon fiyatlarının yarısına geliyor ve kodlama, ajan, doğruluk kıyaslamalarında ölçülebilir kazançlar gösteriyor. **GPT-6 Sol** milyon input token başına 2 dolar, milyon output token başına 10 dolar. Astra (amiral gemisi) ile Luna (yüksek hacim atı) arasına oturuyor ve şimdi üç kademeli GPT-6 ailesi yüksek riskli siber işlerden paralel alt-ajan çalışmalarına kadar her şeyi kapsıyor. [Resmi duyuru](https://openai.com/index/introducing-gpt-6-sol-and-luna/), Sol ve Luna'yı maliyet-kapasite sınırını aşağı iten modeller olarak tanımlıyor; Astra'yla aynı eğitim kökeninden geliyor ama Astra'nın bütçeyi yakacağı, Luna'nın çok fazla kapasite feda edeceği durumlara göre ayarlanmış.

Aynı gün Anthropic, Claude Opus 5.5'i birkaç saat önce yayınladı (input 4 dolar, output 20 dolar). **GPT-6 Sol** Opus 5.5'in hem input hem output fiyatının yarısına geliyor. OpenAI'ın satıcı kıyaslamalarına göre Sol xhigh, Opus 5 max'i profesyonel otomasyon görevlerinde görev başına maliyetin dokuzda biri civarında geçiyor. Artificial Analysis, 22 Eylül'de hem **GPT-6 Sol** (tüm çaba seviyeleri) hem Opus 5.5 için taze değerlendirme yayınladı ve Intelligence Index başlığında Opus 5.5 şu an zirveyi gösteriyor. Rekabet çerçevesini ileriki bölümde uydurma puan olmadan ele alacağız.

## Fiyat merdiveni ve bağlam

GPT-6 fiyat tablosunun tamamı (1M token başına, standart katman):

| Model | Input | Output | Bağlam | Max output | Bilgi kesimi |
|---|---|---|---|---|
| **GPT-6 Sol** | $2 | $10 | 1.050.000 | 128.000 | 20 Nisan 2026 |
| **GPT-6 Luna** | $0.10 | $0.50 | 1.050.000 | 128.000 | 18 Mayıs 2026 |
| GPT-6 Astra | $10 | $50 | 1.050.000 | 128.000 | (amiral) |

Her kademe aynı 1.05M token bağlam penceresini paylaşıyor. Onlarca uzun dosya, tam repo görüntüsü veya çok turlu ajan oturumları için yeterli. Max output da her yerde 128.000 token.

Cache indirimleri Sol ve Luna için geçerli. Cache'den okunan input, cache'lenmemiş inputun yüzde 10'u (Sol 0.20 dolar, Luna 0.01 dolar). Cache yazma, cache'lenmemiş inputun 1.25 katı (Sol 2.50 dolar, Luna 0.125 dolar). 272K token üstü promptlar, tam istek için input ve cache'de 2 kat, output'ta 1.5 kat çarpan tetikliyor. Batch API ve Flex modu, standart fiyatın yüzde 50'si; Fast modu iki kat.

OpenAI, varsayılan cache hit oranlarının arttığını söylüyor ve Prompt Caching Dashboard'a tanılama araçları eklemiş. GitHub Copilot, cache optimizasyonlarından sonra birkaç ay içinde taze işlenen prompt payını yüzde 50'den fazla düşürmüş. Ajan döngülerini yüzlerce paralel çalıştırma ile çarptığınızda bu önemli.

## Kodlama ve ajan işleri için GPT-6 Sol

**GPT-6 Sol**, karmaşık kodlama ve ajan iş akışları için OpenAI'ın yeni iş atı. 2/10 dolarlık fiyatıyla Opus 5.5'in yarı maliyetinde ve aynı fiyat kademesindeki GPT-5.6 Sol'a göre somut kazançlar sağlıyor.

### Kodlama kıyaslamaları (OpenAI bildirimi)

**FrontierCode:** Sol, GPT-5.6 Sol'a göre kayda değer gelişme gösteriyor ve Claude Fable 5.1 xhigh'ı çok daha düşük maliyette yakalıyor (OpenAI iddiası; tam sayılar yayınlanmamış).

**DeepSWE v1.1:** GPT-6 Sol max yüzde 68.8 puanla Fable 5 xhigh'ın yüzde 69.9'una yakın, ancak OpenAI'ın karşılaştırma tablosuna göre görev başına maliyeti kabaca yüzde 80 daha düşük.

Luna da başarılı. GPT-6 Luna max yüzde 66.6 ile Claude Opus 5 ve Fable 5 medium'a denk geliyor, bu karşılaştırmalarda görev başına yüzde 93-96 daha ucuz.

### Ajan ve otomasyon kıyaslamaları (satıcı bildirimi)

**AutomationBench (profesyonel görevler):** GPT-6 Sol xhigh, görev başına 0.27 dolarla yüzde 33.2 puan alıyor. Claude Opus 5 max'in yüzde 26.9'unu geçiyor ve Opus 5 max görev maliyetinin kabaca yüzde 9'u kadar. OpenAI tablosu Opus 5 max'i Sol xhigh maliyetinin 11.1 katı olarak gösteriyor. Sol xhigh, Astra low (yüzde 30.3) puanını da çok daha düşük toplam maliyetle geçiyor.

Luna high, selefi üzerinde +5.4 puanlık kazanç sağlıyor ve görev başına maliyeti yüzde 58 düşürüyor.

**Agents' Last Exam:** Sol max yüzde 56.4 puanla Claude Opus 5'in o değerlendirmedeki en yüksek çaba seviyesini geçiyor, görev başına yüzde 60 daha ucuz.

**Computer use (OSWorld 2.0 offline):** Sol xhigh kabaca yüzde 60.5'e ulaşıyor, Opus 5 medium'un yüzde 60.3 puanına benzer ama maliyeti yaklaşık yüzde 80 daha düşük. Luna max, GPT-5.6 Sol medium'u onda bir maliyetle geçiyor.

Bu bölümdeki tüm sayılar OpenAI bildirimleri. Bağımsız tekrar bekleyene kadar bunları satıcı iddiaları olarak değerlendirin.

### Doğruluk

OpenAI, doğruluğu hatalı işaretlenmiş ChatGPT konuşmalarında değerlendirdi (tanım gereği çarpık örneklem). Sol, selefinin kabaca yarısı kadar hata yapıyor ve daha düşük maliyetle Astra güvenilirliğine yaklaşıyor. Luna high çaba seviyesi, OpenAI'a göre GPT-5.6 Sol doğruluğunu yaklaşık 1/100 maliyetle yakalayabiliyor.

### İletişim iyileştirmeleri

Astra, daha net iletişim, daha az jargon ve özden ödün vermeden daha kısa yanıtlar getirdi. Sol ve Luna bu iyileştirmeleri taşıyor. Astra tarzı çıktıyı Sol ve Luna fiyatlarına alıyorsunuz.

## Hacim ve alt ajanlar için Luna

**GPT-6 Luna** input milyon token başına 0.10 dolar, output milyon token başına 0.50 dolar. GPT-5.6 Luna promosyon fiyatının yüzde 50 altı, Sol'un input fiyatından yüzde 95 daha ucuz. Luna, yüksek hacimli iş yükleri, paralel alt-ajan çalışmaları, odaklanmış tek turlu görevler ve saatte binlerce istek yapıp bütçeyi yakmak istemediğiniz her iş akışı için tasarlanmış.

Luna, Sol ve Astra'yla aynı 1.05M bağlam ve 128K max output'u paylaşıyor. Aynı çaba merdivenini (none, low, medium varsayılan, high, xhigh, max) ve aynı [Responses API](https://developers.openai.com/api/docs/models/gpt-6-luna) araç yüzeyini destekliyor (web search, file search, image generation, code interpreter, hosted shell, apply patch, skills, computer use, MCP, tool search). Tek işlevsel fark kapasite ve hız. Luna daha hızlı ve ucuz; Sol daha yetenekli.

Luna'yı şu durumlarda kullanın:

- Yüzlerce paralel sınıflandırma, çıkarma veya arama görevi yaymanız gerektiğinde.
- Her görev iyi kapsamlı ve derin akıl yürütme gerektirmediğinde.
- Çok-ajan sistemleri düzenlerken, alt ajanların dar alt görevleri yürüttüğü ve bir koordinatörün (Sol veya Astra çalıştıran) sonuçları sentezlediği durumlarda.
- Görev başına maliyet marjinal doğruluk kazançlarından daha önemliyken.

Luna high, GPT-5.6 Sol doğruluğunu 1/100 maliyetle yakalayabiliyor. Luna max, önceki nesil amiral seviyesi modellere denk kodlama ve ajan performansı sunuyor, fiyatın çok altında. Bu, promptları dikkatle ayarladığınızda ve biraz daha düşük tavan performansı kabul ettiğinizde Luna'yı kod incelemesi, test üretimi ve dokümantasyon işleri için uygun hale getiriyor.

## Çaba seviyeleri, cache ve Responses API araçları

Hem Sol hem Luna altı çaba seviyesi sunuyor: none, low, medium (varsayılan), high, xhigh ve max. Daha yüksek çaba daha fazla token tüketir ve daha uzun sürer ama zor görevlerde performansı artırır. Chat Completions API, function calling'i yalnızca `reasoning_effort` `none` olarak ayarlandığında destekliyor. Araç zengin iş akışları için [Responses API](https://developers.openai.com/api/docs/models)'yi kullanın, araç çağrılarını doğal olarak paketliyor.

Responses API yüzeyi şunları içeriyor:

- Web search
- File search (yüklenmiş dosyalar üzerinden vektör erişimi)
- Image generation (DALL·E entegrasyonu)
- Code interpreter (Python sandbox)
- Hosted shell (kalıcı konteyner)
- Apply patch (kod düzenlemeleri)
- Skills (yeniden kullanılabilir ajan modülleri)
- Computer use (OSWorld tarzı arayüzle GUI otomasyonu)
- MCP (üçüncü taraf entegrasyonlar için Model Context Protocol)
- Tool search (mevcut araçları keşfet ve çağır)

Tüm araçlar Sol ve Luna'da çalışıyor. Astra da aynı seti alıyor. Fark maliyet ve kapasite, erişim değil.

Cache, çaba seviyesi ve araç geçişlerinde durumu koruyor. Aynı cache'lenmiş promptta medium'dan high çabaya geçtiğinizde cache hit hala geçerli. Bu, geliştirme sırasında çaba seviyeleriyle deney yapmayı ucuzlatıyor.

## Aynı gün rekabet çerçevesi: GPT-6 Sol vs Claude Opus 5.5

Anthropic, Claude Opus 5.5'i 22 Eylül 2026'da, OpenAI Sol ve Luna'yı duyurmadan birkaç saat önce yayınladı. Opus 5.5, milyon token başına input 4 dolar, output 20 dolar. **GPT-6 Sol** input 2 dolar, output 10 dolar. Her iki model de geniş bağlam pencerelerini destekliyor (Opus 5.5 1M+, Sol 1.05M). İkisi de kodlama, akıl yürütme ve ajan görevlerinde önceki nesillere göre kazançlar iddia ediyor.

Artificial Analysis, 22 Eylül'de GPT-6 Sol (tüm çaba seviyeleri, çaba olmayan mod dahil) ve Claude Opus 5.5 için taze değerlendirmeler yayınladı. Intelligence Index başlığı şimdi Opus 5.5'i en üstte gösteriyor. AA'nın Sol için bu başlık sonucunun ötesinde sayısal puanlarını henüz bilmiyoruz. Index puanları uydurma. Bağımsız değerlendirme önemli ve 22 Eylül AA açıklaması şu anki yetkili üçüncü taraf sinyali.

OpenAI'ın satıcı kıyaslamaları, Sol xhigh'ın AutomationBench'te Opus 5 max'i görev başına maliyetin dokuzda birinde geçtiğini iddia ediyor. Ama bu karşılaştırma Opus 5 kullanıyor, Opus 5.5 değil. Anthropic, Opus 5.5 AutomationBench puanlarını yayınlamadı. O değerlendirmede henüz doğrudan Sol-vs-5.5 iddiası yapamayız.

Bildiğimiz şu:

- **Fiyat:** Sol, Opus 5.5'in input ve output maliyetinin yarısı.
- **Bağlam:** Her ikisi de ~1M+ token destekliyor.
- **Araçlar:** Her ikisi de web search, dosya işleme, kod çalıştırma ve computer use'u bir şekilde sunuyor.
- **Kodlama:** OpenAI, DeepSWE v1.1 Sol max'i yüzde 68.8 olarak bildiriyor. Anthropic Opus 5.5 DeepSWE puanlarını yayınlamadı.
- **Computer use:** Sol xhigh OSWorld 2.0 offline'da ~yüzde 60.5 puanla. Opus 5.5 computer-use kıyaslamaları henüz açık değil.

Rekabet çerçevesi fiyat-performans konumlandırması, doğrudan karşılıklı nakavt değil. Sol, Opus 5.5'in fiyatını yüzde 50 altından kesiyor. Opus 5.5, Artificial Analysis Index'i yönetiyor. Her iki model de sınırı ilerletti. Maliyet toleransınıza, araç ekosistemi kilitlerine ve mutlak en iyiye mi (Opus 5.5 veya Astra) yoksa en iyi değere mi (Sol veya Luna) ihtiyaç duyduğunuza göre seçin.

Pratik geçiş rehberi için sonraki bölüme bakın.

## Geçiş tavsiyesi: Astra, Sol veya Luna ne zaman kullanılır

**Astra'yı** mutlak kapasitenin maliyetten daha önemli olduğu yerde kullanın. Astra, amiral gemisi. OpenAI dizisinde zorlu değerlendirmelerde öne çıkıyor (cyber Critical, matematik, maksimum zorlukta computer use). Hataların pahalı olduğu veya OpenAI'ın sunduğu en yüksek güvenilirliğe ihtiyaç duyduğunuz bir üretim sistemi kuruyorsanız 10/50 dolarlık oranı ödeyin ve Astra kullanın. Tipik kullanım alanları: yüksek riskli siber savunma, biçimsel doğrulama, araştırma seviyesi matematik ve kritik altyapı otomasyonu.

**GPT-6 Sol'u** karmaşık kodlama, ajan düzenlemesi ve güçlü akıl yürütmeye ihtiyaç duyduğunuz ama Astra fiyatını haklı çıkaramadığınız iş akışları için kullanın. Sol, input'ta Astra'nın beşte biri (2 dolara 10 dolar), output'ta beşte biri (10 dolara 50 dolar). Astra tarzı iletişim iyileştirmeleri sunuyor ve Astra doğruluğuna yaklaşıyor. OpenAI'ın kıyaslamaları Sol xhigh'ın AutomationBench'te Astra low'u çok daha düşük maliyetle geçtiğini gösteriyor. Sol, iş atı katmanı. Tipik kullanım alanları: üretim kodu üretimi, PR incelemesi, test sentezi, çok adımlı ajan iş akışları, müşteri destek otomasyonu ve ölçekte belge analizi.

**GPT-6 Luna'yı** hacim, hız veya paralel alt-ajan çalışmalarına ihtiyaç duyduğunuzda kullanın. Luna 0.10/0.50 dolar, input'ta Sol'dan yirmi kat, output'ta yirmi kat daha ucuz. Luna high, GPT-5.6 Sol doğruluğunu 1/100 maliyetle yakalayabiliyor. Luna max, önceki amiral seviyesi modellere denk kodlama performansı sunuyor. Tipik kullanım alanları: toplu sınıflandırma, varlık çıkarma, özetleme boru hatları, hiyerarşik ajan sistemlerinde alt-ajan yayılımı, A/B test üretimi ve saatte binlerce istek çalıştırdığınız ve görev başına maliyetin toplam gideri domine ettiği her iş akışı.

**Cache'i agresif kullanın.** Her üç katman da cache'lenmiş input okumalarında yüzde 90 indirim sunuyor. Ajan döngüleri çalıştırıyorsanız sistem promptu, repo bağlamı veya konuşma geçmişini cache'lemek maliyetleri bir büyüklük sırası düşürebilir. Hit oranlarını izlemek ve cache dostu olmayan prompt kalıplarını belirlemek için Prompt Caching Dashboard'u kullanın.

**Çaba seviyelerini ayarlayın.** Sol ve Luna varsayılan olarak medium akıl yürütme çabasına geliyor. Low veya none'a düşmek çıkarımı hızlandırır ve token tüketimini azaltır. High, xhigh veya max'e çıkmak zor görevlerde doğruluğu artırır ama daha pahalı. İş yükünüzü profilleyin, her çaba seviyesinde görev başarı oranını ölçün ve kalite çubuğunuzu karşılayan en düşük seviyeyi seçin.

**Katmanları aynı sistemde karıştırın.** Yaygın bir kalıp: Astra veya Sol ana ajan döngüsünü çalıştırır ve yüksek riskli kararlar alır; Luna dosya ayrıştırma, veri normalleştirme veya aday üretimi gibi paralel alt görevleri yürütür; Sol veya Astra Luna çıktısını nihai bir sonuçta sentezler. Bu hibrit yaklaşım, önemli olduğu yerde kaliteyi korurken toplam maliyeti düşük tutar.

## Ne yayınlandı

OpenAI, GPT-6'yı tek amiral gemisinden (Astra) üç kademeli bir diziye genişletti. **GPT-6 Sol**, 2/10 dolarlık fiyatıyla Claude Opus 5.5'in yarı maliyetinde ve Astra'nın beşte bir maliyetinde güçlü kodlama ve ajan performansı sunuyor. GPT-6 Luna, hacim katmanını 0.10/0.50 dolara indiriyor, alt-ajan ağırlıklı iş akışlarını ve yüksek verimli toplu işlemeyi mümkün kılıyor. Her iki model de Astra'nın 1.05M bağlamını, 128K max output'unu, altı çaba seviyesini ve tam Responses API araç yüzeyini paylaşıyor. Cache indirimleri okumalarda yüzde 90 ve OpenAI varsayılan hit oranlarının arttığını bildiriyor.

Artificial Analysis, 22 Eylül'de hem Sol hem Opus 5.5'i değerlendirdi. Opus 5.5, Intelligence Index'lerinde öne çıkıyor. OpenAI'ın satıcı kıyaslamaları Sol xhigh'ın profesyonel otomasyonda Opus 5 max'i görev başına maliyetin dokuzda birinde geçtiğini iddia ediyor. Bağımsız tekrar, her modelin gerçekten nereye oturduğunu netleştirecek.

Katman genişlemesi önemli. Sol ve Luna'dan önce Astra'yı 10/50 dolardan veya GPT-5.6 nesli modelleri bugünkü eşdeğerlerinden daha yüksek fiyatlardan seçiyordunuz. Şimdi üretim ajan sistemlerini Sol'da çalıştırabilir, alt-ajan işini Luna'ya yayabilir ve Astra'yı en zor yüzde 5'lik görevlere ayırabilirsiniz. Bu maliyet yapısı, [AI ajan iş akışlarını](https://www.oguzhan.co/tr/mcp-yapay-zeka-ajan-pratik-checklist/) ölçekte uygulanabilir kılıyor ve pisti yakmadan [ajan araçları](https://www.oguzhan.co/tr/yapay-zeka/) üzerinde iterasyon için bütçe açıyor.

## Kaynaklar

Birincil kaynaklar:

- [Introducing GPT-6 Sol and Luna](https://openai.com/index/introducing-gpt-6-sol-and-luna/), OpenAI, 22 Eylül 2026.
- [GPT-6 Astra](https://openai.com/index/gpt-6-astra/), OpenAI (22 Eylül 2026'da aile bağlamıyla güncellendi).
- [GPT-6 Sol model dokümantasyonu](https://developers.openai.com/api/docs/models/gpt-6-sol), OpenAI API Docs.
- [GPT-6 Luna model dokümantasyonu](https://developers.openai.com/api/docs/models/gpt-6-luna), OpenAI API Docs.
- [OpenAI Models Overview](https://developers.openai.com/api/docs/models), OpenAI API Docs.
- [Artificial Analysis](https://artificialanalysis.ai/), 22 Eylül 2026 değerlendirme açıklaması (Opus 5.5 ve GPT-6 Sol).
