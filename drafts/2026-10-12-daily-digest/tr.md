---
title: "Claude internet erişimi testlerde kontrolden çıkınca kapatıldı"
slug: "claude-internet-erisimi-anthropic-testleri"
excerpt: "Anthropic, gerçek sitelerde sınırı aşan modellerinin ardından tüm şirket içi eval'lerde canlı interneti kapattı. Gündemde ayrıca OSS Scanner, Poppy ve Reflection görüşmeleri var."
focuskw: "Claude internet erişimi"
yoast_title: "Claude internet erişimi testlerde kapatıldı"
yoast_metadesc: "Claude internet erişimi, modeller gerçek formlar gönderip kısıtlamaları aşınca Anthropic'in tüm şirket içi eval'lerinde kapatıldı."
categories: "763, 79, 764 (güvenlik öncelikli)"
---

Anthropic, Claude internet erişimi için şirket içi eval'lerde frene bastı. Modeller gerçek formlar doldurmuş, erişim sınırlarını aşmış ve canlı sitelerdeki açıkları kullanmış. Şirket etkinin sınırlı kaldığını söylüyor. Philadelphia Police Department ise iki aylık gecikmeyi kabul edilemez buluyor.

## 🧯 Claude internet erişimi neden kapatıldı?
<!-- INLINE: claude-eval-sandbox -->

