---
title: "Jev ajan guardrail'leri: şema geçerli olmak güvenli demek değil"
slug: jev-ajan-guardrail-sema-gecerli-guvenli-degil
yoast_title: "Jev guardrail: ajanlarda şema geçerli ≠ güvenli | oguzhan.co"
yoast_metadesc: "Kod ajanlarında tool gate, kanıt kaydı, uyanma kontrolü ve çalıştırma öncesi tarama. Jev karar önerir; izni host verir."
focus_keyphrase: Jev guardrail
lang: tr
word_count_target: 800-1200
---

Jev guardrail kullanmanın asıl sebebi, ajanın kurallara uygun biçimde araç çağırmasının doğru ya da güvenli davrandığı anlamına gelmemesi. Jev, türü belli sorulara kalibre edilmiş olasılıklar döndürüyor. İzin verme, kullanıcıya sorma, reddetme ve yan etkileri uygulama işi ise host kodunda, izin ekranında ve işletim sistemi sandbox'ında kalıyor.

Bu ayrım, [awesome-jev](https://github.com/cobanov/awesome-jev) listesinin Agents bölümünü ve projelerin README dosyalarını okurken karşıma tekrar tekrar çıktı. Listenin uyarısı gayet açık: “Bir model yargısı güvenliği tesis etmez, host uygulamasının izin kontrollerinin yerini de tutmaz.” Otomatik çalışan ajanlar için bundan daha sağlıklı bir başlangıç cümlesi zor bulunur.

## 🛡️ Jev guardrail için doğru sıra

Önce kodun kesin olarak denetleyebildiği şeylere bakmak gerekiyor. Yoruma açık kısım kalırsa Jev devreye giriyor. Gelen olasılığı gerçek bir karara çeviren taraf yine host politikası.

[OpenRouter'ın iade örneği](https://openrouter.ai/docs/cookbook/building-agents/gate-tool-calls-with-jev) bu sırayı kuru bir şema olmaktan çıkarıyor. Sistem önce siparişin destek kaydındaki müşteriye ait olup olmadığını ve iade tutarının kalan bakiyeyi aşıp aşmadığını normal kodla kontrol ediyor. Bakiye aşılmışsa Jev'e soru dahi gitmiyor.

Bu kontrollerden geçen talep için üç Noul sorusu var: Müşteri iadeyi istedi mi, doğru sipariş mi seçildi, şirket politikası bu durumu kapsıyor mu? Örnekte 0,9 ve üstü onay, 0,1 ve altı ret; aradaki bölge ise insan incelemesi demek.

Canlı örnekler de gündelik: Geç ulaşan kettle için kargo iadesi onaylanıyor. Başkasına ait espresso siparişi reddediliyor. Ezilmiş kutunun politikaya uyup uymadığı netleşmeyince talep incelemeye düşüyor. Bakiyeyi aşan tutarıysa daha ilk kod kontrolü durduruyor. Bu denemelerde Decisions çağrısı 0,0001 doların altında kalmış ve yaklaşık 600 ms'den kısa sürmüş. Kontrol kodu bozulursa sessizce onay vermek yerine hata fırlatıyor.

Özet sırası şu: kesin kontroller, türü belli olasılıklar, host kararı. Şemanın düzgün olması iadeyi doğru hale getirmiyor. Serinin temel çerçevesi [ana yazıda](https://www.oguzhan.co/tr/typesafe-jev-system-one-karar-modeli/); bugün önemli olan, modelin yetkisinin nerede bittiği.

## ⛔ jev-guard her araç çağrısının önüne geçiyor

[jev-guard](https://github.com/leepokai/jev-guard), aynı fikri kod ajanlarında auto-mode tarzı bir PreToolUse hook ile uyguluyor. Claude Code, Codex, Copilot CLI, Gemini CLI, Cursor, pi, OpenCode ve ACP listelenen ortamlar arasında.

Araç çalışmadan önce Jev, salt okumadan yıkıcı işleme uzanan 0 ile 3 arası bir `risk` Score üretiyor. Ayrıca oturumun bütününe bakarak `approval`, `user_requested` ve `from_untrusted` için Noul olasılıkları hesaplıyor.

Karar modeli değil, kod veriyor. Yaklaşık politikaya göre risk 2,5'e ya da güvenilmeyen kaynaktan gelme olasılığı 0,7'ye ulaşırsa çağrı reddediliyor. Risk 1,5 veya onay ihtiyacı 0,75 olduğunda kullanıcıya soruluyor. Eylemin kullanıcı tarafından istendiğine dair olasılık 0,85'i aşarsa “sor” kararı “izin ver”e dönebiliyor; fakat bir “ret” kararını kaldıramıyor.

Bu son kural önemli. Kullanıcının talebi delildir, bütün kapıları açan anahtar değil.

İşlemden sonra da kontrol bitmiyor. Araç çıktısında prompt injection ve canary işaretleri aranıyor, bulgu oturum boyunca hatırlanıyor. Skill, plugin ve talimat dosyalarındaki beklenmedik kötü niyetli içerik de denetlenebiliyor. Proje, tipik çağrı başına yaklaşık 1.000 token ve milyon input token için 0,042 dolarlık liste fiyatıyla 0,00004 dolar hesaplıyor. Taiwan'dan Gateway üzerinden kendi ölçümleri 580 ile 750 ms arasında. Bu, TypeSafe'in West Coast için verdiği 70 ile 500 ms değerinden ayrı bir ölçüm.

Bunların hiçbiri “bütün saldırıları durdurur” anlamına gelmiyor. jev-guard bir yargıyı açık eşiklerle politikaya bağlıyor. Uygulayan yine host.

## 📒 Canny, “bitti” sözüne kayıt soruyor

İzinli komut çalıştırmak, işin tamamlandığını göstermiyor. Ajan bütün araç çağrılarını kurala uygun yapıp ortada başarılı test yokken “tamamlandı” diyebilir.

[Canny](https://github.com/qkal/Canny), her oturum için eklemeli ve sonradan değiştirilmeyen bir evidence ledger tutuyor. Dosya düzenlendi mi, komut hangi exit code ile bitti, aynı hata tekrarlanıyor mu, yazılmayı bekleyen metin AWS anahtarına benzeyen bir parça içeriyor mu? Bunlar deterministic hook'ların kaydettiği olgular.

Jev'e ise kodun kolayca kesinleştiremeyeceği sorular kalıyor: Bu mesaj gerçekten işin bittiğini mi iddia ediyor, yapılan değişiklik proje kuralıyla çelişiyor mu?

Canny'deki ince ama değerli ayrım şu: Jev hiçbir zaman engelleyen taraf değil. “Bitti” mesajı reddedilmişse sebebi bir olasılık eşiği değil, ledger içinde başarılı kontrol bulunmaması. Jev kararsız kaldığında ya da API anahtarı olmadığında fail-open davranıyor. Oturum kaydı `canny replay` ile yeniden okunabiliyor; Claude Code ve Codex hook'ları `init` üzerinden kuruluyor.

Model iddiayı tanıyabilir. İddiayı haklı çıkaracak somut kayıt başka yerde durur.

## ⏰ Boş yere uyandırmayan kapı

Uzun süre çalışan bir ajanın her olayda tam model turuna dönmesi sessiz bir israf. Bazen değişen hiçbir şey yok.

[wakegate](https://github.com/shitianfang/wakegate), uyuyan ajan devam etmeden önce Jev'e tek soru soruyor: `waitingFor`, varsa yeni olay ya da gözlem ve atlanan tur sayısı düşünüldüğünde bu uyanış tam bir LLM turuna değer mi?

Kullanıcıdan gelen mesaj her zaman uyandırıyor. Hatalar da öyle. Varsayılan `maxSkips` değeri olan 10'a ulaşınca uyanma zorlanıyor; kapı fail-open çalışıyor. Workers, Durable Objects ve uzun çalışan Node ajanlarını hedefleyen proje kendi denemelerinde yaklaşık 250 ms bildiriyor. Uyku süresini seçmiyor, yalnızca gelen olayın dönüşe değip değmediğine bakıyor.

Yarınki Day 5 yazısının konusu context compaction. Şimdilik wakegate'in hatırlattığı yeterli: Bazen en ucuz model turu, hiç başlamayandır.

## 🦠 Tanımadığın kodu çalıştırmadan önce

Bir de yeni indirilen repo meselesi var. Setup komutunu çalıştırdıktan sonra kaynak ağacını incelemek için biraz geç kalmış olabiliriz.

[is-malicious](https://github.com/luantak/is-malicious), kaynak kodu, yapılandırmayı, build ve CI metinlerini çalıştırma öncesinde Jev ile tarayan bir CLI. Raporda dosya ve satır aralığı, kategori, olasılık, confidence ve gerekçe bulunuyor. GitHub Actions örnekleri aynı yaklaşımı pull request diff'lerine uyguluyor.

Fakat temiz rapor, güvenlik belgesi değil. Araç antivirüs değil; dependency CVE denetimi ya da secret scanner görevi de görmüyor. Telemetry bulgularını bilgi olarak gösteriyor, tek başına başarısız exit sebebi saymıyor. `TYPESAFE_API_KEY` istiyor ve ücretli input token kullanıyor.

Dolayısıyla tanımadığım bir ağacı çalıştırmadan önce bu taramadan geçiririm. Ardından şüpheli dosyalara yine bakar, izinleri kısıtlar ve belirsiz kodu sandbox içinde çalıştırırım. Bir model raporu bu tedbirleri iptal edemez.

## Sınırı bilmek sistemin parçası

Jev'in ucuz ve hızlı yargısı, ajan akışının daha çok noktasına kapı koymayı mümkün hale getiriyor: araçtan önce, araç sonucundan sonra, “bitti” demeden önce, uyanmadan önce ve yabancı kodu çalıştırmadan önce. [TypeSafe'in tanıtım yazısı](https://typesafe.ai/blog/introducing-system-one-models-and-jev) doğrulama, guardrail ve jailbreak tespitini System One kullanım alanları arasında sayıyor. Buradaki projeler, güvenlik politikasını modele teslim etmeden bunun nasıl uygulanabileceğini gösteriyor.

Kodun kesin bildiğini kod denetler. Belirsiz yerde Jev görüş verir. Kararı host uygular, arada kalan vakayı insan inceler, yan etkileri sandbox sınırlar.

Bu yaklaşım [Day 3'teki hız ve maliyet yazısına](https://www.oguzhan.co/tr/jev-hiz-maliyet-paralel-ornekleyici/) da bağlanıyor. Ucuz yargı, sık kontrolü uygulanabilir kılıyor. Hatasız hale getirmiyor. Day 5'te kapı bu kez ajanın yanında taşıdığı context için kurulacak.
