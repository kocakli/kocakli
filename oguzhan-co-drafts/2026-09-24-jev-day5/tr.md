---
title: "Jev Context Compaction: Aynen Budama, Kayıplı Yeniden Yazma Değil"
slug: "jev-context-compaction-aynen-budama"
yoast_title: "Jev Context Compaction: Aynen Budama, Kayıplı Yeniden Yazma Değil"
yoast_metadesc: "Jev, ajan bağlamında eskiyen araç çağrılarını puanlar ve siler; kalan metin aynen durur. Fast-jev-compaction, Winnow ve Yoshi örnekleriyle."
focus_keyphrase: "Jev compaction"
---

## Jev Bağlamı Yeniden Yazmaz, Eskiyeni Siler

Çoğu ajan sistemi eski bağlamı başka bir LLM geçişiyle özetler. Jev farklı bir şey yapar: alakayı puanlar ve ev sahibi kod eskiyen araç çağrılarını siler; kalan metin aynen durur. [Fast-jev-compaction](https://github.com/tamaratran/fast-jev-compaction) hiçbir zaman tarihi yeniden yazmaz; her araç çağrısı için Jev'e iki evet/hayır sorusu sorar, sonra eşiğin altında kalan blokları düşürür ya da kısaltır. Geriye kalan her şey kelimesi kelimesine orijinaldir.

[Awesome-jev kataloğu](https://github.com/cobanov/awesome-jev) şunu söyler: "Kalan metnin aynen korunması, çıkarılan geçmişin gereksiz olduğunu kanıtlamaz." Olasılık, kanıt değildir.

<!-- INLINE_IMAGE_1: prune-tiers diagram -->

Jev'in compaction işindeki rolü dar: her parça için yazılı Noul sorularını yanıtla. Pin'ler, eşikler, kesik başlıklar ve yedek politikayı kod yönetir. Başarısızlık modu özetlemeden farklıdır. Yazılı bir System One modeli, hiç var olmamış bir dosya yolunu uyduramaz. *Alakayı yanlış değerlendirebilir*.

## Budama Deseni: Sor, Eşikle, Hareket Et

Desen basittir. Jev'e (ya da başka bir System One modele) bir Noul sorusu sor: "Bu araç sonucu hâlâ mevcut görevle alakalı mı?" Jev bir olasılık döndürür. Kod o puanı eşikle karşılaştırır (genelde 0,5) ve harekete geçer: tut, kısalt ya da at.

Fast-jev-compaction (tamaratran) bir Claude Code eklentisi ve npm kütüphanesidir. Pin'lenmemiş her araç çağrısı için iki Noul sorusu sorar: çağrıyı tutalım mı? Sonucu aynen tutalım mı? Üç kademe çıkar. `keepThreshold` (varsayılan 0,5) üstündeki puanlar hem çağrıyı hem sonucu tutar. Kabaca 0,2 ile 0,5 arası puanlar çağrıyı tutar ama sonucu `truncateHeadChars` kadar kısaltır (varsayılan 300) ve not ekler. Altında kalanlar tamamen kaybolur. Pin'ler basittir: ilk kullanıcı mesajı artı en yeni `preserveRecentMessages` (varsayılan 6) dokunulmadan kalır. Durum `maxStateTokens` sınırına sığdırılır (25 bin); istek yığınları `maxRequestTokens` altında kalır (30 bin). Jev hata verirse ya da azaltma yetersiz kalırsa, kanca Claude Code'un yerleşik özetine döner.

Kurtarma yolu araç yeniden çalıştırmasıdır. README açık: "Bir olasılık, sonucun silinmesinin güvenli olduğunun kanıtı değildir. Asistan her zaman aracı yeniden çalıştırabilir."

[Fast-dev-compaction](https://github.com/leonaaardob/fast-dev-compaction) (leonaaardob) aynı motor fikrini Codex'e taşır (Roblox AI ajanı); Codex tarihi Claude kancaları gibi değiştiremez. Bunun yerine tutulan parçaları yerleşik özet çalıştıktan sonra `additionalContext` olarak enjekte eder. Yazarın README'si uyarı koyar: üretim kullanımı *tavsiye edilmez*. Eleştiri Theo'dan (t3.gg) gelir: olasılıkla budama compaction'ı yanlış anlar. Kendi compaction akışlarıyla eğitilen modeller API üzerinden asla yüzeye çıkmayan akıl yürütme izlerini atar. Geçmişi düzenlemek önbellek yeniden yazmalarını tetikler. Araç fikir belgesidir, sevk edilecek kod değil. Beşinci gün için nüans sağlar: bir port bile şüphe eder.

<!-- INLINE_IMAGE_2: admit-vs-compact contrast -->

## Winnow: Kabul Anı Eleği

[Winnow](https://github.com/GhalebDweikat/winnow) (GhalebDweikat) büyük Read, Bash ya da Grep sonuçlarını Claude Code bağlamına girmeden *önce* değerlendirir. Çıktıyı kabaca 25 satırlık bloklara böler, sonra blok başına bir alakalı mı sorusu sorar (varsayılan hakim: Jev). Kesin hayır cevapları (DROP eşiğinin altında, varsayılan 0,1) üç satırlık stub artı `~/.winnow/cache/` altında yerel önbellek anahtarı haline gelir, isteğe bağlı ucuz özet eklenir. Tam bloğu sonra `winnow_recall` ile geri çağır.

Güvenlik politikası: hata çıktıları asla gizlenmez. DROP (0,1) ile KEEP (0,5) arasındaki belirsiz bant aynen kalır. Yazar gölge modu önerir, bir hafta boyunca neyin budanmış olacağını izle. 300 vakadan 97 elle etiketlenmiş vaka üzerinde yazar 0,1 altında gizlenen parçaların kabaca %5'inin temiz olduğunu ölçtü (kendi bildirimi; bağımsız test yok). Winnow ayrıca prompt zamanında bellek dosyalarını sıralar.

Kabul anı yaklaşımı şu demek: Winnow araç çıktısı başına bir kez çalışır, birikmiş geçmişte değil. Stub'lar görünür; kurtarma açıktır (anahtarla `winnow_recall` çağır). Takas anlıktır: Jev değerlendirme maliyetini bağlam baskısı compaction geçişi zorlayana kadar ertelemek yerine peşin ödersiniz.

## Yoshi: Dürüst Metrikli Proxy POC

[Yoshi](https://github.com/compozy/yoshi) (compozy) Claude Code ve Codex için yerel bir proxy. Jev, boyut kapısının üstündeki parçaları değerlendirir; kod doğrulanmış atlamaları protokolü koruyarak uygular; sağlayıcı yanıtı değişmeden akar. Yazar dürüst: bu CompozyOS'a giden deneysel bir proof-of-concept. Mevcut v12 denemeleri temel çizgiden *daha yavaş* çalıştı. Fable tanılama oturumu kabaca %34 birikmiş girdi azaltması gösterdi; Sonnet karışık oturumu neredeyse %0 tasarruf gösterdi. Birleşik maliyetler bilinmiyor çünkü Jev makbuzları deneme sırasında eksikti. Aday parçalar (Write, Edit ve Bash kaynağı dahil) Vercel AI Gateway üzerinden TypeSafe'e gider. Sıfır kesinti süresiyle geri alma (ZDR) yok.

Yoshi'yi kanıtlanmış tasarruf olarak satmayın. Değeri dürüst raporlamadır: bir POC tokenları azaltıp duvar saati ekleyebilir, ya da oturum şekline bağlı olarak hiç azaltma üretmeyebilir. GitHub yıldızları doğruluk ya da verimlilik eşittir anlamına gelmez.

## Jev Seçer, Kod Tutar

Jev yazılı Noul olasılıklarını yanıtlar. Ev sahibi kod politikaya karar verir. Fast-jev-compaction son mesajları ve açılışı pin'ler; Winnow hata çıktılarını ve belirsiz bantı pin'ler; Yoshi parçaları boyuta göre kapılar. Hiçbiri kullanıcı talimatlarını ya da hata yollarını budamaz.

[aiskill.market](https://aiskill.market/blog/context-gc-fast-jev-compaction-winnow) üzerindeki compaction denemesi başarısızlık modunu özetler: yazılı bir hakim hiç orada olmayanı uyduramaz ama alakayı yanlış değerlendirebilir. Fast-jev README'si tekrarlar: asistan aracı yeniden çalıştırabilir. Winnow önbellek anahtarıyla `winnow_recall` sunar. Güvenlik ağı geri getirimdir, yanılmazlık değil.

Budama, özetleme değildir. Özetleme bir LLM'den bağlamı daha az tokene yeniden yazmasını ister; orijinal kelimeler kaybolur. Budama bir hakimden hangi parçaların önemli olduğunu sorar, sonra geri kalanını siler. Kalan metin aynen, sırayla durur. Risk yeniden yazma hatalarından (uydurulmuş yollar, birleştirilmiş talimatlar) seçim hatalarına (üç tur sonra önemli çıkacak bir parçayı düşürmek) kayar.

TypeSafe [Jev'i System One olarak tanıttı](https://typesafe.ai/blog/introducing-system-one-models-and-jev), üretim eşiğinin altındaki kararlar için. Context compaction böyle bir karardır: buda ya da tut, yeniden yazma değil. Model şekli kasıtlıdır. Yukarıdaki araçlar bu şekli paylaşır. Fast-jev, Winnow ve Yoshi hepsi Jev'e (ya da eş System One modele) yazılı evet/hayır soruları sorar, sonra puana göre hareket eder. Ne zaman sordukları (çağrı başına, blok başına, istek başına), atlamaları nerede gizledikleri (tarihten sil, geri çağırma anahtarıyla stub, proxy yükünden atla) ve nasıl kurtardıklarında (yeniden çalıştır, açık geri çağırma, henüz yok) farklılık gösterirler.

[TypeSafe Jev hub'ı](https://www.oguzhan.co/tr/typesafe-jev-system-one-karar-modeli/) manifesto ve Doom/Wikirace demolarını kapsar. [Dördüncü gün guardrail'leri kapsadı](https://www.oguzhan.co/tr/jev-ajan-guardrail-sema-gecerli-guvenli-degil/): is-malicious, jev-guard, Canny, wakegate. Beşinci gün compaction: eskiyen çağrıları sil, kalanları aynen tut. Bir olasılık, atılan bağlamın güvenle unutulduğunun kanıtı değildir. Ama ajan aracı yeniden çalıştırabildiğinde ya da önbellek anahtarını geri çağırabildiğinde, yanılmanın maliyeti bir gidiş-dönüş yolculuğudur, uydurulmuş yanıt değil.
