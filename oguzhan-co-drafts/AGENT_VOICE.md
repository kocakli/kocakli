# oguzhan.co agent voice pack (pass to Cloud Agents)

Coordinator: Grok/AI Blog Bot. You (Cloud Agent) WRITE prose. Coordinator publishes to WordPress.

## Pipeline
1. Coordinator supplies FACTS brief (EN sources, numbers, URLs) + this voice pack.
2. Cloud Agent (default model: gpt-5.6-sol unless user named another) drafts:
   - `drafts/en-....md` first (original English)
   - `drafts/tr-....md` second (ORIGINAL Turkish — never line-translate EN)
3. Coordinator reviews for calques/slop, then WP publish (Polylang, Yoast, IndexNow).

## EN voice (anti-slop)
- Uneven burstiness; short punch next to longer specific sentence
- Ban: em dash —, delve/tapestry/landscape/robust/leverage/underscore/pivotal clusters
- Ban: not-only-but-also stacks, "In this article we will", phantom experts, uniform paragraph rhythm
- Specific nouns: product names, dates, %, CVE counts, org names
- First-person OK for digests/weeklies; open with the fact

## TR voice (Dünya Halleri / M. Serdar Kuzuloğlu canon — https://bulten.mserdark.com/)
Studied corpus: 55 issues (215–269). Register:
- Personable short opener (not "Bu yazıda ele alacağız")
- Story → concrete fact/number/name → source link
- Keep EN proper nouns (OpenAI, Claude, CVE, FINRA, Wired…)
- Dry one-line aside OK; brochure Turkish banned (-mektedir, günümüzde, sonuç olarak, devrim niteliğinde, oyun değiştirici)
- NEVER English rhetoric calques:
  - receipts → not makbuz; use "somut döküm / olanlar / dosyalar"
  - theater → not tiyatro default; "şov / duyuru gürültüsü"
  - slide deck landed → not "slayt destesi olarak indi"
  - standards body/organ → **standartlar kuruluşu/kurumu** NEVER "standart organı"
  - "policy spine started just before the window" → NEVER "politika omurgası pencerenin…"
    Natural: "Bu haftanın politika tartışması aslında hafta başlamadan açıldı ve Pazar’a kadar kapanmadı."
- Read aloud test: if it only works because English metaphor sits underneath, rewrite the thought in Turkish first

## Formats (oguzhan.co)
- A daily digest: multi-story, first person, shorter
- B deep dive Wed/Sat: one topic, sourced
- C Sunday weekly: WORLD bulletin (HN + primary EN tech), NOT recap of own blog posts; Kuzuloğlu weekend-magazine energy

## Full skill dump
---
name: oguzhan.co human voice (anti AI-slop)
description: >-
  Use for every oguzhan.co EN/TR draft. Natural Turkish (keep tech English when
  native), uneven human rhythm in English, ban detector-friendly AI patterns.
  Apply before publish; rewrite drafts that smell translated or template-AI.
---

# oguzhan.co human voice (anti AI-slop)

User rule (2026-09-20): TR must read as native blog Turkish, not English-with-Turkish-words. EN must not read as ChatGPT template. Past posts stay; new and same-day rewrites follow this.

## Turkish — native first

### Keep English when Turkish would blur meaning
OK / preferred in tech register: AI, agent, sandbox, prompt, eval, benchmark, CVE, patch, model, frontier, misalignment, deploy, API, latency, token, fine-tune, RAG, jailbreak, red team, SOC, CVE flood, FINRA (as analogy label).
Do **not** force calques like “hizasızlık” for every misalignment, “değerlendirici” spam, or “yaşanmış hava” for “lived weather.” Prefer the English term + short Turkish gloss once if needed.

### Hard TR bans (AI / çeviri kokusu)
- `-maktadır / -mektedir` stacks; same sentence-ending rhyme
- `sadece X değil, aynı zamanda Y` / `mesele X değil Y` spam
- Bürokratik dolgu: `kapsamında`, `bağlamında`, `noktasında`, `doğrultusunda` stacks
- Her cümlede gereksiz `bir` (English a/an residue)
- Her cümlede gereksiz `siz/ben` (Turkish is pro-drop)
- Em dash `—`; decorative en dash
- Broşür: `eşsiz`, `büyüleyici`, `oyun değiştirici`, `devrim niteliğinde`
- Şablon açılış/kapanış: `Günümüzde…`, `Sonuç olarak…`, `Kısacası…` paragraph seals
- SEO focus phrase jammed into every H2 like a robot

