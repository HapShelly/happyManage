<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ProManage – PO & APD Management</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --navy: #1B2B4B;
    --navy-light: #243761;
    --steel: #4A6FA5;
    --steel-light: #6B8FC4;
    --mint: #E8F4F1;
    --mint-dark: #C5E4DC;
    --gold: #F0A500;
    --gold-light: #FFF3D0;
    --danger: #E05252;
    --danger-light: #FDEAEA;
    --success: #2ECC71;
    --success-light: #E9FAF0;
    --text: #1A1F36;
    --text-muted: #6B7080;
    --border: #E4E8F0;
    --bg: #F5F7FC;
    --white: #FFFFFF;
    --sidebar-w: 260px;
    --radius: 12px;
    --radius-sm: 8px;
    --shadow: 0 2px 12px rgba(27,43,75,0.08);
    --shadow-md: 0 4px 24px rgba(27,43,75,0.12);
  }

  body {
    font-family: 'Inter', sans-serif;
    background: var(--bg);
    color: var(--text);
    display: flex;
    min-height: 100vh;
    font-size: 14px;
  }

  /* ── SIDEBAR ── */
  .sidebar {
    width: var(--sidebar-w);
    background: var(--navy);
    min-height: 100vh;
    position: fixed;
    top: 0; left: 0;
    display: flex;
    flex-direction: column;
    z-index: 100;
    transition: transform .3s;
  }

  .sidebar-brand {
    padding: 24px 20px 20px;
    border-bottom: 1px solid rgba(255,255,255,0.08);
  }
  .brand-logo {
    display: flex;
    align-items: center;
    gap: 10px;
    text-decoration: none;
  }
  .brand-icon {
    width: 38px; height: 38px;
    background: var(--gold);
    border-radius: 10px;
    display: flex; align-items: center; justify-content: center;
    font-size: 18px;
    flex-shrink: 0;
  }
  .brand-text { color: var(--white); }
  .brand-text strong { display: block; font-size: 15px; font-weight: 700; }
  .brand-text span { font-size: 11px; color: rgba(255,255,255,0.5); font-weight: 400; }

  .sidebar-nav { flex: 1; padding: 16px 12px; overflow-y: auto; }
  .nav-label {
    font-size: 10px; font-weight: 600; letter-spacing: 1.2px;
    color: rgba(255,255,255,0.35);
    text-transform: uppercase;
    padding: 0 8px;
    margin: 18px 0 6px;
  }
  .nav-label:first-child { margin-top: 0; }

  .nav-item {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 10px 12px;
    border-radius: var(--radius-sm);
    color: rgba(255,255,255,0.65);
    cursor: pointer;
    font-size: 13.5px;
    font-weight: 500;
    transition: all .18s;
    position: relative;
    user-select: none;
  }
  .nav-item:hover { background: rgba(255,255,255,0.07); color: var(--white); }
  .nav-item.active {
    background: var(--steel);
    color: var(--white);
    box-shadow: 0 2px 8px rgba(74,111,165,0.35);
  }
  .nav-icon { font-size: 16px; width: 20px; text-align: center; flex-shrink: 0; }

  .sidebar-footer {
    padding: 16px 20px;
    border-top: 1px solid rgba(255,255,255,0.08);
    color: rgba(255,255,255,0.45);
    font-size: 11.5px;
  }

  /* ── MAIN ── */
  .main {
    margin-left: var(--sidebar-w);
    flex: 1;
    display: flex;
    flex-direction: column;
    min-height: 100vh;
  }

  .topbar {
    background: var(--white);
    border-bottom: 1px solid var(--border);
    padding: 0 28px;
    height: 60px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    position: sticky;
    top: 0;
    z-index: 50;
  }
  .topbar-title { font-size: 16px; font-weight: 700; color: var(--navy); }
  .topbar-actions { display: flex; align-items: center; gap: 12px; }
  .topbar-date { font-size: 12px; color: var(--text-muted); }

  .content { padding: 28px; flex: 1; }

  /* ── CARDS & GRID ── */
  .grid-4 { display: grid; grid-template-columns: repeat(4, 1fr); gap: 16px; margin-bottom: 24px; }
  .grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-bottom: 24px; }
  .grid-3 { display: grid; grid-template-columns: repeat(3, 1fr); gap: 16px; margin-bottom: 24px; }

  .card {
    background: var(--white);
    border-radius: var(--radius);
    box-shadow: var(--shadow);
    border: 1px solid var(--border);
  }
  .card-body { padding: 20px; }
  .card-header {
    padding: 16px 20px;
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .card-title { font-size: 14px; font-weight: 700; color: var(--navy); }
  .card-subtitle { font-size: 12px; color: var(--text-muted); margin-top: 2px; }

  /* ── STAT CARDS ── */
  .stat-card {
    background: var(--white);
    border-radius: var(--radius);
    padding: 20px;
    box-shadow: var(--shadow);
    border: 1px solid var(--border);
    position: relative;
    overflow: hidden;
  }
  .stat-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 3px;
  }
  .stat-card.blue::before { background: var(--steel); }
  .stat-card.gold::before { background: var(--gold); }
  .stat-card.green::before { background: var(--success); }
  .stat-card.red::before { background: var(--danger); }

  .stat-label { font-size: 11px; font-weight: 600; color: var(--text-muted); text-transform: uppercase; letter-spacing: .6px; }
  .stat-value { font-size: 24px; font-weight: 800; color: var(--navy); margin: 6px 0 4px; line-height: 1; }
  .stat-sub { font-size: 12px; color: var(--text-muted); }
  .stat-icon {
    position: absolute;
    top: 16px; right: 16px;
    font-size: 28px;
    opacity: .12;
  }

  /* ── PROGRESS BAR ── */
  .progress-wrap { margin-top: 10px; }
  .progress-labels { display: flex; justify-content: space-between; font-size: 11px; color: var(--text-muted); margin-bottom: 5px; }
  .progress-track {
    height: 8px;
    background: var(--bg);
    border-radius: 99px;
    overflow: hidden;
  }
  .progress-fill {
    height: 100%;
    border-radius: 99px;
    transition: width .5s ease;
  }
  .progress-fill.safe { background: var(--success); }
  .progress-fill.warn { background: var(--gold); }
  .progress-fill.danger { background: var(--danger); }

  /* ── BADGE ── */
  .badge {
    display: inline-flex;
    align-items: center;
    padding: 3px 10px;
    border-radius: 99px;
    font-size: 11px;
    font-weight: 600;
  }
  .badge-blue { background: #EEF3FB; color: var(--steel); }
  .badge-green { background: var(--success-light); color: #18924E; }
  .badge-gold { background: var(--gold-light); color: #B07A00; }
  .badge-red { background: var(--danger-light); color: var(--danger); }
  .badge-gray { background: var(--bg); color: var(--text-muted); }

  /* ── BUTTONS ── */
  .btn {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    padding: 9px 18px;
    border-radius: var(--radius-sm);
    font-size: 13px;
    font-weight: 600;
    border: none;
    cursor: pointer;
    transition: all .18s;
    text-decoration: none;
    font-family: inherit;
  }
  .btn-primary { background: var(--steel); color: var(--white); }
  .btn-primary:hover { background: var(--navy); }
  .btn-gold { background: var(--gold); color: var(--white); }
  .btn-gold:hover { background: #D4900A; }
  .btn-danger { background: var(--danger); color: var(--white); }
  .btn-danger:hover { background: #C44040; }
  .btn-outline {
    background: transparent;
    border: 1.5px solid var(--border);
    color: var(--text);
  }
  .btn-outline:hover { border-color: var(--steel); color: var(--steel); }
  .btn-sm { padding: 5px 12px; font-size: 12px; }
  .btn-icon { padding: 7px; }

  /* ── TABLE ── */
  .table-wrap { overflow-x: auto; }
  table { width: 100%; border-collapse: collapse; }
  th {
    text-align: left;
    padding: 10px 14px;
    font-size: 11px;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: .6px;
    color: var(--text-muted);
    background: var(--bg);
    border-bottom: 1px solid var(--border);
    white-space: nowrap;
  }
  td {
    padding: 12px 14px;
    border-bottom: 1px solid var(--border);
    font-size: 13px;
    color: var(--text);
    vertical-align: middle;
  }
  tr:last-child td { border-bottom: none; }
  tr:hover td { background: #FAFBFD; }

  /* ── FORM ── */
  .form-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
  .form-group { display: flex; flex-direction: column; gap: 6px; }
  .form-group.full { grid-column: 1 / -1; }
  label { font-size: 12px; font-weight: 600; color: var(--navy); }
  input[type=text], input[type=number], input[type=date], input[type=email],
  select, textarea {
    width: 100%;
    padding: 9px 12px;
    border: 1.5px solid var(--border);
    border-radius: var(--radius-sm);
    font-size: 13px;
    font-family: inherit;
    color: var(--text);
    background: var(--white);
    transition: border-color .18s;
    outline: none;
  }
  input:focus, select:focus, textarea:focus { border-color: var(--steel); }
  textarea { resize: vertical; min-height: 80px; }

  /* ── MODAL ── */
  .modal-overlay {
    display: none;
    position: fixed;
    inset: 0;
    background: rgba(0,0,0,0.45);
    z-index: 200;
    align-items: center;
    justify-content: center;
    backdrop-filter: blur(2px);
  }
  .modal-overlay.show { display: flex; }
  .modal {
    background: var(--white);
    border-radius: var(--radius);
    width: 100%;
    max-width: 580px;
    max-height: 90vh;
    overflow-y: auto;
    box-shadow: var(--shadow-md);
    margin: 16px;
  }
  .modal-header {
    padding: 20px 24px 16px;
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .modal-title { font-size: 16px; font-weight: 700; color: var(--navy); }
  .modal-body { padding: 24px; }
  .modal-footer {
    padding: 16px 24px;
    border-top: 1px solid var(--border);
    display: flex;
    justify-content: flex-end;
    gap: 10px;
  }
  .btn-close {
    background: none;
    border: none;
    font-size: 20px;
    color: var(--text-muted);
    cursor: pointer;
    padding: 0 4px;
    line-height: 1;
  }

  /* ── SECTION PAGES ── */
  .page { display: none; }
  .page.active { display: block; }

  .page-header {
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
    margin-bottom: 24px;
    gap: 12px;
  }
  .page-header h1 { font-size: 22px; font-weight: 800; color: var(--navy); }
  .page-header p { font-size: 13px; color: var(--text-muted); margin-top: 3px; }
  .page-header-actions { display: flex; gap: 10px; flex-shrink: 0; }

  /* ── APD PHOTO CARDS ── */
  .apd-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(180px, 1fr)); gap: 16px; }
  .apd-card {
    background: var(--white);
    border-radius: var(--radius);
    border: 1px solid var(--border);
    box-shadow: var(--shadow);
    overflow: hidden;
    transition: transform .2s, box-shadow .2s;
  }
  .apd-card:hover { transform: translateY(-2px); box-shadow: var(--shadow-md); }
  .apd-photo {
    width: 100%;
    height: 140px;
    object-fit: cover;
    display: block;
    background: var(--bg);
  }
  .apd-photo-placeholder {
    width: 100%;
    height: 140px;
    background: var(--mint);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    color: var(--steel);
    font-size: 36px;
  }
  .apd-photo-placeholder span { font-size: 11px; color: var(--text-muted); margin-top: 6px; }
  .apd-info { padding: 12px 14px; }
  .apd-name { font-size: 13px; font-weight: 700; color: var(--navy); margin-bottom: 4px; }
  .apd-meta { font-size: 11.5px; color: var(--text-muted); }
  .apd-stock {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-top: 8px;
    padding-top: 8px;
    border-top: 1px solid var(--border);
  }
  .apd-stock-val { font-size: 18px; font-weight: 800; color: var(--navy); }
  .apd-stock-label { font-size: 10px; color: var(--text-muted); }

  /* ── ALERT ── */
  .alert {
    padding: 12px 16px;
    border-radius: var(--radius-sm);
    font-size: 13px;
    display: flex;
    align-items: flex-start;
    gap: 10px;
    margin-bottom: 16px;
  }
  .alert-warn { background: var(--gold-light); color: #7A5500; border-left: 4px solid var(--gold); }
  .alert-danger { background: var(--danger-light); color: #8B1F1F; border-left: 4px solid var(--danger); }
  .alert-success { background: var(--success-light); color: #145C35; border-left: 4px solid var(--success); }
  .alert-icon { font-size: 16px; flex-shrink: 0; margin-top: 1px; }

  /* ── PO PROGRESS ── */
  .po-progress-card { padding: 20px; }
  .po-name { font-size: 15px; font-weight: 700; color: var(--navy); margin-bottom: 2px; }
  .po-number { font-size: 12px; color: var(--text-muted); }
  .po-amounts {
    display: flex;
    gap: 20px;
    margin: 12px 0;
  }
  .po-amount-item { }
  .po-amount-label { font-size: 10px; color: var(--text-muted); text-transform: uppercase; letter-spacing: .6px; font-weight: 600; }
  .po-amount-value { font-size: 14px; font-weight: 700; color: var(--navy); margin-top: 2px; }
  .po-amount-value.green { color: var(--success); }
  .po-amount-value.red { color: var(--danger); }
  .po-amount-value.gold { color: var(--gold); }

  /* ── DIVIDER ── */
  .divider { border: none; border-top: 1px solid var(--border); margin: 20px 0; }

  /* ── EMPTY STATE ── */
  .empty-state {
    text-align: center;
    padding: 48px 24px;
    color: var(--text-muted);
  }
  .empty-state-icon { font-size: 48px; margin-bottom: 12px; opacity: .4; }
  .empty-state h3 { font-size: 15px; font-weight: 600; color: var(--text); margin-bottom: 6px; }
  .empty-state p { font-size: 13px; }

  /* ── FILE INPUT ── */
  .file-input-wrap {
    border: 2px dashed var(--border);
    border-radius: var(--radius-sm);
    padding: 24px;
    text-align: center;
    cursor: pointer;
    transition: border-color .18s, background .18s;
  }
  .file-input-wrap:hover { border-color: var(--steel); background: var(--mint); }
  .file-input-wrap input[type=file] { display: none; }
  .file-input-icon { font-size: 28px; color: var(--steel-light); margin-bottom: 8px; }
  .file-input-text { font-size: 12px; color: var(--text-muted); }
  .file-preview {
    width: 100%;
    height: 160px;
    object-fit: cover;
    border-radius: var(--radius-sm);
    margin-top: 10px;
    display: none;
  }

  /* ── RESPONSIVE ── */
  @media (max-width: 900px) {
    .sidebar { transform: translateX(-100%); }
    .sidebar.open { transform: translateX(0); }
    .main { margin-left: 0; }
    .grid-4 { grid-template-columns: 1fr 1fr; }
    .grid-2 { grid-template-columns: 1fr; }
    .form-grid { grid-template-columns: 1fr; }
  }
  @media (max-width: 600px) {
    .grid-4 { grid-template-columns: 1fr; }
    .grid-3 { grid-template-columns: 1fr 1fr; }
    .content { padding: 16px; }
  }

  .tag-new { font-size: 9px; background: var(--gold); color: white; border-radius: 4px; padding: 1px 5px; font-weight: 700; letter-spacing: .5px; vertical-align: middle; margin-left: 4px; }
  .text-right { text-align: right; }
  .mt-16 { margin-top: 16px; }
  .mb-16 { margin-bottom: 16px; }
  .flex-between { display: flex; align-items: center; justify-content: space-between; }
  .flex-gap { display: flex; align-items: center; gap: 8px; }
  .full-w { grid-column: 1 / -1; }
</style>
</head>
<body>

<!-- SIDEBAR -->
<nav class="sidebar" id="sidebar">
  <div class="sidebar-brand">
    <a class="brand-logo" href="#">
      <div class="brand-icon">📋</div>
      <div class="brand-text">
        <strong>ProManage</strong>
        <span>PO & APD System</span>
      </div>
    </a>
  </div>
  <div class="sidebar-nav">
    <div class="nav-label">Utama</div>
    <div class="nav-item active" onclick="showPage('dashboard', this)">
      <span class="nav-icon">🏠</span> Dashboard
    </div>

    <div class="nav-label">Purchase Order</div>
    <div class="nav-item" onclick="showPage('po-list', this)">
      <span class="nav-icon">📄</span> Daftar PO
    </div>
    <div class="nav-item" onclick="showPage('po-tagihan', this)">
      <span class="nav-icon">🧾</span> Tagihan PO
    </div>

    <div class="nav-label">JCN</div>
    <div class="nav-item" onclick="showPage('jcn-master', this)">
      <span class="nav-icon">🔖</span> No. JCN
    </div>

    <div class="nav-label">APD Management</div>
    <div class="nav-item" onclick="showPage('apd-master', this)">
      <span class="nav-icon">🦺</span> Master Data APD
    </div>
    <div class="nav-item" onclick="showPage('apd-stok', this)">
      <span class="nav-icon">📦</span> Stok APD
    </div>
    <div class="nav-item" onclick="showPage('apd-rencana', this)">
      <span class="nav-icon">📝</span> Rencana Pembelian
    </div>
    <div class="nav-item" onclick="showPage('apd-terima', this)">
      <span class="nav-icon">✅</span> Terima Barang
    </div>
  </div>
  <div class="sidebar-footer">
    ProManage v1.0 &nbsp;·&nbsp; © 2025
  </div>
</nav>

<!-- MAIN -->
<div class="main">
  <header class="topbar">
    <div class="topbar-title" id="topbar-title">Dashboard</div>
    <div class="topbar-actions">
      <span class="topbar-date" id="topbar-date"></span>
    </div>
  </header>

  <div class="content">

    <!-- ════════════════════════════════ DASHBOARD ════════════════════════════════ -->
    <div id="page-dashboard" class="page active">
      <div class="page-header">
        <div>
          <h1>Dashboard</h1>
          <p>Ringkasan Purchase Order dan stok APD Anda</p>
        </div>
      </div>

      <!-- STAT CARDS -->
      <div class="grid-4" id="dash-stats"></div>

      <!-- ALERT AREA -->
      <div id="dash-alerts"></div>

      <!-- PO OVERVIEW + STOK LOW -->
      <div class="grid-2">
        <div class="card">
          <div class="card-header">
            <div>
              <div class="card-title">Monitor PO Aktif</div>
              <div class="card-subtitle">Progres tagihan vs nilai PO</div>
            </div>
          </div>
          <div id="dash-po-list" class="card-body"></div>
        </div>
        <div class="card">
          <div class="card-header">
            <div>
              <div class="card-title">Stok APD Rendah</div>
              <div class="card-subtitle">Item yang perlu segera dibeli</div>
            </div>
          </div>
          <div id="dash-stok-rendah" class="card-body"></div>
        </div>
      </div>
    </div>

    <!-- ════════════════════════════════ PO LIST ════════════════════════════════ -->
    <div id="page-po-list" class="page">
      <div class="page-header">
        <div>
          <h1>Daftar Purchase Order</h1>
          <p>Kelola semua PO yang sedang berjalan</p>
        </div>
        <div class="page-header-actions">
          <button class="btn btn-primary" onclick="openModal('modal-add-po')">＋ Tambah PO</button>
        </div>
      </div>
      <div class="card">
        <div class="card-body table-wrap">
          <table id="tbl-po">
            <thead>
              <tr>
                <th>No. PO</th>
                <th>Nama / Deskripsi</th>
                <th>Nilai PO</th>
                <th>Total Ditagihkan</th>
                <th>Sisa</th>
                <th>% Terpakai</th>
                <th>Status</th>
                <th>Aksi</th>
              </tr>
            </thead>
            <tbody id="tbl-po-body"></tbody>
          </table>
        </div>
      </div>
    </div>

    <!-- ════════════════════════════════ TAGIHAN ════════════════════════════════ -->
    <div id="page-po-tagihan" class="page">
      <div class="page-header">
        <div>
          <h1>Tagihan PO</h1>
          <p>Input tagihan bulanan per PO</p>
        </div>
        <div class="page-header-actions">
          <button class="btn btn-primary" onclick="openModal('modal-add-tagihan')">＋ Input Tagihan</button>
        </div>
      </div>
      <div class="card">
        <div class="card-body table-wrap">
          <table>
            <thead>
              <tr>
                <th>Tanggal</th>
                <th>No. PO</th>
                <th>Nama PO</th>
                <th>Periode</th>
                <th>Nominal Tagihan</th>
                <th>Keterangan</th>
                <th>Status PO</th>
                <th>Aksi</th>
              </tr>
            </thead>
            <tbody id="tbl-tagihan-body"></tbody>
          </table>
        </div>
      </div>
    </div>

    <!-- ════════════════════════════════ JCN MASTER ════════════════════════════════ -->
    <div id="page-jcn-master" class="page">
      <div class="page-header">
        <div>
          <h1>Master Data No. JCN</h1>
          <p>Pencatatan dan pengelolaan nomor Job Completion Notice (JCN)</p>
        </div>
      </div>

      <!-- STAT CARDS JCN -->
      <div class="grid-3" id="jcn-stats" style="margin-bottom:24px"></div>

      <!-- FORM INPUT JCN -->
      <div class="card" style="margin-bottom:24px">
        <div class="card-header">
          <div class="card-title">＋ Tambah No. JCN</div>
        </div>
        <div class="card-body">
          <div style="display:grid;grid-template-columns:160px 200px 1fr 170px auto;gap:12px;align-items:end">
            <div class="form-group" style="margin:0">
              <label>Tanggal *</label>
              <input type="date" id="jcn-date">
            </div>
            <div class="form-group" style="margin:0">
              <label>No. JCN *</label>
              <input type="text" id="jcn-no" placeholder="JCN-2025-001">
            </div>
            <div class="form-group" style="margin:0">
              <label>Uraian Pekerjaan *</label>
              <input type="text" id="jcn-desc" placeholder="Deskripsi pekerjaan...">
            </div>
            <div class="form-group" style="margin:0">
              <label>Status</label>
              <select id="jcn-status">
                <option value="Belum Dipakai">Belum Dipakai</option>
                <option value="Sudah Dipakai">Sudah Dipakai</option>
              </select>
            </div>
            <button class="btn btn-primary" onclick="addJCN()" style="white-space:nowrap">＋ Tambah</button>
          </div>
        </div>
      </div>

      <!-- TABEL JCN -->
      <div class="card">
        <div class="card-header">
          <div class="card-title">Daftar No. JCN</div>
          <div style="display:flex;gap:10px;align-items:center">
            <input type="text" id="jcn-search" placeholder="🔍 Cari no. / uraian..." oninput="renderJCN()" style="width:220px;padding:7px 12px;font-size:13px;border:1.5px solid var(--border);border-radius:var(--radius-sm);font-family:inherit;outline:none" onfocus="this.style.borderColor='var(--steel)'" onblur="this.style.borderColor='var(--border)'">
            <select id="jcn-filter" onchange="renderJCN()" style="padding:7px 32px 7px 12px;border:1.5px solid var(--border);border-radius:var(--radius-sm);font-size:13px;font-family:inherit;outline:none;appearance:none;background:var(--white) url(\"data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='16' height='16' viewBox='0 0 24 24' fill='none' stroke='%236B7080' stroke-width='2'%3E%3Cpath d='M6 9l6 6 6-6'/%3E%3C/svg%3E\") no-repeat right 10px center;cursor:pointer">
              <option value="">Semua Status</option>
              <option value="Belum Dipakai">Belum Dipakai</option>
              <option value="Sudah Dipakai">Sudah Dipakai</option>
            </select>
            <button class="btn btn-outline btn-sm" onclick="exportJCNCSV()">📥 Export CSV</button>
          </div>
        </div>
        <div class="card-body table-wrap" style="padding:0">
          <table>
            <thead>
              <tr>
                <th style="width:40px">No</th>
                <th>Tanggal</th>
                <th>No. JCN</th>
                <th>Uraian Pekerjaan</th>
                <th>Status</th>
                <th style="width:130px">Aksi</th>
              </tr>
            </thead>
            <tbody id="tbl-jcn-body"></tbody>
          </table>
          <div id="jcn-empty" style="display:none;text-align:center;padding:48px 24px;color:var(--text-muted)">
            <div style="font-size:48px;margin-bottom:12px;opacity:.4">🔖</div>
            <h3 style="font-size:15px;font-weight:600;color:var(--text);margin-bottom:6px">Belum ada data JCN</h3>
            <p style="font-size:13px">Tambahkan No. JCN pertama di atas.</p>
          </div>
        </div>
      </div>
    </div>


    <div id="page-apd-master" class="page">
      <div class="page-header">
        <div>
          <h1>Master Data APD</h1>
          <p>Data induk seluruh item APD beserta foto</p>
        </div>
        <div class="page-header-actions">
          <button class="btn btn-primary" onclick="openModal('modal-add-apd')">＋ Tambah APD</button>
        </div>
      </div>
      <div class="apd-grid" id="apd-card-grid"></div>
    </div>

    <!-- ════════════════════════════════ STOK APD ════════════════════════════════ -->
    <div id="page-apd-stok" class="page">
      <div class="page-header">
        <div>
          <h1>Stok APD</h1>
          <p>Monitor jumlah stok seluruh APD</p>
        </div>
        <div class="page-header-actions">
          <button class="btn btn-outline" onclick="showPage('apd-terima', document.querySelector('[onclick*=apd-terima]'))">📥 Terima Barang</button>
          <button class="btn btn-primary" onclick="openModal('modal-adj-stok')">± Adjust Stok</button>
        </div>
      </div>
      <div class="card">
        <div class="card-body table-wrap">
          <table>
            <thead>
              <tr>
                <th>Nama APD</th>
                <th>Kategori</th>
                <th>Satuan</th>
                <th>Stok Saat Ini</th>
                <th>Stok Min</th>
                <th>Status Stok</th>
                <th>Aksi</th>
              </tr>
            </thead>
            <tbody id="tbl-stok-body"></tbody>
          </table>
        </div>
      </div>
    </div>

    <!-- ════════════════════════════════ RENCANA BELI ════════════════════════════════ -->
    <div id="page-apd-rencana" class="page">
      <div class="page-header">
        <div>
          <h1>Rencana Pembelian APD</h1>
          <p>Daftar APD yang akan dibeli bulan depan</p>
        </div>
        <div class="page-header-actions">
          <button class="btn btn-outline" onclick="openModal('modal-roles')">⚙️ Kelola Role</button>
          <button class="btn btn-outline" onclick="exportRencanaPDF()">📄 Export PDF</button>
          <button class="btn btn-primary" onclick="openModal('modal-add-rencana')">＋ Tambah Rencana</button>
        </div>
      </div>
      <div class="card">
        <div class="card-body table-wrap">
          <table>
            <thead>
              <tr>
                <th>Nama APD</th>
                <th>Stok Saat Ini</th>
                <th>Breakdown Role</th>
                <th>Qty Total</th>
                <th>Satuan</th>
                <th>Catatan</th>
                <th>Aksi</th>
              </tr>
            </thead>
            <tbody id="tbl-rencana-body"></tbody>
          </table>
        </div>
        <div class="card-header" style="border-top:1px solid var(--border); border-bottom:none; background:#FAFBFD;">
          <div class="card-title">Total Qty Seluruh Item</div>
          <div style="font-size:18px;font-weight:800;color:var(--navy);" id="total-rencana">0</div>
        </div>
      </div>
    </div>

    <!-- ════════════════════════════════ TERIMA BARANG ════════════════════════════════ -->
    <div id="page-apd-terima" class="page">
      <div class="page-header">
        <div>
          <h1>Terima Barang APD</h1>
          <p>Catat barang yang sudah diterima dan update stok</p>
        </div>
        <div class="page-header-actions">
          <button class="btn btn-primary" onclick="openModal('modal-terima')">＋ Terima Barang</button>
        </div>
      </div>
      <div class="card">
        <div class="card-body table-wrap">
          <table>
            <thead>
              <tr>
                <th>Tgl Terima</th>
                <th>Nama APD</th>
                <th>Qty Diterima</th>
                <th>Satuan</th>
                <th>Aksi</th>
              </tr>
            </thead>
            <tbody id="tbl-terima-body"></tbody>
          </table>
        </div>
      </div>
    </div>

  </div><!-- /content -->
</div><!-- /main -->

<!-- ════════════ MODALS ════════════ -->

<!-- ADD PO -->
<div class="modal-overlay" id="modal-add-po">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title">Tambah Purchase Order</div>
      <button class="btn-close" onclick="closeModal('modal-add-po')">✕</button>
    </div>
    <div class="modal-body">
      <div class="form-grid">
        <div class="form-group">
          <label>Nomor PO *</label>
          <input type="text" id="po-no" placeholder="PO-2025-001">
        </div>
        <div class="form-group">
          <label>Tanggal PO *</label>
          <input type="date" id="po-date">
        </div>
        <div class="form-group full">
          <label>Nama / Deskripsi PO *</label>
          <input type="text" id="po-name" placeholder="Misal: Jasa Keamanan Semester I 2025">
        </div>
        <div class="form-group">
          <label>Nilai Total PO (Rp) *</label>
          <input type="number" id="po-nilai" placeholder="0" min="0">
        </div>
        <div class="form-group">
          <label>Status</label>
          <select id="po-status">
            <option value="Aktif">Aktif</option>
            <option value="Selesai">Selesai</option>
            <option value="Ditangguhkan">Ditangguhkan</option>
          </select>
        </div>
        <div class="form-group full">
          <label>Catatan</label>
          <textarea id="po-catatan" placeholder="Catatan tambahan..."></textarea>
        </div>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeModal('modal-add-po')">Batal</button>
      <button class="btn btn-primary" onclick="savePO()">Simpan PO</button>
    </div>
  </div>
</div>

<!-- ADD TAGIHAN -->
<div class="modal-overlay" id="modal-add-tagihan">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title">Input Tagihan Bulanan</div>
      <button class="btn-close" onclick="closeModal('modal-add-tagihan')">✕</button>
    </div>
    <div class="modal-body">
      <div class="form-grid">
        <div class="form-group full">
          <label>Pilih PO *</label>
          <select id="t-po-id"></select>
        </div>
        <div class="form-group">
          <label>Tanggal Tagihan *</label>
          <input type="date" id="t-tanggal">
        </div>
        <div class="form-group">
          <label>Periode (Bulan/Tahun)</label>
          <input type="text" id="t-periode" placeholder="Januari 2025">
        </div>
        <div class="form-group full">
          <label>Nominal Tagihan (Rp) *</label>
          <input type="number" id="t-nominal" placeholder="0" min="0">
        </div>
        <div class="form-group full">
          <label>Keterangan</label>
          <textarea id="t-ket" placeholder="Keterangan tagihan..."></textarea>
        </div>
      </div>
      <div id="tagihan-preview" style="margin-top:14px;display:none;">
        <hr class="divider" style="margin:0 0 12px;">
        <div style="font-size:12px;font-weight:700;color:var(--text-muted);margin-bottom:8px;">RINGKASAN PO SETELAH TAGIHAN INI</div>
        <div id="tagihan-preview-content"></div>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeModal('modal-add-tagihan')">Batal</button>
      <button class="btn btn-primary" onclick="saveTagihan()">Simpan Tagihan</button>
    </div>
  </div>
</div>

<!-- ADD APD -->
<div class="modal-overlay" id="modal-add-apd">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title" id="modal-apd-title">Tambah Data APD</div>
      <button class="btn-close" onclick="closeModal('modal-add-apd')">✕</button>
    </div>
    <div class="modal-body">
      <div class="form-grid">
        <div class="form-group full">
          <label>Foto APD</label>
          <div class="file-input-wrap" onclick="document.getElementById('apd-foto-input').click()">
            <div class="file-input-icon">📷</div>
            <div class="file-input-text">Klik untuk upload foto APD<br><small>JPG, PNG – maks 5MB</small></div>
            <input type="file" id="apd-foto-input" accept="image/*" onchange="previewApdPhoto(event)">
          </div>
          <img id="apd-foto-preview" class="file-preview" alt="Preview">
        </div>
        <div class="form-group full">
          <label>Nama APD *</label>
          <input type="text" id="apd-nama" placeholder="Misal: Sarung Tangan Nitril">
        </div>
        <div class="form-group">
          <label>Kategori</label>
          <select id="apd-kategori">
            <option>Pelindung Tangan</option>
            <option>Pelindung Kepala</option>
            <option>Pelindung Kaki</option>
            <option>Pelindung Mata</option>
            <option>Pelindung Tubuh</option>
            <option>Pelindung Pernapasan</option>
            <option>Lainnya</option>
          </select>
        </div>
        <div class="form-group">
          <label>Satuan</label>
          <select id="apd-satuan">
            <option>Pasang</option>
            <option>Pcs</option>
            <option>Kotak</option>
            <option>Lusin</option>
            <option>Set</option>
            <option>Buah</option>
          </select>
        </div>
        <div class="form-group">
          <label>Stok Awal</label>
          <input type="number" id="apd-stok" placeholder="0" min="0" value="0">
        </div>
        <div class="form-group">
          <label>Stok Minimum</label>
          <input type="number" id="apd-stok-min" placeholder="5" min="0" value="5">
        </div>
        <div class="form-group full">
          <label>Keterangan / Spesifikasi</label>
          <textarea id="apd-ket" placeholder="Spesifikasi atau catatan..."></textarea>
        </div>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeModal('modal-add-apd')">Batal</button>
      <button class="btn btn-primary" onclick="saveAPD()">Simpan APD</button>
    </div>
  </div>
</div>

<!-- ADJ STOK -->
<div class="modal-overlay" id="modal-adj-stok">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title">Adjust Stok APD</div>
      <button class="btn-close" onclick="closeModal('modal-adj-stok')">✕</button>
    </div>
    <div class="modal-body">
      <div class="form-grid">
        <div class="form-group full">
          <label>Pilih APD *</label>
          <select id="adj-apd-id"></select>
        </div>
        <div class="form-group">
          <label>Tipe Adjust</label>
          <select id="adj-tipe">
            <option value="tambah">Tambah (+)</option>
            <option value="kurang">Kurang (−)</option>
            <option value="set">Set langsung</option>
          </select>
        </div>
        <div class="form-group">
          <label>Jumlah</label>
          <input type="number" id="adj-qty" placeholder="0" min="0">
        </div>
        <div class="form-group full">
          <label>Alasan</label>
          <textarea id="adj-alasan" placeholder="Alasan penyesuaian stok..."></textarea>
        </div>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeModal('modal-adj-stok')">Batal</button>
      <button class="btn btn-primary" onclick="saveAdjStok()">Simpan</button>
    </div>
  </div>
</div>

<!-- ADD RENCANA -->
<div class="modal-overlay" id="modal-add-rencana">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title">Tambah Rencana Pembelian</div>
      <button class="btn-close" onclick="closeModal('modal-add-rencana')">✕</button>
    </div>
    <div class="modal-body">
      <div class="form-grid">
        <div class="form-group full">
          <label>APD *</label>
          <select id="r-apd-id" onchange="fillRencanaStok()"></select>
        </div>
        <div class="form-group">
          <label>Stok Saat Ini</label>
          <input type="number" id="r-stok-now" readonly style="background:var(--bg);">
        </div>
        <div class="form-group full">
          <label>Breakdown Qty per Role *</label>
          <div id="r-role-grid" style="display:grid;grid-template-columns:1fr 1fr;gap:10px;background:var(--bg);padding:12px;border-radius:var(--radius-sm)"></div>
          <div style="display:flex;justify-content:flex-end;margin-top:8px;font-weight:700;color:var(--navy)">Total: <span id="r-qty-total" style="margin-left:6px">0</span></div>
        </div>
        <div class="form-group full">
          <label>Catatan</label>
          <textarea id="r-catatan" placeholder="Catatan..."></textarea>
        </div>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeModal('modal-add-rencana')">Batal</button>
      <button class="btn btn-primary" onclick="saveRencana()">Simpan</button>
    </div>
  </div>
</div>

<!-- KELOLA ROLE -->
<div class="modal-overlay" id="modal-roles">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title">Kelola Daftar Role Pekerja</div>
      <button class="btn-close" onclick="closeModal('modal-roles')">✕</button>
    </div>
    <div class="modal-body">
      <div class="form-group full">
        <label>Daftar Role (satu role per baris)</label>
        <textarea id="roles-textarea" rows="10" placeholder="Fitter Project&#10;Fitter Maintenance&#10;Welder Project&#10;..."></textarea>
        <small style="color:var(--text-muted);display:block;margin-top:6px;">Daftar role ini bersifat baku dan digunakan sebagai kolom breakdown di setiap rencana pembelian & laporan PDF.</small>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeModal('modal-roles')">Batal</button>
      <button class="btn btn-primary" onclick="saveRoles()">Simpan Daftar Role</button>
    </div>
  </div>
</div>

<!-- TERIMA BARANG -->
<div class="modal-overlay" id="modal-terima">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title">Terima Barang APD</div>
      <button class="btn-close" onclick="closeModal('modal-terima')">✕</button>
    </div>
    <div class="modal-body">
      <div class="form-grid">
        <div class="form-group full">
          <label>APD yang Diterima *</label>
          <select id="trm-apd-id"></select>
        </div>
        <div class="form-group">
          <label>Tanggal Terima *</label>
          <input type="date" id="trm-tgl">
        </div>
        <div class="form-group">
          <label>Qty Diterima *</label>
          <input type="number" id="trm-qty" placeholder="0" min="0">
        </div>
        <div class="form-group full">
          <label>Catatan</label>
          <textarea id="trm-catatan" placeholder="Catatan..."></textarea>
        </div>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeModal('modal-terima')">Batal</button>
      <button class="btn btn-primary" onclick="saveTerima()">Simpan & Update Stok</button>
    </div>
  </div>
</div>

<!-- MODAL EDIT JCN -->
<div class="modal-overlay" id="modal-edit-jcn">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title">Edit No. JCN</div>
      <button class="btn-close" onclick="closeModal('modal-edit-jcn')">✕</button>
    </div>
    <div class="modal-body">
      <input type="hidden" id="ejcn-id">
      <div class="form-grid">
        <div class="form-group">
          <label>Tanggal</label>
          <input type="date" id="ejcn-date">
        </div>
        <div class="form-group">
          <label>No. JCN</label>
          <input type="text" id="ejcn-no">
        </div>
        <div class="form-group full">
          <label>Uraian Pekerjaan</label>
          <input type="text" id="ejcn-desc">
        </div>
        <div class="form-group full">
          <label>Status</label>
          <select id="ejcn-status">
            <option value="Belum Dipakai">Belum Dipakai</option>
            <option value="Sudah Dipakai">Sudah Dipakai</option>
          </select>
        </div>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeModal('modal-edit-jcn')">Batal</button>
      <button class="btn btn-primary" onclick="saveEditJCN()">Simpan Perubahan</button>
    </div>
  </div>
</div>


<script>
let db = {
  po: [],
  tagihan: [],
  apd: [],
  rencana: [],
  terima: [],
  jcn: [],
  roles: ['Fitter Project','Fitter Maintenance','Fitter Walkway','Welder Project','Welder Walkway','Welder Maintenance','Helper Walkway','Helper Rotating','Helper Project','Housekeeping']
};

// Load from localStorage
function loadDB() {
  const saved = localStorage.getItem('promanage_db');
  if (saved) {
    try { db = JSON.parse(saved); } catch(e) {}
  }
  // Ensure all arrays exist
  ['po','tagihan','apd','rencana','terima','jcn'].forEach(k => { if(!db[k]) db[k] = []; });
  if (!db.roles || !db.roles.length) {
    db.roles = ['Fitter Project','Fitter Maintenance','Fitter Walkway','Welder Project','Welder Walkway','Welder Maintenance','Helper Walkway','Helper Rotating','Helper Project','Housekeeping'];
  }
}

function saveDB() {
  localStorage.setItem('promanage_db', JSON.stringify(db));
}

function genId() { return Date.now().toString(36) + Math.random().toString(36).slice(2,6); }

// ════════════════ NAVIGATION ════════════════
const pageTitles = {
  'dashboard': 'Dashboard',
  'po-list': 'Daftar Purchase Order',
  'po-tagihan': 'Tagihan PO',
  'apd-master': 'Master Data APD',
  'apd-stok': 'Stok APD',
  'apd-rencana': 'Rencana Pembelian',
  'apd-terima': 'Terima Barang',
  'jcn-master': 'Master Data No. JCN'
};

function showPage(id, el) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
  document.getElementById('page-' + id).classList.add('active');
  if (el) el.classList.add('active');
  document.getElementById('topbar-title').textContent = pageTitles[id] || id;
  renderPage(id);
}

function renderPage(id) {
  if (id === 'dashboard') renderDashboard();
  else if (id === 'po-list') renderPOList();
  else if (id === 'po-tagihan') renderTagihan();
  else if (id === 'apd-master') renderAPDCards();
  else if (id === 'apd-stok') renderStok();
  else if (id === 'apd-rencana') renderRencana();
  else if (id === 'apd-terima') renderTerima();
  else if (id === 'jcn-master') renderJCN();
}

// ════════════════ MODAL ════════════════
function openModal(id) {
  if (id === 'modal-add-tagihan') populateTagihanModal();
  if (id === 'modal-adj-stok') populateAdjModal();
  if (id === 'modal-add-rencana') populateRencanaModal();
  if (id === 'modal-roles') document.getElementById('roles-textarea').value = db.roles.join('\n');
  if (id === 'modal-terima') populateTerimaModal();
  if (id === 'modal-add-apd') resetAPDModal();
  document.getElementById(id).classList.add('show');
}
function closeModal(id) {
  document.getElementById(id).classList.remove('show');
}
document.querySelectorAll('.modal-overlay').forEach(o => {
  o.addEventListener('click', e => { if (e.target === o) o.classList.remove('show'); });
});

// ════════════════ HELPERS ════════════════
function fmtRp(n) {
  return 'Rp ' + (Number(n)||0).toLocaleString('id-ID');
}

function pctClass(pct) {
  if (pct >= 90) return 'danger';
  if (pct >= 70) return 'warn';
  return 'safe';
}

function getTagihanByPO(poId) {
  return db.tagihan.filter(t => t.poId === poId);
}

function getTotalTagihan(poId) {
  return getTagihanByPO(poId).reduce((s, t) => s + (Number(t.nominal)||0), 0);
}

function getPoById(id) { return db.po.find(p => p.id === id); }
function getApdById(id) { return db.apd.find(a => a.id === id); }

// ════════════════ DASHBOARD ════════════════
function renderDashboard() {
  const totalPO = db.po.length;
  const totalNilaiPO = db.po.reduce((s,p) => s + (Number(p.nilai)||0), 0);
  const totalDitagih = db.po.reduce((s,p) => s + getTotalTagihan(p.id), 0);
  const totalSisaPO = totalNilaiPO - totalDitagih;

  document.getElementById('dash-stats').innerHTML = `
    <div class="stat-card blue">
      <div class="stat-icon">📄</div>
      <div class="stat-label">Total PO Aktif</div>
      <div class="stat-value">${db.po.filter(p=>p.status==='Aktif').length}</div>
      <div class="stat-sub">${totalPO} total PO</div>
    </div>
    <div class="stat-card gold">
      <div class="stat-icon">💰</div>
      <div class="stat-label">Nilai Total PO</div>
      <div class="stat-value" style="font-size:18px">${fmtRp(totalNilaiPO)}</div>
      <div class="stat-sub">Semua PO</div>
    </div>
    <div class="stat-card green">
      <div class="stat-icon">🧾</div>
      <div class="stat-label">Total Ditagihkan</div>
      <div class="stat-value" style="font-size:18px">${fmtRp(totalDitagih)}</div>
      <div class="stat-sub">${db.tagihan.length} tagihan</div>
    </div>
    <div class="stat-card ${totalSisaPO < totalNilaiPO * 0.15 ? 'red' : 'blue'}">
      <div class="stat-icon">📊</div>
      <div class="stat-label">Sisa Anggaran PO</div>
      <div class="stat-value" style="font-size:18px;color:${totalSisaPO < totalNilaiPO*0.15 ? 'var(--danger)' : 'var(--navy)'}">${fmtRp(totalSisaPO)}</div>
      <div class="stat-sub">&nbsp;</div>
    </div>
  `;

  // Alerts
  let alertsHtml = '';
  const stokRendah = db.apd.filter(a => a.stok <= a.stokMin);
  if (stokRendah.length > 0) {
    alertsHtml += `<div class="alert alert-warn"><span class="alert-icon">⚠️</span><div><strong>${stokRendah.length} item APD</strong> memiliki stok di bawah minimum – segera rencanakan pembelian.</div></div>`;
  }
  db.po.filter(p => p.status === 'Aktif').forEach(p => {
    const total = getTotalTagihan(p.id);
    const pct = p.nilai > 0 ? (total / p.nilai * 100) : 0;
    if (pct >= 90) alertsHtml += `<div class="alert alert-danger"><span class="alert-icon">🚨</span><div>PO <strong>${p.noPO}</strong> sudah terpakai <strong>${pct.toFixed(1)}%</strong> – hampir habis!</div></div>`;
    else if (pct >= 70) alertsHtml += `<div class="alert alert-warn"><span class="alert-icon">⚠️</span><div>PO <strong>${p.noPO}</strong> sudah terpakai <strong>${pct.toFixed(1)}%</strong>.</div></div>`;
  });
  document.getElementById('dash-alerts').innerHTML = alertsHtml;

  // PO List in dashboard
  let poHtml = '';
  if (db.po.length === 0) {
    poHtml = '<div class="empty-state"><div class="empty-state-icon">📄</div><h3>Belum ada PO</h3><p>Tambahkan PO terlebih dahulu</p></div>';
  } else {
    db.po.filter(p=>p.status==='Aktif').slice(0,5).forEach(p => {
      const total = getTotalTagihan(p.id);
      const sisa = (Number(p.nilai)||0) - total;
      const pct = p.nilai > 0 ? Math.min(100, total / p.nilai * 100) : 0;
      const cls = pctClass(pct);
      poHtml += `
        <div class="po-progress-card" style="border-bottom:1px solid var(--border);padding-bottom:16px;margin-bottom:16px;">
          <div class="po-name">${p.nama}</div>
          <div class="po-number">${p.noPO}</div>
          <div class="po-amounts">
            <div class="po-amount-item"><div class="po-amount-label">Nilai PO</div><div class="po-amount-value">${fmtRp(p.nilai)}</div></div>
            <div class="po-amount-item"><div class="po-amount-label">Ditagihkan</div><div class="po-amount-value gold">${fmtRp(total)}</div></div>
            <div class="po-amount-item"><div class="po-amount-label">Sisa</div><div class="po-amount-value ${sisa < 0 ? 'red' : 'green'}">${fmtRp(sisa)}</div></div>
          </div>
          <div class="progress-wrap">
            <div class="progress-labels"><span>${pct.toFixed(1)}% terpakai</span><span>${fmtRp(sisa)} tersisa</span></div>
            <div class="progress-track"><div class="progress-fill ${cls}" style="width:${pct}%"></div></div>
          </div>
        </div>`;
    });
  }
  document.getElementById('dash-po-list').innerHTML = poHtml || '<div class="empty-state"><div class="empty-state-icon">📄</div><h3>Tidak ada PO aktif</h3></div>';

  // Stok rendah
  let stokHtml = '';
  if (stokRendah.length === 0) {
    stokHtml = '<div class="empty-state"><div class="empty-state-icon">✅</div><h3>Semua stok aman</h3><p>Tidak ada APD di bawah stok minimum</p></div>';
  } else {
    stokRendah.forEach(a => {
      stokHtml += `
        <div style="display:flex;align-items:center;gap:12px;padding:12px 0;border-bottom:1px solid var(--border);">
          ${a.foto ? `<img src="${a.foto}" style="width:40px;height:40px;border-radius:8px;object-fit:cover;">` : '<div style="width:40px;height:40px;border-radius:8px;background:var(--mint);display:flex;align-items:center;justify-content:center;font-size:18px;">🦺</div>'}
          <div style="flex:1">
            <div style="font-weight:600;font-size:13px">${a.nama}</div>
            <div style="font-size:11px;color:var(--text-muted)">${a.kategori}</div>
          </div>
          <div style="text-align:right">
            <div style="font-weight:800;color:var(--danger);font-size:15px">${a.stok}</div>
            <div style="font-size:10px;color:var(--text-muted)">Min: ${a.stokMin}</div>
          </div>
        </div>`;
    });
  }
  document.getElementById('dash-stok-rendah').innerHTML = stokHtml;
}

// ════════════════ PO ════════════════
function savePO() {
  const noPO = document.getElementById('po-no').value.trim();
  const nama = document.getElementById('po-name').value.trim();
  const nilai = Number(document.getElementById('po-nilai').value);
  const date = document.getElementById('po-date').value;
  const status = document.getElementById('po-status').value;
  const catatan = document.getElementById('po-catatan').value;
  if (!noPO || !nama || !nilai) return alert('Mohon isi semua field wajib!');
  db.po.push({ id: genId(), noPO, nama, nilai, date, status, catatan });
  saveDB();
  closeModal('modal-add-po');
  ['po-no','po-name','po-nilai','po-date','po-catatan'].forEach(id => document.getElementById(id).value = '');
  document.getElementById('po-status').value = 'Aktif';
  renderPOList();
}

function deletePO(id) {
  if (!confirm('Hapus PO ini? Semua tagihan terkait juga akan dihapus.')) return;
  db.po = db.po.filter(p => p.id !== id);
  db.tagihan = db.tagihan.filter(t => t.poId !== id);
  saveDB();
  renderPOList();
}

function renderPOList() {
  const tbody = document.getElementById('tbl-po-body');
  if (db.po.length === 0) {
    tbody.innerHTML = `<tr><td colspan="8" style="text-align:center;padding:40px;color:var(--text-muted)">Belum ada PO. Klik "+ Tambah PO" untuk mulai.</td></tr>`;
    return;
  }
  tbody.innerHTML = db.po.map(p => {
    const total = getTotalTagihan(p.id);
    const sisa = (Number(p.nilai)||0) - total;
    const pct = p.nilai > 0 ? Math.min(100, total / p.nilai * 100) : 0;
    const cls = pctClass(pct);
    const statusBadge = p.status === 'Aktif' ? 'badge-green' : p.status === 'Selesai' ? 'badge-blue' : 'badge-gray';
    return `<tr>
      <td><strong>${p.noPO}</strong></td>
      <td>${p.nama}<br><small style="color:var(--text-muted)">${p.date||''}</small></td>
      <td>${fmtRp(p.nilai)}</td>
      <td>${fmtRp(total)}</td>
      <td style="color:${sisa < 0 ? 'var(--danger)' : 'var(--success)'};font-weight:700">${fmtRp(sisa)}</td>
      <td>
        <div style="display:flex;align-items:center;gap:8px;">
          <div class="progress-track" style="flex:1;min-width:70px">
            <div class="progress-fill ${cls}" style="width:${pct}%"></div>
          </div>
          <span style="font-size:11px;font-weight:700;color:var(--text-muted)">${pct.toFixed(0)}%</span>
        </div>
      </td>
      <td><span class="badge ${statusBadge}">${p.status}</span></td>
      <td>
        <div class="flex-gap">
          <button class="btn btn-outline btn-sm" onclick="showTagihanForPO('${p.id}')">🧾 Tagihan</button>
          <button class="btn btn-danger btn-sm" onclick="deletePO('${p.id}')">🗑</button>
        </div>
      </td>
    </tr>`;
  }).join('');
}

function showTagihanForPO(poId) {
  showPage('po-tagihan', document.querySelector('[onclick*=po-tagihan]'));
  setTimeout(() => { document.getElementById('t-po-id').value = poId; }, 100);
}

// ════════════════ TAGIHAN ════════════════
function populateTagihanModal() {
  const sel = document.getElementById('t-po-id');
  sel.innerHTML = db.po.map(p => `<option value="${p.id}">${p.noPO} – ${p.nama}</option>`).join('');
  document.getElementById('t-tanggal').value = new Date().toISOString().split('T')[0];
  updateTagihanPreview();
  sel.onchange = updateTagihanPreview;
  document.getElementById('t-nominal').oninput = updateTagihanPreview;
}

function updateTagihanPreview() {
  const poId = document.getElementById('t-po-id').value;
  const nominal = Number(document.getElementById('t-nominal').value)||0;
  const po = getPoById(poId);
  if (!po || !poId) { document.getElementById('tagihan-preview').style.display = 'none'; return; }
  const totalSudah = getTotalTagihan(poId);
  const totalSetelah = totalSudah + nominal;
  const sisa = po.nilai - totalSetelah;
  const pct = po.nilai > 0 ? Math.min(100, totalSetelah / po.nilai * 100) : 0;
  document.getElementById('tagihan-preview').style.display = 'block';
  document.getElementById('tagihan-preview-content').innerHTML = `
    <div class="po-amounts" style="flex-wrap:wrap">
      <div class="po-amount-item"><div class="po-amount-label">Nilai PO</div><div class="po-amount-value">${fmtRp(po.nilai)}</div></div>
      <div class="po-amount-item"><div class="po-amount-label">Sudah Ditagih</div><div class="po-amount-value gold">${fmtRp(totalSudah)}</div></div>
      <div class="po-amount-item"><div class="po-amount-label">+ Tagihan Ini</div><div class="po-amount-value blue" style="color:var(--steel)">${fmtRp(nominal)}</div></div>
      <div class="po-amount-item"><div class="po-amount-label">Sisa Setelah</div><div class="po-amount-value ${sisa < 0 ? 'red' : 'green'}">${fmtRp(sisa)}</div></div>
    </div>
    <div class="progress-wrap">
      <div class="progress-labels"><span>${pct.toFixed(1)}% dari PO terpakai</span></div>
      <div class="progress-track"><div class="progress-fill ${pctClass(pct)}" style="width:${pct}%"></div></div>
    </div>
    ${pct >= 100 ? '<div class="alert alert-danger" style="margin-top:10px"><span class="alert-icon">🚨</span>Tagihan melebihi nilai PO!</div>' :
      pct >= 90 ? '<div class="alert alert-warn" style="margin-top:10px"><span class="alert-icon">⚠️</span>PO hampir habis (≥90%)!</div>' : ''}
  `;
}

function saveTagihan() {
  const poId = document.getElementById('t-po-id').value;
  const tanggal = document.getElementById('t-tanggal').value;
  const periode = document.getElementById('t-periode').value;
  const nominal = Number(document.getElementById('t-nominal').value);
  const ket = document.getElementById('t-ket').value;
  if (!poId || !tanggal || !nominal) return alert('Mohon isi semua field wajib!');
  const po = getPoById(poId);
  db.tagihan.push({ id: genId(), poId, noPO: po?.noPO, namaPO: po?.nama, tanggal, periode, nominal, ket });
  saveDB();
  closeModal('modal-add-tagihan');
  ['t-periode','t-nominal','t-ket'].forEach(id => document.getElementById(id).value = '');
  renderTagihan();
}

function deleteTagihan(id) {
  if (!confirm('Hapus tagihan ini?')) return;
  db.tagihan = db.tagihan.filter(t => t.id !== id);
  saveDB();
  renderTagihan();
}

function renderTagihan() {
  const tbody = document.getElementById('tbl-tagihan-body');
  if (db.tagihan.length === 0) {
    tbody.innerHTML = `<tr><td colspan="8" style="text-align:center;padding:40px;color:var(--text-muted)">Belum ada tagihan.</td></tr>`;
    return;
  }
  const sorted = [...db.tagihan].sort((a,b) => b.tanggal > a.tanggal ? 1 : -1);
  tbody.innerHTML = sorted.map(t => {
    const po = getPoById(t.poId);
    const total = po ? getTotalTagihan(t.poId) : 0;
    const pct = po && po.nilai > 0 ? (total / po.nilai * 100) : 0;
    const badgeClass = pct >= 90 ? 'badge-red' : pct >= 70 ? 'badge-gold' : 'badge-green';
    return `<tr>
      <td>${t.tanggal}</td>
      <td><strong>${t.noPO||'-'}</strong></td>
      <td>${t.namaPO||'-'}</td>
      <td>${t.periode||'-'}</td>
      <td><strong>${fmtRp(t.nominal)}</strong></td>
      <td style="max-width:160px;word-break:break-word">${t.ket||'-'}</td>
      <td><span class="badge ${badgeClass}">${pct.toFixed(0)}% terpakai</span></td>
      <td><button class="btn btn-danger btn-sm" onclick="deleteTagihan('${t.id}')">🗑</button></td>
    </tr>`;
  }).join('');
}

// ════════════════ APD MASTER ════════════════
let editingApdId = null;
let apdFotoData = null;

function resetAPDModal() {
  editingApdId = null;
  apdFotoData = null;
  document.getElementById('modal-apd-title').textContent = 'Tambah Data APD';
  ['apd-nama','apd-stok','apd-stok-min','apd-ket'].forEach(id => document.getElementById(id).value = id==='apd-stok' ? '0' : id==='apd-stok-min' ? '5' : '');
  document.getElementById('apd-foto-preview').style.display = 'none';
  document.getElementById('apd-foto-preview').src = '';
  document.getElementById('apd-foto-input').value = '';
}

function previewApdPhoto(e) {
  const file = e.target.files[0];
  if (!file) return;
  const reader = new FileReader();
  reader.onload = ev => {
    apdFotoData = ev.target.result;
    const img = document.getElementById('apd-foto-preview');
    img.src = apdFotoData;
    img.style.display = 'block';
  };
  reader.readAsDataURL(file);
}

function saveAPD() {
  const nama = document.getElementById('apd-nama').value.trim();
  if (!nama) return alert('Nama APD wajib diisi!');
  const obj = {
    id: editingApdId || genId(),
    nama,
    kategori: document.getElementById('apd-kategori').value,
    satuan: document.getElementById('apd-satuan').value,
    stok: Number(document.getElementById('apd-stok').value)||0,
    stokMin: Number(document.getElementById('apd-stok-min').value)||5,
    ket: document.getElementById('apd-ket').value,
    foto: apdFotoData || (editingApdId ? getApdById(editingApdId)?.foto : null)
  };
  if (editingApdId) {
    const idx = db.apd.findIndex(a => a.id === editingApdId);
    if (idx >= 0) db.apd[idx] = obj;
  } else {
    db.apd.push(obj);
  }
  saveDB();
  closeModal('modal-add-apd');
  renderAPDCards();
}

function editAPD(id) {
  const a = getApdById(id);
  if (!a) return;
  editingApdId = id;
  apdFotoData = null;
  document.getElementById('modal-apd-title').textContent = 'Edit Data APD';
  document.getElementById('apd-nama').value = a.nama;
  document.getElementById('apd-kategori').value = a.kategori;
  document.getElementById('apd-satuan').value = a.satuan;
  document.getElementById('apd-stok').value = a.stok;
  document.getElementById('apd-stok-min').value = a.stokMin;
  document.getElementById('apd-ket').value = a.ket || '';
  const img = document.getElementById('apd-foto-preview');
  if (a.foto) { img.src = a.foto; img.style.display = 'block'; }
  else { img.style.display = 'none'; img.src = ''; }
  document.getElementById('modal-add-apd').classList.add('show');
}

function deleteAPD(id) {
  if (!confirm('Hapus APD ini?')) return;
  db.apd = db.apd.filter(a => a.id !== id);
  saveDB();
  renderAPDCards();
}

function renderAPDCards() {
  const grid = document.getElementById('apd-card-grid');
  if (db.apd.length === 0) {
    grid.innerHTML = `<div class="empty-state" style="grid-column:1/-1"><div class="empty-state-icon">🦺</div><h3>Belum ada data APD</h3><p>Klik "+ Tambah APD" untuk mulai</p></div>`;
    return;
  }
  grid.innerHTML = db.apd.map(a => {
    const stokStatus = a.stok <= 0 ? 'badge-red' : a.stok <= a.stokMin ? 'badge-gold' : 'badge-green';
    const stokLabel = a.stok <= 0 ? 'Habis' : a.stok <= a.stokMin ? 'Rendah' : 'Aman';
    return `<div class="apd-card">
      ${a.foto
        ? `<img class="apd-photo" src="${a.foto}" alt="${a.nama}">`
        : `<div class="apd-photo-placeholder">🦺<span>${a.kategori}</span></div>`}
      <div class="apd-info">
        <div class="apd-name">${a.nama}</div>
        <div class="apd-meta">${a.kategori}</div>
        <div class="apd-stock">
          <div>
            <div class="apd-stock-val">${a.stok} <small style="font-size:11px;font-weight:400;color:var(--text-muted)">${a.satuan}</small></div>
            <div class="apd-stock-label">Stok Saat Ini</div>
          </div>
          <span class="badge ${stokStatus}">${stokLabel}</span>
        </div>
        <div style="display:flex;gap:6px;margin-top:10px">
          <button class="btn btn-outline btn-sm" style="flex:1" onclick="editAPD('${a.id}')">✏️ Edit</button>
          <button class="btn btn-danger btn-sm" onclick="deleteAPD('${a.id}')">🗑</button>
        </div>
      </div>
    </div>`;
  }).join('');
}

// ════════════════ STOK ════════════════
function populateAdjModal() {
  document.getElementById('adj-apd-id').innerHTML = db.apd.map(a => `<option value="${a.id}">${a.nama} (stok: ${a.stok} ${a.satuan})</option>`).join('');
}

function saveAdjStok() {
  const id = document.getElementById('adj-apd-id').value;
  const tipe = document.getElementById('adj-tipe').value;
  const qty = Number(document.getElementById('adj-qty').value)||0;
  const idx = db.apd.findIndex(a => a.id === id);
  if (idx < 0) return;
  if (tipe === 'tambah') db.apd[idx].stok += qty;
  else if (tipe === 'kurang') db.apd[idx].stok = Math.max(0, db.apd[idx].stok - qty);
  else db.apd[idx].stok = qty;
  saveDB();
  closeModal('modal-adj-stok');
  renderStok();
}

function renderStok() {
  const tbody = document.getElementById('tbl-stok-body');
  if (db.apd.length === 0) {
    tbody.innerHTML = `<tr><td colspan="7" style="text-align:center;padding:40px;color:var(--text-muted)">Belum ada data APD.</td></tr>`;
    return;
  }
  tbody.innerHTML = db.apd.map(a => {
    const stokStatus = a.stok <= 0 ? 'badge-red' : a.stok <= a.stokMin ? 'badge-gold' : 'badge-green';
    const stokLabel = a.stok <= 0 ? 'Habis' : a.stok <= a.stokMin ? 'Di bawah minimum' : 'Aman';
    return `<tr>
      <td>
        <div style="display:flex;align-items:center;gap:10px">
          ${a.foto ? `<img src="${a.foto}" style="width:36px;height:36px;border-radius:8px;object-fit:cover">` : '<div style="width:36px;height:36px;border-radius:8px;background:var(--mint);display:flex;align-items:center;justify-content:center;font-size:16px">🦺</div>'}
          <strong>${a.nama}</strong>
        </div>
      </td>
      <td>${a.kategori}</td>
      <td>${a.satuan}</td>
      <td><strong style="font-size:16px">${a.stok}</strong></td>
      <td>${a.stokMin}</td>
      <td><span class="badge ${stokStatus}">${stokLabel}</span></td>
      <td>
        <button class="btn btn-outline btn-sm" onclick="editAPD('${a.id}');closeModal('modal-adj-stok')">✏️ Edit APD</button>
      </td>
    </tr>`;
  }).join('');
}

// ════════════════ ROLES ════════════════
function saveRoles() {
  const lines = document.getElementById('roles-textarea').value
    .split('\n').map(s => s.trim()).filter(Boolean);
  if (!lines.length) return alert('Daftar role tidak boleh kosong!');
  db.roles = lines;
  saveDB();
  closeModal('modal-roles');
  renderRencana();
}

// ════════════════ RENCANA ════════════════
function populateRencanaModal() {
  document.getElementById('r-apd-id').innerHTML = db.apd.map(a => `<option value="${a.id}">${a.nama}</option>`).join('');
  document.getElementById('r-role-grid').innerHTML = db.roles.map(role => `
    <div class="form-group" style="margin:0">
      <label style="font-size:11.5px">${role}</label>
      <input type="number" class="r-role-qty" data-role="${role}" placeholder="0" min="0" value="0" oninput="updateRencanaTotal()">
    </div>`).join('');
  fillRencanaStok();
  updateRencanaTotal();
}

function updateRencanaTotal() {
  const total = [...document.querySelectorAll('.r-role-qty')]
    .reduce((sum, inp) => sum + (Number(inp.value) || 0), 0);
  document.getElementById('r-qty-total').textContent = total;
  return total;
}

function fillRencanaStok() {
  const id = document.getElementById('r-apd-id').value;
  const a = getApdById(id);
  document.getElementById('r-stok-now').value = a ? a.stok : 0;
}

function saveRencana() {
  const apdId = document.getElementById('r-apd-id').value;
  const breakdown = {};
  document.querySelectorAll('.r-role-qty').forEach(inp => {
    const v = Number(inp.value) || 0;
    if (v > 0) breakdown[inp.dataset.role] = v;
  });
  const qty = updateRencanaTotal();
  const catatan = document.getElementById('r-catatan').value;
  if (!apdId || qty <= 0) return alert('Mohon isi APD dan jumlah breakdown role!');
  const a = getApdById(apdId);
  db.rencana.push({ id: genId(), apdId, namaApd: a?.nama, satuan: a?.satuan, stokNow: a?.stok||0, qty, breakdown, catatan });
  saveDB();
  closeModal('modal-add-rencana');
  document.getElementById('r-catatan').value = '';
  renderRencana();
}

function deleteRencana(id) {
  db.rencana = db.rencana.filter(r => r.id !== id);
  saveDB();
  renderRencana();
}

function renderRencana() {
  const tbody = document.getElementById('tbl-rencana-body');
  let totalQty = 0;
  if (db.rencana.length === 0) {
    tbody.innerHTML = `<tr><td colspan="7" style="text-align:center;padding:40px;color:var(--text-muted)">Belum ada rencana pembelian.</td></tr>`;
    document.getElementById('total-rencana').textContent = '0';
    return;
  }
  tbody.innerHTML = db.rencana.map(r => {
    totalQty += Number(r.qty) || 0;
    const breakdownHtml = r.breakdown && Object.keys(r.breakdown).length
      ? `<ul style="margin:0;padding-left:16px;font-size:12px;color:var(--text-muted)">${Object.entries(r.breakdown).map(([role,q]) => `<li>${role} (${q})</li>`).join('')}</ul>`
      : '-';
    return `<tr>
      <td><strong>${r.namaApd}</strong></td>
      <td>${r.stokNow} ${r.satuan}</td>
      <td style="max-width:220px">${breakdownHtml}</td>
      <td><strong>${r.qty}</strong></td>
      <td>${r.satuan}</td>
      <td style="max-width:160px;word-break:break-word">${r.catatan||'-'}</td>
      <td><button class="btn btn-danger btn-sm" onclick="deleteRencana('${r.id}')">🗑</button></td>
    </tr>`;
  }).join('');
  document.getElementById('total-rencana').textContent = totalQty;
}

// ════════════════ EXPORT PDF RENCANA ════════════════
function exportRencanaPDF() {
  if (!db.rencana.length) return alert('Belum ada rencana pembelian untuk diexport!');
  const { jsPDF } = window.jspdf;
  const doc = new jsPDF({ unit: 'pt', format: 'a4' });
  const pageW = doc.internal.pageSize.getWidth();
  const marginX = 40;
  let y = 50;

  doc.setFont('helvetica','bold'); doc.setFontSize(16);
  doc.text('Laporan Rencana Pembelian APD', marginX, y);
  doc.setFont('helvetica','normal'); doc.setFontSize(10); doc.setTextColor(100);
  y += 16;
  doc.text(new Date().toLocaleDateString('id-ID', { weekday:'long', year:'numeric', month:'long', day:'numeric' }), marginX, y);
  doc.setTextColor(0);
  y += 20;
  doc.setDrawColor(220); doc.line(marginX, y, pageW - marginX, y);
  y += 20;

  const imgSize = 70;
  const textX = marginX + imgSize + 24;
  const totalColX = pageW - marginX - 90;
  let grandTotal = 0;

  db.rencana.forEach((r, idx) => {
    const breakdown = r.breakdown || {};
    const lines = Object.entries(breakdown);
    const blockHeight = Math.max(imgSize, 18 + lines.length * 14 + 10);

    if (y + blockHeight > doc.internal.pageSize.getHeight() - 60) {
      doc.addPage();
      y = 50;
    }

    const apd = getApdById(r.apdId);
    if (apd && apd.foto) {
      try { doc.addImage(apd.foto, 'JPEG', marginX, y, imgSize, imgSize); }
      catch(e) {
        try { doc.addImage(apd.foto, 'PNG', marginX, y, imgSize, imgSize); } catch(e2) {}
      }
    } else {
      doc.setDrawColor(220); doc.setFillColor(245,247,252);
      doc.rect(marginX, y, imgSize, imgSize, 'FD');
    }

    doc.setFont('helvetica','bold'); doc.setFontSize(11);
    doc.text(r.namaApd || '', textX, y + 12);

    doc.setFont('helvetica','normal'); doc.setFontSize(10);
    let ly = y + 30;
    lines.forEach(([role, q]) => {
      doc.text(`- ${role} (${q})`, textX, ly);
      ly += 14;
    });

    doc.setFont('helvetica','bold');
    doc.text(`Total: ${r.qty}`, totalColX, y + 30);
    grandTotal += r.qty;

    y += blockHeight + 16;
    if (idx < db.rencana.length - 1) {
      doc.setDrawColor(235); doc.line(marginX, y - 8, pageW - marginX, y - 8);
    }
  });

  if (y > doc.internal.pageSize.getHeight() - 60) { doc.addPage(); y = 50; }
  doc.setDrawColor(0); doc.setLineWidth(1);
  doc.line(marginX, y, pageW - marginX, y);
  y += 22;
  doc.setFont('helvetica','bold'); doc.setFontSize(13);
  doc.text('Grand Total', marginX, y);
  doc.text(String(grandTotal), totalColX, y);

  doc.save(`Rencana-Pembelian-APD-${new Date().toISOString().split('T')[0]}.pdf`);
}

// ════════════════ TERIMA BARANG ════════════════
function populateTerimaModal() {
  document.getElementById('trm-apd-id').innerHTML = db.apd.map(a => `<option value="${a.id}">${a.nama} (stok: ${a.stok})</option>`).join('');
  document.getElementById('trm-tgl').value = new Date().toISOString().split('T')[0];
}

function saveTerima() {
  const apdId = document.getElementById('trm-apd-id').value;
  const tgl = document.getElementById('trm-tgl').value;
  const qty = Number(document.getElementById('trm-qty').value)||0;
  const catatan = document.getElementById('trm-catatan').value;
  if (!apdId || qty <= 0) return alert('Mohon isi APD dan jumlah!');
  const a = getApdById(apdId);
  db.terima.push({ id: genId(), apdId, namaApd: a?.nama, satuan: a?.satuan, tgl, qty, catatan });
  // Update stok
  const idx = db.apd.findIndex(x => x.id === apdId);
  if (idx >= 0) db.apd[idx].stok += qty;
  saveDB();
  closeModal('modal-terima');
  ['trm-qty','trm-catatan'].forEach(id => document.getElementById(id).value = '');
  renderTerima();
}

function renderTerima() {
  const tbody = document.getElementById('tbl-terima-body');
  if (db.terima.length === 0) {
    tbody.innerHTML = `<tr><td colspan="5" style="text-align:center;padding:40px;color:var(--text-muted)">Belum ada penerimaan barang.</td></tr>`;
    return;
  }
  const sorted = [...db.terima].sort((a,b) => b.tgl > a.tgl ? 1 : -1);
  tbody.innerHTML = sorted.map(t => `<tr>
    <td>${t.tgl}</td>
    <td><strong>${t.namaApd}</strong></td>
    <td><strong style="color:var(--success)">${t.qty}</strong></td>
    <td>${t.satuan}</td>
    <td><button class="btn btn-danger btn-sm" onclick="deleteTerima('${t.id}')">🗑</button></td>
  </tr>`).join('');
}

function deleteTerima(id) {
  if (!confirm('Hapus record terima barang ini? Stok tidak akan dikurangi kembali.')) return;
  db.terima = db.terima.filter(t => t.id !== id);
  saveDB();
  renderTerima();
}

// ════════════════ JCN ════════════════
function fmtDate(str) {
  if (!str) return '-';
  const [y,m,d] = str.split('-');
  const months = ['Jan','Feb','Mar','Apr','Mei','Jun','Jul','Agu','Sep','Okt','Nov','Des'];
  return `${parseInt(d)} ${months[parseInt(m)-1]} ${y}`;
}

function addJCN() {
  const date   = document.getElementById('jcn-date').value;
  const no     = document.getElementById('jcn-no').value.trim();
  const desc   = document.getElementById('jcn-desc').value.trim();
  const status = document.getElementById('jcn-status').value;
  if (!date || !no || !desc) { alert('⚠️ Tanggal, No. JCN, dan Uraian wajib diisi.'); return; }
  db.jcn.unshift({ id: genId(), date, no, desc, status });
  saveDB();
  document.getElementById('jcn-no').value = '';
  document.getElementById('jcn-desc').value = '';
  document.getElementById('jcn-status').value = 'Belum Dipakai';
  document.getElementById('jcn-date').valueAsDate = new Date();
  renderJCN();
}

function deleteJCN(id) {
  if (!confirm('Hapus No. JCN ini?')) return;
  db.jcn = db.jcn.filter(j => j.id !== id);
  saveDB(); renderJCN();
}

function openEditJCN(id) {
  const j = db.jcn.find(x => x.id === id);
  if (!j) return;
  document.getElementById('ejcn-id').value     = id;
  document.getElementById('ejcn-date').value   = j.date;
  document.getElementById('ejcn-no').value     = j.no;
  document.getElementById('ejcn-desc').value   = j.desc;
  document.getElementById('ejcn-status').value = j.status;
  openModal('modal-edit-jcn');
}

function saveEditJCN() {
  const id     = document.getElementById('ejcn-id').value;
  const date   = document.getElementById('ejcn-date').value;
  const no     = document.getElementById('ejcn-no').value.trim();
  const desc   = document.getElementById('ejcn-desc').value.trim();
  const status = document.getElementById('ejcn-status').value;
  if (!date || !no || !desc) { alert('⚠️ Semua field wajib diisi.'); return; }
  const idx = db.jcn.findIndex(j => j.id === id);
  if (idx > -1) db.jcn[idx] = { id, date, no, desc, status };
  saveDB();
  closeModal('modal-edit-jcn');
  renderJCN();
}

function toggleJCNStatus(id) {
  const idx = db.jcn.findIndex(j => j.id === id);
  if (idx < 0) return;
  db.jcn[idx].status = db.jcn[idx].status === 'Sudah Dipakai' ? 'Belum Dipakai' : 'Sudah Dipakai';
  saveDB(); renderJCN();
}

function exportJCNCSV() {
  if (!db.jcn.length) { alert('Tidak ada data untuk diekspor.'); return; }
  const rows = [['No','Tanggal','No. JCN','Uraian Pekerjaan','Status']];
  db.jcn.forEach((j, i) => rows.push([i+1, j.date, j.no, j.desc, j.status]));
  const csv = rows.map(r => r.map(c => `"${String(c).replace(/"/g,'""')}"`).join(',')).join('\n');
  const a = document.createElement('a');
  a.href = 'data:text/csv;charset=utf-8,\uFEFF' + encodeURIComponent(csv);
  a.download = `JCN_${new Date().toISOString().slice(0,10)}.csv`;
  a.click();
}

function renderJCN() {
  const q      = (document.getElementById('jcn-search')?.value || '').toLowerCase();
  const filter = document.getElementById('jcn-filter')?.value || '';
  const tbody  = document.getElementById('tbl-jcn-body');
  const empty  = document.getElementById('jcn-empty');
  if (!tbody) return;

  // Set default date if empty
  const dateInput = document.getElementById('jcn-date');
  if (dateInput && !dateInput.value) dateInput.valueAsDate = new Date();

  let data = (db.jcn||[]).filter(j => {
    const matchQ = j.no.toLowerCase().includes(q) || j.desc.toLowerCase().includes(q);
    const matchF = !filter || j.status === filter;
    return matchQ && matchF;
  });

  const total  = (db.jcn||[]).length;
  const used   = (db.jcn||[]).filter(j => j.status === 'Sudah Dipakai').length;
  const unused = total - used;

  document.getElementById('jcn-stats').innerHTML = `
    <div class="stat-card blue">
      <div class="stat-icon">🔖</div>
      <div class="stat-label">Total No. JCN</div>
      <div class="stat-value">${total}</div>
      <div class="stat-sub">Semua JCN tercatat</div>
    </div>
    <div class="stat-card green">
      <div class="stat-icon">✅</div>
      <div class="stat-label">Sudah Dipakai</div>
      <div class="stat-value" style="color:var(--success)">${used}</div>
      <div class="stat-sub">JCN terpakai</div>
    </div>
    <div class="stat-card gold">
      <div class="stat-icon">⏳</div>
      <div class="stat-label">Belum Dipakai</div>
      <div class="stat-value" style="color:var(--gold)">${unused}</div>
      <div class="stat-sub">Tersedia</div>
    </div>`;

  if (data.length === 0) {
    tbody.innerHTML = '';
    empty.style.display = 'block';
    return;
  }
  empty.style.display = 'none';

  tbody.innerHTML = data.map((j, idx) => {
    const used = j.status === 'Sudah Dipakai';
    return `<tr>
      <td style="color:var(--text-muted);font-size:12px">${idx+1}</td>
      <td style="white-space:nowrap;font-size:13px">${fmtDate(j.date)}</td>
      <td><span style="font-family:monospace;font-size:13px;font-weight:600;color:var(--navy);background:var(--bg);padding:3px 8px;border-radius:5px;border:1px solid var(--border)">${j.no}</span></td>
      <td style="max-width:280px;word-break:break-word;font-size:13px">${j.desc}</td>
      <td>
        <span class="badge ${used ? 'badge-green' : 'badge-gold'}" style="cursor:pointer" onclick="toggleJCNStatus('${j.id}')" title="Klik untuk ubah status">
          ${used ? '✅ ' : '⏳ '}${j.status}
        </span>
      </td>
      <td>
        <div style="display:flex;gap:6px">
          <button class="btn btn-outline btn-sm" onclick="openEditJCN('${j.id}')">✏️ Edit</button>
          <button class="btn btn-danger btn-sm" onclick="deleteJCN('${j.id}')">🗑</button>
        </div>
      </td>
    </tr>`;
  }).join('');
}


function setDate() {
  const now = new Date();
  document.getElementById('topbar-date').textContent = now.toLocaleDateString('id-ID', { weekday:'long', year:'numeric', month:'long', day:'numeric' });
}

loadDB();
setDate();
renderDashboard();
</script>
</body>
</html>
