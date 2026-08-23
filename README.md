<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>ALL PRINTING SERVICES WORKING FINE</title>
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
      --bg-gradient: linear-gradient(135deg, #090d16 0%, #111827 50%, #090d16 100%);
      --card-bg: rgba(17, 24, 39, 0.9);
      --accent-blue: #38bdf8;
      --accent-purple: #a855f7;
      --btn-add: linear-gradient(135deg, #f59e0b 0%, #d97706 100%);
      --btn-download: linear-gradient(135deg, #10b981 0%, #059669 100%);
      --text-main: #f3f4f6;
      --text-muted: #9ca3af;
      --border-color: rgba(56, 189, 248, 0.15);
    }

    * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Poppins', sans-serif; }
    
    body { 
      background: var(--bg-gradient); 
      min-height: 100vh;
      padding: 20px 10px; 
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
      background: linear-gradient(135deg, #38bdf8 0%, #a855f7 50%, #ec4899 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      margin-bottom: 20px;
      text-align: center;
    }

    .auth-box {
      background: var(--card-bg);
      backdrop-filter: blur(25px);
      border: 1px solid var(--border-color);
      padding: 40px 30px;
      border-radius: 24px;
      box-shadow: 0 30px 70px rgba(0, 0, 0, 0.7);
      width: 100%;
      max-width: 420px;
      text-align: center;
    }

    .badge {
      display: inline-block;
      padding: 5px 16px;
      font-size: 11px;
      font-weight: 600;
      letter-spacing: 1px;
      text-transform: uppercase;
      background: rgba(56, 189, 248, 0.1);
      color: var(--accent-blue);
      border: 1px solid rgba(56, 189, 248, 0.3);
      border-radius: 20px;
      margin-bottom: 15px;
    }

    .slot-counter-badge {
      background: rgba(245, 158, 11, 0.12);
      color: #fbbf24;
      border: 1px solid rgba(245, 158, 11, 0.3);
      padding: 6px 16px;
      font-size: 12px;
      font-weight: 600;
      border-radius: 20px;
      display: inline-block;
      margin-bottom: 15px;
    }

    .login-input {
      width: 100%;
      padding: 14px 16px;
      margin-bottom: 16px;
      background: rgba(3, 7, 18, 0.8);
      border: 1px solid rgba(56, 189, 248, 0.3);
      border-radius: 12px;
      color: #fff;
      font-size: 14px;
      outline: none;
      transition: 0.2s;
    }
    .login-input:focus {
      border-color: var(--accent-blue);
      box-shadow: 0 0 10px rgba(56, 189, 248, 0.2);
    }

    .login-btn {
      width: 100%;
      padding: 14px;
      background: linear-gradient(135deg, #0284c7 0%, #2563eb 100%);
      color: #fff;
      font-weight: 600;
      border: none;
      border-radius: 12px;
      cursor: pointer;
      font-size: 15px;
      transition: 0.3s;
    }
    .login-btn:hover { opacity: 0.9; transform: translateY(-1px); }

    .auth-link {
      display: inline-block;
      margin-top: 16px;
      font-size: 13px;
      color: var(--accent-blue);
      cursor: pointer;
      text-decoration: underline;
    }

    .error-msg {
      color: #f87171;
      font-size: 13px;
      margin-top: 12px;
      display: none;
    }

    .tab-nav {
      display: flex;
      justify-content: center;
      gap: 8px;
      margin-bottom: 18px;
      flex-wrap: wrap;
    }

    .tab-btn {
      padding: 10px 14px;
      background: rgba(15, 23, 42, 0.8);
      border: 1px solid rgba(255, 255, 255, 0.08);
      color: var(--text-muted);
      border-radius: 12px;
      cursor: pointer;
      font-weight: 600;
      font-size: 12px;
      transition: 0.3s;
    }
    .tab-btn:hover { color: #fff; border-color: rgba(56, 189, 248, 0.4); }

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
      backdrop-filter: blur(20px);
      border: 1px solid var(--border-color);
      padding: 30px 24px; 
      border-radius: 24px; 
      box-shadow: 0 25px 60px rgba(0, 0, 0, 0.6); 
      width: 100%; 
      text-align: center; 
      position: relative; 
    }

    .logout-btn {
      background: rgba(239, 68, 68, 0.15);
      border: 1px solid rgba(239, 68, 68, 0.4);
      color: #fca5a5;
      padding: 8px 16px;
      font-size: 12px;
      font-weight: 600;
      border-radius: 10px;
      cursor: pointer;
      transition: 0.2s;
    }
    .logout-btn:hover { background: rgba(239, 68, 68, 0.3); }

    h1 { 
      background: linear-gradient(to right, #38bdf8, #a855f7, #ec4899);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      font-size: 22px; 
      font-weight: 700;
      margin-bottom: 8px; 
    }

    .tab-content { display: none; }
    .tab-content.active { display: block; }

    .upload-section { 
      display: flex; 
      gap: 15px; 
      justify-content: center; 
      margin: 18px 0; 
      flex-wrap: wrap; 
    }

    .upload-box { 
      border: 2px dashed rgba(56, 189, 248, 0.3); 
      padding: 18px 16px; 
      border-radius: 16px; 
      cursor: pointer; 
      background: rgba(3, 7, 18, 0.6); 
      flex: 1; 
      min-width: 220px; 
      transition: 0.3s; 
    }
    .upload-box:hover { 
      border-color: var(--accent-blue);
      background: rgba(56, 189, 248, 0.06);
    }

    input[type="file"] { display: none; }

    .preview-container { 
      display: flex; 
      justify-content: center; 
      gap: 20px; 
      margin: 18px 0; 
      flex-wrap: wrap; 
    }

    .preview-box { 
      border: 1px solid var(--border-color); 
      padding: 12px; 
      background: rgba(3, 7, 18, 0.7); 
      border-radius: 14px; 
    }

    .preview-box h4 { 
      font-size: 12px; 
      color: var(--text-muted); 
      margin-bottom: 8px; 
    }
    
    canvas { 
      max-width: 100%; 
      height: auto; 
      display: block; 
      margin: 0 auto; 
      border-radius: 6px;
      background: #fff; 
    }

    .btn-group { 
      display: flex; 
      gap: 10px; 
      justify-content: center; 
      margin-top: 18px; 
      flex-wrap: wrap; 
    }

    .action-btn { 
      padding: 11px 22px; 
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
      box-shadow: 0 6px 20px rgba(0,0,0,0.5);
    }

    .btn-add { background: var(--btn-add); }
    .btn-download { background: var(--btn-download); }
    .btn-reset { background: rgba(239, 68, 68, 0.2); border: 1px solid rgba(239, 68, 68, 0.4); color: #fca5a5; }

    .btn-manual-crop {
      background: rgba(56, 189, 248, 0.15);
      border: 1px solid var(--accent-blue);
      color: var(--accent-blue);
      padding: 5px 12px;
      font-size: 11px;
      border-radius: 8px;
      margin-top: 8px;
      cursor: pointer;
      font-weight: 600;
      transition: 0.2s;
    }
    .btn-manual-crop:hover { background: var(--accent-blue); color: #0f172a; }

    .action-btn:disabled { 
      background: #1f2937; 
      color: #4b5563; 
      cursor: not-allowed; 
      box-shadow: none;
    }

    .control-panel {
      background: rgba(3, 7, 18, 0.6);
      border: 1px solid var(--border-color);
      border-radius: 16px;
      padding: 16px 20px;
      max-width: 600px;
      margin: 18px auto;
      text-align: center;
    }

    .qty-select-group {
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
      margin-top: 10px;
      flex-wrap: wrap;
    }

    .qty-input {
      width: 80px;
      padding: 8px 10px;
      border-radius: 10px;
      background: rgba(3, 7, 18, 0.9);
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
      padding: 9px 12px;
      border-radius: 10px;
      background: rgba(3, 7, 18, 0.9);
      border: 1px solid var(--accent-blue);
      color: #fff;
      font-size: 13px;
      outline: none;
      margin-bottom: 4px;
    }

    .quick-qty-btn {
      padding: 6px 12px;
      background: #1f2937;
      border: 1px solid rgba(255, 255, 255, 0.1);
      color: #fff;
      border-radius: 8px;
      font-size: 11px;
      cursor: pointer;
      font-weight: 600;
      transition: 0.2s;
    }
    .quick-qty-btn:hover { background: #374151; }

    .slider-range {
      -webkit-appearance: none;
      width: 100%;
      height: 6px;
      border-radius: 5px;
      background: #1f2937;
      outline: none;
      margin: 8px 0 10px 0;
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
      background: rgba(3, 7, 18, 0.8);
      padding: 12px;
      border-radius: 12px;
      margin-top: 12px;
      border: 1px solid var(--border-color);
    }

    .file-gallery-list {
      display: flex;
      flex-wrap: wrap;
      gap: 14px;
      justify-content: center;
      margin: 18px 0;
      max-height: 420px;
      overflow-y: auto;
      padding: 16px;
      background: rgba(3, 7, 18, 0.7);
      border-radius: 14px;
      border: 1px solid var(--border-color);
    }

    .draggable-card {
      position: relative;
      width: 125px;
      background: #030712;
      border: 2px solid rgba(56, 189, 248, 0.3);
      border-radius: 12px;
      padding: 8px 6px 10px 6px;
      display: flex;
      flex-direction: column;
      align-items: center;
      box-shadow: 0 6px 16px rgba(0,0,0,0.6);
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
      border-radius: 6px;
      pointer-events: none;
    }

    .draggable-card .file-label {
      font-size: 11px;
      color: #9ca3af;
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
      width: 100%;
      margin: 6px 0 4px 0;
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
      background: #1f2937;
      color: #f3f4f6;
      border: 1px solid rgba(255,255,255,0.12);
      border-radius: 6px;
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
      border: 2px solid #030712;
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
      margin-top: 18px;
      overflow-x: auto;
      background: rgba(3, 7, 18, 0.7);
      border-radius: 14px;
      border: 1px solid var(--border-color);
    }

    .history-table {
      width: 100%;
      border-collapse: collapse;
      font-size: 12px;
      text-align: left;
    }

    .history-table th, .history-table td {
      padding: 12px 16px;
      border-bottom: 1px solid rgba(255, 255, 255, 0.06);
    }

    .history-table th {
      background: rgba(17, 24, 39, 0.95);
      color: var(--accent-blue);
      font-weight: 600;
    }

    .history-table tr:hover { background: rgba(56, 189, 248, 0.04); }

    .history-download-btn {
      background: #0284c7;
      color: #fff;
      border: none;
      padding: 6px 12px;
      border-radius: 8px;
      cursor: pointer;
      font-size: 11px;
      font-weight: 600;
      margin-right: 6px;
      transition: 0.2s;
    }
    .history-download-btn:hover { background: #0369a1; }

    .history-delete-btn {
      background: rgba(239, 68, 68, 0.2);
      color: #fca5a5;
      border: 1px solid rgba(239, 68, 68, 0.4);
      padding: 6px 12px;
      border-radius: 8px;
      cursor: pointer;
      font-size: 11px;
      font-weight: 600;
      transition: 0.2s;
    }
    .history-delete-btn:hover { background: rgba(239, 68, 68, 0.4); }

    /* Modal System */
    .generic-modal {
      display: none !important;
      position: fixed;
      top: 0; left: 0; width: 100%; height: 100%;
      background: rgba(0, 0, 0, 0.88);
      backdrop-filter: blur(8px);
      z-index: 99999;
      align-items: center;
      justify-content: center;
      padding: 20px;
    }

    .generic-modal.active-modal {
      display: flex !important;
    }

    .generic-modal-box {
      background: var(--card-bg);
      border: 1px solid var(--accent-blue);
      border-radius: 20px;
      padding: 30px 24px;
      max-width: 440px;
      width: 100%;
      text-align: center;
      box-shadow: 0 20px 60px rgba(0, 0, 0, 0.8);
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
  </style>
</head>
<body>

<div class="portal-main-heading">
  ALL PRINTING SERVICES WORKING FINE
</div>

<!-- 1. Login Screen -->
<div id="loginScreen" class="auth-box">
  <div class="badge">Protected Access</div>
  <h2 style="font-size: 22px; margin-bottom: 6px;">Sign In</h2>
  <p style="font-size: 12px; color: var(--text-muted); margin-bottom: 20px;">Card & Photo Generator Portal</p>

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
  <p style="font-size: 12px; color: var(--text-muted); margin-bottom: 20px;">पुराने पासवर्ड का उपयोग करके नया पासवर्ड सेट करें</p>

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
    <button id="historyTabBtn" class="tab-btn" onclick="switchTab('tab-history')" style="border-color: rgba(56, 189, 248, 0.5);">📂 History (60-Day)</button>
  </div>

  <div class="container">
    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 18px; flex-wrap: wrap; gap: 10px;">
      <div id="validityCounterBadge" style="background: rgba(16, 185, 129, 0.15); border: 1px solid #10b981; color: #34d399; padding: 6px 14px; border-radius: 20px; font-size: 12px; font-weight: 600;">
        ⏳ Validity: Initializing...
      </div>
      <button id="logoutBtn" class="logout-btn">🔒 Logout</button>
    </div>

    <!-- TAB 1: 5 CARDS SYSTEM (FULLY MANUAL 4-WAY & CORNER CROPPING) -->
    <div id="tab-cards" class="tab-content active">
      <div class="badge">Fully Manual Precision Cropper • Exact 1013×638 Fit • 2.5mm Gap • 5 Cards</div>
      <h1>Card Generator System</h1>
      <p style="font-size: 12px; color: var(--text-muted); margin-bottom: 10px;">इमेज या PDF अपलोड करें। फाइल आते ही **Manual Crop Box** खुलेगा जहाँ से आप चारों कोनों और साइड्स को अपनी मर्जी से सेट करके बिल्कुल सटीक 1013×638 साइज में ला सकते हैं।</p>
      
      <div id="slotCounter" class="slot-counter-badge">Cards on Page: 0 / 5 (Next Slot: #1)</div>

      <div class="upload-section">
        <label class="upload-box" for="card1Input">
          <strong style="display:block; font-size:14px; margin-bottom:4px;">📁 Front Side (Upload & Crop)</strong>
          <div id="file1Name" style="font-size: 12px; color: var(--text-muted);">इमेज या PDF चुनें</div>
        </label>
        <input type="file" id="card1Input" accept="image/*,application/pdf">

        <label class="upload-box" for="card2Input">
          <strong style="display:block; font-size:14px; margin-bottom:4px;">📁 Back Side (Upload & Crop)</strong>
          <div id="file2Name" style="font-size: 12px; color: var(--text-muted);">इमेज या PDF चुनें</div>
        </label>
        <input type="file" id="card2Input" accept="image/*,application/pdf">
      </div>

      <div class="preview-container">
        <div class="preview-box">
          <h4>Front Card Preview</h4>
          <canvas id="canvas1" width="1013" height="638" style="width: 180px;"></canvas>
          <button id="manualCropFrontBtn" class="btn-manual-crop" style="display:none;" onclick="openManualCropForCard('front')">✂️ Recrop Front</button>
        </div>
        <div class="preview-box">
          <h4>Back Card Preview</h4>
          <canvas id="canvas2" width="1013" height="638" style="width: 180px;"></canvas>
          <button id="manualCropBackBtn" class="btn-manual-crop" style="display:none;" onclick="openManualCropForCard('back')">✂️ Recrop Back</button>
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

    <!-- TAB 2: PASSPORT SIZE PHOTOS (STANDARD) -->
    <div id="tab-passport" class="tab-content">
      <div class="badge">Standard 35mm × 45mm • Manual Quantity Selection</div>
      <h1>Passport Photo Generator</h1>
      <p style="font-size: 12px; color: var(--text-muted); margin-bottom: 15px;">फ़ोटो अपलोड करें, संख्या (Quantity) चुनें और शीट तैयार करें।</p>

      <div class="upload-section">
        <label class="upload-box" for="passportInput" style="max-width: 380px;">
          <strong style="display:block; font-size:14px; margin-bottom:4px;">📁 Passport Photo Upload</strong>
          <div id="passportFileName" style="font-size: 12px; color: var(--text-muted);">फ़ोटो चुनें व क्रॉप करें</div>
        </label>
        <input type="file" id="passportInput" accept="image/*">
      </div>

      <div class="preview-container">
        <div class="preview-box">
          <h4>Cropped Passport Photo</h4>
          <canvas id="passportCanvas" width="413" height="531" style="width: 140px;"></canvas>
        </div>
      </div>

      <div class="control-panel">
        <span style="font-size: 14px; font-weight:600; color: var(--accent-blue);">🔢 फ़ोटो की संख्या (Quantity) चुनें:</span>
        <div class="qty-select-group">
          <input type="number" id="passportQtyInput" class="qty-input" value="8" min="1" max="30">
          <button class="quick-qty-btn" onclick="setPassportQty(4)">4</button>
          <button class="quick-qty-btn" onclick="setPassportQty(6)">6</button>
          <button class="quick-qty-btn" onclick="setPassportQty(8)">8</button>
          <button class="quick-qty-btn" onclick="setPassportQty(12)">12</button>
          <button class="quick-qty-btn" onclick="setPassportQty(16)">16</button>
          <button class="quick-qty-btn" onclick="setPassportQty(30)">30</button>
        </div>
      </div>

      <div class="btn-group">
        <button id="make4x6CustomPassportBtn" class="action-btn btn-add" disabled>🖼️ Generate on 4×6 Sheet</button>
        <button id="makeA4CustomPassportBtn" class="action-btn btn-add" disabled>📄 Generate on A4 Sheet</button>
      </div>

      <div style="margin-top: 25px; border-top: 1px solid var(--border-color); padding-top: 15px;">
        <h3 id="passportSheetTitle" style="font-size: 15px; color: var(--accent-blue); margin-bottom: 6px;">Passport Sheet Preview</h3>
        <div style="display:inline-block; max-width: 250px; background:#fff; border-radius:6px; overflow:hidden; border: 1px solid #475569;">
          <canvas id="passportSheetCanvas" width="1800" height="1200" style="width: 100%; display:block;"></canvas>
        </div>
        <div class="btn-group">
          <button id="downloadPassportPdfBtn" class="action-btn btn-download" disabled>📥 Download Passport Sheet PDF</button>
        </div>
      </div>
    </div>

    <!-- TAB 3: NAME & DATE PASSPORT PHOTO MAKER -->
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
          <div style="background:rgba(3,7,18,0.6); padding:10px 12px; border-radius:10px; border:1px solid var(--border-color);">
            <div style="display:flex; justify-content:space-between; align-items:center;">
              <label style="font-size:11px; color:var(--text-muted);">👤 Candidate Name:</label>
              <span id="nameFontLabel" style="font-size:11px; color:var(--accent-blue); font-weight:600;">Size: 24px</span>
            </div>
            <input type="text" id="candNameInput" class="text-field-input" style="max-width:100%;" placeholder="e.g. HARSHAL SATISH MARATHE" oninput="renderNamePassportPreview()">
            <input type="range" id="nameFontSlider" class="slider-range" min="14" max="36" value="24" oninput="updateNameFontSize(this.value)">
          </div>

          <div style="background:rgba(3,7,18,0.6); padding:10px 12px; border-radius:10px; border:1px solid var(--border-color);">
            <div style="display:flex; justify-content:space-between; align-items:center;">
              <label style="font-size:11px; color:var(--text-muted);">🎂 Date of Birth (DOB):</label>
              <span id="dobFontLabel" style="font-size:11px; color:var(--accent-blue); font-weight:600;">Size: 20px</span>
            </div>
            <input type="text" id="candDobInput" class="text-field-input" style="max-width:100%;" placeholder="e.g. 15/08/1998" oninput="renderNamePassportPreview()">
            <input type="range" id="dobFontSlider" class="slider-range" min="12" max="30" value="20" oninput="updateDobFontSize(this.value)">
          </div>

          <div style="background:rgba(3,7,18,0.6); padding:10px 12px; border-radius:10px; border:1px solid var(--border-color);">
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

    <!-- TAB 5: PDF ARRANGER (DRAG & DROP / HOLD & MOVE) -->
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

    <!-- TAB 6: UNIVERSAL MERGE & RE-ORDER -->
    <div id="tab-jpg-to-pdf" class="tab-content">
      <div class="badge">Universal File Merger • Drag & Drop Re-order • Individual Delete</div>
      <h1>PDF, JPG, PNG to PDF Converter</h1>
      <p style="font-size: 12px; color: var(--text-muted); margin-bottom: 12px;">फ़ाइलों को <strong>माउस से पकड़कर आगे-पीछे क्रमबद्ध करें</strong> और कंबाइंड PDF बनाएँ।</p>

      <div class="upload-section" style="margin-bottom: 15px;">
        <label class="upload-box" for="universalMultiInput" style="max-width: 450px;">
          <strong style="display:block; font-size:14px; margin-bottom:4px; color:var(--accent-blue);">📁 Select Files (PDF, JPG, PNG Allowed)</strong>
          <div id="universalMultiStatus" style="font-size: 12px; color: var(--text-muted);">क्लिक करके PDF या इमेज फाइलें चुनें</div>
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

    <!-- TAB 7: CUSTOM IMAGE RESIZER -->
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

    <!-- TAB 8: PDF TO HIGH-DPI JPG CONVERTER (WITH PASSWORD UNLOCK FEATURE) -->
    <div id="tab-pdf-to-jpg" class="tab-content">
      <div class="badge">Password Unlock • Ultra High-Res • Manual & Quick DPI • Batch ZIP Export</div>
      <h1>PDF to High-DPI JPG Converter</h1>
      <p style="font-size: 12px; color: var(--text-muted); margin-bottom: 12px;">PDF फ़ाइल अपलोड करें। यदि PDF पासवर्ड प्रोटेक्टेड है, तो पासवर्ड दर्ज करके अनलॉक करें।</p>

      <div class="upload-section" style="margin-bottom: 15px;">
        <label class="upload-box" for="pdfToJpgInput" style="max-width: 420px;">
          <strong style="display:block; font-size:14px; margin-bottom:4px; color:var(--accent-blue);">📄 Select PDF File to Convert</strong>
          <div id="pdfToJpgStatus" style="font-size: 12px; color: var(--text-muted);">क्लिक करके .pdf फाइल चुनें</div>
        </label>
        <input type="file" id="pdfToJpgInput" accept="application/pdf">
      </div>

      <!-- Password Input Box for Protected PDFs -->
      <div id="pdfPasswordBox" style="display:none; max-width: 400px; margin: 15px auto; background: rgba(3, 7, 18, 0.8); padding: 15px; border-radius: 12px; border: 1px solid rgba(239, 68, 68, 0.4);">
        <div style="font-size: 12px; color: #f87171; font-weight: 600; margin-bottom: 6px;">🔒 Protected PDF Detected! Enter Password:</div>
        <div style="display:flex; gap:8px;">
          <input type="password" id="pdfPasswordInput" class="text-field-input" style="max-width:100%; margin:0;" placeholder="PDF Password">
          <button class="action-btn btn-add" style="padding: 8px 14px; font-size:12px;" onclick="unlockAndLoadProtectedPdf()">🔓 Unlock</button>
        </div>
        <div id="pdfPasswordError" style="font-size: 11px; color: #ef4444; margin-top: 6px; display:none;">⚠️ गलत पासवर्ड! कृपया पुनः प्रयास करें।</div>
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

    <!-- TAB 10: DYNAMIC PRINT HISTORY -->
    <div id="tab-history" class="tab-content">
      <div id="historyRetentionBadge" class="badge">Automatic 60-Day Storage • All Features Supported</div>
      <h1 id="historyHeaderTitle">60-Day Print & Download History</h1>
      <p id="historyDescText" style="font-size: 12px; color: var(--text-muted); margin-bottom: 12px;">आपके द्वारा डाउनलोड की गई सभी फाइल्स यहाँ सुरक्षित हैं।</p>

      <div style="text-align: right; margin-bottom: 12px;">
        <button onclick="clearAllHistoryDB()" class="action-btn btn-reset" style="padding: 7px 14px; font-size: 11px;">🗑️ Clear Entire History Now</button>
      </div>

      <div class="history-table-container">
        <table class="history-table">
          <thead>
            <tr>
              <th>Type / Feature</th>
              <th>File Name</th>
              <th>Generated Time</th>
              <th>Action</th>
            </tr>
          </thead>
          <tbody id="historyTableBody">
            <tr>
              <td colspan="4" style="text-align:center; color:var(--text-muted); padding:20px;">कोई प्रिंट रिकॉर्ड नहीं मिला।</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>

    <footer style="margin-top: 30px; font-size: 12px; color: var(--text-muted); font-weight: 600; letter-spacing: 0.5px;">
      DESIGNED AND DEVELOPED BY - EASYWAYTECH - @2026 ALL RIGHTS RESERVED
    </footer>
  </div>
</div>

<!-- Global Crop Modal -->
<div id="cropModal" class="generic-modal">
  <div class="generic-modal-box" style="max-width: 90vw; padding: 20px;">
    <div id="cropModalTitle" style="color:#fff; margin-bottom: 10px; font-weight: 600;">आईडी कार्ड का सही हिस्सा सेलेक्ट (Crop) करें:</div>
    <div class="crop-wrapper">
      <img id="imageToCrop" src="">
    </div>
    <div class="btn-group">
      <button id="cropSaveBtn" class="action-btn btn-download">✂️ Crop & Set to ID Size</button>
      <button id="cropCancelBtn" class="action-btn" style="background:#ef4444;">रद्द करें</button>
    </div>
  </div>
</div>

<script>
  if (typeof pdfjsLib !== 'undefined') {
    pdfjsLib.GlobalWorkerOptions.workerSrc = '';
  }

  const AUTH_EMAIL = "oneplus777000@gmail.com";
  const DEFAULT_PASS = "Pass@123";
  const SIXTY_DAYS_MS = 60 * 24 * 60 * 60 * 1000;

  // ==========================================================
  // 60-DAYS SECURE ACTIVATION ENGINE
  // ==========================================================
  function getActivationExpiryTime() {
    let expTime = localStorage.getItem('secure_60day_activation_expiry');
    if (!expTime) {
      expTime = (Date.now() + SIXTY_DAYS_MS).toString();
      localStorage.setItem('secure_60day_activation_expiry', expTime);
    }
    return parseInt(expTime, 10);
  }

  function checkAndHandleExpiry() {
    const expTime = getActivationExpiryTime();
    const remainingMs = expTime - Date.now();
    const daysRemaining = Math.ceil(remainingMs / (24 * 60 * 60 * 1000));

    if (daysRemaining <= 0) {
      return 0;
    }
    return daysRemaining;
  }

  function updateValidityDisplay() {
    const badge = document.getElementById('validityCounterBadge');
    const remainingDays = checkAndHandleExpiry();

    if (remainingDays > 0) {
      badge.innerHTML = `⏳ 60-Days Portal Validity: <strong style="color:#fbbf24;">${remainingDays} Days Left</strong>`;
      badge.style.borderColor = '#10b981';
      badge.style.color = '#34d399';
      badge.style.background = 'rgba(16, 185, 129, 0.15)';
    } else {
      badge.innerHTML = `⏳ Portal Validity: <strong style="color:#ef4444;">Expired (60 Days Completed)</strong>`;
      badge.style.borderColor = '#ef4444';
      badge.style.color = '#f87171';
      badge.style.background = 'rgba(239, 68, 68, 0.15)';
    }
  }

  // ==========================================================
  // FIXED ROBUST FILE UPLOAD & MANUAL CROP BRIDGE
  // ==========================================================
  async function handleCardUpload(file, targetCanvas, ctx, isFront) {
    if (!file) return;

    if (file.type === 'application/pdf') {
      const arrayBuffer = await file.arrayBuffer();
      try {
        const pdf = await pdfjsLib.getDocument({ data: new Uint8Array(arrayBuffer) }).promise;
        let pageNum = 1;
        if (!isFront && pdf.numPages > 1) pageNum = 2;
        const page = await pdf.getPage(pageNum);
        renderAndOpenCropper(page, targetCanvas, ctx, isFront, file.name);
      } catch(err) {
        if (err.name === 'PasswordException') {
          let pwd = prompt("यह PDF पासवर्ड प्रोटेक्टेड है। कृपया पासवर्ड दर्ज करें:");
          if (pwd) {
            try {
              const pdf = await pdfjsLib.getDocument({ data: new Uint8Array(arrayBuffer), password: pwd }).promise;
              const page = await pdf.getPage(1);
              renderAndOpenCropper(page, targetCanvas, ctx, isFront, file.name);
              return;
            } catch(e) {
              alert("❌ गलत पासवर्ड!");
            }
          }
        }
      }
    } else {
      const reader = new FileReader();
      reader.onload = function(e) {
        if (isFront) frontCardRawData = e.target.result;
        else backCardRawData = e.target.result;
        
        document.getElementById(isFront ? 'file1Name' : 'file2Name').innerText = `✅ Loaded: ${file.name}`;
        openCropEngine(e.target.result, isFront ? 'card_front' : 'card_back');
      };
      reader.readAsDataURL(file);
    }
  }

  async function renderAndOpenCropper(page, targetCanvas, ctx, isFront, fileName) {
    const viewport = page.getViewport({ scale: 2.5 });
    const tempCanvas = document.createElement('canvas');
    const tempCtx = tempCanvas.getContext('2d');
    tempCanvas.width = viewport.width;
    tempCanvas.height = viewport.height;

    await page.render({ canvasContext: tempCtx, viewport: viewport }).promise;
    const dataUrl = tempCanvas.toDataURL('image/jpeg', 0.98);

    if (isFront) frontCardRawData = dataUrl;
    else backCardRawData = dataUrl;

    document.getElementById(isFront ? 'file1Name' : 'file2Name').innerText = `✅ Loaded: ${fileName}`;
    openCropEngine(dataUrl, isFront ? 'card_front' : 'card_back');
  }

  // ==========================================================
  // INDEXEDDB 60-DAY HISTORY STORAGE & INDIVIDUAL DELETE ENGINE
  // ==========================================================
  const DB_NAME = 'PrintPortal60DayDB';
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
      
      const record = {
        feature: featureName,
        fileName: fileName,
        data: blobOrDataUrl,
        fileType: fileType,
        timestamp: Date.now(),
        dateFormatted: new Date().toLocaleString('en-IN', { timeZone: 'Asia/Kolkata' })
      };

      store.add(record);
      tx.oncomplete = () => {
        cleanupOldHistoryRecords();
      };
    } catch(err) {
      console.error("Storage error:", err);
    }
  }

  async function cleanupOldHistoryRecords() {
    try {
      const db = await openHistoryDB();
      const tx = db.transaction(DB_STORE, 'readwrite');
      const store = tx.objectStore(DB_STORE);
      const now = Date.now();
      const retentionMs = SIXTY_DAYS_MS;

      const request = store.openCursor();
      request.onsuccess = function(e) {
        const cursor = e.target.result;
        if (cursor) {
          if (now - cursor.value.timestamp > retentionMs) {
            cursor.delete();
          }
          cursor.continue();
        }
      };
    } catch(err) {}
  }

  async function renderHistoryTable() {
    try {
      await cleanupOldHistoryRecords();
      const db = await openHistoryDB();
      const tx = db.transaction(DB_STORE, 'readonly');
      const store = tx.objectStore(DB_STORE);
      const request = store.getAll();

      request.onsuccess = function() {
        const records = request.result || [];
        const tbody = document.getElementById('historyTableBody');
        tbody.innerHTML = '';

        if (!records.length) {
          tbody.innerHTML = `<tr><td colspan="4" style="text-align:center; color:var(--text-muted); padding:20px;">कोई प्रिंट रिकॉर्ड नहीं मिला।</td></tr>`;
          return;
        }

        records.reverse().forEach(rec => {
          const tr = document.createElement('tr');
          tr.innerHTML = `
            <td><strong style="color:var(--accent-blue);">${rec.feature}</strong></td>
            <td>${rec.fileName}</td>
            <td style="color:#9ca3af; font-size:11px;">${rec.dateFormatted}</td>
            <td>
              <button class="history-download-btn" onclick="reDownloadHistoryFile(${rec.id})">📥 Download</button>
              <button class="history-delete-btn" onclick="deleteHistoryItem(${rec.id})">🗑️ Delete</button>
            </td>
          `;
          tbody.appendChild(tr);
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
      if (typeof rec.data === 'string') {
        link.href = rec.data;
      } else {
        link.href = URL.createObjectURL(rec.data);
      }
      link.download = rec.fileName;
      link.click();
    };
  }

  async function deleteHistoryItem(recordId) {
    if (!confirm('क्या आप इस फाइल को हिस्ट्री से हटाना चाहते हैं?')) return;
    try {
      const db = await openHistoryDB();
      const tx = db.transaction(DB_STORE, 'readwrite');
      const store = tx.objectStore(DB_STORE);
      store.delete(recordId);
      tx.oncomplete = () => renderHistoryTable();
    } catch(err) {
      console.error("Delete error:", err);
    }
  }

  async function clearAllHistoryDB() {
    if (!confirm('क्या आप सभी इतिहास रिकॉर्ड्स तुरंत मिटाना चाहते हैं?')) return;
    const db = await openHistoryDB();
    const tx = db.transaction(DB_STORE, 'readwrite');
    tx.objectStore(DB_STORE).clear();
    tx.oncomplete = () => renderHistoryTable();
  }

  function switchTab(tabId) {
    document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
    document.querySelectorAll('.tab-content').forEach(content => content.classList.remove('active'));
    
    event.target.classList.add('active');
    document.getElementById(tabId).classList.add('active');

    if (tabId === 'tab-history') {
      renderHistoryTable();
    }
  }

  const loginScreen = document.getElementById('loginScreen');
  const changePwdScreen = document.getElementById('changePwdScreen');
  const mainApp = document.getElementById('mainApp');
  
  const loginEmail = document.getElementById('loginEmail');
  const loginPass = document.getElementById('loginPass');
  const authBtn = document.getElementById('authBtn');
  const errorMsg = document.getElementById('errorMsg');
  const logoutBtn = document.getElementById('logoutBtn');

  const goToChangePwd = document.getElementById('goToChangePwd');
  const backToLogin = document.getElementById('backToLogin');
  const oldPassInput = document.getElementById('oldPassInput');
  const newPassInput = document.getElementById('newPassInput');
  const confirmPassInput = document.getElementById('confirmPassInput');
  const saveNewPwdBtn = document.getElementById('saveNewPwdBtn');
  const pwdStatusMsg = document.getElementById('pwdStatusMsg');

  sessionStorage.removeItem('isLoggedIn');

  const today = new Date();
  const curDay = String(today.getDate()).padStart(2, '0');
  const curMonth = String(today.getMonth() + 1).padStart(2, '0');
  const curYear = today.getFullYear();
  document.getElementById('candDopInput').value = `DOP: ${curDay}/${curMonth}/${curYear}`;

  goToChangePwd.addEventListener('click', () => {
    loginScreen.style.display = 'none';
    changePwdScreen.style.display = 'block';
    oldPassInput.value = '';
    newPassInput.value = '';
    confirmPassInput.value = '';
    pwdStatusMsg.style.display = 'none';
  });

  backToLogin.addEventListener('click', () => {
    changePwdScreen.style.display = 'none';
    loginScreen.style.display = 'block';
    errorMsg.style.display = 'none';
  });

  saveNewPwdBtn.addEventListener('click', () => {
    const oldP = oldPassInput.value.trim();
    const newP = newPassInput.value.trim();
    const confP = confirmPassInput.value.trim();
    const activePass = localStorage.getItem('system_auth_pwd') || DEFAULT_PASS;

    if (oldP !== activePass) {
      pwdStatusMsg.innerText = "❌ पुराना पासवर्ड गलत है!";
      pwdStatusMsg.style.color = "#ef4444";
      pwdStatusMsg.style.display = "block";
      return;
    }

    if (newP.length < 4) {
      pwdStatusMsg.innerText = "❌ नया पासवर्ड कम से कम 4 अक्षरों का होना चाहिए!";
      pwdStatusMsg.style.color = "#ef4444";
      pwdStatusMsg.style.display = "block";
      return;
    }

    if (newP !== confP) {
      pwdStatusMsg.innerText = "❌ नया पासवर्ड और कन्फर्म पासवर्ड मैच नहीं हो रहे!";
      pwdStatusMsg.style.color = "#ef4444";
      pwdStatusMsg.style.display = "block";
      return;
    }

    localStorage.setItem('system_auth_pwd', newP);
    pwdStatusMsg.innerText = "✅ पासवर्ड बदल गया! अब नए पासवर्ड से लॉगिन करें।";
    pwdStatusMsg.style.color = "#34d399";
    pwdStatusMsg.style.display = "block";

    setTimeout(() => {
      changePwdScreen.style.display = 'none';
      loginScreen.style.display = 'block';
      loginPass.value = '';
    }, 1200);
  });

  function handleLogin() {
    const inputEmail = loginEmail.value.trim().toLowerCase();
    const inputPass = loginPass.value.trim();
    const activePass = localStorage.getItem('system_auth_pwd') || DEFAULT_PASS;

    if (inputEmail === AUTH_EMAIL.toLowerCase() && inputPass === activePass) {
      const remainingDays = checkAndHandleExpiry();

      if (remainingDays > 0) {
        sessionStorage.setItem('isLoggedIn', 'true');
        loginScreen.style.display = 'none';
        changePwdScreen.style.display = 'none';
        errorMsg.style.display = 'none';
        mainApp.style.display = 'block';
        updateValidityDisplay();
        initAllCanvases();
        cleanupOldHistoryRecords();
      } else {
        errorMsg.innerText = "⚠️ 60 दिनों की वैधता समाप्त हो चुकी है!";
        errorMsg.style.display = 'block';
      }
    } else {
      errorMsg.innerText = "⚠️ गलत ईमेल आईडी या पासवर्ड!";
      errorMsg.style.display = 'block';
    }
  }

  authBtn.addEventListener('click', handleLogin);
  loginPass.addEventListener('keypress', (e) => { if (e.key === 'Enter') handleLogin(); });

  logoutBtn.addEventListener('click', () => {
    sessionStorage.removeItem('isLoggedIn');
    mainApp.style.display = 'none';
    changePwdScreen.style.display = 'none';
    loginScreen.style.display = 'block';
    loginPass.value = '';
  });
</script>

</body>
</html>
