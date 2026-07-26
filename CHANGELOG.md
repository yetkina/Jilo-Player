# Changelog

All notable changes to **Jilo Player** are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.2.8] — 2026-07-27

### Fixed

- Playlist ekleme: macOS’ta «QR ile web’den ekle» tıklanamıyordu (TV odak sarmalayıcısı fareyi yutuyordu); QR URL’sine trailing slash eklendi.
- QR eşleştirme diyaloğunda upload sayfası tıklanabilir link olarak gösterilir (`https://www.yaydin.com/{lang}/jiloplayer/upload/`).

### Distribution

- **Mac App Store:** `1.2.8` build **39** (`DISTRIBUTION=appstore`) — incelemede; promo unlock kapalı (IAP only).
- **GitHub Releases:** [v1.2.8](https://github.com/yetkina/Jilo-Player/releases/tag/v1.2.8) — `JiloPlayer_macOS_v1.2.8.zip` (`DISTRIBUTION=direct`, **promo kod açık**).

## [1.2.7] — 2026-07-25

### Fixed

- App Store Guideline **3.1.1**: promo code redeem UI/flow App Store build’de kapatıldı (`DISTRIBUTION=appstore`); Pro yalnızca IAP. Direct build’de promo açık kaldı.
- App Store Guideline **2.1(b)**: IAP `com.yaydin.jiloplayer.pro` uygulama sürümüyle birlikte gönderildi.
- App Store Guideline **2.3.6**: Parental controls Review Notes + ekran yolu belgelendi.
- macOS App Store: `com.apple.security.network.server` entitlement kaldırıldı (istemci-only).
- macOS açılış: ağ / Keychain / hoş geldin takılmaları ve beyaz ekran düzeltildi.
- Playlist ekleme: macOS’ta «Yerel dosya» seçimi tıklanamıyordu.

### Added

- Hoş geldin ekranı: **Demo kanal listesini yükle** (yaydin.com demo M3U).
- Mac App Store’da **1.2.7** yayına alındı (build **37**).
- App Store StoreKit satın alma + sunucu doğrulama (`/api/purchase/verify`).
- macOS GitHub Release otomasyonu: `deploy_mac.sh`.
- App Store felaket senaryosu checklist (`docs/appstore_continuity.md`).
- **[Security]** Input validation / certificate pinning şablonu; **[License]** `LICENSES/FFMPEG.md`.

### Changed

- Hoş geldin ekranı: güvenlik bölümü metni veri güvenlik protokolünü ve Jilo farkını anlatacak şekilde güncellendi; «Etkinleştir» varsayılan kapalı.
- Hoş geldin ekranı: «Etkinleştir» açıldığında kullanıcı şifresi belirleme diyaloğu gösteriliyor; ebeveyn kilidi yalnızca şifre kurulduysa etkinleştiriliyor.
- Hoş geldin ekranı: «Veri Güvenliği» metni yeniden yazıldı — parolanın ebeveyn kontrolü + şifreleme rolü, gizlilik faydası, Jilo farkı ve parola unutma uyarısı daha anlaşılır anlatılıyor.
- Hoş geldin ekranı: «Yasal uyarı (kısa)» başlığı sadeleştirildi; IPTV barındırmama ve kullanıcı sorumluluğu metinleri güçlendirildi; «Hadi başlayalım» ile kabul onayı netleştirildi.
- Web playlist aktarımı: MAC/HWID ve sunucu kuyruğu kaldırıldı; sunucuda playlist içeriği saklanmaz, yalnızca ~2 dk eşleştirme oturumu.
- macOS bundle ID: `com.yaydin.jiloPlayerMacos` → `com.yaydin.jiloplayer` (çok platformlu uyum).
- macOS dağıtımı artık repoda `.app` klasörü değil; GitHub **Releases** üzerinden `JiloPlayer_macOS_*.zip` indirilir.
- **[Security]** Promo code service: input validation eklendi.

### Removed

- Arka planda sürekli web playlist senkronu (poll + `playlist_push_queue`).

### Fixed

- Cihaz ID (hwid): Keychain kaybında veya sürüm/build güncellemesinde kimlik değişmesi giderildi; UserDefaults + Flutter yedeği, v1/v2 şema ve eski Keychain servisi ile kurtarma.
- macOS build: minimum sürüm 13.5’e yükseltildi (`passkeys_darwin` / Supabase bağımlılığı).
- Hoş geldin / ayarlarda şifre belirlerken `int` tercih anahtarları (lisans/deneme) yüzünden oluşan type cast hatası giderildi.
- Aktivasyon Bilgileri kartında içerik taşması (overflow) giderildi; diyalog kaydırılabilir, pencere minimum yüksekliği 780px.
- Xtream Canlı (ve VOD/Dizi) grup sıralaması artık M3U kanal sırası yerine `get_*_categories` API sırasına göre.
- Kanal numarası ayarı anında kaydedilir; listede numara logo solunda gösterilir (`tvg-chno` varsa o, yoksa sıra no).
- Hız testi sırasında canlı yayın otomatik yeniden bağlanma devre dışı (test bitince oynatma kaldığı yerden devam eder).
- Web playlist senkronu: Supabase yapılandırması device ping yanıtından alınır; broadcast payload ayrıştırması düzeltildi.
- Android TV: metin kutusunda OK/Select ile klavyenin anında kapanması giderildi; dokunmatik tıklamada düzenleme modu açılır.
- Android TV: düzenlenebilir metin kutularında mavi kabuk çerçevesi klavyeyi kapatmaz; odaklanınca doğrudan düzenleme modu açılır (geri tuşu hariç).
- Android TV: Ayarlar metin kutusundan ok tuşu ile switch/dropdown satırlarına geçiş (Playlist ekle ile aynı davranış).
- Android TV: hoş geldin sonrası «Playlist ekle» ile açılan diyalogda odak ana menüde kalmaz; isim alanına gider.
- Büyük Xtream listelerinde uygulama çökmesi (OutOfMemory): kanal önbelleği sıkıştırılmış formatta isolate'ta yazılıyor, büyük listeler dosyaya kaydediliyor; UI önce gösteriliyor.
- Xtream M3U ayrıştırma ana thread yerine isolate'ta; hiyerarşi debug logları sadeleştirildi (ANR riski).
- Büyük listeler (26MB+) için SQLite kanal deposu: açılışta anında gösterim, grup bazlı sorgu, arka planda güncelleme.
- Oynatma sırasında donma: canlı yayında gereksiz UI yenilemesi kapatıldı; liste/EPG güncellemesi oynatma bitene kadar ertelenir.
- Android TV canlı oynatma: donanım decode (MediaCodec), küçük buffer, düşük gecikme profili; donma izleme sıklığı azaltıldı.
- Android TV codec oynatma hatası: zorunlu `mediacodec-copy` kaldırıldı; `hwdec=auto-safe` ve codec hatasında otomatik yazılım decode denemesi.
- Android TV Canlı kanal listesinden geçişte `isLive` bayrağı eksikliği giderildi; gereksiz MPV özellik sorgusu ve ana thread yükü azaltıldı.
- Android TV kayıtlı MPV seçeneklerindeki `hwdec=mediacodec-copy` ve yazım hatalı anahtarlar otomatik temizlenir; canlı yayında güvenli profil her zaman uygulanır.
- Android TV çıkış (çift geri): oynatıcı durdurulmadan kapanırken `FlutterJNI is not attached` çökmesi giderildi.

### Security

- Güvenlik denetim raporu: [SECURITY_AUDIT_REPORT.md](SECURITY_AUDIT_REPORT.md); güncelleme özeti: [docs/SECURITY_UPDATES_JUNE2026.md](docs/SECURITY_UPDATES_JUNE2026.md).
- **[Critical]** iOS ve macOS `ITSAppUsesNonExemptEncryption = true` — yerel AES-256 şifreleme için App Store export compliance bildirimi (`ios/Runner/Info.plist`, `macos/Runner/Info.plist`).
- **[Critical]** FFmpeg LGPL-2.1+ atıfı: `LICENSES/FFMPEG.md` + «Hakkında» ekranında kaynak bağlantısı (`about_jilo_dialog.dart`).
- **[Verified]** macOS iCloud yedek konteyneri (`NSUbiquitousContainers`) yapılandırması doğrulandı; yedek içeriği yerel depolama ile aynı AES-256 şifrelemesini kullanır.
- Platform güvenlik: macOS/iOS App Sandbox entitlements kontrol edildi.
- Şifreleme: AES-256 + PBKDF2 (100k iterations) + X25519 key exchange doğrulandı.
- API güvenlik: HTTPS-only, server-side purchase verification, no hardcoded credentials.
- Input validation: URL, HWID, promo code formatı doğrulama eklendi (promo servisi entegre; playlist URL entegrasyonu devam ediyor).

## [1.0.0] — 2026-05-30

### Added

- macOS sürümü: GitHub Releases’ta `JiloPlayer_macOS_v1.0.0.zip` (release build).
- Aktivasyon Bilgileri ekranı; alt çubuk lisans rozetlerinden açılır (Demo / Promosyon / Pro).
- Alt çubukta tek lisans rozeti (öncelik: Pro → aktif promosyon → demo); hover ipucu «Aktivasyon Bilgileri».
- Canlı yayın sessiz donma algısı ve otomatik yeniden bağlanma.
- Offline açılış kapısı ve ağ bağlantısı kontrolü.
- Promosyon kodu girişi ve cihaz ping senkronizasyonu.
- Kararlı cihaz kimliği (Keychain + platform).
- Ayarlar performans iyileştirmesi (`SettingsShell`).

### Changed

- «Cihaz bilgileri» → **Aktivasyon Bilgileri**; üst araç çubuğundaki (i) düğmesi kaldırıldı.
- Lisans süresi dolduğunda yalnızca trafik ışıkları + aktivasyon ekranı.
- Varsayılan macOS pencere boyutu 1000×720.

### Fixed

- Ayarlar ekranı performansı ve ListTile uyarıları.
- Canlı yayın URL çift slash normalizasyonu.

---

[Unreleased]: https://github.com/yetkina/Jilo-Player/compare/v1.2.8...HEAD
[1.2.8]: https://github.com/yetkina/Jilo-Player/releases/tag/v1.2.8
[1.2.7]: https://github.com/yetkina/Jilo-Player/compare/v1.0.0...v1.2.8
[1.0.0]: https://github.com/yetkina/Jilo-Player/releases/tag/v1.0.0
