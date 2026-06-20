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
    height: 100vh;
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
    flex-shrink: 0;
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

  .sidebar-nav { flex: 1; min-height: 0; padding: 16px 12px; overflow-y: auto; }
  .sidebar-nav::-webkit-scrollbar { width: 6px; }
  .sidebar-nav::-webkit-scrollbar-track { background: transparent; }
  .sidebar-nav::-webkit-scrollbar-thumb { background: rgba(255,255,255,0.15); border-radius: 99px; }
  .sidebar-nav::-webkit-scrollbar-thumb:hover { background: rgba(255,255,255,0.28); }
  .sidebar-nav { scrollbar-width: thin; scrollbar-color: rgba(255,255,255,0.15) transparent; }
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
    flex-shrink: 0;
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
  th[data-sort-key] {
    cursor: pointer;
    user-select: none;
    transition: color .15s, background .15s;
  }
  th[data-sort-key]:hover { color: var(--steel); background: var(--mint); }
  th[data-sort-key].sort-asc,
  th[data-sort-key].sort-desc { color: var(--steel); }
  .sort-icon {
    display: inline-block;
    margin-left: 4px;
    font-size: 9px;
    opacity: .45;
  }
  th[data-sort-key].sort-asc .sort-icon,
  th[data-sort-key].sort-desc .sort-icon { opacity: 1; }
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
    .jcn-add-row { grid-template-columns: 1fr !important; }
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

    <div class="nav-label">Operasional</div>
    <div class="nav-item" onclick="showPage('operasional', this)">
      <span class="nav-icon">💰</span> Biaya Operasional
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

      <!-- BIAYA OPERASIONAL CARD -->
      <div id="dash-ops-card" style="margin-bottom:24px"></div>

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
                <th data-sort-key="noPO" onclick="toggleSort('po-list','noPO',renderPOList)">No. PO <span class="sort-icon">⇅</span></th>
                <th data-sort-key="nama" onclick="toggleSort('po-list','nama',renderPOList)">Nama / Deskripsi <span class="sort-icon">⇅</span></th>
                <th data-sort-key="nilai" onclick="toggleSort('po-list','nilai',renderPOList)">Nilai PO <span class="sort-icon">⇅</span></th>
                <th data-sort-key="total" onclick="toggleSort('po-list','total',renderPOList)">Total Ditagihkan <span class="sort-icon">⇅</span></th>
                <th data-sort-key="sisa" onclick="toggleSort('po-list','sisa',renderPOList)">Sisa <span class="sort-icon">⇅</span></th>
                <th data-sort-key="pct" onclick="toggleSort('po-list','pct',renderPOList)">% Terpakai <span class="sort-icon">⇅</span></th>
                <th data-sort-key="status" onclick="toggleSort('po-list','status',renderPOList)">Status <span class="sort-icon">⇅</span></th>
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
                <th data-sort-key="tanggal" onclick="toggleSort('tagihan','tanggal',renderTagihan)">Tanggal <span class="sort-icon">⇅</span></th>
                <th data-sort-key="noPO" onclick="toggleSort('tagihan','noPO',renderTagihan)">No. PO <span class="sort-icon">⇅</span></th>
                <th data-sort-key="namaPO" onclick="toggleSort('tagihan','namaPO',renderTagihan)">Nama PO <span class="sort-icon">⇅</span></th>
                <th data-sort-key="periode" onclick="toggleSort('tagihan','periode',renderTagihan)">Periode <span class="sort-icon">⇅</span></th>
                <th data-sort-key="nominal" onclick="toggleSort('tagihan','nominal',renderTagihan)">Nominal Tagihan <span class="sort-icon">⇅</span></th>
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
          <div class="jcn-add-row" style="display:grid;grid-template-columns:150px 1fr 170px;gap:12px;align-items:end">
            <div class="form-group" style="margin:0">
              <label>Tanggal *</label>
              <input type="date" id="jcn-date">
            </div>
            <div class="form-group" style="margin:0">
              <label>No. PO (untuk Auto No. JCN)</label>
              <select id="jcn-po">
                <option value="">— Pilih No. PO —</option>
              </select>
            </div>
            <div class="form-group" style="margin:0">
              <label>Status</label>
              <select id="jcn-status">
                <option value="Belum Dipakai">Belum Dipakai</option>
                <option value="Sudah Dipakai">Sudah Dipakai</option>
              </select>
            </div>
          </div>
          <div class="jcn-add-row" style="display:grid;grid-template-columns:1fr 1fr auto;gap:12px;align-items:end;margin-top:12px">
            <div class="form-group" style="margin:0">
              <label>No. JCN *</label>
              <div style="display:flex;gap:6px">
                <input type="text" id="jcn-no" placeholder="JCN/05/05/2026/8100002321/005" style="flex:1">
                <button type="button" class="btn btn-outline btn-sm" onclick="generateJCNNo()" title="Buat No. JCN otomatis dari Tanggal, No. PO & urutan berikutnya" style="white-space:nowrap">🔄 Auto</button>
              </div>
            </div>
            <div class="form-group" style="margin:0">
              <label>Uraian Pekerjaan *</label>
              <input type="text" id="jcn-desc" placeholder="Deskripsi pekerjaan...">
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
                <th data-sort-key="date" onclick="toggleSort('jcn','date',renderJCN)">Tanggal <span class="sort-icon">⇅</span></th>
                <th data-sort-key="no" onclick="toggleSort('jcn','no',renderJCN)">No. JCN <span class="sort-icon">⇅</span></th>
                <th data-sort-key="desc" onclick="toggleSort('jcn','desc',renderJCN)">Uraian Pekerjaan <span class="sort-icon">⇅</span></th>
                <th data-sort-key="status" onclick="toggleSort('jcn','status',renderJCN)">Status <span class="sort-icon">⇅</span></th>
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
                <th data-sort-key="nama" onclick="toggleSort('stok','nama',renderStok)">Nama APD <span class="sort-icon">⇅</span></th>
                <th data-sort-key="kategori" onclick="toggleSort('stok','kategori',renderStok)">Kategori <span class="sort-icon">⇅</span></th>
                <th data-sort-key="satuan" onclick="toggleSort('stok','satuan',renderStok)">Satuan <span class="sort-icon">⇅</span></th>
                <th data-sort-key="stok" onclick="toggleSort('stok','stok',renderStok)">Stok Saat Ini <span class="sort-icon">⇅</span></th>
                <th data-sort-key="stokMin" onclick="toggleSort('stok','stokMin',renderStok)">Stok Min <span class="sort-icon">⇅</span></th>
                <th data-sort-key="statusStok" onclick="toggleSort('stok','statusStok',renderStok)">Status Stok <span class="sort-icon">⇅</span></th>
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
                <th data-sort-key="namaApd" onclick="toggleSort('rencana','namaApd',renderRencana)">Nama APD <span class="sort-icon">⇅</span></th>
                <th data-sort-key="stokNow" onclick="toggleSort('rencana','stokNow',renderRencana)">Stok Saat Ini <span class="sort-icon">⇅</span></th>
                <th>Breakdown Role</th>
                <th data-sort-key="qty" onclick="toggleSort('rencana','qty',renderRencana)">Qty Total <span class="sort-icon">⇅</span></th>
                <th data-sort-key="satuan" onclick="toggleSort('rencana','satuan',renderRencana)">Satuan <span class="sort-icon">⇅</span></th>
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
                <th data-sort-key="tgl" onclick="toggleSort('terima','tgl',renderTerima)">Tgl Terima <span class="sort-icon">⇅</span></th>
                <th data-sort-key="namaApd" onclick="toggleSort('terima','namaApd',renderTerima)">Nama APD <span class="sort-icon">⇅</span></th>
                <th data-sort-key="qty" onclick="toggleSort('terima','qty',renderTerima)">Qty Diterima <span class="sort-icon">⇅</span></th>
                <th data-sort-key="satuan" onclick="toggleSort('terima','satuan',renderTerima)">Satuan <span class="sort-icon">⇅</span></th>
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
                <th data-sort-key="tgl" onclick="toggleSort('keluar','tgl',renderKeluar)">Tanggal <span class="sort-icon">⇅</span></th>
                <th data-sort-key="namaApd" onclick="toggleSort('keluar','namaApd',renderKeluar)">Nama APD <span class="sort-icon">⇅</span></th>
                <th data-sort-key="qty" onclick="toggleSort('keluar','qty',renderKeluar)">Qty Keluar <span class="sort-icon">⇅</span></th>
                <th data-sort-key="satuan" onclick="toggleSort('keluar','satuan',renderKeluar)">Satuan <span class="sort-icon">⇅</span></th>
                <th>Penerima / Keterangan</th>
                <th>Aksi</th>
              </tr>
            </thead>
            <tbody id="tbl-keluar-body"></tbody>
          </table>
        </div>
      </div>
    </div>

    <!-- ════════════════════════════════ BIAYA OPERASIONAL ════════════════════════════════ -->
    <div id="page-operasional" class="page">
      <div class="page-header">
        <div>
          <h1>Biaya Operasional</h1>
          <p>Pencatatan biaya operasional untuk penagihan perusahaan</p>
        </div>
        <div class="page-header-actions">
          <button class="btn btn-outline" onclick="exportOperasionalPDF()">📄 Export PDF</button>
          <button class="btn btn-primary" onclick="openModal('modal-add-operasional')">＋ Tambah Biaya</button>
        </div>
      </div>

      <div class="grid-4" id="operasional-stats"></div>

      <!-- FILTER BAR -->
      <div class="card" style="margin-bottom:20px">
        <div class="card-body" style="padding:16px 20px">
          <div style="display:grid;grid-template-columns:1fr 1fr 1fr auto;gap:12px;align-items:end">
            <div class="form-group" style="margin:0">
              <label>Dari Tanggal</label>
              <input type="date" id="filter-ops-dari" oninput="renderOperasional()" style="padding:9px 12px;border:1.5px solid var(--border);border-radius:var(--radius-sm);font-size:13px;font-family:inherit;outline:none;width:100%" onfocus="this.style.borderColor='var(--steel)'" onblur="this.style.borderColor='var(--border)'">
            </div>
            <div class="form-group" style="margin:0">
              <label>Sampai Tanggal</label>
              <input type="date" id="filter-ops-sampai" oninput="renderOperasional()" style="padding:9px 12px;border:1.5px solid var(--border);border-radius:var(--radius-sm);font-size:13px;font-family:inherit;outline:none;width:100%" onfocus="this.style.borderColor='var(--steel)'" onblur="this.style.borderColor='var(--border)'">
            </div>
            <div class="form-group" style="margin:0">
              <label>Cari Uraian</label>
              <input type="text" id="filter-ops-uraian" placeholder="Cari uraian biaya..." oninput="renderOperasional()" style="padding:9px 12px;border:1.5px solid var(--border);border-radius:var(--radius-sm);font-size:13px;font-family:inherit;outline:none;width:100%" onfocus="this.style.borderColor='var(--steel)'" onblur="this.style.borderColor='var(--border)'">
            </div>
            <button class="btn btn-outline" onclick="resetFilterOperasional()" style="white-space:nowrap">🔄 Reset</button>
          </div>
        </div>
      </div>

      <div class="card">
        <div class="card-body table-wrap">
          <table id="tbl-operasional">
            <thead>
              <tr>
                <th style="width:40px">No</th>
                <th data-sort-key="tanggal" onclick="toggleSort('operasional','tanggal',renderOperasional)">Tanggal <span class="sort-icon">⇅</span></th>
                <th data-sort-key="uraian" onclick="toggleSort('operasional','uraian',renderOperasional)">Uraian <span class="sort-icon">⇅</span></th>
                <th data-sort-key="jumlah" onclick="toggleSort('operasional','jumlah',renderOperasional)">Jumlah <span class="sort-icon">⇅</span></th>
                <th>Keterangan</th>
                <th style="width:90px">Bukti</th>
                <th style="width:130px">Aksi</th>
              </tr>
            </thead>
            <tbody id="tbl-operasional-body"></tbody>
          </table>
          <div id="operasional-empty" style="display:none;text-align:center;padding:48px 24px;color:var(--text-muted)">
            <div style="font-size:48px;margin-bottom:12px;opacity:.4">💰</div>
            <h3 style="font-size:15px;font-weight:600;color:var(--text);margin-bottom:6px">Belum ada biaya operasional</h3>
            <p style="font-size:13px">Klik "+ Tambah Biaya" untuk mulai mencatat.</p>
          </div>
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

