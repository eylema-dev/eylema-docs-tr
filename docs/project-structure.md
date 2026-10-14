# Proje yapısı ve kabul edilen ilk ürün kararları

Sürüm **0.5.0**, 13 Ekim 2026. [İngilizce kaynak](https://github.com/eyleme-dev/eylema-docs-en/blob/main/docs/project-structure.md).

Bakımcı 12 Ekim 2026 tarihinde 1, 2, 4, 5, 6 ve 8 numaralı önerileri kabul etti, aşağıdaki üç cihazlık envanteri bildirdi ve Apache-2.0 seçti. Bu kararlar güncel ürün yönünü günceller. Tarihsel Goal kayıtlarını yeniden yazmaz; kalan runtime, model veya donanım kabulünün geçtiğini iddia etmez.

## İlk kullanıcı ve ürün sonucu

Bakımcının 13 Ekim 2026 açıklaması Eyleme’yi agentic çerçeveyi oluşturan platform olarak tanımlar: kullanıcılar işbirlikli geri besleme döngülerini kurar, uyumlu yerel modelleri atayıp değiştirir, kararları inceler ve izinli eğitim verisini toplar. Sabit rol/davranış sözleşmeleri belirli model ailelerinden uzun ömürlüdür. MiniCPM, Qwen ve yerel karar politikaları bu çerçevedeki katılımcılardır; ürünün sabit kimliği değildir. [Mimari revizyonu](architecture.md#işbirlikli-agentic-döngü-ve-sabit-platform-sözleşmeleri) döngüyü, değiştirme yaşam döngüsünü, kanıt ve veri kümesi sınırlarını tanımlar; bütünleşmeleri uygulanıp kabul edilene kadar öneridir.

Platformun kullanıcı akışı: döngü ile eylem/gözlem sözleşmelerini tanımla → rolleri bağla → kabul edilmiş model atamalarını ve toplama politikasını seç → çalıştır/incele/durdur → bölümleri düzelt ve kürasyondan geçir → aday modeli karşılaştır → uyumlu atamayı güvenli sınırda etkinleştir. Konsol döngü, model, bölüm ve veri kümesi sürümlerini göstermelidir. Yerleştirme uygulaması ile belge-kanıt inceleme uygulaması, platform her modele göre yeniden yazılmadan, aynı platform sözleşmeleriyle farklı döngü tanımları olarak ifade edilebilmelidir. Aşağıdaki deterministik konsol ilk teslim edilen temel olarak kalır; ürün amacının sınırı değildir.

İlk kullanıcı, yerel bir eylemci uygulaması geliştiren yazılımcıdır. İlk teslimat tek kullanıcılı görev konsoludur: görev oluşturma, sınırlı deterministik adımları yürütme, ilerleme/sonuç inceleme, yetkili kalan işi durdurma, hizmeti yeniden başlatma ve aynı kalıcı görevi açma. İlk adımlar yalnız uygulamanın kendi görev durumunu değiştirir. Uzak yönetim, birden fazla tenant ve keyfî dosya sistemi/süreç/ağ eylemleri ilk ürünün dışındadır.

Kullanılabilir görev konsolu önizlemesi GPU, model veya eğitimi beklemeden M2'de değerlendirilir. Kabul edilmiş çekirdek/örnek temelinden sonra ve isteğe bağlı öğrenme çalışmasından önce küçük bir gerçek ihtiyaçtan PR'a kanıt gelir. Tam otonom geliştirme/sağlayıcı kabulü ve bütün deneysel sürüm ayrı M7/G44/G45 kapılarını korur. Küçük 3B yerleştirme ortamı, sonraki yeteneklerin referans uygulamasıdır; ilk kullanıcının görev konsolu için ön koşul değildir.

Çekirdekte Rust görev/runtime/journal/host/web bileşenleri ve CLI zaten vardır. [Güncel çekirdek durumuna](https://github.com/eyleme-dev/eyleme/blob/main/README.tr.md) ve revizyona bağlı kanıtlarına bakın. Gerçek kişi doğrulaması açık sınırlama olarak kalır: varsayılan insan olmayan oturumun FORBIDDEN alması, insan yetkisiyle etkili durdurma senaryosunu kanıtlamaz. Bu karar F3'ü kaldırmaz veya kontrolünün zayıflatılmasına izin vermez.

Kabul edilen harness revizyonu dokuz rol sözleşmesini, ayrı STT/TTS/görüntü profillerini, alan model havuzlarını, projeye özel/açık ekosistem sınırlarını ve kendi Rust RAG hattımızı ekler. [Rol tablosu ve örnekler](architecture.md#rust-harness-model-rolleri-ve-alana-göre-seçim) ile [güncel aksiyon planına](https://github.com/eyleme-dev/devguide/blob/main/docs/tr/platform-action-plan.md) bakın. İlk uygulama parçası yeniden kullanılabilir döngü/rol kaydıdır; native inference, araç yürütme ve tam iş kabulü ayrı kartlarını korur.

## Dil, sahiplik ve bileşen sınırları

İngilizce kanonik, Türkçe eşzamanlı karşılığıdır. Kod, kimlikler, şablonlar ve görev kayıtları İngilizce kalır. [Depo haritası](https://github.com/eyleme-dev/devguide/blob/main/docs/tr/repository-map.md) depo sınırlarını tanımlar. Ürün sözleşmeleri dil depolarında, ortak katkı politikası devguide'da, uygulama/şemalar çekirdekte kalır.

Tek, bize ait Rust çalışma alanı ve tek yerel native host süreci kullanılır. Modül/crate ancak test edilmiş sınır ve gerçek tüketici için eklenir.

| Bileşen | Sorumluluk |
|---|---|
| `crates/eylema-contracts` | Kanonik Rust alan tipleri, sürümlü geçişler, sınırlı EYL iletim kayıtları ve onay içeriği üretimi |
| `crates/eylema-runtime` | Kapsamlı kabul, deterministik adımlar, yetki, bütçeler, gözlemler ve etkili iptal |
| `crates/eylema-journal` | Sınırlı EYLJ ekleme/yeniden oynatma, açık kalıcılık ve bozulma hataları |
| `crates/eylema-platform` | Dar standart host kripto/entropi/senkronizasyon ve native GPU bağları |
| `crates/eylema-host` | Runtime/journal bileşimi, dayanıklı kurtarma ve yerel hizmet sınırı |
| `crates/eylema-web` | Yerel tarayıcı arayüzü ve sınırlı sunum/taşıma adaptörleri |
| `apps/eylema` | Native CLI/hizmet bileşimi ve yapılandırma |
| `eylema-examples/task-console` | Çekirdek revizyonuna sabit dış tüketici; runtime kodunun kopyası yok |

Bağımlılıklar sözleşmelere yönelir. Yürütme, yetki ve kalıcılık host'a aittir. Tarayıcı durumu sunar ve tanımlı GPU yeteneklerini kullanır; günlüğü doğrudan değiştiremez veya native yetki veremez. Tarayıcının kapanması native işi durdurmaz; yeniden açılış snapshot/olayları okur. Rust 1.99.0 ve aarch64-apple-darwin native temel olarak kalır; seçili taşınabilir kütüphaneler wasm32-unknown-unknown'a derlenir. Derleme ve gerçek hedef yürütümü ayrı kanıttır.

## Erişilebilir test envanteri

Bu takma adlar bakımcının mevcut cihazlarını kaydeder; kabul edilmiş runtime HardwareProfile kimlikleri değildir. Ölçülen her HardwareProfile ve WorkloadProfiles için kesin OS, CPU/GPU, SDK/sürücü/tarayıcı sürümleri, iş yükü hash'leri ve kod revizyonu kaydedilir. İki iş yükü olan tek cihaz yine tek fiziksel cihazdır.

| Envanter adı | Sahibinin bildirdiği donanım | İlk rol | Kanıt sınırı |
|---|---|---|---|
| `mbp-m4-pro-24` | MacBook Pro, Apple M4 Pro, 24 GB birleşik bellek | Birincil yerel görev konsolu kabulü; sonra CPU/Metal ve tarayıcı WebGPU ölçümleri | Mevcut çekirdek kanıtı bu cihazla sınırlıdır; bu karar değişikliği donanım kabulünü yeniden çalıştırmaz |
| `mini-m4-24` | Mac mini, Apple M4, 24 GB birleşik bellek | İkinci fiziksel Mac uyumluluğu ve kaynak karşılaştırması | Bu cihazdaki OS/araç/tarayıcı ve bütün Eyleme yürütümleri: not_run |
| `rtx4070ti-super-16-32` | NVIDIA RTX 4070 Ti Super, 16 GB VRAM, 32 GB sistem RAM'i | Sonraki ayrık GPU karşılaştırması ve eğitim fizibilitesi | Linux sahibi tarafından doğrulandı; CPU/dağıtım/kernel doğrulanmadı; sürücü/backend/erişim ve bütün Eyleme yürütümleri: not_run |

İki ek makine birincil görev konsolu önizlemesini engellemez. Kabulleri ayrı sınırlı görevdir; envanter satırı Linux/Windows backend'i etkinleştirmez, uzak erişim, kurulum veya eğitim yetkisi vermez. Apple birleşik belleği ile RTX ayrık VRAM/sistem RAM'i ayrı kaydedilir; birbirinin yerine geçen uydurma ortak bütçeye toplanmaz.

Önce aynı sürümlü deterministik görev sabit girdilerle ölçülür: soğuk/sıcak başlangıç, görev gecikmesi p95/p99, tepe bellek ve başarılı/hatalı eylem sayısı. GPU işlerinde referans çıktı toleransı, kare süresi dağılımı ve birleşik iş yükü belleği eklenir. Sayısal kalite/kaynak eşikleri başlangıç ölçümünden sonra ve aday karşılaştırmasından önce sabitlenir. Erişilemeyen gözlemler unknown/not_run kalır.

## Kesinleştirilen görev, depolama ve API kararları

| Konu | Kabul edilen ilk uygulama sözleşmesi |
|---|---|
| Anlamın kaynağı | eylema-contracts içindeki bize ait Rust tipleri ve kurucular; HTTP/CLI/tarayıcı adaptörleri aynı anlamı kullanır. OpenAPI/JSON Schema/MCP üretimi sonraki iştir; üretilmiş destek iddiasından önce uyum örnekleri gerekir |
| Durum ve yetki | Görev/yürütme kimlikleri ayrı; eski revizyon ve yetkisiz etkiler reddedilir; başarı, hata, etkili iptal ve belirsiz sonuç ayrıdır |
| Kanonik onay | Mevcut EYL codec v1 ve canonical_approval_payload tipli görev/öneri/eylem alanlarını bağlar; standart host SHA-256 bu baytları özetler. Map/set sırası deterministiktir; taşıma istek/korelasyon kimlikleri dışarıdadır; örtük metin normalleştirme veya float kodlama yoktur |
| Kalıcılık | Host'un sahip olduğu yerel dizinde mevcut EYLJ v1 journal, intent/commit kayıtları ve dayanıklı alındı; bozuk/yarım/uyumsuz girdi sessiz tamir veya migration olmadan reddedilir |
| Tekrar saklama | Tutulan kabul anahtarları/sonuçlar doğrulanmış journal replay sonrasında korunur; otomatik silme, döndürme veya süre aşımı eklenmez. Sınırlı kapasite dolunca yinelenmiş iş kabul etmek yerine açık hata verilir |
| Yeniden başlatma | Doğrulanmış kimlik/sonuç/etkiler korunur. Bitmemiş yürütme OutcomeUnknown olur; eski oturumlar emekliye ayrılır, yeni güvenilir kayıt gerekir. Belirsiz dış etkiler sessizce tekrarlanmaz |
| Uyumluluk | Mevcut runtime 0.1.0, EYL v1 ve EYLJ v1 değişmez. Gelecekteki uyumsuz değişiklikler yeni sürüm ve açık migration/ret testleri gerektirir |

Uygulama ayrıntıları ve çalıştırılmış kapsam: [tipli sözleşmeler](https://github.com/eyleme-dev/eyleme/blob/main/docs/tr/typed-contracts.md), [kanonik codec/platform](https://github.com/eyleme-dev/eyleme/blob/main/docs/tr/codec-platform.md), [journal](https://github.com/eyleme-dev/eyleme/blob/main/docs/tr/local-journal.md), [kurtarma](https://github.com/eyleme-dev/eyleme/blob/main/docs/tr/runtime-recovery.md). Geniş [API kataloğu](api-reference.md) önerilen işlemler içerir; bu karar her rotanın uygulandığını ilan etmez.

## Yerel yetki ve açık platform bağımlılıkları

İlk hizmet tek kullanıcılıdır ve yalnız loopback üzerinde çalışır. Kapsamlı oturumlar, Host/Origin ve CSRF kontrolleri, sınırlı istekler ve host tarafından doğrulanmış özne/onay kayıtları zorunludur. Model veya iddia edilen insan alanı yetki oluşturamaz. Zaten yetkilendirilmiş rutin eylemler tekrar onay istemez; belirlenmiş kontrol noktaları, yönetişim ve durdurma izinleri uygulanmaya devam eder. Public/LAN erişimi, uzak kimlik ve TLS sonlandırma ayrı kabul edilmiş tasarım ister; yerel prototip uzak/TLS desteği iddia etmez.

Sıfır üçüncü taraf üretim Cargo paketi politikası değişmez. macOS CommonCrypto/Security/libSystem standart hash, entropi ve senkronizasyon hizmetlerini dar, incelenmiş bağlarla sağlar; kendi kodumuz kriptografi uygulamaz. Metal/SDK bağları ve Metal shader kaynakları, asgari tarayıcı host JavaScript'i, WebAssembly/WebCrypto, WebGPU ve WGSL açık platform girdileridir. Native Metal ile tarayıcı WebGPU ayrı cihaz bağlamlarıdır; ortak GPU buffer veya evrensel zero-copy garantisi yoktur. Python/Unsloth ve paketleme dönüştürücüleri ayrı sabitlenmiş geliştirme/eğitim envanterlerinde kalır.

## İlk tarayıcı gösteriminin kabul koşulları

| ID | Senaryo | Gereken kanıt | Yol haritası |
|---|---|---|---|
| F1 | Geçerli görev oluştur ve incele | Kalıcı görev kimliği, kapsam, bütçe ve revizyon; geçersiz girdi reddi | M1–M2 / EYL-004, EYL-006 |
| F2 | Yetkili deterministik görevi çalıştır | Kayıtlı yürütme, sıralı ilerleme ve sonuç; reddedilen eylemin yetkisiz etkisi yok | M1–M2 / EYL-004 |
| F3 | İş sürerken yürütmeyi durdur | İsteğin alınması ile etkili durma ayrı; kalan adımlar durur; tamamlanan etkiler görünür; geç durdurma tamamlanmış sonucu korur | M1–M2 / EYL-004, EYL-006 |
| F4 | Yeniden başlat ve kayıtlı durumu aç | Aynı görev/yürütme kimlikleri, revizyonlar, sonuçlar ve olaylar; sürmekte olan işin kurtarma politikası denenir | M2 / EYL-005, EYL-006 |
| F5 | İsteği tekrarla veya eski revizyon gönder | Aynı tekrar özgün referansı döndürür; farklı içerik ve eski revizyon açıkça reddedilir | M1–M2 / EYL-004, EYL-005 |
| F6 | Yazmayı kes veya uyumsuz kayıtla karşılaş | Tanımlı kurtarma ya da açık hata; uydurma tamamlanma ve sessiz veri kaybı yok | M2 / EYL-005 |
| F7 | Limit aş veya erişilemeyen yetenekle karşılaş | Sınırlı girdi/kuyruk/iş, açık hatalar ve süre dolduktan sonra doğru sonuç bildirimi | M1–M2 / EYL-003, EYL-004, EYL-006 |

F1–F7 birincil cihazda aynı aday revizyonunda gösterilmeli; gerçek kişi doğrulaması güvenilir host test örneklerinden ayrılmalıdır. İptal alındısı etkili durma, süre sınırı da fiziksel sonlanma değildir. İlk üründe dış görev etkisi yoktur; olumsuz örnekler yine kısmi/belirsiz sonuçları doğru korur. Bu kapsam kararı hiçbir kontrolü kaldırmaz.

## Lisans ve ilk öğrenme deneyi

Kendi kaynak kodumuz ve belgelerimiz bakımcının seçtiği Apache-2.0 lisansını kullanır. [Lisans ve katkı kapsamına](https://github.com/eyleme-dev/devguide/blob/main/docs/tr/licensing.md) bakın. Üçüncü taraf model/veri koşulları bağımsızdır.

Mevcut Qwen3-0.6B seçimi aday olarak kalır; yürütüm/destek iddiası değildir. Model kabulünden önce kesin işleç/varlıkları sabitleyin ve seçilen donanımda deterministik başlangıcı ölçün. İlk öğrenme deneyini tek izinli görev, insan düzeltmesi, sabitlenmiş tarif ve sonlu bütçe içinde bağımsız ayrılmış değerlendirmeyle sınırlayın. [Öğrenme protokolü](learning-and-training.md) toplama/eğitimden önce izin, saklama ve kaynak kararlarını gerektirir. Bu kararların yayımlanması yeni veri toplamayı veya eğitim çalıştırmayı yetkilendirmez.

Güncel harness revizyonu modele özel native Rust LoRA/QLoRA iyileştirmesini, router/skill sözleşmelerini ve kalibre kapasite/yatırım planlamasını G74–G86'ya bağlar. Projeye özel türevler özel kalır; isteğe bağlı harici büyük modeller açık açıklama/çağrı yetkisi gerektirir. İlk yerel metin/RAG kanıtı G72 isteğe bağlı modalitelerden önce ilerler; gerçek insan kaydı/durdurma G73'tedir.
