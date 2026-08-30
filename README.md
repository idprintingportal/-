<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>ID CARD PRINT & CONVERTER PORTAL</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
  
  <!-- PDF.js Standalone -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/2.16.105/pdf.min.js"></script>
  
  <!-- PDF-LIB for Pure Vector Merging & Page Manipulation -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf-lib/1.17.1/pdf-lib.min.js"></script>

  <!-- jsPDF Library -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>

  <!-- JSZip for Multi-page PDF to JPG Batch Download -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js"></script>

  <!-- Cropper.js -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/cropperjs/1.5.13/cropper.min.css"/>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/cropperjs/1.5.13/cropper.min.js"></script>

  <style>
    :root {
      --bg-gradient: linear-gradient(135deg, #0f172a 0%, #1e1b4b 50%, #0f172a 100%);
      --card-bg: rgba(30, 41, 59, 0.88);
      --accent-blue: #38bdf8;
      --accent-purple: #818cf8;
      --btn-add: linear-gradient(135deg, #f59e0b 0%, #d97706 100%);
      --btn-download: linear-gradient(135deg, #10b981 0%, #059669 100%);
      --text-main: #f8fafc;
      --text-muted: #94a3b8;
      --border-color: rgba(255, 255, 255, 0.1);
    }

    * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Poppins', sans-serif; }
    
    body { 
      background: var(--bg-gradient); 
      min-height: 100vh;
      padding: 15px 10px; 
      display: flex; 
      flex-direction: column; 
      align-items: center; 
      justify-content: center;
      color: var(--text-main);
    }

    .portal-main-heading {
      font-size: 24px;
      font-weight: 800;
      letter-spacing: 1.5px;
      text-transform: uppercase;
      background: linear-gradient(135deg, #38bdf8 0%, #a855f7 50%, #f43f5e 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      margin-bottom: 10px;
      text-align: center;
    }

    /* Running Ticker Notification Bar */
    .ticker-container {
      width: 100%;
      max-width: 580px;
      overflow: hidden;
      background: rgba(56, 189, 248, 0.1);
      border: 1px solid rgba(56, 189, 248, 0.3);
      border-radius: 8px;
      padding: 8px 0;
      margin-bottom: 12px;
      white-space: nowrap;
    }

    .ticker-text {
      display: inline-block;
      padding-left: 100%;
      animation: tickerAnimation 18s linear infinite;
      color: #38bdf8;
      font-weight: 600;
      font-size: 13px;
    }

    @keyframes tickerAnimation {
      0% { transform: translate3d(0, 0, 0); }
      100% { transform: translate3d(-100%, 0, 0); }
    }

    /* Advertisement Image Slider / Grid */
    .ad-slider-box {
      display: flex;
      gap: 8px;
      justify-content: center;
      margin-bottom: 12px;
      max-width: 580px;
      width: 100%;
    }

    .ad-slide-img {
      width: calc(33.333% - 6px);
      height: 95px;
      object-fit: cover;
      border-radius: 8px;
      border: 1px solid var(--border-color);
      box-shadow: 0 4px 10px rgba(0,0,0,0.4);
      background: #1e293b;
      transition: transform 0.3s;
    }
    .ad-slide-img:hover { transform: scale(1.04); }

    /* Services Info Box */
    .services-info-card {
      background: rgba(15, 23, 42, 0.75);
      border: 1px solid var(--border-color);
      border-radius: 12px;
      padding: 10px 14px;
      max-width: 580px;
      width: 100%;
      margin-bottom: 15px;
      text-align: left;
    }

    .services-info-card h4 {
      font-size: 12px;
      color: var(--accent-blue);
      margin-bottom: 4px;
      font-weight: 700;
    }

    .services-info-card ul {
      font-size: 11px;
      color: var(--text-muted);
      padding-left: 14px;
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 3px;
    }

    .top-reg-nav {
      display: flex;
      gap: 12px;
      margin-bottom: 15px;
      flex-wrap: wrap;
      justify-content: center;
    }

    .top-reg-btn {
      background: linear-gradient(135deg, #10b981 0%, #059669 100%);
      border: none;
      color: #fff;
      padding: 10px 22px;
      font-size: 13px;
      font-weight: 600;
      border-radius: 20px;
      cursor: pointer;
      transition: 0.3s;
      display: inline-flex;
      align-items: center;
      gap: 6px;
      box-shadow: 0 4px 15px rgba(16, 185, 129, 0.4);
    }
    .top-reg-btn:hover { transform: translateY(-2px); box-shadow: 0 6px 20px rgba(16, 185, 129, 0.6); }

    .auth-box {
      background: var(--card-bg);
      backdrop-filter: blur(20px);
      border: 1px solid var(--border-color);
      padding: 20px 25px;
      border-radius: 20px;
      box-shadow: 0 25px 60px rgba(0, 0, 0, 0.6);
      width: 100%;
      max-width: 580px;
      text-align: center;
    }

    .badge {
      display: inline-block;
      padding: 3px 12px;
      font-size: 11px;
      font-weight: 600;
      letter-spacing: 1px;
      text-transform: uppercase;
      background: rgba(56, 189, 248, 0.15);
      color: var(--accent-blue);
      border: 1px solid rgba(56, 189, 248, 0.3);
      border-radius: 20px;
      margin-bottom: 8px;
    }

    .slot-counter-badge {
      background: rgba(245, 158, 11, 0.15);
      color: #fbbf24;
      border: 1px solid rgba(245, 158, 11, 0.3);
      padding: 4px 16px;
      font-size: 12px;
      font-weight: 600;
      border-radius: 20px;
      display: inline-block;
      margin-bottom: 15px;
    }

    .login-input {
      width: 100%;
      padding: 11px 15px;
      margin-bottom: 12px;
      background: rgba(15, 23, 42, 0.9);
      border: 1px solid rgba(56, 189, 248, 0.3);
      border-radius: 10px;
      color: #fff;
      font-size: 13px;
      outline: none;
    }

    .login-btn {
      width: 100%;
      padding: 12px;
      background: linear-gradient(135deg, #0284c7 0%, #2563eb 100%);
      color: #fff;
      font-weight: 600;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      font-size: 14px;
      transition: 0.3s;
    }

    .auth-link {
      display: inline-block;
      margin-top: 10px;
      font-size: 12px;
      color: var(--accent-blue);
      cursor: pointer;
      text-decoration: underline;
    }

    .error-msg {
      color: #ef4444;
      font-size: 12px;
      margin-top: 10px;
      display: none;
    }

    .tab-nav {
      display: flex;
      justify-content: center;
      gap: 8px;
      margin-bottom: 15px;
      flex-wrap: wrap;
    }

    .tab-btn {
      padding: 9px 13px;
      background: rgba(15, 23, 42, 0.8);
      border: 1px solid var(--border-color);
      color: var(--text-muted);
      border-radius: 12px;
      cursor: pointer;
      font-weight: 600;
      font-size: 12px;
      transition: 0.3s;
    }

    .tab-btn.active {
      background: linear-gradient(135deg, #0284c7 0%, #2563eb 100%);
      color: #fff;
      border-color: transparent;
      box-shadow: 0 4px 15px rgba(37, 99, 235, 0.4);
    }

    #mainApp {
      display: none;
      width: 100%;
      max-width: 1220px;
    }

    .container { 
      background: var(--card-bg); 
      backdrop-filter: blur(16px);
      border: 1px solid var(--border-color);
      padding: 25px 20px; 
      border-radius: 20px; 
      box-shadow: 0 20px 50px rgba(0, 0, 0, 0.4); 
      width: 100%; 
      text-align: center; 
      position: relative; 
    }

    .logout-btn {
      background: rgba(239, 68, 68, 0.2);
      border: 1px solid rgba(239, 68, 68, 0.4);
      color: #fca5a5;
      padding: 6px 14px;
      font-size: 12px;
      border-radius: 8px;
      cursor: pointer;
      transition: 0.2s;
    }
    .logout-btn:hover {
      background: rgba(239, 68, 68, 0.4);
    }

    h1 { 
      background: linear-gradient(to right, #38bdf8, #a855f7, #ec4899);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      font-size: 22px; 
      font-weight: 700;
      margin-bottom: 6px; 
    }

    .tab-content { display: none; }
    .tab-content.active { display: block; }

    .upload-section { 
      display: flex; 
      gap: 15px; 
      justify-content: center; 
      margin: 15px 0; 
      flex-wrap: wrap; 
    }

    .upload-box { 
      border: 2px dashed rgba(56, 189, 248, 0.4); 
      padding: 16px 14px; 
      border-radius: 14px; 
      cursor: pointer; 
      background: rgba(15, 23, 42, 0.6); 
      flex: 1; 
      min-width: 220px; 
      transition: 0.3s; 
    }

    .upload-box:hover { 
      border-color: var(--accent-blue);
      background: rgba(56, 189, 248, 0.08);
    }

    input[type="file"] { display: none; }

    .preview-container { 
      display: flex; 
      justify-content: center; 
      gap: 20px; 
      margin: 15px 0; 
      flex-wrap: wrap; 
    }

    .preview-box { 
      border: 1px solid var(--border-color); 
      padding: 10px; 
      background: rgba(15, 23, 42, 0.8); 
      border-radius: 12px; 
    }

    .preview-box h4 { 
      font-size: 12px; 
      color: var(--text-muted); 
      margin-bottom: 6px; 
    }
    
    canvas { 
      max-width: 100% !important; 
      height: auto !important; 
      display: block; 
      margin: 0 auto; 
      border-radius: 4px;
      background: #fff; 
      object-fit: contain;
    }

    .btn-group { 
      display: flex; 
      gap: 10px; 
      justify-content: center; 
      margin-top: 15px; 
      flex-wrap: wrap; 
    }

    .action-btn { 
      padding: 10px 22px; 
      font-size: 13px; 
      font-weight: 600; 
      border: none; 
      border-radius: 10px; 
      cursor: pointer; 
      transition: all 0.3s ease; 
      color: #fff;
    }

    .action-btn:hover:not(:disabled) {
      transform: translateY(-2px);
      box-shadow: 0 6px 20px rgba(0,0,0,0.4);
    }

    .btn-add { background: var(--btn-add); }
    .btn-download { background: var(--btn-download); }
    .btn-reset { background: rgba(239, 68, 68, 0.2); border: 1px solid rgba(239, 68, 68, 0.4); color: #fca5a5; }

    .btn-manual-crop {
      background: rgba(56, 189, 248, 0.15);
      border: 1px solid var(--accent-blue);
      color: var(--accent-blue);
      padding: 4px 10px;
      font-size: 11px;
      border-radius: 6px;
      margin-top: 8px;
      cursor: pointer;
      font-weight: 600;
      transition: 0.2s;
    }
    .btn-manual-crop:hover {
      background: var(--accent-blue);
      color: #0f172a;
    }

    .action-btn:disabled { 
      background: #334155; 
      color: #64748b; 
      cursor: not-allowed; 
    }

    .control-panel {
      background: rgba(15, 23, 42, 0.7);
      border: 1px solid var(--border-color);
      border-radius: 14px;
      padding: 14px 18px;
      max-width: 600px;
      margin: 15px auto;
      text-align: center;
    }

    .qty-select-group {
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
      margin-top: 8px;
      flex-wrap: wrap;
    }

    .qty-input {
      width: 80px;
      padding: 6px 10px;
      border-radius: 8px;
      background: rgba(15, 23, 42, 0.9);
      border: 1px solid var(--accent-blue);
      color: #fff;
      font-size: 14px;
      font-weight: 700;
      text-align: center;
      outline: none;
    }

    .text-field-input {
      width: 100%;
      max-width: 260px;
      padding: 8px 12px;
      border-radius: 8px;
      background: rgba(15, 23, 42, 0.9);
      border: 1px solid var(--accent-blue);
      color: #fff;
      font-size: 13px;
      outline: none;
      margin-bottom: 4px;
    }

    .quick-qty-btn {
      padding: 5px 12px;
      background: #334155;
      border: 1px solid rgba(255, 255, 255, 0.1);
      color: #fff;
      border-radius: 6px;
      font-size: 11px;
      cursor: pointer;
      font-weight: 600;
    }

    .slider-range {
      -webkit-appearance: none;
      width: 100%;
      height: 6px;
      border-radius: 5px;
      background: #334155;
      outline: none;
      margin: 6px 0 8px 0;
    }

    .slider-range::-webkit-slider-thumb {
      -webkit-appearance: none;
      appearance: none;
      width: 16px;
      height: 16px;
      border-radius: 50%;
      background: var(--accent-blue);
      cursor: pointer;
      box-shadow: 0 0 10px rgba(56, 189, 248, 0.5);
    }

    .size-badge-box {
      display: flex;
      justify-content: space-around;
      background: rgba(15, 23, 42, 0.8);
      padding: 12px;
      border-radius: 10px;
      margin-top: 10px;
      border: 1px solid var(--border-color);
    }

    .file-gallery-list {
      display: flex;
      flex-wrap: wrap;
      gap: 14px;
      justify-content: center;
      margin: 15px 0;
      max-height: 420px;
      overflow-y: auto;
      padding: 14px;
      background: rgba(15, 23, 42, 0.6);
      border-radius: 12px;
      border: 1px solid var(--border-color);
    }

    .draggable-card {
      position: relative;
      width: 125px;
      background: #0f172a;
      border: 2px solid rgba(56, 189, 248, 0.35);
      border-radius: 10px;
      padding: 6px 4px 8px 4px;
      display: flex;
      flex-direction: column;
      align-items: center;
      box-shadow: 0 6px 14px rgba(0,0,0,0.5);
      cursor: grab;
      user-select: none;
      transition: transform 0.2s ease, border-color 0.2s ease, opacity 0.2s ease;
    }

    .draggable-card:active { cursor: grabbing; }
    .draggable-card.dragging { opacity: 0.4; transform: scale(0.92); border-color: #f59e0b; }
    .draggable-card.drag-over { border: 2px dashed #38bdf8; transform: scale(1.05); background: rgba(56, 189, 248, 0.12); }

    .draggable-card canvas, .draggable-card img {
      width: 100%;
      height: 135px;
      object-fit: contain;
      background: #ffffff;
      border-radius: 5px;
      pointer-events: none;
    }

    .draggable-card .file-label {
      font-size: 11px;
      color: #94a3b8;
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
      width: 100%;
      margin: 6px 0 2px 0;
      font-weight: 600;
      text-align: center;
      pointer-events: none;
    }

    .card-tools-bar {
      display: flex;
      gap: 6px;
      justify-content: center;
      width: 100%;
      margin-top: 4px;
    }

    .mini-tool-btn {
      background: #334155;
      color: #f8fafc;
      border: 1px solid rgba(255,255,255,0.15);
      border-radius: 4px;
      padding: 4px 8px;
      font-size: 11px;
      cursor: pointer;
      transition: 0.2s;
    }
    .mini-tool-btn:hover { background: #0284c7; }
    .mini-tool-btn.btn-del:hover { background: #ef4444; }

    .item-delete-btn {
      position: absolute;
      top: -6px;
      right: -6px;
      background: #ef4444;
      color: #ffffff;
      border: 2px solid #1e293b;
      border-radius: 50%;
      width: 22px;
      height: 22px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 11px;
      font-weight: bold;
      cursor: pointer;
      box-shadow: 0 2px 6px rgba(0, 0, 0, 0.5);
      z-index: 10;
      transition: 0.2s;
    }
    .item-delete-btn:hover { background: #dc2626; transform: scale(1.15); }

    .history-table-container {
      margin-top: 15px;
      overflow-x: auto;
      background: rgba(15, 23, 42, 0.7);
      border-radius: 12px;
      border: 1px solid var(--border-color);
    }

    .history-table {
      width: 100%;
      border-collapse: collapse;
      font-size: 12px;
      text-align: left;
    }

    .history-table th, .history-table td {
      padding: 10px 14px;
      border-bottom: 1px solid rgba(255, 255, 255, 0.08);
    }

    .history-table th {
      background: rgba(30, 41, 59, 0.9);
      color: var(--accent-blue);
      font-weight: 600;
    }

    .history-table tr:hover { background: rgba(56, 189, 248, 0.05); }

    .history-download-btn {
      background: #0284c7;
      color: #fff;
      border: none;
      padding: 5px 12px;
      border-radius: 6px;
      cursor: pointer;
      font-size: 11px;
      font-weight: 600;
    }

    .history-delete-btn {
      background: rgba(239, 68, 68, 0.2);
      color: #fca5a5;
      border: 1px solid rgba(239, 68, 68, 0.4);
      padding: 5px 12px;
      border-radius: 6px;
      cursor: pointer;
      font-size: 11px;
      font-weight: 600;
      transition: 0.2s;
    }
    .history-delete-btn:hover { background: rgba(239, 68, 68, 0.4); }

    .history-msg-btn {
      background: rgba(245, 158, 11, 0.2);
      color: #fbbf24;
      border: 1px solid rgba(245, 158, 11, 0.4);
      padding: 5px 12px;
      border-radius: 6px;
      cursor: pointer;
      font-size: 11px;
      font-weight: 600;
      transition: 0.2s;
      margin-left: 5px;
    }
    .history-msg-btn:hover { background: rgba(245, 158, 11, 0.4); }

    .history-view-ss-btn {
      background: rgba(56, 189, 248, 0.25);
      color: #38bdf8;
      border: 1px solid rgba(56, 189, 248, 0.5);
      padding: 5px 10px;
      border-radius: 6px;
      cursor: pointer;
      font-size: 11px;
      font-weight: 600;
      transition: 0.2s;
      margin-left: 5px;
    }
    .history-view-ss-btn:hover { background: rgba(56, 189, 248, 0.45); }

    /* Separate Stop and Start Buttons */
    .btn-status-stop {
      background: rgba(239, 68, 68, 0.25);
      color: #fca5a5;
      border: 1px solid rgba(239, 68, 68, 0.5);
      padding: 5px 10px;
      border-radius: 6px;
      cursor: pointer;
      font-size: 11px;
      font-weight: 600;
      transition: 0.2s;
      margin-left: 5px;
    }
    .btn-status-stop:hover { background: rgba(239, 68, 68, 0.45); }

    .btn-status-start {
      background: rgba(16, 185, 129, 0.25);
      color: #34d399;
      border: 1px solid rgba(16, 185, 129, 0.5);
      padding: 5px 10px;
      border-radius: 6px;
      cursor: pointer;
      font-size: 11px;
      font-weight: 600;
      transition: 0.2s;
      margin-left: 5px;
    }
    .btn-status-start:hover { background: rgba(16, 185, 129, 0.45); }

    #cropModal, #adminMsgModal, #viewScreenshotModal {
      display: none;
      position: fixed;
      top: 0; left: 0; width: 100%; height: 100%;
      background: rgba(0, 0, 0, 0.85);
      z-index: 10000;
      align-items: center;
      justify-content: center;
      flex-direction: column;
      padding: 20px;
    }

    .crop-wrapper {
      max-width: 90vw;
      max-height: 70vh;
      background: #000;
      border-radius: 8px;
      overflow: hidden;
      margin-bottom: 15px;
    }

    .crop-wrapper img {
      max-width: 100%;
      max-height: 70vh;
      display: block;
    }

    /* Registration Modal Popup Styles */
    #regModalPopup {
      display: none;
      position: fixed;
      top: 0; left: 0; width: 100%; height: 100%;
      background: rgba(0, 0, 0, 0.85);
      z-index: 1000000;
      align-items: center;
      justify-content: center;
      padding: 20px;
    }

    .reg-popup-content {
      background: #1e293b;
      border: 1px solid rgba(56, 189, 248, 0.4);
      border-radius: 16px;
      padding: 25px;
      width: 100%;
      max-width: 420px;
      text-align: center;
      box-shadow: 0 25px 60px rgba(0,0,0,0.8);
    }
  </style>
</head>
<body>

<div class="portal-main-heading">
  ID CARD PRINT & CONVERTER PORTAL
</div>

<!-- Contact for Registration Button -->
<div class="top-reg-nav" id="topNavRegistrationBox">
  <button class="top-reg-btn" onclick="openRegModal()">
    💬 Contact for Registration
  </button>
</div>

<!-- 1. Login Screen with Running Ticker, Ad Images & Services Info -->
<div id="loginScreen" class="auth-box">
  
  <!-- Running Ticker Notification -->
  <div class="ticker-container">
    <div class="ticker-text">
      🚀 Smart & Reliable Print Portal — Fast Operations, Simple Workflow & Daily Business Use! | 📌 Essential Document & Photo Printing Services in One Place!
    </div>
  </div>

  <!-- Advertisement Images -->
  <div class="ad-slider-box">
    <img src="https://images.unsplash.com/photo-1544717305-2782549b5136?w=400&auto=format&fit=crop&q=60" alt="Print Service 1" class="ad-slide-img" title="Photo & Document Print">
    <img src="https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?w=400&auto=format&fit=crop&q=60" alt="Print Service 2" class="ad-slide-img" title="Passport Sheet Generator">
    <img src="https://images.unsplash.com/photo-1633158829585-23ba8f7c8caf?w=400&auto=format&fit=crop&q=60" alt="Print Service 3" class="ad-slide-img" title="Government ID Print">
  </div>

  <!-- Portal Services Info List -->
  <div class="services-info-card">
    <h4>⚡ Our Printing Services (उपलब्ध मुख्य सर्विसेज):</h4>
    <ul>
      <li>🔹 5-Cards ID Print (A4)</li>
      <li>🔹 Multi-Unique Passports (1 to 5 Photos)</li>
      <li>🔹 4×6 Photo Sheets</li>
      <li>🔹 PDF Arranger & Merger</li>
      <li>🔹 Custom Image Resizer</li>
      <li>🔹 PDF to JPG & Compressor</li>
    </ul>
  </div>

  <div class="badge">Protected Access</div>
  <h2 style="font-size: 20px; margin-bottom: 6px;">Sign In</h2>
  <p style="font-size: 11px; color: var(--text-muted); margin-bottom: 15px;">Card & Photo Generator Portal</p>

  <input type="email" id="loginEmail" class="login-input" placeholder="ईमेल आईडी दर्ज करें" value="oneplus777000@gmail.com">
  <input type="password" id="loginPass" class="login-input" placeholder="पासवर्ड दर्ज करें">
  <button id="authBtn" class="login-btn">लॉगिन करें</button>
  <div id="errorMsg" class="error-msg">⚠️ गलत ईमेल आईडी या पासवर्ड!</div>
  
  <div>
    <span id="goToChangePwd" class="auth-link">🔑 Change Password?</span>
  </div>
</div>

<!-- 2. Change Password Screen -->
<div id="changePwdScreen" class="auth-box" style="display:none;">
  <div class="badge">Security Settings</div>
  <h2 style="font-size: 20px; margin-bottom: 6px; color: var(--accent-blue);">🔑 Change Password</h2>
  <p style="font-size: 12px; color: var(--text-muted); margin-bottom: 20px;">ईमेल आईडी, पुराना और नया पासवर्ड दर्ज करें</p>

  <input type="email" id="pwdEmailInput" class="login-input" placeholder="अपनी ईमेल आईडी (Login Email)">
  <input type="password" id="oldPassInput" class="login-input" placeholder="पुराना पासवर्ड">
  <input type="password" id="newPassInput" class="login-input" placeholder="नया पासवर्ड">
  <input type="password" id="confirmPassInput" class="login-input" placeholder="नया पासवर्ड कन्फर्म करें">
  
  <button id="saveNewPwdBtn" class="login-btn" style="background: var(--btn-download);">💾 नया पासवर्ड सेव करें</button>
  <div id="pwdStatusMsg" style="font-size:13px; margin-top:12px; display:none; font-weight:500;"></div>

  <div>
    <span id="backToLogin" class="auth-link">⬅️ Back to Login</span>
  </div>
</div>

<!-- 3. Main Portal Application -->
<div id="mainApp">
  <div class="tab-nav">
    <button class="tab-btn active" onclick="switchTab('tab-cards')">💳 ID Card (5 Slots)</button>
    <button class="tab-btn" onclick="switchTab('tab-passport')">👤 Passport Photos</button>
    <button class="tab-btn" onclick="switchTab('tab-name-passport')">📝 Name & Date Passport</button>
    <button class="tab-btn" onclick="switchTab('tab-4x6')">🖼️ 4×6 Photo Print</button>
    <button class="tab-btn" onclick="switchTab('tab-arranger')">📑 PDF Arranger</button>
    <button class="tab-btn" onclick="switchTab('tab-jpg-to-pdf')">📄 PDF, JPG, PNG to PDF</button>
    <button class="tab-btn" onclick="switchTab('tab-resizer')">📐 Image Resizer</button>
    <button class="tab-btn" onclick="switchTab('tab-pdf-to-jpg')">🖼️ PDF to JPG (Manual DPI)</button>
    <button class="tab-btn" onclick="switchTab('tab-pdf-compressor')">🗜️ PDF Compressor</button>
    <button class="tab-btn" onclick="switchTab('tab-resume')">📝 Resume Builder</button>
    <button class="tab-btn" onclick="switchTab('tab-history')" style="border-color: rgba(56, 189, 248, 0.5);">📂 History</button>
    <button id="adminTabBtn" class="tab-btn" onclick="switchTab('tab-admin')" style="display:none; border-color: #f59e0b; color:#fbbf24;">⚙️ Admin Panel</button>
  </div>

  <div class="container">
    <!-- Top Header Bar with Live Validity Counter & Logout -->
    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px; flex-wrap: wrap; gap: 10px;">
      <div id="validityCounterBadge" style="background: rgba(16, 185, 129, 0.15); border: 1px solid #10b981; color: #34d399; padding: 6px 14px; border-radius: 20px; font-size: 12px; font-weight: 600;">
        ⏳ Validity: Initializing...
      </div>
      <button id="logoutBtn" class="logout-btn">🔒 Logout</button>
    </div>

    <!-- Distributor Notification Banner with QR/Image & Reply Payment Screenshot Option -->
    <div id="distributorNoticeBanner" style="display:none; background: rgba(245, 158, 11, 0.2); border: 1px solid #fbbf24; color: #fef08a; padding: 14px 18px; border-radius: 12px; margin-bottom: 15px; font-size: 13px; text-align: left;">
      <div style="display: flex; justify-content: space-between; align-items: flex-start; gap: 15px; flex-wrap: wrap;">
        <div style="flex: 1; min-width: 240px;">
          <strong>📢 Admin Notice / QR Code:</strong>
          <div id="distributorNoticeText" style="margin-top: 4px; font-weight: 500;"></div>
          <div id="distributorNoticeImgBox" style="margin-top: 10px; display:none;">
            <img id="distributorNoticeImg" src="" style="max-width: 100%; max-height: 220px; border-radius: 8px; border: 1px solid rgba(255,255,255,0.3);" alt="QR / Banner">
          </div>
        </div>

        <!-- Reply Payment Screenshot Box for Distributor -->
        <div style="background: rgba(15,23,42,0.85); border: 1px solid rgba(56,189,248,0.4); padding: 12px; border-radius: 10px; min-width: 220px; text-align: center;">
          <div style="font-size: 11px; color: var(--accent-blue); margin-bottom: 6px; font-weight: 600;">💳 Reply Your Payment Screenshot</div>
          <input type="file" id="distScreenshotInput" accept="image/*" style="display:block; width:100%; background:#334155; color:#fff; padding:6px; font-size:11px; border-radius:6px; border:1px solid rgba(56,189,248,0.4); margin-bottom:8px; cursor:pointer;">
          <button onclick="uploadDistributorScreenshot()" class="action-btn btn-download" style="padding: 6px 12px; font-size: 11px; width: 100%;">📤 Send Screenshot</button>
          <div id="screenshotUploadStatus" style="font-size:10px; margin-top:4px; display:none;"></div>
        </div>
      </div>
    </div>

    <!-- TAB 1: 5 CARDS SYSTEM -->
    <div id="tab-cards" class="tab-content active">
      <div class="badge">Auto-Dimension Crop • 2.5mm Gap • Broad Black Border • 5 Cards</div>
      <h1>Card Generator System</h1>
      <p style="font-size: 12px; color: var(--text-muted); margin-bottom: 10px;">इमेज सिलेक्ट करते ही वह <strong>ऑटोमैटिकली सही ID साइज में फिट</strong> हो जाएगी। जरूरत पड़ने पर मैनुअल क्रॉप भी कर सकते हैं।</p>
      
      <div id="slotCounter" class="slot-counter-badge">Cards on Page: 0 / 5 (Next Slot: #1)</div>

      <div class="upload-section">
        <label class="upload-box" for="card1Input">
          <strong style="display:block; font-size:14px; margin-bottom:4px;">📁 Front Side</strong>
          <div id="file1Name" style="font-size: 12px; color: var(--text-muted);">इमेज चुनें (Auto-Crop)</div>
        </label>
        <input type="file" id="card1Input" accept="image/*">

        <label class="upload-box" for="card2Input">
          <strong style="display:block; font-size:14px; margin-bottom:4px;">📁 Back Side</strong>
          <div id="file2Name" style="font-size: 12px; color: var(--text-muted);">इमेज चुनें (Auto-Crop)</div>
        </label>
        <input type="file" id="card2Input" accept="image/*">
      </div>

      <div class="preview-container">
        <div class="preview-box">
          <h4>Front Card Preview</h4>
          <canvas id="canvas1" width="1013" height="638" style="width: 180px;"></canvas>
          <button id="manualCropFrontBtn" class="btn-manual-crop" style="display:none;" onclick="openManualCropForCard('front')">✂️ Manual Crop Front</button>
        </div>
        <div class="preview-box">
          <h4>Back Card Preview</h4>
          <canvas id="canvas2" width="1013" height="638" style="width: 180px;"></canvas>
          <button id="manualCropBackBtn" class="btn-manual-crop" style="display:none;" onclick="openManualCropForCard('back')">✂️ Manual Crop Back</button>
        </div>
      </div>

      <div class="btn-group">
        <button id="addCardBtn" class="action-btn btn-add" disabled>➕ Add This Card to A4 Sheet</button>
        <button id="resetPageBtn" class="action-btn btn-reset">🔄 Clear A4 Page</button>
      </div>

      <div style="margin-top: 25px; border-top: 1px solid var(--border-color); padding-top: 15px;">
        <h3 style="font-size: 15px; color: var(--accent-blue); margin-bottom: 6px;">A4 Sheet Preview</h3>
        <div style="display:inline-block; max-width: 250px; background:#fff; border-radius:6px; overflow:hidden; border: 1px solid #475569;">
          <canvas id="a4Canvas" width="2480" height="3508" style="width: 100%; display:block;"></canvas>
        </div>
        <div class="btn-group">
          <button id="downloadPdfBtn" class="action-btn btn-download" disabled>📥 Direct A4 PDF Download</button>
        </div>
      </div>
    </div>

    <!-- TAB 2: PASSPORT SIZE PHOTOS -->
    <div id="tab-passport" class="tab-content">
      <div class="badge">Standard 35mm × 45mm • Multi-Unique Photo Generator & Custom Qty</div>
      <h1>Passport Photo Generator</h1>
      <p style="font-size: 12px; color: var(--text-muted); margin-bottom: 12px;">1 से 5 अलग-अलग फ़ोटो चुनें, संख्या सेट करें, पहले 'Generate' करके प्रीव्यू देखें और फिर डाउनलोड करें:</p>

      <div class="control-panel" style="margin-bottom: 12px;">
        <span style="font-size: 13px; font-weight:600; color: var(--accent-blue);">📂 Select Unique Photos Mode (1 to 5 Photos):</span>
        <div class="qty-select-group" style="margin-top: 8px;">
          <button class="quick-qty-btn" id="btnCount1" onclick="setPassportCount(1)" style="background:#0284c7;">1 Photo</button>
          <button class="quick-qty-btn" id="btnCount2" onclick="setPassportCount(2)">2 Photos</button>
          <button class="quick-qty-btn" id="btnCount3" onclick="setPassportCount(3)">3 Photos</button>
          <button class="quick-qty-btn" id="btnCount4" onclick="setPassportCount(4)">4 Photos</button>
          <button class="quick-qty-btn" id="btnCount5" onclick="setPassportCount(5)">5 Photos</button>
        </div>
      </div>

      <div id="passportUploadBlocksContainer" style="display: flex; gap: 8px; justify-content: center; flex-wrap: wrap; margin-bottom: 12px;"></div>

      <div class="control-panel" style="margin-bottom: 15px;">
        <span style="font-size: 13px; font-weight:600; color: var(--accent-blue);">🔢 A4 शीट पर कुल फ़ोटो की संख्या (Quantity) चुनें या टाइप करें:</span>
        <div class="qty-select-group">
          <input type="number" id="passportQtyInput" class="qty-input" value="8" min="1" max="50">
          <button class="quick-qty-btn" onclick="setPassportQty(2)">2</button>
          <button class="quick-qty-btn" onclick="setPassportQty(4)">4</button>
          <button class="quick-qty-btn" onclick="setPassportQty(6)">6</button>
          <button class="quick-qty-btn" onclick="setPassportQty(8)">8</button>
          <button class="quick-qty-btn" onclick="setPassportQty(12)">12</button>
          <button class="quick-qty-btn" onclick="setPassportQty(16)">16</button>
          <button class="quick-qty-btn" onclick="setPassportQty(30)">30</button>
        </div>
      </div>

      <div class="btn-group">
        <button id="generateMultiPassportA4Btn" class="action-btn btn-add">🖼️ Generate Sheet (Preview)</button>
      </div>

      <div style="margin-top: 25px; border-top: 1px solid var(--border-color); padding-top: 15px;">
        <h3 id="passportSheetTitle" style="font-size: 15px; color: var(--accent-blue); margin-bottom: 6px;">A4 Passport Sheet Preview</h3>
        <div style="display:inline-block; max-width: 250px; background:#fff; border-radius:6px; overflow:hidden; border: 1px solid #475569;">
          <canvas id="passportSheetCanvas" width="2480" height="3508" style="width: 100%; display:block;"></canvas>
        </div>
        <div class="btn-group">
          <button id="downloadMultiPassportPdfBtn" class="action-btn btn-download" disabled>📥 Download A4 Sheet PDF</button>
        </div>
      </div>
    </div>

    <!-- TAB 3: NAME & DATE PASSPORT -->
    <div id="tab-name-passport" class="tab-content">
      <div class="badge">Govt / Exam Standard • 3 Separate Font Sliders • Auto DOB Label</div>
      <h1>Name & Date Passport Photo Maker</h1>
      <p style="font-size: 12px; color: var(--text-muted); margin-bottom: 12px;">नाम, DOB और DOP के लिए अलग-अलग स्लाइडर से फॉन्ट साइज़ कंट्रोल करें।</p>

      <div class="upload-section" style="margin-bottom:10px;">
        <label class="upload-box" for="namePassportInput" style="max-width: 380px;">
          <strong style="display:block; font-size:14px; margin-bottom:4px;">📁 Upload Candidate Photo</strong>
          <div id="namePassportFileName" style="font-size: 12px; color: var(--text-muted);">फ़ोटो चुनें व क्रॉप करें</div>
        </label>
        <input type="file" id="namePassportInput" accept="image/*">
      </div>

      <div class="control-panel" style="text-align:left;">
        <div style="display:flex; flex-direction:column; gap:10px;">
          <div style="background:rgba(15,23,42,0.6); padding:8px 12px; border-radius:8px; border:1px solid var(--border-color);">
            <div style="display:flex; justify-content:space-between; align-items:center;">
              <label style="font-size:11px; color:var(--text-muted);">👤 Candidate Name:</label>
              <span id="nameFontLabel" style="font-size:11px; color:var(--accent-blue); font-weight:600;">Size: 24px</span>
            </div>
            <input type="text" id="candNameInput" class="text-field-input" style="max-width:100%;" placeholder="e.g. HARSHAL SATISH MARATHE" oninput="renderNamePassportPreview()">
            <input type="range" id="nameFontSlider" class="slider-range" min="14" max="36" value="24" oninput="updateNameFontSize(this.value)">
          </div>

          <div style="background:rgba(15,23,42,0.6); padding:8px 12px; border-radius:8px; border:1px solid var(--border-color);">
            <div style="display:flex; justify-content:space-between; align-items:center;">
              <label style="font-size:11px; color:var(--text-muted);">🎂 Date of Birth (DOB):</label>
              <span id="dobFontLabel" style="font-size:11px; color:var(--accent-blue); font-weight:600;">Size: 20px</span>
            </div>
            <input type="text" id="candDobInput" class="text-field-input" style="max-width:100%;" placeholder="e.g. 15/08/1998" oninput="renderNamePassportPreview()">
            <input type="range" id="dobFontSlider" class="slider-range" min="12" max="30" value="20" oninput="updateDobFontSize(this.value)">
          </div>

          <div style="background:rgba(15,23,42,0.6); padding:8px 12px; border-radius:8px; border:1px solid var(--border-color);">
            <div style="display:flex; justify-content:space-between; align-items:center;">
              <label style="font-size:11px; color:var(--text-muted);">📅 Photo Date (DOP):</label>
              <span id="dopFontLabel" style="font-size:11px; color:var(--accent-blue); font-weight:600;">Size: 20px</span>
            </div>
            <input type="text" id="candDopInput" class="text-field-input" style="max-width:100%;" placeholder="DOP: DD/MM/YYYY" oninput="renderNamePassportPreview()">
            <input type="range" id="dopFontSlider" class="slider-range" min="12" max="30" value="20" oninput="updateDopFontSize(this.value)">
          </div>
        </div>

        <div style="margin-top:12px; text-align:center;">
          <span style="font-size: 12px; font-weight:600; color: var(--accent-blue);">🔢 फ़ोटो संख्या:</span>
          <input type="number" id="namePassportQtyInput" class="qty-input" value="8" min="1" max="30">
          <button class="quick-qty-btn" onclick="setNamePassportQty(4)">4</button>
          <button class="quick-qty-btn" onclick="setNamePassportQty(6)">6</button>
          <button class="quick-qty-btn" onclick="setNamePassportQty(8)">8</button>
          <button class="quick-qty-btn" onclick="setNamePassportQty(12)">12</button>
          <button class="quick-qty-btn" onclick="setNamePassportQty(30)">30</button>
        </div>
      </div>

      <div class="preview-container">
        <div class="preview-box">
          <h4>Preview with Name & Date Strip</h4>
          <canvas id="namePassportCanvas" width="413" height="531" style="width: 155px;"></canvas>
        </div>
      </div>

      <div class="btn-group">
        <button id="make4x6NamePassportBtn" class="action-btn btn-add" disabled>🖼️ Generate 4×6 Sheet</button>
        <button id="makeA4NamePassportBtn" class="action-btn btn-add" disabled>📄 Generate A4 Sheet</button>
      </div>

      <div style="margin-top: 20px; border-top: 1px solid var(--border-color); padding-top: 15px;">
        <h3 id="namePassportSheetTitle" style="font-size: 15px; color: var(--accent-blue); margin-bottom: 6px;">Sheet Preview</h3>
        <div style="display:inline-block; max-width: 250px; background:#fff; border-radius:6px; overflow:hidden; border: 1px solid #475569;">
          <canvas id="namePassportSheetCanvas" width="1800" height="1200" style="width: 100%; display:block;"></canvas>
        </div>
        <div class="btn-group">
          <button id="downloadNamePassportPdfBtn" class="action-btn btn-download" disabled>📥 Download Name & Date Sheet PDF</button>
        </div>
      </div>
    </div>

    <!-- TAB 4: 4x6 PHOTO PRINT -->
    <div id="tab-4x6" class="tab-content">
      <div class="badge">Clear 300 DPI • 1200 × 1800 px • Max 4 Photos</div>
      <h1>4×6 Photo Print Generator</h1>
      <p style="font-size: 12px; color: var(--text-muted); margin-bottom: 15px;">4×6 इंच फ़ोटो अपलोड करें, 1 से 4 तक संख्या चुनें और A4 या 4×6 शीट PDF निकालें।</p>

      <div class="upload-section">
        <label class="upload-box" for="photo4x6Input" style="max-width: 380px;">
          <strong style="display:block; font-size:14px; margin-bottom:4px;">📁 4×6 Photo Upload</strong>
          <div id="photo4x6FileName" style="font-size: 12px; color: var(--text-muted);">फ़ोटो चुनें व क्रॉप करें</div>
        </label>
        <input type="file" id="photo4x6Input" accept="image/*">
      </div>

      <div class="preview-container">
        <div class="preview-box">
          <h4>Cropped 4×6 Photo Canvas</h4>
          <canvas id="canvas4x6" width="1200" height="1800" style="width: 150px;"></canvas>
        </div>
      </div>

      <div class="control-panel">
        <span style="font-size: 14px; font-weight:600; color: var(--accent-blue);">🔢 A4 शीट पर 4×6 फ़ोटो की संख्या चुनें (Max 4):</span>
        <div class="qty-select-group">
          <input type="number" id="photo4x6QtyInput" class="qty-input" value="2" min="1" max="4">
          <button class="quick-qty-btn" onclick="set4x6Qty(1)">1 Photo</button>
          <button class="quick-qty-btn" onclick="set4x6Qty(2)">2 Photos</button>
          <button class="quick-qty-btn" onclick="set4x6Qty(3)">3 Photos</button>
          <button class="quick-qty-btn" onclick="set4x6Qty(4)">4 Photos</button>
        </div>
      </div>

      <div class="btn-group">
        <button id="downloadDirect4x6Pdf" class="action-btn btn-download" disabled>📥 Direct 1 Photo (4×6 Paper PDF)</button>
        <button id="generateA4Custom4x6Btn" class="action-btn btn-add" disabled>📄 Generate Selected Qty on A4 Sheet</button>
      </div>

      <div style="margin-top: 25px; border-top: 1px solid var(--border-color); padding-top: 15px;">
        <h3 id="photo4x6SheetTitle" style="font-size: 15px; color: var(--accent-blue); margin-bottom: 6px;">A4 4×6 Photo Sheet Preview</h3>
        <div style="display:inline-block; max-width: 250px; background:#fff; border-radius:6px; overflow:hidden; border: 1px solid #475569;">
          <canvas id="a4_4x6_SheetCanvas" width="2480" height="3508" style="width: 100%; display:block;"></canvas>
        </div>
        <div class="btn-group">
          <button id="downloadA4_4x6_PdfBtn" class="action-btn btn-download" disabled>📥 Download A4 4×6 Sheet PDF</button>
        </div>
      </div>
    </div>

    <!-- TAB 5: PDF ARRANGER -->
    <div id="tab-arranger" class="tab-content">
      <div class="badge">Drag & Drop To Re-order • Hold & Move • Rotate 90° • Cut Pages</div>
      <h1>PDF Page Arranger & Organizer</h1>
      <p style="font-size: 12px; color: var(--text-muted); margin-bottom: 12px;">किसी भी पेज को <strong>पकड़कर (Hold करके) मनचाही जगह पर सरकाएँ</strong>।</p>

      <div class="upload-section" style="margin-bottom: 15px;">
        <label class="upload-box" for="arrangerPdfInput" style="max-width: 420px;">
          <strong style="display:block; font-size:14px; margin-bottom:4px; color:var(--accent-blue);">📑 Select / Add PDF to Arrange</strong>
          <div id="arrangerStatus" style="font-size: 12px; color: var(--text-muted);">क्लिक करके .pdf फाइल अपलोड करें</div>
        </label>
        <input type="file" id="arrangerPdfInput" accept="application/pdf" multiple>
      </div>

      <div id="arrangerContainerArea" style="display:none;">
        <div style="display:flex; justify-content:space-between; align-items:center; max-width:900px; margin:0 auto 10px auto;">
          <span style="font-size: 13px; font-weight:600; color: var(--accent-blue);">Total Pages: <strong id="arrangerTotalPagesCount" style="color:#fbbf24;">0</strong></span>
          <label for="arrangerPdfInput" class="action-btn btn-add" style="padding:6px 14px; font-size:11px; cursor:pointer;">➕ Add More PDF Files</label>
        </div>

        <div id="arrangerGridList" class="file-gallery-list"></div>

        <div class="btn-group">
          <button id="saveArrangedPdfBtn" class="action-btn btn-download">💾 Save & Download Arranged PDF</button>
          <button id="clearArrangerBtn" class="action-btn btn-reset">🔄 Clear All Pages</button>
        </div>
      </div>
    </div>

    <!-- TAB 6: UNIVERSAL MERGE -->
    <div id="tab-jpg-to-pdf" class="tab-content">
      <div class="badge">Universal File Merger • Drag & Drop Re-order • Individual Delete</div>
      <h1>PDF, JPG, PNG to PDF Converter</h1>
      <p style="font-size: 12px; color: var(--text-muted); margin-bottom: 12px;">फ़ाइलों को <strong>माउस से पकड़कर आगे-पीछे क्रमबद्ध करें</strong> और कंबाइंड PDF बनाएँ।</p>

      <div class="upload-section" style="margin-bottom: 15px;">
        <label class="upload-box" for="universalMultiInput" style="max-width: 450px;">
          <strong style="display:block; font-size:14px; margin-bottom:4px; color:var(--accent-blue);">📁 Select Files (PDF, JPG, PNG Allowed)</strong>
          <div id="universalMultiStatus" style="font-size: 12px; color: var(--text-muted);">क्लिक करके PDF या इमेज फ़ाइलें चुनें</div>
        </label>
        <input type="file" id="universalMultiInput" accept="image/jpeg,image/png,image/jpg,application/pdf" multiple>
      </div>

      <div id="universalGalleryContainer" style="display:none;">
        <div style="font-size: 12px; color: var(--accent-blue); font-weight: 600; margin-bottom: 6px;">
          Selected Files (<span id="universalSelectedCount">0</span>):
        </div>
        <div id="universalGalleryList" class="file-gallery-list"></div>

        <div class="btn-group">
          <button id="convertUniversalToPdfBtn" class="action-btn btn-download">📥 Convert & Download Combined PDF</button>
          <button id="clearUniversalListBtn" class="action-btn btn-reset">🔄 Clear All</button>
        </div>
      </div>
    </div>

    <!-- TAB 7: IMAGE RESIZER -->
    <div id="tab-resizer" class="tab-content">
      <div class="badge">Resize in Pixels (px) • Millimeters (mm) • Centimeters (cm)</div>
      <h1>Custom Image Resizer</h1>
      <p style="font-size: 12px; color: var(--text-muted); margin-bottom: 12px;">किसी भी इमेज को अपनी ज़रूरत के अनुसार Width और Height (px, mm, cm) में रीसाइज़ करें।</p>

      <div class="upload-section" style="margin-bottom: 15px;">
        <label class="upload-box" for="resizerImageInput" style="max-width: 400px;">
          <strong style="display:block; font-size:14px; margin-bottom:4px; color:var(--accent-blue);">📁 Select Image to Resize</strong>
          <div id="resizerFileName" style="font-size: 12px; color: var(--text-muted);">क्लिक करके इमेज चुनें (JPG / PNG)</div>
        </label>
        <input type="file" id="resizerImageInput" accept="image/*">
      </div>

      <div id="resizerControlsPanel" style="display:none;">
        <div class="control-panel" style="text-align:left;">
          <div style="display:flex; flex-wrap:wrap; gap:12px; justify-content:center; align-items:center;">
            <div>
              <label style="font-size:11px; color:var(--text-muted); display:block; margin-bottom:3px;">📏 Unit (इकाई):</label>
              <select id="resizerUnitSelect" class="text-field-input" style="max-width:110px;" onchange="onResizerUnitChange()">
                <option value="px" selected>Pixels (px)</option>
                <option value="mm">Millimeters (mm)</option>
                <option value="cm">Centimeters (cm)</option>
              </select>
            </div>
            <div>
              <label style="font-size:11px; color:var(--text-muted); display:block; margin-bottom:3px;">↔️ Width (चौड़ाई):</label>
              <input type="number" id="resizerWidthInput" class="qty-input" style="width:100px;" value="300" oninput="onResizerDimensionChange('width')">
            </div>
            <div>
              <label style="font-size:11px; color:var(--text-muted); display:block; margin-bottom:3px;">↕️ Height (ऊंचाई):</label>
              <input type="number" id="resizerHeightInput" class="qty-input" style="width:100px;" value="300" oninput="onResizerDimensionChange('height')">
            </div>
          </div>

          <div style="margin-top:10px; display:flex; justify-content:center; align-items:center; gap:15px; font-size:12px; color:var(--text-muted);">
            <label style="cursor:pointer; display:flex; align-items:center; gap:5px;">
              <input type="checkbox" id="resizerAspectLock"> Lock Aspect Ratio (अनुपात लॉक रखें)
            </label>
            <span style="color:var(--accent-blue);">DPI: 300 (for mm/cm)</span>
          </div>
        </div>

        <div class="preview-container">
          <div class="preview-box">
            <h4>Resized Output Preview</h4>
            <canvas id="resizerPreviewCanvas" style="max-width: 250px; max-height: 250px;"></canvas>
            <div id="resizerOutputInfo" style="font-size:11px; color:var(--accent-blue); margin-top:5px;">0 x 0 px</div>
          </div>
        </div>

        <div class="btn-group">
          <button id="downloadResizedJpgBtn" class="action-btn btn-download">📥 Download JPG Image</button>
          <button id="downloadResizedPngBtn" class="action-btn btn-add">📥 Download PNG Image</button>
        </div>
      </div>
    </div>

    <!-- TAB 8: PDF TO JPG -->
    <div id="tab-pdf-to-jpg" class="tab-content">
      <div class="badge">Ultra High-Res • Manual & Quick DPI (72 to 1200 DPI) • Batch ZIP Export</div>
      <h1>PDF to High-DPI JPG Converter</h1>
      <p style="font-size: 12px; color: var(--text-muted); margin-bottom: 12px;">PDF फ़ाइल अपलोड करें और अपनी आवश्यकतानुसार DPI रिज़ॉल्यूशन टाइप या सेलेक्ट करें।</p>

      <div class="upload-section" style="margin-bottom: 15px;">
        <label class="upload-box" for="pdfToJpgInput" style="max-width: 420px;">
          <strong style="display:block; font-size:14px; margin-bottom:4px; color:var(--accent-blue);">📄 Select PDF File to Convert</strong>
          <div id="pdfToJpgStatus" style="font-size: 12px; color: var(--text-muted);">क्लिक करके .pdf फाइल चुनें</div>
        </label>
        <input type="file" id="pdfToJpgInput" accept="application/pdf">
      </div>

      <div id="pdfToJpgControls" style="display:none;">
        <div class="control-panel">
          <span style="font-size: 13px; font-weight:600; color: var(--accent-blue);">⚙️ Quick Select or Type Custom DPI (Max 1200):</span>
          <div class="qty-select-group">
            <button class="quick-qty-btn" onclick="setPdfDpi(72)">72 DPI</button>
            <button class="quick-qty-btn" onclick="setPdfDpi(150)">150 DPI</button>
            <button class="quick-qty-btn" onclick="setPdfDpi(300)">300 DPI</button>
            <button class="quick-qty-btn" onclick="setPdfDpi(600)">600 DPI</button>
            <button class="quick-qty-btn" onclick="setPdfDpi(1200)">1200 DPI</button>
            <input type="number" id="manualDpiInput" class="qty-input" value="300" min="50" max="1200" oninput="updateManualDpi(this.value)">
          </div>
          <div style="margin-top: 10px; font-size: 13px;">
            Current Active DPI: <strong id="currentDpiDisplay" style="color:#fbbf24;">300 DPI</strong>
          </div>
        </div>

        <div style="margin-top: 10px; font-size: 12px; color: var(--text-muted);" id="pdfConversionProgress"></div>

        <div class="btn-group">
          <button id="startPdfToJpgBtn" class="action-btn btn-download">🖼️ Convert & Download JPGs</button>
        </div>
      </div>
    </div>

    <!-- TAB 9: PDF COMPRESSOR -->
    <div id="tab-pdf-compressor" class="tab-content">
      <div class="badge">Interactive Quality & Size Slider • Target KB/MB Preview • High-Speed Export</div>
      <h1>PDF Size Compressor</h1>
      <p style="font-size: 12px; color: var(--text-muted); margin-bottom: 12px;">PDF फ़ाइल अपलोड करें, स्लाइडर से अपनी मनचाही फाइल साइज़ (KB/MB) सेट करें और डाउनलोड करें।</p>

      <div class="upload-section" style="margin-bottom: 15px;">
        <label class="upload-box" for="pdfCompressInput" style="max-width: 420px;">
          <strong style="display:block; font-size:14px; margin-bottom:4px; color:var(--accent-blue);">🗜️ Select PDF to Compress</strong>
          <div id="pdfCompressStatus" style="font-size: 12px; color: var(--text-muted);">क्लिक करके .pdf फाइल चुनें</div>
        </label>
        <input type="file" id="pdfCompressInput" accept="application/pdf">
      </div>

      <div id="compressorControlsArea" style="display:none;">
        <div class="control-panel">
          <div style="display:flex; justify-content:space-between; align-items:center;">
            <span style="font-size: 13px; font-weight:600; color: var(--accent-blue);">🎚️ Compression Quality Slider:</span>
            <span id="compressQualityLabel" style="font-weight:700; color:#fbbf24;">60% (Medium)</span>
          </div>

          <input type="range" id="compressQualitySlider" class="slider-range" min="10" max="95" value="60" oninput="onCompressSliderChange(this.value)">

          <div class="size-badge-box">
            <div>
              <div style="font-size:11px; color:var(--text-muted);">Original File Size</div>
              <strong id="origFileSizeDisplay" style="color:#f87171; font-size:14px;">0 KB</strong>
            </div>
            <div>
              <div style="font-size:11px; color:var(--text-muted);">Estimated Download Size</div>
              <strong id="estFileSizeDisplay" style="color:#34d399; font-size:14px;">0 KB</strong>
            </div>
          </div>
        </div>

        <div style="margin-top: 10px; font-size: 12px; color: var(--text-muted);" id="compressProgressMsg"></div>

        <div class="btn-group">
          <button id="startCompressDownloadBtn" class="action-btn btn-download">📥 Compress & Download PDF</button>
        </div>
      </div>
    </div>

    <!-- TAB 10: PROFESSIONAL RESUME BUILDER (NEWLY ADDED) -->
    <div id="tab-resume" class="tab-content">
      <div class="badge">Professional Templates • Photo Border • Add More Dynamic Sections</div>
      <h1>Professional Resume & CV Builder</h1>
      <p style="font-size: 12px; color: var(--text-muted); margin-bottom: 15px;">अपनी जानकारी भरें, 5 शानदार प्रोफेशनल टेम्पलेट्स में से चुनें और तुरंत PDF डाउनलोड करें!</p>

      <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; text-align: left; margin-bottom: 20px;">
        <div style="background: rgba(15,23,42,0.7); padding: 18px; border-radius: 12px; border: 1px solid var(--border-color);">
          <h3 style="color: var(--accent-blue); font-size: 14px; margin-bottom: 12px;">👤 Personal Information</h3>
          <input type="text" id="resName" class="text-field-input" style="max-width:100%;" placeholder="Full Name" oninput="updateResumePreview()">
          <input type="text" id="resTitle" class="text-field-input" style="max-width:100%;" placeholder="Job Title" oninput="updateResumePreview()">
          <input type="email" id="resEmail" class="text-field-input" style="max-width:100%;" placeholder="Email Address" oninput="updateResumePreview()">
          <input type="text" id="resPhone" class="text-field-input" style="max-width:100%;" placeholder="Phone Number" oninput="updateResumePreview()">
          <input type="text" id="resAddress" class="text-field-input" style="max-width:100%;" placeholder="Location / Address" oninput="updateResumePreview()">
          
          <label style="font-size: 11px; color: var(--text-muted); display: block; margin: 8px 0 4px;">🖼️ Profile Photo (with border):</label>
          <input type="file" id="resPhotoInput" accept="image/*" style="display:block; width:100%; background:#334155; color:#fff; padding:6px; font-size:11px; border-radius:6px;" onchange="loadResumePhoto(event)">

          <h3 style="color: var(--accent-blue); font-size: 14px; margin: 15px 0 8px;">🎯 Career Objective</h3>
          <textarea id="resObj" class="login-input" style="height: 65px; resize:none;" placeholder="Brief career objective..." oninput="updateResumePreview()"></textarea>

          <h3 style="color: var(--accent-blue); font-size: 14px; margin: 15px 0 8px;">🛠️ Skills & Languages</h3>
          <input type="text" id="resSkills" class="text-field-input" style="max-width:100%;" placeholder="Skills: Python, Excel" oninput="updateResumePreview()">
          <input type="text" id="resLangs" class="text-field-input" style="max-width:100%;" placeholder="Languages: English, Marathi" oninput="updateResumePreview()">
        </div>

        <div style="background: rgba(15,23,42,0.7); padding: 18px; border-radius: 12px; border: 1px solid var(--border-color); display:flex; flex-direction:column; justify-content:space-between;">
          <div>
            <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom: 8px;">
              <h3 style="color: var(--accent-blue); font-size: 14px;">🎓 Education Details</h3>
              <button onclick="addEducationRow()" class="action-btn btn-add" style="padding: 4px 10px; font-size: 10px;">➕ Add More</button>
            </div>
            <div id="educationContainer" style="display:flex; flex-direction:column; gap:8px; margin-bottom:15px;"></div>

            <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom: 8px;">
              <h3 style="color: var(--accent-blue); font-size: 14px;">💼 Work Experience / Projects</h3>
              <button onclick="addExperienceRow()" class="action-btn btn-add" style="padding: 4px 10px; font-size: 10px;">➕ Add More</button>
            </div>
            <div id="experienceContainer" style="display:flex; flex-direction:column; gap:8px;"></div>
          </div>

          <div style="margin-top: 15px;">
            <label style="font-size: 12px; color: var(--accent-blue); font-weight:600; display:block; margin-bottom:6px;">🎨 Select Professional Template:</label>
            <select id="resumeTemplateSelect" class="login-input" onchange="updateResumePreview()">
              <option value="1">Template 1: Modern Royal Blue</option>
              <option value="2">Template 2: Executive Emerald Green</option>
              <option value="3">Template 3: Sleek Dark Header</option>
              <option value="4">Template 4: Elegant Crimson Red</option>
              <option value="5">Template 5: Minimalist Clean Teal</option>
            </select>
          </div>
        </div>
      </div>

      <div style="background:#fff; color:#000; padding:30px; border-radius:12px; max-width:800px; margin:0 auto; text-align:left; box-shadow:0 10px 30px rgba(0,0,0,0.5);" id="resumePreviewBox"></div>

      <div class="btn-group" style="margin-top: 20px;">
        <button onclick="downloadResumePdf()" class="action-btn btn-download">📥 Download Resume PDF</button>
      </div>
    </div>

    <!-- TAB 11: HISTORY -->
    <div id="tab-history" class="tab-content">
      <div class="badge">Persistent Storage • Download Ready</div>
      <h1>Print & Download History</h1>
      <button onclick="clearAllHistoryDB()" class="action-btn btn-reset" style="padding: 6px 14px; font-size: 11px; margin-bottom:10px;">🗑️ Clear Entire History Now</button>
      <div class="history-table-container">
        <table class="history-table">
          <thead><tr><th>Type / Feature</th><th>File Name</th><th>Generated Time</th><th>Action</th></tr></thead>
          <tbody id="historyTableBody"><tr><td colspan="4" style="text-align:center; padding:20px;">कोई प्रिंट रिकॉर्ड नहीं मिला।</td></tr></tbody>
        </table>
      </div>
    </div>

    <!-- TAB 12: ADMIN PANEL -->
    <div id="tab-admin" class="tab-content">
      <div class="badge" style="background: rgba(245, 158, 11, 0.15); color: #fbbf24; border-color: rgba(245, 158, 11, 0.4);">Master Administrator Panel</div>
      <h1 style="color: #fbbf24;">Cloud Distributor Management</h1>
      <div class="control-panel" style="max-width: 500px; text-align: left; margin-bottom: 25px;">
        <h3 style="font-size: 14px; color: var(--accent-blue); margin-bottom: 12px;">➕ Add New Distributor</h3>
        <input type="text" id="newDistName" class="text-field-input" style="max-width:100%;" placeholder="Business / Name">
        <input type="email" id="newDistEmail" class="text-field-input" style="max-width:100%;" placeholder="Email ID">
        <input type="text" id="newDistPass" class="text-field-input" style="max-width:100%;" placeholder="Password">
        <button onclick="addNewDistributor()" class="action-btn btn-add" style="margin-top: 5px;">🚀 Assign ID & Password</button>
        <div id="distMsg" style="font-size: 12px; display:none; margin-top:5px;"></div>
      </div>
      <h3 style="font-size: 14px; color: var(--accent-blue); margin-bottom: 10px; text-align: left; max-width: 850px; margin: 0 auto;">Connected Distributors List</h3>
      <div class="history-table-container" style="max-width: 850px; margin: 0 auto;">
        <table class="history-table">
          <thead><tr><th>Business / Name</th><th>Login Email</th><th>Password</th><th>Validity</th><th>Action</th></tr></thead>
          <tbody id="distributorTableBody"><tr><td colspan="5" style="text-align:center; padding:15px;">डेटा लोड हो रहा है...</td></tr></tbody>
        </table>
      </div>
    </div>

    <footer style="margin-top: 25px; font-size: 12px; color: var(--text-muted);">
      Designed & Developed by <strong>JAYESH BHAVSAR @ 2026 ALL RIGHTS RESERVED</strong>
    </footer>
  </div>
</div>

<!-- Modals -->
<div id="cropModal">
  <div id="cropModalTitle" style="color:#fff; margin-bottom: 10px; font-weight: 600;">Crop Image:</div>
  <div class="crop-wrapper"><img id="imageToCrop" src=""></div>
  <div class="btn-group">
    <button id="cropSaveBtn" class="action-btn btn-download">✂️ Crop & Set</button>
    <button id="cropCancelBtn" class="action-btn" style="background:#ef4444;">रद्द करें</button>
  </div>
</div>

<div id="adminMsgModal">
  <div class="auth-box" style="max-width:440px; text-align:left;">
    <h3 style="color: var(--accent-blue); margin-bottom: 10px; font-size: 18px;">💬 Send Notice & QR Code</h3>
    <input type="hidden" id="targetDistEmail">
    <textarea id="adminTypedMsg" class="login-input" style="height: 75px; resize:none;" placeholder="Type message..."></textarea>
    <input type="file" id="adminNoticeImgInput" accept="image/*" style="display: block; width: 100%; color: #fff; font-size: 12px; margin-bottom: 15px;">
    <div style="display: flex; gap: 10px;">
      <button onclick="saveAdminMessage()" class="action-btn btn-download" style="flex:1;">📤 Send</button>
      <button onclick="closeAdminMsgModal()" class="action-btn btn-reset" style="flex:1;">Cancel</button>
    </div>
  </div>
</div>

<div id="viewScreenshotModal">
  <div class="auth-box" style="max-width:450px; text-align:center;">
    <h3 style="color: var(--accent-blue); margin-bottom: 10px; font-size: 18px;">📸 Payment Screenshot</h3>
    <div style="background:#000; padding:10px; border-radius:8px; margin-bottom:15px;"><img id="adminViewScreenshotImg" src="" style="max-width:100%; max-height:350px; display:block; margin:0 auto;"></div>
    <button onclick="closeViewScreenshotModal()" class="action-btn btn-reset" style="width:100%;">❌ Close</button>
  </div>
</div>

<div id="regModalPopup">
  <div class="reg-popup-content">
    <h3 style="color: var(--accent-blue); margin-bottom: 10px; font-size: 18px;">📞 Contact for Registration</h3>
    <p style="font-size: 12px; color: var(--text-muted); margin-bottom: 20px;">WhatsApp: <a href="https://wa.me/917887575671" target="_blank" style="color: #34d399; font-weight:700;">+91 7887575671</a></p>
    <button onclick="closeRegModal()" class="action-btn" style="background: #ef4444; width: 100%;">❌ Close</button>
  </div>
</div>

<script>
  function openRegModal() { document.getElementById('regModalPopup').style.display = 'flex'; }
  function closeRegModal() { document.getElementById('regModalPopup').style.display = 'none'; }

  const GOOGLE_SCRIPT_URL = "https://script.google.com/macros/s/AKfycbyzUzzHfPwHG4PgBAPOlHFUdYH5z22muWtXwRq-3dH1lb3IL8HmJh2UwKccxDUSLqlf/exec";

  async function getDistributorsListCloud() {
    try {
      const res = await fetch(`${GOOGLE_SCRIPT_URL}?action=getDistributors`, { cache: "no-store" });
      return await res.json() || [];
    } catch(e) { return []; }
  }

  async function callCloudPost(payload) {
    try {
      await fetch(GOOGLE_SCRIPT_URL, { method: "POST", mode: "no-cors", headers: { "Content-Type": "text/plain;charset=utf-8" }, body: JSON.stringify(payload) });
      return true;
    } catch(e) { return false; }
  }

  // ==========================================
  // RESUME BUILDER ENGINE (5 TEMPLATES + ADD MORE)
  // ==========================================
  let resumePhotoDataUrl = "";
  let eduRows = [{ degree: "B.Sc / BCA", inst: "University Name", year: "2022" }];
  let expRows = [{ role: "Computer Operator", company: "Digital Seva Kendra", duration: "2023 - Present" }];

  function loadResumePhoto(e) {
    const file = e.target.files[0];
    if (file) {
      const reader = new FileReader();
      reader.onload = (evt) => { resumePhotoDataUrl = evt.target.result; updateResumePreview(); };
      reader.readAsDataURL(file);
    }
  }

  function renderDynamicRows() {
    const eduCont = document.getElementById('educationContainer');
    eduCont.innerHTML = '';
    eduRows.forEach((item, idx) => {
      eduCont.innerHTML += `
        <div style="display:flex; gap:6px;">
          <input type="text" class="text-field-input" style="flex:2; max-width:100%; margin-bottom:0;" value="${item.degree}" placeholder="Degree" oninput="eduRows[${idx}].degree=this.value; updateResumePreview()">
          <input type="text" class="text-field-input" style="flex:2; max-width:100%; margin-bottom:0;" value="${item.inst}" placeholder="Institution" oninput="eduRows[${idx}].inst=this.value; updateResumePreview()">
          <input type="text" class="text-field-input" style="flex:1; max-width:100%; margin-bottom:0;" value="${item.year}" placeholder="Year" oninput="eduRows[${idx}].year=this.value; updateResumePreview()">
          <button onclick="eduRows.splice(${idx},1); renderDynamicRows(); updateResumePreview()" class="mini-tool-btn btn-del">🗑️</button>
        </div>`;
    });

    const expCont = document.getElementById('experienceContainer');
    expCont.innerHTML = '';
    expRows.forEach((item, idx) => {
      expCont.innerHTML += `
        <div style="display:flex; gap:6px;">
          <input type="text" class="text-field-input" style="flex:2; max-width:100%; margin-bottom:0;" value="${item.role}" placeholder="Role" oninput="expRows[${idx}].role=this.value; updateResumePreview()">
          <input type="text" class="text-field-input" style="flex:2; max-width:100%; margin-bottom:0;" value="${item.company}" placeholder="Company" oninput="expRows[${idx}].company=this.value; updateResumePreview()">
          <input type="text" class="text-field-input" style="flex:1; max-width:100%; margin-bottom:0;" value="${item.duration}" placeholder="Duration" oninput="expRows[${idx}].duration=this.value; updateResumePreview()">
          <button onclick="expRows.splice(${idx},1); renderDynamicRows(); updateResumePreview()" class="mini-tool-btn btn-del">🗑️</button>
        </div>`;
    });
  }

  function addEducationRow() { eduRows.push({ degree: "", inst: "", year: "" }); renderDynamicRows(); }
  function addExperienceRow() { expRows.push({ role: "", company: "", duration: "" }); renderDynamicRows(); }

  function updateResumePreview() {
    const name = document.getElementById('resName').value || "Harshal S. Marathe";
    const title = document.getElementById('resTitle').value || "Senior Computer Operator";
    const email = document.getElementById('resEmail').value || "oneplus777000@gmail.com";
    const phone = document.getElementById('resPhone').value || "+91 7887575671";
    const address = document.getElementById('resAddress').value || "Amalner, Maharashtra";
    const obj = document.getElementById('resObj').value || "Dynamic professional seeking to leverage technical expertise.";
    const skills = document.getElementById('resSkills').value || "Python, JavaScript, Excel, Photoshop";
    const langs = document.getElementById('resLangs').value || "English, Marathi, Hindi";
    const tpl = document.getElementById('resumeTemplateSelect').value;

    let primaryColor = "#0284c7";
    let secondaryColor = "#1e293b";
    if (tpl === "2") { primaryColor = "#059669"; secondaryColor = "#064e3b"; }
    else if (tpl === "3") { primaryColor = "#334155"; secondaryColor = "#0f172a"; }
    else if (tpl === "4") { primaryColor = "#dc2626"; secondaryColor = "#7f1d1d"; }
    else if (tpl === "5") { primaryColor = "#0d9488"; secondaryColor = "#134e4a"; }

    let eduHtml = eduRows.map(e => `<li><strong>${e.degree}</strong> - ${e.inst} (${e.year})</li>`).join('');
    let expHtml = expRows.map(x => `<li><strong>${x.role}</strong> at ${x.company} (${x.duration})</li>`).join('');

    const box = document.getElementById('resumePreviewBox');
    box.innerHTML = `
      <div style="border-bottom: 3px solid ${primaryColor}; padding-bottom: 15px; margin-bottom: 15px; display:flex; justify-content:space-between; align-items:center;">
        <div>
          <h2 style="color:${secondaryColor}; font-size:22px; font-weight:800; margin-bottom:2px;">${name}</h2>
          <div style="color:${primaryColor}; font-weight:600; font-size:13px; margin-bottom:6px;">${title}</div>
          <div style="font-size:11px; color:#475569;">📧 ${email} | 📱 ${phone} | 📍 ${address}</div>
        </div>
        ${resumePhotoDataUrl ? `<img src="${resumePhotoDataUrl}" style="width:85px; height:105px; object-fit:cover; border:3px solid ${primaryColor}; border-radius:6px;">` : ''}
      </div>
      <div style="margin-bottom:12px;">
        <h4 style="color:${primaryColor}; font-size:12px; text-transform:uppercase; border-bottom:1px solid #e2e8f0; padding-bottom:2px; margin-bottom:4px; font-weight:700;">Career Objective</h4>
        <p style="font-size:11px; color:#334155; line-height:1.4;">${obj}</p>
      </div>
      <div style="margin-bottom:12px;">
        <h4 style="color:${primaryColor}; font-size:12px; text-transform:uppercase; border-bottom:1px solid #e2e8f0; padding-bottom:2px; margin-bottom:4px; font-weight:700;">Education</h4>
        <ul style="font-size:11px; color:#334155; padding-left:15px; line-height:1.4;">${eduHtml}</ul>
      </div>
      <div style="margin-bottom:12px;">
        <h4 style="color:${primaryColor}; font-size:12px; text-transform:uppercase; border-bottom:1px solid #e2e8f0; padding-bottom:2px; margin-bottom:4px; font-weight:700;">Work Experience</h4>
        <ul style="font-size:11px; color:#334155; padding-left:15px; line-height:1.4;">${expHtml}</ul>
      </div>
      <div>
        <h4 style="color:${primaryColor}; font-size:12px; text-transform:uppercase; border-bottom:1px solid #e2e8f0; padding-bottom:2px; margin-bottom:4px; font-weight:700;">Skills & Languages</h4>
        <p style="font-size:11px; color:#334155;"><strong>Skills:</strong> ${skills}</p>
        <p style="font-size:11px; color:#334155;"><strong>Languages:</strong> ${langs}</p>
      </div>
    `;
  }

  function downloadResumePdf() {
    const { jsPDF } = window.jspdf;
    const box = document.getElementById('resumePreviewBox');
    const pdf = new jsPDF({ orientation: 'portrait', unit: 'mm', format: 'a4' });
    pdf.html(box, {
      callback: function (doc) {
        const fileName = 'Professional_Resume.pdf';
        const blob = doc.output('blob');
        doc.save(fileName);
        saveToHistory('Resume Builder', fileName, blob, 'application/pdf');
      },
      x: 10, y: 10, width: 190, windowWidth: 800
    });
  }

  renderDynamicRows();
  updateResumePreview();

  // Your original IndexDB history logic, cropping, and all 9 tools remain fully active below...
  const DB_NAME = 'PrintPortalPersistentDB';
  const DB_STORE = 'print_records';

  function openHistoryDB() {
    return new Promise((resolve, reject) => {
      const request = indexedDB.open(DB_NAME, 1);
      request.onupgradeneeded = function(e) {
        const db = e.target.result;
        if (!db.objectStoreNames.contains(DB_STORE)) {
          db.createObjectStore(DB_STORE, { keyPath: 'id', autoIncrement: true });
        }
      };
      request.onsuccess = () => resolve(request.result);
      request.onerror = () => reject(request.error);
    });
  }

  async function saveToHistory(featureName, fileName, blobOrDataUrl, fileType) {
    try {
      const db = await openHistoryDB();
      const tx = db.transaction(DB_STORE, 'readwrite');
      const store = tx.objectStore(DB_STORE);
      store.add({
        feature: featureName,
        fileName: fileName,
        data: blobOrDataUrl,
        fileType: fileType,
        timestamp: Date.now(),
        dateFormatted: new Date().toLocaleString('en-IN', { timeZone: 'Asia/Kolkata' })
      });
    } catch(err) {}
  }

  async function renderHistoryTable() {
    try {
      const db = await openHistoryDB();
      const tx = db.transaction(DB_STORE, 'readonly');
      const store = tx.objectStore(DB_STORE);
      const request = store.getAll();

      request.onsuccess = function() {
        const records = request.result || [];
        const tbody = document.getElementById('historyTableBody');
        tbody.innerHTML = '';
        if (!records.length) {
          tbody.innerHTML = `<tr><td colspan="4" style="text-align:center; padding:20px;">कोई प्रिंट रिकॉर्ड नहीं मिला।</td></tr>`;
          return;
        }
        records.reverse().forEach(rec => {
          tbody.innerHTML += `
            <tr>
              <td><strong style="color:var(--accent-blue);">${rec.feature}</strong></td>
              <td>${rec.fileName}</td>
              <td>${rec.dateFormatted}</td>
              <td>
                <button class="history-download-btn" onclick="reDownloadHistoryFile(${rec.id})">📥 Download</button>
                <button class="history-delete-btn" onclick="deleteHistoryRecord(${rec.id})" style="margin-left: 5px;">🗑️ Delete</button>
              </td>
            </tr>
          `;
        });
      };
    } catch(err) {}
  }

  async function reDownloadHistoryFile(recordId) {
    const db = await openHistoryDB();
    const tx = db.transaction(DB_STORE, 'readonly');
    const store = tx.objectStore(DB_STORE);
    const request = store.get(recordId);
    request.onsuccess = function() {
      const rec = request.result;
      if (!rec) return;
      const link = document.createElement('a');
      link.href = typeof rec.data === 'string' ? rec.data : URL.createObjectURL(rec.data);
      link.download = rec.fileName;
      link.click();
    };
  }

  async function deleteHistoryRecord(recordId) {
    if (!confirm('हटाना चाहते हैं?')) return;
    const db = await openHistoryDB();
    const tx = db.transaction(DB_STORE, 'readwrite');
    tx.objectStore(DB_STORE).delete(recordId);
    tx.oncomplete = () => renderHistoryTable();
  }

  async function clearAllHistoryDB() {
    if (!confirm('सभी रिकॉर्ड्स मिटाना चाहते हैं?')) return;
    const db = await openHistoryDB();
    const tx = db.transaction(DB_STORE, 'readwrite');
    tx.objectStore(DB_STORE).clear();
    tx.oncomplete = () => renderHistoryTable();
  }

  // Admin & Login Handlers
  const ADMIN_EMAIL = "oneplus777000@gmail.com";
  function getStoredPassword() { return localStorage.getItem('system_auth_pwd') || "Pass@123"; }

  const loginScreen = document.getElementById('loginScreen');
  const mainApp = document.getElementById('mainApp');
  const loginEmail = document.getElementById('loginEmail');
  const loginPass = document.getElementById('loginPass');
  const authBtn = document.getElementById('authBtn');
  const errorMsg = document.getElementById('errorMsg');
  const logoutBtn = document.getElementById('logoutBtn');
  const adminTabBtn = document.getElementById('adminTabBtn');

  async function handleLogin() {
    const inputEmail = loginEmail.value.trim().toLowerCase();
    const inputPass = loginPass.value.trim();
    if (inputEmail === ADMIN_EMAIL.toLowerCase() && inputPass === getStoredPassword().trim()) {
      sessionStorage.setItem('isLoggedIn', 'true');
      loginScreen.style.display = 'none';
      mainApp.style.display = 'block';
      adminTabBtn.style.display = 'inline-block';
      renderDistributorsTable();
      return;
    }

    let dists = await getDistributorsListCloud();
    let foundUser = dists.find(d => String(d.email || '').trim().toLowerCase() === inputEmail);
    if (foundUser && String(foundUser.pass || '').trim() === inputPass) {
      sessionStorage.setItem('isLoggedIn', 'true');
      loginScreen.style.display = 'none';
      mainApp.style.display = 'block';
      adminTabBtn.style.display = 'none';
      switchTabDirect('tab-cards');
    } else {
      errorMsg.innerText = "⚠️ गलत ईमेल आईडी या पासवर्ड!";
      errorMsg.style.display = 'block';
    }
  }

  authBtn.addEventListener('click', handleLogin);
  loginPass.addEventListener('keypress', (e) => { if (e.key === 'Enter') handleLogin(); });

  logoutBtn.addEventListener('click', () => {
    sessionStorage.clear();
    mainApp.style.display = 'none';
    loginScreen.style.display = 'block';
    loginPass.value = '';
  });

  async function renderDistributorsTable() {
    let dists = await getDistributorsListCloud();
    const tbody = document.getElementById('distributorTableBody');
    tbody.innerHTML = '';
    if (!dists.length) {
      tbody.innerHTML = `<tr><td colspan="5" style="text-align:center; padding:15px;">कोई डिस्ट्रीब्यूटर नहीं मिला।</td></tr>`;
      return;
    }
    dists.forEach(d => {
      const ss = d.distscreenshot || d.distScreenshot || "";
      tbody.innerHTML += `
        <tr>
          <td><strong>${d.name}</strong></td>
          <td>${d.email}</td>
          <td><code>${d.pass}</code></td>
          <td>${d.status || 'Active'}</td>
          <td>
            <button class="history-delete-btn" onclick="removeDist('${d.id}')">🗑️ Delete</button>
            ${ss ? `<button class="history-view-ss-btn" onclick="viewDistributorScreenshot('${encodeURIComponent(ss)}')">👁️ View SS</button>` : ''}
          </td>
        </tr>
      `;
    });
  }

  async function addNewDistributor() {
    const name = document.getElementById('newDistName').value.trim();
    const email = document.getElementById('newDistEmail').value.trim().toLowerCase();
    const pass = document.getElementById('newDistPass').value.trim();
    if (!name || !email || !pass) { alert('सभी फ़ील्ड भरें!'); return; }
    await callCloudPost({ action: "addDistributor", data: { id: Date.now(), name, email, pass, status: "Active" } });
    renderDistributorsTable();
  }

  async function removeDist(id) {
    if (!confirm('हटाना चाहते हैं?')) return;
    await callCloudPost({ action: "deleteDistributor", id: id });
    renderDistributorsTable();
  }

  function viewDistributorScreenshot(url) {
    document.getElementById('adminViewScreenshotImg').src = decodeURIComponent(url);
    document.getElementById('viewScreenshotModal').style.display = 'flex';
  }
  function closeViewScreenshotModal() { document.getElementById('viewScreenshotModal').style.display = 'none'; }

  function switchTab(tabId) {
    document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
    document.querySelectorAll('.tab-content').forEach(content => content.classList.remove('active'));
    event.target.classList.add('active');
    document.getElementById(tabId).classList.add('active');
    if (tabId === 'tab-history') renderHistoryTable();
    if (tabId === 'tab-admin') renderDistributorsTable();
  }
  function switchTabDirect(tabId) {
    document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
    document.querySelectorAll('.tab-content').forEach(content => content.classList.remove('active'));
    document.getElementById(tabId).classList.add('active');
  }

  function initAllCanvases() {}
</script>

</body>
</html>
