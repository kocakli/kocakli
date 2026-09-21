---
title: "Açık görüntü ağırlıkları, Google’ın ajan runtime’ı ve para işinde tökezleyen AI"
slug: "ai-gundemi-21-eylul-2026-qwen-image-ax-runtime"
yoast_title: "Qwen Image 2.1, Google AX ve hatalı AI para tavsiyeleri"
yoast_metadesc: "Qwen Image 2.1 açık ağırlıklarla geldi. Google AX ajanlara kontrol katmanı sunarken, finans testinden hayli kötü sonuçlar çıktı."
focus_keyphrase: "Qwen Image 2.1"
excerpt: "Bugünün AI gündeminde Qwen’in 7B görüntü modeli, Google’ın açık ajan runtime’ı, Pirate Face’in BitTorrent tracker’ı, finans testleri ve Trump’ın AI Force önerisi var."
---

Pazartesi dosyasının başına Qwen Image 2.1 yerleşti: 7 milyar parametre, doğal RGBA desteği ve açık ağırlıklar. Fakat ticari kullanım için ayrıca izin gerekiyor. Google’ın AX adlı ajan runtime’ı altyapı tarafını hareketlendirirken, Saturn’ün finans araştırması günün tatsız hesabını çıkardı: 18 model, 121 sorunun ortalama yüzde 57’sinde yanlış yanıt verdi.

## 🎨 Qwen Image 2.1 şeffaflığı modelin içine aldı

