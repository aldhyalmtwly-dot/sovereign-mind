<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>المنصة الشاملة — النظام السيادي</title>
  <script src="https://cdn.jsdelivr.net/npm/tesseract.js@5/dist/tesseract.min.js"></script>
  <style>
    :root {
      --bg: #0a0e14;
      --surface: #111722;
      --surface-2: #161f2e;
      --border-gold: rgba(212, 160, 76, 0.32);
      --border-blue: rgba(78, 161, 255, 0.32);
      --border-subtle: rgba(255, 255, 255, 0.08);
      --text: #ffffff;
      --text-muted: #9aa7b8;
      --gold: #d4a04c;
      --gold-soft: rgba(212, 160, 76, 0.14);
      --blue: #4ea1ff;
      --blue-soft: rgba(78, 161, 255, 0.14);
      --danger: #ff5c6c;
      --success: #2dd4bf;
      --whatsapp: #25d366;
      --radius: 16px;
      --shadow: 0 20px 50px rgba(0, 0, 0, 0.55);
    }

    * { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      background-color: var(--bg);
      background-image:
        radial-gradient(circle at 15% 15%, rgba(78, 161, 255, 0.08), transparent 35%),
        radial-gradient(circle at 85% 85%, rgba(212, 160, 76, 0.08), transparent 35%);
      color: var(--text);
      font-family: "Cairo", "Tajawal", "Segoe UI", Tahoma, Arial, sans-serif;
      min-height: 100vh;
      line-height: 1.65;
      overflow-x: hidden;
    }

    .app-shell {
      max-width: 960px;
      margin: 0 auto;
      padding: 24px 18px 96px;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
    }

    .screen { display: none; animation: fadeIn 0.28s ease; }
    .screen.active { display: block; }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(8px); }
      to { opacity: 1; transform: translateY(0); }
    }

    .card {
      background: linear-gradient(160deg, var(--surface) 0%, #0d121b 100%);
      border: 1px solid var(--border-subtle);
      border-radius: var(--radius);
      padding: 28px;
      box-shadow: var(--shadow);
      position: relative;
      overflow: hidden;
    }

    .card::before {
      content: "";
      position: absolute;
      inset: 0 0 auto 0;
      height: 2px;
      background: linear-gradient(90deg, transparent, var(--gold), var(--blue), transparent);
      opacity: 0.85;
    }

    .topbar {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 12px;
      margin-bottom: 24px;
      padding-bottom: 16px;
      border-bottom: 1px solid var(--border-subtle);
      flex-wrap: wrap;
    }

    .brand { display: flex; align-items: center; gap: 12px; }

    .brand-mark {
      width: 44px; height: 44px; border-radius: 12px;
      background: linear-gradient(135deg, var(--gold-soft), var(--blue-soft));
      border: 1px solid var(--border-gold);
      display: grid; place-items: center;
      color: var(--gold); font-weight: 800; font-size: 1.1rem;
    }

    .brand-title h1, .screen-title { font-size: 1.4rem; font-weight: 800; color: var(--text); }
    .brand-title p, .subtitle { font-size: 0.9rem; color: var(--text-muted); }

    .badge {
      display: inline-flex; align-items: center; gap: 6px;
      padding: 6px 12px; border-radius: 999px;
      font-size: 0.8rem; font-weight: 700;
      border: 1px solid var(--border-gold);
      background: var(--gold-soft); color: var(--gold);
    }

    .badge.blue { border-color: var(--border-blue); background: var(--blue-soft); color: var(--blue); }

    .btn {
      appearance: none; border: 1px solid transparent; border-radius: 12px;
      padding: 12px 20px; font-family: inherit; font-size: 0.95rem; font-weight: 700;
      cursor: pointer; transition: all 0.2s ease; display: inline-flex;
      align-items: center; justify-content: center; gap: 8px;
      text-decoration: none; color: var(--text); background: var(--surface-2);
    }

    .btn:hover { transform: translateY(-2px); }
    .btn:active { transform: translateY(0); }

    .btn-gold { background: linear-gradient(135deg, var(--gold), #b9832f); color: #0a0e14; box-shadow: 0 8px 24px rgba(212, 160, 76, 0.25); }
    .btn-blue { background: linear-gradient(135deg, var(--blue), #2a7de1); color: #0a0e14; box-shadow: 0 8px 24px rgba(78, 161, 255, 0.25); }
    .btn-outline { background: rgba(255, 255, 255, 0.03); border-color: var(--border-subtle); color: var(--text); }
    .btn-outline:hover { border-color: var(--blue); color: var(--blue); }
    .btn-whatsapp { background: rgba(37, 211, 102, 0.14); border-color: rgba(37, 211, 102, 0.45); color: #7bf0a5; }
    .btn-whatsapp:hover { background: rgba(37, 211, 102, 0.24); }

    .input, .textarea, .select {
      width: 100%; background: #080c12; border: 1px solid var(--border-subtle);
      border-radius: 12px; padding: 13px 16px; color: var(--text);
      font-family: inherit; font-size: 1rem; outline: none; transition: border-color 0.2s ease, box-shadow 0.2s ease;
    }

    .input:focus, .textarea:focus, .select:focus {
      border-color: var(--blue); box-shadow: 0 0 0 3px rgba(78, 161, 255, 0.16);
    }

    .textarea { min-height: 130px; resize: vertical; }
    .label { display: block; margin-bottom: 8px; font-size: 0.92rem; font-weight: 700; color: var(--gold); }

    .status-msg { margin-top: 12px; padding: 11px 14px; border-radius: 10px; font-size: 0.9rem; font-weight: 600; display: none; }
    .status-msg.show { display: block; }
    .status-msg.error { background: rgba(255, 92, 108, 0.12); border: 1px solid rgba(255, 92, 108, 0.4); color: #ff99a4; }
    .status-msg.success { background: rgba(45, 212, 191, 0.12); border: 1px solid rgba(45, 212, 191, 0.4); color: #7ef2e4; }
    .status-msg.info { background: var(--blue-soft); border: 1px solid var(--border-blue); color: #a9d2ff; }

    .lock-wrap { max-width: 430px; margin: 0 auto; text-align: center; }
    .lock-icon {
      width: 68px; height: 68px; margin: 0 auto 16px; border-radius: 20px;
      background: linear-gradient(135deg, var(--gold-soft), var(--blue-soft));
      border: 1px solid var(--border-gold); display: grid; place-items: center; color: var(--gold);
    }

    .pin-dots { display: flex; justify-content: center; gap: 14px; margin: 20px 0; direction: ltr; }
    .pin-dot { width: 16px; height: 16px; border-radius: 50%; border: 2px solid var(--border-gold); background: transparent; transition: all 0.18s ease; }
    .pin-dot.filled { background: var(--gold); box-shadow: 0 0 12px rgba(212, 160, 76, 0.65); transform: scale(1.1); }

    .keypad { display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; margin-top: 18px; direction: ltr; }
    .key-btn {
      height: 54px; border-radius: 12px; border: 1px solid var(--border-subtle);
      background: var(--surface-2); color: var(--text); font-size: 1.2rem; font-weight: 700;
      font-family: inherit; cursor: pointer; transition: all 0.15s ease;
    }
    .key-btn:hover { border-color: var(--gold); background: #1c273a; }
    .key-btn:active { transform: scale(0.97); }
    .key-btn.action-key { font-size: 0.92rem; color: var(--blue); }

    .hub-grid { display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 16px; }
    @media (max-width: 640px) { .hub-grid { grid-template-columns: 1fr; } .card { padding: 20px; } }

    .hub-tile {
      text-align: right; background: linear-gradient(155deg, var(--surface-2), #0d131d);
      border: 1px solid var(--border-subtle); border-radius: 16px; padding: 22px;
      cursor: pointer; color: var(--text); font-family: inherit; transition: all 0.2s ease;
      display: flex; flex-direction: column; gap: 10px; position: relative;
    }

    .hub-tile:hover { transform: translateY(-4px); border-color: var(--gold); box-shadow: 0 14px 30px rgba(0, 0, 0, 0.45); }
    .hub-tile.blue-accent:hover { border-color: var(--blue); }

    .tile-head { display: flex; align-items: center; justify-content: space-between; gap: 10px; }
    .tile-icon {
      width: 46px; height: 46px; border-radius: 12px; display: grid; place-items: center;
      background: var(--gold-soft); border: 1px solid var(--border-gold); color: var(--gold);
    }
    .hub-tile.blue-accent .tile-icon { background: var(--blue-soft); border-color: var(--border-blue); color: var(--blue); }
    .tile-title { font-size: 1.15rem; font-weight: 800; color: var(--text); }
    .tile-desc { font-size: 0.88rem; color: var(--text-muted); }

    .lock-banner {
      background: linear-gradient(135deg, rgba(212, 160, 76, 0.1), rgba(78, 161, 255, 0.08));
      border: 1px solid var(--border-gold); border-radius: 14px; padding: 22px; margin-bottom: 20px;
    }

    .payment-grid { display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 12px; margin-top: 16px; }
    @media (max-width: 580px) { .payment-grid { grid-template-columns: 1fr; } }

    .payment-box {
      background: #0b1018; border: 1px solid var(--border-subtle);
      border-radius: 12px; padding: 16px; display: flex; flex-direction: column; gap: 10px;
    }

    .price-tag { font-size: 1.25rem; font-weight: 800; color: var(--gold); }

    .dropzone {
      border: 2px dashed var(--border-blue); border-radius: 14px; padding: 26px;
      text-align: center; background: rgba(78, 161, 255, 0.04); cursor: pointer; transition: all 0.2s ease;
    }
    .dropzone:hover { background: rgba(78, 161, 255, 0.09); border-color: var(--gold); }

    .preview-img { max-width: 100%; max-height: 260px; border-radius: 12px; border: 1px solid var(--border-subtle); margin-top: 14px; display: none; }

    .progress-track { width: 100%; height: 10px; background: #080c12; border-radius: 999px; overflow: hidden; border: 1px solid var(--border-subtle); margin-top: 14px; display: none; }
    .progress-fill { height: 100%; width: 0%; background: linear-gradient(90deg, var(--gold), var(--blue)); transition: width 0.2s ease; }

    .asdn-summary {
      display: flex; align-items: center; justify-content: space-between; flex-wrap: wrap; gap: 12px;
      background: #080c12; border: 1px solid var(--border-gold); border-radius: 12px; padding: 16px; margin: 18px 0;
    }

    .asdn-chain { display: flex; flex-wrap: wrap; gap: 8px; margin-top: 8px; }
    .signifier-pill {
      display: inline-flex; align-items: center; justify-content: center; min-width: 38px; height: 38px;
      padding: 0 10px; border-radius: 10px; background: var(--gold-soft);
      border: 1px solid var(--border-gold); color: var(--gold); font-size: 1.1rem; font-weight: 800;
    }

    .asdn-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(150px, 1fr)); gap: 12px; margin-top: 14px; }
    .word-card {
      background: var(--surface-2); border: 1px solid var(--border-subtle); border-radius: 12px;
      padding: 14px; display: flex; flex-direction: column; gap: 8px; align-items: center; text-align: center;
    }

    .word-index { font-size: 0.75rem; color: var(--blue); font-weight: 700; }
    .word-text { font-size: 1.05rem; font-weight: 700; color: var(--text); word-break: break-word; }
    .word-signifier {
      width: 42px; height: 42px; border-radius: 10px; display: grid; place-items: center;
      background: rgba(212, 160, 76, 0.16); border: 1px solid var(--gold); color: var(--gold); font-size: 1.25rem; font-weight: 800;
    }

    .atlas-hero { background: linear-gradient(135deg, rgba(212, 160, 76, 0.11), rgba(78, 161, 255, 0.11)); border: 1px solid var(--border-blue); border-radius: 14px; padding: 24px; margin-bottom: 18px; }
    .orcid-box { display: flex; align-items: center; justify-content: space-between; flex-wrap: wrap; gap: 12px; background: #080c12; border: 1px solid var(--border-gold); border-radius: 12px; padding: 14px 18px; margin-top: 16px; }
    .orcid-code { font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace; font-size: 1.08rem; font-weight: 700; color: var(--blue); direction: ltr; }

    .row { display: flex; gap: 10px; flex-wrap: wrap; align-items: center; }
    .char-counter { font-size: 0.85rem; font-weight: 700; color: var(--blue); margin-top: 8px; display: flex; justify-content: space-between; align-items: center; }

    .floating-wa {
      position: fixed; bottom: 22px; left: 22px; z-index: 999; display: none; align-items: center; gap: 10px;
      background: linear-gradient(135deg, #25d366, #189e4b); color: #ffffff; text-decoration: none;
      padding: 12px 18px; border-radius: 999px; font-weight: 800; font-size: 0.92rem;
      box-shadow: 0 12px 30px rgba(37, 211, 102, 0.35); border: 1px solid rgba(255, 255, 255, 0.25);
      transition: all 0.2s ease;
    }
    .floating-wa.visible { display: inline-flex; }
    .floating-wa:hover { transform: translateY(-3px) scale(1.02); box-shadow: 0 16px 36px rgba(37, 211, 102, 0.48); }

    .mt-12 { margin-top: 12px; }
    .mt-16 { margin-top: 16px; }
    .mt-20 { margin-top: 20px; }
    .hidden { display: none !important; }
  </style>
</head>
<body>
  <main class="app-shell">
    <!-- 1. شاشة القفل -->
    <section id="screen-lock" class="screen active">
      <div class="card lock-wrap">
        <div class="lock-icon" aria-hidden="true">
          <svg width="30" height="30" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <rect x="3" y="11" width="18" height="11" rx="2" ry="2"></rect>
            <path d="M7 11V7a5 5 0 0 1 10 0v4"></path>
          </svg>
        </div>
        <h1 class="screen-title">المنصة الشاملة</h1>
        <p class="subtitle mt-12">أدخل رمز التحقق (PIN) للدخول إلى النظام</p>

        <div class="pin-dots" id="pin-dots" aria-hidden="true">
          <span class="pin-dot"></span>
          <span class="pin-dot"></span>
          <span class="pin-dot"></span>
          <span class="pin-dot"></span>
        </div>

        <input id="pin-input" type="password" inputmode="numeric" maxlength="4" class="input" style="text-align:center; letter-spacing: 8px; font-size: 1.25rem; direction: ltr;" placeholder="••••" autocomplete="off" />

        <div class="keypad" id="pin-keypad">
          <button type="button" class="key-btn" data-key="1">1</button>
          <button type="button" class="key-btn" data-key="2">2</button>
          <button type="button" class="key-btn" data-key="3">3</button>
          <button type="button" class="key-btn" data-key="4">4</button>
          <button type="button" class="key-btn" data-key="5">5</button>
          <button type="button" class="key-btn" data-key="6">6</button>
          <button type="button" class="key-btn" data-key="7">7</button>
          <button type="button" class="key-btn" data-key="8">8</button>
          <button type="button" class="key-btn" data-key="9">9</button>
          <button type="button" class="key-btn action-key" data-action="clear">مسح</button>
          <button type="button" class="key-btn" data-key="0">0</button>
          <button type="button" class="key-btn action-key" data-action="back">حذف</button>
        </div>

        <button type="button" id="unlock-btn" class="btn btn-gold mt-16" style="width:100%;">دخول إلى المنصة</button>
        <div id="lock-status" class="status-msg error"></div>
      </div>
    </section>

    <!-- 2. الشاشة الرئيسية -->
    <section id="screen-hub" class="screen">
      <div class="card">
        <div class="topbar">
          <div class="brand">
            <div class="brand-mark">AS</div>
            <div class="brand-title">
              <h1>المركز الرئيسي — المنصة الشاملة</h1>
              <p>بوابة الأدوات البنيوية والتحليل الإشاري</p>
            </div>
          </div>
          <div class="row">
            <span class="badge">النظام نشط</span>
            <button type="button" id="lock-system-btn" class="btn btn-outline">قفل الشاشة</button>
          </div>
        </div>

        <div class="hub-grid">
          <button type="button" class="hub-tile" data-nav="screen-scanner">
            <div class="tile-head">
              <div class="tile-icon">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M3 7V5a2 2 0 0 1 2-2h2"></path><path d="M17 3h2a2 2 0 0 1 2 2v2"></path><path d="M21 17v2a2 2 0 0 1-2 2h-2"></path><path d="M7 21H5a2 2 0 0 1-2-2v-2"></path><line x1="7" y1="12" x2="17" y2="12"></line>
                </svg>
              </div>
              <span id="hub-ocr-badge" class="badge">مقفل</span>
            </div>
            <div class="tile-title">الماسح الضوئي</div>
            <div class="tile-desc">استخراج النصوص العربية والإنجليزية من الصور عبر تقنية Tesseract OCR.</div>
          </button>

          <button type="button" class="hub-tile blue-accent" data-nav="screen-asdn">
            <div class="tile-head">
              <div class="tile-icon">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <polyline points="4 7 4 4 20 4 20 7"></polyline><line x1="9" y1="20" x2="15" y2="20"></line><line x1="12" y1="4" x2="12" y2="20"></line>
                </svg>
              </div>
              <span class="badge blue">صفرية التقدير</span>
            </div>
            <div class="tile-title">محلل ASDN</div>
            <div class="tile-desc">تفكيك الجمل العربية واستخراج الحرف الأخير من كل كلمة كرمز إشاري دقيق.</div>
          </button>

          <button type="button" class="hub-tile" data-nav="screen-atlas">
            <div class="tile-head">
              <div class="tile-icon">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M4 19.5A2.5 2.5 0 0 1 6.5 17H20"></path><path d="M6.5 2H20v20H6.5A2.5 2.5 0 0 1 4 19.5v-15A2.5 2.5 0 0 1 6.5 2z"></path>
                </svg>
              </div>
              <span class="badge">ORCID</span>
            </div>
            <div class="tile-title">الأطلس البنيوي</div>
            <div class="tile-desc">المرجع التعريفي للمؤلف ثروت البهي والمعرّف البحثي الدولي المعتمد.</div>
          </button>

          <button type="button" class="hub-tile blue-accent" data-nav="screen-settings">
            <div class="tile-head">
              <div class="tile-icon">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <circle cx="12" cy="12" r="3"></circle><path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 0 1-2.83 2.83l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-4 0v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 0 1-2.83-2.83l.06-.06a1.65 1.65 0 0 0 .33-1.82 1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1 0-4h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 0 1 2.83-2.83l.06.06a1.65 1.65 0 0 0 1.82.33H9a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 4 0v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 0 1 2.83 2.83l-.06.06a1.65 1.65 0 0 0-.33 1.82V9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 0 1 0 4h-.09a1.65 1.65 0 0 0-1.51 1z"></path>
                </svg>
              </div>
              <span class="badge blue">محلي</span>
            </div>
            <div class="tile-title">إعدادات المدير</div>
            <div class="tile-desc">إدارة وحفظ كلمة مرور التطبيق (16 حرفاً) داخل التخزين المحلي للمتصفح.</div>
          </button>
        </div>
      </div>
    </section>

    <!-- 3. شاشة الماسح الضوئي -->
    <section id="screen-scanner" class="screen">
      <div class="card">
        <div class="topbar">
          <div>
            <h2 class="screen-title">الماسح الضوئي (OCR)</h2>
            <p class="subtitle">استخراج النصوص من الصور محلياً في المتصفح عبر Tesseract.js</p>
          </div>
          <button type="button" class="btn btn-outline" data-nav="screen-hub">العودة للمركز</button>
        </div>

        <div id="ocr-lock-view">
          <div class="lock-banner">
            <span class="badge">الماسح مقفل</span>
            <h3 style="margin-top:10px; font-size:1.15rem;">تفعيل وحدة الماسح الضوئي</h3>
            <p class="subtitle mt-12">هذه الوحدة مقفلة. أدخل كود التفعيل الصحيح لفتح أداة استخراج النصوص من الصور.</p>

            <div class="mt-16">
              <label for="ocr-code-input" class="label">كود التفعيل</label>
              <div class="row">
                <input id="ocr-code-input" type="text" class="input" style="flex:1; min-width:220px; direction:ltr; text-align:center; font-weight:700;" placeholder="أدخل كود التفعيل" autocomplete="off" />
                <button type="button" id="ocr-activate-btn" class="btn btn-gold">تفعيل الماسح</button>
              </div>
            </div>
            <div id="ocr-lock-status" class="status-msg error"></div>
          </div>

          <h4 style="color:var(--blue); font-size:1rem; margin-bottom:6px;">خيارات الحصول على كود التفعيل عبر واتساب</h4>
          <p class="subtitle">اختر الباقة المناسبة للتواصل الفوري والحصول على كود التفعيل:</p>

          <div class="payment-grid">
            <div class="payment-box">
              <span class="badge">داخل مصر</span>
              <div class="price-tag">10 جنيهات مصرية</div>
              <p class="subtitle">اشتراك وتفعيل كامل لأداة الماسح الضوئي داخل جمهورية مصر العربية.</p>
              <a class="btn btn-whatsapp" target="_blank" rel="noopener noreferrer" href="https://wa.me/201033063978?text=%D9%85%D8%B1%D8%AD%D8%A8%D8%A7%D9%8B%D8%8C%20%D8%A3%D8%B1%D8%BA%D8%A8%20%D9%81%D9%8A%20%D8%AA%D9%81%D8%B9%D9%8A%D9%84%20%D8%A7%D9%84%D9%85%D8%A7%D8%B3%D8%AD%20%D8%A7%D9%84%D8%B6%D9%88%D8%A6%D9%8A%20(%D8%A8%D8%A7%D9%82%D8%A9%20%D9%85%D8%B5%D8%B1%20-%2010%20%D8%AC%D9%86%D9%8A%D9%87%D8%A7%D8%AA).">طلب التفعيل (10 جنيهات - مصر)</a>
            </div>

            <div class="payment-box">
              <span class="badge blue">خارج مصر / دولي</span>
              <div class="price-tag" style="color:var(--blue);">1 دولار أمريكي</div>
              <p class="subtitle">تفعيل دولي فوري لأداة الماسح الضوئي خارج جمهورية مصر العربية.</p>
              <a class="btn btn-whatsapp" target="_blank" rel="noopener noreferrer" href="https://wa.me/201033063978?text=%D9%85%D8%B1%D8%AD%D8%A8%D8%A7%D9%8B%D8%8C%20%D8%A3%D8%B1%D8%BA%D8%A8%20%D9%81%D9%8A%20%D8%AA%D9%81%D8%B9%D9%8A%D9%84%20%D8%A7%D9%84%D9%85%D8%A7%D8%B3%D8%AD%20%D8%A7%D9%84%D8%B6%D9%88%D8%A6%D9%8A%20(%D8%A7%D9%84%D8%A8%D8%A7%D9%82%D8%A9%20%D8%A7%D9%84%D8%AF%D9%88%D9%84%D9%8A%D8%A9%20-%201%20%D8%AF%D9%88%D9%84%D8%A7%D8%B1).">طلب التفعيل (1 دولار - للخارج)</a>
            </div>
          </div>
        </div>

        <div id="ocr-workspace" class="hidden">
          <div class="row" style="justify-content:space-between; margin-bottom:14px;">
            <span class="badge">تم التفعيل بنجاح</span>
            <button type="button" id="ocr-relock-btn" class="btn btn-outline" style="padding:8px 14px; font-size:0.85rem;">إعادة قفل الماسح</button>
          </div>

          <div class="row" style="margin-bottom:14px;">
            <div style="flex:1; min-width:200px;">
              <label for="ocr-lang" class="label">لغة القراءة الضوئية</label>
              <select id="ocr-lang" class="select">
                <option value="ara+eng">العربية + الإنجليزية (ara+eng)</option>
                <option value="ara">العربية فقط (ara)</option>
                <option value="eng">الإنجليزية فقط (eng)</option>
              </select>
            </div>
          </div>

          <label for="ocr-file" class="dropzone" style="display:block;">
            <strong style="color:var(--gold); font-size:1.05rem;">اضغط لاختيار صورة أو اسحبها هنا</strong>
            <p class="subtitle mt-12">يدعم PNG و JPG و WEBP — تتم المعالجة مباشرة داخل متصفحك</p>
            <input id="ocr-file" type="file" accept="image/*" class="hidden" />
            <img id="ocr-preview" class="preview-img" alt="معاينة الصورة" />
          </label>

          <div class="row mt-16">
            <button type="button" id="ocr-run-btn" class="btn btn-blue">استخراج النص الآن</button>
            <button type="button" id="ocr-copy-btn" class="btn btn-outline">نسخ النص</button>
            <button type="button" id="ocr-clear-btn" class="btn btn-outline">مسح</button>
          </div>

          <div id="ocr-progress-track" class="progress-track">
            <div id="ocr-progress-fill" class="progress-fill"></div>
          </div>
          <div id="ocr-status" class="status-msg info"></div>

          <div class="mt-16">
            <label for="ocr-output" class="label">النص المستخرج</label>
            <textarea id="ocr-output" class="textarea" placeholder="سيظهر النص المستخرج من الصورة هنا..."></textarea>
          </div>
        </div>
      </div>
    </section>

    <!-- 4. شاشة محلل ASDN -->
    <section id="screen-asdn" class="screen">
      <div class="card">
        <div class="topbar">
          <div>
            <h2 class="screen-title">محلل ASDN — صفرية التقدير</h2>
            <p class="subtitle">تفكيك الجملة العربية واستخلاص الحرف الأخير من كل كلمة كرمز إشاري</p>
          </div>
          <button type="button" class="btn btn-outline" data-nav="screen-hub">العودة للمركز</button>
        </div>

        <label for="asdn-input" class="label">أدخل الجملة العربية</label>
        <textarea id="asdn-input" class="textarea" placeholder="اكتب جملة عربية هنا لتحليلها إلى كلمات واستخراج الرمز الإشاري لكل كلمة..."></textarea>

        <div class="row mt-16">
          <button type="button" id="asdn-analyze-btn" class="btn btn-gold">تحليل الجملة</button>
          <button type="button" id="asdn-sample-btn" class="btn btn-blue">إدراج مثال</button>
          <button type="button" id="asdn-clear-btn" class="btn btn-outline">مسح</button>
        </div>

        <div id="asdn-results" class="hidden">
          <div class="asdn-summary">
            <div>
              <div style="font-size:0.9rem; color:var(--text-muted);">تسلسل الرموز الإشارية (صفرية التقدير):</div>
              <div id="asdn-chain" class="asdn-chain"></div>
            </div>
            <div class="badge blue" id="asdn-count-badge">0 كلمات</div>
          </div>
          <div id="asdn-grid" class="asdn-grid"></div>
        </div>
        <div id="asdn-status" class="status-msg error"></div>
      </div>
    </section>

    <!-- 5. شاشة الأطلس البنيوي -->
    <section id="screen-atlas" class="screen">
      <div class="card">
        <div class="topbar">
          <div>
            <h2 class="screen-title">الأطلس البنيوي</h2>
            <p class="subtitle">البطاقة المرجعية والتوثيق العلمي للمؤلف</p>
          </div>
          <button type="button" class="btn btn-outline" data-nav="screen-hub">العودة للمركز</button>
        </div>

        <div class="atlas-hero">
          <span class="badge">توثيق المؤلف</span>
          <h3 style="font-size:1.5rem; margin-top:12px; color:var(--gold);">ثروت البهي</h3>
          <p class="mt-12" style="color:var(--text); line-height:1.9;">
            الأطلس البنيوي هو المرجع النظري والتطبيقي الذي يقدمه الباحث والمؤلف <strong>ثروت البهي</strong>،
            لتأسيس منهجية التحليل البنيوي الإشاري القائمة على مبدأ <strong>صفرية التقدير</strong>؛ حيث تُقرأ
            البنية اللغوية بوصفها إشارات محكمة ومنضبطة بالحرف الأخير في كل كلمة دون اجتهاد تأويلي أو تقدير شخصي.
          </p>

          <div class="orcid-box">
            <div>
              <div style="font-size:0.82rem; color:var(--text-muted);">المعرّف البحثي الدولي (ORCID)</div>
              <div class="orcid-code" id="orcid-value">0009-000-8043-9651</div>
            </div>
            <button type="button" id="copy-orcid-btn" class="btn btn-blue">نسخ رقم ORCID</button>
          </div>
          <div id="atlas-status" class="status-msg success"></div>
        </div>
      </div>
    </section>

    <!-- 6. شاشة إعدادات المدير -->
    <section id="screen-settings" class="screen">
      <div class="card">
        <div class="topbar">
          <div>
            <h2 class="screen-title">إعدادات المدير</h2>
            <p class="subtitle">حفظ كلمة مرور التطبيق محلياً في المتصفح (localStorage)</p>
          </div>
          <button type="button" class="btn btn-outline" data-nav="screen-hub">العودة للمركز</button>
        </div>

        <label for="app-password-input" class="label">كلمة مرور التطبيق 16 حرفاً</label>
        <div class="row">
          <input id="app-password-input" type="password" maxlength="16" class="input" style="flex:1; min-width:240px; direction:ltr; font-family:monospace; letter-spacing:2px;" placeholder="أدخل 16 حرفاً أو رقماً" autocomplete="off" />
          <button type="button" id="toggle-pass-btn" class="btn btn-outline">إظهار</button>
        </div>

        <div class="char-counter">
          <span id="pass-counter">0 / 16 حرف</span>
          <span id="pass-saved-indicator" style="color:var(--gold);"></span>
        </div>

        <div class="row mt-16">
          <button type="button" id="save-pass-btn" class="btn btn-gold">حفظ في localStorage</button>
          <button type="button" id="delete-pass-btn" class="btn btn-outline">حذف المحفوظ</button>
        </div>

        <div id="settings-status" class="status-msg"></div>
      </div>
    </section>
  </main>

  <!-- زر واتساب عائم -->
  <a id="floating-whatsapp" class="floating-wa" href="https://wa.me/201033063978?text=%D9%85%D8%B1%D8%AD%D8%A8%D8%A7%D9%8B%D8%8C%20%D8%A3%D8%AA%D9%88%D8%A7%D8%B5%D9%84%20%D9%85%D8%B9%D9%83%D9%85%20%D8%B9%D8%A8%D8%B1%20%D8%A7%D9%84%D9%85%D9%86%D8%B5%D8%A9%20%D8%A7%D9%84%D8%B4%D8%A7%D9%85%D9%84%D8%A9." target="_blank" rel="noopener noreferrer" aria-label="تواصل عبر واتساب">
    <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">
      <path d="M20.52 3.48A11.86 11.86 0 0 0 12.06 0C5.49 0 .14 5.34.14 11.91c0 2.1.55 4.15 1.6 5.95L0 24l6.31-1.65a11.88 11.88 0 0 0 5.75 1.47h.01c6.57 0 11.92-5.34 11.92-11.91 0-3.18-1.24-6.17-3.47-8.43zm-8.46 18.32h-.01a9.9 9.9 0 0 1-5.05-1.38l-.36-.22-3.74.98 1-3.64-.24-.37a9.89 9.89 0 0 1-1.52-5.26C2.14 6.45 6.6 2 12.07 2c2.64 0 5.13 1.03 7 2.9a9.84 9.84 0 0 1 2.9 7.01c0 5.46-4.45 9.89-9.91 9.89zm5.43-7.42c-.3-.15-1.76-.87-2.03-.97-.27-.1-.47-.15-.67.15-.2.3-.77.97-.94 1.17-.17.2-.35.22-.65.07-.3-.15-1.26-.46-2.4-1.48-.89-.79-1.49-1.76-1.66-2.06-.17-.3-.02-.46.13-.61.13-.13.3-.35.45-.52.15-.17.2-.3.3-.5.1-.2.05-.37-.02-.52-.07-.15-.67-1.61-.92-2.2-.24-.58-.49-.5-.67-.51h-.57c-.2 0-.52.07-.79.37-.27.3-1.04 1.02-1.04 2.48s1.07 2.88 1.22 3.08c.15.2 2.1 3.21 5.09 4.5.71.31 1.27.49 1.7.63.71.23 1.36.2 1.87.12.57-.09 1.76-.72 2.01-1.41.25-.7.25-1.3.17-1.42-.07-.12-.27-.2-.57-.35z"/>
    </svg>
    <span>واتساب</span>
  </a>

  <script>
    (function () {
      const CORRECT_PIN = "7777";
      const OCR_CODE = "MATWALI-OCR-777";
      const STORAGE_PASS_KEY = "almanassa_app_password_16";
      const STORAGE_OCR_KEY = "almanassa_ocr_unlocked";

      let isUnlocked = false;
      let ocrUnlocked = false;
      try { ocrUnlocked = localStorage.getItem(STORAGE_OCR_KEY) === "true"; } catch (e) {}
      
      let selectedImageFile = null;

      const screens = document.querySelectorAll(".screen");
      const floatingWa = document.getElementById("floating-whatsapp");

      function showStatus(el, text, type) {
        if (!el) return;
        el.textContent = text;
        el.className = "status-msg show " + type;
      }

      function hideStatus(el) {
        if (!el) return;
        el.textContent = "";
        el.className = "status-msg";
      }

      function navigate(screenId) {
        if (!isUnlocked && screenId !== "screen-lock") {
          screenId = "screen-lock";
        }
        screens.forEach((s) => s.classList.toggle("active", s.id === screenId));
        if (floatingWa) {
          floatingWa.classList.toggle("visible", isUnlocked && screenId !== "screen-lock");
        }
        if (screenId === "screen-scanner") {
          renderOcrLockState();
        }
      }

      document.querySelectorAll("[data-nav]").forEach((btn) => {
        btn.addEventListener("click", () => navigate(btn.getAttribute("data-nav")));
      });

      // ---------------- 1. شاشة القفل ----------------
      const pinInput = document.getElementById("pin-input");
      const pinDots = document.querySelectorAll("#pin-dots .pin-dot");
      const lockStatus = document.getElementById("lock-status");
      const unlockBtn = document.getElementById("unlock-btn");

      function syncPinDots() {
        if(!pinInput) return;
        const len = pinInput.value.length;
        pinDots.forEach((dot, idx) => dot.classList.toggle("filled", idx < len));
      }

      function attemptUnlock() {
        if(!pinInput) return;
        const entered = pinInput.value.trim();
        if (entered === CORRECT_PIN) {
          isUnlocked = true;
          hideStatus(lockStatus);
          pinInput.value = "";
          syncPinDots();
          navigate("screen-hub");
        } else {
          showStatus(lockStatus, "رمز PIN غير صحيح. الرمز المطلوب مكوّن من 4 أرقام.", "error");
          pinInput.value = "";
          syncPinDots();
          pinInput.focus();
        }
      }

      if (pinInput) {
        pinInput.addEventListener("input", () => {
          pinInput.value = pinInput.value.replace(/\D/g, "").slice(0, 4);
          syncPinDots();
          hideStatus(lockStatus);
          if (pinInput.value.length === 4) {
            attemptUnlock();
          }
        });

        pinInput.addEventListener("keydown", (e) => {
          if (e.key === "Enter") {
            attemptUnlock();
          }
        });
      }

      const pinKeypad = document.getElementById("pin-keypad");
      if (pinKeypad) {
        pinKeypad.addEventListener("click", (e) => {
          const btn = e.target.closest("button");
          if (!btn) return;
          const key = btn.getAttribute("data-key");
          const action = btn.getAttribute("data-action");
          if (key !== null && pinInput && pinInput.value.length < 4) {
            pinInput.value += key;
            syncPinDots();
            hideStatus(lockStatus);
            if (pinInput.value.length === 4) {
              attemptUnlock();
            }
          } else if (action === "clear" && pinInput) {
            pinInput.value = "";
            syncPinDots();
            hideStatus(lockStatus);
          } else if (action === "back" && pinInput) {
            pinInput.value = pinInput.value.slice(0, -1);
            syncPinDots();
          }
        });
      }

      if (unlockBtn) unlockBtn.addEventListener("click", attemptUnlock);

      const lockSystemBtn = document.getElementById("lock-system-btn");
      if (lockSystemBtn) {
        lockSystemBtn.addEventListener("click", () => {
          isUnlocked = false;
          navigate("screen-lock");
        });
      }

      // ---------------- 3. شاشة الماسح الضوئي ----------------
      const ocrLockView = document.getElementById("ocr-lock-view");
      const ocrWorkspace = document.getElementById("ocr-workspace");
      const hubOcrBadge = document.getElementById("hub-ocr-badge");
      const ocrCodeInput = document.getElementById("ocr-code-input");
      const ocrLockStatus = document.getElementById("ocr-lock-status");
      const ocrFile = document.getElementById("ocr-file");
      const ocrPreview = document.getElementById("ocr-preview");
      const ocrProgressTrack = document.getElementById("ocr-progress-track");
      const ocrProgressFill = document.getElementById("ocr-progress-fill");
      const ocrStatus = document.getElementById("ocr-status");
      const ocrOutput = document.getElementById("ocr-output");
      const ocrLang = document.getElementById("ocr-lang");

      function renderOcrLockState() {
        if(ocrLockView) ocrLockView.classList.toggle("hidden", ocrUnlocked);
        if(ocrWorkspace) ocrWorkspace.classList.toggle("hidden", !ocrUnlocked);
        if(hubOcrBadge) hubOcrBadge.textContent = ocrUnlocked ? "مفعّل" : "مقفل";
      }

      renderOcrLockState();

      const ocrActivateBtn = document.getElementById("ocr-activate-btn");
      if (ocrActivateBtn) {
        ocrActivateBtn.addEventListener("click", () => {
          const code = ocrCodeInput ? ocrCodeInput.value.trim() : "";
          if (code === OCR_CODE) {
            ocrUnlocked = true;
            try { localStorage.setItem(STORAGE_OCR_KEY, "true"); } catch (e) {}
            hideStatus(ocrLockStatus);
            if(ocrCodeInput) ocrCodeInput.value = "";
            renderOcrLockState();
          } else {
            showStatus(ocrLockStatus, "كود التفعيل غير صحيح. يرجى التأكد من الكود أو طلبه عبر واتساب.", "error");
          }
        });
      }

      if (ocrCodeInput) {
        ocrCodeInput.addEventListener("keydown", (e) => {
          if (e.key === "Enter" && ocrActivateBtn) {
            ocrActivateBtn.click();
          }
        });
      }

      const ocrRelockBtn = document.getElementById("ocr-relock-btn");
      if (ocrRelockBtn) {
        ocrRelockBtn.addEventListener("click", () => {
          ocrUnlocked = false;
          try { localStorage.removeItem(STORAGE_OCR_KEY); } catch (e) {}
          renderOcrLockState();
        });
      }

      if (ocrFile) {
        ocrFile.addEventListener("change", () => {
          const file = ocrFile.files && ocrFile.files[0];
          if (!file) return;
          selectedImageFile = file;
          const reader = new FileReader();
          reader.onload = (ev) => {
            if(ocrPreview) {
              ocrPreview.src = ev.target.result;
              ocrPreview.style.display = "inline-block";
            }
          };
          reader.readAsDataURL(file);
          hideStatus(ocrStatus);
        });
      }

      const ocrRunBtn = document.getElementById("ocr-run-btn");
      if (ocrRunBtn) {
        ocrRunBtn.addEventListener("click", async () => {
          if (!ocrUnlocked) return;
          if (!selectedImageFile) {
            showStatus(ocrStatus, "يرجى اختيار صورة أولاً قبل بدء الاستخراج.", "error");
            return;
          }
          if (typeof Tesseract === "undefined") {
            showStatus(ocrStatus, "تعذر تحميل مكتبة Tesseract.js من CDN. تحقق من الاتصال بالإنترنت.", "error");
            return;
          }

          if(ocrProgressTrack) ocrProgressTrack.style.display = "block";
          if(ocrProgressFill) ocrProgressFill.style.width = "5%";
          showStatus(ocrStatus, "جاري تهيئة محرك القراءة الضوئية ومعالجة الصورة...", "info");

          try {
            const result = await Tesseract.recognize(selectedImageFile, ocrLang ? ocrLang.value : "ara+eng", {
              logger: (info) => {
                if (typeof info.progress === "number") {
                  const pct = Math.max(5, Math.round(info.progress * 100));
                  if(ocrProgressFill) ocrProgressFill.style.width = pct + "%";
                  showStatus(ocrStatus, "جاري استخراج النص... (" + pct + "%)", "info");
                }
              }
            });

            const text = (result && result.data && result.data.text ? result.data.text : "").trim();
            if(ocrOutput) ocrOutput.value = text;
            if(ocrProgressFill) ocrProgressFill.style.width = "100%";
            if (text) {
              showStatus(ocrStatus, "تم استخراج النص بنجاح.", "success");
            } else {
              showStatus(ocrStatus, "لم يتم العثور على نص واضح داخل الصورة.", "info");
            }
          } catch (err) {
            showStatus(ocrStatus, "حدث خطأ أثناء معالجة الصورة: " + (err.message || err), "error");
          }
        });
      }

      const ocrCopyBtn = document.getElementById("ocr-copy-btn");
      if (ocrCopyBtn) {
        ocrCopyBtn.addEventListener("click", async () => {
          if (!ocrOutput || !ocrOutput.value.trim()) return;
          try {
            await navigator.clipboard.writeText(ocrOutput.value);
            showStatus(ocrStatus, "تم نسخ النص المستخرج إلى الحافظة.", "success");
          } catch {
            ocrOutput.select();
            document.execCommand("copy");
            showStatus(ocrStatus, "تم نسخ النص.", "success");
          }
        });
      }

      const ocrClearBtn = document.getElementById("ocr-clear-btn");
      if (ocrClearBtn) {
        ocrClearBtn.addEventListener("click", () => {
          selectedImageFile = null;
          if(ocrFile) ocrFile.value = "";
          if(ocrPreview) { ocrPreview.src = ""; ocrPreview.style.display = "none"; }
          if(ocrOutput) ocrOutput.value = "";
          if(ocrProgressTrack) ocrProgressTrack.style.display = "none";
          if(ocrProgressFill) ocrProgressFill.style.width = "0%";
          hideStatus(ocrStatus);
        });
      }

      // ---------------- 4. شاشة محلل ASDN ----------------
      const asdnInput = document.getElementById("asdn-input");
      const asdnResults = document.getElementById("asdn-results");
      const asdnChain = document.getElementById("asdn-chain");
      const asdnGrid = document.getElementById("asdn-grid");
      const asdnCountBadge = document.getElementById("asdn-count-badge");
      const asdnStatus = document.getElementById("asdn-status");

      function extractLastLetter(rawWord) {
        const cleaned = rawWord
          .replace(/[\u064B-\u065F\u0670\u0640]/g, "")
          .replace(/[.,،؛:!؟?"'()\[\]{}«»\-_/\\]/g, "");
        if (!cleaned.length) {
          return rawWord.slice(-1);
        }
        const chars = Array.from(cleaned);
        return chars[chars.length - 1];
      }

      function analyzeAsdn() {
        if(!asdnInput) return;
        const raw = asdnInput.value.trim();
        if (!raw) {
          if(asdnResults) asdnResults.classList.add("hidden");
          showStatus(asdnStatus, "أدخل جملة عربية أولاً لتطبيق تحليل صفرية التقدير.", "error");
          return;
        }
        hideStatus(asdnStatus);

        const words = raw.split(/\s+/).filter(Boolean);
        if(asdnChain) asdnChain.innerHTML = "";
        if(asdnGrid) asdnGrid.innerHTML = "";

        words.forEach((word, index) => {
          const signifier = extractLastLetter(word);

          if(asdnChain) {
            const pill = document.createElement("span");
            pill.className = "signifier-pill";
            pill.textContent = signifier;
            asdnChain.appendChild(pill);
          }

          if(asdnGrid) {
            const card = document.createElement("div");
            card.className = "word-card";
            const idxEl = document.createElement("div");
            idxEl.className = "word-index";
            idxEl.textContent = "كلمة #" + (index + 1);
            const wordEl = document.createElement("div");
            wordEl.className = "word-text";
            wordEl.textContent = word;
            const sigLabel = document.createElement("div");
            sigLabel.style.fontSize = "0.75rem";
            sigLabel.style.color = "var(--text-muted)";
            sigLabel.textContent = "الرمز الإشاري";
            const sigEl = document.createElement("div");
            sigEl.className = "word-signifier";
            sigEl.textContent = signifier;
            
            card.appendChild(idxEl); card.appendChild(wordEl); card.appendChild(sigLabel); card.appendChild(sigEl);
            asdnGrid.appendChild(card);
          }
        });

        if(asdnCountBadge) asdnCountBadge.textContent = words.length + " كلمة — صفرية التقدير";
        if(asdnResults) asdnResults.classList.remove("hidden");
      }

      const asdnAnalyzeBtn = document.getElementById("asdn-analyze-btn");
      if (asdnAnalyzeBtn) asdnAnalyzeBtn.addEventListener("click", analyzeAsdn);

      const asdnSampleBtn = document.getElementById("asdn-sample-btn");
      if (asdnSampleBtn) {
        asdnSampleBtn.addEventListener("click", () => {
          if(asdnInput) asdnInput.value = "المنصة الشاملة توثق البنية الإشارية وفق صفرية التقدير";
          analyzeAsdn();
        });
      }

      const asdnClearBtn = document.getElementById("asdn-clear-btn");
      if (asdnClearBtn) {
        asdnClearBtn.addEventListener("click", () => {
          if(asdnInput) asdnInput.value = "";
          if(asdnChain) asdnChain.innerHTML = "";
          if(asdnGrid) asdnGrid.innerHTML = "";
          if(asdnResults) asdnResults.classList.add("hidden");
          hideStatus(asdnStatus);
        });
      }

      // ---------------- 5. شاشة الأطلس البنيوي ----------------
      const atlasStatus = document.getElementById("atlas-status");
      const copyOrcidBtn = document.getElementById("copy-orcid-btn");
      if (copyOrcidBtn) {
        copyOrcidBtn.addEventListener("click", async () => {
          const orcid = "0009-000-8043-9651";
          try {
            await navigator.clipboard.writeText(orcid);
            showStatus(atlasStatus, "تم نسخ رقم ORCID بنجاح: " + orcid, "success");
          } catch {
            showStatus(atlasStatus, "رقم ORCID: " + orcid, "info");
          }
        });
      }

      // ---------------- 6. شاشة الإعدادات ----------------
      const passInput = document.getElementById("app-password-input");
      const passCounter = document.getElementById("pass-counter");
      const passSavedIndicator = document.getElementById("pass-saved-indicator");
      const settingsStatus = document.getElementById("settings-status");
      const togglePassBtn = document.getElementById("toggle-pass-btn");

      function updatePassUI() {
        if(!passInput) return;
        const len = passInput.value.length;
        if(passCounter) passCounter.textContent = len + " / 16 حرف";
        let saved = null;
        try { saved = localStorage.getItem(STORAGE_PASS_KEY); } catch(e) {}
        if(passSavedIndicator) passSavedIndicator.textContent = saved ? "الحالة: توجد كلمة مرور محفوظة" : "الحالة: غير محفوظة";
      }

      let existingPass = null;
      try { existingPass = localStorage.getItem(STORAGE_PASS_KEY); } catch(e) {}
      if (existingPass && passInput) {
        passInput.value = existingPass;
      }
      updatePassUI();

      if (passInput) {
        passInput.addEventListener("input", () => {
          if (passInput.value.length > 16) {
            passInput.value = passInput.value.slice(0, 16);
          }
          updatePassUI();
          hideStatus(settingsStatus);
        });
      }

      if (togglePassBtn && passInput) {
        togglePassBtn.addEventListener("click", () => {
          const isHidden = passInput.type === "password";
          passInput.type = isHidden ? "text" : "password";
          togglePassBtn.textContent = isHidden ? "إخفاء" : "إظهار";
        });
      }

      const savePassBtn = document.getElementById("save-pass-btn");
      if (savePassBtn) {
        savePassBtn.addEventListener("click", () => {
          if(!passInput) return;
          const val = passInput.value;
          if (val.length !== 16) {
            showStatus(settingsStatus, "يجب أن تتكون كلمة مرور التطبيق من 16 حرفاً بالضبط (الحالي: " + val.length + ").", "error");
            return;
          }
          try { localStorage.setItem(STORAGE_PASS_KEY, val); } catch(e) {}
          updatePassUI();
          showStatus(settingsStatus, "تم حفظ كلمة مرور التطبيق (16 حرفاً) في localStorage بنجاح.", "success");
        });
      }

      const deletePassBtn = document.getElementById("delete-pass-btn");
      if (deletePassBtn) {
        deletePassBtn.addEventListener("click", () => {
          try { localStorage.removeItem(STORAGE_PASS_KEY); } catch(e) {}
          if(passInput) passInput.value = "";
          updatePassUI();
          showStatus(settingsStatus, "تم حذف كلمة مرور التطبيق من localStorage.", "info");
        });
      }
    })();
  </script>
</body>
</html>
