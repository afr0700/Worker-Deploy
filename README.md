🌙 Cloudflare Worker Auto-Deployment Guide
<p align="center"><b>Dark Theme · Dual Language · 2 Columns · GitHub Compatible</b></p>
<table> <tr> <td width="50%" valign="top"> <h2 style="color:#86c5ff;">🇺🇸 English Version</h2> <h3 style="color:#ffd27f;">🚀 Overview</h3> Automated deployment system for Cloudflare Worker using GitHub Actions. Supports: - Auto route creation - Multi-domain sharding - Timeout-safe deployment <h3 style="color:#ff7f7f;">⚠️ Issue: Cloudflare 504 Timeout</h3> Too many routes in one Worker may trigger:
504 Timeout – Cloudflare API took too long to respond


Two strategies are available to prevent this.

<h3 style="color:#a3ffac;">🔍 Strategy Comparison</h3>
Strategy	Description	Best For
Legacy (Single Worker)	All routes in one Worker	Small projects
Sharded (Multi Worker)	One Worker per domain	Large projects
<h3 style="color:#ff9bf0;">📦 Required Files</h3>
File	Purpose
worker.js	Worker script
customdomain.txt	Subdomain prefixes
main_domains.txt	Domain list
[Deploy Injektor].yml	Legacy workflow
deploy_chunked.yml	Sharded workflow
<h3 style="color:#ffd27f;">🧰 Legacy Mode</h3> **Workflow:** `[Deploy Injektor].yml`

Inputs:

worker_name

main_domain

Cloudflare API credentials

Flow:

Load main domain

Read prefixes

Build route list

Deploy one Worker

<h3 style="color:#a3ffac;">🧩 Sharded Mode</h3> **Workflow:** `deploy_chunked.yml`

Inputs:

Cloudflare API token

Cloudflare account ID

Flow:

One Worker per domain

Auto-named Worker

Build routes automatically

Deploy sequentially

20s cooldown

<h3 style="color:#fad08c;">▶️ Run</h3> 1. Open GitHub Actions 2. Select workflow 3. Enter credentials 4. Deploy 🎉 </td> <td width="50%" valign="top" style="border-left:1px solid #333; padding-left:15px;"> <h2 style="color:#86c5ff;">🇮🇩 Versi Indonesia</h2> <h3 style="color:#ffd27f;">🚀 Ringkasan</h3> Sistem deployment otomatis untuk Cloudflare Worker menggunakan GitHub Actions. Mendukung: - Pembuatan rute otomatis - Multi-domain sharding - Anti timeout <h3 style="color:#ff7f7f;">⚠️ Masalah: Cloudflare 504 Timeout</h3> Jika terlalu banyak rute digabung, Cloudflare memunculkan:
504 Timeout – API Cloudflare terlambat merespons


Ada dua metode deployment sebagai solusi.

<h3 style="color:#a3ffac;">🔍 Perbandingan Strategi</h3>
Strategi	Penjelasan	Cocok Untuk
Legacy (Single Worker)	Semua rute digabung	Proyek kecil
Sharded (Multi Worker)	1 domain = 1 Worker	Proyek besar
<h3 style="color:#ff9bf0;">📦 File yang Dibutuhkan</h3>
File	Fungsi
worker.js	Script Worker
customdomain.txt	Prefix subdomain
main_domains.txt	Daftar domain
[Deploy Injektor].yml	Workflow Legacy
deploy_chunked.yml	Workflow Sharded
<h3 style="color:#ffd27f;">🧰 Mode Legacy</h3> **Workflow:** `[Deploy Injektor].yml`

Input:

worker_name

main_domain

API credentials

Alur:

Membaca domain utama

Memuat prefix

Menggabungkan rute

Deploy satu Worker

<h3 style="color:#a3ffac;">🧩 Mode Sharded</h3> **Workflow:** `deploy_chunked.yml`

Input:

API token

Account ID Cloudflare

Alur:

Tiap domain → Worker unik

Nama Worker otomatis

Rute otomatis

Deploy satu per satu

Jeda 20 detik

<h3 style="color:#fad08c;">▶️ Jalankan</h3> 1. Masuk GitHub Actions 2. Pilih workflow 3. Isi kredensial 4. Deploy otomatis 🎉 </td> </tr> </table>