<!-- ADD/EDIT BIAYA OPERASIONAL -->
<div class="modal-overlay" id="modal-add-operasional">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title" id="modal-ops-title">Tambah Biaya Operasional</div>
      <button class="btn-close" onclick="closeModal('modal-add-operasional')">✕</button>
    </div>
    <div class="modal-body">
      <div class="form-grid">
        <div class="form-group">
          <label>Tanggal *</label>
          <input type="date" id="ops-tanggal">
        </div>
        <div class="form-group full" style="margin-top:4px">
          <label>Item dalam Nota *</label>
          <div id="ops-item-list" style="display:flex;flex-direction:column;gap:8px;margin-bottom:8px"></div>
          <button type="button" class="btn btn-outline btn-sm" onclick="addOpsItemRow()" style="white-space:nowrap">＋ Tambah Item</button>
          <div style="font-size:12px;color:var(--text-muted);margin-top:6px">1 nota boleh berisi beberapa item (mis. materai + ATK dalam 1 struk). Uraian & Jumlah di bawah otomatis tersusun dari item-item ini.</div>
        </div>
        <div class="form-group full">
          <label>Uraian (otomatis tersusun, bisa diedit manual)</label>
          <input type="text" id="ops-uraian" placeholder="Misal: Beli materai 10.000">
        </div>
        <div class="form-group">
          <label>Jumlah (Rp) *</label>
          <input type="number" id="ops-jumlah" placeholder="0" min="0">
          <div style="font-size:11.5px;color:var(--text-muted);margin-top:4px" id="ops-jumlah-hint"></div>
        </div>
        <div class="form-group full">
          <label>Keterangan</label>
          <textarea id="ops-keterangan" rows="3" placeholder="Catatan tambahan (opsional)"></textarea>
        </div>
        <div class="form-group full">
          <label>Upload Bukti Nota</label>
          <div class="file-input-wrap" onclick="document.getElementById('ops-bukti-input').click()">
            <div class="file-input-icon">🧾</div>
            <div class="file-input-text">Klik untuk upload bukti nota<br><small>JPG, PNG, PDF – maks 15MB</small></div>
            <input type="file" id="ops-bukti-input" accept="image/jpeg,image/jpg,image/png,application/pdf" onchange="previewOpsBukti(event)">
          </div>
          <img id="ops-bukti-preview" class="file-preview" alt="Preview">
          <div id="ops-bukti-pdf-name" style="display:none;margin-top:10px;padding:10px 12px;background:var(--bg);border-radius:var(--radius-sm);font-size:12.5px;color:var(--text-muted)">📄 <span id="ops-bukti-pdf-name-text"></span></div>
        </div>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeModal('modal-add-operasional')">Batal</button>
      <button class="btn btn-primary" onclick="saveOperasional()">Simpan</button>
    </div>
  </div>
</div>

<!-- PREVIEW BUKTI OPERASIONAL -->
<div class="modal-overlay" id="modal-preview-bukti">
  <div class="modal" style="max-width:520px">
    <div class="modal-header">
      <div class="modal-title">👁 Preview Bukti Nota</div>
      <button class="btn-close" onclick="closeModal('modal-preview-bukti')">✕</button>
    </div>
    <div class="modal-body" id="preview-bukti-content" style="text-align:center"></div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeModal('modal-preview-bukti')">Tutup</button>
    </div>
  </div>
</div>

<!-- DETAIL BIAYA OPERASIONAL -->
<div class="modal-overlay" id="modal-detail-operasional">
  <div class="modal" style="max-width:480px">
    <div class="modal-header">
      <div class="modal-title">👁 Detail Biaya Operasional</div>
      <button class="btn-close" onclick="closeModal('modal-detail-operasional')">✕</button>
    </div>
    <div class="modal-body" id="detail-operasional-content"></div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeModal('modal-detail-operasional')">Tutup</button>
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
  operasional: [],
  roles: ['Fitter Project','Fitter Maintenance','Fitter Walkway','Welder Project','Welder Walkway','Welder Maintenance','Helper Walkway','Helper Rotating','Helper Project','Housekeeping']
};