### TR rhythm (do this)
- Mix short punches with longer flowing sentences; vary openings
- Chain verbs with commas when natural: “okudum, not aldım, kaynaklara döndüm”
- Prefer spoken-blog Oğuzhan: concrete verbs, numbers, names, mild opinion
- One idea per paragraph; no “mini summary” closing every section
- If a sentence sounds like English word order with Turkish vocabulary, rewrite until it doesn’t

### TR quality gate
Read aloud. If a native reader would say “bu AI çevirisi,” do not publish.

## English — anti-detector / anti-slop

Detectors lean on **rhythm + scaffolding**, not single banned words. Still avoid high-frequency AI vocabulary clusters.

### Hard EN bans
- Em dash `—`; delve, tapestry, landscape, robust, leverage, underscore, pivotal, testament, realm
- `It's worth noting`, `In today's fast-paced…`, `At the end of the day`, `Not only X but also Y` stacks
- Rule-of-three padding; every paragraph same length; every sentence ~15–20 words
- Phantom experts (“experts say”) without a named source
- FAQ/roadmap intros (“In this article we will…”); symmetric “Challenges / Future” closers
- Polished corporate neutrality with zero stance

### EN rhythm (do this)
- Burstiness: short line next to a longer, specific one
- Specific nouns: product names, dates, percentages, CVE counts, org names
- Occasional imperfect aside or judgment in first person (digests/weeklies)
- Open sections with the fact, not a throat-clear
- Vary sentence openings; don’t start four sentences with “The” / “This” / “AI”

### EN quality gate
If GPTZero-style “uniform scaffold + low burstiness” would light up, rewrite for uneven cadence and concrete detail before publish.

## Process for every new post
1. Draft EN with this skill in mind.
2. Draft TR as **original Turkish**, same facts — never line-by-line translation.
3. Pass both through the bans above.
4. Only then Yoast / publish.

## Out of scope
Do not mass-edit historical posts unless the user asks. Same-calendar-day corrections are in scope when requested.


### Institutional English → Turkish (never calque)
- EN **standards body / standards organ / regulatory body** → TR **standartlar kuruluşu** / **standartlar kurumu** / **standartlar kurulu** (matches Turkish tech press on the Hassabis/DeepMind FINRA-like proposal).
- NEVER write **standart organı** or **AI organı**. In Turkish *organ* is a body part or a political “state organ”; it is not the default noun for an industry SRO.
- EN **self-regulatory organization (SRO)** → TR **özdenetim kuruluşu**, or spell out **FINRA benzeri kamu-özel standartlar kuruluşu**.
- When unsure: check Turkish coverage of the same story and mirror their noun; keep the English proper name in parentheses once.


## TR voice lock: Dünya Halleri / mserdark (primary model)

**Canon:** https://bulten.mserdark.com/ — M. Serdar Kuzuloğlu, *Dünya Halleri*.  
**Corpus studied (2026-09-20):** 55 consecutive weekly issues (`dunya-halleri-215` … `269`), stored under `/workspace/seo/mserdark-voice/`.  
**Rule:** Every new oguzhan.co **Turkish** digest/weekly/deep-dive must read like it could sit next to a Dünya Halleri issue: same register, rhythm, and source habits — not a translation of an English draft.

### What that voice actually does
1. **Opens as a person, not a briefing bot.** Often a short personal aside, a wry note, or “bu hafta X uzayınca Y’yi çıkardım” before the news. Never “Bu yazıda ele alacağız.”
2. **Story → fact → link.** Names, numbers, who said what, then the primary link woven in. No abstract thesis paragraph before the news.
3. **Category energy, magazine flow.** Sections feel like labeled trays (genel, YZ, ağ, keşif…) but prose inside is continuous, not bullet-essay.
4. **Keeps global proper nouns in original form.** OpenAI, Claude, Gemini, CVE, FINRA, Federal Register, Wired… Turkish wraps them; it does not rename them into clumsy calques.
5. **Opinion is dry and brief.** One sharp clause (“restini gördü”, “bol su kaldırır cinsten”, “belgeseli çekilse yeridir”) — not motivational essay.
6. **Rhythm is uneven on purpose.** Corpus mean ~15 words/sentence, high variance (short punches next to 25–30 word explainers). Starts often with *Bu / Ancak / Fakat / Ek / Bunun…* — not identical scaffolds.
7. **Zero AI-brochure Turkish.** In 40+ issues: no `günümüzde`, `sonuç olarak`, `önemle belirtmek`, `-maktadır/-mektedir`, `devrim niteliğinde`, `oyun değiştirici`.

