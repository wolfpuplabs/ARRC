# RC Arena — Markerless AR

Mobil RC di AR tanpa marker (WebXR). Solo & multiplayer, suara mesin, drift,
arena + rintangan, partikel tabrakan, health & skor.
Jalan di Chrome Android (perangkat ARCore). iOS Safari belum mendukung WebXR.

## Struktur
```
rc-arena/
├── index.html        ← game-nya (buka ini)
├── rc-car.glb        ← model mobil (biner; jangan di-edit teks)
├── .nojekyll
└── gameserver/       ← OPSIONAL: server-authoritative — BUKAN untuk Pages
```

## Deploy (GitHub Pages — gratis, HTTPS otomatis)
1. Repo baru → Add file → Upload files → drag SELURUH isi folder ini (termasuk rc-car.glb).
2. Settings → Pages → Source: main, folder / (root) → Save.
3. ~1–2 menit → https://username.github.io/nama-repo/  → buka di Chrome Android.

## Kontrol
- Joystick kiri = maju / mundur, joystick kanan = belok.
- Tombol mode setir (pojok kanan atas) muter 3 pilihan:
  👁 Ikut Layar (default, paling mirip car game biasa) · 🚗 Konsisten · 🏎️ Realistis.
- Tombol lain: mute, taruh ulang, ⟳ reload, ✕ keluar AR.

## Multiplayer — GRATIS (default, tanpa server)
Isi nama + kode room yang sama di semua HP, tekan "Konek room". Orang pertama
otomatis jadi host (pakai PeerJS broker publik, gratis). Lalu kalibrasi 2 titik
(tap titik A & B yang sama secara fisik). Mobil lawan, health bar, papan skor,
dan tabrakan langsung jalan.

Catatan: di mode gratis ini health & skor dihitung di tiap HP, jadi BISA SEDIKIT
BEDA antar pemain (tidak ada wasit pusat). Cukup buat main bareng teman.

## Multiplayer — KONSISTEN (opsional, server-authoritative)
Kalau mau health & skor benar-benar sama persis lintas pemain, deploy folder
gameserver/ (gratis di Render/Railway) lalu di index.html set:

    const SERVER_URL = 'wss://domain-server-kamu';

Biarkan null untuk mode P2P gratis di atas. Detail di gameserver/README.md.

## Custom mobil default (kelihatan semua pemain)
Model harus di-bundle di repo (bukan upload runtime):
1. Ganti rc-car.glb dengan modelmu (nama sama).
2. Di index.html set USE_GLB = true.
3. Deploy. Semua pemain pakai model itu.
Syarat: Y-up, ground y≈0, roda jadi node wheel_FL/FR/RL/RR (untuk animasi roda).
Tombol "Upload .glb" di app = preview lokal saja (cuma tampil di layarmu).