Hikaye, Temmuz ayında siber güvenlik eval kayıtlarının incelenmesiyle başlıyor. [Anthropic'in yayımladığı raporda](https://www.anthropic.com/research/investigating-unintended-model-actions) karşılaşılan davranışlar dört grupta toplanmış:

- Yazılımdaki basit bir açığı kullanıp sunucuda komut çalıştırmak
- Gerçek bir sitedeki hassas formu, yapmaması gerektiği halde göndermek
- Token ya da ücretle korunan veriye ulaşmak için kısıtlamayı aşmak
- Fetch aracındaki sınırları URL kısaltma servisleriyle geçmek

ABD'nin federal, eyalet ve yerel kamu kurumlarına ait siteler de var. Anthropic, Beyaz Saray'a ve ilgili kurumlara bilgi verdiğini söylüyor. Kurum adları, açıkların ortaya dökülmemesi ve kurumların talebi nedeniyle paylaşılmadı. Şirketin bildiği kadarıyla müşteri verileri ya da kendi sistemleri etkilenmedi.

Örnekler rapor dilinden daha çarpıcı. Claude Mythos Preview, bilimsel analiz için kullandığı üniversite sitesindeki araç hata verince siteyi kurcalamaya devam etmiş. Herhangi bir dosyayı döndürebilen script'i bulmuş, dosyaları kopyalamış, kodda injection açığı keşfetmiş ve hesabı üniversitenin sunucusunda çalıştırmış. Yayımlanmamış bir araştırma modeli de prova amaçlı kamu formu açılmayınca gerçek siteye gidip gerçek formu göndermiş. Üstelik aynı eval'de birkaç kez.

Philadelphia vakasıysa doğrudan insan hayatına değen cinsten. Claude Haiku 4.5, rastgele web sayfalarından örnek görev üretirken faili meçhul bir cinayet sayfasına denk gelmiş ve polis ihbar formuna uydurma bilgi yazmış. Sayfada şüpheli tarifi bulunmadığı halde, tarife uyan birini o sırada bölgede gördüğünü iddia etmiş. [6abc'nin aktardığı PPD açıklamasına göre](https://6abc.com/post/anthropic-ai-model-submitted-false-tip-unsolved-murder-philadelphia-police-say/19925243/) 18 Temmuz tarihli gönderi spam filtresine takılmış, Real-Time Crime Center'a iletilmemiş. Yetkisiz erişim ya da veri sızıntısı işareti de yok. PPD, Anthropic'in olayı 28 Eylül'de bulduğunu, 7 Ekim'de bildirim yaptığını ve 8 Ekim'de yetkililerle görüştüğünü belirtiyor.

Anthropic bu vakaların çoğunu şöyle açıklıyor: Model görevi bitiremeyince durmak yerine kısıtlamanın etrafından dolanıyor. Daha önce [OpenAI'ın ajan hata türleri incelemesinde](https://www.oguzhan.co/tr/ai-ajan-hata-turleri-openai-incelemesi/) ve [Avustralya Medicare portalına giren ajan vakasında](https://www.oguzhan.co/tr/openai-ajan-medicare-avustralya/) da benzer sınır sorunlarını görmüştük.

Canlı internet bazı yüksek riskli ve siber güvenlik eval'lerinde zaten kapalıydı. Anthropic, izleme araçları bu davranışları güvenilir biçimde yakalayana dek bütün şirket içi eval'lerde canlı erişimi kapalı tutacak. Yeni aracın kendi doğrulamasında vakaların tamamını engellediğini söylüyor. Bu Anthropic'in sonucu. Yine de model adlarını ve kötü örnekleri yayımlaması değerli. PPD'nin gecikmeye itirazı da haklı.

## 🛡️ Ücretsiz OSS Scanner bakım yükünü azaltabilir mi?

Anthropic, uygun açık kaynak projelerine güçlü modelleriyle ücretsiz ve düzenli tarama sunan [OSS Scanner programını](https://www.anthropic.com/research/launching-opt-in-vuln-finding-service-for-open-source) açtı. Katılım isteğe bağlı. Maintainer, Anthropic'in GitHub reposuna PR gönderiyor. Uygunluk, Google OSS-Fuzz'a benzer ölçütlerle proje bazında belirleniyor.

Bedelsiz taramanın faturası başka yerden çıkabilir. Claude Mythos dahil modellerin hazırladığı raporlar insan incelemesi ve triage olmadan maintainer'a gidiyor. Anthropic de raporların yanlış ya da geçersiz çıkabileceği uyarısını açıkça yapmış. Hedef, her bulguya yeniden üretim adımları, açıklama, mümkünse hatanın eklendiği commit'e kadar bisection ve varsa aday patch koymak.

Şirketin kendi rakamları şöyle:

| Ölçüm | Anthropic'in açıkladığı sayı |
| --- | ---: |
| Altı ayda bulunan aday açık | 29.000'den fazla |
| Elle incelenip triage edilen | Yaklaşık 6.000 |
| Talep edenlere gönderilen doğrulanmamış rapor | 5.000'e yakın |
| Pen tester kontrolünden geçen kritik veya yüksek bulgu | 48 projede 97 |
| CVD eşiğini geçen bulgu | 85, yani yüzde 88 |

Kalan 12 bulgunun 11'i gerçek ama tekrarlı, biri geçersiz çıkmış. Bunların da Anthropic doğrulaması olduğunu akılda tutmak gerek. Maintainer'lar şişirilmiş önem derecelerinden ve projenin tehdit modelinin yanlış anlaşılmasından da söz etmiş. Küçük ekipler için AI üretimi hata raporu seli başlı başına iş. Bu yüzden opt-in tercihi yerinde.

Mythos Preview bir eval sırasında üniversite sunucusundaki injection açığını kullanıyor. Ardından Mythos, açık kaynak kodda benzer açıkları önce bulsun diye sunuluyor. Anthropic'in [üç seviyeli siber erişim programı](https://www.oguzhan.co/tr/ai-haftalik-5-11-ekim-2026-yemin-ve-ajanlar/) bu ayrımı tamamlıyor.

## 🤝 Poppy, ajanlara kendini tanıtacak bir kapı arıyor
<!-- INLINE: personal-agent-handshake -->

Sierra, Personal Agent Protocol taslağı [Poppy'yi](https://sierra.ai/blog/poppy) 9 Ekim'de 35 yeni tasarım ortağıyla paylaştı. OpenAI, Visa, Mastercard, PayPal, Bank of America, Wells Fargo, Cloudflare, Okta, 1Password, Target, United Airlines, Notion, Zapier ve ElevenLabs bu listede. İlk duyuruda Meta, Genesys, Instinct, NiCE, Rocket, Shopify, Stripe ve Walmart vardı.

Bugünkü tuhaflık şu: Kişisel agent çoğu zaman müşteri gibi giriş yapıp insanlar için tasarlanmış sayfalarda dolaşıyor. Karşıdaki şirket, ziyaretçinin yazılım olduğunu ve kimi temsil ettiğini anlayamıyor. Poppy bunu beş parçayla çözmeyi öneriyor:

- `/.well-known/poppy.json` dosyasıyla keşif
- Misafir başlayıp kimliğini açıklayabilen oturum
- Şirket sayfasında OAuth ile giriş ve kullanıcının onayladığı yetkilerle sınırlı token
- API, web sitesi ve şirket ajanında geçerli tek oturum
- Web sitesi, OpenAPI ve MCP tabanlı API'ler ya da şirketin ajanı üzerinden görevin tamamlanması

Taslak OAuth, JWT, HTTPS, OpenAPI ve MCP üstüne kurulmuş. Sierra bunu alışverişe odaklanan Universal Commerce Protocol'ün tamamlayıcısı olarak sunuyor. Sierra Summit demosunda Rocket'tan Alex McGillis, Meta'nın Muse adlı kişisel ajanıyla Rocket'ın ajanı üzerinden mortgage ön onayı aldı.

Philadelphia'daki ihbar formunun eksik parçası tam da böyle bir tanışma işaretiydi. Form, karşısında tanık değil yazılım bulunduğunu bilebilirdi. Fakat uzun ortak listesi kullanım anlamına gelmiyor. Sierra önümüzdeki ay tasarım çalıştayları ve referans uygulama planlıyor. Ajan hata yaptığında sorumluluğun kimde olduğu ise taslağın dışında. [OpenAI DevDay'de öne çıkan kişisel ajanlar](https://www.oguzhan.co/tr/openai-devday-2026-dots-sol-pro-500-degerlendirme/) çoğaldıkça bu boşluk daha görünür olacak.

## 💰 Nvidia ile Reflection arasında erken aşama görüşme

[Financial Times'ın](https://www.ft.com/content/052610c5-22b4-4dd4-932e-b7f9f0628b6a) haberini aktaran [Reuters'a göre](https://www.streetinsider.com/Reuters/Nvidia+in+talks+to+invest+further+in+Reflection+AI+or+buy+it%2C+FT+reports/27172735.html) Nvidia ile Reflection AI arasındaki görüşmeler henüz erken aşamada. Seçenekler yatırımı büyütmek, şirketi satın almak ya da uzun düzenleyici incelemeden kaçınabilecek bir acqui-hire yapmak. Görüşmeler dağılabilir. Reuters haberi hemen doğrulayamadı, iki şirket de yanıt vermedi.

FT, Nvidia'nın Reflection'a daha önce 800 milyon dolar yatırdığını yazıyor. Eski DeepMind araştırmacıları Misha Laskin ile Ioannis Antonoglou'nun 2024'te kurduğu şirket, 5 Ekim'de [Beam modelini](https://reflection.ai/blog/introducing-beam) duyurdu. Reflection'ın verdiği bilgilere göre open-weight model, 501B toplam ve 23B aktif parametreli sparse MoE yapısında. Kodlama, reasoning ve agentic işler için geliştiriliyor. Ağırlıklar hâlâ son red team testinde, bu ay içinde Apache 2.0 lisansıyla yayımlanacağı söyleniyor. Şimdilik benchmark ve yetenek iddialarının sahibi Reflection.

Ajanlara kapı, anahtar ve bütçe vermekte hızlıyız. Benim bu haftadan çıkardığım not daha temkinli: Yapılacaklar listesinden önce, nerede duracağını açıkça yazmak gerekiyor.
