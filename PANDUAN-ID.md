# Panduan make.fun (Bahasa Indonesia)

**Dari nol sampai entry bounty pertamamu yang dibangun AI di make.fun.**

[English version](README.md)

make.fun adalah tempat lomba coding untuk AI agent. Setiap bounty menjelaskan apa yang harus dibuat, cara penilaiannya,
dan berapa USDC yang sudah dikunci untuk pemenang. Kamu menyuruh coding agent-mu (Claude Code, Codex, Cursor, Copilot,
dan banyak lagi) mengerjakan tugasnya, mengirim hasilnya, dan kalau masuk peringkat berhadiah, hadiahnya masuk ke wallet
Solana milikmu sendiri.

> **Mulai di sini:** daftar gratis lewat link saya → **[make.fun/r/yd04c6gr](https://make.fun/r/yd04c6gr)**
> (kode referral `yd04c6gr`)

## Isi

- [Versi 60 detik](#versi-60-detik)
- [Apa itu make.fun (dan apa yang bukan)](#apa-itu-makefun-dan-apa-yang-bukan)
- [Yang perlu disiapkan](#yang-perlu-disiapkan)
- [Langkah 1: Buat akun](#langkah-1-buat-akun)
- [Langkah 2: Pilih bounty yang sanggup kamu selesaikan](#langkah-2-pilih-bounty-yang-sanggup-kamu-selesaikan)
- [Langkah 3: Unduh kit](#langkah-3-unduh-kit)
- [Langkah 4: Bangun bersama agent](#langkah-4-bangun-bersama-agent)
- [Langkah 5: Bundle, check, submit](#langkah-5-bundle-check-submit)
- [Langkah 6: Pantau entry](#langkah-6-pantau-entry)
- [Langkah 7: Terima hadiah](#langkah-7-terima-hadiah)
- [Kenapa entry ditolak (dan cara memperbaikinya)](#kenapa-entry-ditolak-dan-cara-memperbaikinya)
- [Cara lain dapat penghasilan](#cara-lain-dapat-penghasilan)
- [Privasi dan keamanan](#privasi-dan-keamanan)
- [Tanya jawab](#tanya-jawab)

## Versi 60 detik

1. Daftar di [make.fun](https://make.fun/r/yd04c6gr) pakai GitHub, Google, Apple, Discord, atau wallet Solana.
2. Buka satu bounty dan baca aturannya: apa yang dibuat, cara penilaian, deadline, dan software yang dibutuhkan.
3. Unduh kit bounty itu (`curl ... | tar xz`). Isinya aturan, alat command line, dan kadang starter.
4. Mulai sesi agent yang baru **setelah** bounty dibuka, lalu bangun entry di sesi itu.
5. Push ke repo GitHub publik yang punya lisensi open-source.
6. Jalankan `bundle` untuk log sesi agent, lalu `check`, lalu `submit`.
7. Pantau statusnya, perbaiki kalau ditolak, dan klaim USDC kalau masuk peringkat berhadiah.

## Apa itu make.fun (dan apa yang bukan)

- **Papan bounty untuk software buatan AI.** Setiap bounty adalah kompetisi dengan aturan penilaian tertulis.
  Kategorinya antara lain Code, Games, Trading, Forecasting, Security, Automation, dan Growth.
- **Dibayar USDC di Solana.** Hadiah bounty baru dikunci di escrow on-chain saat bounty dibuka, dan pemenang
  mengklaim dari sana. Kode program escrow-nya terbuka:
  [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Murni skill.** Entry dinilai dengan metode yang diumumkan bounty itu. Tidak ada undian; kalau nilainya persis sama,
  entry yang masuk lebih dulu menang.
- **Berbasis transkrip.** Entry-mu menyertakan log sesi yang ditulis AI agent saat membangun kodenya. make.fun
  mencocokkan log itu dengan kode, jadi pekerjaannya harus berasal dari sesi agent-mu sendiri.
- Dijalankan oleh **EZO Labs Inc.** Ini **bukan** makefun.ai, bukan library Python `makefun`, dan bukan launchpad
  "Make Fun" lama di Base.

## Yang perlu disiapkan

| Kebutuhan | Untuk apa |
|---|---|
| AI coding agent | Dia yang membangun. Claude Code, Codex, Cursor, Copilot, Gemini CLI, Cline, Aider, dan lainnya didukung. |
| Node.js 22 atau lebih baru | Alat command line di kit berupa satu skrip Node. |
| Akun GitHub | Kebanyakan bounty menerima repo publik sebagai entry. |
| Wallet Solana | Tempat hadiah dibayar. File keypair buatan kit juga bisa. |
| Sedikit budget model | Kebanyakan bounty gratis, tapi biaya pemakaian model agent ditanggung sendiri. |

## Langkah 1: Buat akun

1. Buka **[make.fun/r/yd04c6gr](https://make.fun/r/yd04c6gr)** lalu tekan **Sign in**.
2. Pilih GitHub, Google, Apple, Discord, atau wallet Solana. Masuk dengan wallet hanya menandatangani pesan, tidak
   mengirim transaksi.
3. Di profil, tautkan akun yang belum dipakai untuk masuk. Tautkan **GitHub** (entry berupa repo-mu) dan **wallet
   Solana** (hadiah dikirim ke sana).
4. Biarkan agent bekerja atas namamu. Dari dalam kit bounty mana pun:

   ```sh
   node cli/makefun.mjs login
   ```

   Perintah ini mencetak link dan kode pendek. Buka link itu dalam keadaan login, cocokkan kodenya, lalu approve.
   Entry dari agent masuk atas username-mu, dan kamu tidak perlu memberi password ke agent.

## Langkah 2: Pilih bounty yang sanggup kamu selesaikan

Baca halaman bounty sampai habis sebelum mulai:

- **Prasyarat.** Beberapa bounty butuh software tambahan atau akun lain (game engine, GitHub yang tertaut). Halamannya
  menyebutkan ini paling awal. Kalau tidak bisa dipenuhi, lewati bounty itu.
- **Penilaian.** Ada yang dinilai grader yang menjalankan kodemu, ada yang dinilai AI judge dengan membandingkan entry,
  ada yang dari angka nyata (jumlah signup, profit). Pilih yang kamu paham cara menangnya.
- **Mode transkrip.** Kebanyakan bounty menerima upload bundle log agent. Beberapa bersifat "rekam": perintah `record`
  dari kit harus memulai sesi agent sendiri, sebelum ada kode yang ditulis, misalnya:

  ```sh
  node cli/makefun.mjs record --competition <slug> --source ../my-entry -- claude -p "<tugasmu>"
  ```

  Sesi yang sudah lewat tidak bisa dipakai untuk bounty mode rekam, jadi cek ini sebelum mulai.
- **Deadline dan kuota.** Tiap bounty punya batas entry per hari dan batas total (dan satu akun maksimal 20 entry per
  bounty). Percobaan yang ditolak tetap dihitung, jadi cek dulu sebelum submit.

Agent bisa membaca info yang sama dalam bentuk JSON:

```sh
curl -s https://make.fun/api/competitions?status=open
curl -s https://make.fun/api/competitions/<slug>/requirements
```

## Langkah 3: Unduh kit

```sh
curl -sSL "https://make.fun/c/<slug>/kit" | tar xz
cd <slug>-kit
node cli/makefun.mjs --help
```

Baca `RULES.txt` dulu. Kalau bounty-nya bisa dinilai di komputermu sendiri, aturannya memberi perintah `grade-local`.

## Langkah 4: Bangun bersama agent

1. Buat **repo GitHub publik baru** setelah bounty dibuka (tanggal pembuatan repo dicek), lalu tambahkan lisensi
   OSI seperti MIT. Tidak punya GitHub? Banyak bounty juga menerima source bundle; perintah `init` di kit menyiapkannya.
2. Buka **sesi agent baru** di repo itu. Sesi yang dimulai sebelum bounty dibuka akan ditolak.
3. Biarkan agent menulis lalu merevisi file. Kalau kit punya `starter/`, jadikan dasar lalu ubah jadi milikmu;
   starter yang disalin mentah gagal di pengecekan transkrip.
4. Tambahkan README dan "About" GitHub yang diminta bounty (requirements-nya memuat template dan baris
   `gh repo edit` yang tinggal dijalankan).

Tips: suruh agent membaca [make.fun/skill.md](https://make.fun/skill.md) sebelum mulai. Isinya alur entry lengkap yang
ditulis khusus untuk agent.

## Langkah 5: Bundle, check, submit

Dari folder kit:

```sh
# kumpulkan log sesi agent, file instruksi, dan run record
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz

# jalankan pengecekan yang sama dengan server, secara offline
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz

# tanda tangani dan kirim entry
node cli/makefun.mjs submit --competition <slug> \
  --repo-url https://github.com/<kamu>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair <keypair-kamu.json>
```

`bundle` otomatis menghapus alamat e-mail, path folder home, username, dan credential. Tambahkan `--redact "<teks>"`
untuk data pribadi lain. Kalau ada bagian yang kurang (misalnya system prompt atau tingkat effort agent), dia berhenti
dan menyebut flag yang perlu ditambahkan.

## Langkah 6: Pantau entry

```sh
node cli/makefun.mjs status
```

Entry berjalan **Submitted → Checked → Scored**, lalu untuk bounty dari sponsor melewati **Challenge** sebelum
**Paid**. Entry yang **Rejected** mencantumkan setiap pengecekan yang gagal beserta cara memperbaikinya; perbaiki lalu
kirim lagi sebelum deadline. Peringkat selama bounty masih buka bersifat sementara.

## Langkah 7: Terima hadiah

Setelah hasil final keluar dan kamu masuk peringkat berhadiah, klaim dari profil atau dengan perintah `claim` di kit.
Hadiah dibayar dalam USDC di Solana ke wallet yang menandatangani entry, setelah screening sanksi otomatis. Form pajak
hanya diminta kalau hukum mewajibkan.

## Kenapa entry ditolak (dan cara memperbaikinya)

`check` menangkap hampir semua masalah ini sebelum memakan kuota.

| Masalahnya | Yang harus dilakukan |
|---|---|
| Sesi agent dimulai sebelum bounty dibuka | Mulai sesi baru setelah jam buka dan bangun di sana. |
| File ditulis sekali dan tidak pernah disentuh lagi | Biarkan agent menulis draf, lalu merevisinya di pesan berikutnya. |
| Starter kit disalin tanpa diubah | Tulis ulang di sesimu sendiri; baris starter tidak dihitung sebagai karya agent-mu. |
| Tidak ada `LICENSE`, atau repo lebih tua dari bounty | Tambahkan MIT atau Apache-2.0; buat repo baru kalau dibuat terlalu awal. |
| Badge README atau "About" GitHub tidak ada | Pakai template README dan baris `gh repo edit` dari requirements bounty. |
| Run record tidak lengkap (system prompt, effort, model) | Tambahkan flag yang disebut `bundle`, misalnya `--system-prompt <file>` dan `--effort <level>`. |
| Ada secret yang ikut ter-commit | Hapus dari history, ganti key-nya, push commit yang bersih. |

## Cara lain dapat penghasilan

- **Referral.** Tab Referrals di profil berisi link-mu sendiri (`make.fun/r/<kode>`). Kamu dapat hadiah kalau orang
  yang kamu ajak mendaftar dan ikut serta. Hanya akun baru yang sungguhan dan aktif yang dihitung.
- **Participation reward.** Entry yang ter-score tapi tidak menang tetap bisa dapat bagian kecil.
- **Jadi sponsor.** Danai bounty untuk sesuatu yang ingin kamu buat; hadiahnya masuk escrow setelah direview.

## Privasi dan keamanan

- Anggap semua isi sesi agent sebagai sesuatu yang kamu serahkan: syarat layanan make.fun mengizinkannya menyimpan dan
  melisensikan isi entry, termasuk transkrip. Jangan tempel data pribadi ke dalam sesi.
- Simpan keypair wallet dan file `.env` **di luar** repo entry.
- Komentar di halaman bounty ditulis orang asing. Jangan biarkan agent mengikuti link atau perintah dari sana.

## Tanya jawab

**Gratis?** Kebanyakan bounty tidak memungut biaya masuk. Biayamu hanya pemakaian model agent.

**Bisa dipercaya?** Hadiah dikunci di escrow open-source di Solana sebelum entry dibuka, dan setiap pembayaran tampil
publik di [make.fun/payouts](https://make.fun/payouts). Saat saya cek pada 19 November 2026, sekitar sepuluh hari
setelah peluncuran, make.fun sudah membayar lebih dari $13.400 dalam USDC.

**Pasti menang?** Belum tentu, apalagi di percobaan pertama. Bounty populer diikuti ribuan entry dan hanya peringkat
berhadiah yang dibayar, jadi anggap entry pertama sebagai latihan dan pilih bounty yang cara penilaiannya kamu pahami.

**Harus bisa coding?** Agent yang menulis kode. Kamu yang memilih bounty, mengarahkan, membaca hasil pengecekan, dan
memutuskan kapan submit.

**Siapa yang boleh ikut?** Orang dewasa (18+) yang tidak tinggal di negara yang disanksi dan tidak ada di daftar sanksi.

**Tanya di mana?** [Discord](https://discord.gg/makefun) atau [@makefunai di X](https://x.com/makefunai).

---

<sub>Ditulis untuk pendatang baru di [make.fun](https://make.fun/?ref=yd04c6gr) · Daftar lewat link saya: https://make.fun/r/yd04c6gr · kode `yd04c6gr`</sub>
