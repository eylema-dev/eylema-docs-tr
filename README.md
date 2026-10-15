# Eyleme Türkçe belgeleri

**Ad güncellemesi — 14 Ekim 2026:** Ürünün adı **Eyleme** (önceki adı Eylema), tamamlayıcı ürünün adı **Derleme** (önceki adı Derlema) oldu; **Onama** aynı kaldı. GitHub organizasyonunun adı artık `eyleme-dev` (önceki adı `eylema-dev`). Ana deponun adı artık `eyleme-dev/eyleme`. 15 Ekim 2026 tarihinde altı `eylema-*` alt deposu `eyleme-*` olarak değişti. Komutlar, crate/paket adları, ortam değişkenleri, veri yolları ve protokol/şema tanımlayıcıları uyumluluk için mevcut yazımlarını korur. Tarihsel kanıtlar özgün ad ve bağlantıları korur.

İngilizce asılların Türkçe mimari, API ve ürün belgeleri. [English](https://github.com/eyleme-dev/eyleme-docs-en). İngilizce kanonik dildir; tanımlayıcılar çevrilmez.

**Aşama: tasarım ve depo araçları.** Bu belgeler çalışan Rust uygulaması, GPU sonucu, eğitilmiş model veya üretim dağıtımı sunmaz. İlk ürün yönü deterministik görev konsoludur; sonraki kilometre taşları hesaplama, modeller ve öğrenmeyi ekler.

## Tek marka ve topluluk

**Eyleme**, tek marka ve [eyleme.dev](https://eyleme.dev) üzerindeki bağımsız kullanılabilen açık kaynak üründür. **Eyleme Derleme** ve **Eyleme Onama**, ayrı geliştirilen private kaynaklı abonelik ürünleridir. Birlikte kullanım akışı **Derleme → Onama → Eyleme** sırasındadır; desteklenen bağımsız Eyleme çekirdeği, ücretli abonelik olmadan erişim ve güvenlik kontrollerini korur.

Kanonik [ürün ailesi sözleşmesi](https://github.com/eyleme-dev/eyleme/blob/main/docs/tr/product-family.md), public arayüzleri, ticari sınırları ve kanıt sınırlarını tanımlar. [Public örnekleri](https://github.com/eyleme-dev/eyleme-examples) inceleyin, [Discussions](https://github.com/eyleme-dev/eyleme/discussions) üzerinden tartışmalara katılın, [public issue formlarını](https://github.com/eyleme-dev/eyleme/issues/new/choose) kullanın ve aşağıdaki katkı akışını izleyin. Ticari ürün açıklamaları private depo erişimi gerektirmeyen [public site tanıtımında](https://eyleme.dev/#products) yer alır. Güncel topluluk alan adı tarihsel `eylema.dev` hedefinin yerini alır; teknik kimlikler değişmez.

## Sözleşmeler

- [Mimari](docs/architecture.md)
- [API ve insan denetimi](docs/api-reference.md)
- [Geliştirme ve işletim](docs/development-and-operations.md)
- [Öğrenme ve eğitim](docs/learning-and-training.md)
- [Proje yapısı ve ilk uygulama](docs/project-structure.md)
- [Yol haritası](docs/roadmap.md)

## Depo sınırları

Çalışma zamanı kaynakları ve makine şemaları [Eyleme](https://github.com/eyleme-dev/eyleme) içinde; katkı politikası ve kalite kapıları [devguide](https://github.com/eyleme-dev/devguide) içindedir. [Depo haritası](https://github.com/eyleme-dev/devguide/blob/main/docs/tr/repository-map.md) her sorumluluğu tanımlar. Kendi kaynak kodumuz ve belgelerimiz [Apache-2.0](LICENSE) lisanslıdır. Ayrı belirtilen üçüncü taraf içerikleri, model ağırlıkları ve veri kümeleri kendi koşullarını korur.

Düzenlemeden önce [katkı rehberini](CONTRIBUTING.tr.md) okuyun. İngilizce asıl ile devguide içindeki sabitlenmiş depo kümesini birlikte güncelleyin. Yerel parmak izleri incelenen baytları kaydeder; depo kümesi kontrolü iki dili, API tanımlayıcılarını, yol haritası kimliklerini ve depolar arası bağlantıları karşılaştırır. Anlamsal çeviri doğruluğunu kanıtlamaz.

## Tarihsel kayıtlar

- [Mimari v0.1](archive/architecture-v0.1.tr.md)
- [Mimari v0.2](archive/architecture-v0.2.tr.md)
- [İlk API taslağı](archive/api-outline-v0.1.tr.md)

Bu kayıtlar yürürlükteki sözleşmeler değildir. [Taşıma kaydı](https://github.com/eyleme-dev/devguide/blob/main/docs/tr/repository-migration.md) kaynak revizyonlarını ve birleştirme sırasını açıklar. Yeni varsayılan dal belge bağlantıları, bakımcı eşgüdümlü taşıma PR'larını birleştirdiğinde erişilebilir olur.