### Hard “write like DH” checklist (before publish TR)
- [ ] Could this paragraph appear under a 🤖 Yapay Zeka Gündemi heading without smelling like ChatGPT-TR?
- [ ] Did I invent a metaphor that only exists because English had “receipts / theater / landed / slide deck / organ”? If yes, delete and restate in plain Turkish.
- [ ] Are institutions named the way Turkish press names them (`standartlar kuruluşu`, not `standart organı`)?
- [ ] Is there at least one concrete number, proper name, or dated event per major claim?
- [ ] Read aloud: do I sound like a columnist talking to “dostlar,” or like a model summarizing bullets?

### Steal these moves (patterns, not plagiarism)
- “Uzunluğundan dolayı… devam bağlantısı” honesty about length — rare; prefer cutting.
- “Olumlu gelişmelere gelirsek; …” soft turn inside a section.
- “Notlarımızda bulunsun.” / “Belgeseli çekilse yeridir.” — short editorial stamps.
- Parenthetical asides for precision: `(yazılım botu değil elbette; bildiğimiz yüzen bot)`.
- English tech term first, Turkish only when it clarifies: `YZ` after `yapay zeka` once, then free mix.

### Do not cargo-cult
- Don’t copy his personal life openers (tatil, Yunan adası, Oksijen gazetesi) unless they’re truly Oğuzhan’s week.
- Don’t paste his section emoji set wholesale if the theme layout differs; take the **prose**, not the costume.
- Don’t inflate with fake intimacy. Warm ≠ fluffy.

### Rhetoric calques (EN scaffold ≠ TR prose)
Never transplant English columnist skeletons word-for-word:
- “I needed this week’s **receipts**” ≠ “bu haftanın **makbuzlarına** ihtiyacım vardı” → “bu hafta olanlara bakmak istiyordum” / “eldeki somut döküm”
- “**launch theater**” ≠ default “lansman **tiyatrosu**” → “lansman şovu” / “duyuru gürültüsü”
- “**landed** as a slide deck” ≠ “slayt destesi olarak indi” → “böyle kapandı” / “sunum gibi değil, sahada”
- “**cameo**” → “figüran” / “bir an görünüp kaybolan X”
- “CVE **tsunami**” → “CVE seli” / “yama seli”
Test: if the Turkish only works because an English metaphor is underneath, rewrite the thought in Turkish first.

### Institutional English → Turkish
- standards body/organ → **standartlar kuruluşu / kurumu / kurulu** (never **standart organı**)
- SRO → **özdenetim kuruluşu** or **FINRA benzeri kamu-özel standartlar kuruluşu**

## Process for every new post
1. Draft EN with anti-slop rules.
2. Draft TR as **original Turkish** in Dünya Halleri register (same facts) — never line-by-line from EN.
3. Run DH checklist + bans above.
4. Only then Yoast / publish.

## Out of scope
Do not mass-edit historical posts unless asked. Same-calendar-day corrections are in scope when requested.


## Dünya Halleri style excerpts (samples — do not plagiarize personal openers)
# Dünya Halleri: 269 (dunya-halleri-269)

