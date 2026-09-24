---
title: "Lab kendi kâğıdını verdiğinde Türkiye'de AI'yi kim ölçer?"
slug: "turkiye-bagimsiz-ai-degerlendirme"
lang: tr
focus_keyphrase: "bağımsız AI değerlendirme Türkiye"
yoast_title: "Türkiye'de bağımsız AI değerlendirme: TSE, özel lab, boşluk"
yoast_metadesc: "Türkiye'de AI'yi kim bağımsız ölçer? TSE GYZD damgası henüz açık değil, özel EvalOps lab'leri var; TBMM 260 sayılı rapor ne öneriyor."
excerpt: "Lab'ler kendi güvenlik hikâyesini yazıyor. Türkiye'de bağımsız AI ölçümü: henüz açılmamış bir damga, özel EvalOps lab'leri ve yasa olmayan 900 sayfalık Meclis raporu."
categories_note: "coordinator maps IDs: 763+79"
---

Satıcı modeli geliştiriyor, testi hazırlıyor, puanı veriyor, sonra da karnesini önünüze koyuyor. Pek rahat bir düzen. Peki **bağımsız AI değerlendirme Türkiye** tarafında bugün gerçekten kimin kapısını çalabilirsiniz? Kısa yanıt şu: Frontier sistemleri inceleyip devlet adına belge veren, faal ve tek bir ulusal kurum henüz yok. TSE'nin hazırladığı ama başvuru almaya başlamadığı GYZD var. Belirli sektörlere dönük çalışmalar var. Özel EvalOps ve red team şirketleri ölçüm yapıyor. Bir de TBMM'nin geniş bir tartışma açan araştırma raporu bulunuyor.

Bunların her biri başka iş görüyor. Aradaki etiketleri sökerseniz teknik inceleme raporunu devlet belgesi, Meclis önerisini de yürürlükteki kanun sanmak işten bile değil.

## Bağımsız AI değerlendirme Türkiye haritasında kim, ne yapıyor?
<!-- INLINE_IMAGE_1 -->

Haritayı üç kata ayırmak gerekiyor.

İlk katta standart ve belgelendirme var. TSE, Güvenilir Yapay Zekâ Damgası'nı, kısa adıyla GYZD'yi hazırlıyor. Ama damga henüz dağıtılmıyor.

İkinci katta teknik değerlendirme bulunuyor. Özel bir lab modeli, uygulamayı ya da agent sistemini test edebilir; Türkçe davranışı ölçebilir, saldırı senaryoları çalıştırabilir ve rapor yazabilir. Rapor değerlidir. Yine de kendiliğinden resmî belgeye dönüşmez.

Üçüncü kat politika ve araştırma. TBMM Yapay Zekâ Araştırma Komisyonu'nun raporu olası kurumları, yasal düzenlemeleri ve kamu politikasını tartışmaya açıyor. Bu belge yasa değil. Üstelik Türkiye'de faal bir AI Safety Institute kurmuş da değil.

