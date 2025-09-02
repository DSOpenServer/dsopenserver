# DSOpenServer (DokuzSistem Open Server)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)


DSOpen ekosisteminin backend tarafı olan **DSOpenServer**, DokuzSistem’in açık kaynak (OSS) sunucu/servis framework’üdür. Amacı; modüler, genişletilebilir ve “coder dostu” bir çekirdek üzerinde kurulu, çoklu veritabanı ve esnek yetkilendirme desteğiyle **modern backend** geliştirme deneyimi sunmaktır.

> Bu proje, şirket içinde **DokuzSistemBase** adıyla geliştirilen kapalı kaynak çözümün OSS karşılığıdır. Aşağıdaki özellik ve modül yapısı, bu temel üzerinden sadeleştirilerek yeniden düzenlenmiştir.

---

## Neden DSOpenServer?

- **Geliştirici dostu çekirdek**: Expression tabanlı yardımcılar ve zengin extension’lar ile tekrarı azaltan, okunaklı kod.
- **Kriptografi & Token**: `ChaCha20` (simetrik) ve `Curve25519` (asimetrik) ile güçlendirilmiş **DokuzToken** altyapısı.
- **DORM: Çoklu veritabanı ORM**: MsSql, MySql, PostgreSql desteği; **DataContainer** ile tek listede farklı tipleri birlikte yönetebilme; form/dictionary/json giriş-çıkışları; bulk CRUD ve server-side paging.
- **Eklenti (Plugin) mimarisi**: Uygulamayı yeniden başlatmadan modül yükleme/çıkarma; özelleştirilebilir operasyon akışları.
- **Veri Kuyruğu = Cache yaklaşımı**: Redis gerektirmeden **DataContainer** ile zamanlanmış/elle tetiklenen yenilemeler ve insert/update/delete tetikleyicileri.
- **Esnek Yetkilendirme**: Senaryodan bağımsız; operasyon bazlı ve nokta bazlı yetkilendirme birlikte.
- **Ayar Yönetimi**: **AppSettingsManager** ile tip güvenli, esnek konfigürasyon.

> Not: Kurumsal sürümde bazı sınıflar geçici olarak `Obsolete` ile işaretlenmiş olabilir; OSS sürümde bu işaretlemeler temizlenerek kalıcı mimariye taşınacaktır.

---

## Mimari Genel Bakış

DSOpenServer, portföyünüzdeki UI projelerini (**DSOpen**) tamamlayan bir **sunucu runtime + framework** sağlar. Amaç; **katmanlı mimari** ile core → data → operation → presentation → test zincirinde net sorumluluklar ve genişletilebilir yüzeyler sunmaktır.

### Katmanlar & Modüller

> Aşağıdaki adlandırmalar, önceki “DokuzSistemBase” eşlemesini parantez içinde belirtir; OSS’de yeni isimlendirme DSOpenServer olarak sadeleştirilmiştir.

**1) Core**  _(DokuzSistemBase.Core)_
- **DokuzToken**: `ChaCha20` tabanlı token üretimi ve yardımcıları.
- **Helper**: Ortak extension’lar ve yardımcı sınıflar.
- **Helper.Service / Helper.WebApp**: Console ve Web uygulamaları için yardımcılar.
- **Migration**: Veritabanı geçişi için temel altyapı (sorgu/strateji dışı çekirdek bileşenler).
- **Security**: `ChaCha20`, `Curve25519` dâhil kripto yardımcıları.

**2) Data**  _(DokuzSistemBase.Data)_
- **DORM (Dokuz ORM)**: Girdi (Entity/Dictionary/Form/Json), Mapper, QueryBuilder; Context ve Infrastructure paketleri.
- **OutputDatas**: Liste/Dictionary/Json vb. çıktı formatları.
- **DataContainer**: Farklı veri tiplerini tek listede yöneten çekirdek; Infrastructure ile desteklenir.
- **DtoModel / EntityModel**: Ana çözüme taşınacak anlaşma/test amaçlı modeller.
- **Helper / Infrastructure / Repositories**: Veri katmanı yardımcıları ve taban sınıflar.

**3) Operation**  _(DokuzSistemBase.Operation)_
- **ExceptionHandling**: Exception/Validation/Log akışları.
- **Helper / Infrastructure**: Operasyon genel yardımcıları ve taban sınıflar.
- **Manager**: Konfigürasyona göre uygun Repository/Context çözümleyen OperationManager.
- **ServiceApp / WebApp**: Servis (Console) ve Web/App/API tabanları.

**4) Presentation**  _(DokuzSistemBase.Presentation)_
- **Authentication / Authorization**: Kimlik ve yetki altyapıları.
- **Infrastructure**: Servis, WebApp/WebApi/WebService ve Windows için başlangıç sınıfları.

**5) Test**  _(DokuzSistemBase.Test)_
- **Test**: Birim/entegrasyon testleri için temel paketler.
- **Presentation.TestServiceApp / TestWebApi**: Sunum katmanı örnek test uygulamaları.

---

## Desteklenen Veritabanları
- Microsoft SQL Server (MsSql)
- MySql
- PostgreSql

> DORM; bulk CRUD, server-side paging ve form/dictionary/json veri alışverişini destekleyecek şekilde tasarlanmıştır.

---

## Yol Haritası (Kısa)
- **Belgeler**: Kurulum, yapılandırma ve mimari rehberlerin tamamlanması.
- **Paketleme**: Katmanların bağımsız paketlere ayrılması ve sürümleme (SemVer) düzeni.
- **Eklenti SDK’sı**: Plugin geliştirme kılavuzu ve örnekleri.
- **Güvenlik Sertleşmesi**: Kripto/Token katmanlarının ek tehdit modellemesi ve kılavuzları.
- **Benchmark’lar**: DORM ve DataContainer performans ölçümleri.

---

## Katkıda Bulunma
- Sorun/öneri için **Issues** açın; büyük değişiklikler için önce tartışma başlatın.
- PR’larda küçük ve odaklı değişiklikleri tercih edin; test ve dokümantasyon eşlik etsin.
- Sürümleme **SemVer** ile yapılacaktır; `feat:` ve `fix:` odaklı net PR açıklamaları değerlidir.

---

## Lisans
**MIT** — Bu proje MIT lisansı ile dağıtılır. Ayrıntılar için `LICENSE` dosyasına bakın.

*Kısa özet*: Kullanım, kopyalama, değiştirme ve ticari dağıtıma izin verir; telif hakkı bildirimi ve lisans metni korunmalıdır. Yazılım **“olduğu gibi”** sunulur, herhangi bir garanti verilmez.

---

## İletişim & Güvenlik
- Soru ve destek: _repo Issues_
- Güvenlik bildirimleri: **[security contact eklenecek]** (lütfen özelden iletin)