Bazılarınıza tuhaf gelecek bir açıklamayla başlamak istiyorum. Yorumlarda sık sık “ bahsettiğiniz falanca konu hakkında bir kaynak site var mı? ” gibi sorulara denk geliyorum. Sevgili dostlar; bu bültende okuduğunuz her gelişme için bazen onlarca farklı kaynak tarıyor ve içlerinde ve bilgi verici olanı özene bezene seçerek metnin içine mutlaka ekliyorum. Mevcut temada turuncu renkli sözcüklere tıklayarak ulaşabilirsiniz. 🤓 Bu hafta Oksijen gazetesinde yapay zeka şirketleriyle gündeme gelen token tabanlı yeni bir finansman modeline yer verdim . Gerekçelerinden birini bu sayıdaki “Yapay Zeka Gündemi” başlığında okuyabilirsiniz. Blogumda ise OpenAI’ın (hesapta) kapalı devre siber güvenlik testinde yaşanan ve akılalmaz gelişmelere sahne olan deneyini yazdım . Belgeseli çekilse yeridir. Bültene gelirsek; uzunluğundan dolayı e-posta üzerinden okuyanlarda yarıda kesilecek. Lütfen devam bağlantısına tıklamayı unutmayın . Sağlık kategorisinde oldukça ilginç gelişmeler var. Kapanış da sürprizli. 🌍 Genel Gündem Böyle adlandırmaya dilim varmıyor fakat ilginç bir şekilde dünya gündeminde ve piyasalarda “düşük yoğunluklu” algılanan bir savaş dalgasının içindeyiz. Teknoloji de tarihte olmadığı kadar büyük bir paya sahip. Dronlar ile perdesi aralanan yeni nesil savaşın ikinci dalgası, yapay zeka (YZ) destekli ve otonom sistemler . Üstelik artık tam bir distopyayı andırır şekilde birbirleriyle savaşıyorlar (insan kaybından iyidir mi desek?). Otonom olMAmakla birlikte ilk örnek elbette Rusya - Ukrayna cephesinden geldi. Ukrayna donanmasına ait uzaktan kumandalı 7 metrelik bir savaş botu (yazılım botu değil elbette; bildiğimiz yüzen bot ), Rusya’ya bağlı 5 metrelik bir diğer uzaktan kumandalı savaş botunu ağır makineli silahıyla batırdı . Savaş tarihinde yeni bir sayfa daha. Notlarımızda bulunsun. Olay anından bir kare. Ek bilgi: H I Sutton’ın yazıda da bahsi geçen Bluesky hesabına da bakmanızı tavsiye ederim. Bu yeni nesil muharebeye yönelik çok ilginç bir arşive sahip. ( Şu video da izlenesi.) Yeni nesil muharebeden devam edelim. İran’ın 6 ay önce vurduğu Amazon’un Bahreyn ve Birleşik Arap Emirlikleri’ndeki (BAE) veri merkezlerinde kayıplar kalıcı hale geldi . BAE’de 135, Bahreyn’de 144 hizmet halen ve tamamen durmuş halde . Daha da enteresan bir gelişme. ABD Hazine Bakanlığı, İran’ın Hürmüz Boğazı’ndan geçen gemilerden aldığı “ güvenli geçiş ” ücretlerinin bir bölümünü Bitcoin üzerinden tahsil ettiğini keşfederek bu amaçla kullanılan İran merkezli BitBank platformunu ve y


---

# Dünya Halleri: 264 (dunya-halleri-264)