// Load from localStorage
// ════════════════ STORAGE LAYER (IndexedDB, dengan fallback localStorage) ════════════════
// Data aplikasi disimpan di IndexedDB (kapasitas jauh lebih besar dari localStorage, cocok untuk bukti nota/foto).
// Tema/preferensi UI tetap di localStorage (data kecil, tidak perlu IndexedDB).
const IDB_NAME = 'ProManageDB';
const IDB_VERSION = 1;
const IDB_STORE = 'appdata';
const IDB_KEY = 'promanage_db';
let _idbInstance = null;

function openIDB() {
  return new Promise((resolve, reject) => {
    if (!window.indexedDB) { reject(new Error('IndexedDB tidak didukung browser ini')); return; }
    const req = indexedDB.open(IDB_NAME, IDB_VERSION);
    req.onupgradeneeded = () => {
      const idb = req.result;
      if (!idb.objectStoreNames.contains(IDB_STORE)) idb.createObjectStore(IDB_STORE);
    };
    req.onsuccess = () => resolve(req.result);
    req.onerror = () => reject(req.error);
  });
}

async function idbGet() {
  const idb = await openIDB();
  return new Promise((resolve, reject) => {
    const tx = idb.transaction(IDB_STORE, 'readonly');
    const req = tx.objectStore(IDB_STORE).get(IDB_KEY);
    req.onsuccess = () => resolve(req.result || null);
    req.onerror = () => reject(req.error);
  });
}

async function idbSet(value) {
  const idb = await openIDB();
  return new Promise((resolve, reject) => {
    const tx = idb.transaction(IDB_STORE, 'readwrite');
    tx.objectStore(IDB_STORE).put(value, IDB_KEY);
    tx.oncomplete = () => resolve(true);
    tx.onerror = () => reject(tx.error);
  });
}

// Memuat data saat aplikasi pertama dibuka. Async karena IndexedDB selalu async,
// makanya dipanggil dengan `await loadDB()` sekali di awal sebelum render pertama.
async function loadDB() {
  try {
    const fromIdb = await idbGet();
    if (fromIdb) {
      db = fromIdb;
    } else {
      // IndexedDB kosong — kemungkinan pertama kali pakai versi ini.
      // Migrasi otomatis dari localStorage versi lama, supaya data lama tidak hilang.
      const legacy = localStorage.getItem(IDB_KEY);
      if (legacy) {
        try { db = JSON.parse(legacy); } catch (e) {}
        await idbSet(db); // pindahkan ke IndexedDB supaya selanjutnya pakai ini
      }
    }
  } catch (e) {
    // Browser tidak mendukung IndexedDB (mode privat ketat, dsb) — pakai localStorage sebagai fallback penuh.
    console.warn('IndexedDB tidak tersedia, memakai localStorage sebagai fallback:', e);
    const saved = localStorage.getItem(IDB_KEY);
    if (saved) { try { db = JSON.parse(saved); } catch (e2) {} }
  }
  // Ensure all arrays exist
  ['po','tagihan','apd','rencana','terima','jcn','keluar','operasional'].forEach(k => { if(!db[k]) db[k] = []; });
  if (!db.roles || !db.roles.length) {
    db.roles = ['Fitter Project','Fitter Maintenance','Fitter Walkway','Welder Project','Welder Walkway','Welder Maintenance','Helper Walkway','Helper Rotating','Helper Project','Housekeeping'];
  }
}

