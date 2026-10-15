# Eyleme ilk sürüm yol haritası

Sürüm **0.7.0**, 13 Ekim 2026. İngilizce kanoniktir; [English](https://github.com/eyleme-dev/eyleme-docs-en/blob/main/docs/roadmap.md). Hedef: M2 aşamasında daha erken kullanılabilir görev konsolu önizlemesiyle **v0.1.0 deneysel**. Aşamalar teslim tarihi sözü değil, kabul kapısıdır. Çekirdekte görev/runtime/journal/hizmet/CLI/tarayıcı çalışmaları ve sınırlı GPU bileşenleri vardır; [çekirdek kanıtı](https://github.com/eyleme-dev/eyleme/blob/main/README.tr.md) her uygulamanın kapsamını belirtir. Tam insan kimliği doğrulanmış akış, model, öğrenme ve otonom geliştirme kabulü ayrıdır.

## Seçilen ilk çalışan uygulama

Bakımcı görev çekirdeği ve web arayüzünü seçti: görev oluşturma, çalıştırma, inceleme, durdurma, kaydetme ve yeniden açma. M1 deterministik yürütmeyi kurar, M2 kayıtlı görevle tarayıcı akışını tamamlar. [Bileşen önerisi ve kabul senaryoları](project-structure.md) bu hedefi uygulamadan önce incelenebilir kılar. İlk kanıt model veya GPU gerektirmez.

Sonraki deneysel sürüm aynı uygulamayı küçük 3B yerleştirme ortamı, öğrenilmiş politika/dünya dinamiği, desteklenen tek yerel dil modeli, izinli öğrenme ve geliştirme takımının PR akışıyla genişletir. Her yeteneğin kendi kabul koşulu vardır; ilk kanıtın seçilmesi sonraki yeteneklerin hazır olduğu anlamına gelmez.

Birincil kabul cihazı 24 GB birleşik bellekli MacBook Pro M4 Pro olarak kalır. Bakımcı ayrıca 24 GB birleşik bellekli Mac mini M4 ve RTX 4070 Ti Super 16 GB VRAM + 32 GB RAM içeren Linux sistemi bildirdi. [Üç cihazlık envanter](project-structure.md#erişilebilir-test-envanteri), birincil/sonraki karşılaştırma rollerini, sahibinin bildirdiği bilgileri ve çalıştırılmamış kontrolleri kaydeder. Ek cihaz veya tek cihazdaki iki iş yükü yeni destek kanıtı değildir. Sayısal kalite/kaynak sınırları başlangıç ölçümünden sonra sabitlenir; Linux ve ikinci cihaz yürütümü ayrı kabul ister.

| ID | Sürüm kapısı | Kapsam | Kabul kanıtı | Bağımlılık |
|---|---|---|---|---|
| M0 | Katkı temeli | Eylemci kuralları, iki dil, issue/PR şablonları, salt okunur CI | Doğrulayıcılar olumsuz örnekleri reddeder; PR ve main CI gözlenir; bakımcı incelemesi/dal kuralı durumu açıktır | Yok |
| M1 | `v0.1.0-alpha.1` | Kendi Rust çalışma alanı, tipli görev/durum/eylem sözleşmeleri, deterministik yürütücü | Rust 1.99.0; sıfır harici üretim Cargo bağımlılığı; native aarch64-apple-darwin derleme/test ve seçilmiş taşınabilir kütüphane Wasm derlemesi; native birim/kurtarma, sınır ve yetki ret testleri; Rust kaynağıyla birlikte uygulama CI’ı etkin | M0 |
| M2 | `v0.1.0-alpha.2` | İlk görev konsolu: kendi web arayüzü, yerel sunucu ve dayanıklı durum | Oluştur/çalıştır/incele/durdur/kaydet/yeniden başlat/aç; yinelenen istek, yetki reddi, etkili durma; loopback oturumu, Host/Origin, CSRF, sınırlı girdi; dayanıklı onay ve kurtarma hataları | M1 |
| M3 | `v0.1.0-alpha.3` | Native Metal işçisi, tarayıcı WebGPU ve küçük 3B sahne | M4’te gerçek hesaplama/readback; adlandırılmış tarayıcı/sürücü WebGPU; işçi/cihaz kaybı ve desteklenmeyen yol hataları; ortak bellek/iş bütçeleri; birleşik yük/kare süresi ölçümleri; host, Metal shader ve WGSL envanteri | M2 |
| M4 | `v0.1.0-beta.1` | Sınırlı 8×8 yerleştirme için CPU/Metal tensör referansları, öğrenilmiş politika ve küçük dünya modeli | Önceden tanımlı toleransta CPU/Metal eşliği; ayrılmış görevlerde kapalı döngü başarı ve tahmin hatası; kısıtlar; deterministik başlangıçla dürüst karşılaştırma | M3 |
| M5 | `v0.1.0-beta.2` | Kendi runtime’ımızda sabit Qwen3-0.6B adayı | G27 kesin artifact/tokenizer/operatör/hakları sabitler; FP32 CPU referansı ve FP16 Metal yürütümü; nicemleme isteğe bağlı; yükleme/ilk sonuç/sıcak ölçüm ve ayrılmış kalite; ortak sahne/politika/LLM bütçeleri; desteklenmeyende açık hata, hosted fallback yok | M4 |
| M6 | `v0.1.0-rc.1` | Sürümlü model atama ve izinli yerel öğrenme | Tek M4 cihazında en az iki ölçülmüş iş yükü; model-set 0.2.0 fiziksel/iş yükü bağları; kabul manifesti, canary/geri dönüş; izin/köken/tekilleştirme/holdout; sınırlı sabit yerel Unsloth Studio/MLX denemesi; export kendi Rust motorunda yeniden kabul edilmiş | M5 |
| M7 | `v0.1.0` | İhtiyaçtan PR’a protokol ve deneysel sürüm | Gerçek görevde girdi/plan/kod/kontrol/ayrı inceleme; aynı sözleşmede gerçek Codex ve Claude adaptörleri, açık çevrimiçi GitHub/sağlayıcı erişimi, idempotent PR tekrarı; yeniden üretilebilir sürüm paketinden önce Apache-2.0 bildirimleri/varlık hakları incelemesi ve G44 tam Mac kabulü | M6 |

## İlk uygulanabilir iş listesi

Bu EYL kimlikleri plan referansı olarak kalır. Kabul edilmiş G00–G45/W01 kartları bunları sınırlı işlere böler; tekil Goal issue’ları kesin kapsam ve kabule bağlanır. Her uygulamadan önce sınırlı issue açın. Tarihsel ilk Goal önerileri canlı tamamlanma kaydı değildir.

| ID | Sonraki iş | Tamamlanma koşulu |
|---|---|---|
| EYL-001 | Apache-2.0 ve katkı koşullarını uygula | Bakımcı 12 Ekim 2026 tarihinde kendi kod/belgeleri için Apache-2.0 seçti; LICENSE/NOTICE, üstveri ve köken kapsamı bağlantılı PR’larda yer alır; üçüncü taraf varlık hakları ve sürüm incelemesi ayrıdır |
| EYL-002 | Mevcut donanım matrisini ölç | Birincil M4 Pro/24 GB; ikinci Mac mini M4/24 GB; Linux RTX 4070 Ti Super/16 GB VRAM + 32 GB RAM karşılaştırma envanteri; her cihazda kesin ortam/iş yükü bağı ve gerçek kanıt; çalıştırılmayanlar not_run kalır |
| EYL-003 | Kendi Rust çalışma alanı ve CI’ını kur | Rust 1.99.0, lockfile, native macOS derleme/test ve seçilmiş taşınabilir Wasm kütüphaneleri; harici runtime crate’i yok; G02 aşama kuralları ve G07 gerçek uygulama kapıları |
| EYL-004 | Görev durum makinesini uygula | Başarı, hata, yetki reddi, zaman aşımı, yinelenen teslim ve iptal testli; dış etkiler için tam bir kez garantisi iddiası yok |
| EYL-005 | Kalıcı yerel görev günlüğünü uygula | Kesilmiş kayıt, çökme/yeniden başlatma ve uyumsuz biçim testli; sürüm ve kurtarma davranışı açık |
| EYL-006 | İlk web görev ekranını yap | Oluştur/çalıştır/incele/durdur/kaydet/yeniden aç akışı tarayıcıda sınırlı yetki ve görünür hatalarla gösterilmiş |
| EYL-007 | Native Metal ve WebGPU kaynak sınırlarını prototiple | Gerçek M4 hesaplama/readback ve tarayıcı 3B sahnesi; CPU referansı, desteklenmeyen/cihaz kaybı hataları ve birleşik bellek/iş limitleri |
| EYL-008 | İlk model sözleşmelerini sabitle | Qwen3-0.6B kabul edilmiş ilk adaydır; FP32 CPU ve FP16 Metal yolları, isteğe bağlı nicemleme; G27 artifact/hak/operatör kapsamını sabitler; politika/dünya modeli sözleşmeleri ve ölçülmüş kaynak limitleri kabul gerektirir; aday seçimi destek değildir |

## Goal sırası ve kanıt sınırları

**Kabul edilen öncelik:** kabul edilmiş M2/G17 temelinden sonra, isteğe bağlı model/eğitim çalışmasından önce geliştirici görev konsolu önizlemesini ve sınırlı tek gerçek ihtiyaçtan PR’a kanıtı teslim et. Kanıt; görev, kapsamlı değişiklik, kontroller, ayrı inceleme ve gerçek PR yanıtını kaydetmelidir; elle hazırlanmış depo PR’ları otonom koordinatörü kanıtlamaz. G38–G43 iki sağlayıcılı protokolü M3–M6’dan bağımsız tamamlayabilir. Tam deneysel M7/G44/G45 sürümü kalan yetenek ve kabullerini gerektirir; erken teslim bunları kaldırmaz.

G03 bu sözleşmeleri eşler; G04 gerçek Rust/macOS/SDK/tarayıcı ortamını doğrular. G07 uygulama CI’ıyla runtime kaynağını etkinleştirir. F1–F7, M1/M2 akışıdır; G17 dış örneği kabul edilmiş çekirdeğe karşı kanıtlar. Kabul edilmiş aksiyon planı bu temelden sonra, GPU işlerinden önce G38–G43 geliştirme orkestrasyonuna izin verir; M7 sürüm kapısı yine M6’ya bağlıdır. G18 sayısal kaynak limitleri kabulünden önce iş yüklerini ölçer. G27 tensör/yükleyici/model yürütümünden önce model sözleşmesini sabitler; G35/G36 yerel eğitim ve kendi motorumuzda export’u ayrı kanıtlar. G45 paketinden önce G44 bu Mac’te tam on iki adımlı akışı çalıştırır. W01 doğru website içeriğini hazırlayabilir; yayın ayrı yetki ve eşleşen canlı kanıt gerektirir.

Eklenen model-set şeması 0.2.0’dır; runtime/NeedSpec 0.1.0 kalır. Sentetik şema örneği, belge CI’ı, başarılı derleme, GPU yürütümü, eğitilmiş model kalitesi ve sürüm kabulü ayrı kanıtlardır. Bu yol haritası runtime, GPU veya eğitim sonucu sağlamaz.

## Kabul edilen Rust harness Goal revizyonu — 13 Ekim 2026

Bakımcı dokuz model rolünü, isteğe bağlı açık dış büyük model atamalarını ve yerel açık ağırlık inference için kendi Rust motorumuzu birleştiren harness’ı kabul etti. [Güncel aksiyon planı](https://github.com/eyleme-dev/devguide/blob/main/docs/tr/platform-action-plan.md) ve [güncel kartlar](https://github.com/eyleme-dev/devguide/blob/main/records/platform-goal-plan.json) yalnız gelecek yürütme önerilerini günceller. Kabul edilen yirmi dört özgün Goal kaydı değişmez; kalan yirmi üç özgün kart revize edilir, G46–G86 sınırlı platform parçaları ekler. Bunlar planlandı, tamamlanmadı. G40 mevcut gizlilik/host/çağrı/onarım sınırlarıyla engelli kalır; yeni hak verilmez.

| Sıra | Teslim | Gerekli kanıt |
|---|---|---|
| Temel | G46, G63, G54, G50: döngü/rol/model sözleşmesi, proje sınırı, türlü araç ve karar kanıtı | İki sözleşme tüketicisi; uyumsuz profil/yetki/veri çıkışı reddi, gerçek kendi araçlarımız, tam etki/kanıt geçmişi |
| Model profilleri | G27, G56, G49, G59, G67: dil, karar, görüntü, ayrı STT/TTS ve embedding | Tam artifact/operatör/hak/ön işleme/çıktı anlamı; alan ve EN/TR değerlendirme tanımları |
| Kendi inference motorumuz | Mevcut G23–G31 ve G52–G53, G57–G58, G60–G62, G68–G69 | Önce CPU referansı, sonra gerçek M4 Metal; birleşik yükte iş kalitesi, hassasiyet, gecikme/throughput/bellek ve etkili durdurma |
| Birleşim | G47–G48, G66, G55, G32, G70–G71 | İncelenen yalnız XState koordinasyon profili; sınırlı alt akış, açık dış rol sözleşmesi, yerel iş ve projeye bağlı kaynaklı RAG |
| Öğrenme/ekosistem | G33–G37, G64–G65 | İzinli episode/türev, bölme/geri çekme, aday eğitimi ve kendi Rust kabulümüz, incelenen paylaşım paketi ve uyumlu içe alma |
| Erken metin kanıtı | G73, G74, G75, G72 | Gerçek insan kaydı/durdurma, türlü skill/router ve özel yerel EN/TR kaynaklı rapor; görüntü/ses/dünya önkoşulu yok |
| Native iyileştirme | G76–G79, G83–G86 | Modele özel profiller, kendi Rust gradyan/CPU ve Metal LoRA/QLoRA, sabit holdout ve kontrollü skill terfisi |
| Kapasite | G80–G82 | Kontrollü tahmin, gerçek kalibrasyon, belirsizlik ve tarihli yatırım senaryoları; otomatik harcama yok |
| Yeniden kullanım/sürüm | G51, kalan G06/G40–G45/W01 | İki uygulama, uyumlu model değişimi ve tam döngü faydası; özgün sürüm/provider/dağıtım kapıları korunur |

Sayısal kalite/kaynak sınırları başlangıç ölçümünden sonra, aday karşılaştırmasından önce sabitlenir; popülerlik veya yayıncı hızından uydurulmaz. [Mimarideki rol tablosu](architecture.md#rust-harness-model-rolleri-ve-alana-göre-seçim) çalışma konumunu model rolünden ayırır; STT, TTS, görsel algı ve metin alanlarını ayrı tutar. Hiçbir açık ağırlık model evrensel destek sayılmaz. XState açık önerilen iş akışı bağımlılığıdır; inference motoru veya Rust yetkisinin yerine geçmez, envanter/profil kabulü bütünleşmeden önce gelir. Aynı anda bir Goal uygulanır; bağımlı işe geçmeden özel tüketim yenileme, tam kontroller, gerçek ayrı inceleme, güncel CI ve bakımcı yetkili merge gerekir.

## v0.1.0 sürüm kontrol listesi

- Her aşamanın zorunlu kontrolleri aynı sürüm adayı için güncel kanıta sahiptir; atlanan zorunlu donanım kontrolleri ilgili destek iddiasını engeller.
- Tanımlanan profiller için kalite eşikleri, p95/p99 gecikme/kare süresi, bellek ve başlangıç limitleri belirlenmiş ve karşılanmıştır. Kazançlar kadar başarısızlıklar raporlanır.
- HITL/HOTL/HIC sözleşmeleri, yetki geri alma, müdahale ve geri dönüş sınırları denenmiştir. Model çıktısı yetki genişletemez.
- EN/TR rehberler ilk uygulamayı yeniden üretir; desteklenen/desteklenmeyen hedefler açıktır. API/kod/şema sürümleri uyumludur.
- Dağıtım lisansı, model/veri hakları, toolchain/sürücü/tarayıcı envanteri ve sınırlar kayıtlıdır. Kernel yeniden yazımı, üretim kriptografisi veya platform yetkisini aşan donanım erişimi ima edilmez.
- Sürümü bakımcı kabul eder. CI tek başına model etkinleştiremez, merge veya sürüm yayını yapamaz.

## İlk sürüm dışında bırakılanlar

Linux desteği, ikinci fiziksel cihaz kabulü, genel CAD çekirdeği, bütün model mimarileri, dağıtık eğitim, yalnız Rust'tan oluşan Linux çekirdeği, her GPU sürücüsü, otomatik satın alma, gözetimsiz ayrıcalıklı kendi kendini değiştirme ve tüm üretim web özellikleri sonraki kararlardır. Yol haritası uzun vadeli mimariyi korurken önce sınırlı tek uçtan uca uygulamayı kanıtlar.

## Bellek kabul uzantısı

G87–G90 amaç kontrollü bellek sözleşmeleri, kendi episodik/semantik/knowledge graph erişimimiz, analitik snapshot ve sınırlı backend profilleri ekler. G72 artık G88’i gerektirir; isteğe bağlı analitik/veri alışverişi erken yerel metin kanıtını geciktirmez. Dört yeni kapı G44’e bağlanır. Mevcut gerekli release/tarihsel kabul ve bloke G40 sınırları korunur. [Bellek tasarımı](https://github.com/eyleme-dev/devguide/blob/main/docs/tr/memory-layer.md) kanıt, saklama süresi ve Rust bağımlılık sınırlarını tanımlar. Bunlar planlı kapılardır; yürütülmüş veritabanı/model desteği değildir.
