---
title: "Gemini 4 Argon önce siber savunmacılara açıldı"
slug: "gemini-4-argon-once-siber-savunma"
excerpt: "Google, Gemini 4 Argon'u ücretli müşterilerden önce seçili siber savunma ekiplerine veriyor. Gündemin devamında protein filigranı, Codex Security ve yaptırımı olmayan Beyaz Saray mutabakatı var."
focuskw: "Gemini 4 Argon"
yoast_title: "Gemini 4 Argon önce siber savunmacılara açıldı"
yoast_metadesc: "Gemini 4 Argon önce siber savunmacılara gidiyor. SynthID proteinlere inerken Codex Security GitHub'ı izliyor, FTC ise şirketlerin kapısını çalıyor."
categories: [763, 79, 764]
---

Google, Gemini 4 Argon'u önce seçili siber güvenlik ekiplerine açıyor; ücretini ödeyen API müşterileri sırasını bekleyecek. Benim için duyurunun asıl haberi benchmark tablosu değil, bu sıra. Bugünün diğer üç gelişmesi de aynı sorunun çevresinde dönüyor: Güveni kim vaat ediyor, kim ölçüyor, gerektiğinde kim hesap soruyor?

## 🛡️ Gemini 4 Argon'un ilk durağı Fairwind
<!-- INLINE: argon-fairwind -->

Google DeepMind, [Gemini 4 Argon'u 30 Eylül'de duyurdu](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-4-argon/). Chief AI Architect Koray Kavukcuoglu'nun açıklamasına göre model önce Fairwind Programı içindeki güvenilir siber savunma ekiplerine dağıtılıyor. Google ayrıca ABD'nin gönüllü yayın öncesi model erişimi sürecine katılmış. Ücretli API müşterileri ile Google AI Ultra aboneleri daha sonra gelecek; takvim şimdilik yok.

Argon'un hedefi tek promptluk kısa cevaplar değil. Google; gerçek yazılım projeleri, hukuk ve finans araştırmaları ile siber savunma gibi uzun soluklu işleri sayıyor. Önceki yaklaşık 64 bin tokenlık çıktı sınırı 1 milyona çıkmış. Tanıtım döneminde 1 milyon input token 2 dolar, output ise 10 dolar. Cache içinden kullanılan input yaklaşık yüzde 95 indirimli. Sonrasında fiyatlar 4 ve 20 dolara yükselecek.

Şirketin kendi benchmark tablosunda Argon, GPT-6 Astra, Claude Fable 5.1 ve Claude Opus 5.5'ı birçok testte geçiyor; her testte değil. Üreticinin karnesini yine üreticinin doldurduğunu unutmayalım. Daha ilginç iddia Wiz'den: Argon'un, diğer frontier modellerin kaçırdığı hastane bağlantılı kritik bir açığı bulduğu aktarılıyor. Fakat ayrıntılar yayımlanmadığı için sonucu bağımsız biçimde sınamak mümkün değil.