Tatil yörelerinde memleket gündeminden koptuğu için ne kadar memnun ve huzurlu olduğundan bahsedenlere denk geliyorum. “Ne İsa’ya ne de Musa’ya yaranmanın mümkün olmayacağı” bu tehlikeli konuyu burada açmak vardı ama yükü sırtımdan atıp, size devredeyim. Sandığımızın aksine son derece kısıtlı zamanımızı ve zihin “ kapasitemizi ” neye harcadığımıza dikkat edelim dostlar. Bazı şeyler “ tercih ” ile şekilleniyor. Bu uğurda size yine bol bol malzeme topladım. 🌍 Genel Gündem Beğendiklerim ve beğenmediklerimle Güney Kore’nin zihnimdeki yeri ayrı. Dünya Halleri bülteni özelindeki en önemli kısmı şu: Biz Türkiye olarak sanayi ve teknoloji yolculuğuna Güney Kore ile aynı zamanda ve aynı noktadan başladık. Fakat olayın seyri ve sonuçlar çok farklı oldu. Sebepleri muhtelif. Güney Kore Cumhurbaşkanı Lee Jae Myung bu hafta “ Seven Major SEED ” (Yedi Temel TOHUM) adlı ulusal strateji planını açıkladı . Yeni nesil enerji (modüler nükleer reaktörler ve füzyon enerjisi ), kuantum teknolojileri, uzay ve ileri biyoteknoloji, kritik madenler ve tedarik zinciri gibi başlıklar altında birçok teşvik programı içeriyor . Ek bilgi: En güncel IMF verileri ışığında nominal gayrısafi yurtiçi hasıla (yani bir yılda üretilen toplam ekonomik değer) olarak Güney Kore 1,93 trilyon dolar, Türkiye ise 1,64 trilyon dolar seviyesinde. Güney Kore’nin kişi başı (nominal) ekonomik üretimi 37 bin 410 dolar iken Türkiye’de bu tutar 19 bin 20 dolarda. (Gelir dağılımındaki adaletsizliğini gözardı ediyorum.) Önümüzdeki dönemin en büyük pazarlarından biri hiç şüphesiz YZ destekli bireysel ve endüstriyel insansı robotlar olacak. Smart Analytics Global şirketinin raporuna göre 2026’nın ilk yarısında bu alandaki satışlar 19 bin 100 adede ulaşmış. Daha da ilginci, bunun yüzde 97’si Çinli markalara ait . Ek bilgi: Yüzde 44 pazar payıyla bu alanın en büyüğü ( Çinli ) Unitree, Shanghai Borsası’nda 900 milyon dolarlık halka arz gerçekleştirdi. Bireysel yatırımcılardan 8 bin kattan fazla talep görerek . (Kuruyemiş sektörünü de ihmal etmeyin .) Tekrar gibi olacak ancak Apple cephesinden güvenilir kaynaklar iPhone 18’in 2027 yılına ertelendiği konusunda ısrarcı . (Bu yıl sadece iPhone 18 Pro ve iPhone 18 Pro Max satışa sunulacak.) Ek bilgi: TrendForce’un araştırması , özellikle bellek donanımı alanında yaşanan tedarik sorunları sebebiyle iPhone 18 Pro’nun üretim maliyetinin neredeyse yüzde 40 oranında artacağını gösteriyor. Google ise bu hafta akıllı telefonu “ Pixel 11 ” serisine ait yeni modelleri ve “ Pixel Wa


---

# Dünya Halleri: 254 (dunya-halleri-254)

Haziran ayının ilk sayısından merhaba. Bu hafta blogumda Amazon’un kurucusu olarak tanınan Jeff Bezos’un CNBC kanalındaki ses getiren röportajından ilhamla, Ayn Rand ile Peter Thiel arasında salınan, yeni nesil “ara form tekno-liberteryen” akıma yönelik bir yazı yayımladım . Oksijen gazetesindeki sayfamda ise aynı akımın ikonik isimlerinin liderliğinde ilerleyen “tarihin gördüğü en büyük halka arz” sürecinin ayrıntılarına baktım . Trilyon dolarların havada uçuştuğu ve sorgulamanın günah sayıldığı, enteresan bir dönemden kesitler. En azından tarihe not düşmüş olalım. Podcast dinleyicilerim “Haddini Aşan Yaşam Rehberi” ne oldu diye sorup duruyor. Yeni bölümler çektik ama bilemediğim bir sebepten henüz yayına girmedi. Ama en azından yanıtım net: “Hayır. Henüz yaz tatiline girmedi”. Benden bir şeyler dinlemek isteyenler için Aslı Şafak’ın konuğu olarak katıldığım (sanıyorum bir ay önce çektiğimiz ve bu hafta yayımlanan) “İşin Aslı” programına bakabilir. Şimdi gelelim esas meseleye. 🌍 Genel Gündem “ Freedom Ship ” (Özgürlük Gemisi) ismi taşıyan bir proje, bende nedense haksız yere tutsak edilmişleri kurtaran türden bir izlenim yaratıyor. Ama değil. Bu proje, “ Floating City ” adlı 80 bin kapasiteli, nükleer enerjiyle çalışan dev bir seyir (cruise) gemisiyle 2 yıl sürecek bir dünya turunu içeriyor. Bu seyahat 50 bin yolcu, 10 bin günlük ziyaretçi ve 20 bin mürettebat ile gerçekleşecek. 1 mil ( 1,6 km ) uzunluğundaki gemide 24 kilometre yürüyüş parkuru ve 30 güverte yer alacak. Hatta hastane, okul, çalışma alanları, 15 bin kişilik stadyum, opera salonu, kumarhane gibi daha pek çok şey... Maliyeti 16 milyar dolar . Böyle düşününce bizim gibilerin arasında tutsak hayatı yaşayan seçkinlere özgürlük getirecek gibi. Videosunu MUTLAKA izleyin. Hatırlar mısınız bilmem; bir zamanlar Elon Musk’ın özel uçağının koordinatını açık kaynaklardan takip ederek paylaşan “ ElonJet ” adlı bir Twitter hesabı vardı. Musk bundan pek hoşlanmamış olacak ki, “ ifade özgürlüğü getirmek ” amacıyla satın aldığı Twitter’da ilk iş olarak bu hesabı kapattırmış ve sahibini dava edeceğini açıklamıştı . Hatta ABD Havacılık İdaresi (FAA), durumdan vazife çıkararak özel uçakların takibini zorlaştırıcı düzenlemeler getirmişti . ElonJet o günden beri hayatına BlueSky platformunda devam ediyor . Musk onu da satın alana dek diyelim. Elon Musk’ın birden çok özel uçağı var. Ama en sık kullandığı, 78 milyon dolarlık bu nadide model. Bu eski defterleri neden karıştırdığıma gelelim. Kyle McDonald adlı bir s