Qwen ekibi, Qwen-Image-2.1’i 20 Eylül’de yayımladı. [Hugging Face’teki model kartına ve lisansına](https://huggingface.co/Qwen/Qwen-Image-2.1) göre 7B parametreli model, 32 Single-Stream DiT katmanından oluşuyor; hem metinden görüntü üretme hem de mevcut görüntüyü düzenleme işini üstleniyor.

Benim dikkatimi çeken taraf RGBA desteği oldu. Şeffaf zemine sahip görseli doğrudan üretebiliyor, şeffaf katmanları düzenleyebiliyor ve fotoğraftaki bir nesneyi arka plandan ayırabiliyor. Düzenleme sırasında en fazla 10 referans görüntü kabul ediyor. Çember, boyalı işaret ya da ayrı bir maske ile değiştirilecek bölgeyi göstermek mümkün. İnsanların ve ürünlerin kimliğini koruma iddiası da kartta özellikle anılmış. Diffusers tarafındaki sınıfın adı `QwenImage21Pipeline`; örnekler arasında 2048×2048 çıktı ve daha geniş oranlar var.

Buradaki “açık” sözcüğünü biraz dikkatli okumak gerekiyor. Qwen Research License yalnızca ticari olmayan kullanıma izin veriyor. Üründe kullanmak isteyenlerin Hangzhou Tongyi Laboratory Technology Co., Ltd. ile ayrı lisans anlaşması yapması şart. Ağırlıklar erişilebilir, ticari haklar değil. Üstelik birincil belgede doğrulanmış karşılaştırma tablosu bulunmadığı için ortalıkta dolaşan benchmark puanlarını buraya taşımıyorum.

## ⚙️ Google AX ajanlara Kubernetes usulü düzen getiriyor

Google, [AX’i (Agent Executor)](https://github.com/google/ax) “açık agentic orchestrator” olarak tanımlıyor. Apache-2.0 lisanslı depo araştırma sırasında yaklaşık 3.819 yıldızdaydı; son güncellemesi 20 Eylül tarihliydi. Kullanım biçimi Kubernetes’e aşina olanlara yabancı gelmeyecek: İş yükü `ax.io/v1alpha1` YAML dosyasıyla tanımlanıyor; `ax apply`, `watch`, `ssh`, `suspend` ve `resume` gibi komutlarla yönetiliyor.

Sistemin dört temel parçası var. `Task`, CPU ve bellek sınırı bulunan yalıtılmış sandbox’ı kuruyor. `Workspace`; Git depolarını, MCP sunucularını ve skill’leri bir araya getiriyor. `Gateway`, dışarıya açılabilecek host’ları allowlist ile sınırlıyor. `Model` ise platformdaki LLM’i Kubernetes secret’larında tutulan kimlik bilgileriyle bağlıyor. Üretim için önerilen yol Agent Substrate’i Kubernetes üzerinde çalıştırmak; kontrol katmanı `ax-system` namespace’ine kuruluyor.

Dünkü [ajan sandbox dosyasında](https://www.oguzhan.co/tr/ai-gundemi-20-eylul-2026-ai-ajan-sandbox/) gördüğümüz sorunun altyapıdaki karşılığı tam da bu: Güçlü bir ajana güzel arayüzden önce sınır, ağ kuralı ve yaşam döngüsü yönetimi lazım. Google yüksek yoğunluk, checkpoint ve boşta duran ajanı bir saniyeden kısa sürede geri getirme sözü veriyor. Bunlar şirketin ürün iddiaları. README’de projenin erken geliştirme aşamasında olduğu, kararlı sürümden önce büyük kırılmalar yaşanabileceği ve dışarıdan pull request kabulünün geçici olarak durdurulduğu da açıkça yazıyor. Boyası kurumamış ama borular doğru yerde.

## 🏴‍☠️ Pirate Face model dosyalarına tracker ekledi

Açık ağırlıkların tek bir merkezde durması tuhaf bir çelişki. O depo silindiğinde “açık” dosyayı bulmak bir anda zorlaşabiliyor. Pirate Face, izin veren Hugging Face modelleri için SHA-256 ile doğrulanan BitTorrent magnet bağlantıları hazırlıyor; BEP-19 web seed’leri de asıl dosyaya işaret ediyor. [20 Eylül güncellemesiyle](https://pirateface.co/how-it-works) kendi tracker’ını ve DHT keşfini devreye aldı. Kaynak ortadan kalksa bile peer’ler birbirini bulabilecek.

Magnet’lerde bildirilen adres `udp://tracker.pirateface.co:6969/announce`. Tracker yalnızca eşleri buluşturuyor, ağırlıkları kendi üzerinden aktarmıyor. Pirate Face, Apache-2.0 veya MIT lisanslı 669 binden fazla modelin sisteme uygun olduğunu söylüyor. Bu sayı, 669 bin tam yedek var demek değil. 20 Eylül’de görülen 4.891 “witnessed record” da sürüm ve checksum kaydı; depolanmış dosya ya da çalışan seeder kanıtı sayılmaz.

Model yüzlerce gigabayta ulaştığında aradaki fark büyüyor. Pirate Face kendi altyapısındaki magnet’i listeden çıkarabilir, seed etmeyi bırakabilir. Bağımsız kullanıcıların indirdiği kopyaları geri çağıramaz. Dağıtık kalıcılığın iyi tarafı da zor tarafı da aynı cümlede.

## 💸 AI para sorularında hesabı tutturamadı

İngiltere merkezli fintech Saturn, ChatGPT, Claude, Copilot, Grok ve Gemini’nin de bulunduğu 18 modele 121 finans sorusu yöneltti. Eylül tarihli [Artificial Authority araştırmasında](https://www.saturnos.com/report/artificial-authority) ortalama yanlış yanıt oranı yüzde 57 çıktı. Çok adımlı, zor sorularda hata yüzde 88’e yükseldi; bazı modeller bu grubun yüzde 99’unu kaçırdı.

Ücret ödemek tabloyu düzeltiyor ama kurtarmıyor: Ücretsiz modeller yüzde 63, ücretliler yüzde 49 hata yaptı. Hesaplama yanlışları, güncel vergi değişikliklerini atlama, var olmayan kurallar uydurma ve risk uyarısını unutma sık görülen sorunlar arasında. Rapordaki bir emeklilik vergisi hatası, kullanıcıya 17.500 sterlinlik HMRC ödemesi çıkarabilirdi.

FCA araştırmasına göre İngiltere’deki tüketicilerin yüzde 26’sı genel amaçlı AI araçlarına finans tavsiyesi konusunda güveniyor. Tehlikeli eşleşme burada. [Claude, GPT ve Gemini’yi işe göre seçme rehberimde](https://www.oguzhan.co/tr/claude-gpt-gemini-karsilastirma-hangi-is/) model seçimini pratik açıdan ele almıştım; Saturn’ün çalışması ise finans için daha sert bir sınır çiziyor. Chatbot soruyu hazırlamaya yardım edebilir. Güncel mevzuat, kontrol edilmiş hesap ve sorumluluğu belli insan denetimi olmadan para tavsiyesi veremez.

## 🏛️ Trump bir “AI Force” ve AI czar istiyor

ABD Başkanı Donald Trump, 20 Eylül’de Truth Social üzerinden bir “AI Force” kurmak ve başına “AI czar” atamak istediğini duyurdu. [The Verge’ün aktardığına göre](https://www.theverge.com/ai-artificial-intelligence/997867/trump-ai-force-ai-czar) bunu Space Force ile kıyasladı; yönetimin sektörün büyümesini hiçbir şekilde engellemeyeceğini söyledi.

Ortada henüz takvim, aday ya da çalışma planı yok. Trump, czar görevi için “Yalnızca yüksek IQ’lu kişiler başvursun” notunu da düşmüş. Şimdilik Washington’dan gelen mesaj hızlanma ve yeni bir tabela. Aynı gün bir tarafta ajanların ağ erişimini sınırlayan runtime, diğer tarafta yanlış finans yanıtlarının dökümü var. Tabeladan sonraki iş listesi epey uzun.
