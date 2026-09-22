---
title: "MCP yapay zeka ajan: araç bağlamadan önce pratik checklist"
slug: "mcp-yapay-zeka-ajan-pratik-checklist"
focus_keyphrase: "MCP yapay zeka ajan"
yoast_title: "MCP yapay zeka ajan: araç ve governance checklist"
yoast_metadesc: "Model Context Protocol ajanlara ne katar, eylülde kurumsal governance nereye oturdu, Plugin4Shell pinning riski ve araç bağlamadan önce masa checklist’i."
excerpt: "MCP araç otobüsü olmanın ötesine geçti; kurumlar ajan sınırını protokol katmanında koyuyor. Araç bağlamadan önce masa checklist’i."
lang: tr
---

Bir ajana hava durumunu sormakla şirket deposunda kod çalıştırma yetkisi vermek arasında epey mesafe var. Şemalarda bu mesafe pek görünmüyor. MCP yapay zeka ajan dünyasında model ile aracı birbirine bağlayan düzenli bir hat sunuyor; asıl dert, hattın öbür ucunda kimin kimliğiyle neyin çalıştığı. Eylül ayında peş peşe gelen üç kurumsal ürün, Microsoft'un distributed skills deneyi ve Plugin4Shell açığı bu derdi aynı masaya koydu. Elimizde artık iyi bir kontrol listesi çıkaracak kadar somut malzeme var.

## MCP yapay zeka ajan trafiğinde kapı nerede duruyor?

