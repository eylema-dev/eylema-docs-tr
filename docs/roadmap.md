# Eylema ilk sürüm yol haritası

Revizyon **0.3.0**, 11 Ekim 2026. İngilizce kanoniktir; [English](https://github.com/eylema-dev/eylema-docs-en/blob/main/docs/roadmap.md). Hedef: **v0.1.0 deneysel**; üretime hazır evrensel framework değildir. Kilometre taşları kabul kapılarıdır, tarih taahhüdü değildir. Bugün yalnızca depo belgeleri ve araçları vardır. M0 temeli ve depo bölünmesi merge edilmiştir; G02 belge/uygulama aşama kapıları ayrı inceleme ve güncel PR/main CI’dan geçmiştir. Bu depo araçları kanıtıdır; uygulama yürütümü değildir.

## Seçilen ilk çalışan uygulama

Bakımcı görev çekirdeği ve web arayüzünü seçti: görev oluşturma, çalıştırma, inceleme, durdurma, kaydetme ve yeniden açma. M1 deterministik yürütmeyi kurar, M2 kayıtlı görevle tarayıcı akışını tamamlar. [Bileşen önerisi ve kabul senaryoları](project-structure.md) bu hedefi uygulamadan önce incelenebilir kılar. İlk kanıt model veya GPU gerektirmez.

Sonraki deneysel sürüm aynı uygulamayı küçük 3B yerleştirme ortamı, öğrenilmiş politika/dünya dinamiği, desteklenen tek yerel dil modeli, izinli öğrenme ve geliştirme takımının PR akışıyla genişletir. Her yeteneğin kendi kabul koşulu vardır; ilk kanıtın seçilmesi sonraki yeteneklerin hazır olduğu anlamına gelmez.

İlk deneysel sürüm 24 GB birleşik bellekli tek Apple M4 Pro MacBook Pro’yu; aynı cihazda native macOS CPU/Metal ve tarayıcı Wasm/WebGPU’yu hedefler. macOS 27.0.1 gözlenmiştir; G04 gerçek araç/SDK/tarayıcıyı doğrular. Linux desteği ve ikinci fiziksel cihaz kabulü ertelenmiştir. Atama, tek HardwareProfile’a bağlı en az iki ölçülmüş WorkloadProfile karşılaştırır; bunlar iki cihaz sayılmaz. Sayısal limitlerden önce gerçek bellek, gecikme/kare süresi ve kalite başlangıçlarını ölçün; donanım ve iş yükü seçilmeden rakam uydurmayın.

| ID | Sürüm kapısı | Kapsam | Kabul kanıtı | Bağımlılık |
|---|---|---|---|---|
| M0 | Katkı temeli | Eylemci kuralları, iki dil, issue/PR şablonları, salt okunur CI | Doğrulayıcılar olumsuz örnekleri reddeder; PR ve main CI gözlenir; bakımcı incelemesi/dal kuralı durumu açıktır | Yok |
| M1 | `v0.1.0-alpha.1` | Kendi Rust çalışma alanı, tipli görev/durum/eylem sözleşmeleri, deterministik yürütücü | Rust 1.99.0; sıfır harici üretim Cargo bağımlılığı; native aarch64-apple-darwin derleme/test ve seçilmiş taşınabilir kütüphane Wasm derlemesi; native birim/kurtarma, sınır ve yetki ret testleri; Rust kaynağıyla birlikte uygulama CI’ı etkin | M0 |
| M2 | `v0.1.0-alpha.2` | İlk görev konsolu: kendi web arayüzü, yerel sunucu ve dayanıklı durum | Oluştur/çalıştır/incele/durdur/kaydet/yeniden başlat/aç; yinelenen istek, yetki reddi, etkili durma; loopback oturumu, Host/Origin, CSRF, sınırlı girdi; dayanıklı onay ve kurtarma hataları | M1 |
| M3 | `v0.1.0-alpha.3` | Native Metal işçisi, tarayıcı WebGPU ve küçük 3B sahne | M4’te gerçek hesaplama/readback; adlandırılmış tarayıcı/sürücü WebGPU; işçi/cihaz kaybı ve desteklenmeyen yol hataları; ortak bellek/iş bütçeleri; birleşik yük/kare süresi ölçümleri; host, Metal shader ve WGSL envanteri | M2 |
| M4 | `v0.1.0-beta.1` | Sınırlı 8×8 yerleştirme için CPU/Metal tensör referansları, öğrenilmiş politika ve küçük dünya modeli | Önceden tanımlı toleransta CPU/Metal eşliği; ayrılmış görevlerde kapalı döngü başarı ve tahmin hatası; kısıtlar; deterministik başlangıçla dürüst karşılaştırma | M3 |
| M5 | `v0.1.0-beta.2` | Kendi runtime’ımızda sabit Qwen3-0.6B adayı | G27 kesin artifact/tokenizer/operatör/hakları sabitler; FP32 CPU referansı ve FP16 Metal yürütümü; nicemleme isteğe bağlı; yükleme/ilk sonuç/sıcak ölçüm ve ayrılmış kalite; ortak sahne/politika/LLM bütçeleri; desteklenmeyende açık hata, hosted fallback yok | M4 |
| M6 | `v0.1.0-rc.1` | Sürümlü model atama ve izinli yerel öğrenme | Tek M4 cihazında en az iki ölçülmüş iş yükü; model-set 0.2.0 fiziksel/iş yükü bağları; kabul manifesti, canary/geri dönüş; izin/köken/tekilleştirme/holdout; sınırlı sabit yerel Unsloth Studio/MLX denemesi; export kendi Rust motorunda yeniden kabul edilmiş | M5 |
| M7 | `v0.1.0` | İhtiyaçtan PR’a protokol ve deneysel sürüm | Gerçek görevde girdi/plan/kod/kontrol/ayrı inceleme; aynı sözleşmede gerçek Codex ve Claude adaptörleri, açık çevrimiçi GitHub/sağlayıcı erişimi, idempotent PR tekrarı; yeniden üretilebilir sürüm paketinden önce lisans kararı ve G44 tam Mac kabulü | M6 |

## İlk uygulanabilir iş listesi

Bu EYL kimlikleri plan referansı olarak kalır. Kabul edilmiş G00–G45/W01 kartları bunları sınırlı işlere böler; tekil Goal issue’ları kesin kapsam ve kabule bağlanır. Her uygulamadan önce sınırlı issue açın. Tarihsel ilk Goal önerileri canlı tamamlanma kaydı değildir.

| ID | Sonraki iş | Tamamlanma koşulu |
|---|---|---|
| EYL-001 | Lisans ve katkı koşullarını seç | Bakımcı kararı ve köken kuralları kaydedilmiş; örtük katkıcı anlaşması yok |
| EYL-002 | İlk iş yükü/donanım matrisini sabitle | G03 sözleşmeleri tek M4 Pro/24 GB Mac ve ayrı native/tarayıcı iş yüklerini belirtir; G04 araç envanterini çıkarır; G18 görev/sahneyi ölçer; Linux ve ikinci fiziksel cihaz sonraki kapsamdır; çalıştırılmamış yürütüm `not_run` kalır |
| EYL-003 | Kendi Rust çalışma alanı ve CI’ını kur | Rust 1.99.0, lockfile, native macOS derleme/test ve seçilmiş taşınabilir Wasm kütüphaneleri; harici runtime crate’i yok; G02 aşama kuralları ve G07 gerçek uygulama kapıları |
| EYL-004 | Görev durum makinesini uygula | Başarı, hata, yetki reddi, zaman aşımı, yinelenen teslim ve iptal testli; dış etkiler için tam bir kez garantisi iddiası yok |
| EYL-005 | Kalıcı yerel görev günlüğünü uygula | Kesilmiş kayıt, çökme/yeniden başlatma ve uyumsuz biçim testli; sürüm ve kurtarma davranışı açık |
| EYL-006 | İlk web görev ekranını yap | Oluştur/çalıştır/incele/durdur/kaydet/yeniden aç akışı tarayıcıda sınırlı yetki ve görünür hatalarla gösterilmiş |
| EYL-007 | Native Metal ve WebGPU kaynak sınırlarını prototiple | Gerçek M4 hesaplama/readback ve tarayıcı 3B sahnesi; CPU referansı, desteklenmeyen/cihaz kaybı hataları ve birleşik bellek/iş limitleri |
| EYL-008 | İlk model sözleşmelerini sabitle | Qwen3-0.6B kabul edilmiş ilk adaydır; FP32 CPU ve FP16 Metal yolları, isteğe bağlı nicemleme; G27 artifact/hak/operatör kapsamını sabitler; politika/dünya modeli sözleşmeleri ve ölçülmüş kaynak limitleri kabul gerektirir; aday seçimi destek değildir |

## Goal sırası ve kanıt sınırları

G03 bu sözleşmeleri eşler; G04 gerçek Rust/macOS/SDK/tarayıcı ortamını doğrular. G07 uygulama CI’ıyla runtime kaynağını etkinleştirir. F1–F7, M1/M2 akışıdır; G17 dış örneği kabul edilmiş çekirdeğe karşı kanıtlar. Kabul edilmiş aksiyon planı bu temelden sonra, GPU işlerinden önce G38–G43 geliştirme orkestrasyonuna izin verir; M7 sürüm kapısı yine M6’ya bağlıdır. G18 sayısal kaynak limitleri kabulünden önce iş yüklerini ölçer. G27 tensör/yükleyici/model yürütümünden önce model sözleşmesini sabitler; G35/G36 yerel eğitim ve kendi motorumuzda export’u ayrı kanıtlar. G45 paketinden önce G44 bu Mac’te tam on iki adımlı akışı çalıştırır. W01 doğru website içeriğini hazırlayabilir; yayın ayrı yetki ve eşleşen canlı kanıt gerektirir.

Eklenen model-set şeması 0.2.0’dır; runtime/NeedSpec 0.1.0 kalır. Sentetik şema örneği, belge CI’ı, başarılı derleme, GPU yürütümü, eğitilmiş model kalitesi ve sürüm kabulü ayrı kanıtlardır. Bu yol haritası runtime, GPU veya eğitim sonucu sağlamaz.

## v0.1.0 sürüm kontrol listesi

- Her aşamanın zorunlu kontrolleri aynı sürüm adayı için güncel kanıta sahiptir; atlanan zorunlu donanım kontrolleri ilgili destek iddiasını engeller.
- Tanımlanan profiller için kalite eşikleri, p95/p99 gecikme/kare süresi, bellek ve başlangıç limitleri belirlenmiş ve karşılanmıştır. Kazançlar kadar başarısızlıklar raporlanır.
- HITL/HOTL/HIC sözleşmeleri, yetki geri alma, müdahale ve geri dönüş sınırları denenmiştir. Model çıktısı yetki genişletemez.
- EN/TR rehberler ilk uygulamayı yeniden üretir; desteklenen/desteklenmeyen hedefler açıktır. API/kod/şema sürümleri uyumludur.
- Dağıtım lisansı, model/veri hakları, toolchain/sürücü/tarayıcı envanteri ve sınırlar kayıtlıdır. Kernel yeniden yazımı, üretim kriptografisi veya platform yetkisini aşan donanım erişimi ima edilmez.
- Sürümü bakımcı kabul eder. CI tek başına model etkinleştiremez, merge veya sürüm yayını yapamaz.

## İlk sürüm dışında bırakılanlar

Linux desteği, ikinci fiziksel cihaz kabulü, genel CAD çekirdeği, bütün model mimarileri, dağıtık eğitim, yalnız Rust'tan oluşan Linux çekirdeği, her GPU sürücüsü, otomatik satın alma, gözetimsiz ayrıcalıklı kendi kendini değiştirme ve tüm üretim web özellikleri sonraki kararlardır. Yol haritası uzun vadeli mimariyi korurken önce sınırlı tek uçtan uca uygulamayı kanıtlar.
