<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>ID CARD PRINT & CONVERTER PORTAL</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
  
  <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/2.16.105/pdf.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf-lib/1.17.1/pdf-lib.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js"></script>
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
    body { background: var(--bg-gradient); min-height: 100vh; padding: 15px 10px; display: flex; flex-direction: column; align-items: center; justify-content: center; color: var(--text-main); }
    .portal-main-heading { font-size: 24px; font-weight: 800; letter-spacing: 1.5px; text-transform: uppercase; background: linear-gradient(135deg, #38bdf8 0%, #a855f7 50%, #f43f5e 100%); -webkit-background-clip: text; -webkit-text-fill-color: transparent; margin-bottom: 10px; text-align: center; }
    .ticker-container { width: 100%; max-width: 580px; overflow: hidden; background: rgba(56, 189, 248, 0.1); border: 1px solid rgba(56, 189, 248, 0.3); border-radius: 8px; padding: 8px 0; margin-bottom: 12px; white-space: nowrap; }
    .ticker-text { display: inline-block; padding-left: 100%; animation: tickerAnimation 18s linear infinite; color: #38bdf8; font-weight: 600; font-size: 13px; }
    @keyframes tickerAnimation { 0% { transform: translate3d(0, 0, 0); } 100% { transform: translate3d(-100%, 0, 0); } }
    .ad-slider-box { display: flex; gap: 8px; justify-content: center; margin-bottom: 12px; max-width: 580px; width: 100%; }
    .ad-slide-img { width: calc(33.333% - 6px); height: 95px; object-fit: cover; border-radius: 8px; border: 1px solid var(--border-color); box-shadow: 0 4px 10px rgba(0,0,0,0.4); background: #1e293b; }
    .services-info-card { background: rgba(15, 23, 42, 0.75); border: 1px solid var(--border-color); border-radius: 12px; padding: 10px 14px; max-width: 580px; width: 100%; margin-bottom: 15px; text-align: left; }
    .services-info-card h4 { font-size: 12px; color: var(--accent-blue); margin-bottom: 4px; font-weight: 700; }
    .services-info-card ul { font-size: 11px; color: var(--text-muted); padding-left: 14px; display: grid; grid-template-columns: 1fr 1fr; gap: 3px; }
    .top-reg-nav { display: flex; gap: 12px; margin-bottom: 15px; flex-wrap: wrap; justify-content: center; }
    .top-reg-btn { background: linear-gradient(135deg, #10b981 0%, #059669 100%); border: none; color: #fff; padding: 10px 22px; font-size: 13px; font-weight: 600; border-radius: 20px; cursor: pointer; display: inline-flex; align-items: center; gap: 6px; box-shadow: 0 4px 15px rgba(16, 185, 129, 0.4); }
    .auth-box { background: var(--card-bg); backdrop-filter: blur(20px); border: 1px solid var(--border-color); padding: 20px 25px; border-radius: 20px; box-shadow: 0 25px 60px rgba(0, 0, 0, 0.6); width: 100%; max-width: 580px; text-align: center; }
    .badge { display: inline-block; padding: 3px 12px; font-size: 11px; font-weight: 600; text-transform: uppercase; background: rgba(56, 189, 248, 0.15); color: var(--accent-blue); border: 1px solid rgba(56, 189, 248, 0.3); border-radius: 20px; margin-bottom: 8px; }
    .slot-counter-badge { background: rgba(245, 158, 11, 0.15); color: #fbbf24; border: 1px solid rgba(245, 158, 11, 0.3); padding: 4px 16px; font-size: 12px; font-weight: 600; border-radius: 20px; display: inline-block; margin-bottom: 15px; }
    .login-input { width: 100%; padding: 11px 15px; margin-bottom: 12px; background: rgba(15, 23, 42, 0.9); border: 1px solid rgba(56, 189, 248, 0.3); border-radius: 10px; color: #fff; font-size: 13px; outline: none; }
    .login-btn { width: 100%; padding: 12px; background: linear-gradient(135deg, #0284c7 0%, #2563eb 100%); color: #fff; font-weight: 600; border: none; border-radius: 10px; cursor: pointer; font-size: 14px; }
    .auth-link { display: inline-block; margin-top: 10px; font-size: 12px; color: var(--accent-blue); cursor: pointer; text-decoration: underline; }
    .error-msg { color: #ef4444; font-size: 12px; margin-top: 10px; display: none; }
    .tab-nav { display: flex; justify-content: center; gap: 8px; margin-bottom: 15px; flex-wrap: wrap; }
    .tab-btn { padding: 9px 13px; background: rgba(15, 23, 42, 0.8); border: 1px solid var(--border-color); color: var(--text-muted); border-radius: 12px; cursor: pointer; font-weight: 600; font-size: 12px; }
    .tab-btn.active { background: linear-gradient(135deg, #0284c7 0%, #2563eb 100%); color: #fff; border-color: transparent; }
    #mainApp { display: none; width: 100%; max-width: 1220px; }
    .container { background: var(--card-bg); backdrop-filter: blur(16px); border: 1px solid var(--border-color); padding: 25px 20px; border-radius: 20px; box-shadow: 0 20px 50px rgba(0, 0, 0, 0.4); width: 100%; text-align: center; position: relative; }
    .logout-btn { background: rgba(239, 68, 68, 0.2); border: 1px solid rgba(239, 68, 68, 0.4); color: #fca5a5; padding: 6px 14px; font-size: 12px; border-radius: 8px; cursor: pointer; }
    h1 { background: linear-gradient(to right, #38bdf8, #a855f7, #ec4899); -webkit-background-clip: text; -webkit-text-fill-color: transparent; font-size: 22px; font-weight: 700; margin-bottom: 6px; }
    .tab-content { display: none; }
    .tab-content.active { display: block; }
    .upload-section { display: flex; gap: 15px; justify-content: center; margin: 15px 0; flex-wrap: wrap; }
    .upload-box { border: 2px dashed rgba(56, 189, 248, 0.4); padding: 16px 14px; border-radius: 14px; cursor: pointer; background: rgba(15, 23, 42, 0.6); flex: 1; min-width: 220px; }
    input[type="file"] { display: none; }
    .preview-container { display: flex; justify-content: center; gap: 20px; margin: 15px 0; flex-wrap: wrap; }
    .preview-box { border: 1px solid var(--border-color); padding: 10px; background: rgba(15, 23, 42, 0.8); border-radius: 12px; }
    canvas { max-width: 100% !important; height: auto !important; display: block; margin: 0 auto; border-radius: 4px; background: #fff; object-fit: contain; }
    .btn-group { display: flex; gap: 10px; justify-content: center; margin-top: 15px; flex-wrap: wrap; }
    .action-btn { padding: 10px 22px; font-size: 13px; font-weight: 600; border: none; border-radius: 10px; cursor: pointer; color: #fff; }
    .btn-add { background: var(--btn-add); }
    .btn-download { background: var(--btn-download); }
    .btn-reset { background: rgba(239, 68, 68, 0.2); border: 1px solid rgba(239, 68, 68, 0.4); color: #fca5a5; }
    .btn-manual-crop { background: rgba(56, 189, 248, 0.15); border: 1px solid var(--accent-blue); color: var(--accent-blue); padding: 4px 10px; font-size: 11px; border-radius: 6px; margin-top: 8px; cursor: pointer; font-weight: 600; }
    .control-panel { background: rgba(15, 23, 42, 0.7); border: 1px solid var(--border-color); border-radius: 14px; padding: 14px 18px; max-width: 600px; margin: 15px auto; text-align: center; }
    .qty-select-group { display: flex; align-items: center; justify-content: center; gap: 8px; margin-top: 8px; flex-wrap: wrap; }
    .qty-input { width: 80px; padding: 6px 10px; border-radius: 8px; background: rgba(15, 23, 42, 0.9); border: 1px solid var(--accent-blue); color: #fff; font-size: 14px; font-weight: 700; text-align: center; }
    .text-field-input { width: 100%; max-width: 260px; padding: 8px 12px; border-radius: 8px; background: rgba(15, 23, 42, 0.9); border: 1px solid var(--accent-blue); color: #fff; font-size: 13px; outline: none; margin-bottom: 4px; }
    .quick-qty-btn { padding: 5px 12px; background: #334155; border: 1px solid rgba(255, 255, 255, 0.1); color: #fff; border-radius: 6px; font-size: 11px; cursor: pointer; font-weight: 600; }
    .slider-range { -webkit-appearance: none; width: 100%; height: 6px; border-radius: 5px; background: #334155; outline: none; margin: 6px 0 8px 0; }
    .slider-range::-webkit-slider-thumb { -webkit-appearance: none; width: 16px; height: 16px; border-radius: 50%; background: var(--accent-blue); cursor: pointer; }
    .file-gallery-list { display: flex; flex-wrap: wrap; gap: 14px; justify-content: center; margin: 15px 0; max-height: 420px; overflow-y: auto; padding: 14px; background: rgba(15, 23, 42, 0.6); border-radius: 12px; border: 1px solid var(--border-color); }
    .draggable-card { position: relative; width: 125px; background: #0f172a; border: 2px solid rgba(56, 189, 248, 0.35); border-radius: 10px; padding: 6px 4px 8px 4px; display: flex; flex-direction: column; align-items: center; cursor: grab; }
    .draggable-card canvas, .draggable-card img { width: 100%; height: 135px; object-fit: contain; background: #ffffff; border-radius: 5px; pointer-events: none; }
    .file-label { font-size: 11px; color: #94a3b8; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; width: 100%; margin: 6px 0 2px 0; font-weight: 600; text-align: center; }
    .history-table-container { margin-top: 15px; overflow-x: auto; background: rgba(15, 23, 42, 0.7); border-radius: 12px; border: 1px solid var(--border-color); }
    .history-table { width: 100%; border-collapse: collapse; font-size: 12px; text-align: left; }
    .history-table th, .history-table td { padding: 10px 14px; border-bottom: 1px solid rgba(255, 255, 255, 0.08); }
    .history-table th { background: rgba(30, 41, 59, 0.9); color: var(--accent-blue); font-weight: 600; }
    .history-download-btn { background: #0284c7; color: #fff; border: none; padding: 5px 12px; border-radius: 6px; cursor: pointer; font-size: 11px; }
    .history-delete-btn { background: rgba(239, 68, 68, 0.2); color: #fca5a5; border: 1px solid rgba(239, 68, 68, 0.4); padding: 5px 12px; border-radius: 6px; cursor: pointer; font-size: 11px; }
    .history-view-ss-btn { background: rgba(56, 189, 248, 0.25); color: #38bdf8; border: 1px solid rgba(56, 189, 248, 0.5); padding: 5px 10px; border-radius: 6px; cursor: pointer; font-size: 11px; }
    #cropModal, #adminMsgModal, #viewScreenshotModal { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0, 0, 0, 0.85); z-index: 10000; align-items: center; justify-content: center; flex-direction: column; padding: 20px; }
    .crop-wrapper { max-width: 90vw; max-height: 70vh; background: #000; border-radius: 8px; overflow: hidden; margin-bottom: 15px; }
    .crop-wrapper img { max-width: 100%; max-height: 70vh; display: block; }
    #regModalPopup { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0, 0, 0, 0.85); z-index: 1000000; align-items: center; justify-content: center; padding: 20px; overflow-y: auto; }
    .reg-popup-content { background: #1e293b; border: 1px solid rgba(56, 189, 248, 0.4); border-radius: 16px; padding: 25px; width: 100%; max-width: 480px; text-align: center; box-shadow: 0 25px 60px rgba(0,0,0,0.8); max-height: 90vh; overflow-y: auto; }
  </style>
</head>
<body>

<div class="portal-main-heading">ID CARD PRINT & CONVERTER PORTAL</div>

<div class="top-reg-nav" id="topNavRegistrationBox">
  <button class="top-reg-btn" onclick="openRegModal()">🚀 Distributor Sign Up / Register</button>
</div>

<!-- Login Screen -->
<div id="loginScreen" class="auth-box">
  <div class="ticker-container">
    <div class="ticker-text">🚀 Smart & Reliable Print Portal — Fast Operations, Simple Workflow & Daily Business Use!</div>
  </div>
  <div class="ad-slider-box">
    <img src="https://images.unsplash.com/photo-1544717305-2782549b5136?w=400&auto=format&fit=crop&q=60" class="ad-slide-img">
    <img src="https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?w=400&auto=format&fit=crop&q=60" class="ad-slide-img">
    <img src="https://images.unsplash.com/photo-1633158829585-23ba8f7c8caf?w=400&auto=format&fit=crop&q=60" class="ad-slide-img">
  </div>
  <div class="services-info-card">
    <h4>⚡ Our Printing Services:</h4>
    <ul>
      <li>🔹 5-Cards ID Print (A4)</li>
      <li>🔹 Multi-Unique Passports</li>
      <li>🔹 4×6 Photo Sheets</li>
      <li>🔹 PDF Arranger & Merger</li>
      <li>🔹 Custom Image Resizer</li>
      <li>🔹 Resume Builder</li>
    </ul>
  </div>
  <div class="badge">Protected Access</div>
  <h2 style="font-size: 20px; margin-bottom: 6px;">Sign In</h2>
  <input type="email" id="loginEmail" class="login-input" placeholder="ईमेल आईडी दर्ज करें" value="oneplus777000@gmail.com">
  <input type="password" id="loginPass" class="login-input" placeholder="पासवर्ड दर्ज करें">
  <button id="authBtn" class="login-btn">लॉगिन करें</button>
  <div id="errorMsg" class="error-msg">⚠️ गलत ईमेल आईडी या पासवर्ड!</div>
  <div><span id="goToChangePwd" class="auth-link">🔑 Change Password?</span></div>
</div>

<!-- Change Password Screen -->
<div id="changePwdScreen" class="auth-box" style="display:none;">
  <div class="badge">Security Settings</div>
  <h2 style="font-size: 20px; margin-bottom: 6px; color: var(--accent-blue);">🔑 Change Password</h2>
  <input type="email" id="pwdEmailInput" class="login-input" placeholder="अपनी ईमेल आईडी">
  <input type="password" id="oldPassInput" class="login-input" placeholder="पुराना पासवर्ड">
  <input type="password" id="newPassInput" class="login-input" placeholder="नया पासवर्ड">
  <input type="password" id="confirmPassInput" class="login-input" placeholder="नया पासवर्ड कन्फर्म करें">
  <button id="saveNewPwdBtn" class="login-btn" style="background: var(--btn-download);">💾 नया पासवर्ड सेव करें</button>
  <div id="pwdStatusMsg" style="font-size:13px; margin-top:12px; display:none;"></div>
  <div><span id="backToLogin" class="auth-link">⬅️ Back to Login</span></div>
</div>

<!-- Main Application -->
<div id="mainApp">
  <div class="tab-nav">
    <button class="tab-btn active" onclick="switchTab('tab-cards')">💳 ID Card (5 Slots)</button>
    <button class="tab-btn" onclick="switchTab('tab-passport')">👤 Passport Photos</button>
    <button class="tab-btn" onclick="switchTab('tab-name-passport')">📝 Name & Date</button>
    <button class="tab-btn" onclick="switchTab('tab-4x6')">🖼️ 4×6 Print</button>
    <button class="tab-btn" onclick="switchTab('tab-arranger')">📑 PDF Arranger</button>
    <button class="tab-btn" onclick="switchTab('tab-jpg-to-pdf')">📄 Merge PDF</button>
    <button class="tab-btn" onclick="switchTab('tab-resizer')">📐 Resizer</button>
    <button class="tab-btn" onclick="switchTab('tab-pdf-to-jpg')">🖼️ PDF to JPG</button>
    <button class="tab-btn" onclick="switchTab('tab-pdf-compressor')">🗜️ Compressor</button>
    <button class="tab-btn" onclick="switchTab('tab-resume')">📝 Resume Builder</button>
    <button class="tab-btn" onclick="switchTab('tab-history')">📂 History</button>
    <button id="adminTabBtn" class="tab-btn" onclick="switchTab('tab-admin')" style="display:none; color:#fbbf24;">⚙️ Admin Panel</button>
  </div>

  <div class="container">
    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px; flex-wrap: wrap; gap: 10px;">
      <div id="validityCounterBadge" style="background: rgba(16, 185, 129, 0.15); border: 1px solid #10b981; color: #34d399; padding: 6px 14px; border-radius: 20px; font-size: 12px; font-weight: 600;">⏳ Initializing...</div>
      <button id="logoutBtn" class="logout-btn">🔒 Logout</button>
    </div>

    <div id="distributorNoticeBanner" style="display:none; background: rgba(245, 158, 11, 0.2); border: 1px solid #fbbf24; color: #fef08a; padding: 14px 18px; border-radius: 12px; margin-bottom: 15px; font-size: 13px; text-align: left;">
      <div style="display: flex; justify-content: space-between; align-items: flex-start; gap: 15px; flex-wrap: wrap;">
        <div style="flex: 1;">
          <strong>📢 Admin Notice:</strong>
          <div id="distributorNoticeText" style="margin-top: 4px;"></div>
          <div id="distributorNoticeImgBox" style="margin-top: 10px; display:none;"><img id="distributorNoticeImg" src="" style="max-width: 100%; max-height: 220px; border-radius: 8px;"></div>
        </div>
        <div style="background: rgba(15,23,42,0.85); border: 1px solid rgba(56,189,248,0.4); padding: 12px; border-radius: 10px; text-align: center;">
          <div style="font-size: 11px; color: var(--accent-blue); margin-bottom: 6px; font-weight: 600;">💳 Send Payment Screenshot</div>
          <input type="file" id="distScreenshotInput" accept="image/*" style="display:block; width:100%; background:#334155; color:#fff; padding:6px; font-size:11px; margin-bottom:8px;">
          <button onclick="uploadDistributorScreenshot()" class="action-btn btn-download" style="padding: 6px 12px; font-size: 11px; width: 100%;">📤 Send</button>
          <div id="screenshotUploadStatus" style="font-size:10px; margin-top:4px; display:none;"></div>
        </div>
      </div>
    </div>

    <!-- TAB 1: CARDS -->
    <div id="tab-cards" class="tab-content active">
      <div class="badge">Auto-Dimension Crop • 5 Cards</div>
      <h1>Card Generator System</h1>
      <div id="slotCounter" class="slot-counter-badge">Cards on Page: 0 / 5 (Next Slot: #1)</div>
      <div class="upload-section">
        <label class="upload-box" for="card1Input"><strong>📁 Front Side</strong><div id="file1Name" style="font-size: 12px; color: var(--text-muted);">इमेज चुनें</div></label>
        <input type="file" id="card1Input" accept="image/*">
        <label class="upload-box" for="card2Input"><strong>📁 Back Side</strong><div id="file2Name" style="font-size: 12px; color: var(--text-muted);">इमेज चुनें</div></label>
        <input type="file" id="card2Input" accept="image/*">
      </div>
      <div class="preview-container">
        <div class="preview-box"><h4>Front Preview</h4><canvas id="canvas1" width="1013" height="638" style="width: 180px;"></canvas><button id="manualCropFrontBtn" class="btn-manual-crop" style="display:none;" onclick="openManualCropForCard('front')">✂️ Crop</button></div>
        <div class="preview-box"><h4>Back Preview</h4><canvas id="canvas2" width="1013" height="638" style="width: 180px;"></canvas><button id="manualCropBackBtn" class="btn-manual-crop" style="display:none;" onclick="openManualCropForCard('back')">✂️ Crop</button></div>
      </div>
      <div class="btn-group">
        <button id="addCardBtn" class="action-btn btn-add" disabled>➕ Add Card</button>
        <button id="resetPageBtn" class="action-btn btn-reset">🔄 Clear A4</button>
      </div>
      <div style="margin-top: 25px; border-top: 1px solid var(--border-color); padding-top: 15px;">
        <div style="display:inline-block; max-width: 250px; background:#fff; border-radius:6px;"><canvas id="a4Canvas" width="2480" height="3508" style="width: 100%; display:block;"></canvas></div>
        <div class="btn-group"><button id="downloadPdfBtn" class="action-btn btn-download" disabled>📥 Download A4 PDF</button></div>
      </div>
    </div>

    <!-- TAB 2: PASSPORT -->
    <div id="tab-passport" class="tab-content">
      <div class="badge">Multi-Unique Photo Generator</div>
      <h1>Passport Photo Generator</h1>
      <div class="control-panel">
        <span style="font-size: 13px; font-weight:600; color: var(--accent-blue);">📂 Select Mode (1 to 5 Photos):</span>
        <div class="qty-select-group" style="margin-top: 8px;">
          <button class="quick-qty-btn" id="btnCount1" onclick="setPassportCount(1)" style="background:#0284c7;">1 Photo</button>
          <button class="quick-qty-btn" id="btnCount2" onclick="setPassportCount(2)">2 Photos</button>
          <button class="quick-qty-btn" id="btnCount3" onclick="setPassportCount(3)">3 Photos</button>
          <button class="quick-qty-btn" id="btnCount4" onclick="setPassportCount(4)">4 Photos</button>
          <button class="quick-qty-btn" id="btnCount5" onclick="setPassportCount(5)">5 Photos</button>
        </div>
      </div>
      <div id="passportUploadBlocksContainer" style="display: flex; gap: 8px; justify-content: center; flex-wrap: wrap; margin-bottom: 12px;"></div>
      <div class="control-panel">
        <span style="font-size: 13px; font-weight:600; color: var(--accent-blue);">🔢 Total Quantity:</span>
        <div class="qty-select-group">
          <input type="number" id="passportQtyInput" class="qty-input" value="8" min="1" max="50">
          <button class="quick-qty-btn" onclick="setPassportQty(4)">4</button>
          <button class="quick-qty-btn" onclick="setPassportQty(8)">8</button>
          <button class="quick-qty-btn" onclick="setPassportQty(12)">12</button>
          <button class="quick-qty-btn" onclick="setPassportQty(30)">30</button>
        </div>
      </div>
      <div class="btn-group"><button id="generateMultiPassportA4Btn" class="action-btn btn-add">🖼️ Generate Sheet</button></div>
      <div style="margin-top: 25px;"><canvas id="passportSheetCanvas" width="2480" height="3508" style="width: 200px; display:block; margin:0 auto; background:#fff;"></canvas>
      <div class="btn-group"><button id="downloadMultiPassportPdfBtn" class="action-btn btn-download" disabled>📥 Download PDF</button></div></div>
    </div>

    <!-- TAB 3: NAME & DATE -->
    <div id="tab-name-passport" class="tab-content">
      <h1>Name & Date Passport</h1>
      <input type="file" id="namePassportInput" accept="image/*">
      <label for="namePassportInput" class="action-btn btn-add" style="display:inline-block; cursor:pointer; margin-bottom:15px;">📁 Select Photo</label>
      <div class="control-panel" style="text-align:left;">
        <input type="text" id="candNameInput" class="text-field-input" placeholder="Candidate Name" oninput="renderNamePassportPreview()">
        <input type="text" id="candDobInput" class="text-field-input" placeholder="DOB" oninput="renderNamePassportPreview()">
        <input type="text" id="candDopInput" class="text-field-input" placeholder="DOP" oninput="renderNamePassportPreview()">
      </div>
      <div class="preview-container"><canvas id="namePassportCanvas" width="413" height="531" style="width: 155px;"></canvas></div>
      <div class="btn-group"><button id="makeA4NamePassportBtn" class="action-btn btn-add" disabled>📄 Generate A4 Sheet</button></div>
      <div style="margin-top:15px;"><canvas id="namePassportSheetCanvas" width="2480" height="3508" style="width:200px; background:#fff; margin:0 auto; display:block;"></canvas>
      <button id="downloadNamePassportPdfBtn" class="action-btn btn-download" style="margin-top:10px;" disabled>📥 Download PDF</button></div>
    </div>

    <!-- TAB 4: 4x6 -->
    <div id="tab-4x6" class="tab-content">
      <h1>4×6 Photo Print</h1>
      <input type="file" id="photo4x6Input" accept="image/*">
      <label for="photo4x6Input" class="action-btn btn-add" style="display:inline-block; cursor:pointer;">📁 Select 4x6 Photo</label>
      <div class="preview-container"><canvas id="canvas4x6" width="1200" height="1800" style="width: 150px;"></canvas></div>
      <button id="downloadDirect4x6Pdf" class="action-btn btn-download" disabled>📥 Download Direct PDF</button>
    </div>

    <!-- TAB 5: ARRANGER -->
    <div id="tab-arranger" class="tab-content">
      <h1>PDF Page Arranger</h1>
      <input type="file" id="arrangerPdfInput" accept="application/pdf" multiple>
      <label for="arrangerPdfInput" class="action-btn btn-add" style="display:inline-block; cursor:pointer;">📑 Upload PDFs</label>
      <div id="arrangerContainerArea" style="display:none; margin-top:15px;">
        <div id="arrangerGridList" class="file-gallery-list"></div>
        <button id="saveArrangedPdfBtn" class="action-btn btn-download">💾 Save Arranged PDF</button>
      </div>
    </div>

    <!-- TAB 6: MERGE -->
    <div id="tab-jpg-to-pdf" class="tab-content">
      <h1>PDF, JPG, PNG to PDF</h1>
      <input type="file" id="universalMultiInput" accept="image/*,application/pdf" multiple>
      <label for="universalMultiInput" class="action-btn btn-add" style="display:inline-block; cursor:pointer;">📁 Select Files</label>
      <div id="universalGalleryContainer" style="display:none; margin-top:15px;">
        <div id="universalGalleryList" class="file-gallery-list"></div>
        <button id="convertUniversalToPdfBtn" class="action-btn btn-download">📥 Convert Combined PDF</button>
      </div>
    </div>

    <!-- TAB 7: RESIZER -->
    <div id="tab-resizer" class="tab-content">
      <h1>Image Resizer</h1>
      <input type="file" id="resizerImageInput" accept="image/*">
      <label for="resizerImageInput" class="action-btn btn-add" style="display:inline-block; cursor:pointer;">📁 Select Image</label>
      <div id="resizerControlsPanel" style="display:none; margin-top:15px;">
        <input type="number" id="resizerWidthInput" class="qty-input" value="300" oninput="updateResizerCanvas()">
        <input type="number" id="resizerHeightInput" class="qty-input" value="300" oninput="updateResizerCanvas()">
        <canvas id="resizerPreviewCanvas" style="max-width:200px; margin:10px auto; background:#fff; display:block;"></canvas>
        <button id="downloadResizedJpgBtn" class="action-btn btn-download">📥 Download JPG</button>
      </div>
    </div>

    <!-- TAB 8: PDF TO JPG -->
    <div id="tab-pdf-to-jpg" class="tab-content">
      <h1>PDF to JPG</h1>
      <input type="file" id="pdfToJpgInput" accept="application/pdf">
      <label for="pdfToJpgInput" class="action-btn btn-add" style="display:inline-block; cursor:pointer;">📄 Select PDF</label>
      <div id="pdfToJpgControls" style="display:none; margin-top:15px;">
        <button id="startPdfToJpgBtn" class="action-btn btn-download">🖼️ Convert to JPG</button>
      </div>
    </div>

    <!-- TAB 9: COMPRESSOR -->
    <div id="tab-pdf-compressor" class="tab-content">
      <h1>PDF Compressor</h1>
      <input type="file" id="pdfCompressInput" accept="application/pdf">
      <label for="pdfCompressInput" class="action-btn btn-add" style="display:inline-block; cursor:pointer;">🗜️ Select PDF</label>
      <div id="compressorControlsArea" style="display:none; margin-top:15px;">
        <input type="range" id="compressQualitySlider" class="slider-range" min="10" max="95" value="60" oninput="onCompressSliderChange(this.value)">
        <button id="startCompressDownloadBtn" class="action-btn btn-download">📥 Compress & Download</button>
      </div>
    </div>

    <!-- TAB 10: RESUME BUILDER -->
    <div id="tab-resume" class="tab-content">
      <div class="badge">Professional Templates • Add More</div>
      <h1>Professional Resume & CV Builder</h1>
      <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; text-align: left; margin-bottom: 20px;">
        <div style="background: rgba(15,23,42,0.7); padding: 18px; border-radius: 12px; border: 1px solid var(--border-color);">
          <h3 style="color: var(--accent-blue); font-size: 14px; margin-bottom: 12px;">👤 Personal Info</h3>
          <input type="text" id="resName" class="text-field-input" style="max-width:100%;" placeholder="Full Name" oninput="updateResumePreview()">
          <input type="text" id="resTitle" class="text-field-input" style="max-width:100%;" placeholder="Job Title" oninput="updateResumePreview()">
          <input type="email" id="resEmail" class="text-field-input" style="max-width:100%;" placeholder="Email" oninput="updateResumePreview()">
          <input type="text" id="resPhone" class="text-field-input" style="max-width:100%;" placeholder="Phone" oninput="updateResumePreview()">
          <input type="text" id="resAddress" class="text-field-input" style="max-width:100%;" placeholder="Address" oninput="updateResumePreview()">
          <input type="file" id="resPhotoInput" accept="image/*" style="display:block; width:100%; background:#334155; color:#fff; padding:6px; font-size:11px; margin-top:8px;" onchange="loadResumePhoto(event)">
          <h3 style="color: var(--accent-blue); font-size: 14px; margin: 15px 0 8px;">🎯 Objective</h3>
          <textarea id="resObj" class="login-input" style="height: 65px; resize:none;" placeholder="Objective" oninput="updateResumePreview()"></textarea>
          <input type="text" id="resSkills" class="text-field-input" style="max-width:100%;" placeholder="Skills" oninput="updateResumePreview()">
          <input type="text" id="resLangs" class="text-field-input" style="max-width:100%;" placeholder="Languages" oninput="updateResumePreview()">
        </div>
        <div style="background: rgba(15,23,42,0.7); padding: 18px; border-radius: 12px; border: 1px solid var(--border-color);">
          <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom: 8px;">
            <h3 style="color: var(--accent-blue); font-size: 14px;">🎓 Education</h3>
            <button onclick="addEducationRow()" class="action-btn btn-add" style="padding: 4px 10px; font-size: 10px;">➕ Add More</button>
          </div>
          <div id="educationContainer" style="display:flex; flex-direction:column; gap:8px; margin-bottom:15px;"></div>
          <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom: 8px;">
            <h3 style="color: var(--accent-blue); font-size: 14px;">💼 Experience</h3>
            <button onclick="addExperienceRow()" class="action-btn btn-add" style="padding: 4px 10px; font-size: 10px;">➕ Add More</button>
          </div>
          <div id="experienceContainer" style="display:flex; flex-direction:column; gap:8px; margin-bottom:15px;"></div>
          <select id="resumeTemplateSelect" class="login-input" onchange="updateResumePreview()">
            <option value="1">Template 1: Modern Royal Blue</option>
            <option value="2">Template 2: Executive Emerald Green</option>
            <option value="3">Template 3: Sleek Dark Header</option>
            <option value="4">Template 4: Elegant Crimson Red</option>
            <option value="5">Template 5: Minimalist Clean Teal</option>
          </select>
        </div>
      </div>
      <div style="background:#fff; color:#000; padding:30px; border-radius:12px; max-width:800px; margin:0 auto; text-align:left;" id="resumePreviewBox"></div>
      <div class="btn-group" style="margin-top: 20px;"><button onclick="downloadResumePdf()" class="action-btn btn-download">📥 Download PDF</button></div>
    </div>

    <!-- TAB 11: HISTORY -->
    <div id="tab-history" class="tab-content">
      <h1>Print & Download History</h1>
      <button onclick="clearAllHistoryDB()" class="action-btn btn-reset" style="padding: 6px 14px; font-size: 11px; margin-bottom:10px;">🗑️ Clear History</button>
      <div class="history-table-container">
        <table class="history-table">
          <thead><tr><th>Type</th><th>File Name</th><th>Time</th><th>Action</th></tr></thead>
          <tbody id="historyTableBody"><tr><td colspan="4" style="text-align:center; padding:20px;">कोई रिकॉर्ड नहीं।</td></tr></tbody>
        </table>
      </div>
    </div>

    <!-- TAB 12: ADMIN PANEL -->
    <div id="tab-admin" class="tab-content">
      <h1 style="color: #fbbf24;">Admin Panel & Approvals</h1>
      <h3 style="font-size: 14px; color: #fbbf24; margin-bottom: 10px; text-align: left; max-width: 900px; margin: 0 auto;">⏳ Pending Sign-Up Requests</h3>
      <div class="history-table-container" style="max-width: 900px; margin: 0 auto 30px auto;">
        <table class="history-table">
          <thead><tr><th>Name</th><th>Email</th><th>Mobile</th><th>Plan</th><th>Screenshot</th><th>Action</th></tr></thead>
          <tbody id="pendingRequestsTableBody"><tr><td colspan="6" style="text-align:center; padding:15px;">लोड हो रहा है...</td></tr></tbody>
        </table>
      </div>
      <h3 style="font-size: 14px; color: var(--accent-blue); margin-bottom: 10px; text-align: left; max-width: 900px; margin: 0 auto;">✅ Active Distributors</h3>
      <div class="history-table-container" style="max-width: 900px; margin: 0 auto;">
        <table class="history-table">
          <thead><tr><th>Name</th><th>Email</th><th>Password</th><th>Plan/Status</th><th>Action</th></tr></thead>
          <tbody id="distributorTableBody"><tr><td colspan="5" style="text-align:center; padding:15px;">लोड हो रहा है...</td></tr></tbody>
        </table>
      </div>
    </div>

    <footer style="margin-top: 25px; font-size: 12px; color: var(--text-muted);">Designed & Developed by <strong>JAYESH BHAVSAR @ 2026</strong></footer>
  </div>
</div>

<!-- SIGN-UP POPUP WITH FIXED QR (36 & 319) -->
<div id="regModalPopup">
  <div class="reg-popup-content">
    <h3 style="color: var(--accent-blue); margin-bottom: 8px; font-size: 18px;">🚀 Distributor Sign Up</h3>
    <div style="text-align: left; display:flex; flex-direction:column; gap:8px; margin-bottom:12px;">
      <input type="text" id="regName" class="login-input" style="margin-bottom:0;" placeholder="दुकानदार / बिजनेस का नाम">
      <input type="email" id="regEmail" class="login-input" style="margin-bottom:0;" placeholder="ईमेल आईडी">
      <input type="text" id="regMobile" class="login-input" style="margin-bottom:0;" placeholder="मोबाइल नंबर">
      <input type="password" id="regPass" class="login-input" style="margin-bottom:0;" placeholder="पासवर्ड">
    </div>
    <div style="background: rgba(15,23,42,0.8); padding: 12px; border-radius: 10px; margin-bottom: 12px; text-align: left;">
      <label style="font-size: 12px; color: var(--accent-blue); font-weight: 600; display: block; margin-bottom: 8px;">💳 Select Plan:</label>
      <div style="display:flex; gap:10px;">
        <label style="flex:1; background:#334155; padding:8px; border-radius:8px; text-align:center; cursor:pointer; font-size:12px; font-weight:600;"><input type="radio" name="subPlan" value="1 Month" checked onclick="onPlanSelect('1 Month')"> 1 Month (₹36)</label>
        <label style="flex:1; background:#334155; padding:8px; border-radius:8px; text-align:center; cursor:pointer; font-size:12px; font-weight:600;"><input type="radio" name="subPlan" value="1 Year" onclick="onPlanSelect('1 Year')"> 1 Year (₹319)</label>
      </div>
    </div>
    <div style="background: rgba(15,23,42,0.9); padding: 12px; border-radius: 10px; margin-bottom: 12px; text-align: center;">
      <div id="planAmountLabel" style="font-size: 13px; color: #fbbf24; font-weight: 700; margin-bottom: 6px;">Scan & Pay: ₹36</div>
      <img id="dynamicQrImg" src="" style="width: 140px; height: 140px; border-radius: 6px; background:#fff; padding:4px; display:inline-block;" alt="QR">
      <div style="margin-top: 10px; text-align: left;">
        <label style="font-size: 11px; color: var(--accent-blue); display: block; margin-bottom: 4px; font-weight: 600;">📁 Upload Payment Screenshot:</label>
        <input type="file" id="regScreenshotInput" accept="image/*" style="display: block; width: 100%; background: #334155; color: #fff; padding: 6px; font-size: 11px; border-radius: 6px;">
      </div>
    </div>
    <div id="regStatusMsg" style="font-size: 12px; margin-bottom: 10px; display:none;"></div>
    <div style="display: flex; gap: 10px;">
      <button onclick="submitRegistrationRequest()" class="action-btn btn-download" style="flex:1;">🚀 Submit</button>
      <button onclick="closeRegModal()" class="action-btn btn-reset" style="flex:1;">❌ Cancel</button>
    </div>
  </div>
</div>

<!-- View Screenshot Modal -->
<div id="viewScreenshotModal">
  <div class="auth-box" style="max-width:450px; text-align:center;">
    <h3 style="color: var(--accent-blue); margin-bottom: 10px; font-size: 18px;">📸 Payment Screenshot</h3>
    <div style="background:#000; padding:10px; border-radius:8px; margin-bottom:15px;"><img id="adminViewScreenshotImg" src="" style="max-width:100%; max-height:350px; display:block; margin:0 auto;"></div>
    <button onclick="closeViewScreenshotModal()" class="action-btn btn-reset" style="width:100%;">❌ Close</button>
  </div>
</div>

<script>
  // Base64 QR strings for 36 and 319 based on your uploaded images
  const QR_36_DATA = "data:image/jpeg;base64,/9j/4AAQSkZJRgABAQEASABIAAD/4QBaRXhpZgAATU0AKgAAAAgABAEaAAUAAAABAAAAPgEbAAUAAAABAAAARgEoAAMAAAABAAIAAAExAAIAAAAnAAARRgEyAAIAAAAUAAARVIdpAAQAAAABAAARXoglAAQAAAABAAALQohwbgcA...";
  const QR_319_DATA = "data:image/jpeg;base64,/9j/4AAQSkZJRgABAQEASABIAAD/4QBaRXhpZgAATU0AKgAAAAgABAEaAAUAAAABAAAAPgEbAAUAAAABAAAARgEoAAMAAAABAAIAAAExAAIAAAAnAAARRgEyAAIAAAAUAAARVIdpAAQAAAABAAARXoglAAQAAAABAAALQohwbgcA...";

  function openRegModal() { document.getElementById('regModalPopup').style.display = 'flex'; onPlanSelect('1 Month'); }
  function closeRegModal() { document.getElementById('regModalPopup').style.display = 'none'; }

  function onPlanSelect(plan) {
    const qrImg = document.getElementById('dynamicQrImg');
    const label = document.getElementById('planAmountLabel');
    if (plan === '1 Month') {
      label.innerText = "Scan & Pay: ₹36";
      qrImg.src = "36.jpeg"; // Or base64 variable
    } else {
      label.innerText = "Scan & Pay: ₹319";
      qrImg.src = "319.jpeg"; // Or base64 variable
    }
  }

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

  async function submitRegistrationRequest() {
    const name = document.getElementById('regName').value.trim();
    const email = document.getElementById('regEmail').value.trim().toLowerCase();
    const mobile = document.getElementById('regMobile').value.trim();
    const pass = document.getElementById('regPass').value.trim();
    const plan = document.querySelector('input[name="subPlan"]:checked').value;
    const file = document.getElementById('regScreenshotInput').files[0];
    const msg = document.getElementById('regStatusMsg');

    if (!name || !email || !mobile || !pass || !file) {
      msg.innerText = "⚠️ कृपया सभी जानकारी भरें और स्क्रीनशॉट अपलोड करें!"; msg.style.color = "#ef4444"; msg.style.display = "block"; return;
    }

    msg.innerText = "⏳ Submitting..."; msg.style.color = "#fbbf24"; msg.style.display = "block";
    const reader = new FileReader();
    reader.onload = async function(e) {
      const success = await callCloudPost({
        action: "addDistributor",
        data: { id: Date.now(), name, email, pass, assignedTimestamp: Date.now(), expiryTime: Date.now() + (plan === '1 Year' ? 365 : 30)*86400000, status: "Pending", distScreenshot: e.target.result, mobile, plan }
      });
      if (success) {
        msg.innerText = "✅ Submitted! Admin will approve soon."; msg.style.color = "#34d399";
        setTimeout(closeRegModal, 2000);
      } else {
        msg.innerText = "⚠️ Error! Try again."; msg.style.color = "#ef4444";
      }
    };
    reader.readAsDataURL(file);
  }

  async function renderDistributorsTable() {
    let dists = await getDistributorsListCloud();
    const pendingTbody = document.getElementById('pendingRequestsTableBody');
    const activeTbody = document.getElementById('distributorTableBody');
    pendingTbody.innerHTML = ''; activeTbody.innerHTML = '';

    let pendingList = dists.filter(d => String(d.status || '').trim() === 'Pending');
    let activeList = dists.filter(d => String(d.status || '').trim() !== 'Pending');

    if (!pendingList.length) pendingTbody.innerHTML = `<tr><td colspan="6" style="text-align:center; padding:15px;">कोई पेंडिंग रिक्वेस्ट नहीं है।</td></tr>`;
    else pendingList.forEach(d => {
      pendingTbody.innerHTML += `<tr><td><strong>${d.name}</strong></td><td>${d.email}</td><td>${d.mobile||'-'}</td><td>${d.plan||'1 Month'}</td><td>${d.distscreenshot?`<button class="history-view-ss-btn" onclick="viewDistributorScreenshot('${encodeURIComponent(d.distscreenshot)}')">👁️ View</button>`:'No SS'}</td><td><button class="action-btn btn-download" style="padding:4px;" onclick="approveDist('${d.email}','Active')">✅ Accept</button> <button class="history-delete-btn" onclick="approveDist('${d.email}','Rejected')">❌</button></td></tr>`;
    });

    if (!activeList.length) activeTbody.innerHTML = `<tr><td colspan="5" style="text-align:center; padding:15px;">कोई एक्टिव डिस्ट्रीब्यूटर नहीं।</td></tr>`;
    else activeList.forEach(d => {
      activeTbody.innerHTML += `<tr><td><strong>${d.name}</strong></td><td>${d.email}</td><td><code>${d.pass}</code></td><td>${d.plan||'1'} (${d.status||'Active'})</td><td>-</td></tr>`;
    });
  }

  async function approveDist(email, status) {
    await callCloudPost({ action: "toggleStatus", email, status });
    alert(`✅ Done!`); renderDistributorsTable();
  }

  function viewDistributorScreenshot(url) {
    document.getElementById('adminViewScreenshotImg').src = decodeURIComponent(url);
    document.getElementById('viewScreenshotModal').style.display = 'flex';
  }
  function closeViewScreenshotModal() { document.getElementById('viewScreenshotModal').style.display = 'none'; }

  // Resume builder logic
  let eduRows = [{ degree: "BCA", inst: "University", year: "2022" }];
  let expRows = [{ role: "Operator", company: "Seva Kendra", duration: "2023" }];
  function renderDynamicRows() {
    document.getElementById('educationContainer').innerHTML = eduRows.map((e,i)=>`<div style="display:flex;gap:4px;"><input type="text" class="text-field-input" value="${e.degree}" oninput="eduRows[${i}].degree=this.value;updateResumePreview()"><input type="text" class="text-field-input" value="${e.inst}" oninput="eduRows[${i}].inst=this.value;updateResumePreview()"></div>`).join('');
    document.getElementById('experienceContainer').innerHTML = expRows.map((e,i)=>`<div style="display:flex;gap:4px;"><input type="text" class="text-field-input" value="${e.role}" oninput="expRows[${i}].role=this.value;updateResumePreview()"><input type="text" class="text-field-input" value="${e.company}" oninput="expRows[${i}].company=this.value;updateResumePreview()"></div>`).join('');
  }
  function addEducationRow() { eduRows.push({degree:"",inst:"",year:""}); renderDynamicRows(); }
  function addExperienceRow() { expRows.push({role:"",company:"",duration:""}); renderDynamicRows(); }
  function updateResumePreview() {
    const name = document.getElementById('resName').value || "Harshal Marathe";
    document.getElementById('resumePreviewBox').innerHTML = `<h2 style="color:#0284c7;">${name}</h2><p>Professional Resume Preview</p>`;
  }
  renderDynamicRows(); updateResumePreview();

  function switchTab(tabId) {
    document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
    document.querySelectorAll('.tab-content').forEach(content => content.classList.remove('active'));
    event.target.classList.add('active');
    document.getElementById(tabId).classList.add('active');
    if (tabId === 'tab-admin') renderDistributorsTable();
  }
</script>

</body>
</html>
