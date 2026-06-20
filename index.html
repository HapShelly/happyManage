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
const TTD_ASPECT_RATIO = 211/325; // lebar/tinggi gambar tanda tangan asli (dipertahankan agar tidak gepeng)

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
  doc.text('Tuban, 2 Maret 2026', koorColCenterX, y, { align:'center' });
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