Fairwind daha önce Gemini 3.8 Flash Cyber ve CodeMender ile açılmıştı. Programa CrowdStrike ve Palo Alto Networks dahil 650'den fazla kuruluşun katıldığı bildiriliyor. Yakın zamanda [model erişiminin Washington tarafından ülke sırasına bağlandığını](https://www.oguzhan.co/tr/washington-ingiltere-aisi-model-erisimi/) görmüştük. Araç kullanan agent'ların sınır ihlalleri de [Avustralya'da Senato gündemine kadar çıktı](https://www.oguzhan.co/tr/avustralya-altman-amodei-senato-openai-freni/). Şimdi baskı, doğrudan ürünün dağıtım planına girmiş halde. “Henüz kullanamazsınız” cümlesi bu lansmanın dipnotu değil, başlığı.

## 🧬 SynthID Bio, filigranı laboratuvara taşıyor
<!-- INLINE: synthid-bio -->

DeepMind'in aynı gün tanıttığı [SynthID Bio](https://deepmind.google/blog/introducing-synthid-bio/), yapay zekanın tasarladığı biyolojik koda fark edilmesi güç bir imza yerleştiriyor. İmza, protein fiziksel olarak sentezlendiğinde de doğrulanabiliyor; laboratuvar testlerine göre işlevi bozmuyor. Amino asit dizilerinde eşdeğer seçimler yönlendiriliyor, tahmin edilen 3D yapılarda ise atom koordinatları küçük ölçülerde ayarlanıyor.

Islak laboratuvar deneyi burada belirleyici. AlphaProteo ve SynthID uyarlanmış ProteinMPNN ile üretilen filigranlı protein bağlayıcılar; VEGF-A, SARS-CoV-2 spike RBD ve PD-L1 hedeflerinde filigransız örneklerle benzer başarı oranı, bağlanma gücü ve dizi çeşitliliği vermiş. Yapı tarafında AlphaFold 3'ün diffusion ağının küçük bir bölümü fine-tune edilerek koordinatlara tespit edilebilir imza eklenmiş.

Bunun pratik karşılığı DNA sentezi taraması olabilir. Tarama hizmeti, bir dizinin güvenlik önlemleri bulunan modelden geldiğine dair makineyle okunabilir işaret görebilir. PDB, UniProt ya da GenBank'a giren AI üretimi kayıtları ayırmak da mümkün olabilir. Yine de filigran, dizinin zararsız olduğunu kanıtlamaz; niyet okumaz, değiştirilmiş her örneği yakalayamaz. Peynirin yeni bir güvenlik dilimi diyelim, tamamı değil.

Stanford'daki Hie lab ile Arc Institute yöntemi Evo 2'de deniyor. Filigranlı bakteriyofaj genomunun ilk bakteri kültürü testlerinde işlevsel faj ürettiği belirtiliyor. DeepMind makaleyi, kodu, in vitro verileri ve model ağırlıklarını araştırmacılara açacağını söylüyor. Görseldeki filigran tartışması böylece petri kabına kadar uzandı.

## 🔧 Codex Security, GitHub nöbetini sürekli hale getiriyor

OpenAI, Codex Security Cloud'u talep üzerine tarama yapan bir araçtan bağlı GitHub repolarını ve yeni commit'leri sürekli izleyen bir hizmete çeviriyor. [Kurulum belgelerindeki akış](https://developers.openai.com/codex/security/setup) açık: şüpheli açığı araştır, izole ortamda doğrula, yamayı hazırla ve insan onayına sun. Production kodunu kendiliğinden değiştirmiyor.

Yerel kullanım ve CI için Codex Security CLI da var. Daybreak Blue savunma modelleri Cloud sürümüne eklenmiş. OpenAI'ın Ağustos güvenlik güncellemesinde verdiği rakamlar hayli büyük: 30 binden fazla kod tabanında 30 milyonun üzerinde commit incelenmiş; 500 binden fazla bulgu otomatik olarak, 70 binden fazlası da insanlar tarafından giderilmiş şeklinde işaretlenmiş.

Hizmet halen research preview aşamasında. ChatGPT Enterprise, Edu, Business ve Pro hesaplarına açık; bugün yalnızca GitHub Cloud destekleniyor. Sürekli tarama faydalı, fakat hatalı bulgunun ve kötü yamanın maliyetini de büyütür. Merge kararının insanda kalması bu yüzden önemli. Aynı haftada Google modeli kimin kullanacağını sınırlıyor, OpenAI modelin önereceği düzeltmenin son düğmesini insana bırakıyor.

## 📜 Beyaz Saray sözü verdi, FTC dosya istedi

29 Eylül'deki Beyaz Saray toplantısının ardından altı isim Frontier Responsibilities ortak taahhüdüne imza attı: Sundar Pichai, Dario Amodei, Mark Zuckerberg, Greg Brockman, Elon Musk ve Jensen Huang. Metin; şirket içi kontrol ve tespit sistemleri, bağımsız dış değerlendirme ve bunları yürüten ekipler için yönetim kurulu gözetimi istiyor. Donald Trump anlaşmayı “ahlaken bağlayıcı” diye tarif etti; [The Verge'ün haberinde](https://www.theverge.com/ai-artificial-intelligence/1002584/trump-us-ai-safety-deal-self-regulation-tech-execs) ayrıntılar var.

Hukuken bağlayıcı değil. Yaptırım yok, son tarih yok, denetçinin adını ya da raporunu kamuya açıklama zorunluluğu yok. Şirket yönetimi bir süreci denetleyebilir, kamuoyu da o sürece dair hiçbir şey görmeyebilir.

Ertesi gün başka türden bir belge haberi geldi. [Reuters'a göre](https://www.reuters.com/business/ftc-opens-probe-into-ai-giants-including-anthropic-openai-new-york-post-reports-2026-09-30/) FTC; son siber olayların ardından ürün güvenliği ve tüketicinin korunması konusunda Anthropic, OpenAI ve başka şirketlere resmi bilgi talepleri göndermeye hazırlanıyor. Bunlar mahkeme celbine benzer güce sahip civil investigative demand belgeleri. Bloomberg, FTC Başkanı Andrew Ferguson'ın Beyaz Saray toplantısında da bulunduğunu yazıyor.

Ben bu iki adımı tek bir güvenilirlik dosyası olarak okuyorum. Gönüllü mutabakatta şirketler verecekleri sözü kendileri tarif ediyor. FTC ise şirket sunumlarının dışında kayıt oluşturabilecek sorular soruyor. İkisi de tek başına güvenli agent garantisi değil; fakat yalnızca biri cevap vermeyi zorunlu kılabilir.

Savunmacılara öncelik, proteinin içine imza, repolarda sürekli nöbet ve hukuki gücü olmayan bir Beyaz Saray sözü. Gerçek güvenlik araçlarıyla duyuru gürültüsü aynı pakette geliyor. Ben araca bakarım; kimin doğrulayabildiğini ve resmi dosyaya ne girdiğini de ayrıca not ederim.
