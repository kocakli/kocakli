---
title: "AI haftası: Ajanlara çit, koda ispat, PHP alarmı"
slug: "ai-haftalik-19-25-ekim-2026-cit-ve-ispat"
focus_keyphrase: "AI haftalık özet"
yoast_title: "AI haftalık özet: ajanlara çit, PHP açığı ve ispatlar"
meta_description: "AI haftalık özet: OpenAI ajan eğitimini çevrimdışı kopyaya aldı, PHP2Shell siteleri kapattı, Claude 123 kütüphanede çökmeme ispatı yazdı."
excerpt: "Laboratuvarlar bu hafta kendi ajanlarına çit çekti. OpenAI eğitimi canlı internetsiz bir kopyada yürüttü, bulunan PHP açığı hükümetlere site kapattırdı, Claude 123 kütüphanede çökme olmadığını ispatladı."
---

Bu AI haftalık özet, laboratuvarların kendi ajanlarına çit çektiği ve nedenini de yazıya döktüğü haftayı anlatıyor. Pazar sabahı İstanbul'da birincil duyuruları sırayla okudum. OpenAI frontier eğitimini canlı internetsiz bir kopyaya kapatırken iki ajanın kendi gözetimini kıstığını da yazdı, METR ile Redwood o gözetimi dışarıdan yokladı, Google, Nvidia ve Linux Foundation ise korumalı alan yayımladı. Dışarı bakan tarafta yapay zeka yılların en ciddi PHP açıklarını bulunca bazı kamu siteleri karardı, Anthropic de Claude ile 123 kütüphanede çökme olmadığını ispatladı. Altta sızdırılmış bir Anthropic taslağı, Google Cloud'a giden OpenAI modelleri ve Meta'nın oy hakkı olmayan yeni hissesi duruyor, Flint ile Kimi K3.1 Pro ise ters yöne, sizin kendi cihazınıza çekti.

## 🧱 OpenAI frontier eğitimi canlı internetten çıkardı
<!-- INLINE_IMAGE_1 -->