---

# Dünya Halleri: 239 (dunya-halleri-239)

Bu hafta yoğunluktan ne Oksijen gazetesindeki sayfamı, ne de podcast bölümünü yapabildim. Bunun yarattığı vicdani azabı bültene yüklenerek gidermeye çalıştım. Ama blogumda ilginç bir konu sizi bekliyor: Bir senede 200 aşk romanı yazarak köşeyi dönen bir kadın yazar . Sırrını tahmin ettiniz mi? Haydi başlayalım. 🌍 Genel Gündem Bir parola yöneticisi kullanıyor musunuz bilemiyorum. Mutlaka kullanın. Ben çok uzun zamandır ücretli bir çözüm ile ilerliyorum fakat dilerseniz ücretsiz birçok seçenek de var (Şahsi tavsiyem ücretsiz Proton Pass fakat sanıyorum web sitesi Türkiye’den engelli . Siz bir yolunu bulursunuz.) Ek bilgi: En basit tanımıyla bu uygulamalar sizden bir ana parola belirlemenizi istiyor. Ardından mevcut ve sonradan eklenecek tüm parolaları kendisi saklıyor. Gerektiğinde size ana parolayı sorup onayladıktan sonra, site ya da uygulamada kendisi dolduruyor. Tüm diğer cihazlarınızla eşzamanlı (Türklerin daha sevdiği bir tabirle “ senkronize ”) hale getiriyor. Yeni bir tanesini oluşturmanız gerektiğinde son derece güçlü parolalar üretiyor. Dolayısıyla bir daha hiçbir parolayı hatırlamak zorunda kalmıyorsunuz. Her yerde aynı parolayı kullanma tehlikesinden de kurtuluyorsunuz. Bu uygulamaların tek marifeti parola saklamak da değil . Kredi kart bilgilerinizi ve benzeri tüm dijital dosyalarınızı da benzer şekilde koruyor ve her cihazınızdan erişilebilir hale getiriyor. Bu uzun girizgahın sebebine gelince: Şimdiye dek parola yöneticilerinin hepsi “ bizim hiçbirinizin bilgilerine erişimimiz yok ” diye kendini pazarlıyordu. Ancak ETH Zürich ve USI Lugano üniversitelerinin konuyla ilgili araştırması , durumun her zaman öyle olmayabileceğini ortaya koydu. Örneğin Bitwarden uygulamasında “hesap kurtarma” ya da “grup paylaşımı” açıkken sahte anahtarlarla tüm verilere erişilme ihtimali var. LastPass ’te kullanıcı parolası sıfırladığı zaman saldırgan tarafı süper yöneticinin anahtarlarını doğrulama gerektirmeden alabiliyor. Dashlane ve 1Password de benzer açıklara sahip . Özetle; uygulama ayarlarınıza dikkat edin ve güçlü bir ana parola kullanın . Hiçbir şeyin asla güvencede olmadığı, garip bir dönemdeyiz. Uzun süre hayatta kalmanın sırrı malum 👇 2025 yılını 1,15 trilyon dolar büyüklüğe ulaşan Suudi Arabistan Varlık Fonu’nun oyun sektörüne yönelik yatırımlarından önceki sayılarda sıkça bahsetmiştim . Fon yönetimi bu hafta sürpriz bir kararla ikinci büyük ortağı olduğu ve Grand Theft Auto, NBA 2K, Red Dead Redemption ve Civilization gibi birçok başarılı oyunun geli