Standartları kimin yazacağına dair daha geniş tartışmayı [AI standartlar kuruluşu pakt mı, kartel mi](https://www.oguzhan.co/tr/ai-standart-organi-pakt-mi-kartel-mi/) yazısında ele almıştım. Buradaki soru daha gündelik: Bir satın alma ekibi hangi iddiayı kime kontrol ettirebilir ve karşılığında eline ne geçer?

## TSE cephesi: hazırlık var, canlı damga yok

TSE'nin [GYZD sayfasındaki](https://www.tse.org.tr/guvenilir-yapay-zeka-damgasi-gyzd-belgelendirmesi/) en önemli bölüm logo ya da hedef listesi değil, sürecin bugünkü hali. Ulusal Yapay Zekâ Stratejisi altında teknik, yönetişim ve etik belgeler hazırlanmış. TÜBİTAK ile toplantılar yapılmış, ilgili kurumlar belgeleri değerlendirip onaylamış. Fakat 29 Ocak 2026'da yayımlanan ve 12 Mart 2026'da güncellenen sayfaya göre başvuru ile belgelendirme faaliyetleri başlamamış. Altyapı ve süreç hazırlıkları sürüyor.

Dolayısıyla bugün “GYZD belgeli” diye sunulan bir üretim sistemi görürseniz güncel ve TSE üzerinden doğrulanabilen kanıtı istemek gerekir. Açılmamış başvuru sürecinden belge çıkmaz.

Program devreye girdiğinde başvuruların TSE portalından alınması planlanıyor. Ücretlendirme esaslarına ilişkin çalışma da devam ediyor. Teknik altyapı, veri yönetimi, algoritmik şeffaflık, insan haklarına etkiler, önyargı ve ayrımcılık kontrolleri, güvenlik tedbirleri ile hesap verebilirlik değerlendirme başlıkları arasında. Bu liste planlanan incelemenin genişliğini anlatıyor; bugüne dek kaç sisteme damga verildiğini değil. Zaten doğrulanmış böyle bir sayı yok.

Bir de daha dar alan var. TSE'nin [uzaktan kimlik tespiti yapan AI algoritmalarına ilişkin belgelendirme sayfası](https://www.tse.org.tr/uzaktan-kimlik-tespiti-yapay-zeka-algoritmalari-ve-tse-belgelendirme-sureci/), MASAK 19 Sıra No'lu Genel Tebliği için hazırlanacak test altyapısını anlatıyor. TSE ile TÜBİTAK BİLGEM işbirliği planlanmış. Aynı tarihler itibarıyla burada da belgelendirme başlamamış.

Sistem açılırsa düzenlenecek rapor, algoritmanın finans sektöründeki uzaktan kimlik kullanımı için MASAK 19 şartlarını karşılayıp karşılamadığına bakacak. Genel amaçlı bir modelin bütün güvenlik sorunlarını çözmeyecek. Bir bankanın kimlik doğrulama algoritmasını inceleyen dar bir hat ile ulusal AI güvenlik kurumunu aynı şey sayamayız.

## Özel EvalOps lab'leri bugün test yapabiliyor

Kamudaki hazırlık sürerken özel taraf beklemiyor.

[LLM Turkey](https://llmturkey.com/en), kendini özel bir EvalOps merkezi olarak tanıtıyor. Judex adlı bağımsız LLM test platformunun yanında eğitim ve kurumsal danışmanlık sunuyor. Judex için verilen ölçü dokuz parametre ve 12 senaryo. Talimata uyma, doğruluk, güvenlik ve uyum, önyargı ve adalet, muhakeme derinliği, anlatım açıklığı ile açıklanabilirlik bunların arasında.

Türkiye'deki alıcı için asıl fark Türkçe odaklı benchmark iddiası. İngilizce testten yüksek puan alan model; Türkçedeki dolaylı anlatımı, hitap biçimlerini, yerel referansları ya da çok turlu zararlı talepleri aynı başarıyla karşılamak zorunda değil. Dil burada arayüz süsü değil, test yüzeyinin kendisi.

Sitedeki Turkish Truthfulness, yani TR-Truth leaderboard görüntüsü 5 Mayıs 2026 saat 21:00 güncellemesini taşıyor. GPT-4o, Claude 3.5 Sonnet, Gemini 1.5 Pro, Llama 3.1 70B ve Mistral Large listelenen modeller arasında. Bunu LLM Turkey'nin yayımladığı ölçüm olarak okumak doğru olur. Kurumun bağımsız denetimi diye sunmak başka bir iddia. Satın alma ekibi test setinin kurallarını, örneklem yöntemini, model sürümünü, çalıştırma ayarlarını ve olası çıkar çatışmalarını ayrıca sormalı.

[TestMy.AI](https://testmy.ai/tr/about) ise sınırı kendi sitesinde açıkça çiziyor. 2025'te kurulduğunu belirten butik şirket; otomasyon ağırlıklı saldırgan testleri, raporu imzalayan insan baş denetçiyle birleştiriyor. Bulguları OWASP LLM Top 10, ISO 42001, NIST AI RMF ve EU AI Act Madde 15 ile eşliyor. ABD'de St Petersburg, Florida; EMEA tarafında İstanbul üzerinden çalışıyor.

En kıymetli cümle şu: TestMy.AI bir belgelendirme kuruluşu olmadığını söylüyor. Teslim ettiği Technical Assessment Report, uzman hukukçuyla yürütülecek uyum çalışmasına teknik girdi sağlıyor. Böylesi netlik piyasada standart olmalı. Prompt injection açığını bulan red team raporu başka, belirli şartlara uygunluğu gösteren belge başka, hukuki görüş yine başka.

“Bağımsız” sözcüğü de tek başına yetmez. Testi yapan şirket incelediği modeli, orchestration katmanını ya da guardrail ürününü satıyor mu? Başarı ücretine benzer bir düzen var mı? Başarısız vakaları ve ham bulguları görebilecek misiniz, yoksa elinize renkli bir puan kartı mı geçecek? Üçüncü taraf olmak, tarafsızlığın başlangıç iddiası. İspatı değil.

## TBMM 260 sayılı rapor düzenleyici kurum değildir

Meclis belgesi hafife alınacak türden değil. TBMM 28. Dönem Meclis Araştırması Komisyonu'nun [Sıra Sayısı 260 raporu](https://cdn.tbmm.gov.tr/KKBSPublicFile/D28/Y1/T10/DosyaKomisyonRaporunuVerdi/9f0e7abf-41f6-4133-ab3d-4879113f7f9f.pdf), kapağında Mart 2026 tarihini taşıyor. Yapay zekânın kazanımları, hukuki altyapı ve risklere karşı alınabilecek tedbirler için atılacak adımları inceliyor. İkincil kaynaklar yaklaşık 900 sayfadan ve 100 dolayında politika önerisinden söz ediyor.

Aktarılan öneriler arasında AI ve ileri teknolojiler için TBMM'de daimi komisyon kurulması, Meclis'in kendi AI kullanımı için ilkeler rehberi hazırlanması, AI kaynaklı çalışma hayatı değişimine göre sosyal güvenlik düzenlemeleri ve Türk Devletleri Teşkilatı ile Türkçe LLM ve standart çalışmaları var. Bunlar araştırma raporunun önerileri. Ruhsat veren bir ofis açılmış değil; 260 sayılı rapor da yürürlükte bir AI kanunu değil.

Raporun değeri başka yerde. Kamu genelinde hukuk, bütçe, denetim ve kurumsal tasarım tartışmasını besleyebilir; ileride çıkacak kanunlara malzeme sunabilir. Fakat bu çeyrekte alınacak model için değerlendirme raporunu bir öneri listesi imzalayamaz.

Yurt dışındaki agent erişimi vakaları sonrası “bunu kim kontrol etti?” sorusunun niçin ansızın yönetim masasına geldiğini [Avustralya Medicare olayında](https://www.oguzhan.co/tr/openai-ajan-medicare-avustralya/) gördük; telaş, hazırlık aşamasındaki kurumu faal denetçiye çevirmiyor.

## “Belgeli AI” diyen satıcıya sorulacaklar
<!-- INLINE_IMAGE_2 -->

Önce neyin incelendiğini netleştirin. Temel model mi, fine-tune edilmiş sürüm mü, bütün uygulama mı, MCP ve API izinleri mi, yoksa şirketin yönetim süreci mi? Statik benchmark testini geçen model, gereğinden geniş erişime sahip agent içinde tehlikeli davranabilir.

Ardından şu beş soruyu sorun:

1. **Tam olarak ne test edildi?** Model kimliği ve sürümü, system prompt, bağlı araçlar, veri sınırları ve test tarihi yazılı olsun. “AI çözümümüz testi geçti” bir kapsam tarifi değil.
2. **Değerlendiren taraf ne kadar bağımsız?** İncelenen parçayı geliştiriyor, yeniden satıyor ya da yönlendirme geliri alıyor mu? Çıkar çatışması politikasını isteyin.
3. **Teslim edilecek dosya ne?** Leaderboard kaydı, red team raporu, hukuk notu ve sertifika aynı ağırlığı taşımaz. Sözleşme elveriyorsa başarısız vakaları, önem derecesi kurallarını ve düzeltme durumunu da alın.
4. **Türkçe gerçekten test edildi mi?** İngilizceden çevrilmiş vakalar yerel ifadeleri, kültürel referansları ve uzun konuşmalardaki davranışı ıskalar. Türkçe senaryoları kimin yazıp gözden geçirdiğini sorun.
5. **İddia belge mi, teknik değerlendirme mi?** Programın adını, belgeyi veren kuruluşu, geçerlilik alanını, düzenleme tarihini, sona erme ya da takip şartlarını ve doğrulama yolunu isteyin. Bunlar yoksa o dosyanın adını sertifika koymayın.

Değerlendirme operasyonla da birleşmeli. Rapor çekildiği günün fotoğrafıdır. Model, prompt, yetki ve tedarikçi değişir. [Operator için misalignment bildirim çerçevesi](https://www.oguzhan.co/tr/openai-misalignment-bildirim-cercevesi-operator/) bu yüzden olay kabulü, yükseltme ve kanıt saklama işini test bittikten sonra da sürdürür.

## Kendi kâğıdını veren lab için basit kural

Satıcının iç testini, özel teknik değerlendirmeyi, standart belgelendirmesini ve kamu politikasını ayrı sütunlara yazın. Sonra her sütunun gerçekten neyi kanıtladığına bakın.

TSE iki ayrı hatta hazırlık yapıyor. Özel lab'ler Türkçe test ve saldırgan inceleme satıyor. TBMM geniş bir öneri dosyasını tartışmaya açtı. Bütün bu parçalar değerli; ama yan yana gelince bugün faal tek bir devlet değerlendirme kurumu etmiyor.

İhtiyacınız olan incelemeyi alın, adını doğru koyun. Modelleri, kuralları ve sahadaki uygulamayı birlikte takip etmek için [oguzhan.co yapay zekâ merkezi](https://www.oguzhan.co/tr/yapay-zeka/) bütün başlıkları aynı yerde tutuyor. Raporu damga, damgayı da kanun diye tanıtmadan.
