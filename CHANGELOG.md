# Changelog

All notable changes to **Jilo Player** are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.0.0] — 2026-05-30

### Added

- macOS dağıtım paketi: `releases/v1.0.0/Jilo Player.app` (release build).
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

[Unreleased]: https://github.com/yetkina/Jilo-Player/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/yetkina/Jilo-Player/releases/tag/v1.0.0
