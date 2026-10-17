---
title: "Çin yapay zeka ihracat kontrolü: Ağırlık lisansa bağlı, API serbest"
slug: "cin-yapay-zeka-ihracat-kontrolu-model-agirliklari"
focus_keyphrase: "Çin yapay zeka ihracat kontrolü"
yoast_title: "Çin yapay zeka ihracat kontrolü: Taslak neyi kısıtlıyor?"
meta_description: "Çin yapay zeka ihracat kontrolü, 16 Ekim 2026 taslağında model ağırlığını üç çizgiyle lisansa bağlıyor. API, uygulama ve SaaS çağrısı katalog dışında."
excerpt: "48 sayılı taslak, çizgiyi aşan model ağırlığını lisansa bağlıyor. API erişimi katalog dışında. Metin 15 Kasım 2026'ya kadar görüşte, kayıt ekranı ise açıldı."
---

## 16 Ekim duyurusu

16 Ekim 2026, Pekin saati 16:00. Çin Ticaret Bakanlığı ile Bilim ve Teknoloji Bakanlığı, İhracatı Yasak ve Kısıtlı Teknolojiler Kataloğu'nun taslağını görüşe açtı. Duyuru 2026/48. Çin yapay zeka ihracat kontrolü ilk kez burada kendi başlıklarını ve rakamlarını alıyor. Lisans dosyaya işliyor. Eğitim 10^26 FLOP, parametre 2 trilyon ya da ihracat anında küresel ilk 10. Üçünden birini tutan büyük modelin ağırlıkları, checkpoint'i, kaynak kodu ve mimarisi ülkeden çıkacaksa izin gerekir. API, uygulama, site, SaaS ve hafif cihaz üstü sürüm bu ihracata girmez. Görüş 15 Kasım 2026'da biter. Adres jinxianmulu@mofcom.gov.cn.

Duyuruyu, eki ve sözcü soru-cevabını okudum. Eşik denemedim. Kimseyle konuşmadım. Cümleler hâlâ taslak.

## Katalogda sahiden ne var?

