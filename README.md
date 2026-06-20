
<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ProManage – PO & APD Management</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.min.js"></script>
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
    --text-strong: #1B2B4B;
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

  /* ── DARK MODE ── */
  [data-theme="dark"] {
    --navy: #0F1A30;
    --navy-light: #18253F;
    --steel: #5B82BC;
    --steel-light: #7DA0D4;
    --mint: #1B2E3A;
    --mint-dark: #24404F;
    --gold: #F0A500;
    --gold-light: #3A2E12;
    --danger: #F0716E;
    --danger-light: #3A1E22;
    --success: #3FDD8B;
    --success-light: #173628;
    --text: #E7EBF5;
    --text-strong: #F2F4FA;
    --text-muted: #9099AD;
    --border: #2A3550;
    --bg: #10172B;
    --white: #1A2238;
    --shadow: 0 2px 12px rgba(0,0,0,0.35);
    --shadow-md: 0 4px 24px rgba(0,0,0,0.45);
  }
  body, .card, .topbar, .modal, .stat-card, .badge, .btn, input, select, textarea {
    transition: background-color .25s ease, color .25s ease, border-color .25s ease;
  }

  /* ── THEME TOGGLE ── */
  .theme-toggle {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 38px; height: 38px;
    border-radius: var(--radius-sm);
    border: 1.5px solid var(--border);
    background: var(--white);
    cursor: pointer;
    color: var(--text);
    font-size: 17px;
    transition: background .18s, border-color .18s, color .18s;
    flex-shrink: 0;
  }
  .theme-toggle:hover { background: var(--mint); border-color: var(--steel); }

  body {
    font-family: 'Inter', sans-serif;
    background: var(--bg);
    color: var(--text);
    display: flex;
    min-height: 100vh;
    font-size: 14px;
  }


  /* ── TOAST NOTIFICATION ── */
  #toast-container {
    position: fixed;
    top: 20px;
    right: 20px;
    z-index: 99999;
    display: flex;
    flex-direction: column;
    gap: 10px;
    pointer-events: none;
  }
  .toast {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 13px 18px;
    border-radius: var(--radius-sm);
    font-size: 13px;
    font-weight: 500;
    color: #fff;
    min-width: 260px;
    max-width: 360px;
    box-shadow: 0 6px 24px rgba(0,0,0,0.15);
    pointer-events: all;
    animation: toastIn 0.3s cubic-bezier(.4,0,.2,1) forwards;
    position: relative;
    overflow: hidden;
  }
  .toast::after {
    content: '';
    position: absolute;
    bottom: 0; left: 0;
    height: 3px;
    background: rgba(255,255,255,0.4);
    animation: toastBar 3s linear forwards;
    border-radius: 0 0 var(--radius-sm) var(--radius-sm);
  }
  .toast.toast-success { background: #1a9e5c; }
  .toast.toast-error   { background: var(--danger); }
  .toast.toast-warn    { background: #d48806; }
  .toast.toast-info    { background: var(--steel); }
  .toast.toast-hide    { animation: toastOut 0.3s ease forwards; }
  .toast-icon { font-size: 16px; flex-shrink: 0; }
  .toast-msg  { flex: 1; line-height: 1.4; }
  .toast-close {
    background: none; border: none; color: rgba(255,255,255,0.7);
    cursor: pointer; font-size: 16px; padding: 0 0 0 6px; flex-shrink: 0;
  }
  .toast-close:hover { color: #fff; }
  @keyframes toastIn  { from { opacity:0; transform:translateX(40px); } to { opacity:1; transform:translateX(0); } }
  @keyframes toastOut { from { opacity:1; transform:translateX(0); } to { opacity:0; transform:translateX(40px); } }
  @keyframes toastBar { from { width:100%; } to { width:0%; } }

  /* ── SIDEBAR ── */
  .sidebar {
    width: var(--sidebar-w);
    background: var(--navy);
    min-height: 100vh;
    position: fixed;
    top: 0; left: 0;
    display: flex;
    flex-direction: column;
    z-index: 200;
    transition: transform .35s cubic-bezier(.22,.61,.36,1);
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
  .topbar-title { font-size: 16px; font-weight: 700; color: var(--text-strong); }
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
  .card-title { font-size: 14px; font-weight: 700; color: var(--text-strong); }
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
  .stat-value { font-size: 24px; font-weight: 800; color: var(--text-strong); margin: 6px 0 4px; line-height: 1; }
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

  /* ── STANDARDIZED STATUS BADGES ── */
  /* 🟢 Aman | 🟡 Perhatian | 🔴 Kritis | 🔵 Informasi — dipakai konsisten di seluruh modul */
  .badge-aman      { background: var(--success-light); color: #18924E; }
  .badge-perhatian { background: var(--gold-light);     color: #B07A00; }
  .badge-kritis    { background: var(--danger-light);   color: var(--danger); }
  .badge-info      { background: #EEF3FB;               color: var(--steel); }
  .badge-aman::before      { content: "🟢"; margin-right: 5px; font-size: 9px; }
  .badge-perhatian::before { content: "🟡"; margin-right: 5px; font-size: 9px; }
  .badge-kritis::before    { content: "🔴"; margin-right: 5px; font-size: 9px; }
  .badge-info::before      { content: "🔵"; margin-right: 5px; font-size: 9px; }

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
  .table-wrap {
    overflow-x: auto;
    overflow-y: auto;
    max-height: 520px; /* tabel jadi box dengan scroll sendiri, agar sticky header tidak tabrakan dgn elemen lain di halaman */
  }
  table { width: 100%; border-collapse: collapse; }
  thead {
    position: sticky;
    top: 0; /* relatif terhadap .table-wrap (scroll container-nya sendiri), bukan window */
    z-index: 10;
  }
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
  label { font-size: 12px; font-weight: 600; color: var(--text-strong); }
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
  .modal-title { font-size: 16px; font-weight: 700; color: var(--text-strong); }
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
  .page-header h1 { font-size: 22px; font-weight: 800; color: var(--text-strong); }
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
  .apd-name { font-size: 13px; font-weight: 700; color: var(--text-strong); margin-bottom: 4px; }
  .apd-meta { font-size: 11.5px; color: var(--text-muted); }
  .apd-stock {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-top: 8px;
    padding-top: 8px;
    border-top: 1px solid var(--border);
  }
  .apd-stock-val { font-size: 18px; font-weight: 800; color: var(--text-strong); }
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
  .po-name { font-size: 15px; font-weight: 700; color: var(--text-strong); margin-bottom: 2px; }
  .po-number { font-size: 12px; color: var(--text-muted); }
  .po-amounts {
    display: flex;
    gap: 20px;
    margin: 12px 0;
  }
  .po-amount-item { }
  .po-amount-label { font-size: 10px; color: var(--text-muted); text-transform: uppercase; letter-spacing: .6px; font-weight: 600; }
  .po-amount-value { font-size: 14px; font-weight: 700; color: var(--text-strong); margin-top: 2px; }
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

  /* ── HAMBURGER BUTTON ── */
  .hamburger {
    display: none;
    align-items: center;
    justify-content: center;
    width: 38px; height: 38px;
    border-radius: var(--radius-sm);
    border: none;
    background: none;
    cursor: pointer;
    color: var(--text-strong);
    font-size: 20px;
    transition: background .18s, color .18s;
    flex-shrink: 0;
    margin-right: 10px;
  }
  .hamburger:hover { background: var(--mint); }

  /* ── SIDEBAR OVERLAY ── */
  .sidebar-overlay {
    display: none;
    position: fixed;
    inset: 0;
    background: rgba(10,20,40,.45);
    z-index: 190;
    backdrop-filter: blur(1px);
    opacity: 0;
    pointer-events: none; /* FIX: jangan tangkap klik/tap saat overlay tersembunyi (opacity:0 saja tidak cukup) */
    transition: opacity .35s cubic-bezier(.22,.61,.36,1);
  }
  .sidebar-overlay.show {
    opacity: 1;
    pointer-events: auto; /* aktifkan tangkapan klik hanya saat overlay benar-benar tampil */
  }

  @media (max-width: 900px) {
    .hamburger { display: flex; }
    .sidebar-overlay { display: block; }
    .sidebar {
      transform: translateX(-100%);
      box-shadow: none;
    }
    .sidebar.open {
      transform: translateX(0);
      box-shadow: 0 0 40px rgba(0,0,0,.25);
    }
    .main { margin-left: 0; }
    .grid-4 { grid-template-columns: 1fr 1fr; }
    .grid-2 { grid-template-columns: 1fr; }
    .form-grid { grid-template-columns: 1fr; }
    .topbar { padding: 0 16px; }
  }
  @media (max-width: 600px) {
    .grid-4 { grid-template-columns: 1fr; }
    .grid-3 { grid-template-columns: 1fr 1fr; }
    .content { padding: 16px; }
  }


  .tag-new { font-size: 9px; background: var(--gold); color: white; border-radius: 4px; padding: 1px 5px; font-weight: 700; letter-spacing: .5px; vertical-align: middle; margin-left: 4px; }

  /* ── DASHBOARD CALENDAR WIDGET ── */
  .cal-grid { display: grid; grid-template-columns: repeat(7, 1fr); gap: 4px; }
  .cal-dow {
    text-align: center;
    font-size: 10px;
    font-weight: 700;
    color: var(--text-muted);
    text-transform: uppercase;
    letter-spacing: .4px;
    padding-bottom: 6px;
  }
  .cal-day {
    position: relative;
    aspect-ratio: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    border-radius: var(--radius-sm);
    font-size: 12.5px;
    font-weight: 500;
    color: var(--text);
    cursor: pointer;
    background: var(--bg);
    transition: background .15s, color .15s;
    user-select: none;
  }
  .cal-day:hover { background: var(--mint); }
  .cal-day.empty { background: transparent; cursor: default; pointer-events: none; }
  .cal-day.today { border: 1.5px solid var(--steel); font-weight: 800; color: var(--steel); }
  .cal-day.selected { background: var(--steel); color: var(--white); }
  .cal-day.selected .cal-day-dots span { background: var(--white); }
  .cal-day-dots { display: flex; gap: 2px; margin-top: 2px; height: 5px; }
  .cal-day-dots span { width: 4.5px; height: 4.5px; border-radius: 50%; display: block; }
  .cal-dot-po    { background: var(--steel); }
  .cal-dot-trm   { background: var(--success); }
  .cal-dot-jcn   { background: var(--gold); }
  .cal-legend { display: flex; gap: 14px; flex-wrap: wrap; margin-top: 14px; font-size: 11.5px; color: var(--text-muted); }
  .cal-legend span { display: inline-flex; align-items: center; gap: 5px; }
  .cal-legend .dot { width: 7px; height: 7px; border-radius: 50%; display: inline-block; }
  .cal-event-item {
    display: flex;
    align-items: flex-start;
    gap: 10px;
    padding: 10px 0;
    border-bottom: 1px solid var(--border);
  }
  .cal-event-item:last-child { border-bottom: none; }
  .cal-event-icon { font-size: 16px; flex-shrink: 0; margin-top: 1px; }
  .cal-event-text { flex: 1; min-width: 0; }
  .cal-event-label { font-weight: 600; font-size: 12.5px; }
  .cal-event-date { font-size: 11px; color: var(--text-muted); margin-top: 1px; }

  /* ── SKELETON LOADING ── */
  @keyframes skeletonShimmer {
    0%   { background-position: -300px 0; }
    100% { background-position: 300px 0; }
  }
  .skel {
    background: linear-gradient(90deg, var(--bg) 25%, var(--border) 37%, var(--bg) 63%);
    background-size: 600px 100%;
    animation: skeletonShimmer 1.4s ease-in-out infinite;
    border-radius: 6px;
    display: inline-block;
  }
  .skel-row td { padding: 14px; }
  .skel-line { height: 12px; width: 100%; }
  .skel-line.w-60 { width: 60%; }
  .skel-line.w-40 { width: 40%; }
  .skel-badge { height: 20px; width: 64px; border-radius: 99px; }
  .skel-card {
    background: var(--white);
    border-radius: var(--radius);
    border: 1px solid var(--border);
    padding: 16px;
    display: flex;
    flex-direction: column;
    gap: 10px;
  }
  .skel-chart {
    height: 220px;
    width: 100%;
    border-radius: var(--radius-sm);
  }
  .skel-stat-card {
    background: var(--white);
    border-radius: var(--radius);
    border: 1px solid var(--border);
    padding: 16px;
    display: flex;
    flex-direction: column;
    gap: 10px;
  }
  .skel-fade-in { animation: skelFadeIn .25s ease; }
  @keyframes skelFadeIn { from { opacity: 0; } to { opacity: 1; } }
  .text-right { text-align: right; }
  .mt-16 { margin-top: 16px; }
  .mb-16 { margin-bottom: 16px; }
  .flex-between { display: flex; align-items: center; justify-content: space-between; }
  .flex-gap { display: flex; align-items: center; gap: 8px; }
  .full-w { grid-column: 1 / -1; }
</style>
</head>
<body>

<!-- SIDEBAR OVERLAY -->
<div class="sidebar-overlay" id="sidebar-overlay" onclick="closeSidebar()"></div>

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
    <div class="nav-item" onclick="showPage('apd-keluar', this)">
      <span class="nav-icon">📤</span> Pengeluaran Barang
    </div>
  </div>
  <div class="sidebar-footer">
    ProManage v1.0 &nbsp;·&nbsp; © 2025
  </div>
</nav>

<!-- MAIN -->
<div class="main">
  <header class="topbar">
    <button class="hamburger" id="hamburger-btn" onclick="toggleSidebar()" aria-label="Toggle menu">☰</button>
    <div class="topbar-title" id="topbar-title">Dashboard</div>
    <div class="topbar-actions">
      <span class="topbar-date" id="topbar-date"></span>
      <button class="theme-toggle" id="theme-toggle-btn" onclick="toggleTheme()" aria-label="Ganti mode gelap/terang" title="Mode Gelap">🌙</button>
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

      <!-- CALENDAR WIDGET -->
      <div class="grid-2" style="margin-bottom:24px;align-items:start">
        <div class="card">
          <div class="card-header">
            <div>
              <div class="card-title">📅 Kalender Aktivitas</div>
              <div class="card-subtitle">PO baru, barang datang & JCN baru bulan ini</div>
            </div>
            <div style="display:flex;gap:4px">
              <button class="btn btn-outline btn-icon" onclick="calendarShiftMonth(-1)" title="Bulan sebelumnya">‹</button>
              <button class="btn btn-outline btn-sm" onclick="calendarGoToday()">Hari ini</button>
              <button class="btn btn-outline btn-icon" onclick="calendarShiftMonth(1)" title="Bulan berikutnya">›</button>
            </div>
          </div>
          <div class="card-body" id="dash-calendar"></div>
        </div>
        <div class="card">
          <div class="card-header">
            <div>
              <div class="card-title" id="dash-calendar-detail-title">📌 Aktivitas Mendatang</div>
              <div class="card-subtitle" id="dash-calendar-detail-sub">Klik tanggal di kalender untuk lihat detail</div>
            </div>
          </div>
          <div class="card-body" id="dash-calendar-detail"></div>
        </div>
      </div>

      <!-- CHARTS ROW 1: Tagihan per Bulan + Nilai vs Tagihan vs Sisa -->
      <div class="grid-2" style="margin-bottom:24px">
        <div class="card">
          <div class="card-header">
            <div>
              <div class="card-title">📈 Tagihan PO per Bulan</div>
              <div class="card-subtitle">Total nominal tagihan masuk setiap bulan</div>
            </div>
          </div>
          <div class="card-body" style="padding:16px 20px">
            <canvas id="chart-tagihan-bulan" height="220"></canvas>
          </div>
        </div>
        <div class="card">
          <div class="card-header">
            <div>
              <div class="card-title">📊 Perbandingan per PO</div>
              <div class="card-subtitle">Nilai PO vs Total Tagihan vs Sisa Anggaran</div>
            </div>
          </div>
          <div class="card-body" style="padding:16px 20px">
            <canvas id="chart-po-compare" height="220"></canvas>
          </div>
        </div>
      </div>

      <!-- CHART ROW 2: Donut ringkasan anggaran -->
      <div class="grid-2" style="margin-bottom:24px">
        <div class="card">
          <div class="card-header">
            <div>
              <div class="card-title">🥧 Komposisi Anggaran</div>
              <div class="card-subtitle">Proporsi tagihan vs sisa dari total seluruh PO</div>
            </div>
          </div>
          <div class="card-body" style="padding:16px 20px;display:flex;align-items:center;justify-content:center">
            <canvas id="chart-donut-anggaran" height="200" style="max-width:260px"></canvas>
          </div>
        </div>
        <div class="card">
          <div class="card-header">
            <div>
              <div class="card-title">📉 Tren Kumulatif Tagihan</div>
              <div class="card-subtitle">Akumulasi tagihan dari waktu ke waktu</div>
            </div>
          </div>
          <div class="card-body" style="padding:16px 20px">
            <canvas id="chart-kumulatif" height="200"></canvas>
          </div>
        </div>
      </div>

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
          <button class="btn btn-primary" onclick="openTagihanModalFresh()">＋ Input Tagihan</button>
        </div>
      </div>

      <!-- FILTER BAR -->
      <div class="card" style="margin-bottom:20px">
        <div class="card-body" style="padding:16px 20px">
          <div style="display:grid;grid-template-columns:1fr 1fr 1fr auto;gap:12px;align-items:end">
            <div class="form-group" style="margin:0">
              <label>Filter No. PO</label>
              <select id="filter-tagihan-po" onchange="renderTagihan()" style="padding:9px 12px;border:1.5px solid var(--border);border-radius:var(--radius-sm);font-size:13px;font-family:inherit;outline:none;width:100%">
                <option value="">Semua No. PO</option>
              </select>
            </div>
            <div class="form-group" style="margin:0">
              <label>Filter Periode</label>
              <input type="text" id="filter-tagihan-periode" placeholder="Cth: Januari 2025" oninput="renderTagihan()" style="padding:9px 12px;border:1.5px solid var(--border);border-radius:var(--radius-sm);font-size:13px;font-family:inherit;outline:none;width:100%" onfocus="this.style.borderColor='var(--steel)'" onblur="this.style.borderColor='var(--border)'">
            </div>
            <div class="form-group" style="margin:0">
              <label>Filter Keterangan</label>
              <input type="text" id="filter-tagihan-ket" placeholder="Cari keterangan..." oninput="renderTagihan()" style="padding:9px 12px;border:1.5px solid var(--border);border-radius:var(--radius-sm);font-size:13px;font-family:inherit;outline:none;width:100%" onfocus="this.style.borderColor='var(--steel)'" onblur="this.style.borderColor='var(--border)'">
            </div>
            <button class="btn btn-outline" onclick="resetFilterTagihan()" style="white-space:nowrap">🔄 Reset</button>
          </div>
        </div>
      </div>

      <div class="card">
        <div class="card-body table-wrap" style="padding:0">
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
          <div id="tagihan-empty" style="display:none;text-align:center;padding:48px 24px;color:var(--text-muted)">
            <div style="font-size:48px;margin-bottom:12px;opacity:.4">🧾</div>
            <h3 style="font-size:15px;font-weight:600;color:var(--text);margin-bottom:6px">Tidak ada tagihan ditemukan</h3>
            <p style="font-size:13px">Coba ubah filter pencarian.</p>
          </div>
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
          <button class="btn btn-outline" onclick="showPage('apd-keluar', document.querySelector('[onclick*=apd-keluar]'))">📤 Pengeluaran</button>
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
          <div style="font-size:18px;font-weight:800;color:var(--text-strong);" id="total-rencana">0</div>
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
                <th>Catatan</th>
                <th>Aksi</th>
              </tr>
            </thead>
            <tbody id="tbl-terima-body"></tbody>
          </table>
        </div>
      </div>
    </div>


    <!-- ════════════════════════════════ PENGELUARAN BARANG ════════════════════════════════ -->
    <div id="page-apd-keluar" class="page">
      <div class="page-header">
        <div>
          <h1>Pengeluaran Barang APD</h1>
          <p>Catat barang yang keluar dan kurangi stok secara otomatis</p>
        </div>
        <div class="page-header-actions">
          <button class="btn btn-primary" onclick="openModal('modal-keluar')">＋ Catat Pengeluaran</button>
        </div>
      </div>
      <div class="card">
        <div class="card-body table-wrap">
          <table>
            <thead>
              <tr>
                <th>Tanggal</th>
                <th>Nama APD</th>
                <th>Qty Keluar</th>
                <th>Satuan</th>
                <th>Penerima / Keterangan</th>
                <th>Aksi</th>
              </tr>
            </thead>
            <tbody id="tbl-keluar-body"></tbody>
          </table>
        </div>
      </div>
    </div>

  </div><!-- /content -->
</div><!-- /main -->

<div id="toast-container"></div>

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
      <div class="modal-title" id="modal-tagihan-title">Input Tagihan Bulanan</div>
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
          <div style="display:flex;justify-content:flex-end;margin-top:8px;font-weight:700;color:var(--text-strong)">Total: <span id="r-qty-total" style="margin-left:6px">0</span></div>
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


<!-- MODAL DETAIL PO -->
<div class="modal-overlay" id="modal-detail-po">
  <div class="modal" style="max-width:560px">
    <div class="modal-header">
      <div class="modal-title">👁 Detail Purchase Order</div>
      <button class="btn-close" onclick="closeModal('modal-detail-po')">✕</button>
    </div>
    <div class="modal-body" id="detail-po-content"></div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeModal('modal-detail-po')">Tutup</button>
    </div>
  </div>
</div>

<!-- MODAL DETAIL TAGIHAN -->
<div class="modal-overlay" id="modal-detail-tagihan">
  <div class="modal" style="max-width:520px">
    <div class="modal-header">
      <div class="modal-title">👁 Detail Tagihan</div>
      <button class="btn-close" onclick="closeModal('modal-detail-tagihan')">✕</button>
    </div>
    <div class="modal-body" id="detail-tagihan-content"></div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeModal('modal-detail-tagihan')">Tutup</button>
    </div>
  </div>
</div>

<!-- MODAL DETAIL RENCANA -->
<div class="modal-overlay" id="modal-detail-rencana">
  <div class="modal" style="max-width:520px">
    <div class="modal-header">
      <div class="modal-title">👁 Detail Rencana Pembelian</div>
      <button class="btn-close" onclick="closeModal('modal-detail-rencana')">✕</button>
    </div>
    <div class="modal-body" id="detail-rencana-content"></div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeModal('modal-detail-rencana')">Tutup</button>
    </div>
  </div>
</div>

<!-- MODAL DETAIL TERIMA -->
<div class="modal-overlay" id="modal-detail-terima">
  <div class="modal" style="max-width:480px">
    <div class="modal-header">
      <div class="modal-title">👁 Detail Penerimaan Barang</div>
      <button class="btn-close" onclick="closeModal('modal-detail-terima')">✕</button>
    </div>
    <div class="modal-body" id="detail-terima-content"></div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeModal('modal-detail-terima')">Tutup</button>
    </div>
  </div>
</div>

<!-- MODAL EDIT PO -->
<div class="modal-overlay" id="modal-edit-po">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title">✏️ Edit Purchase Order</div>
      <button class="btn-close" onclick="closeModal('modal-edit-po')">✕</button>
    </div>
    <div class="modal-body">
      <input type="hidden" id="epo-id">
      <div class="form-grid">
        <div class="form-group">
          <label>Nomor PO *</label>
          <input type="text" id="epo-no" placeholder="PO-2025-001">
        </div>
        <div class="form-group">
          <label>Tanggal PO *</label>
          <input type="date" id="epo-date">
        </div>
        <div class="form-group full">
          <label>Nama / Deskripsi PO *</label>
          <input type="text" id="epo-name">
        </div>
        <div class="form-group">
          <label>Nilai Total PO (Rp) *</label>
          <input type="number" id="epo-nilai" min="0">
        </div>
        <div class="form-group">
          <label>Status</label>
          <select id="epo-status">
            <option value="Aktif">Aktif</option>
            <option value="Selesai">Selesai</option>
            <option value="Ditangguhkan">Ditangguhkan</option>
          </select>
        </div>
        <div class="form-group full">
          <label>Catatan</label>
          <textarea id="epo-catatan"></textarea>
        </div>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeModal('modal-edit-po')">Batal</button>
      <button class="btn btn-primary" onclick="saveEditPO()">Simpan Perubahan</button>
    </div>
  </div>
</div>

<!-- MODAL EDIT RENCANA -->
<div class="modal-overlay" id="modal-edit-rencana">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title">✏️ Edit Rencana Pembelian</div>
      <button class="btn-close" onclick="closeModal('modal-edit-rencana')">✕</button>
    </div>
    <div class="modal-body">
      <input type="hidden" id="er-id">
      <div class="form-grid">
        <div class="form-group full">
          <label>Nama APD</label>
          <input type="text" id="er-nama" readonly style="background:var(--bg)">
        </div>
        <div class="form-group">
          <label>Qty Total *</label>
          <input type="number" id="er-qty" min="0">
        </div>
        <div class="form-group">
          <label>Satuan</label>
          <input type="text" id="er-satuan" readonly style="background:var(--bg)">
        </div>
        <div class="form-group full">
          <label>Catatan</label>
          <textarea id="er-catatan"></textarea>
        </div>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeModal('modal-edit-rencana')">Batal</button>
      <button class="btn btn-primary" onclick="saveEditRencana()">Simpan Perubahan</button>
    </div>
  </div>
</div>

<!-- MODAL EDIT TERIMA -->
<div class="modal-overlay" id="modal-edit-terima">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title">✏️ Edit Penerimaan Barang</div>
      <button class="btn-close" onclick="closeModal('modal-edit-terima')">✕</button>
    </div>
    <div class="modal-body">
      <input type="hidden" id="etrm-id">
      <div class="form-grid">
        <div class="form-group full">
          <label>Nama APD</label>
          <input type="text" id="etrm-nama" readonly style="background:var(--bg)">
        </div>
        <div class="form-group">
          <label>Tanggal Terima *</label>
          <input type="date" id="etrm-tgl">
        </div>
        <div class="form-group">
          <label>Qty Diterima *</label>
          <input type="number" id="etrm-qty" min="0">
        </div>
        <div class="form-group full">
          <label>Catatan</label>
          <textarea id="etrm-catatan"></textarea>
        </div>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeModal('modal-edit-terima')">Batal</button>
      <button class="btn btn-primary" onclick="saveEditTerima()">Simpan Perubahan</button>
    </div>
  </div>
</div>


<!-- PENGELUARAN BARANG -->
<div class="modal-overlay" id="modal-keluar">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title" id="modal-keluar-title">📤 Catat Pengeluaran Barang</div>
      <button class="btn-close" onclick="closeModal('modal-keluar')">✕</button>
    </div>
    <div class="modal-body">
      <div class="form-grid">
        <div class="form-group full">
          <label>APD yang Dikeluarkan *</label>
          <select id="klr-apd-id" onchange="updateKeluarStokInfo()"></select>
          <div id="klr-stok-info" style="margin-top:6px;font-size:12px;color:var(--text-muted)"></div>
        </div>
        <div class="form-group">
          <label>Tanggal Keluar *</label>
          <input type="date" id="klr-tgl">
        </div>
        <div class="form-group">
          <label>Qty Keluar *</label>
          <input type="number" id="klr-qty" placeholder="0" min="1" oninput="updateKeluarStokInfo()">
        </div>
        <div class="form-group full">
          <label>Penerima / Keterangan</label>
          <textarea id="klr-ket" placeholder="Nama penerima, lokasi, atau keterangan lain..."></textarea>
        </div>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeModal('modal-keluar')">Batal</button>
      <button class="btn btn-primary" onclick="saveKeluar()">Simpan & Kurangi Stok</button>
    </div>
  </div>
</div>

<!-- MODAL EDIT KELUAR -->
<div class="modal-overlay" id="modal-edit-keluar">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title">✏️ Edit Pengeluaran Barang</div>
      <button class="btn-close" onclick="closeModal('modal-edit-keluar')">✕</button>
    </div>
    <div class="modal-body">
      <input type="hidden" id="eklr-id">
      <div class="form-grid">
        <div class="form-group full">
          <label>Nama APD</label>
          <input type="text" id="eklr-nama" readonly style="background:var(--bg)">
        </div>
        <div class="form-group">
          <label>Tanggal Keluar *</label>
          <input type="date" id="eklr-tgl">
        </div>
        <div class="form-group">
          <label>Qty Keluar *</label>
          <input type="number" id="eklr-qty" min="1">
        </div>
        <div class="form-group full">
          <label>Penerima / Keterangan</label>
          <textarea id="eklr-ket"></textarea>
        </div>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeModal('modal-edit-keluar')">Batal</button>
      <button class="btn btn-primary" onclick="saveEditKeluar()">Simpan Perubahan</button>
    </div>
  </div>
</div>

<!-- MODAL DETAIL KELUAR -->
<div class="modal-overlay" id="modal-detail-keluar">
  <div class="modal" style="max-width:480px">
    <div class="modal-header">
      <div class="modal-title">👁 Detail Pengeluaran Barang</div>
      <button class="btn-close" onclick="closeModal('modal-detail-keluar')">✕</button>
    </div>
    <div class="modal-body" id="detail-keluar-content"></div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeModal('modal-detail-keluar')">Tutup</button>
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

// ════════════════ SIDEBAR MOBILE ════════════════
function toggleSidebar() {
  const sidebar = document.getElementById('sidebar');
  const overlay = document.getElementById('sidebar-overlay');
  const btn     = document.getElementById('hamburger-btn');
  const isOpen  = sidebar.classList.contains('open');
  if (isOpen) {
    closeSidebar();
  } else {
    sidebar.classList.add('open');
    overlay.classList.add('show');
    btn.textContent = '✕';
    btn.setAttribute('aria-label', 'Tutup menu');
    document.body.style.overflow = 'hidden';
  }
}

function closeSidebar() {
  const sidebar = document.getElementById('sidebar');
  const overlay = document.getElementById('sidebar-overlay');
  const btn     = document.getElementById('hamburger-btn');
  sidebar.classList.remove('open');
  overlay.classList.remove('show');
  btn.textContent = '☰';
  btn.setAttribute('aria-label', 'Buka menu');
  document.body.style.overflow = '';
}

// ════════════════ TOAST NOTIFICATION ════════════════
function showToast(msg, type = 'success', duration = 3000) {
  const icons = { success: '✅', error: '❌', warn: '⚠️', info: 'ℹ️' };
  const container = document.getElementById('toast-container');
  const toast = document.createElement('div');
  toast.className = `toast toast-${type}`;
  toast.innerHTML = `
    <span class="toast-icon">${icons[type] || '✅'}</span>
    <span class="toast-msg">${msg}</span>
    <button class="toast-close" onclick="this.parentElement.remove()">✕</button>
  `;
  container.appendChild(toast);
  setTimeout(() => {
    toast.classList.add('toast-hide');
    setTimeout(() => toast.remove(), 320);
  }, duration);
}

let db = {
  po: [],
  tagihan: [],
  apd: [],
  rencana: [],
  terima: [],
  keluar: [],
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
  'apd-keluar': 'Pengeluaran Barang',
  'jcn-master': 'Master Data No. JCN'
};

function showPage(id, el) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
  document.getElementById('page-' + id).classList.add('active');
  if (el) el.classList.add('active');
  document.getElementById('topbar-title').textContent = pageTitles[id] || id;
  showPageSkeleton(id);
  setTimeout(() => renderPage(id), 0); // skeleton sempat tergambar 1 frame sebelum render data sebenarnya (terasa instan, tidak "kosong sebentar")
  if (window.innerWidth <= 900) closeSidebar();
}

// ════════════════ SKELETON LOADING ════════════════
function skelRows(n, cols) {
  const cells = Array.from({ length: cols }, (_, i) =>
    `<td><span class="skel skel-line ${i === 0 ? 'w-40' : i === cols - 1 ? 'w-60' : ''}"></span></td>`
  ).join('');
  return Array.from({ length: n }, () => `<tr class="skel-row">${cells}</tr>`).join('');
}

const skeletonMap = {
  'po-list':     { tbody: 'tbl-po-body',      cols: 8 },
  'po-tagihan':  { tbody: 'tbl-tagihan-body', cols: 5 },
  'jcn-master':  { tbody: 'tbl-jcn-body',     cols: 6 },
  'apd-stok':    { tbody: 'tbl-stok-body',    cols: 6 },
  'apd-rencana': { tbody: 'tbl-rencana-body', cols: 6 },
  'apd-terima':  { tbody: 'tbl-terima-body',  cols: 5 },
  'apd-keluar':  { tbody: 'tbl-keluar-body',  cols: 6 },
};

function showPageSkeleton(id) {
  if (id === 'dashboard') { showDashboardSkeleton(); return; }
  if (id === 'apd-master') { showAPDCardsSkeleton(); return; }
  const conf = skeletonMap[id];
  if (!conf) return; // halaman tanpa tabel (mis. master data sederhana) — lewati
  const tbody = document.getElementById(conf.tbody);
  if (tbody) tbody.innerHTML = skelRows(5, conf.cols);
}

function showAPDCardsSkeleton() {
  const grid = document.getElementById('apd-card-grid');
  if (!grid) return;
  grid.innerHTML = Array.from({ length: 6 }, () => `
    <div class="skel-card">
      <span class="skel skel-chart" style="height:120px"></span>
      <span class="skel skel-line w-60"></span>
      <span class="skel skel-line w-40"></span>
    </div>`).join('');
}

function showDashboardSkeleton() {
  const statRow = document.getElementById('dash-stats');
  if (statRow) {
    statRow.innerHTML = Array.from({ length: 4 }, () => `
      <div class="skel-stat-card">
        <span class="skel skel-line w-60"></span>
        <span class="skel skel-line" style="height:22px;width:80%"></span>
        <span class="skel skel-line w-40"></span>
      </div>`).join('');
  }
  const alerts = document.getElementById('dash-alerts');
  if (alerts) alerts.innerHTML = '';
  const poList = document.getElementById('dash-po-list');
  if (poList) poList.innerHTML = Array.from({ length: 2 }, () => `<div class="skel-card" style="margin-bottom:10px"><span class="skel skel-line w-60"></span><span class="skel" style="height:8px;width:100%"></span></div>`).join('');
  const stokRendah = document.getElementById('dash-stok-rendah');
  if (stokRendah) stokRendah.innerHTML = Array.from({ length: 2 }, () => `<div class="skel-card" style="margin-bottom:10px"><span class="skel skel-line w-40"></span><span class="skel skel-badge"></span></div>`).join('');
  document.querySelectorAll('#page-dashboard canvas').forEach(c => {
    c.style.visibility = 'hidden';
    if (!c.parentElement.querySelector('.skel-chart-overlay')) {
      const overlay = document.createElement('div');
      overlay.className = 'skel skel-chart skel-chart-overlay';
      overlay.style.position = 'absolute';
      c.parentElement.style.position = 'relative';
      c.parentElement.appendChild(overlay);
    }
  });
}

function hideDashboardChartSkeletons() {
  document.querySelectorAll('#page-dashboard canvas').forEach(c => { c.style.visibility = 'visible'; });
  document.querySelectorAll('#page-dashboard .skel-chart-overlay').forEach(el => el.remove());
}

function renderPage(id) {
  if (id === 'dashboard') renderDashboard();
  else if (id === 'po-list') renderPOList();
  else if (id === 'po-tagihan') renderTagihan();
  else if (id === 'apd-master') renderAPDCards();
  else if (id === 'apd-stok') renderStok();
  else if (id === 'apd-rencana') renderRencana();
  else if (id === 'apd-terima') renderTerima();
  else if (id === 'apd-keluar') renderKeluar();
  else if (id === 'jcn-master') renderJCN();
}

// ════════════════ MODAL ════════════════
function openModal(id) {
  if (id === 'modal-add-tagihan') populateTagihanModal();
  if (id === 'modal-keluar') populateKeluarModal();
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
      <div class="stat-value" style="font-size:18px;color:${totalSisaPO < totalNilaiPO*0.15 ? 'var(--danger)' : 'var(--text-strong)'}">${fmtRp(totalSisaPO)}</div>
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
  setTimeout(renderDashboardCharts, 50);
  renderCalendar();
}

// ════════════════ DASHBOARD CALENDAR WIDGET ════════════════
const bulanNamaID = ['Januari','Februari','Maret','April','Mei','Juni','Juli','Agustus','September','Oktober','November','Desember'];
let calViewYear  = new Date().getFullYear();
let calViewMonth = new Date().getMonth(); // 0-11
let calSelectedDate = null; // 'YYYY-MM-DD'

function pad2(n) { return String(n).padStart(2, '0'); }

// Kumpulkan semua event nyata dari data: { 'YYYY-MM-DD': [{type, label, icon}] }
function getCalendarEvents() {
  const map = {};
  const add = (dateStr, type, icon, label) => {
    if (!dateStr) return;
    if (!map[dateStr]) map[dateStr] = [];
    map[dateStr].push({ type, icon, label });
  };
  (db.po || []).forEach(p => add(p.date, 'po', '📄', `PO Baru — ${p.noPO || p.nama || ''}`));
  (db.terima || []).forEach(t => add(t.tgl, 'trm', '📦', `Barang Datang — ${t.namaApd || ''}`));
  (db.jcn || []).forEach(j => add(j.date, 'jcn', '🔖', `JCN Baru — ${j.no || ''}`));
  return map;
}

function calendarShiftMonth(delta) {
  calViewMonth += delta;
  if (calViewMonth > 11) { calViewMonth = 0; calViewYear++; }
  if (calViewMonth < 0)  { calViewMonth = 11; calViewYear--; }
  calSelectedDate = null;
  renderCalendar();
}

function calendarGoToday() {
  const now = new Date();
  calViewYear = now.getFullYear();
  calViewMonth = now.getMonth();
  calSelectedDate = `${calViewYear}-${pad2(calViewMonth+1)}-${pad2(now.getDate())}`;
  renderCalendar();
}

function calendarSelectDate(dateStr) {
  calSelectedDate = calSelectedDate === dateStr ? null : dateStr;
  renderCalendar();
}

function renderCalendar() {
  const grid = document.getElementById('dash-calendar');
  if (!grid) return;
  const events = getCalendarEvents();
  const todayStr = (() => { const n = new Date(); return `${n.getFullYear()}-${pad2(n.getMonth()+1)}-${pad2(n.getDate())}`; })();

  const firstDow = new Date(calViewYear, calViewMonth, 1).getDay(); // 0=Minggu
  const daysInMonth = new Date(calViewYear, calViewMonth + 1, 0).getDate();
  const dowLabels = ['Min','Sen','Sel','Rab','Kam','Jum','Sab'];

  let html = `<div style="text-align:center;font-weight:700;color:var(--text-strong);margin-bottom:10px;font-size:13.5px">${bulanNamaID[calViewMonth]} ${calViewYear}</div>`;
  html += '<div class="cal-grid">';
  dowLabels.forEach(d => html += `<div class="cal-dow">${d}</div>`);
  for (let i = 0; i < firstDow; i++) html += '<div class="cal-day empty"></div>';

  for (let d = 1; d <= daysInMonth; d++) {
    const dateStr = `${calViewYear}-${pad2(calViewMonth+1)}-${pad2(d)}`;
    const dayEvents = events[dateStr] || [];
    const classes = ['cal-day'];
    if (dateStr === todayStr) classes.push('today');
    if (dateStr === calSelectedDate) classes.push('selected');
    const types = [...new Set(dayEvents.map(e => e.type))];
    const dotsHtml = types.length
      ? `<div class="cal-day-dots">${types.map(t => `<span class="cal-dot-${t}"></span>`).join('')}</div>`
      : '';
    html += `<div class="${classes.join(' ')}" onclick="calendarSelectDate('${dateStr}')" title="${dayEvents.length} aktivitas">${d}${dotsHtml}</div>`;
  }
  html += '</div>';
  html += `<div class="cal-legend">
    <span><span class="dot" style="background:var(--steel)"></span> PO Baru</span>
    <span><span class="dot" style="background:var(--success)"></span> Barang Datang</span>
    <span><span class="dot" style="background:var(--gold)"></span> JCN Baru</span>
  </div>`;
  grid.innerHTML = html;

  renderCalendarDetail(events, todayStr);
}

function renderCalendarDetail(events, todayStr) {
  const titleEl = document.getElementById('dash-calendar-detail-title');
  const subEl   = document.getElementById('dash-calendar-detail-sub');
  const bodyEl  = document.getElementById('dash-calendar-detail');
  if (!bodyEl) return;

  let list = [];
  if (calSelectedDate) {
    titleEl.textContent = '📌 Aktivitas Tanggal Terpilih';
    subEl.textContent = new Date(calSelectedDate + 'T00:00:00').toLocaleDateString('id-ID', { weekday:'long', day:'numeric', month:'long', year:'numeric' });
    list = events[calSelectedDate] || [];
  } else {
    titleEl.textContent = '📌 Aktivitas Mendatang';
    subEl.textContent = '7 hari ke depan';
    const now = new Date(todayStr + 'T00:00:00');
    for (let i = 0; i <= 7; i++) {
      const d = new Date(now); d.setDate(now.getDate() + i);
      const ds = `${d.getFullYear()}-${pad2(d.getMonth()+1)}-${pad2(d.getDate())}`;
      (events[ds] || []).forEach(e => list.push({ ...e, _date: ds }));
    }
  }

  if (list.length === 0) {
    bodyEl.innerHTML = `<div class="empty-state"><div class="empty-state-icon">📅</div><h3>Tidak ada aktivitas</h3><p>Belum ada PO, barang masuk, atau JCN tercatat${calSelectedDate ? ' pada tanggal ini' : ' dalam 7 hari ke depan'}.</p></div>`;
    return;
  }
  bodyEl.innerHTML = list.map(e => `
    <div class="cal-event-item">
      <span class="cal-event-icon">${e.icon}</span>
      <div class="cal-event-text">
        <div class="cal-event-label">${e.label}</div>
        ${e._date ? `<div class="cal-event-date">${new Date(e._date + 'T00:00:00').toLocaleDateString('id-ID', { weekday:'short', day:'numeric', month:'short' })}</div>` : ''}
      </div>
    </div>`).join('');
}

// ════════════════ PO ════════════════
function savePO() {
  const noPO = document.getElementById('po-no').value.trim();
  const nama = document.getElementById('po-name').value.trim();
  const nilai = Number(document.getElementById('po-nilai').value);
  const date = document.getElementById('po-date').value;
  const status = document.getElementById('po-status').value;
  const catatan = document.getElementById('po-catatan').value;
  if (!noPO || !nama || !nilai) return showToast('Mohon isi semua field wajib!', 'error');
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
  showToast('PO berhasil dihapus', 'info');
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
    const statusBadge = p.status === 'Aktif' ? 'badge-aman' : p.status === 'Selesai' ? 'badge-info' : 'badge-info';
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
      <td style="white-space:nowrap">
        <div class="flex-gap">
          <button class="btn btn-outline btn-sm" onclick="showTagihanForPO('${p.id}')" title="Tagihan">🧾</button>
          <button class="btn btn-outline btn-sm" onclick="detailPO('${p.id}')" title="Detail">👁</button>
          <button class="btn btn-outline btn-sm" onclick="editPO('${p.id}')" title="Edit">✏️</button>
          <button class="btn btn-danger btn-sm" onclick="deletePO('${p.id}')" title="Hapus">🗑</button>
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

let editingTagihanId = null;

function editTagihan(id) {
  const t = db.tagihan.find(x => x.id === id);
  if (!t) return;
  editingTagihanId = id;
  document.getElementById('modal-tagihan-title').textContent = 'Edit Tagihan';
  openModal('modal-add-tagihan');
  // Set values after modal opens & select populated
  setTimeout(() => {
    document.getElementById('t-po-id').value = t.poId;
    document.getElementById('t-tanggal').value = t.tanggal;
    document.getElementById('t-periode').value = t.periode || '';
    document.getElementById('t-nominal').value = t.nominal;
    document.getElementById('t-ket').value = t.ket || '';
    updateTagihanPreview();
  }, 50);
}

function saveTagihan() {
  const poId = document.getElementById('t-po-id').value;
  const tanggal = document.getElementById('t-tanggal').value;
  const periode = document.getElementById('t-periode').value;
  const nominal = Number(document.getElementById('t-nominal').value);
  const ket = document.getElementById('t-ket').value;
  if (!poId || !tanggal || !nominal) return showToast('Mohon isi semua field wajib!', 'error');
  const po = getPoById(poId);
  if (editingTagihanId) {
    const idx = db.tagihan.findIndex(x => x.id === editingTagihanId);
    if (idx >= 0) db.tagihan[idx] = { ...db.tagihan[idx], poId, noPO: po?.noPO, namaPO: po?.nama, tanggal, periode, nominal, ket };
    editingTagihanId = null;
  } else {
    db.tagihan.push({ id: genId(), poId, noPO: po?.noPO, namaPO: po?.nama, tanggal, periode, nominal, ket });
  }
  saveDB();
  closeModal('modal-add-tagihan');
  document.getElementById('modal-tagihan-title').textContent = 'Input Tagihan Bulanan';
  ['t-periode','t-nominal','t-ket'].forEach(id => document.getElementById(id).value = '');
  renderTagihan();
  showToast(editingTagihanId ? 'Tagihan berhasil diperbarui' : 'Tagihan berhasil disimpan');
}

function deleteTagihan(id) {
  if (!confirm('Hapus tagihan ini?')) return;
  db.tagihan = db.tagihan.filter(t => t.id !== id);
  saveDB();
  renderTagihan();
  showToast('Tagihan berhasil dihapus', 'info');
}

function populateFilterPO() {
  const sel = document.getElementById('filter-tagihan-po');
  if (!sel) return;
  const current = sel.value;
  const seen = new Map();
  db.tagihan.forEach(t => { if (!seen.has(t.poId)) seen.set(t.poId, t); });
  const uniquePOs = [...seen.values()];
  sel.innerHTML = '<option value="">Semua No. PO</option>' +
    uniquePOs.map(t => `<option value="${t.poId}" ${current===t.poId?'selected':''}>${t.noPO||'-'}</option>`).join('');
}

function resetFilterTagihan() {
  ['filter-tagihan-po','filter-tagihan-periode','filter-tagihan-ket'].forEach(id => {
    const el = document.getElementById(id);
    if (el) el.value = '';
  });
  renderTagihan();
}

function renderTagihan() {
  populateFilterPO();
  const tbody = document.getElementById('tbl-tagihan-body');
  const emptyEl = document.getElementById('tagihan-empty');

  const filterPO      = document.getElementById('filter-tagihan-po')?.value || '';
  const filterPeriode = (document.getElementById('filter-tagihan-periode')?.value || '').toLowerCase();
  const filterKet     = (document.getElementById('filter-tagihan-ket')?.value || '').toLowerCase();

  if (db.tagihan.length === 0) {
    tbody.innerHTML = `<tr><td colspan="8" style="text-align:center;padding:40px;color:var(--text-muted)">Belum ada tagihan.</td></tr>`;
    if (emptyEl) emptyEl.style.display = 'none';
    return;
  }

  let data = [...db.tagihan].sort((a,b) => b.tanggal > a.tanggal ? 1 : -1);
  if (filterPO)      data = data.filter(t => t.poId === filterPO);
  if (filterPeriode) data = data.filter(t => (t.periode||'').toLowerCase().includes(filterPeriode));
  if (filterKet)     data = data.filter(t => (t.ket||'').toLowerCase().includes(filterKet));

  if (data.length === 0) {
    tbody.innerHTML = '';
    if (emptyEl) emptyEl.style.display = 'block';
    return;
  }
  if (emptyEl) emptyEl.style.display = 'none';

  tbody.innerHTML = data.map(t => {
    const po = getPoById(t.poId);
    const total = po ? getTotalTagihan(t.poId) : 0;
    const pct = po && po.nilai > 0 ? (total / po.nilai * 100) : 0;
    const badgeClass = pct >= 90 ? 'badge-kritis' : pct >= 70 ? 'badge-perhatian' : 'badge-aman';
    return `<tr>
      <td>${t.tanggal}</td>
      <td><strong>${t.noPO||'-'}</strong></td>
      <td>${t.namaPO||'-'}</td>
      <td>${t.periode||'-'}</td>
      <td><strong>${fmtRp(t.nominal)}</strong></td>
      <td style="max-width:160px;word-break:break-word">${t.ket||'-'}</td>
      <td><span class="badge ${badgeClass}">${pct.toFixed(0)}% terpakai</span></td>
      <td style="white-space:nowrap">
        <button class="btn btn-outline btn-sm" onclick="detailTagihan('${t.id}')" title="Detail" style="margin-right:4px">👁</button>
        <button class="btn btn-outline btn-sm" onclick="editTagihan('${t.id}')" title="Edit" style="margin-right:4px">✏️</button>
        <button class="btn btn-danger btn-sm" onclick="deleteTagihan('${t.id}')" title="Hapus">🗑</button>
      </td>
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
  if (!nama) return showToast('Nama APD wajib diisi!', 'error');
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
  showToast(editingApdId ? 'Data APD berhasil diperbarui' : 'APD berhasil ditambahkan');
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
  showToast('APD berhasil dihapus', 'info');
}

function renderAPDCards() {
  const grid = document.getElementById('apd-card-grid');
  if (db.apd.length === 0) {
    grid.innerHTML = `<div class="empty-state" style="grid-column:1/-1"><div class="empty-state-icon">🦺</div><h3>Belum ada data APD</h3><p>Klik "+ Tambah APD" untuk mulai</p></div>`;
    return;
  }
  grid.innerHTML = db.apd.map(a => {
    const stokStatus = a.stok <= 0 ? 'badge-kritis' : a.stok <= a.stokMin ? 'badge-perhatian' : 'badge-aman';
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
    const stokStatus = a.stok <= 0 ? 'badge-kritis' : a.stok <= a.stokMin ? 'badge-perhatian' : 'badge-aman';
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
  if (!lines.length) return showToast('Daftar role tidak boleh kosong!', 'error');
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
  if (!apdId || qty <= 0) return showToast('Mohon isi APD dan jumlah breakdown role!', 'error');
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
  showToast('Rencana pembelian dihapus', 'info');
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
      <td style="white-space:nowrap">
        <button class="btn btn-outline btn-sm" onclick="detailRencana('${r.id}')" title="Detail" style="margin-right:4px">👁</button>
        <button class="btn btn-outline btn-sm" onclick="editRencana('${r.id}')" title="Edit" style="margin-right:4px">✏️</button>
        <button class="btn btn-danger btn-sm" onclick="deleteRencana('${r.id}')" title="Hapus">🗑</button>
      </td>
    </tr>`;
  }).join('');
  document.getElementById('total-rencana').textContent = totalQty;
}

// ════════════════ EXPORT PDF RENCANA ════════════════
function exportRencanaPDF() {
  if (!db.rencana.length) return showToast('Belum ada rencana pembelian untuk diexport!', 'warn');
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
  if (!apdId || qty <= 0) return showToast('Mohon isi APD dan jumlah!', 'error');
  const a = getApdById(apdId);
  db.terima.push({ id: genId(), apdId, namaApd: a?.nama, satuan: a?.satuan, tgl, qty, catatan });
  // Update stok
  const idx = db.apd.findIndex(x => x.id === apdId);
  if (idx >= 0) db.apd[idx].stok += qty;
  saveDB();
  closeModal('modal-terima');
  ['trm-qty','trm-catatan'].forEach(id => document.getElementById(id).value = '');
  renderTerima();
  showToast('Penerimaan barang berhasil dicatat & stok diperbarui');
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
    <td style="max-width:160px;word-break:break-word;color:var(--text-muted);font-size:12px">${t.catatan||'-'}</td>
    <td style="white-space:nowrap">
      <button class="btn btn-outline btn-sm" onclick="detailTerima('${t.id}')" title="Detail" style="margin-right:4px">👁</button>
      <button class="btn btn-outline btn-sm" onclick="editTerima('${t.id}')" title="Edit" style="margin-right:4px">✏️</button>
      <button class="btn btn-danger btn-sm" onclick="deleteTerima('${t.id}')" title="Hapus">🗑</button>
    </td>
  </tr>`).join('');
}

function deleteTerima(id) {
  if (!confirm('Hapus record terima barang ini? Stok tidak akan dikurangi kembali.')) return;
  db.terima = db.terima.filter(t => t.id !== id);
  saveDB();
  renderTerima();
  showToast('Data penerimaan dihapus', 'info');
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
  if (!date || !no || !desc) { showToast('Tanggal, No. JCN, dan Uraian wajib diisi.', 'error'); return; }
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
  if (!date || !no || !desc) { showToast('Semua field wajib diisi.', 'error'); return; }
  const idx = db.jcn.findIndex(j => j.id === id);
  if (idx > -1) db.jcn[idx] = { id, date, no, desc, status };
  saveDB();
  closeModal('modal-edit-jcn');
  renderJCN();
  showToast('No. JCN berhasil diperbarui');
}

function toggleJCNStatus(id) {
  const idx = db.jcn.findIndex(j => j.id === id);
  if (idx < 0) return;
  db.jcn[idx].status = db.jcn[idx].status === 'Sudah Dipakai' ? 'Belum Dipakai' : 'Sudah Dipakai';
  saveDB(); renderJCN();
}

function exportJCNCSV() {
  if (!db.jcn.length) { showToast('Tidak ada data untuk diekspor.', 'warn'); return; }
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
      <td><span style="font-family:monospace;font-size:13px;font-weight:600;color:var(--text-strong);background:var(--bg);padding:3px 8px;border-radius:5px;border:1px solid var(--border)">${j.no}</span></td>
      <td style="max-width:280px;word-break:break-word;font-size:13px">${j.desc}</td>
      <td>
        <span class="badge ${used ? 'badge-info' : 'badge-perhatian'}" style="cursor:pointer" onclick="toggleJCNStatus('${j.id}')" title="Klik untuk ubah status">
          ${j.status}
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


// ════════════════ DARK MODE ════════════════
function applyTheme(theme, skipChartRender) {
  const btn = document.getElementById('theme-toggle-btn');
  if (theme === 'dark') {
    document.documentElement.setAttribute('data-theme', 'dark');
    if (btn) { btn.textContent = '☀️'; btn.title = 'Mode Terang'; }
  } else {
    document.documentElement.removeAttribute('data-theme');
    if (btn) { btn.textContent = '🌙'; btn.title = 'Mode Gelap'; }
  }
  if (skipChartRender) return; // saat init awal, renderDashboard() di bawah sudah menangani chart — hindari panggil sebelum chart vars siap
  updateChartsTheme();
}

function toggleTheme() {
  const isDark = document.documentElement.getAttribute('data-theme') === 'dark';
  const next = isDark ? 'light' : 'dark';
  localStorage.setItem('promanage_theme', next);
  applyTheme(next);
}

function updateChartsTheme() {
  // Chart.js tidak membaca CSS variable, jadi grid/label warna disesuaikan manual saat tema berganti
  if (typeof Chart === 'undefined') return; // CDN Chart.js belum/gagal dimuat — lewati dengan aman
  const dark = document.documentElement.getAttribute('data-theme') === 'dark';
  Chart.defaults.color = dark ? '#9099AD' : '#6B7080';
  Chart.defaults.borderColor = dark ? '#2A3550' : '#F0F2F8';
  if (document.getElementById('page-dashboard')?.classList.contains('active')) {
    renderDashboardCharts();
  }
}

function setDate() {
  const now = new Date();
  document.getElementById('topbar-date').textContent = now.toLocaleDateString('id-ID', { weekday:'long', year:'numeric', month:'long', day:'numeric' });
}

loadDB();
applyTheme(localStorage.getItem('promanage_theme') || 'light', true);
setDate();
renderDashboard();

// ════════════════ DETAIL & EDIT FUNCTIONS ════════════════

function detailRow(label, value) {
  return `<div style="display:flex;gap:12px;padding:10px 0;border-bottom:1px solid var(--border)">
    <div style="width:140px;font-size:12px;font-weight:600;color:var(--text-muted);flex-shrink:0">${label}</div>
    <div style="font-size:13px;color:var(--text);flex:1">${value||'-'}</div>
  </div>`;
}

// ── PO ──
function detailPO(id) {
  const p = db.po.find(x => x.id === id);
  if (!p) return;
  const total = getTotalTagihan(id);
  const sisa = (Number(p.nilai)||0) - total;
  const pct = p.nilai > 0 ? Math.min(100,(total/p.nilai*100)) : 0;
  const cls = pctClass(pct);
  document.getElementById('detail-po-content').innerHTML =
    detailRow('No. PO', `<strong>${p.noPO}</strong>`) +
    detailRow('Tanggal', p.date) +
    detailRow('Nama / Deskripsi', p.nama) +
    detailRow('Nilai Total PO', fmtRp(p.nilai)) +
    detailRow('Total Ditagihkan', `<span style="color:var(--gold);font-weight:700">${fmtRp(total)}</span>`) +
    detailRow('Sisa', `<span style="color:${sisa<0?'var(--danger)':'var(--success)'};font-weight:700">${fmtRp(sisa)}</span>`) +
    detailRow('% Terpakai', `<div style="display:flex;align-items:center;gap:10px"><div class="progress-track" style="flex:1"><div class="progress-fill ${cls}" style="width:${pct}%"></div></div><span style="font-weight:700">${pct.toFixed(1)}%</span></div>`) +
    detailRow('Status', `<span class="badge ${p.status==='Aktif'?'badge-aman':p.status==='Selesai'?'badge-info':'badge-info'}">${p.status}</span>`) +
    detailRow('Catatan', p.catatan);
  openModal('modal-detail-po');
}

function editPO(id) {
  const p = db.po.find(x => x.id === id);
  if (!p) return;
  document.getElementById('epo-id').value = id;
  document.getElementById('epo-no').value = p.noPO;
  document.getElementById('epo-date').value = p.date;
  document.getElementById('epo-name').value = p.nama;
  document.getElementById('epo-nilai').value = p.nilai;
  document.getElementById('epo-status').value = p.status;
  document.getElementById('epo-catatan').value = p.catatan||'';
  openModal('modal-edit-po');
}

function saveEditPO() {
  const id = document.getElementById('epo-id').value;
  const idx = db.po.findIndex(x => x.id === id);
  if (idx < 0) return;
  const noPO = document.getElementById('epo-no').value.trim();
  const nama = document.getElementById('epo-name').value.trim();
  const nilai = Number(document.getElementById('epo-nilai').value)||0;
  if (!noPO || !nama || !nilai) return showToast('Mohon isi semua field wajib!', 'error');
  db.po[idx] = { ...db.po[idx], noPO, date: document.getElementById('epo-date').value, nama, nilai, status: document.getElementById('epo-status').value, catatan: document.getElementById('epo-catatan').value };
  // Update noPO & namaPO in tagihan
  db.tagihan.forEach(t => { if (t.poId === id) { t.noPO = noPO; t.namaPO = nama; } });
  saveDB();
  closeModal('modal-edit-po');
  renderPOList();
  showToast('PO berhasil diperbarui');
}

// ── TAGIHAN ──
function detailTagihan(id) {
  const t = db.tagihan.find(x => x.id === id);
  if (!t) return;
  const po = getPoById(t.poId);
  const total = po ? getTotalTagihan(t.poId) : 0;
  const pct = po && po.nilai > 0 ? (total/po.nilai*100) : 0;
  document.getElementById('detail-tagihan-content').innerHTML =
    detailRow('No. PO', `<strong>${t.noPO||'-'}</strong>`) +
    detailRow('Nama PO', t.namaPO) +
    detailRow('Tanggal', t.tanggal) +
    detailRow('Periode', t.periode) +
    detailRow('Nominal Tagihan', `<strong style="color:var(--text-strong)">${fmtRp(t.nominal)}</strong>`) +
    detailRow('Keterangan', t.ket) +
    detailRow('Status PO', `<span class="badge ${pct>=90?'badge-kritis':pct>=70?'badge-perhatian':'badge-aman'}">${pct.toFixed(0)}% terpakai</span>`);
  openModal('modal-detail-tagihan');
}

// ── RENCANA ──
function detailRencana(id) {
  const r = db.rencana.find(x => x.id === id);
  if (!r) return;
  const breakdownHtml = r.breakdown && Object.keys(r.breakdown).length
    ? Object.entries(r.breakdown).map(([role,q]) => `<div style="display:flex;justify-content:space-between;padding:4px 0"><span>${role}</span><strong>${q}</strong></div>`).join('')
    : '-';
  document.getElementById('detail-rencana-content').innerHTML =
    detailRow('Nama APD', `<strong>${r.namaApd}</strong>`) +
    detailRow('Stok Saat Ini', `${r.stokNow} ${r.satuan}`) +
    detailRow('Qty Total', `<strong style="color:var(--text-strong);font-size:16px">${r.qty} ${r.satuan}</strong>`) +
    detailRow('Breakdown Role', `<div>${breakdownHtml}</div>`) +
    detailRow('Catatan', r.catatan);
  openModal('modal-detail-rencana');
}

function editRencana(id) {
  const r = db.rencana.find(x => x.id === id);
  if (!r) return;
  document.getElementById('er-id').value = id;
  document.getElementById('er-nama').value = r.namaApd;
  document.getElementById('er-qty').value = r.qty;
  document.getElementById('er-satuan').value = r.satuan;
  document.getElementById('er-catatan').value = r.catatan||'';
  openModal('modal-edit-rencana');
}

function saveEditRencana() {
  const id = document.getElementById('er-id').value;
  const idx = db.rencana.findIndex(x => x.id === id);
  if (idx < 0) return;
  const qty = Number(document.getElementById('er-qty').value)||0;
  if (!qty) return showToast('Qty harus diisi!', 'error');
  db.rencana[idx] = { ...db.rencana[idx], qty, catatan: document.getElementById('er-catatan').value };
  saveDB();
  closeModal('modal-edit-rencana');
  renderRencana();
  showToast('Rencana pembelian berhasil diperbarui');
}

// ── TERIMA BARANG ──
function detailTerima(id) {
  const t = db.terima.find(x => x.id === id);
  if (!t) return;
  document.getElementById('detail-terima-content').innerHTML =
    detailRow('Nama APD', `<strong>${t.namaApd}</strong>`) +
    detailRow('Tanggal Terima', t.tgl) +
    detailRow('Qty Diterima', `<strong style="color:var(--success);font-size:16px">${t.qty} ${t.satuan||''}</strong>`) +
    detailRow('Catatan', t.catatan);
  openModal('modal-detail-terima');
}

function editTerima(id) {
  const t = db.terima.find(x => x.id === id);
  if (!t) return;
  document.getElementById('etrm-id').value = id;
  document.getElementById('etrm-nama').value = t.namaApd;
  document.getElementById('etrm-tgl').value = t.tgl;
  document.getElementById('etrm-qty').value = t.qty;
  document.getElementById('etrm-catatan').value = t.catatan||'';
  openModal('modal-edit-terima');
}

function saveEditTerima() {
  const id = document.getElementById('etrm-id').value;
  const idx = db.terima.findIndex(x => x.id === id);
  if (idx < 0) return;
  const oldQty = db.terima[idx].qty;
  const newQty = Number(document.getElementById('etrm-qty').value)||0;
  const tgl = document.getElementById('etrm-tgl').value;
  if (!newQty || !tgl) return showToast('Mohon isi semua field wajib!', 'error');
  const diff = newQty - oldQty;
  // Adjust stok APD
  const apdIdx = db.apd.findIndex(a => a.id === db.terima[idx].apdId);
  if (apdIdx >= 0) db.apd[apdIdx].stok += diff;
  db.terima[idx] = { ...db.terima[idx], tgl, qty: newQty, catatan: document.getElementById('etrm-catatan').value };
  saveDB();
  closeModal('modal-edit-terima');
  renderTerima();
  showToast('Data penerimaan berhasil diperbarui');
}


// ════════════════ DASHBOARD CHARTS ════════════════
let chartTagihanBulan = null;
let chartPoCompare    = null;
let chartDonut        = null;
let chartKumulatif    = null;

function destroyChart(c) { if (c) { try { c.destroy(); } catch(e) {} } return null; }

function renderDashboardCharts() {
  // ── DATA PREP ──
  // 1. Tagihan per bulan
  const bulanMap = {};
  db.tagihan.forEach(t => {
    if (!t.tanggal) return;
    const [y, m] = t.tanggal.split('-');
    const key = `${y}-${m}`;
    bulanMap[key] = (bulanMap[key] || 0) + (Number(t.nominal) || 0);
  });
  const bulanKeys = Object.keys(bulanMap).sort();
  const bulanLabels = bulanKeys.map(k => {
    const [y, m] = k.split('-');
    const names = ['Jan','Feb','Mar','Apr','Mei','Jun','Jul','Agu','Sep','Okt','Nov','Des'];
    return `${names[parseInt(m)-1]} ${y}`;
  });
  const bulanValues = bulanKeys.map(k => bulanMap[k]);

  // 2. Per PO comparison
  const poLabels = db.po.map(p => p.noPO || p.nama);
  const poNilai  = db.po.map(p => Number(p.nilai) || 0);
  const poTagih  = db.po.map(p => getTotalTagihan(p.id));
  const poSisa   = db.po.map(p => Math.max(0, (Number(p.nilai)||0) - getTotalTagihan(p.id)));

  // 3. Donut
  const totalNilai = db.po.reduce((s,p) => s + (Number(p.nilai)||0), 0);
  const totalTagih = db.po.reduce((s,p) => s + getTotalTagihan(p.id), 0);
  const totalSisa  = Math.max(0, totalNilai - totalTagih);

  // 4. Kumulatif
  let cumul = 0;
  const cumulData = bulanKeys.map(k => { cumul += bulanMap[k]; return cumul; });

  // ── CHART 1: Tagihan per Bulan (Bar) ──
  const ctx1 = document.getElementById('chart-tagihan-bulan');
  chartTagihanBulan = destroyChart(chartTagihanBulan);
  if (ctx1) {
    chartTagihanBulan = new Chart(ctx1, {
      type: 'bar',
      data: {
        labels: bulanLabels.length ? bulanLabels : ['Belum ada data'],
        datasets: [{
          label: 'Total Tagihan',
          data: bulanValues.length ? bulanValues : [0],
          backgroundColor: 'rgba(74,111,165,0.75)',
          borderColor: '#4A6FA5',
          borderWidth: 1.5,
          borderRadius: 6,
        }]
      },
      options: {
        responsive: true, maintainAspectRatio: false,
        plugins: { legend: { display: false }, tooltip: { callbacks: { label: ctx => 'Rp ' + ctx.parsed.y.toLocaleString('id-ID') } } },
        scales: {
          x: { grid: { display: false }, ticks: { font: { size: 11 } } },
          y: { grid: { color: Chart.defaults.borderColor }, ticks: { font: { size: 11 }, callback: v => 'Rp ' + (v/1e6).toFixed(0) + 'jt' } }
        }
      }
    });
  }

  // ── CHART 2: Per PO Comparison (Grouped Bar) ──
  const ctx2 = document.getElementById('chart-po-compare');
  chartPoCompare = destroyChart(chartPoCompare);
  if (ctx2) {
    chartPoCompare = new Chart(ctx2, {
      type: 'bar',
      data: {
        labels: poLabels.length ? poLabels : ['Belum ada data'],
        datasets: [
          { label: 'Nilai PO', data: poNilai, backgroundColor: 'rgba(74,111,165,0.7)', borderRadius: 4 },
          { label: 'Ditagihkan', data: poTagih, backgroundColor: 'rgba(240,165,0,0.8)', borderRadius: 4 },
          { label: 'Sisa', data: poSisa, backgroundColor: 'rgba(46,204,113,0.75)', borderRadius: 4 },
        ]
      },
      options: {
        responsive: true, maintainAspectRatio: false,
        plugins: {
          legend: { position: 'bottom', labels: { font: { size: 11 }, boxWidth: 12 } },
          tooltip: { callbacks: { label: ctx => ctx.dataset.label + ': Rp ' + ctx.parsed.y.toLocaleString('id-ID') } }
        },
        scales: {
          x: { grid: { display: false }, ticks: { font: { size: 10 } } },
          y: { grid: { color: Chart.defaults.borderColor }, ticks: { font: { size: 11 }, callback: v => 'Rp ' + (v/1e6).toFixed(0) + 'jt' } }
        }
      }
    });
  }

  // ── CHART 3: Donut Anggaran ──
  const ctx3 = document.getElementById('chart-donut-anggaran');
  chartDonut = destroyChart(chartDonut);
  if (ctx3) {
    chartDonut = new Chart(ctx3, {
      type: 'doughnut',
      data: {
        labels: ['Sudah Ditagihkan', 'Sisa Anggaran'],
        datasets: [{
          data: [totalTagih || 0, totalSisa || (totalNilai > 0 ? totalNilai : 1)],
          backgroundColor: ['rgba(240,165,0,0.85)', 'rgba(46,204,113,0.75)'],
          borderColor: ['#F0A500', '#2ECC71'],
          borderWidth: 2,
          hoverOffset: 8
        }]
      },
      options: {
        responsive: true, maintainAspectRatio: false,
        cutout: '62%',
        plugins: {
          legend: { position: 'bottom', labels: { font: { size: 11 }, boxWidth: 12 } },
          tooltip: { callbacks: { label: ctx => ctx.label + ': Rp ' + ctx.parsed.toLocaleString('id-ID') } }
        }
      }
    });
  }

  // ── CHART 4: Kumulatif Tagihan (Line) ──
  const ctx4 = document.getElementById('chart-kumulatif');
  chartKumulatif = destroyChart(chartKumulatif);
  if (ctx4) {
    chartKumulatif = new Chart(ctx4, {
      type: 'line',
      data: {
        labels: bulanLabels.length ? bulanLabels : ['Belum ada data'],
        datasets: [{
          label: 'Kumulatif Tagihan',
          data: cumulData.length ? cumulData : [0],
          fill: true,
          backgroundColor: 'rgba(74,111,165,0.10)',
          borderColor: '#4A6FA5',
          borderWidth: 2.5,
          pointBackgroundColor: '#4A6FA5',
          pointRadius: 4,
          tension: 0.35
        }]
      },
      options: {
        responsive: true, maintainAspectRatio: false,
        plugins: { legend: { display: false }, tooltip: { callbacks: { label: ctx => 'Rp ' + ctx.parsed.y.toLocaleString('id-ID') } } },
        scales: {
          x: { grid: { display: false }, ticks: { font: { size: 11 } } },
          y: { grid: { color: Chart.defaults.borderColor }, ticks: { font: { size: 11 }, callback: v => 'Rp ' + (v/1e6).toFixed(0) + 'jt' } }
        }
      }
    });
  }
  hideDashboardChartSkeletons();
}


// ════════════════ PENGELUARAN BARANG ════════════════
function populateKeluarModal() {
  const sel = document.getElementById('klr-apd-id');
  sel.innerHTML = db.apd.map(a => `<option value="${a.id}">${a.nama} (stok: ${a.stok} ${a.satuan})</option>`).join('');
  document.getElementById('klr-tgl').value = new Date().toISOString().split('T')[0];
  document.getElementById('klr-qty').value = '';
  document.getElementById('klr-ket').value = '';
  updateKeluarStokInfo();
}

function updateKeluarStokInfo() {
  const apdId = document.getElementById('klr-apd-id').value;
  const qty   = Number(document.getElementById('klr-qty').value) || 0;
  const apd   = getApdById(apdId);
  const info  = document.getElementById('klr-stok-info');
  if (!apd) { info.textContent = ''; return; }
  const sisaStok = apd.stok - qty;
  const warna = sisaStok < 0 ? 'var(--danger)' : sisaStok <= apd.stokMin ? 'var(--gold)' : 'var(--success)';
  info.innerHTML = `Stok saat ini: <strong>${apd.stok} ${apd.satuan}</strong> &nbsp;→&nbsp; Setelah keluar: <strong style="color:${warna}">${sisaStok} ${apd.satuan}</strong>${sisaStok < 0 ? ' <span style="color:var(--danger)">⚠️ Melebihi stok!</span>' : ''}`;
}

function saveKeluar() {
  const apdId  = document.getElementById('klr-apd-id').value;
  const tgl    = document.getElementById('klr-tgl').value;
  const qty    = Number(document.getElementById('klr-qty').value) || 0;
  const ket    = document.getElementById('klr-ket').value;
  if (!apdId || !tgl || qty <= 0) return showToast('Mohon isi APD, tanggal, dan jumlah yang valid!', 'error');
  const apd = getApdById(apdId);
  if (apd.stok - qty < 0) {
    if (!confirm('Stok akan menjadi negatif. Lanjutkan?')) return;
  }
  db.keluar.push({ id: genId(), apdId, namaApd: apd?.nama, satuan: apd?.satuan, tgl, qty, ket });
  const idx = db.apd.findIndex(a => a.id === apdId);
  if (idx >= 0) db.apd[idx].stok -= qty;
  saveDB();
  closeModal('modal-keluar');
  renderKeluar();
  renderStok();
  showToast('Pengeluaran barang berhasil dicatat & stok dikurangi');
}

function deleteKeluar(id) {
  if (!confirm('Hapus catatan pengeluaran ini? Stok tidak akan dikembalikan secara otomatis.')) return;
  db.keluar = db.keluar.filter(k => k.id !== id);
  saveDB();
  renderKeluar();
  showToast('Data pengeluaran dihapus', 'info');
}

function editKeluar(id) {
  const k = db.keluar.find(x => x.id === id);
  if (!k) return;
  document.getElementById('eklr-id').value = id;
  document.getElementById('eklr-nama').value = k.namaApd;
  document.getElementById('eklr-tgl').value = k.tgl;
  document.getElementById('eklr-qty').value = k.qty;
  document.getElementById('eklr-ket').value = k.ket || '';
  openModal('modal-edit-keluar');
}

function saveEditKeluar() {
  const id  = document.getElementById('eklr-id').value;
  const idx = db.keluar.findIndex(x => x.id === id);
  if (idx < 0) return;
  const oldQty = db.keluar[idx].qty;
  const newQty = Number(document.getElementById('eklr-qty').value) || 0;
  const tgl    = document.getElementById('eklr-tgl').value;
  if (!newQty || !tgl) return showToast('Mohon isi semua field wajib!', 'error');
  const diff = newQty - oldQty; // selisih pengeluaran
  const apdIdx = db.apd.findIndex(a => a.id === db.keluar[idx].apdId);
  if (apdIdx >= 0) db.apd[apdIdx].stok -= diff;
  db.keluar[idx] = { ...db.keluar[idx], tgl, qty: newQty, ket: document.getElementById('eklr-ket').value };
  saveDB();
  closeModal('modal-edit-keluar');
  renderKeluar();
  renderStok();
  showToast('Data pengeluaran berhasil diperbarui');
}

function detailKeluar(id) {
  const k = db.keluar.find(x => x.id === id);
  if (!k) return;
  const apd = getApdById(k.apdId);
  document.getElementById('detail-keluar-content').innerHTML =
    detailRow('Nama APD', `<strong>${k.namaApd}</strong>`) +
    detailRow('Tanggal Keluar', k.tgl) +
    detailRow('Qty Keluar', `<strong style="color:var(--danger);font-size:16px">${k.qty} ${k.satuan||''}</strong>`) +
    detailRow('Stok Saat Ini', apd ? `${apd.stok} ${apd.satuan}` : '-') +
    detailRow('Penerima / Keterangan', k.ket || '-');
  openModal('modal-detail-keluar');
}

function renderKeluar() {
  const tbody = document.getElementById('tbl-keluar-body');
  if (!tbody) return;
  if (db.keluar.length === 0) {
    tbody.innerHTML = `<tr><td colspan="6" style="text-align:center;padding:40px;color:var(--text-muted)">Belum ada catatan pengeluaran barang.</td></tr>`;
    return;
  }
  const sorted = [...db.keluar].sort((a,b) => b.tgl > a.tgl ? 1 : -1);
  tbody.innerHTML = sorted.map(k => `<tr>
    <td>${k.tgl}</td>
    <td><strong>${k.namaApd}</strong></td>
    <td><strong style="color:var(--danger)">${k.qty}</strong></td>
    <td>${k.satuan||'-'}</td>
    <td style="max-width:180px;word-break:break-word;color:var(--text-muted);font-size:12px">${k.ket||'-'}</td>
    <td style="white-space:nowrap">
      <button class="btn btn-outline btn-sm" onclick="detailKeluar('${k.id}')" title="Detail" style="margin-right:4px">👁</button>
      <button class="btn btn-outline btn-sm" onclick="editKeluar('${k.id}')" title="Edit" style="margin-right:4px">✏️</button>
      <button class="btn btn-danger btn-sm" onclick="deleteKeluar('${k.id}')" title="Hapus">🗑</button>
    </td>
  </tr>`).join('');
}

</script>
</body>
</html>