Önce haftanın dikkat çekici tarafı. [Forkast'ın 17 Eylül tarihli dökümünde](https://forkast.news/mcp-is-becoming-the-governance-surface-three-enterprise-vendors-shipped-policy-enforcement-through-the-protocol-this-week/) ServiceNow, Rubrik ve Microsoft'un aynı hafta MCP hattına yerleştirdiği güvenlik kontrolleri yan yana geliyor.

ServiceNow AI Gateway v3.4, 10 Eylül'de MCP runtime enforcement ve server lifecycle özellikleriyle çıktı. Gateway katmanında hangi ajanın hangi MCP server, tool ve resource'a ulaşacağı belirlenebiliyor.

Yaklaşık 15 Eylül'de duyurulan Rubrik MCP, Anthropic ile birlikte geliştirildi. Forkast'ın aktardığına göre OWASP MCP Top 10 ile uyumlu guardrail'ler kullanıyor, her tool çağrısına kapsamı dar ve kısa ömürlü token veriyor. Rubrik Agent Identity, Okta ya da Entra ile federasyon kuruyor. Ajanın RBAC sınırı da insan kullanıcınınkiyle aynı tutuluyor.

Microsoft ise 17 Eylül'de Global Secure Access içindeki Entra Agent ID MCP Firewall'u duyurdu. Ürün MCP server'larını keşfediyor, bilinmeyenleri engelliyor ve method düzeyinde politika uyguluyor. Buradaki keşif işi küçük bir ayrıntı sayılmaz. Güvenlik ekibinin varlığından haberdar olmadığı “shadow MCP” bağlantısını hiçbir allowlist yönetemez.

Forkast, Okta'nın 2026 araştırmasına dayanarak çalışanların yüzde 67'sinin onaysız AI araçları kullandığını, yöneticilerin yüzde 92'sinin de otonom ajanların yaygın kullanımda olduğunu söylediğini aktarıyor. Elimizde araştırmanın metodolojisi yok. Bu nedenle yüzdeleri kesin risk hesabı gibi okumamak gerek. Ürünlerdeki yön ise açık: ServiceNow erişilecek alanı sınırlıyor, Rubrik kimlik ile token'ı daraltıyor, Entra kayıt dışı yolu arıyor.

Aynı haber Cisco Agent Runtime SDK'yı build-time tarafında, NVIDIA OpenShell ile WSO2 Agent Manager'ı runtime tarafında anıyor. Ayrıntısını kaynakta olmayan özelliklerle süslemeye gerek yok. Operasyon ekibinin önündeki ödev zaten yeterince dolu.

## Protokol ne yapar, hangi yükü taşımaz?

Model Context Protocol, araçları ve kaynakları AI uygulamasına JSON-RPC üzerinden açmak için ortak bir yol. Anthropic çıkışlı. [CNCF değerlendirmesini aktaran Forkast yazısına göre](https://forkast.news/cncf-evaluates-mcp-as-the-cloud-native-agent-wire-spec-and-the-standardization-arc-just-reached-infrastructure/) Linux Foundation bünyesindeki Agentic AI Foundation altında barındırılıyor; JSON-RPC 2.0, HTTPS ya da streamable HTTP kullanıyor. CNCF Technical Oversight Committee, MCP'yi Kubernetes üstündeki dağıtık ajan sistemleri için wire spec adayı olarak değerlendiriyor. Süreç devam ediyor. Taç takılmış değil.

MCP, tool'un nasıl tarif edilip çağrılacağını düzenli hale getiriyor. `delete_repository` yetkisinin kimde olacağına, token'ın ne kadar yaşayacağına ya da indirilen plugin kodunun onaylanan commit ile eşleşip eşleşmediğine kendi başına karar vermiyor.

Bu ayrımın günlük karşılığı basit: iyi yazılmış bir tool şeması tehlikeli komutu bulmayı kolaylaştırabilir. Güvenli hale getiremez.

## Uzman ajan yerine SKILL.md ve tool çağrısı

Microsoft Agent Framework ekibinden Tommaso Stocchi, 16 Eylül'de [specialist agent'lardan MCP üstünden dağıtılan skills yapısına geçişi](https://devblogs.microsoft.com/agent-framework/from-specialist-agents-to-distributed-skills-over-mcp/) anlattı. Model şu: uzman servis açıklamasını, `SKILL.md` dosyasını ve typed MCP tool'larını yayımlıyor. Parent konumundaki advisor talimatları kendi model context'ine yüklüyor, araçları doğrudan çağırıyor.

Uzmanlık serviste kalıyor; reasoning advisor'a dönüyor. Böylece her uzman için ayrı model loop açılmıyor.

Örnekte advisor önce `load_skill(weather)` ve `load_skill(lift-traffic)` çalıştırıyor, ardından ilgili MCP tool'larına gidip nihai yanıtı kendi üretiyor. Microsoft Agent Framework tarafında bunun parçaları `SkillsProvider`, `MCPSkillsSource` ve `SkillToolsMiddleware`.

Deneyde sorulan ifade aynen şöyle: “considering weather and waiting time, where should i start?” Üç eşleşmenin tablosu da şu:

| Eşleşme | A2A model çağrısı | A2A süre | Native MCP skills çağrısı | Native MCP skills süre |
|---|---:|---:|---:|---:|
| 1 | 6 | 16,416 sn | 3 | 8,661 sn |
| 2 | 6 | 12,835 sn | 3 | 5,866 sn |
| 3 | 7 | 17,188 sn | 3 | 4,517 sn |
| Ortalama | | 15,480 sn | | 6,348 sn |

Tabloya bakıp “latency yarıya indi” demek cazip. Fakat bu sonuç o cümleyi taşımaz.

Stocchi'nin üç çiftten oluşan gösterimi `gpt41` ile yapılmış, process'ler yeniden kullanılmış ve cache sonucu etkilemiş. Credential hazırlığı, dil runtime'ı, cache ve iki yolun yaptığı iş miktarı birbirinden ayrıştırılmamış. Kontrollü bir çalışma ya da faturaya yansıyacak dolar karşılaştırması değil.

Token hesabı da başka yöne gidiyor. Üç çalışmanın toplamında skills yolu 13.533, A2A yolu 11.134 token tüketmiş. Skills tarafı yaklaşık yüzde 22 daha yüksek. Daha az model çağrısı otomatik olarak daha az token demek değilmiş. Notlarımızda bulunsun.

Bir sürüm dipnotu daha var. Demo, SEP-2640'ın `skill://index.json` kullanan sabitlenmiş eski taslağını izliyor. Yazarın 10 Eylül kontrolünde yeni `skills/list` ve `skills/get` method'ları hâlâ netleşmemişti. Bu yapı draft bir extension hattı; evrensel MCP core özelliği muamelesi görmemeli.

Yine de model sınırlarının azalması incelenmeye değer. Kendi sisteminizde model ve tool çağrılarını, latency'yi, token'ı, initialization masrafını, retry'ları aynı cache ve process koşullarında ölçmeden kapasite kararı vermeyin.

## Plugin4Shell: SHA diye yazılan şey branch çıkarsa

Plugin4Shell hikâyesi güvenlik ekiplerinin sevmediği türden: ekranda pin var, çalışma dizininde başka kod.

[The Hacker News'in Air Security araştırmasına dayanan haberine göre](https://thehackernews.com/2026/09/plugin4shell-lets-repository-owners.html) bazı coding agent'lar plugin'i commit SHA ile pinliyor fakat ortaya çıkan working tree'nin o commit ile eşleştiğini doğrulamıyor. Commit hash görünümünde branch adına izin veren host'larda depo sahibi böyle bir branch oluşturup onu farklı koda yöneltebiliyor.

Bitbucket ve self-hosted Git sunucuları bu ada izin verebilir. GitHub, hash biçimli branch ve tag adlarını engelliyor; GitHub üstündeki senaryonun alanı bu yüzden daha dar. Gemini CLI varyantında `FETCH_HEAD` branch adı devreye giriyor. Plugin, kullanıcının yetkileriyle çalışıyor.

GitHub'da barınan built-in marketplace'ler varsayılan olarak auto-update alıyor. Haberde tarif edilen risk, GitHub dışındaki plugin host'ları için devam ediyor. Pinning kaydı tek başına kanıt sayılmamalı; checkout edilen nesne ayrıca doğrulanmalı.

18 Eylül itibarıyla tablo şöyleydi:

| Coding agent | Plugin4Shell durumu |
|---|---|
| Claude Code | Air Security'ye göre 2.1.179 ve üstünde düzeltildi; Anthropic release notes bunu anmayabilir |
| Codex | 0.146.0 sürümünde düzeltildi; OpenAI PR'ı Git'in SHA'yı branch adı gibi yorumlamasını tarif ediyor |
| GitHub Copilot | The Hacker News yazısı yayımlandığında fix yok |
| Gemini CLI | Fix gelmeyecek; Google Antigravity'yi işaret ediyor, consumer CLI haziranda durdu, enterprise CLI devam edebilir |

Air Security açığı Mayıs 2026'da buldu, haziranda bildirdi. Araştırma 17-18 Eylül civarında yayımlandı. The Hacker News, 18 Eylül kontrolünde CVE ya da vendor advisory bulamadı; gerçek saldırıda kullanıldığına dair bilinen örnek de yoktu. CVE bulunmaması riski silmez. Öte yandan proof of concept'i yaşanmış saldırı diye sunmak da habere bir şeyler eklemek olur.

## Ajanı araca bağlamadan önce masa checklist'i

Üretim ortamına giden kabloyu takmadan önce şu soruların yazılı cevabı olmalı:

1. **Tüm hattı çıkarın.** MCP server, sahibi, transport, tool ve resource listesini tutun. Kayıt dışı server keşfini açın; bilinmeyen endpoint'i engelleyin.
2. **İzni tool ve method düzeyine indirin.** Aynı server içindeki okuma ile silme işlemini tek onaya bağlamayın.
3. **Ajana ayrı kimlik verin.** Ortak insan hesabının arkasına saklamayın. Yapacağı işe uygun RBAC sınırını uygulayın.
4. **Token'ı çağrıya göre daraltın.** Seçili tool ve işlem için kısa ömürlü credential üretin. İş bitince yetki de bitsin.
5. **Pinleyin, ardından doğrulayın.** Uygun yerlerde Claude Code'u 2.1.179+, Codex'i 0.146.0+ sürümüne çıkarın. Git'in çözdüğü nesne ile working tree'nin beklenen commit'e ait olduğunu kontrol edin. GitHub dışı host'ları ayrı ele alın.
6. **Reddetme yolunu deneyin.** Bilinmeyen server, yasak method ve süresi dolmuş token ile test yapın. Ajanın başka yol aramadan durduğunu görün.
7. **Kararı kayda alın.** Log'da ajan kimliği, server, method, token scope, politika sonucu ve gerçekten çalışan kod revizyonu bulunsun.
8. **İşin tamamını ölçün.** Model çağrısı, tool çağrısı, latency, token, initialization ve retry değerlerini birlikte toplayın. Distributed skills deniyorsanız nested-agent sürümüyle eş koşullarda karşılaştırın.
9. **Güncellemenin sahibini belirleyin.** Plugin marketplace ve MCP server değişir. Yeni sürümü, advisory'yi ve permission drift'i kimin inceleyeceği belli olsun.

Konunun geniş çerçevesi için [yapay zeka merkezine](https://www.oguzhan.co/tr/yapay-zeka/) bakabilirsiniz. Tool politikası process isolation ihtiyacını ortadan kaldırmıyor; yakın tarihli [AI ajan sandbox gündemi](https://www.oguzhan.co/tr/ai-gundemi-20-eylul-2026-ai-ajan-sandbox/) bu tarafı tamamlıyor. Davranış belirlenen sınırı aştığında kimin neyi bildireceği ise [misalignment operatör çerçevesinde](https://www.oguzhan.co/tr/openai-misalignment-bildirim-cercevesi-operator/) ayrı bir operasyon konusu.

Temiz allowlist, onaylı tool'a kötü argüman gönderilmesini önleyemez. Geçerli kimliğe fazla yetki tanımlanabilir. Doğrulanmış plugin kasıtlı zararlı kod içerebilir. Kısa ömürlü token da yaşadığı her saniye boyunca gerçek bir yetkidir.

MCP'nin kıymeti bütün bunları görünür bir kavşakta toplaması. O noktaya keşif, kimlik kontrolü, method politikası ve audit kaydı koyabiliyoruz. Fakat etiketlere güvenip altındaki nesneyi doğrulamazsak “SHA pinned” yazısı güvenlik kontrolünden çok masa süsüne dönüşür.
