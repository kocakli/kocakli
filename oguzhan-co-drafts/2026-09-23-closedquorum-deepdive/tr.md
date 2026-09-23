---
title: "CLOSEDQUORUM malware: en fazla dört model saldırıya oy veriyor"
slug: "closedquorum-malware-llm-c2-oylama"
yoast_title: "CLOSEDQUORUM malware: en fazla dört model oy veriyor"
yoast_metadesc: "CLOSEDQUORUM malware nasıl çalışıyor? Çoklu model oylamasını, LLM API’lerinin C2 olarak kullanımını, CAIRN avcılığını ve savunma izlerini inceliyorum."
focus_keyphrase: "CLOSEDQUORUM malware"
excerpt: "CLOSEDQUORUM, en fazla dört ticari LLM API’sini saldırı sonrası karar veren bir heyete dönüştürüyor. Asıl yenilik modelde değil; insan operatörün işinin bir bölümünü devralan dar ama kendi kendine yürüyen döngüde."
---

CLOSEDQUORUM malware, ticari LLM servislerini taktik C2 olarak kullanan, kamuya açık biçimde belgelenmiş ilk Windows implantı. [Cisco Talos’un incelemesine göre](https://blog.talosintelligence.com/the-closed-quorum-inside-the-first-reported-autonomous-ai-c2-implant/) en fazla dört sağlayıcıya, yani DeepSeek, Qwen, Mistral ve Gemini’ye sıradaki hamleyi soruyor; geçerli yanıtları oylayıp parola çalma, kod enjekte etme ya da kalıcılık sağlama işlerinden birini seçiyor. Ancak sahada kullanıldığı doğrulanmış değil ve dağıtımdaki örneğin anahtarları sahte. Dolayısıyla elimizde süren bir saldırı kampanyası değil, saldırganın işini başka yere devreden hayli öğretici bir mimari var.

Konuyu [günün kısa notlarında](https://www.oguzhan.co/tr/closedquorum-ai-malware-dort-model-oylamasi/) özetlemiştim. Fakat “zararlı yazılıma AI eklemişler” deyip geçilecek bir dosya değil bu. 16,4MB büyüklüğündeki bir Windows programının içinden C2 altyapısının geleceğine dair epey kalabalık bir tartışma çıkıyor.

## 🧩 CLOSEDQUORUM malware dosyasının içinde ne var?

Talos bu implantı CAIRN adlı avcılık projesi sayesinde buldu. 64-bit Windows için hazırlanmış dosya Go ile yazılmış. `CGO_ENABLED=1` ayarı açık; böylece doğrudan Windows syscall’larına ulaşabiliyor. Yani model tarafındaki gösterişli bölümün altında bildiğimiz sistem programlama işleri duruyor.

Program açıldığında `gatherSystemInfo()` devreye giriyor. Makinenin adını, işletim sistemi mimarisini, CPU sayısını, Windows sürümünü ve yönetici yetkisinin bulunup bulunmadığını topluyor. Bu bilgiler prompt içine `TARGET:%s` biçiminde ekleniyor. Hedef süreç bilgisi de her turda yenileniyor.

Hemen saldırmıyor. İlk bağlantı için beş dakika bekliyor, sonraki sorguları rastgele beş ile 15 dakika aralıklarla yapıyor. Windows Update adlarını kullanıyor, dosyaları `C:\Windows\Temp\` altında hazırlıyor, `EtwEventWrite` işlevini RET komutuyla etkisizleştirmeye çalışıyor. İkinci payload ise zamandan türetilen anahtarla şifreli.

Burada önemli bir parantez açalım. Talos’un incelediği dağıtım sürümünde `dummy_api_key` ve `dummy_webhook_url` yazıyor. Yani örneği indirip çalıştırınca model servisleriyle görüşmeye, Discord’a dosya göndermeye başlamıyor. Talos ayrıca gerçek bir saldırı kampanyasını doğrulamadı. Buna karşılık geliştiriciyi 2025’e uzanan carding forumu paylaşımlarına bağlayan izler var. Yazılımın eski adı BALZAK; 3 Temmuz 2026’da CLOSEDQUORUM olarak değiştirilmiş.

Eldeki kanıtın sınırı bu. Doğrulanmış mağdur sayısı yok; herhangi bir devlet bağlantısı da doğrulanmış değil. Olmayan hikâyeyi eklemeye hiç gerek yok; mevcut tasarım yeterince ilginç.

## 🔎 Bu dosyayı çalıştırmadan bulan izler

Bu örneği ortaya çıkaran [CAIRN](https://blog.talosintelligence.com/introducing-cairn-frontier-tracking-for-ai-integrated-malware/), açılımıyla Cognitive Artifact Intelligence Research Network, açık kaynak bir araç seti. Avcılığa metadata ile başlıyor. Bu katmanda her şüpheli binary’yi indirip çalıştırmak gerekmiyor.

Aranan şeylere “cognitive artifacts” adı verilmiş. Prompt şablonları, model sağlayıcılarının adresleri, API anahtarı önekleri, jailbreak metinleri, AI analizini yanıltmaya yönelik cümleler ve `tool_call` biçimleri bunların arasında. Toplama filtrelerinde provider API entegrasyonu, Python AI script’leri, yerel LLM runtime’ları, agentic tooling ve AI-analysis evasion gibi başlıklar bulunuyor.

CAIRN bunları üç katmanlı YARA düzenine aktarıyor. T1 basit AI izlerini, T2 davranış bağlamını, T3 ise operasyon ailelerini tanımlıyor. Explorer grafiği örnekler arasındaki ilişkileri gösteriyor. UMAP ve HDBSCAN ile yapılan anlamsal kümeleme de birbirine yakın dosyaları işaretliyor.

İşaretlemek, suçlu ilan etmek değil. PyInstaller, Tauri ve bazı Go PE yapıları T1 ile T2 seviyesinde gereksiz alarm üretebiliyor. Meşru bir uygulamada model servisinin adresi geçebilir. Paketleme biçimi de zararlı yazılıma özgü olmayabilir. Kümeler araştırmacıya “buraya bak” diyor; kimin yazdığını söylemiyor.

Yine de metinsel izler şaşırtıcı derecede kalıcı. Talos, AI analizini susturmayı amaçlayan doğal dildeki bir metni red-team eğitmeninden bağımsız aktörlerin örneklerine kadar takip etmiş. Yayılma 12 ay içinde gerçekleşmiş. Kod parçaları kadar cümlelerin de el değiştirdiği bir dönem. CAIRN tam olarak bunu görünür kılmaya çalışıyor.

## 🌐 Saldırganın kendi sunucusu aradan çıkınca

Klasik düzende C2 için saldırganın kontrolündeki alan adı, IP adresi ya da dinleyici kullanılır. Savunma ekibi bunları bulup engelleyebilir; bağlantılar saldırgana ilişkin iz bırakır ve açığa çıkan altyapıyı yenilemek pahalıdır.

CLOSEDQUORUM başka bir yol deniyor. `ModelOrchestrator` sırasıyla DeepSeek, Alibaba’nın Qwen’i, Mistral ve Google Gemini API’lerine gidiyor. Bu servislerin adresleri her gün binlerce meşru uygulama tarafından kullanılıyor. Bir şirketin Gemini ya da Mistral trafiğini toptan engellemesi, saldırganı durdurmadan önce kendi yazılımlarını bozabilir.

Bu, zararlı yazılımın görünmez olduğu anlamına gelmiyor. Yalnızca tek başına alan adına bakmanın artık yetmediğini gösteriyor. Sıradan görünmeyen bir Windows sürecinin kısa aralıklarla birkaç LLM API’sine bağlanması; aynı süreçte veya host üzerinde LSASS erişimi, askıya alınmış sürece injection, WMI kalıcılığı ve Discord webhook trafiğiyle birlikte görüldüğünde anlam kazanıyor.

CLOSEDQUORUM’daki model ile araç arasındaki bağlantı, [MCP ve yapay zeka ajanları için pratik kontrol listesiyle](https://www.oguzhan.co/tr/mcp-yapay-zeka-ajan-pratik-checklist/) aynı tool-wiring hygiene başlığına dokunuyor. Buradaki yazılım elbette meşru bir agent değil; bağlantı, savunma ekipleri ve agent geliştirenler için yine de öğretici.

## 🗳️ En fazla dört model, hayli basit bir oylama

Sistemin prompt’u pek dolambaçlı sayılmaz: “You are an advanced malware strategist. Provide ONLY executable decisions.” Modellerden yalnızca JSON dönmeleri isteniyor. Seçenek listesi de dört kelimeden ibaret:

- `steal`
- `inject`
- `persist`
- `move`

Her yanıt `LLMDecision` listesine ekleniyor. `interModelDiscussion()` adlı işlev, `Decision` alanında hangi seçeneğin daha çok geçtiğini sayıyor. Adında “tartışma” var ama modeller birbirleriyle uzun uzun konuşmuyor. Yanıt geliyor, bir alana indirgeniyor, oy olarak sayılıyor.

Eşitlik halinde karar da pek demokratik değil. Kod seçimini yalnızca daha yüksek oy gördüğünde değiştiriyor; oylar eşitse ilk karşılaştığı seçenek yerinde kalıyor. Yanıtların sırası yüzünden öncelik DeepSeek’te. Onu Qwen, Mistral ve Gemini izliyor.

Peki neden dört servis? Biri isteği reddedebilir, diğeri zaman aşımına uğrayabilir, bir başkası bozuk JSON gönderebilir. Birden fazla sağlayıcı hata payını azaltıyor. Dördü de çalışmazsa `consensus` adlı yedek karar üretiliyor. Fakat bu kararın karşılığında çalışan bir handler yok. Implant uyuyor, sonraki turu bekliyor. Her şeyi yakıp yıkan gizli bir varsayılan saldırı bulunmuyor.

Otonomi lafını bu nedenle ölçülü kullanmak gerekiyor. Model Windows üzerinde aklına gelen komutu yazıp uygulamıyor. Önüne konmuş dar bir menüden seçim yapıyor; seçimin hangi koda gideceğini klasik program belirliyor. Serbest irade değil. Gece vardiyasına bırakılmış küçük bir karar döngüsü.

### Karardan sonra çalışan kod

`steal` seçildiğinde üç iş birden yapılıyor. `lsassDump()` LSASS tarafına gidiyor. `dumpBrowserCredentials()` Chrome, Edge ve Firefox parolalarını hedefliyor. `extractCryptoWallets()` ise Chrome’daki MetaMask eklentisini, Exodus’u ve Ethereum yolunu arıyor. ATT&CK karşılıklarından ikisi T1003.001 ve T1555.003.

`inject` kararı shellcode üretimiyle başlıyor. Ardından iki yöntemden biri kullanılıyor: Early Bird APC injection (T1055.004) ya da `exploit_type` değeri `process_hollow` ise process hollowing (T1055.012). Model tekniği sıfırdan icat etmiyor; programın hazırladığı kapılardan birini açıyor.

Kalıcılık tarafında üç seçenek var. Registry Run anahtarına `WindowsUpdate` değeri eklenebiliyor, `schtasks` ile görev oluşturulabiliyor ya da kalıcı WMI event subscription kurulabiliyor. WMI için kullanılan PowerShell dosyası `C:\Windows\Temp\wmi.ps1`.

Listede bir de `move` bulunuyor. Dağıtım sürümünde bu kararı uygulayan handler yok. CLOSEDQUORUM’un ağ içinde yatay hareket yaptığını yazmak, incelenen dosyada bulunmayan özelliği kendimiz eklemek olur.

Toplanan veriler Discord webhook’una gidiyor. Önce AES-256-GCM ile şifreleniyor, ardından Base64 parçalarına ayrılıyor. Her parça yaklaşık 1.900 bayt; gönderimler arasında bir saniye var. Kazanan karar, gerekçesi ve makine telemetrisi de operatöre aynı kanaldan iletiliyor.

AES ifadesi ilk bakışta güçlü görünüyor. Gelgelelim simetrik anahtar tarihten türetilmiş. Yöntemi bilen biri için tarih sır değil. Bu yüzden geliştirici ile müşteri arasında gerçekten gizli bir kanal sağladığını söylemek zor.

## 📦 Talos’un çıkarsadığı satış modeli

Talos’un örnekten çıkardığı iş modeli “credentials-as-a-service.” Geliştirici, satın alan kişinin LLM API anahtarlarını ve Discord webhook’unu derleme sırasında dosyaya yerleştiriyor. Implantı hedefe ulaştırma işi müşteriye kalıyor. Sistem çalışınca saldırı sonrası kararları almak için operatörün ekran başında oturması gerekmiyor.

AI ile saldırı denince genellikle iki fayda sayılıyor. İlki hız: phishing metni ya da kod çeşidi daha çabuk hazırlanıyor. İkincisi ölçek: aynı iş daha fazla hedef için tekrarlanıyor. CLOSEDQUORUM üçüncü bir başlık açıyor; insan emeğinin saldırının belirli bir aşamasından çekilip sürekli çalışan yazılım döngüsüne aktarılması.

Benim burada dikkat çekici bulduğum taraf modelin ne kadar “zeki” olduğu değil. Operatör uyurken sistemin anket yapmaya devam etmesi. Ticari API’ler, dar karar şeması ve hazır saldırı işlevleri bunun için yetmiş.

Elbette sağlayıcılara bağımlılık sürüyor. API anahtarı iptal edilebilir, kota dolabilir, istek reddedilebilir, JSON bozuk gelebilir. Ağ kesilirse heyetin toplantısı da dağılıyor. CLOSEDQUORUM bu zayıflıkları birden fazla sağlayıcı ve tekrar deneme düzeniyle azaltmaya çalışmış; ortadan kaldıramamış.

## 🚨 Savunmada tek alarm değil, olayların sırası işe yarar

İlk sinyal, beklenmedik bir Windows sürecinin kısa sürede birden çok LLM servisine bağlanması olabilir. Tek başına yeterli değil. Aynı süreç ya da makinede LSASS erişimi, askıya alınmış sürece injection, Registry Run anahtarı, scheduled task veya WMI kalıcılığı görülüyorsa alarmın rengi değişir. Discord webhook bağlantısı da eklenince oldukça belirgin bir zincir çıkar.

TLS incelemesinin mümkün ve kurallara uygun olduğu yerlerde prompt içeriği ayrıca yardımcı olabilir. Makine bilgileriyle dolu yapılandırılmış istekler, saldırı dili ve dar karar şeması sıradan kurumsal kullanıma pek benzemez. Servis sağlayıcıları da `TARGET:` kalıbını, sistem prompt’unu ve dört karar sözcüğünün tekrarını kendi taraflarında görebilir.

Yine de tek sinyal yetmez:

- DeepSeek, Qwen, Mistral ve Gemini meşru yazılımlarda kullanılıyor.

Bu trafik LSASS erişimi, injection, kalıcılık ve aynı süreçten ya da host üzerinden çıkan Discord bağlantısıyla birlikte görüldüğünde anlam kazanıyor. İlgili agent izolasyonu sorunlarına [önceki AI gündeminde](https://www.oguzhan.co/tr/ai-gundemi-20-eylul-2026-ai-ajan-sandbox/) de yer vermiştim. CLOSEDQUORUM özelinde çevredeki kodun izin verdiği işletim sistemi işlemlerine bakmak gerekiyor.

## ⏱️ Otonomi büyük bir sıçramayla gelmedi

CAIRN’in gördüğü çizgi, 2025 ortasındaki LAMEHUG ve CERT-UA dönemi raporlarından bugüne yaklaşık bir takvim yılına sığıyor. Önce LLM yazılımın isteğe bağlı özelliğiydi. CLOSEDQUORUM’da ise birden fazla modelden oluşan heyet, saldırı sonrası aşamanın karar vericisi haline gelmiş.

“Tam otonom” ifadesini yine de dikkatli okumalı. Dört ticari API’ye, satın alan kişinin anahtarlarına, çalışan internet bağlantısına, kabul edilen isteklere, doğru JSON’a ve önceden yazılmış handler’lara muhtaç. Eşitlik kuralı tahmin edilebilir. `move` eksik. Tarihten anahtar üretmek de iyi bir sır saklama yöntemi sayılmaz.

Fakat bu kusurlar mimarinin verdiği mesajı küçültmüyor. Hangi saldırının seçileceğine model API’leri karar veriyor; seçilen işi önceden yazılmış Windows kodu yürütüyor. İnsan operatör her sorguyu izlemese de döngü devam edebiliyor.

Karşımızda her şeyi bilen bir model yok. Parola çalma, injection, kalıcılık ve veri sızdırma işlevlerine bağlı, sınırları önceden çizilmiş bir karar paneli var. Savunmanın araması gereken de modelin şahane zekâsı değil; API trafiğiyle host üzerindeki eylemlerin birlikte görülmesi. Sağlayıcı adları değişebilir. Savunma açısından kalıcı iş, bu iki sinyal grubunu ilişkilendirmek.

## 📚 Kaynaklar

- Cisco Talos, [“The CLOSED QUORUM: Inside the first reported autonomous AI C2 implant”](https://blog.talosintelligence.com/the-closed-quorum-inside-the-first-reported-autonomous-ai-c2-implant/), 22 Eylül 2026.
- Cisco Talos, [“Introducing CAIRN: Frontier tracking for AI-integrated malware”](https://blog.talosintelligence.com/introducing-cairn-frontier-tracking-for-ai-integrated-malware/), 22 Eylül 2026.
