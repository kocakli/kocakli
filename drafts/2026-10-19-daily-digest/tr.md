---
title: "OpenAI misalignment raporları, eğri tohumları ve open-weight haftası"
slug: openai-misalignment-raporlari-claude-ecdsa-tohumlari
excerpt: "OpenAI'ın haziran vakaları 15 Ekim'de yayımlandı, Fortune'a göre ikisi kritik. Claude, NIST eğri tohumlarını 1997 zaman damgalarına bağladı. Üç open-weight model ve Anthropic'in giriş kademesi payları da aynı günlerde geldi."
focuskw: "OpenAI misalignment raporları"
yoast_title: "OpenAI misalignment raporları ve eğri tohumları"
yoast_metadesc: "OpenAI hazirandan dört misalignment vakası yayımladı, ikisi kritik. Claude, NIST tohumlarını 1997 zaman damgalarına indirdi. Üç open-weight model de çıktı."
categories: Yapay zeka
---

OpenAI misalignment raporları 15 Ekim'de çıktı: Haziran'dan dört vaka, [Fortune](https://fortune.com/2026/10/16/openai-discloses-four-more-rogue-incidents-involving-financial-medical-and-government-data/)'a göre ikisi kritik. [Cüzdan raporuna](https://alignment.openai.com/misalignment-reports/using-a-funded-test-cryptocurrency-wallet-without-authorization/) göre bir model Sepolia'da kendisine ait olmayan test ETH ile ücret ödedi, [pano raporu](https://alignment.openai.com/misalignment-reports/accessing-and-changing-internal-systems-during-dashboard-research/) ise kamu rakamı ararken 147.451 satır kapalı veri indirdiğini yazıyor. Dördü eğitim, değerlendirme ve iç kullanımda, aralarında ChatGPT müşteri hesabı yok.

## 🚨 OpenAI misalignment raporları: Haziran'dan dört vaka, ikisi kritik
<!-- INLINE: openai-agent-borrowed-keys -->

[OpenAI'ın sayfası](https://alignment.openai.com/misalignment-reports/) dört metni 15 Ekim'de koymuş, hepsi Haziran. Fortune'a göre sayfada 19 vaka var, üçü ağustos ya da eylüle kadar bilinmiyormuş, yeni dördün ikisi kritik.

- Bakiyeli test kripto cüzdanını yetkisiz kullanmak (26 Haziran)
- Pano araştırmasında iç sistemlere erişip değiştirmek (17 Haziran)
- Devlet istatistik sitesinde sunucu sırlarını alıp yetkiyi aşmak (17 Haziran)
- Dış tarayıcıyla internet kısıtlarını dolaşmak (16 Haziran)

GPT-5.6 Sol ailesinden iç araştırma modeli, eğitimde kripto alım satım prototipini güncelleyecek, sözleşmeleri Sepolia'ya (Ethereum test ağı) dağıtacakmış. Bakiyeli cüzdan yok. OpenAI'ın cüzdan raporuna göre herkesçe bilinen kurtarma cümlelerinden 362 adres taramış, Sepolia ETH bulmuş, ücreti ödemiş. Chain of thought etik mi diye sormuş. Rapordaki ifadeyle fonlar "fiilen sahipsiz", Sepolia "değersiz". Dağıtım tutmuş. Kaynak final raporunda yok (26 Haziran, keşif 25 Eylül 2026). OpenAI'ın cümlesiyle model "hesap sahibinin izni yerine, olası zarar hakkındaki kendi hükmünü koyabiliyor". Test ETH'in piyasa değeri yok.

OpenAI'ın pano raporuna göre "oldukça ısrarcı bir iç model", değerlendirmede, uluslararası bir araştırma kuruluşunun kamu panosundan yayımlanmış rakam isteyecekmiş. İnternet yalnız HTTP GET. Herkese açık JavaScript'ten canlı OpenSearch kimliğini almış, 1.489 kullanıcı kaydı (ad ve e-posta) indirmiş, küme ayarını değiştirmiş. İkinci koşuda token ayarını değiştirmiş, bulut depolama token'ı almış, beş kapalı tabloda 147.451 satır indirmiş. Ayarı geri almış, token'ı kullanmaya devam etmiş. "Ama etik mi?" deyip "doğruluğa odaklan" demiş, açıklamamış. Beş yanıtın beşi, her değerlendirmede yanlış. Keşif 13 Ağustos 2026.

Fortune'a göre istek engellenince model erişim kontrollerini aşmış, adı verilmeyen bir devlet sitesinden 24 yıllık hastane yatağı verisi indirmiş.

Raporlar ve Fortune: sıkılaştırılmış güvenlik kontrolleri, eğitim ve değerlendirmede canlı internet yok, alignment puanı iyileşti, izleme tüm RL (pekiştirmeli öğrenme) ve değerlendirme trafiğine yayıldı. Temmuzdaki Hugging Face olayından sonra monitör geçmişe dönünce vakalar çıkmış.

[11 Ekim haftalığında](https://www.oguzhan.co/tr/ai-haftalik-5-11-ekim-2026-yemin-ve-ajanlar/) OpenAI'ın eski vakaları taradığını yazmıştım. Bu sayfa o tarama.

## 🔐 Eğri tohumları bir espri cümlesinden mi çıktı?
<!-- INLINE: ecdsa-timestamp-seeds -->

Hayır. Zaman damgası. [Anthropic'in 16 Ekim yazısına](https://www.anthropic.com/research/ecdsa-curve-origins) göre içerdeki Claude buna yarım saatten kısa sürede varmış.

NIST, ECDSA eğrilerini 2000'de FIPS 186-2 ile almış. Tohumun hash'i katsayıyı belirliyor. NSA tohumları açıklamasız vermiş, bu yıllarca arka kapı şüphesini beslemiş.

Jerry Solinas (NSA, 2015) tohumların bir espri cümlesinin hash'i olduğunu söylemiş, kabaca "Bob ve Jerry'ye zam yapın". 2023'te ölmüş.

Ekim 2026'da bir çalışan, ipucunu vermeden, sandbox'taki araştırma modeline sormuş. Claude P-192, P-224, P-256, P-384 ve P-521 tohumlarını bulmuş. Hash yok: C kütüphanesindeki `lrand48` çıktısı, Unix zaman damgasıyla başlatılmış. Anthropic'e göre P-256, 16 Ağustos 1997, 01:52:34 UTC'de tohumlanan koşunun 1.842 numaralı adayı. Asal eğri damgaları Mayıs 1997 ile Nisan 1998 arasında.

Claude bazı tohumlarda her 32 bitlik kelimenin üst bitini sıfır görmüş (`lrand48` imzası), durumları geri çıkarmış, kesik çıktılarda LLL kullanmış.

Anthropic: "Bu bir kriptografi kırılması, yeni bir saldırı ya da zafiyet değil". Arka kapı "çok daha az makul". Yapılacak iş yok.

Açıkta kalanlar: B-163'ün tohumu, P-224, P-256, P-384 ve P-521 taban noktaları. P-256'da 876 numaralı aday da tutarmış, neden geçildiği bilinmiyor.

Filippo Valsorda'nın 36.864 dolarlık ödülü, Let's Encrypt'in arkasındaki Internet Security Research Group'a gidecek. Anthropic, tohumları üreten Python'u CC0 ile yayımladı. Betik P-256 tohumunu yeniden üretiyor.

## 🔓 Üç günde üç open-weight model

15, 16 ve 17 Ekim'de Meta, Reflection ve DeepSeek open-weight model çıkardı. Hiçbirini çalıştırmadım.

[Muse Spark Open](https://research.meta.ai/blog/muse-spark-open) doğuştan çok modlu, kod ve agent için. Meta'nın iddiası: "bugüne kadarki en yetenekli ABD open-weight modeli". Meta'ya göre MLX ile iki Apple M5 Ultra Mac Studio. Lisans Muse Model License, ticari kullanım sınırlı, OSI açık kaynağın dışında. Kapalı Muse Wonder ayrı, [15 Ekim yazısı](https://www.oguzhan.co/tr/muse-wonder-gemini-4-argon-frontier-ajanlar/).

[Beam](https://reflection.ai/blog/beam-is-available) sparse MoE, yalnız metin. BF16, FP8, NVFP4. 40'tan fazla ortak. Reflection'ın kendi kartı, [Hugging Face yazısında](https://huggingface.co/blog/reflection-beam): SWE-bench Verified yüzde 81,6 (BF16). [12 Ekim yazısında](https://www.oguzhan.co/tr/claude-internet-erisimi-anthropic-testleri/) ağırlıklar hâlâ vaatti.

[DeepSeek-V4.1-Flash-1017](https://huggingface.co/deepseek-ai/DeepSeek-V4.1-Flash-1017), [günlükte](https://api-docs.deepseek.com/updates) "küçük güncelleme". DeepSeek'in kendi tablosu: DeepSWE v1.1 77,0 (önce 74,2), Opus 5 74,0, Terminal-Bench 4.0 42,3 (önce 31,2). API `deepseek-flash`, fiyat aynı. Aynı gün Search ve Fetch, uç başına 1.000 çağrı 0,75 dolar. @deepseek_ai faturalamayı 31 Ekim 2026, 16:00 UTC (İstanbul 19:00) diyor.

| Model | Laboratuvar | Tarih | Boyut (toplam / aktif) | Bağlam | Lisans |
|---|---|---|---|---|---|
| Muse Spark Open | Meta | 15 Eki 2026 | 816B / 42B | 1M token | Muse Model License |
| Beam | Reflection | 16 Eki 2026 | 501B / 23B | 1M token | Apache 2.0 |
| DeepSeek-V4.1-Flash-1017 | DeepSeek | 17 Eki 2026 | n.d. | 1M önerilen | MIT |

Ağırlığı çalıştıran, yukarıdaki izlemeyi de devralır.

## 👩‍💻 Anthropic giriş kademesinde ne ölçtü?

[16 Ekim istihdam yazısına](https://www.anthropic.com/research/employment-at-anthropic) göre, 2025 başından beri junior teknik işe alım yüzde 27'den yüzde 9'a, teknik bölümlerdeki junior çalışan payı yüzde 21'den yüzde 14'e inmiş. Teknik işe alım mutlak sayıda artmış, yani bu bir pay. Ağustos 2026'da agent saatleri çalışan saatlerini altıya bir geçmiş. Anthropic buna runtime diyor. Nisan 2026 anketinde yüzde 20, işi yapmaktan Claude yönetmeye kaydığını söylemiş. Medyan çalışan toplantılarda bir yıl öncesine göre yüzde 20 daha fazla vakit geçiriyor. Erken uyarı kurulmuş, yeniden görevlendirme içeride. Anthropic, bunun junior alımdaki yavaşlamayı karşılamadığını kabul ediyor.

[Kamu yararı fonu](https://www.anthropic.com/news/public-benefit-fund), 18 Ekim, tamamı şirkete ait bir LLC. Hisse sahibi onaylarsa yüzde 5 şimdi ayrılır. Açıklanmayan tabanın üstünde her yüzde 50 artışta yönetim kurulu, takdirine göre yüzde 2 daha ekleyebilir. Büyük bağış ya da doğrudan dağıtım mümkün, örnek emek piyasası. Emek piyasası işine 200 milyon dolar şimdiden ayrılmış. Fon hissesi lobiye ve siyasi bağışa gitmez. Kurucu ve çalışan taahhütleriyle Anthropic, hisselerin kabaca yüzde 20'sini kamu yararına sayıyor.

Hafta sonu dördünü de okudum. Agent kendine çizilen işin dışına çıkıyor. Bunu kim yazıyor?