---

# Dünya Halleri: 219 (dunya-halleri-219)

Teknoloji dünyasındaki batışların birçoğunu duymuyoruz. Sonrasında yaşananları da. Bu hafta Oksijen gazetesindeki sayfamda teknoloji şirketlerinin iflaslarının ardından otomobilleri yürümez; hatta gözleri görmez hale gelen mağdurlara yer verdim . Blogumda ise yılda 800 milyar dolar zarar eden ve yakın gelecekte kara geçecek gibi görünmeyen yapay zeka (YZ) sektöründe değirmenin suyunun nerden geldiğine baktım . (Sadece OpenAI bu yılın ilk yarısında 4,3 milyar dolar gelire karşılık 13,5 milyar dolar zarar yazdı .) Ben yazıyı yazdıktan sonra gündeme gelen birkaç güncel gelişmeyi de paylaşayım. Singapur’da düzenlenen Milken Institute’ın 2025 Asya Zirvesi ’nde uzmanlar YZ şirketlerinin topladığı rekor seviyedeki risk sermayesi ve fonların “şişme” belirtisi gösterdiğine dikkat çekti . Etkinlikte yayımlanan rapora göre sadece bu yılın ilk çeyreğinde YZ girişimleri (toplam risk sermayesi yatırımların yüzde 57,9 ’una denk) 73,1 milyar dolar toplamış. İtalya Teknoloji Haftası kapsamında sahne alan Amazon’un kurucusu Jeff Bezos da benzer şekilde YZ sektörünün balon misali şiştiğine dikkat çekti . Citigroup ise teknoloji devlerinin bu alana yapacağı yatırımın 2029 yılında 2,8 trilyon doları geçeceğini öngörüyor . Özetle tam bir “ kazanan her şeyi alır ” oyunu kurulmuş halde. Şimdi gelelim dünyadan diğer güncel gelişmelere. 🌍 Genel Gündem Maria Branyas Morera, İspanya’da yaşayan bir kadındı. Geçtiğimiz yıl, 117 yaşında aramızdan ayrıldı. Barcelona Üniversitesi, “dünyanın en yaşlı insanı” unvanına sahip Morera’dan (yaşarken) topladığı biyolojik örnekler ile uzun ömrünün sırrı üzerine bir çalışma yapmış . Sonuçlara göre yaşam tarzı olarak sakin bir kasabada, basit bir hayat sürmek, sürekli zihinsel faaliyetler içinde olmak, sosyal bağların güçlü olması, Akdeniz diyeti ile (zeytinyağı, sebze, yoğurt ve peynir ağırlıklı) beslenmek, sigara ve içki tüketmemek belirleyici olmuş. Biyolojik olaraksa düşük iltihap düzeyi, düşük oranda kötü kolesterol, yüksek oranda iyi kolesterol, sağlıklı bağırsak mikrobiyomu ve güçlü bağışıklık sistemi öne çıkmış . ( 113 yaşındayken Covid-19’u da yendiğini de eklemiş olayım.) Huzur içinde uyu Maria Branyas Morera. ABD Başkanı Donald Trump, ülkesinde teknoloji sektörünün özel yetenekli yabancı uzmanları istihdam etmek için yoğun olarak kullandığı “ H-1B ” tipi vizenin yıllık harç bedelini 100.000 dolara çıkarmayı planlıyor. Bunu fırsat bilen Çin ise karşı hamleyle “ K vizesi ” adlı yeni bir seçeneği yürürlüğe soktu . Bu program bilim, teknoloji