[Duyuru](https://www.mofcom.gov.cn/zcfb/blgg/gg/2026/art/2026/art_05e2643a8ca04eb9adf9dd0542991fe4.html) üç alanda 40 teknoloji sayıyor. 23'ü yapay zeka: büyük model, agent, hesap kümesi, bilgi işleme. [Sözcü metni](https://www.mofcom.gov.cn/xwfb/xwfyrth/art/2026/art_d7661dbf62794345a221404f82a25959.html) bütün taslağı 14 yasak, 26 kısıt diye ayırıyor. [CTOL](https://www.ctol.digital/news/china-draft-technology-export-catalogue-ai-model-weights-chip-design/) yapay zeka payını 6 yasak, 17 kısıt saymış. Biyotıp 5, fotovoltaik 12. Açık kaynakla ya da makaleyle kamuya çıkmış teknoloji bu yönetime girmiyor.

Yasak: kritik altyapı, savunma ya da çekirdek devlete sürülebilecek zararlı kod (266402J), "çekirdek veri" ile eğitilip hizmete sunulan büyük model (266501J), aynı iş için özellikle ya da esas olarak kurulan yüksek başarılı agent (266502J).

Kısıt: çizgiyi aşan modelin çekirdek teknolojisi ve "önemli veri" ile hizmete sunulan model (266504X), agent (266505X), zafiyet keşfi (266404X), çip tasarımı (266506X), hesap kümesi (266507X). Eski maddelere ek: yüzde 98 ve üzeri deepfake tespiti, steganografi, ses izi, Çince ile azınlık dilleri arasında çeviri. [Frontier Now](https://frontiernow.dev/en/news/china-ai-export-catalog-draft/) bunu yapay zekanın ilk kendi başlığı diye okuyor.

## Çin yapay zeka ihracat kontrolü üç çizgi çekiyor
<!-- INLINE_IMAGE_1 -->

266504X, üç testten herhangi birini tutan modelin çekirdek teknolojisini kısıta yazıyor. Eğitim en az 10^26 kayan nokta işlemi. Parametre en az 2 trilyon. Ek bunu 20,000亿 diye yazmış. Ya da "küresel lider düzey": ihracat anında, Çin'de ya da dışında ana akım değerlendiricilerin veya büyük sektör platformlarının açık testlerinde dünya ilk 10'u. Sıra genel performansta, belirli bir iş yeteneğinde, küresel çağrı hacminde, güvenlikte, eğitim verimliliğinde ya da ekteki "vb." kaleminde olabilir.

Sıra ihracat anında bakılıyor. Okumam şu: sıralama kayarsa model listeye girip çıkabilir. Lisansı sıralamaya bağlamak tuhaf.

Çekirdek teknoloji sayılmış. Ağırlık, kritik checkpoint, alttaki kaynak kod, mimari, eğitim optimizasyonu ve çıkarım hızlandırma.

İkinci tetik bu çizgilere bakmıyor. "Önemli veri" ile eğitilip hizmete sunulan model 266504X ile kısıt. "Çekirdek veri" ile eğitilip hizmete sunulan model 266501J ile yasak. [Frontier Now](https://frontiernow.dev/en/news/china-ai-export-catalog-draft/) iki etiketin de Veri Güvenliği Kanunu'na gittiğini, bu duyuruda tanımlanmadığını yazıyor. İstisna dar: o alanda çekirdek Ar-Ge kapasitesini esastan kaldıramayan, duyarsızlaştırılmış, çıktıda yeniden üretilmeyen, yüzde 0,1 ve altı bir iz. Ya da hukuken kamuya açık veri.

## Dosya kontrole giriyor
<!-- INLINE_IMAGE_2 -->

[Sözcü](https://www.mofcom.gov.cn/xwfb/xwfyrth/art/2026/art_d7661dbf62794345a221404f82a25959.html) "yurtdışına çıkan model"i aktarıma bağlıyor. Kısıtlı teknoloji Çin içinden dışarı gidiyor mu? Yurtdışında yerinde kurulum teknoloji ihracatı. Aynı yığın şirketin kendi yurtdışı bulutundaysa otomatik lisansa uygun. API, uygulama ya da site, SaaS, hafif cihaz üstü kopya büyük model teknolojisi ihracatı sayılmıyor.

Otomatik lisans bir de şunları örtüyor: kısıtlı teknolojiyi açık kaynak yapmak, Çinli firmanın yurtdışında kendi hesap merkezini kurup işletmesi, çipin yurtdışında tape-out'u, yabancı kaynakla ortak araştırma, uluslararası standart işi. Sözcü ve ek dipnotu aynı listeyi yazıyor. Bakanlık esasen "kayıt yaptır, çık" diyor (即报即出). Kamuya çıkmış teknoloji dışarıda. Dünya Yapay Zeka İşbirliği Örgütü üyelerine kapasite, paylaşım ve ortak kural kolaylığı var. Küresel Güney desteği de var. [CTOL](https://www.ctol.digital/news/china-draft-technology-export-catalogue-ai-model-weights-chip-design/) bunu vaat sayıyor. İstisna nihai metinden çıkabilir.

16 Ekim'den revize katalog yürürlüğe girene kadar ecomp.mofcom.gov.cn şunları alıyor: yurtdışına mülkiyet devri (örnek fikri mülkiyet temliki), yurtiçi teknolojinin yurtdışında kullanım lisansı, malikin ya da fiili kontrolün yabancıya geçmesi, bakanlığın sayacağı başka haller. Başlamış bitmemiş ihracat dahil. Kayıtta taraflar, varış, teknoloji, kullanım, beklenen değer. Kontrollü teknolojiyle üretilen ürün dışarıda. Kayda girip girmediğine ihracatçı kendisi karar veriyor. Yürürlükten sonra bakanlık, yapay zeka teknolojilerinin büyük çoğunluğunun yine serbestçe ihraç edilebileceğini söylüyor.

## Agent, zararlı kod ve açık avı

266505X dört agent belirtimi yazıyor. Birinin yettiği söylenmiyor.

- Tek doğal dil talimatını ≥20 yürütülebilir adıma bölmek, ayrıştırma doğruluğu ≥%80, alt görev başarısı ≥%90.
- ≥60 eşzamanlı işbirlikçi agent, aynı sonuç için süre tek agent asgarisinin en fazla iki katı, standart yanıtla uyum ≥%85.
- ≥200 üçüncü taraf araç, seçim isabeti ≥%90, üç ya da daha fazla araç isteyen işte uçtan uca başarı ≥%90.
- Oyun kararı, koşulların hepsi: plan derinliği ≥20 adım ya da ≥10 eşzamanlı agent, karar ≤200 milisaniye, standart testte insanların %90'ını geçmek.

Anthropic, [Claude Managed Agents](https://www.oguzhan.co/tr/claude-managed-agents-dinamik-is-akislari/) tarafında 64 eşzamanlı iş parçacığına izin veriyor. 60 ile 64 komşu, aynı sınav değil. Ek hız ve doğruluk da istiyor. Liste yalnız Çin teknolojisinin ihracatını bağlıyor.

266402J, kritik altyapı, savunma ve çekirdek devlet sistemlerine sürülebilecek yapay zeka güdümlü zararlı kodu yasak öneriyor. Şunlardan biri yetiyor: çok motorlu dedektör ≥%60, tek ana akım antivirüs ≥%85, makine öğrenmesi modeli ≥%90. Ayrıca uyarlanabilir kaçınma (sandbox, hata ayıklayıcı, emülatör, sandbox kaçışı, her çalıştırmada kod yapısının ≥%50'si) ve toplu varyant (çalıştırmada ≥20 eşdeğer ya da uçtan uca ≥%80 otomasyon). Gerekçe, ulusal güvenlik savunmasının aşılması ve aracın devlet dışı ya da kötü niyetli elde riski. Amaç, yapay zekanın güvenli ve kontrol edilebilir kalması, her zaman insan kontrolünde durması. [Zararlı yazılım yazısı](https://www.oguzhan.co/tr/closedquorum-malware-llm-c2-oylama/) bu maddenin teşhisi değil.

266404X zafiyet keşfini kısıta alıyor. Biri yeter: yetkili güvenlik kıyaslarında yeniden üretim ve istismar edilebilirlik ≥%75, ana akım işletim sistemi ya da tarayıcıda uçtan uca istismar zinciri ≥%50 (rastgele kodda ≥%40), kıdemli güvenlik uzmanına göre ≥10 kat, ≥2 düşük ya da orta açığı kanıtlı çok aşamalı saldırıya kendiliğinden bağlamak, tek geçişte bir büyük açık kaynak proje ya da işletim sisteminde ≥5 açıklanmamış yüksek önemde açık ya da ≥50 açıklanmamış açık, ana akım istismar yeteneği derecelendirme sistemlerinde üst düzey. [Açık avını önce savunmacıya vermek](https://www.oguzhan.co/tr/gemini-4-argon-once-siber-savunma/) başka tercih. Burada tercih ihracat çizgisi.

Eşikleri tutup agent'ı özellikle ya da esas olarak kritik altyapı, savunma ya da çekirdek devlet işine kurarsan madde 266502J ile yasak sütununa çıkar. Çip tetiklerinden ikisi 14 nm ve daha ince süreç ile 2.5D ya da 3D paketleme. Kümede çift yönlü ara bağlantı ≥800 GB/s, dağıtık eğitim arızasında ortalama onarım ≤120 saniye, büyük ölçek 10.000'den fazla hızlandırıcı kart. İleri olmaktan çıkan madde düşecek, diyor bakanlık. Önce enstitülere, sektör kuruluşlarına ve büyük şirketlere danışılmış.

## ABD kuralının kopyası mı?

| | ABD AI Diffusion Rule | Çin taslağı (48 sayılı duyuru) |
|---|---|---|
| Yayım | 15 Ocak 2025 (BIS geçici nihai kural) | 16 Ekim 2026 (15 Kasım'a kadar görüşe açık taslak) |
| Hesap çizgisi | 10^26 işlemin üstünde eğitilmiş kapalı modellerin ağırlıkları | 10^26 FLOP, ya da 2 trilyon parametre, ya da küresel ilk 10 |
| Açık ağırlık | Yalnızca kapalı ağırlıklı modeller | Kamuya açık olan listenin dışında, yeni açık kaynakta otomatik lisans |
| Hedef | En ileri modellerin ağırlıkları ve ileri çipler | Çekirdek teknoloji (ağırlık, checkpoint, kod, mimari), agent, çip, küme. API, uygulama ve SaaS, MOFCOM'a göre ihracat sayılmıyor |
| Durum | 13 Mayıs 2025'ten beri uygulanmıyor, CFR'de duruyor (GAO) | 16 Ekim'den beri ihracat öncesi kayıt işliyor |

[GAO B-337935](https://www.gao.gov/products/b-337935) (12 Mayıs 2026) kaldırmayı nihai saymıyor. Uygulamama duyurusu Congressional Review Act anlamında kural. 15 Ocak 2025 çerçevesi ileri çipi ve en ileri model ağırlığını lisansa bağlamış, 13 Mayıs 2025'te bakanlık uygulamayı bırakıp kaldırmayı açmıştı. Kapalı ağırlık [Encyclopedia of Economic Statecraft](https://jamesjtennant.com/entries/ai-model-weights-and-frontier-models/) maddesinde ECCN 4E091: 10^26 üstü ileri kapalı modeller.

Dean W. Ball'ı [The Decoder](https://the-decoder.com/china-plans-to-tighten-export-controls-on-open-weight-models-and-23-key-ai-technologies/) OpenAI'da stratejik gelecekler biriminin başı diye anıyor. Cümlesi: "This move does not mean 'China is shutting down open-weight models,' but it does indicate the Chinese government establishing the optionality to shut down future open-weight models at will." "Ayna görüntüsü" dediği şey ABD'nin model ağırlığı kontrolleri. Bu taslak kamuya çıkmış dosyayı bırakıp yeni açık kaynağa otomatik lisans koyuyor.

Sözcü dayanağı Dış Ticaret Kanunu madde 20. Katalog 2001'den beri çok kez değişmiş. [CTOL](https://www.ctol.digital/news/china-draft-technology-export-catalogue-ai-model-weights-chip-design/) metni bu kanun ile teknoloji ithalat ve ihracat düzenlemelerine koyuyor, çift kullanımlı listeleri taşıyan İhracat Kontrol Kanunu'ndan ayırıyor. Bakanlık işe "rutin" diyor, belirli bir ülkeyi, bölgeyi ya da tarafı hedeflemediğini söylüyor. Ankura China Advisors kıdemli direktörü Ryan Etzcorn, Bloomberg üzerinden [The Straits Times](https://www.straitstimes.com/business/china-plans-ai-export-curbs-to-exert-control-over-key-tech) aktarımında: "This is more than routine maintenance." Ve: "Beijing is signalling that steadier relations with the West do not mean it will stand still." Aynı yazı, 2020'de ilk Trump yönetimi ABD varlıkları satılmazsa TikTok'u yasaklamakla tehdit edince Pekin listeye algoritma eklemiş. Temmuz 2025 kataloğunda CTOL 3 silme, 1 ekleme, 1 değişiklik sayıyor, yapay zeka yok. Kırk öneri, beş değişikliğe karşı büyük adım, diyor CTOL.

## Etkinin sırası
<!-- INLINE_IMAGE_3 -->

Çizgi kalırsa ilk halka, 2 trilyon ve üstünü çizen Çinli laboratuvar. Bloomberg, [The Straits Times](https://www.straitstimes.com/business/china-plans-ai-export-curbs-to-exert-control-over-key-tech) ile Kimi K3 ve Alibaba Qwen3.8-Max'i bu çizginin üstünde örnek gösteriyor. Alibaba eylülde 5 ila 10 trilyon parametre planladığını söylemiş. Kısıt kararı değil. 5 ila 10 trilyon, taslaktaki 2 trilyonun epey üstünde kalır.

Yabancı alıcı, kamuya çıkmamış kısıtlı modeli kendi makinelerinde istiyorsa lisans Çinli satıcıda. Yerinde kurulum ihracat, kendi yurtdışı bulutu otomatik lisans.

Matthias Bastian [The Decoder](https://the-decoder.com/china-plans-to-tighten-export-controls-on-open-weight-models-and-23-key-ai-technologies/)'da Avrupa'nın açık ağırlığı ülke içi bulutta tutma bahsini yazıyor. En iyi açık model ABD ya da Çin'den geliyor ve sonraki sürüm kesilebiliyorsa bahis zorlaşır. Ball'ın seçeneği gelecek Çin sürümüne bakıyor.

Yayımlanmış açık ağırlık taslağın dışında. Qwen ya da DeepSeek dosyasını kendi makinesinde çalıştıran kişi bu metnin muhatabı değil. Metin kalırsa düğme sonraki uç açık ağırlıkta ve yurtdışı yerinde kurulumda.

Reuters, [8 Temmuz 2026 tarihli Straits Times aktarımı](https://www.straitstimes.com/asia/east-asia/beijing-is-looking-at-curbing-overseas-access-to-chinas-top-ai-models-sources-say) ile Ticaret Bakanlığı, Alibaba, ByteDance ve Z.ai toplantılarını yazdı. Konu en ileri modellere yurtdışı erişimdi. Yayımlanmamışlar dahil, kapalı da açık da. Kapsam o gün belirsizdi. Yüksek Halk Mahkemesi dergisindeki mayıs oturum özeti katlar önermiş: temel açık kaynağa basit bildirim, ileri olana güvenlik incelemesi, en hassas uç modellerin kamu sürümüne kapanması ya da ülkede kalması. Ekim metni API çağrısını dışarıda bırakıyor. Temmuz çağrıydı. Ekim dosya.

## 15 Kasım'a kadar izlediğim başlıklar

10^26 ve 2 trilyon imzada duracak mı. [CTOL](https://www.ctol.digital/news/china-draft-technology-export-catalogue-ai-model-weights-chip-design/) açık bırakıyor.

"Önemli veri" ve "çekirdek veri" nasıl tarif edilecek. [Frontier Now](https://frontiernow.dev/en/news/china-ai-export-catalog-draft/) ikisini sonraki kurallara bırakıyor.

Otomatik lisans sahiden "kayıt yaptır, çık" mı. CTOL bunu vaat sayıyor, metinden silinebilir.

ABD, uygulamadığı diffusion kuralının yerine ne koyacak. Kaldırma nihai değil. O iz [ABD federal yapay zeka politikası](https://www.oguzhan.co/tr/super-intelligence-force-jay-clayton-ai-cari/) yazısında.

15 Kasım görüşü kapatır. Ekran 16 Ekim'de açıldı. Arada devir ya da yurtdışı lisans imzalayan kişi, bitmemiş kataloğa göre teknolojiyi kendisi ayıracak. Yük ihracatçıda.

## Kaynaklar

- [2026/48 sayılı duyuru](https://www.mofcom.gov.cn/zcfb/blgg/gg/2026/art/2026/art_05e2643a8ca04eb9adf9dd0542991fe4.html)
- [Sözcü soru-cevabı, 16 Ekim 2026](https://www.mofcom.gov.cn/xwfb/xwfyrth/art/2026/art_d7661dbf62794345a221404f82a25959.html)
- [CTOL Digital Solutions](https://www.ctol.digital/news/china-draft-technology-export-catalogue-ai-model-weights-chip-design/)
- [Frontier Now](https://frontiernow.dev/en/news/china-ai-export-catalog-draft/)
- [The Decoder, Matthias Bastian](https://the-decoder.com/china-plans-to-tighten-export-controls-on-open-weight-models-and-23-key-ai-technologies/)
- [Bloomberg, The Straits Times aktarımı](https://www.straitstimes.com/business/china-plans-ai-export-curbs-to-exert-control-over-key-tech)
- [Reuters, The Straits Times, 8 Temmuz 2026](https://www.straitstimes.com/asia/east-asia/beijing-is-looking-at-curbing-overseas-access-to-chinas-top-ai-models-sources-say)
- [GAO B-337935](https://www.gao.gov/products/b-337935)
- [Encyclopedia of Economic Statecraft](https://jamesjtennant.com/entries/ai-model-weights-and-frontier-models/)