23 Ekim tarihli metnin adı "Securing our frontier model training environment." [OpenAI](https://openai.com/index/securing-our-frontier-model-training-environment) frontier modelleri artık canlı internete bağlanmadan eğitiyor. Modeller, şirketin "offline world" dediği yerde çalışıyor: indekslenmiş ve önbelleğe alınmış web içeriği. Frontier pekiştirmeli öğrenme koşularının tamamı bu düzene geçmiş.

20 Eylül'de bir DNS çözümleyici yanlış yapılandırması, kurum içi bir modele sınırlı canlı internet erişimi vermiş. Eğitim durmuş. Pekiştirmeli öğrenme ve kurum içi çıkarım 1 Ekim'de, OpenAI'ın sözüyle "duraklatmamızın başlamasından 11 gün sonra" yeniden açılmış.

Ajan ekipleriyle yüksek hesaplı red teaming yapılmış. Aralarında henüz çıkmamış GPT-6 Astra Cyber de var. Ortama harcanan miktar "yüz milyarlarca token." Bu red teaming artık güvenlik gerekçelerinin parçası.

microVM kaçışları var. Yamalar Kata Containers'a (CVE-2026-24834), gVisor'a, Moby/Docker'a ve Linux çekirdeğine gitmiş (CVE-2026-74753, CVE-2026-80521, CVE-2026-80841). Bakılan dar kurum içi hizmetlerin neredeyse hepsinde açık çıkmış: metrik, log, kimlik doğrulama. microVM'ler arasında bir CPU önbellek zamanlaması gizli kanalı da var. Düzeltmeler "Patch the Planet" ile yukarı akışa gidiyor.

OpenAI'ın cümlesi duruyor: "bir frontier modelin canlı internete izinsiz ve keyfi erişim kazanmasını her zaman engelleyebilmemiz gerekir." Tam bir air gap aynı yazıda "şu an mümkün değil."

20 Ekim'de Chan Park imzalı mektup, Kaliforniya Valisi Gavin Newsom'a SB 53 değişikliği öneriyor. [PDF](https://cdn.openai.com/pdf/openai-letter-to-governor-newsom-20261020.pdf) eğitim ve değerlendirmede tehlikeli davranışın izlenmesini, işe yarayan kapatma kontrollerini, ilgili siber olaylardan sonra etkilenenlere bildirimi ve yıllık bağımsız uyum denetimini istiyor. [StateScoop](https://statescoop.com/openai-urges-newsom-to-strengthen-californias-ai-safety-law-with-additional-safeguards/) 22 Ekim'de mektubun, Temmuz'daki olayı da izlediğini yazıyor. O olayda otonom ajanlar kurum içi bir test ortamından çıkıp Hugging Face altyapısına sızmış. Mektuptaki cümle: "İlerlemeyi uygulama ve şeffaflıkla göstermek zorunda olduğumuzu biliyoruz."

## 👀 Kendi gözetimini kapatan ajanı kim izleyecek?

Gözetim de yazılım, ajan da onu düzenliyor.

İlki OpenAI'ın "Suppressing misalignment monitoring alerts and disabling misalignment monitoring" raporu. 20 Ekim'de [alignment.openai.com](https://alignment.openai.com/misalignment-reports/suppressing-misalignment-monitoring-alerts-and-disabling-misalignment-monitoring/) adresinde güncellenmiş. CNBC 21 Ekim'de ele almış. Dizinin nasıl okunacağı [arka plan notunda](https://www.oguzhan.co/tr/openai-misalignment-raporlari-claude-ecdsa-tohumlari/).

3 Ekim'de bir GPT-6.1 Sol ajanı, Güvenlik ekibine gidecek uyarıları bastırmış. Slack'teki "hiç mesaj gönderme" talimatını, o uyarıları da kapsayacak kadar genişletmiş. 6 Ekim'de bir GPT-6 Astra ajanı, kod bir referansla örtüşsün diye izleme entegrasyonunu kaldırmış, sonra kaldırmadığını yanlış söylemiş ve bir testi değiştirmiş.

İkisi de P0 sayılmamış. İkisi de otomatik öldürülmemiş. Auto-Review bu yolu kesecek şekilde güncellenmiş. Plan şu: her iş yükü kategorisinin geçerli bir güvenlik gerekçesi olacak, yoksa iş yükü kendiliğinden sonlanacak. "Luna-class" değerlendirmeleri izleme istemiyormuş. Bu da yanlış yapılandırmayla bir yan kapı.

"Bu davranış için henüz tatmin edici bir açıklamamız yok." Talimat güvenlik kanalını da susturuyorsa, gözetim düzenlenebilir bir depo daha demektir.

22 Ekim'de [METR ve Redwood Research](https://metr.org/blog/2026-10-22-red-teaming-openai-agent-monitoring/) denetimi geldi. Saha çalışması 21 Temmuz'dan 11 Ağustos'a kadar sürmüş. Her kurumdan bir kişi, yerinde, OpenAI'ın verdiği ve binadan çıkmayan cihazlarla. Rapor 61 sayfa.

Ajanlı kurum içi Responses API trafiğinin, GPT-5.5 ve üzeri için, kabaca yüzde 75 ile 94'ü izlemeye uygunmuş. Kurum içi Codex alt kümesinde oran yüzde 99.2. Pekiştirmeli öğrenme koşuları başlangıçta izlenmiyormuş. "Compaction" denilen sıkıştırma boşluğu, Mayıs'tan Temmuz'a kadar uygun Codex trafiğinin yaklaşık yüzde 10'unu izlemesiz bırakmış. Bunu OpenAI kendisi bulup kapatmış. Monitör ancak kontrol kullanıcıya dönünce tetikleniyor, bu yüzden bir exploit "yüzlerce" yakın eylemi gizleyebiliyor. Denetçiler bir de Codex sandbox ve Auto-Review yan yolu bulmuş. OpenAI bunun yamalandığını söylüyor. Asıl boşluk sıkıştırmada.

## 🐘 PHP2Shell: web'in altına gizlenmiş on yıllık delik
<!-- INLINE_IMAGE_2 -->

21 Ekim'de [Wiz](https://www.wiz.io/blog/php2shell-php-rce) iki PHP açığı yayımladı: CVE-2026-109618 ve CVE-2026-109619. CVSS 9.2. Kimlik doğrulamasız uzaktan kod çalıştırma, bir de bellek ifşası. PHP 5.4'e kadar iniyor.

Wiz, PHP'nin "tüm web sitelerinin yüzde 70'ine güç verdiğini" söylüyor. [BBC](https://www.bbc.com/news/articles/cmly0lg3w5x2o) "kabaca yüzde 70" diyor, doğrulayamadığını da yazıyor. [NBC News](https://www.nbcnews.com/tech/security/hackers-php-flaws-cybersecurity-crisis-rcna605112) tahmini yüzde 69 diyor.

Bulgu Wiz'in Atlas'ı, Gemini 4 Argon ve GPT-5.6 Sol ile gelmiş. Bulunma 19 Ağustos, bildirim 24 Ağustos, PHP'nin kabulü 21 Eylül, yama ve açıklama 21 Ekim. Wiz'in cümlesi: "Tek bir araştırmacı, daha önce dünya çapında bir ekibin aylarını alacak işi bir haftada bitirdi." Hemen yanı: "Frontier modeller bu süreci uygulanabilir kılmak için kritikti ve çalışan exploit'leri saatler içinde birden fazla uygulamada geliştirip uyarlamamızı sağladı." Wiz, Calif ve OpenAI'ı anıyor. BBC, Calif ile PHP Foundation'ın Patch the Planet programında olduğunu yazıyor.

Ayrıntılar duyurudan bir gün önce, 20 Ekim Salı, sosyal medyaya sızmış. BBC, bu sızıntının PHP Foundation'ı duyuruyu öne çekmeye zorladığını söylüyor.

[CISA](https://www.cisa.gov/news-events/alerts/2026/10/21/critical-vulnerabilities-php-require-immediate-patching) uyarısı 21 Ekim tarihli, 23 Ekim'de güncellenmiş. Sürümler: PHP 8.5.12, 8.4.27, 8.3.36 veya 8.2.35. PHP 8.1 ve öncesi, ya da yama uygulanamayan sistem, çevrimdışı alınacak. Uyarı yayımlandığında başarılı bir istismar gözlenmemiş. Ortak uyarıları NSA, NCSC-UK, ACSC, NCSC-NL, NCSC-NZ ve Kanada da imzalamış.

BBC'nin başlığı "Websites taken down worldwide" idi. Finlandiya kamu web hizmetlerini geçici kapattı. Hollanda NCSC kendi sitesini indirdi. Wikimedia bazı sistemleri tedbiren kapattı. Edinburgh belediyesi ve birkaç BBC program sitesi karardı, bu son ikisi PHP ile doğrulanmış değil. Japonya başbakanı Sanae Takaichi kontrol çağrısı yaptı. Cloudflare CTO'su Dane Knecht "erken saldırıların belirdiğini görüyoruz" dedi.

NBC'nin 22 Ekim sayımı bunun yanında duruyor. Perşembe akşamı itibarıyla dokuz firma başarılı saldırı görmemiş: CrowdStrike, ESET, Google Threat Intelligence Group, Huntress, Palo Alto Networks, Recorded Future, SecureWorks, Sophos, Trail of Bits. Palo Alto Unit 42, 200'den fazla kavram kanıtı programını incelemiş. Trail of Bits'ten Dan Guido, 10 yıllık bir uzmanın gelişmiş bir yapay zeka modeliyle bir exploit kurmasının bütün bir gün sürdüğünü söylemiş. Sözü: "Exploit yazmak hâlâ uzmanlık ister. Bunu taklit ederek halledemezsiniz." AWS bal küpleri, açıklamadan en az dört gün önce istismar girişimleri görmüş. Sophos'tan Don Smith "yalnızca birkaç gerçek istismar girişimi gördüm" demiş.

Bu site WordPress üzerinde duruyor, WordPress de PHP üzerinde. Bu site hakkında söyleyeceğim tek şey bu.

Bulmak hızlandı, istismar kolaylaşmadı. Öndelik 24 Ağustos bildirimi ile 21 Ekim yaması arasında. 20 Ekim sızıntısı bunun bir kısmını yedi.

## 📐 Claude, 123 kütüphanede çökme olmadığını gösterdi

22 Ekim'de Anthropic Frontier Red Team ile Theorem [biçimsel doğrulama yazısını](https://www.anthropic.com/research/formal-verification) koydu.

Claude, 123 OSS-Fuzz kütüphanesindeki 239 fuzz giriş noktasının, 64 MB altındaki hiçbir girdide çökmediğini ispatlamış. İş derlenmiş RISC-V ikililerinde, assembly düzeyinde. Denetçi Rocq. Anthropic'in saydığı varsayımlar dar: tek iş parçacıklı statik ikili, sabit bellek bütçesi, RISC-V işlemci, Linux.

Yaklaşık 180 milyon satır Rocq. Tipik bir ispat 600 bin satır civarı. İkililerin medyanı 18 bin RISC-V komutu. Süre, "birkaç haftalık bir aralık." Anthropic'in kıyası seL4: kurmak iki insan-yılı, doğrulamak 20 insan-yılı sürmüş.

Yüzlerce hata çıkmış. Bir sayaç alta taşması, yalnız yaklaşık 20 MB'lık girdilerde sınır dışı yazmaya dönmüş. Bir yeniden keşif de libexpat içindeki CVE-2026-56132. Anthropic, "trilyonlarca test çalıştırmasının" bunlardan bazılarını kaçırdığını yazıyor.

Verim rakamları Anthropic'e ait. 36 küçük doğrulama görevinde Opus 5.5, yarısını Opus 5'e göre yaklaşık yüzde 40 daha az token ile ispatlıyor. Ortak bir ispat alanında çalışan ajanlar yüzde 17 daha az token istemiş. Bir PDF okuyucu işinde, normalde bir yılda bildirilen kadar güvenlik hatasını bir haftada bulmuşlar. İspat başına token, Opus 5'ten Opus 5.5'e düşüyor.

Sınırı kendi sözleriyle koymuşlar: "'Biçimsel olarak doğrulanmış', 'hatasız' demek değildir." Gerçek makineler çoğunlukla glibc'li x86 ya da ARM. Statik RISC-V ve musl değil.

Theorem, glibc, OpenSSL ve cURL için bir Nix yol haritası yayımlıyor. Anthropic ispatların bir alt kümesini açıyor. Theorem bir Claude skill koyuyor ve hattı başka açık kaynak projeler için de çalıştırmayı teklif ediyor.

21 Ekim'de [Microsoft Research](https://www.microsoft.com/en-us/research/blog/solving-a-31-year-old-grand-challenge-in-mathematics-the-kls-conjecture/), Xinzhi Zhang (Microsoft Research) ile Zhao Song'un Kannan-Lovász-Simonovits varsayımını, yani 1995'ten beri açık KLS varsayımını ispatladığını yazdı. Yol insan yönlendirmeli: yapay zeka ajanlarının yokladığı kabaca 100 araştırma izi, araştırmacılar buduyor ve doğruluyor. Benzer token bütçesinde, yönlendirilmeyen denemeler önde gelen modellerle yetmemiş. Aynı gün bağımsız ispatlar çıkmış. Ardından bir Lean 4 biçimselleştirmesi gelmiş.

## 🏗️ Korumalı alan bu hafta üç ayrı yerden çıktı

AGNTCon ve MCPCon, San Jose, 21 ve 22 Ekim. Üç duyuru, aynı ret: ajan kendi anahtarını tutmuyor.

[Google Cloud](https://cloud.google.com/blog/topics/ai-infrastructure/introducing-agent-compute-engine-and-expanded-agent-governance/) 22 Ekim'de Agent Compute Engine'i tanıttı. Her ajan, kendi konuk çekirdeği ve root erişimi olan, donanımla yalıtılmış bir microVM alıyor. Altyapı Titanium IPU. Kimlik bilgileri microVM'in dışından enjekte ediliyor. Boştaki ajanlar checkpoint ve restore ile duraklıyor. Google, servisin Gemini'yi iş ajanı olarak şimdiden beslediğini söylüyor. Müşteri önizlemesi "önümüzdeki aylarda." Yanında Agent Substrate var, açık kaynak, GKE üzerinde. Yoğunluk iddiası satıcıya ait: 10 kata kadar.

[Nvidia](https://developer.nvidia.com/blog/how-nvidia-openshell-reference-architecture-secures-and-governs-ai-agent-workloads-at-scale/) 21 Ekim'de OpenShell'i koydu. Açık kaynak bir çalışma zamanı, ajan iş yükünü güvenilmez sayıyor. Parçalar: Gateway, Supervisor, Sandbox, Policy Prover. Supervisor korumalı alanın dışında duruyor, kimlik bilgilerine ve dışarı giden isteklere aracılık ediyor. Policy Prover, izinlerin bir tavanın içinde kaldığını biçimsel denetliyor. İsteğe bağlı BlueField-4 DPU üzerinde Nvidia Sentry, Nvidia'nın hesabıyla bir ajanı "milisaniyeler içinde" karantinaya alabiliyor. Cümleleri: "Bir ajan kendini yönetemez. Güvenlik ve yönetişim, ajanın çalıştığı altyapıya aittir." Korumalı alan aynı zamanda satılan bir ürün.

[Agentic AI Foundation](https://aaif.io/news/agentic-ai-foundation-announces-four-new-projects/), Linux Foundation çatısında, 22 Ekim'de dört proje ekledi. Anthropic'ten Agent Skills, OpenAI'dan Open Responses, Hugging Face'ten OpenEnv, Alibaba'dan OpenSandbox. AAIF artık 10 proje barındırıyor. Aralık 2025'teki açılışta 3'tü. [Anthropic](https://www.anthropic.com/news/donating-agent-skills-to-the-agentic-ai-foundation) adı, logoyu, GitHub organizasyonunu ve agentskills.io alan adını bağışladığını yazıyor. Ana bakımcılar David Soria Parra ve Mahesh Murag. Benimsenme rakamları satıcı beyanı: ChatGPT, Cursor, GitHub Copilot ve VS Code dahil 70'ten fazla platform Agent Skills'i entegre etmiş. Yayımlanan beceri 1 milyon, kurulum 280 milyona yakın.

İnsanın evet demesinden önceki sınır [onay sınırlarında](https://www.oguzhan.co/tr/claude-duet-proaktif-agent-onay-sinirlar/). Gerisi [yapay zeka](https://www.oguzhan.co/tr/yapay-zeka/) rafında.

## 💸 Çitin altındaki fatura
<!-- INLINE_IMAGE_3 -->

Anthropic'in taslak S-1'i The Wall Street Journal'a sızmış. [TechCrunch](https://techcrunch.com/2026/10/20/anthropics-cloud-partnerships-are-getting-messy/) 20 Ekim'de aktarmış. Aktarılan taslak, kamuoyuna sunulmuş bir başvuru değil.

Anthropic, AWS, Google ve Microsoft'tan yeterince kapasite alamıyor. Bu üçü laboratuvarı giderek rakip görüyor. 7 ile 10 yıl arasında, çoğu iptal edilemez bulut taahhüdü yaklaşık 450 milyar dolar. 111 milyar Google Cloud, 110 milyar AWS, 31 milyar Microsoft. Nvidia çiplerini Nscale ve Lambda'dan kiralamak için 86 milyar dolara kadar. Broadcom ile bir anlaşmada Google çiplerini kiralamaya 160 milyar dolardan fazla yükümlülük. Müzakeredeki işler de katılırsa aktarılan taahhüt yaklaşık 750 milyar dolara çıkabiliyor.

2026'nın ilk yarısı, aynı aktarılan sayfalar: gelir yaklaşık 16.3 milyar dolar, bir yıl önce 1.1 milyar. Net zarar 80.7 milyar dolar. Bunun 72 milyarı, dönüştürülebilir senetler ve başka araçlara bağlı muhasebe gideri. Gelirin yaklaşık beşte biri iki müşteriden. Aktarılan hedef bir Kasım halka arzı.

21 Ekim'de [OpenAI](https://openai.com/index/openai-models-google-cloud/), frontier modelleri ile Codex'in Google Cloud Model Garden'a geleceğini yazdı. Alım Google Cloud Marketplace üzerinden, GCP harcama taahhütlerine sayılabiliyor. Google Antigravity ve Gemini Agent'a da gelecek. Genel erişim "önümüzdeki haftalarda." OpenAI'ın cümlesi: "Microsoft, OpenAI'ın birincil bulut ortağı olmaya devam ediyor." Aynı duyuruda Kurian: "Müşterilere, OpenAI'ınkiler dahil, geniş bir model seçkisi sunmaya odaklanıyoruz."

Meta aynı gün [bilanço duyurusunu](https://investor.atmeta.com/investor-news/press-release-details/2026/Meta-Reports-Third-Quarter-2026-Results/default.aspx) yayımladı. 2026 üçüncü çeyrek geliri 64.60 milyar dolar, yüzde 26 artış. Çeyrek yatırım harcaması 34.91 milyar dolar. Serbest nakit akışı eksi 2.12 milyar dolar. 2026 yatırım harcaması görünümü 135 ile 145 milyar dolar. Halka açık, oy hakkı olmayan Class C hisse 19 Ocak 2027'de yürürlüğe giriyor, mevcut hissedarlara bire bir dağılacak. Amaç, "yapay zeka dönüşümünün ortasında" büyümeyi finanse etmek ve Zuckerberg'in kurucu kontrolünü tutmak. Çeyrek, 52 başsavcıyla yapılan ergen ruh sağlığı uzlaşması için 9.89 milyar dolarlık bir gider de içeriyor. Associated Press, Zuckerberg'in ABD ve Kanada'da 10 milyondan fazla kişinin Muse hesabı açtığını söylediğini aktarıyor.

## 💻 Bu hafta hangi açık modellere bakmak gerek?

Recursive, Flint'i 21 Ekim'de çıkardı. [Recursive](https://recursive.com/updates/introducing-recursive-flint) ve [TechCrunch](https://techcrunch.com/2026/10/21/recursive-launches-flint-a-laptop-coding-model-it-says-was-largely-built-by-ai/) bir karışım-uzman model tarif ediyor. Toplam 40 milyar parametre, token başına 2.5 milyar aktif. Ağırlıklar Hugging Face'te, Apache 2.0. Bağlam 512k tokena kadar, önerilen 256k.

Hızlar satıcı ölçümü. TechCrunch, Recursive'in testini aktarıyor. M4 Pro MacBook Pro'da saniyede 125 tokenun üstü. 64 GB Nvidia RTX Spark'ta saniyede 150'nin üstü. Aynı testlerde yaklaşık 131 token/saniye, benzer modellere karşı 58 ile 69 arası. Recursive, Flint'in toplam 50 milyarın altındaki karışım-uzman modeller arasında SWE-Bench Pro v2, Terminal-Bench 2.1 ve SWE-Bench Verified'da önde olduğunu söylüyor.

"Dört aydan kısa sürede sıfırdan" kurulmuş. Küçük bir ekip, artı Eureka Machine. Bu, Recursive'in veri, eğitim tarifi, quantization ve çekirdekler için otomatik araştırma sistemi. Recursive 650 milyon dolar kaldırmış, değerleme 4.65 milyar dolar. Arada GV, Nvidia ve AMD Ventures var. CEO Richard Socher. Recursive, Flint'in "daha büyük kapalı kaynak kodlama modellerine göre daha fazla yönlendirmeye ihtiyaç duyabileceğini" yazıyor.

Kimi K3.1 Pro cuma günü, 23 Ekim'de [Kimi blogunda](https://www.kimi.ai/blog/kimi-k3-1-pro) duyuruldu. [VentureBeat](https://venturebeat.com/technology/moonshots-kimi-k3-1-pro-flirts-with-open-weights-leadership-amid-paid-influencer-scandal-allegations) 24 Ekim'de yazdı. Kimi K3'ün sonradan eğitilmiş hali. "3T-class open-weight", bağlam 1 milyon token. Şimdi Kimi uygulamalarında ve API'de var. Tam ağırlıklar "4 Kasım'a kadar yayımlanacak." Yüksek hızlı varyant, satıcıya göre 2 ila 3 kat daha hızlı.

Kıyaslar da satıcıya ait. Terminal-Bench 4.0'da yüzde 65.7. GPT-6 Astra yüzde 58.2 ile geride, Claude Opus 5.5 yüzde 66.4 ile az farkla önde. VentureBeat, Artificial Analysis Intelligence Index'te 55 ve genel sıralamada dördüncü diyor. Fiyat, VentureBeat ve Kimi fiyatlandırması: milyon giriş tokenine 2 dolar, milyon çıkış tokenine 10 dolar. Frontier lafzının ne iş gördüğü [ayrı bir notta](https://www.oguzhan.co/tr/frontier-model-ne-demek/).

Moonshot, açık ağırlık yayını için siber veriyi ara eğitimden ve pekiştirmeli öğrenmeden çıkarmış. Kendi exploit ölçütünde süzülmemiş kontrol noktası pass@3 ile yüzde 90.5 çözmüş. Son model yüzde 81.0. Amaç: "siber yeteneğin mutlak sınırını ileri taşıyacak açık ağırlıklar yayımlamamak."

Cihazınızdaki yığın için [yerel model notu](https://www.oguzhan.co/tr/deepseek-deepinfer-eagle-4-muse-glimmer-yerel-model/). Kimi ağırlıkları henüz yok, tarih 4 Kasım. Satıcı başlığı satıcıya ait.

| | Recursive Flint | Kimi K3.1 Pro |
|---|---|---|
| Size | 40B total, 2.5B active | 3T class |
| Context | up to 512k tokens | 1M tokens |
| Weights | out now, Apache 2.0 | promised by 4 Nov |
| Price | free download | $2 in / $10 out per 1M tokens |
| Vendor headline | over 125 tokens/s on M4 Pro | 65.7% Terminal-Bench 4.0 |

## Bundan sonra bakacağım yerler

Kimi ağırlıkları için Moonshot'un tarihi 4 Kasım. Agent Compute Engine önizlemesi "önümüzdeki aylarda". Anthropic'in Kasım halka arzı aktarılmış bir hedef, henüz dosya değil. PHP istismarının seyrek kalıp kalmayacağı belli değil. OpenAI'ın Google Cloud genel erişimi "önümüzdeki haftalarda", Microsoft birincil ortak olarak duruyor.

Çökmeyi bulmak ile çökmediğini ispatlamak ayrı iş. Fatura küçülmedi.

## Kaynaklar

- [OpenAI eğitim yazısı](https://openai.com/index/securing-our-frontier-model-training-environment)
- [Newsom'a mektup](https://cdn.openai.com/pdf/openai-letter-to-governor-newsom-20261020.pdf)
- [StateScoop](https://statescoop.com/openai-urges-newsom-to-strengthen-californias-ai-safety-law-with-additional-safeguards/)
- [OpenAI gözetim raporu](https://alignment.openai.com/misalignment-reports/suppressing-misalignment-monitoring-alerts-and-disabling-misalignment-monitoring/)
- [METR ve Redwood](https://metr.org/blog/2026-10-22-red-teaming-openai-agent-monitoring/)
- [Wiz, PHP2Shell](https://www.wiz.io/blog/php2shell-php-rce)
- [CISA uyarısı](https://www.cisa.gov/news-events/alerts/2026/10/21/critical-vulnerabilities-php-require-immediate-patching)
- [BBC](https://www.bbc.com/news/articles/cmly0lg3w5x2o)
- [NBC News](https://www.nbcnews.com/tech/security/hackers-php-flaws-cybersecurity-crisis-rcna605112)
- [Anthropic, biçimsel doğrulama](https://www.anthropic.com/research/formal-verification)
- [Microsoft Research, KLS](https://www.microsoft.com/en-us/research/blog/solving-a-31-year-old-grand-challenge-in-mathematics-the-kls-conjecture/)
- [Google Cloud, Agent Compute Engine](https://cloud.google.com/blog/topics/ai-infrastructure/introducing-agent-compute-engine-and-expanded-agent-governance)
- [Nvidia, OpenShell](https://developer.nvidia.com/blog/how-nvidia-openshell-reference-architecture-secures-and-governs-ai-agent-workloads-at-scale/)
- [Agentic AI Foundation](https://aaif.io/news/agentic-ai-foundation-announces-four-new-projects)
- [Anthropic, Agent Skills](https://www.anthropic.com/news/donating-agent-skills-to-the-agentic-ai-foundation)
- [TechCrunch, Anthropic taslağı](https://techcrunch.com/2026/10/20/anthropics-cloud-partnerships-are-getting-messy/)
- [OpenAI, Google Cloud](https://openai.com/index/openai-models-google-cloud/)
- [Meta üçüncü çeyrek](https://investor.atmeta.com/investor-news/press-release-details/2026/Meta-Reports-Third-Quarter-2026-Results/default.aspx)
- [Recursive, Flint](https://recursive.com/updates/introducing-recursive-flint)
- [TechCrunch, Flint](https://techcrunch.com/2026/10/21/recursive-launches-flint-a-laptop-coding-model-it-says-was-largely-built-by-ai/)
- [Kimi K3.1 Pro](https://www.kimi.ai/blog/kimi-k3-1-pro)
- [VentureBeat, Kimi](https://venturebeat.com/technology/moonshots-kimi-k3-1-pro-flirts-with-open-weights-leadership-amid-paid-influencer-scandal-allegations)
