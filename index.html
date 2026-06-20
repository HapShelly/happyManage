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
        <div class="form-group">
          <label>Jumlah (Rp) *</label>
          <input type="number" id="ops-jumlah" placeholder="0" min="0">
        </div>
        <div class="form-group full">
          <label>Uraian *</label>
          <input type="text" id="ops-uraian" placeholder="Misal: Beli materai 10.000">
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

// ════════════════ BIAYA OPERASIONAL ════════════════
let editingOpsId = null;
let opsBuktiData = null;      // base64 file asli (gambar atau PDF), disimpan tanpa kompresi
let opsBuktiType = null;      // 'image' | 'pdf'
let opsBuktiName = null;      // nama file asli, dipakai untuk tampilan PDF

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

function resetOperasionalModal() {
  editingOpsId = null;
  opsBuktiData = null;
  opsBuktiType = null;
  opsBuktiName = null;
  document.getElementById('modal-ops-title').textContent = 'Tambah Biaya Operasional';
  document.getElementById('ops-tanggal').valueAsDate = new Date();
  ['ops-uraian','ops-jumlah','ops-keterangan'].forEach(id => document.getElementById(id).value = '');
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
  let y = 42;

  // Urutkan tanggal lama -> baru untuk laporan rincian (lebih natural dibaca sebagai riwayat)
  const data = [...db.operasional].sort((a,b) => a.tanggal > b.tanggal ? 1 : -1);
  const periodeAwal = data[0]?.tanggal;
  const periodeAkhir = data[data.length-1]?.tanggal;

  // ── HEADER: LOGO + JUDUL ──
  const logoSize = 42;
  try {
    doc.addImage(LOGO_PT_BASE64, 'PNG', marginX, y - 4, logoSize, logoSize * (112/175));
  } catch (e) { /* logo gagal dimuat, lanjutkan tanpa logo */ }

  doc.setFont('helvetica','bold'); doc.setFontSize(12);
  doc.text('RINCIAN BIAYA OPERASIONAL KOORDINATOR PT. USAHA YEKAPEPE', pageW/2, y + 6, { align:'center' });
  y += 22;
  doc.setFont('helvetica','normal'); doc.setFontSize(9);
  doc.text('Dusun Remen Rt.001 Rw.002 Kec. Jenu Kab. Tuban', pageW/2, y, { align:'center' });
  y += 13;
  doc.text('Lokasi kerja Trans - Pacific Petrochemical Indotama - Tuban', pageW/2, y, { align:'center' });
  y += 26;

  // ── PERIODE ──
  doc.setFont('helvetica','normal'); doc.setFontSize(10);
  const periodeText = periodeAwal && periodeAkhir
    ? `Tanggal :  ${fmtDateLong(periodeAwal)} s/d ${fmtDateLong(periodeAkhir)}`
    : 'Tanggal :  -';
  doc.text(periodeText, pageW/2, y, { align:'center' });
  y += 26;

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
  const sigBlockH = 130;
  if (y + sigBlockH > pageH - 30) { doc.addPage(); y = 60; }

  doc.setFont('helvetica','normal'); doc.setFontSize(10);
  doc.text('Operasional,', marginX, y);
  doc.text('Tuban, 2 Maret 2026', pageW - marginX, y, { align:'right' });
  y += 13;
  doc.text(OPS_JABATAN_KOORDINATOR, pageW - marginX, y, { align:'right' });

  // Tanda tangan koordinator (gambar)
  const ttdW = 95;
  const ttdH = 70;
  try {
    doc.addImage(TTD_KOORDINATOR_BASE64, 'PNG', pageW - marginX - ttdW, y + 6, ttdW, ttdH);
  } catch (e) { /* ttd gagal dimuat, lanjutkan tanpa gambar */ }

  y += ttdH + 18;
  doc.setFont('helvetica','normal').setFontSize(10);
  doc.text(OPS_NAMA_OPERASIONAL, marginX, y);
  doc.text(OPS_NAMA_KOORDINATOR, pageW - marginX, y, { align:'right' });
  // garis bawah nama
  doc.setDrawColor(0); doc.setLineWidth(0.5);
  const opNameWidth = doc.getTextWidth(OPS_NAMA_OPERASIONAL);
  doc.line(marginX, y + 2, marginX + opNameWidth, y + 2);
  const koorNameWidth = doc.getTextWidth(OPS_NAMA_KOORDINATOR);
  doc.line(pageW - marginX - koorNameWidth, y + 2, pageW - marginX, y + 2);
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
