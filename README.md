# Workflow Documentation Template

Template repository untuk workflow dokumentasi berbasis Claude Code. Dirancang agar project baru bisa langsung "Use this template" dan dapat struktur `docs/` + `CLAUDE.md` yang siap pakai — tanpa setup manual.

**Cocok untuk:** project solo maupun tim kecil yang ingin AI agent (Claude Code) bekerja dengan konteks terstruktur, keputusan tercatat, dan rencana implementasi yang rapi.

---

## Daftar isi

- [Cara pakai — project baru](#cara-pakai--project-baru)
- [Cara pakai — project sudah berjalan](#cara-pakai--project-sudah-berjalan)
- [Checklist inisialisasi](#checklist-inisialisasi)
- [Workflow sehari-hari](#workflow-sehari-hari)
- [Struktur folder](#struktur-folder)

---

## Cara pakai — project baru

### 1. Buat repo dari template

1. Buka repo template ini di GitHub.
2. Klik tombol hijau **"Use this template"** → pilih **"Create a new repository"**.
3. Isi nama repo, deskripsi, dan visibilitas (public/private).
4. Klik **"Create repository"**.

### 2. Clone dan mulai isi

```bash
git clone git@github.com:<username>/<project-name>.git
cd <project-name>
```

### 3. Isi file template

Ikuti [checklist inisialisasi](#checklist-inisialisasi) di bawah.

---

## Cara pakai — project sudah berjalan

Kalau kamu sudah punya project yang sedang berjalan dan ingin menambahkan workflow ini:

### 1. Salin file template

```bash
# Dari folder template (repo ini)
cp CLAUDE.md /path/ke/project-mu/
cp -r docs/ /path/ke/project-mu/docs/
```

> **Hati-hati:** Kalau project-mu sudah punya `docs/`, timpa hanya file yang kamu butuhkan. Jangan timpa `docs/features/` atau `docs/planning/` kalau sudah ada isinya.

### 2. Opsional: ambil hanya sebagian

Kalau hanya butuh workflow planning-nya saja:

```bash
cp -r docs/planning/ /path/ke/project-mu/docs/planning/
cp docs/backlog.md /path/ke/project-mu/docs/
cp docs/decision-log.md /path/ke/project-mu/docs/
```

Kalau hanya butuh `ai-context.md` sebagai template mandat:

```bash
cp docs/ai-context.md /path/ke/project-mu/docs/
```

### 3. Commit dan mulai isi

```bash
cd /path/ke/project-mu
git add CLAUDE.md docs/
git commit -m "docs: add workflow documentation structure"
```

Lalu ikuti [checklist inisialisasi](#checklist-inisialisasi).

---

## Checklist inisialisasi

Setelah template terpasang, isi 4 file ini sesuai project-mu. Urutan disarankan:

### 1. `CLAUDE.md` — ganti nama project

```markdown
# Nama Project — Claude Code Context
```

Ganti `[Project Name]` dengan nama project-mu. Biarkan link ke `docs/` tetap seperti adanya — itu sudah generik.

### 2. `docs/ai-context.md` — isi 4 section pertama

Hanya 4 section atas yang wajib diisi; section 5 (Documentation Workflow) sudah terisi penuh dan tidak perlu diubah:

| Section | Yang harus diisi |
|---|---|
| 1. Tech Stack | Bahasa, framework, database, versi constraint |
| 2. Architecture Mandates | Aturan arsitektur absolut (contoh: "semua logika domain di `internal/`") |
| 3. Rules | Aturan teknis untuk AI agent (contoh: konvensi naming, error handling) |
| 4. Local Dev Environment | Cara start, rebuild, clear cache, prasyarat |

Setiap section sudah ada placeholder `<!-- ISI DI SINI -->` dan contoh kalimat sebagai panduan.

> **Tips:** Section 1–4 bisa diisi bertahap. Mulai dari Tech Stack dulu (5 menit), lalu tambah Rules sambil jalan.

### 3. `docs/backlog.md` — opsional, bisa dikosongkan dulu

Format item backlog sudah tersedia di file. Tidak wajib diisi di awal.

### 4. `docs/decision-log.md` — opsional, bisa dikosongkan dulu

Format entry + kriteria pencatatan sudah tersedia. Isi saat keputusan teknis pertama muncul.

### File yang TIDAK perlu diisi di awal

- `docs/planning/` — akan terisi otomatis saat kamu mulai membuat ticket planning dengan AI agent.
- `docs/features/` — akan terisi otomatis saat fitur sudah selesai dikerjakan.
- `docs/index.md` — sudah generik, tidak perlu diubah kecuali mau menambah section.

---

## Workflow sehari-hari

Setelah template terinisialisasi, ini alur kerja harian dengan Claude Code:

### Mulai sesi baru

Buka Claude Code di folder project. Claude akan membaca `CLAUDE.md` → `docs/ai-context.md` secara otomatis. Semua mandat, arsitektur, dan rules langsung aktif.

### Tambah ide / bug → backlog

```
"Tambahin ke backlog: tombol logout gak muncul di mobile.
Status BLOCKED karena nunggu desain dari UI/UX."
```

Claude akan menambahkannya ke `docs/backlog.md`.

### Kerjakan sesuatu → planning ticket

```
"Bikin planning ticket untuk fitur dark mode."
```

Claude akan membuat file `docs/planning/TICKET-001.md` dari template `_template-implementation-plan.md`, lalu mendaftarkannya di `docs/planning/index.md`. Kamu review, approve (status jadi `READY`), lalu Claude eksekusi.

### Fitur selesai → feature doc

```
"Fitur dark mode sudah live. Bikin feature doc-nya."
```

Claude akan menulis doc di `docs/features/dark-mode.md` dan mendaftarkannya di `docs/features/index.md`.

### Keputusan teknis → decision log

```
"Catat di decision log: kita pake JWT instead of session karena ada mobile app."
```

Claude akan menambah entry ke `docs/decision-log.md`.

### Ticket selesai → arsip

Setelah ticket `DONE`, Claude akan memindahkan file-nya ke `docs/planning/Ticket-Implemented/` dan menghapus entrinya dari `docs/planning/index.md`.

---

## Struktur folder

```
.
├── CLAUDE.md                           # Entry point — dibaca Claude setiap sesi
├── README.md                           # File ini
└── docs/
    ├── ai-context.md                   # Mandat & aturan absolut (WAJIB diisi)
    ├── index.md                        # Hub dokumentasi
    ├── backlog.md                      # Ide/bug yang belum jadi ticket
    ├── decision-log.md                 # Keputusan teknis & trade-off
    ├── architecture.md                 # (kamu yang bikin) peta modul/komponen
    ├── data-model.md                   # (kamu yang bikin) struktur data
    ├── features/
    │   ├── index.md                    # Indeks fitur + konvensi penulisan
    │   └── *.md                        # Doc per fitur (terisi seiring waktu)
    └── planning/
        ├── index.md                    # Indeks ticket aktif
        ├── current-session.md          # Progress sesi terakhir
        ├── _template-implementation-plan.md   # Template bikin ticket baru
        └── Ticket-Implemented/         # Arsip ticket yang sudah DONE
```

---

## Prasyarat

Template ini mengasumsikan kamu menggunakan **Claude Code** sebagai AI agent. Tidak ada dependency pada bahasa/framework tertentu — section 1–4 `ai-context.md` kamu sendiri yang menentukan stack.

Kalau belum install Claude Code: [dokumentasi resmi](https://docs.anthropic.com/en/docs/claude-code).
