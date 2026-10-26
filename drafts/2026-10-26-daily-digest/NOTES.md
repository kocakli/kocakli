# Notlar

## Kelime sayıları

Sayım, ön yazı kapanışındaki ikinci `---` çizgisinden sonraki gövdededir. HTML yorumları çıkarılmıştır. Başlıklar, tablo, üç maddelik liste ve Kaynaklar satırları dahildir. Ön yazı dahil değildir. Ayırıcı boşluktur (`\S+`).

- EN: 1100
- TR: 911

EN aralığı 800-1100. TR aralığı 700-950. İkisi de aralığın içinde.

## İç bağlantılar

EN:

- Hikaye 1: https://www.oguzhan.co/claude-duet-proactive-agent-approvals-limits/
- Hikaye 3: https://www.oguzhan.co/deepseek-deepinfer-eagle-4-muse-glimmer/

TR:

- Hikaye 1: https://www.oguzhan.co/tr/claude-duet-proaktif-agent-onay-sinirlar/
- Hikaye 3: https://www.oguzhan.co/tr/deepseek-deepinfer-eagle-4-muse-glimmer-yerel-model/

25 Ekim haftalık özetinin bağlantısı kullanılmadı. O sayıda anlatılan konular yeniden özetlenmesin diye.

## Dış bağlantılar

Her hikayede birincil kaynak var. EN ve TR aynı URL'leri kullanır. Kaynaklar listesi madde işareti değildir. Tek madde listesi, hikaye 1'deki pin ve rotate adımlarıdır.

## Bilerek dışarıda bırakılanlar

Aynı olgular iki dilde de gövdeden çıktı. Aralık tutsun diye. Uydurma yok.

1. Oliver Jensen'in unvanı, Director of Security, 23 Ekim yazısında var. Gövde Jensen ve Mateo Wang'ı unvansız anıyor.
2. Sırları webhook.site'a basan CI kayıtları dakikalar içinde silinmiş. Gövde bunu söylemiyor.
3. 23 Ekim yazısı süreç değişikliklerini sonraki haftaya söz etmiş. Gövde bunu yazmıyor. 26 Ekim'de bunların yayımlandığı da doğrulanmadı.
4. "Önceki durum notlarında yanlış varsayım vardı" cümlesi genel haliyle yok. Düzeltmenin kendisi duruyor. 21 Ekim notu token'ları iç LiteLLM kurulumunun loglarına bağlamış. Kök neden yazısı bunu bırakıyor. İlk token Agent Platform API'sinden gelmiş. Claude Code adı geçmiyor.
5. "Adımların hiçbiri egzotik değildi" cümlesi yok. Kapanış, kendi token listesini henüz çıkarmadığını söylüyor.
6. Block'un "dili LLM'lere göre yüzlerce kat az sözcükten öğrendi" iddiası yok.
7. Ses klonlama ve dolandırıcılık, Block'un rakam vermediği uyarı olarak yok. Acı ve duygu alıntısı duruyor.
8. Nanbeige bağlam uzunluğu 524288 token. Tabloda brief'in hücresi var: 512K tokens. Deponun 24 Ekim'de açılıp 25 Ekim'de güncellenmesi de yalnızca tablodaki "24 to 25 Oct" hücresinde.
9. Becerilerin Nanbeige4.3-3B dahil küçüklere damıtılacağı yok. EN "flagship teacher" diyor. TR bunu "asıl öğretmen modeli" diye kuruyor. Ayrı bir ürün adı değil.
10. Terminal-Bench 2.1 rakiplerinin puanları gövdede yok. Brief'teki kart iddiaları: Qwen3.8-27B 73.0, Muse-Glimmer-30B 61.8, Gemma4-31B 47.2. 80.9 hem gövdede hem tabloda. Muse Glimmer, 22 Ekim özetine bağlanarak anılıyor.
11. DeepSWE 65.5, rakip Qwen3.8-27B 42.5. Yok.
12. Topluluk GGUF kuantları brief'te var, depo URL'si yok. Gövdeye alınmadı.
13. kanzhun.com iletişim adresi ve Kanzhun / BOSS Zhipin ekibi yok. Brief, yalnızca "Nanbeige team" demeye izin veriyor. Gövde onu kullanıyor.
14. Nemotron kartındaki şu ayrıntılar gövdede yok. Bir kısmı zaten tabloda (parametre, lisans, bağlam, yerel asistan, IFBench, tarih): 4GB Q4_K_M derlemesi NVIDIA-Nemotron-3.5-Bolt-E4B-4GB, DFlash drafter, conversational mode, runtime thinking budget, düşük bellek, düşük time-to-first-token, etkileşimli persona, gömülü arayüz.
15. İsveç'te Skatteverket ve Statens institutionsstyrelse (SiS) daha önce benzer engel koymuş. Kronofogden değerlendiriyor. Gövdeye alınmadı. Brief SiS için İngilizce açılım vermiyor. Açılım uydurulmadı.
16. Decrypt İngilizce haberi kullanılmadı. Gövdedeki kaynaklar SVT ve Sveriges Radio.
17. GDPval 84.8'in yanındaki 86.4 için brief model adını net vermiyor. Rakip adsız bırakıldı.
18. Qwen3.5 4B Tau2-Bench 75.06, Nemotron kartındaki kıyasa bağlandı. Brief'te bu sayı için ikinci bir URL yok.
19. Dessa klibi dinlenmedi. Sayfa okundu. Klip, sayfada bulunan bir kayıt olarak geçiyor.

## Belirsizlik

EN'de etkilenen kurulum cümlesi, bir önceki paragraftaki PyPI penceresine ve adlandırılmış Docker Hub etiketlerine geri dönüyor. Ayrı satırda 11:46 başlangıcını tekrarlamıyor. TR aynı pencereleri açık yazıyor: pip 11:39 ile 13:23 UTC, Docker etiketleri 11:46 ile 14:20 UTC.
