# DTMF Digit '4' Tone Generator (Project Elka 2)

Proyek simulasi dan perancangan rangkaian pembangkit sinyal **DTMF (Dual-Tone Multi-Frequency)** untuk karakter **angka 4** menggunakan LTspice.

---

## 📌 Deskripsi Proyek

DTMF menggunakan kombinasi dua frekuensi sinusoidal (satu dari kelompok frekuensi rendah dan satu dari kelompok frekuensi tinggi) untuk merepresentasikan tombol pada keypad telepon.

Untuk **Digit 4**:
- **Low Group Frequency ($f_L$)**: `770 Hz` (Baris 2)
- **High Group Frequency ($f_H$)**: `1209 Hz` (Kolom 1)
- **Sinyal Output**: Superposisi linear dari $f_L$ dan $f_H$ melalui rangkaian summing amplifier ($V_{DTMF} = V_{O1} + V_{O2}$).

---

## 📂 Struktur Direktori

```plaintext
oscillator_DTMF4/
├── ltspice_sim/
│   ├── ideal_case/
│   │   ├── Draft1.asc              # Skematik draft awal pengujian osilator
│   │   ├── osilator_1.asc          # Skematik osilator DTMF-4 dengan komponen ideal
│   │   └── dtmf_4.wav              # Hasil ekspor audio simulasi (ideal)
│   ├── standarized_case/
│   │   ├── osilator.asc            # Skematik osilator DTMF-4 dengan nilai komponen standar (E12/E24) & model TL072
│   │   └── dtmf_4.wav              # Hasil ekspor audio simulasi (standar)
│   └── library/
│       ├── TL072.301               # Model SPICE subcircuit untuk Op-Amp TL072
│       └── tl072.pdf               # Datasheet Texas Instruments TL072
├── reference/                      # Dokumen pendukung dan referensi perancangan
├── .gitignore                      # Filter file temporary & output simulasi LTspice (*.raw, *.log, dll)
└── README.md                       # Dokumentasi proyek
```

---

## ⚙️ Rincian Implementasi

1. **Ideal Case (`ltspice_sim/ideal_case/`)**:
   - Menggunakan model `opamp2` ideal.
   - Nilai $R$ dan $C$ menggunakan nilai kalkulasi murni untuk mencapai frekuensi target persis $770\text{ Hz}$ dan $1209\text{ Hz}$.

2. **Standardized Case (`ltspice_sim/standarized_case/`)**:
   - Menggunakan model subcircuit Op-Amp JFET **TL072**.
   - Nilai resistor dan kapasitor disesuaikan dengan nilai toleransi komponen standar pasaran (deret E12 / E24).
   - Dilengkapi direktif `.wave` untuk mengekspor sinyal komposit langsung ke format audio `.wav` 16-bit 44.1 kHz.

---

## 🚀 Cara Menjalankan Simulasi

1. Buka file skematik (`.asc`) di **LTspice**.
2. Pastikan file model SPICE `TL072.301` dapat diakses oleh direktif `.include ../library/TL072.301` pada skematik standar.
3. Tekan **Run (Alt + R)** untuk memulai simulasi transient.
4. Dengarkan file `dtmf_4.wav` yang dihasilkan untuk memverifikasi nada DTMF digit 4.