// Dipanggil di 24+ titik di seluruh modul, selalu TANPA await (fire-and-forget) supaya
// urutan render UI yang sudah ada (sinkron) tidak perlu diubah sama sekali.
// Tidak pernah reject (supaya 23 pemanggil lama yang tidak menangani .catch tidak memunculkan
// "unhandled promise rejection" di console) — selalu resolve dengan boolean sukses/gagal.
// Saat gagal total (IndexedDB & localStorage penuh/tidak tersedia), toast generik muncul otomatis,
// KECUALI dipanggil dengan saveDB(true) — silent, untuk pemanggil yang ingin menampilkan toast sendiri (lihat saveOperasional).
function saveDB(silent) {
  return idbSet(db)
    .then(() => true)
    .catch(e => {
      try {
        localStorage.setItem(IDB_KEY, JSON.stringify(db));
        return true;
      } catch (e2) {
        console.error('Gagal menyimpan data ke IndexedDB maupun localStorage:', e, e2);
        if (!silent) showToast('Gagal menyimpan data: penyimpanan browser penuh.', 'error');
        return false;
      }
    });
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
  'jcn-master': 'Master Data No. JCN',
  'operasional': 'Biaya Operasional'
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
  'operasional': { tbody: 'tbl-operasional-body', cols: 7 },
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
  else if (id === 'jcn-master') { populateJCNPoSelect(); renderJCN(); }
  else if (id === 'operasional') renderOperasional();
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
  if (id === 'modal-add-operasional' && !editingOpsId) resetOperasionalModal();
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

// Format tanggal DD/MM/YYYY, dipakai khusus di tabel rincian PDF Biaya Operasional
function fmtDateSlash(str) {
  if (!str) return '-';
  const [y,m,d] = str.split('-');
  return `${d}/${m}/${y}`;
}

// Format tanggal "1 Februari 2026" (nama bulan panjang), dipakai untuk teks periode di PDF
function fmtDateLong(str) {
  if (!str) return '-';
  const [y,m,d] = str.split('-');
  return `${parseInt(d)} ${bulanNamaID[parseInt(m)-1]} ${y}`;
}

// Konversi objek Date ke string YYYY-MM-DD berdasarkan tanggal LOKAL (bukan UTC), supaya
// tanggal hari ini tidak meleset gara-gara perbedaan timezone seperti toISOString() biasa.
function toISODateLocal(dateObj) {
  const y = dateObj.getFullYear();
  const m = String(dateObj.getMonth() + 1).padStart(2, '0');
  const d = String(dateObj.getDate()).padStart(2, '0');
  return `${y}-${m}-${d}`;
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

// ════════════════ SORT TABEL (GENERIK UNTUK SEMUA MODUL) ════════════════
// State sort per tabel: key = null artinya pakai urutan default bawaan masing-masing render function
const sortState = {
  'po-list':     { key: null, dir: 1 },
  'tagihan':     { key: null, dir: 1 },
  'stok':        { key: null, dir: 1 },
  'rencana':     { key: null, dir: 1 },
  'terima':      { key: null, dir: 1 },
  'keluar':      { key: null, dir: 1 },
  'jcn':         { key: null, dir: 1 },
  'operasional': { key: null, dir: 1 },
};

// Comparator universal: deteksi otomatis apakah nilai numerik, tanggal (YYYY-MM-DD), atau teks
function compareValues(a, b) {
  if (a == null) a = '';
  if (b == null) b = '';
  const aNum = typeof a === 'number' ? a : (a !== '' && !isNaN(a) ? Number(a) : null);
  const bNum = typeof b === 'number' ? b : (b !== '' && !isNaN(b) ? Number(b) : null);
  if (aNum !== null && bNum !== null) return aNum - bNum;
  return String(a).localeCompare(String(b), 'id-ID', { numeric: true, sensitivity: 'base' });
}

// Toggle arah sort saat header diklik: belum aktif -> asc, asc -> desc, desc -> kembali ke default (null)
function toggleSort(tableName, key, renderFn) {
  const st = sortState[tableName];
  if (st.key !== key) { st.key = key; st.dir = 1; }
  else if (st.dir === 1) { st.dir = -1; }
  else { st.key = null; st.dir = 1; } // klik ke-3 -> kembali ke urutan default tabel
  renderFn();
}

// Terapkan sort aktif ke array data, memakai fungsi getter per kolom (fieldMap)
function applySort(tableName, data, fieldMap) {
  const st = sortState[tableName];
  if (!st.key || !fieldMap[st.key]) return data; // tidak ada sort aktif -> kembalikan urutan asli (default)
  const getter = fieldMap[st.key];
  return [...data].sort((a, b) => compareValues(getter(a), getter(b)) * st.dir);
}

// Update ikon panah (▲▼) pada header <th data-sort-key="..."> sesuai state aktif
function renderSortIndicators(tableName, theadSelector) {
  const st = sortState[tableName];
  document.querySelectorAll(`${theadSelector} th[data-sort-key]`).forEach(th => {
    th.classList.remove('sort-asc', 'sort-desc');
    const icon = th.querySelector('.sort-icon');
    if (!icon) return;
    if (th.dataset.sortKey === st.key) {
      th.classList.add(st.dir === 1 ? 'sort-asc' : 'sort-desc');
      icon.textContent = st.dir === 1 ? '▲' : '▼';
    } else {
      icon.textContent = '⇅';
    }
  });
}

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

  // Card Total Biaya Operasional
  const totalOps = db.operasional.reduce((s,o) => s + (Number(o.jumlah)||0), 0);
  const nowOps = new Date();
  const opsBulanIni = db.operasional.filter(o => {
    const d = new Date(o.tanggal + 'T00:00:00');
    return d.getFullYear() === nowOps.getFullYear() && d.getMonth() === nowOps.getMonth();
  }).reduce((s,o) => s + (Number(o.jumlah)||0), 0);
  document.getElementById('dash-ops-card').innerHTML = `
    <div class="card" style="cursor:pointer" onclick="showPage('operasional', document.querySelector('[onclick*=operasional]'))">
      <div class="card-body" style="display:flex;align-items:center;gap:18px;padding:20px 24px">
        <div style="font-size:32px;flex-shrink:0">💰</div>
        <div style="flex:1">
          <div style="font-size:12px;font-weight:700;color:var(--text-muted);text-transform:uppercase;letter-spacing:.5px">Total Biaya Operasional</div>
          <div style="font-size:22px;font-weight:800;color:var(--text-strong);margin-top:4px">${fmtRp(totalOps)}</div>
          <div style="font-size:12px;color:var(--text-muted);margin-top:2px">${db.operasional.length} transaksi tercatat · ${fmtRp(opsBulanIni)} bulan ini</div>
        </div>
      </div>
    </div>`;

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
    renderSortIndicators('po-list', '#tbl-po');
    return;
  }
  // Pre-compute nilai terhitung (total tagihan, sisa, %) agar bisa ikut disortir
  let rows = db.po.map(p => {
    const total = getTotalTagihan(p.id);
    const sisa = (Number(p.nilai)||0) - total;
    const pct = p.nilai > 0 ? Math.min(100, total / p.nilai * 100) : 0;
    return { ...p, total, sisa, pct };
  });
  rows = applySort('po-list', rows, {
    noPO: r => r.noPO, nama: r => r.nama, nilai: r => Number(r.nilai)||0,
    total: r => r.total, sisa: r => r.sisa, pct: r => r.pct, status: r => r.status,
  });
  tbody.innerHTML = rows.map(p => {
    const cls = pctClass(p.pct);
    const statusBadge = p.status === 'Aktif' ? 'badge-aman' : p.status === 'Selesai' ? 'badge-info' : 'badge-info';
    return `<tr>
      <td><strong>${p.noPO}</strong></td>
      <td>${p.nama}<br><small style="color:var(--text-muted)">${p.date||''}</small></td>
      <td>${fmtRp(p.nilai)}</td>
      <td>${fmtRp(p.total)}</td>
      <td style="color:${p.sisa < 0 ? 'var(--danger)' : 'var(--success)'};font-weight:700">${fmtRp(p.sisa)}</td>
      <td>
        <div style="display:flex;align-items:center;gap:8px;">
          <div class="progress-track" style="flex:1;min-width:70px">
            <div class="progress-fill ${cls}" style="width:${p.pct}%"></div>
          </div>
          <span style="font-size:11px;font-weight:700;color:var(--text-muted)">${p.pct.toFixed(0)}%</span>
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
  renderSortIndicators('po-list', '#tbl-po');
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
    renderSortIndicators('tagihan', '#page-po-tagihan thead');
    return;
  }

  let data = [...db.tagihan].sort((a,b) => b.tanggal > a.tanggal ? 1 : -1); // default: tanggal terbaru dulu
  if (filterPO)      data = data.filter(t => t.poId === filterPO);
  if (filterPeriode) data = data.filter(t => (t.periode||'').toLowerCase().includes(filterPeriode));
  if (filterKet)     data = data.filter(t => (t.ket||'').toLowerCase().includes(filterKet));
  data = applySort('tagihan', data, {
    tanggal: t => t.tanggal, noPO: t => t.noPO || '', namaPO: t => t.namaPO || '',
    periode: t => t.periode || '', nominal: t => Number(t.nominal)||0,
  });

  if (data.length === 0) {
    tbody.innerHTML = '';
    if (emptyEl) emptyEl.style.display = 'block';
    renderSortIndicators('tagihan', '#page-po-tagihan thead');
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
  renderSortIndicators('tagihan', '#page-po-tagihan thead');
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
    renderSortIndicators('stok', '#page-apd-stok thead');
    return;
  }
  let rows = db.apd.map(a => {
    const statusStok = a.stok <= 0 ? 2 : a.stok <= a.stokMin ? 1 : 0; // urutan keparahan: Habis > Rendah > Aman
    return { ...a, statusStok };
  });
  rows = applySort('stok', rows, {
    nama: r => r.nama, kategori: r => r.kategori, satuan: r => r.satuan,
    stok: r => Number(r.stok)||0, stokMin: r => Number(r.stokMin)||0, statusStok: r => r.statusStok,
  });
  tbody.innerHTML = rows.map(a => {
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
  renderSortIndicators('stok', '#page-apd-stok thead');
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
  if (db.rencana.length === 0) {
    tbody.innerHTML = `<tr><td colspan="7" style="text-align:center;padding:40px;color:var(--text-muted)">Belum ada rencana pembelian.</td></tr>`;
    document.getElementById('total-rencana').textContent = '0';
    renderSortIndicators('rencana', '#page-apd-rencana thead');
    return;
  }
  const totalQty = db.rencana.reduce((s, r) => s + (Number(r.qty)||0), 0);
  const rows = applySort('rencana', db.rencana, {
    namaApd: r => r.namaApd, stokNow: r => Number(r.stokNow)||0,
    qty: r => Number(r.qty)||0, satuan: r => r.satuan,
  });
  tbody.innerHTML = rows.map(r => {
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
  renderSortIndicators('rencana', '#page-apd-rencana thead');
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
    renderSortIndicators('terima', '#page-apd-terima thead');
    return;
  }
  let sorted = [...db.terima].sort((a,b) => b.tgl > a.tgl ? 1 : -1); // default: tanggal terbaru dulu
  sorted = applySort('terima', sorted, {
    tgl: t => t.tgl, namaApd: t => t.namaApd, qty: t => Number(t.qty)||0, satuan: t => t.satuan,
  });
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
  renderSortIndicators('terima', '#page-apd-terima thead');
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

// Format No. JCN yang berlaku: JCN/tanggal/bulan/tahun/No.PO/No.Urut (mis. JCN/05/05/2026/8100002321/005).
// Ambil segmen TERAKHIR (setelah '/' paling akhir) sebagai angka no. urut untuk keperluan sortir.
// Jika format tidak sesuai / tidak ada angka di segmen terakhir, kembalikan null (akan jatuh ke perbandingan teks biasa).
function getJCNUrutanValue(no) {
  if (!no) return null;
  const parts = String(no).trim().split('/');
  const last = parts[parts.length - 1];
  const n = parseInt(last, 10);
  return isNaN(n) ? null : n;
}

// Isi dropdown "No. PO" pada form Tambah JCN (dipakai untuk generate No. JCN otomatis)
function populateJCNPoSelect() {
  const sel = document.getElementById('jcn-po');
  if (!sel) return;
  const current = sel.value;
  if (!db.po || !db.po.length) {
    sel.innerHTML = '<option value="">— Belum ada data PO —</option>';
    return;
  }
  sel.innerHTML = '<option value="">— Pilih No. PO —</option>' +
    db.po.map(p => `<option value="${p.id}">${p.noPO} – ${p.nama}</option>`).join('');
  if (current && db.po.some(p => p.id === current)) sel.value = current;
}

// Cari no. urut berikutnya secara GLOBAL (lintas semua No. PO), dengan menelusuri seluruh
// No. JCN yang sudah ada dan mengambil angka urut (segmen terakhir) terbesar + 1.
// Catatan: parameter noPO dipertahankan untuk kompatibilitas pemanggil, tapi tidak lagi
// dipakai untuk memfilter — nomor urut harus berurutan untuk semua PO sekaligus.
function getNextJCNUrutan(noPO) {
  let maxN = 0;
  (db.jcn || []).forEach(j => {
    const n = getJCNUrutanValue(j.no);
    if (n !== null && n > maxN) maxN = n;
  });
  return maxN + 1;
}

// Generate No. JCN otomatis: JCN/DD/MM/YYYY/NoPO/UrutBerikutnya (urut 3 digit, mis. 005)
function generateJCNNo() {
  const dateInput = document.getElementById('jcn-date');
  const poSel     = document.getElementById('jcn-po');
  if (!dateInput.value) { showToast('Isi Tanggal terlebih dahulu.', 'warn'); return; }
  const po = (db.po || []).find(p => p.id === poSel.value);
  if (!po) { showToast('Pilih No. PO terlebih dahulu untuk generate otomatis.', 'warn'); return; }
  const [y, m, d] = dateInput.value.split('-');
  const urut = getNextJCNUrutan(po.noPO);
  const no = `JCN/${d}/${m}/${y}/${po.noPO}/${String(urut).padStart(3, '0')}`;
  document.getElementById('jcn-no').value = no;
  showToast(`No. JCN otomatis dibuat: ${no}`, 'success');
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
  const poSel = document.getElementById('jcn-po');
  if (poSel) poSel.value = '';
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
    renderSortIndicators('jcn', '#page-jcn-master thead');
    return;
  }
  empty.style.display = 'none';

  // Urutan default (otomatis): berdasarkan No. JCN, dari No. Urut terbesar/terakhir ke terkecil
  // (format JCN/tgl/bln/thn/NoPO/NoUrut → diambil segmen NoUrut di paling akhir).
  // Jika user memilih sort kolom lain lewat klik header, urutan ini akan ditimpa oleh applySort di bawah.
  data = [...data].sort((a, b) => {
    const av = getJCNUrutanValue(a.no), bv = getJCNUrutanValue(b.no);
    if (av === null && bv === null) return 0;
    if (av === null) return 1;
    if (bv === null) return -1;
    return bv - av;
  });

  data = applySort('jcn', data, {
    date: j => j.date, no: j => getJCNUrutanValue(j.no), desc: j => j.desc, status: j => j.status,
  });

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
  renderSortIndicators('jcn', '#page-jcn-master thead');
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

async function initApp() {
  await loadDB(); // WAJIB ditunggu — IndexedDB selalu async, render pertama tidak boleh jalan sebelum data termuat
  applyTheme(localStorage.getItem('promanage_theme') || 'light', true);
  setDate();
  renderDashboard();
}
initApp();

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
    renderSortIndicators('keluar', '#page-apd-keluar thead');
    return;
  }
  let sorted = [...db.keluar].sort((a,b) => b.tgl > a.tgl ? 1 : -1); // default: tanggal terbaru dulu
  sorted = applySort('keluar', sorted, {
    tgl: k => k.tgl, namaApd: k => k.namaApd, qty: k => Number(k.qty)||0, satuan: k => k.satuan||'',
  });
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
  renderSortIndicators('keluar', '#page-apd-keluar thead');
}

// ════════════════ ASET LOGO & TANDA TANGAN UNTUK PDF ════════════════
const LOGO_PT_BASE64 = 'data:image/png;base64,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';
const TTD_KOORDINATOR_BASE64 = 'data:image/png;base64,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';
const TTD_ASPECT_RATIO = 315/204; // lebar/tinggi gambar tanda tangan asli (landscape, dipertahankan agar tidak gepeng) // lebar/tinggi gambar tanda tangan asli (dipertahankan agar tidak gepeng)

// ════════════════ BIAYA OPERASIONAL ════════════════
let editingOpsId = null;
let opsBuktiData = null;      // base64 file asli (gambar atau PDF), disimpan tanpa kompresi
let opsBuktiType = null;      // 'image' | 'pdf'
let opsBuktiName = null;      // nama file asli, dipakai untuk tampilan PDF

// Item-item dalam 1 nota (mis. 1 struk berisi "Materai" + "ATK"). Disusun jadi 1 baris
// biaya operasional dengan uraian gabungan, sesuai cara nota fisik biasanya dicatat.
// Setiap item: { nama: string, harga: number|null }. harga boleh kosong kalau memang
// mau isi Jumlah totalnya manual saja (tidak breakdown per item).
let opsItems = [];

function previewOpsBukti(e) {
  const file = e.target.files[0];
  if (!file) return;
  const isPdf = file.type === 'application/pdf';
  const isImage = file.type.startsWith('image/');
  if (!isPdf && !isImage) {
    showToast('Format file harus JPG, PNG, atau PDF.', 'error');
    e.target.value = '';
    return;
  }
  // Batas dinaikkan dari versi localStorage (dulu 5MB) — IndexedDB menampung jauh lebih besar,
  // dan bukti nota kini disimpan tanpa kompresi (kualitas/resolusi asli) sesuai permintaan.
  if (file.size > 15 * 1024 * 1024) {
    showToast('Ukuran file maksimal 15MB.', 'error');
    e.target.value = '';
    return;
  }
  const imgPreview = document.getElementById('ops-bukti-preview');
  const pdfNameBox = document.getElementById('ops-bukti-pdf-name');
  const pdfNameText = document.getElementById('ops-bukti-pdf-name-text');

  // Gambar maupun PDF disimpan persis seperti file aslinya (tanpa kompresi) — IndexedDB cukup luas untuk ini.
  const reader = new FileReader();
  reader.onload = ev => {
    opsBuktiData = ev.target.result;
    opsBuktiType = isImage ? 'image' : 'pdf';
    opsBuktiName = file.name;
    if (isImage) {
      imgPreview.src = opsBuktiData;
      imgPreview.style.display = 'block';
      pdfNameBox.style.display = 'none';
    } else {
      imgPreview.style.display = 'none';
      imgPreview.src = '';
      pdfNameText.textContent = file.name;
      pdfNameBox.style.display = 'block';
    }
  };
  reader.onerror = () => showToast('Gagal membaca file.', 'error');
  reader.readAsDataURL(file);
}

// ── PENGELOLA ITEM NOTA (1 nota bisa berisi beberapa item belanja) ──

// Render daftar item ke dalam modal. Tiap baris: nama item + harga (opsional) + tombol hapus.
function renderOpsItemList() {
  const wrap = document.getElementById('ops-item-list');
  if (!wrap) return;
  if (!opsItems.length) {
    wrap.innerHTML = '<div style="font-size:12.5px;color:var(--text-muted)">Belum ada item. Klik "+ Tambah Item" untuk mulai, atau langsung isi Uraian &amp; Jumlah di bawah secara manual.</div>';
    return;
  }
  wrap.innerHTML = opsItems.map((it, idx) => `
    <div style="display:flex;gap:8px;align-items:center">
      <input type="text" value="${(it.nama || '').replace(/"/g,'&quot;')}" placeholder="Nama item, mis. Materai 10.000"
        oninput="updateOpsItem(${idx}, 'nama', this.value)"
        style="flex:1;padding:8px 10px;border:1.5px solid var(--border);border-radius:var(--radius-sm);font-size:13px;font-family:inherit;outline:none">
      <input type="number" value="${it.harga ?? ''}" placeholder="Harga (opsional)" min="0"
        oninput="updateOpsItem(${idx}, 'harga', this.value)"
        style="width:140px;padding:8px 10px;border:1.5px solid var(--border);border-radius:var(--radius-sm);font-size:13px;font-family:inherit;outline:none">
      <button type="button" class="btn-close" onclick="removeOpsItemRow(${idx})" title="Hapus item" style="flex-shrink:0">✕</button>
    </div>
  `).join('');
}

function addOpsItemRow() {
  opsItems.push({ nama: '', harga: null });
  renderOpsItemList();
  syncOpsItemsToFields();
}

function removeOpsItemRow(idx) {
  opsItems.splice(idx, 1);
  renderOpsItemList();
  syncOpsItemsToFields();
}

function updateOpsItem(idx, field, value) {
  if (!opsItems[idx]) return;
  if (field === 'harga') {
    opsItems[idx].harga = value === '' ? null : Number(value);
  } else {
    opsItems[idx].nama = value;
  }
  syncOpsItemsToFields();
}

// Susun field Uraian (gabungan semua nama item, dipisah " + ") dan Jumlah (total harga item
// yang terisi) secara otomatis dari opsItems. Kalau tidak ada item sama sekali, field Uraian
// & Jumlah dibiarkan apa adanya supaya orang tetap bisa isi manual seperti biasa.
function syncOpsItemsToFields() {
  const namaItems = opsItems.map(it => (it.nama || '').trim()).filter(Boolean);
  const hintEl = document.getElementById('ops-jumlah-hint');
  if (namaItems.length) {
    document.getElementById('ops-uraian').value = namaItems.join(' + ');
  }
  const totalFromItems = opsItems.reduce((sum, it) => sum + (Number(it.harga) || 0), 0);
  const adaHargaItem = opsItems.some(it => it.harga != null && it.harga !== '' && !isNaN(it.harga));
  if (adaHargaItem) {
    document.getElementById('ops-jumlah').value = totalFromItems;
    if (hintEl) hintEl.textContent = `Otomatis dari ${opsItems.length} item di atas. Bisa diubah manual kalau perlu.`;
  } else if (hintEl) {
    hintEl.textContent = opsItems.length ? 'Isi harga per item di atas untuk hitung total otomatis, atau isi manual di sini.' : '';
  }
}

function resetOperasionalModal() {
  editingOpsId = null;
  opsBuktiData = null;
  opsBuktiType = null;
  opsBuktiName = null;
  opsItems = [];
  document.getElementById('modal-ops-title').textContent = 'Tambah Biaya Operasional';
  document.getElementById('ops-tanggal').valueAsDate = new Date();
  ['ops-uraian','ops-jumlah','ops-keterangan'].forEach(id => document.getElementById(id).value = '');
  const hintEl = document.getElementById('ops-jumlah-hint');
  if (hintEl) hintEl.textContent = '';
  renderOpsItemList();
  document.getElementById('ops-bukti-input').value = '';
  document.getElementById('ops-bukti-preview').style.display = 'none';
  document.getElementById('ops-bukti-preview').src = '';
  document.getElementById('ops-bukti-pdf-name').style.display = 'none';
}

function saveOperasional() {
  const tanggal = document.getElementById('ops-tanggal').value;
  const uraian = document.getElementById('ops-uraian').value.trim();
  const jumlah = Number(document.getElementById('ops-jumlah').value) || 0;
  const keterangan = document.getElementById('ops-keterangan').value.trim();

  if (!tanggal) return showToast('Tanggal wajib diisi!', 'error');
  if (!uraian) return showToast('Uraian wajib diisi!', 'error');
  if (!jumlah || jumlah <= 0) return showToast('Jumlah wajib diisi!', 'error');

  const existing = editingOpsId ? db.operasional.find(o => o.id === editingOpsId) : null;
  const obj = {
    id: editingOpsId || genId(),
    tanggal, uraian, jumlah, keterangan,
    buktiData: opsBuktiData || existing?.buktiData || null,
    buktiType: opsBuktiType || existing?.buktiType || null,
    buktiName: opsBuktiName || existing?.buktiName || null,
  };

  if (editingOpsId) {
    const idx = db.operasional.findIndex(o => o.id === editingOpsId);
    if (idx >= 0) db.operasional[idx] = obj;
  } else {
    db.operasional.push(obj);
  }

  saveDB(true).then(success => {
    if (!success) {
      // Gagal simpan (storage penuh, dsb) — rollback perubahan di memory agar tidak nyangkut tanpa tersimpan
      if (editingOpsId) {
        const idx = db.operasional.findIndex(o => o.id === editingOpsId);
        if (idx >= 0 && existing) db.operasional[idx] = existing;
      } else {
        db.operasional.pop();
      }
      showToast('Gagal menyimpan: penyimpanan browser penuh. Hapus beberapa bukti nota lama atau gunakan file lebih kecil.', 'error');
      return;
    }
    closeModal('modal-add-operasional');
    renderOperasional();
    showToast(editingOpsId ? 'Biaya operasional berhasil diperbarui' : 'Biaya operasional berhasil ditambahkan');
  });
}

function editOperasional(id) {
  const o = db.operasional.find(x => x.id === id);
  if (!o) return;
  editingOpsId = id;
  opsBuktiData = null;
  opsBuktiType = null;
  opsBuktiName = null;
  // Coba pecah uraian lama yang berformat "item1 + item2 + ..." kembali jadi baris-baris item
  // agar tetap bisa diedit per-item. Kalau uraian tidak memakai pemisah " + ", anggap saja
  // sebagai 1 item utuh (tetap aman untuk data lama yang ditulis bebas).
  const namaParts = (o.uraian || '').split(' + ').map(s => s.trim()).filter(Boolean);
  opsItems = namaParts.length > 1
    ? namaParts.map(nama => ({ nama, harga: null }))
    : [];
  renderOpsItemList();
  const hintEl = document.getElementById('ops-jumlah-hint');
  if (hintEl) hintEl.textContent = opsItems.length ? 'Harga per item tidak tersimpan terpisah untuk data lama — isi ulang kalau perlu breakdown.' : '';
  document.getElementById('modal-ops-title').textContent = 'Edit Biaya Operasional';
  document.getElementById('ops-tanggal').value = o.tanggal;
  document.getElementById('ops-uraian').value = o.uraian;
  document.getElementById('ops-jumlah').value = o.jumlah;
  document.getElementById('ops-keterangan').value = o.keterangan || '';
  document.getElementById('ops-bukti-input').value = '';
  const imgPreview = document.getElementById('ops-bukti-preview');
  const pdfNameBox = document.getElementById('ops-bukti-pdf-name');
  const pdfNameText = document.getElementById('ops-bukti-pdf-name-text');
  if (o.buktiType === 'image' && o.buktiData) {
    imgPreview.src = o.buktiData; imgPreview.style.display = 'block';
    pdfNameBox.style.display = 'none';
  } else if (o.buktiType === 'pdf' && o.buktiData) {
    imgPreview.style.display = 'none'; imgPreview.src = '';
    pdfNameText.textContent = o.buktiName || 'bukti.pdf';
    pdfNameBox.style.display = 'block';
  } else {
    imgPreview.style.display = 'none'; imgPreview.src = '';
    pdfNameBox.style.display = 'none';
  }
  document.getElementById('modal-add-operasional').classList.add('show');
}

function deleteOperasional(id) {
  if (!confirm('Hapus catatan biaya operasional ini?')) return;
  db.operasional = db.operasional.filter(o => o.id !== id);
  saveDB();
  renderOperasional();
  showToast('Biaya operasional dihapus', 'info');
}

function previewOperasionalBukti(id) {
  const o = db.operasional.find(x => x.id === id);
  if (!o || !o.buktiData) return;
  const content = document.getElementById('preview-bukti-content');
  if (o.buktiType === 'image') {
    content.innerHTML = `<img src="${o.buktiData}" style="max-width:100%;border-radius:var(--radius-sm);border:1px solid var(--border)" alt="Bukti nota">`;
  } else if (o.buktiType === 'pdf') {
    content.innerHTML = `
      <div style="padding:30px 20px">
        <div style="font-size:48px;margin-bottom:12px">📄</div>
        <p style="margin-bottom:16px;color:var(--text-muted);font-size:13px">${o.buktiName || 'bukti.pdf'}</p>
        <a href="${o.buktiData}" download="${o.buktiName || 'bukti.pdf'}" class="btn btn-primary">⬇️ Download PDF</a>
      </div>`;
  }
  openModal('modal-preview-bukti');
}

function resetFilterOperasional() {
  ['filter-ops-dari','filter-ops-sampai','filter-ops-uraian'].forEach(id => {
    const el = document.getElementById(id);
    if (el) el.value = '';
  });
  renderOperasional();
}

function detailOperasional(id) {
  const o = db.operasional.find(x => x.id === id);
  if (!o) return;
  document.getElementById('detail-operasional-content').innerHTML =
    detailRow('Tanggal', fmtDate(o.tanggal)) +
    detailRow('Uraian', `<strong>${o.uraian}</strong>`) +
    detailRow('Jumlah', `<strong style="color:var(--steel)">${fmtRp(o.jumlah)}</strong>`) +
    detailRow('Keterangan', o.keterangan || '-') +
    detailRow('Bukti Nota', o.buktiData
      ? `<button class="btn btn-outline btn-sm" onclick="closeModal('modal-detail-operasional');previewOperasionalBukti('${o.id}')">👁 Lihat Bukti</button>`
      : 'Tidak ada bukti');
  openModal('modal-detail-operasional');
}

function renderOperasional() {
  const tbody = document.getElementById('tbl-operasional-body');
  const emptyEl = document.getElementById('operasional-empty');
  if (!tbody) return;

  const dari   = document.getElementById('filter-ops-dari')?.value || '';
  const sampai = document.getElementById('filter-ops-sampai')?.value || '';
  const cari   = (document.getElementById('filter-ops-uraian')?.value || '').toLowerCase();

  // Stat: dihitung dari SELURUH data (tidak ikut filter), sesuai pola modul JCN
  const totalTransaksi = db.operasional.length;
  const totalNominal = db.operasional.reduce((s, o) => s + (Number(o.jumlah) || 0), 0);
  const now = new Date();
  const bulanIni = db.operasional.filter(o => {
    const d = new Date(o.tanggal + 'T00:00:00');
    return d.getFullYear() === now.getFullYear() && d.getMonth() === now.getMonth();
  }).reduce((s, o) => s + (Number(o.jumlah) || 0), 0);

  document.getElementById('operasional-stats').innerHTML = `
    <div class="stat-card blue">
      <div class="stat-icon">🧾</div>
      <div class="stat-label">Total Transaksi</div>
      <div class="stat-value">${totalTransaksi}</div>
      <div class="stat-sub">Seluruh catatan</div>
    </div>
    <div class="stat-card gold">
      <div class="stat-icon">💰</div>
      <div class="stat-label">Total Nominal</div>
      <div class="stat-value" style="font-size:18px">${fmtRp(totalNominal)}</div>
      <div class="stat-sub">Akumulasi semua biaya</div>
    </div>
    <div class="stat-card green">
      <div class="stat-icon">📅</div>
      <div class="stat-label">Biaya Bulan Ini</div>
      <div class="stat-value" style="font-size:18px">${fmtRp(bulanIni)}</div>
      <div class="stat-sub">${bulanNamaID[now.getMonth()]} ${now.getFullYear()}</div>
    </div>
    <div class="stat-card blue">
      <div class="stat-icon">📎</div>
      <div class="stat-label">Dengan Bukti Nota</div>
      <div class="stat-value">${db.operasional.filter(o => o.buktiData).length}</div>
      <div class="stat-sub">dari ${totalTransaksi} transaksi</div>
    </div>`;

  let data = [...db.operasional].sort((a,b) => b.tanggal > a.tanggal ? 1 : -1); // default: tanggal terbaru dulu
  if (dari)   data = data.filter(o => o.tanggal >= dari);
  if (sampai) data = data.filter(o => o.tanggal <= sampai);
  if (cari)   data = data.filter(o => o.uraian.toLowerCase().includes(cari));
  data = applySort('operasional', data, {
    tanggal: o => o.tanggal, uraian: o => o.uraian, jumlah: o => Number(o.jumlah)||0,
  });

  if (data.length === 0) {
    tbody.innerHTML = '';
    if (emptyEl) emptyEl.style.display = 'block';
    renderSortIndicators('operasional', '#tbl-operasional');
    return;
  }
  if (emptyEl) emptyEl.style.display = 'none';

  tbody.innerHTML = data.map((o, idx) => `<tr>
    <td style="color:var(--text-muted);font-size:12px">${idx+1}</td>
    <td style="white-space:nowrap">${fmtDate(o.tanggal)}</td>
    <td><strong>${o.uraian}</strong></td>
    <td><strong style="color:var(--steel)">${fmtRp(o.jumlah)}</strong></td>
    <td style="max-width:200px;word-break:break-word;color:var(--text-muted);font-size:12px">${o.keterangan || '-'}</td>
    <td>${o.buktiData ? `<button class="btn btn-outline btn-sm" onclick="previewOperasionalBukti('${o.id}')">👁 Lihat</button>` : '-'}</td>
    <td style="white-space:nowrap">
      <button class="btn btn-outline btn-sm" onclick="detailOperasional('${o.id}')" title="Detail" style="margin-right:4px">👁</button>
      <button class="btn btn-outline btn-sm" onclick="editOperasional('${o.id}')" title="Edit" style="margin-right:4px">✏️</button>
      <button class="btn btn-danger btn-sm" onclick="deleteOperasional('${o.id}')" title="Hapus">🗑</button>
    </td>
  </tr>`).join('');
  renderSortIndicators('operasional', '#tbl-operasional');
}

// ════════════════ EXPORT PDF BIAYA OPERASIONAL ════════════════
// Nama penanda tangan default pada laporan Biaya Operasional.
// Ubah di sini jika suatu saat penanggung jawab berganti.
const OPS_NAMA_OPERASIONAL = 'RAYI RAHARDJO';
const OPS_NAMA_KOORDINATOR = 'Happy Shelly WK';
const OPS_JABATAN_KOORDINATOR = 'Koordinator Tuban';

function exportOperasionalPDF() {
  if (!db.operasional.length) return showToast('Belum ada biaya operasional untuk diexport!', 'warn');
  const { jsPDF } = window.jspdf;
  const doc = new jsPDF({ unit: 'pt', format: 'a4' });
  const pageW = doc.internal.pageSize.getWidth();
  const pageH = doc.internal.pageSize.getHeight();
  const marginX = 40;
  const tableRight = pageW - marginX;
  let y = 44;

  // Urutkan tanggal lama -> baru untuk laporan rincian (lebih natural dibaca sebagai riwayat)
  const data = [...db.operasional].sort((a,b) => a.tanggal > b.tanggal ? 1 : -1);
  const periodeAwal = data[0]?.tanggal;
  const periodeAkhir = data[data.length-1]?.tanggal;

  // ── HEADER: LOGO (besar, kiri) + JUDUL & ALAMAT (kanan) ──
  const logoW = 76;
  const logoH = logoW * (112/175);
  const headerTextX = marginX + logoW + 16;
  const headerTextW = tableRight - headerTextX;
  try {
    doc.addImage(LOGO_PT_BASE64, 'PNG', marginX, y - 6, logoW, logoH);
  } catch (e) { /* logo gagal dimuat, lanjutkan tanpa logo */ }

  doc.setFont('helvetica','bold'); doc.setFontSize(13);
  doc.text('RINCIAN BIAYA OPERASIONAL KOORDINATOR', headerTextX + headerTextW/2, y + 6, { align:'center' });
  y += 16;
  doc.text('PT. USAHA YEKAPEPE', headerTextX + headerTextW/2, y + 6, { align:'center' });
  y += 20;
  doc.setFont('helvetica','normal'); doc.setFontSize(9);
  doc.text('Dusun Remen Rt.001 Rw.002 Kec. Jenu Kab. Tuban', headerTextX + headerTextW/2, y, { align:'center' });
  y += 13;
  doc.text('Lokasi kerja Trans - Pacific Petrochemical Indotama - Tuban', headerTextX + headerTextW/2, y, { align:'center' });

  // Pastikan y turun cukup jauh agar tidak bertabrakan dengan logo yang besar
  y = Math.max(y, (44 - 6) + logoH) + 14;

  doc.setDrawColor(0); doc.setLineWidth(1);
  doc.line(marginX, y, tableRight, y);
  y += 18;

  // ── PERIODE ──
  doc.setFont('helvetica','normal'); doc.setFontSize(10);
  const periodeText = periodeAwal && periodeAkhir
    ? `Tanggal :  ${fmtDateLong(periodeAwal)} s/d ${fmtDateLong(periodeAkhir)}`
    : 'Tanggal :  -';
  doc.text(periodeText, pageW/2, y, { align:'center' });
  y += 24;

  // ── TABEL RINCIAN (manual, dengan border penuh seperti dokumen contoh) ──
  const colWidths = { no: 26, tgl: 62, uraian: 0, jumlah: 80, ket: 90 };
  colWidths.uraian = (tableRight - marginX) - colWidths.no - colWidths.tgl - colWidths.jumlah - colWidths.ket;
  const colX = {
    no: marginX,
    tgl: marginX + colWidths.no,
    uraian: marginX + colWidths.no + colWidths.tgl,
    jumlah: marginX + colWidths.no + colWidths.tgl + colWidths.uraian,
    ket: marginX + colWidths.no + colWidths.tgl + colWidths.uraian + colWidths.jumlah
  };
  const padX = 4;
  const headerRowH = 22;

  function drawTableHeader() {
    const top = y;
    doc.setFont('helvetica','bold'); doc.setFontSize(9);
    doc.setDrawColor(0); doc.setLineWidth(0.7);
    doc.rect(marginX, top, tableRight - marginX, headerRowH);
    [colX.tgl, colX.uraian, colX.jumlah, colX.ket].forEach(x => doc.line(x, top, x, top + headerRowH));
    const midY = top + headerRowH/2 + 3;
    doc.text('No.', colX.no + colWidths.no/2, midY, { align:'center' });
    doc.text('Tanggal', colX.tgl + colWidths.tgl/2, midY, { align:'center' });
    doc.text('U R A I A N', colX.uraian + colWidths.uraian/2, midY, { align:'center' });
    doc.text('Jumlah', colX.jumlah + colWidths.jumlah/2, midY, { align:'center' });
    doc.text('Keterangan', colX.ket + colWidths.ket/2, midY, { align:'center' });
    y = top + headerRowH;
    doc.setFont('helvetica','normal');
  }
  drawTableHeader();

  const minRowH = 20;
  let grandTotal = 0;

  function drawRow(cells, rowH, isTotal) {
    const top = y;
    doc.setDrawColor(0); doc.setLineWidth(0.6);
    doc.rect(marginX, top, tableRight - marginX, rowH);
    if (!isTotal) {
      [colX.tgl, colX.uraian, colX.jumlah, colX.ket].forEach(x => doc.line(x, top, x, top + rowH));
    } else {
      doc.line(colX.jumlah, top, colX.jumlah, top + rowH);
      doc.line(colX.ket, top, colX.ket, top + rowH);
    }
    return top;
  }

  data.forEach((o, idx) => {
    doc.setFont('helvetica','normal'); doc.setFontSize(9);
    const uraianLines = doc.splitTextToSize(o.uraian || '-', colWidths.uraian - padX*2);
    const ketLines = doc.splitTextToSize(o.keterangan || '', colWidths.ket - padX*2);
    const nLines = Math.max(uraianLines.length, ketLines.length, 1);
    const rowH = Math.max(minRowH, nLines * 11 + 8);

    if (y + rowH > pageH - 130) {
      doc.addPage();
      y = 50;
      drawTableHeader();
    }

    const top = drawRow(null, rowH, false);
    const textY = top + 13;
    doc.text(String(idx + 1), colX.no + colWidths.no/2, textY, { align:'center' });
    doc.text(fmtDateSlash(o.tanggal), colX.tgl + colWidths.tgl/2, textY, { align:'center' });
    doc.text(uraianLines, colX.uraian + padX, textY);
    doc.text(fmtRp(o.jumlah).replace('Rp ',''), colX.jumlah + colWidths.jumlah - padX, textY, { align:'right' });
    if (ketLines && ketLines[0]) doc.text(ketLines, colX.ket + padX, textY);
    grandTotal += Number(o.jumlah) || 0;
    y += rowH;
  });

  // Beberapa baris kosong agar tabel terasa lega seperti dokumen asli (opsional, dibatasi agar tidak kepanjangan)
  const emptyRowsToAdd = Math.max(0, 3 - (data.length % 4 === 0 ? 0 : 1));
  for (let i = 0; i < Math.min(emptyRowsToAdd, 3); i++) {
    if (y + minRowH > pageH - 130) { doc.addPage(); y = 50; drawTableHeader(); }
    drawRow(null, minRowH, false);
    y += minRowH;
  }

  // ── BARIS TOTAL ──
  if (y + minRowH > pageH - 130) { doc.addPage(); y = 50; drawTableHeader(); }
  const totalRowH = minRowH;
  const totalTop = drawRow(null, totalRowH, true);
  doc.setFont('helvetica','bold'); doc.setFontSize(9.5);
  doc.text('TOTAL', colX.uraian + colWidths.uraian - padX, totalTop + 14, { align:'right' });
  doc.text(fmtRp(grandTotal).replace('Rp ',''), colX.jumlah + colWidths.jumlah - padX, totalTop + 14, { align:'right' });
  y = totalTop + totalRowH;
  y += 14;

  doc.setFont('helvetica','italic'); doc.setFontSize(9);
  doc.text('* Bukti Asli Terlampir', marginX, y);
  y += 50;

  // ── TANDA TANGAN ──
  const sigBlockH = 150;
  if (y + sigBlockH > pageH - 30) { doc.addPage(); y = 60; }

  const sigColW = (pageW - marginX*2) / 2;
  const opColCenterX = marginX + sigColW/2;
  const koorColCenterX = pageW - marginX - sigColW/2;

  doc.setFont('helvetica','normal'); doc.setFontSize(10);
  doc.text('Operasional,', opColCenterX, y, { align:'center' });
  doc.text(`Tuban, ${fmtDateLong(toISODateLocal(new Date()))}`, koorColCenterX, y, { align:'center' });
  y += 13;
  doc.text(OPS_JABATAN_KOORDINATOR, koorColCenterX, y, { align:'center' });

  // Tanda tangan koordinator (gambar) — rasio aspek asli dipertahankan agar tidak gepeng/melebar paksa
  const ttdH = 78;
  const ttdW = ttdH * TTD_ASPECT_RATIO;
  const ttdTop = y + 8;
  try {
    doc.addImage(TTD_KOORDINATOR_BASE64, 'PNG', koorColCenterX - ttdW/2, ttdTop, ttdW, ttdH);
  } catch (e) { /* ttd gagal dimuat, lanjutkan tanpa gambar */ }

  y = ttdTop + ttdH + 14;
  doc.setFont('helvetica','normal').setFontSize(10);
  doc.text(OPS_NAMA_OPERASIONAL, opColCenterX, y, { align:'center' });
  doc.text(OPS_NAMA_KOORDINATOR, koorColCenterX, y, { align:'center' });
  // garis bawah nama
  doc.setDrawColor(0); doc.setLineWidth(0.5);
  const opNameWidth = doc.getTextWidth(OPS_NAMA_OPERASIONAL);
  doc.line(opColCenterX - opNameWidth/2, y + 2, opColCenterX + opNameWidth/2, y + 2);
  const koorNameWidth = doc.getTextWidth(OPS_NAMA_KOORDINATOR);
  doc.line(koorColCenterX - koorNameWidth/2, y + 2, koorColCenterX + koorNameWidth/2, y + 2);
  y += 6;

  // ── LAMPIRAN BUKTI (halaman baru per kelompok, foto satu per satu) ──
  const withBukti = data.filter(o => o.buktiData);
  if (withBukti.length) {
    doc.addPage();
    let ly = 50;
    doc.setFont('helvetica','bold'); doc.setFontSize(13);
    doc.text('Lampiran Bukti Pengeluaran', pageW/2, ly, { align:'center' });
    ly += 30;

    withBukti.forEach((o, idx) => {
      const labelHeight = 16;
      const isImage = o.buktiType === 'image';
      const imgMaxW = pageW - marginX*2;
      const imgMaxH = 260;

      // Halaman baru kalau tidak cukup ruang untuk label + konten
      const neededHeight = labelHeight + (isImage ? imgMaxH : 20) + 24;
      if (ly + neededHeight > pageH - 40) {
        doc.addPage();
        ly = 50;
      }

      doc.setFont('helvetica','bold'); doc.setFontSize(10.5);
      doc.text(`${idx + 1}. ${o.uraian}`, marginX, ly);
      ly += labelHeight;

      if (isImage) {
        try {
          // Hitung dimensi gambar asli agar proporsional, dibatasi max width/height halaman
          const imgProps = doc.getImageProperties(o.buktiData);
          let w = imgMaxW, h = (imgProps.height / imgProps.width) * w;
          if (h > imgMaxH) { h = imgMaxH; w = (imgProps.width / imgProps.height) * h; }
          doc.addImage(o.buktiData, 'JPEG', marginX, ly, w, h);
          ly += h + 24;
        } catch (e) {
          doc.setFont('helvetica','normal'); doc.setFontSize(9); doc.setTextColor(150);
          doc.text('(Gagal menampilkan gambar bukti)', marginX, ly);
          doc.setTextColor(0);
          ly += 24;
        }
      } else {
        // Bukti berupa PDF: cukup tampilkan nama file, sesuai instruksi
        doc.setFont('helvetica','normal'); doc.setFontSize(9.5); doc.setTextColor(90);
        doc.text(`📄 File PDF terlampir: ${o.buktiName || 'bukti.pdf'}`, marginX, ly);
        doc.setTextColor(0);
        ly += 24;
      }
    });
  }

  doc.save(`Biaya-Operasional-${new Date().toISOString().split('T')[0]}.pdf`);
}

</script>
</body>
</html>
