<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Global File Converter â€” Convert PDF, Word, Excel, Images</title>
  <meta name="description" content="Convert PDFâ†”Word/Excel, Imagesâ†”Text/Word/Excel, resize images, passport crop. Multi-language UI with flags. 3 free conversions/day, subscription available." />
  <style>
    /* Blue iLovePDF-like theme (calm blue + white) */
    :root{
      --bg:#f4f8fd;
      --primary:#1e6fff; /* main blue */
      --primary-2:#1455d9;
      --muted:#6b7280;
      --card:#ffffff;
      --accent:#4ea3ff;
      --success:#10b981;
      --danger:#ef4444;
      --shadow: 0 8px 30px rgba(20,37,80,0.06);
    }
    *{box-sizing:border-box}
    html,body{height:100%}
    body{margin:0;font-family:Inter,system-ui,Segoe UI,Roboto,Arial;background:var(--bg);color:#0b1220;-webkit-font-smoothing:antialiased}
    header{background:linear-gradient(90deg,#ffffff 0%,#f8fbff 100%);border-bottom:1px solid rgba(15,23,42,0.04)}
    .nav{max-width:1100px;margin:0 auto;padding:18px;display:flex;align-items:center;gap:16px}
    .brand{display:flex;align-items:center;gap:12px}
    .logo{width:46px;height:46px;border-radius:10px;background:linear-gradient(180deg,var(--primary),var(--primary-2));display:flex;align-items:center;justify-content:center;color:#fff;font-weight:800;box-shadow:0 6px 18px rgba(30,111,255,0.18)}
    h1{font-size:18px;margin:0}
    .tools{max-width:1100px;margin:22px auto;padding:22px}
    .hero{display:flex;gap:20px;align-items:center;background:var(--card);padding:22px;border-radius:12px;box-shadow:var(--shadow)}
    .hero-left{flex:1}
    .hero-right{width:280px}
    .tool-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:14px;margin-top:18px}
    .card{background:var(--card);padding:16px;border-radius:12px;border:1px solid rgba(15,23,42,0.03);box-shadow:0 6px 18px rgba(15,23,42,0.02)}
    .card h3{margin:0 0 8px 0}
    .muted{color:var(--muted);font-size:13px}
    .btn{display:inline-block;padding:10px 14px;border-radius:10px;background:var(--primary);color:#fff;font-weight:700;border:0;cursor:pointer;box-shadow:0 6px 18px rgba(30,111,255,0.12)}
    .btn-ghost{background:transparent;border:1px solid rgba(30,111,255,0.12);color:var(--primary);padding:8px 12px;border-radius:10px;cursor:pointer}
    .langbar{margin-left:auto;display:flex;gap:8px;align-items:center}
    select.lang{padding:8px;border-radius:8px;border:1px solid rgba(15,23,42,0.06);background:white}
    footer{max-width:1100px;margin:28px auto;padding:18px;color:var(--muted);font-size:13px}
    .hidden{display:none}
    .center{display:flex;align-items:center;justify-content:center}
    .small{font-size:13px;color:var(--muted)}
    .pill{display:inline-block;padding:6px 10px;border-radius:999px;background:linear-gradient(90deg,#e8f1ff,#f4f9ff);color:var(--primary);font-weight:600}

    /* Floating download */
    #globalDownloadBtn{position:fixed;right:18px;bottom:18px;z-index:4000;padding:12px 16px;border-radius:12px;background:linear-gradient(90deg,var(--primary),var(--accent));color:white;font-weight:700;display:none;text-decoration:none}

    /* Modal / overlay */
    .overlay{position:fixed;inset:0;background:rgba(2,6,23,0.5);display:none;align-items:center;justify-content:center;z-index:5000;padding:20px}
    .modal-card{width:420px;max-width:100%;background:var(--card);padding:20px;border-radius:12px;box-shadow:var(--shadow)}

    /* pricing cards inside modal */
    .pricing-row{display:flex;gap:10px;margin-top:12px}
    .pricing-card{flex:1;padding:14px;border-radius:10px;border:1px solid rgba(15,23,42,0.03);background:linear-gradient(90deg,#ffffff,#f9fbff)}
    .strike{color:var(--muted);text-decoration:line-through;font-weight:600}

    /* smaller screens */
    @media (max-width:720px){.hero{flex-direction:column}.hero-right{width:100%}.pricing-row{flex-direction:column}}
  </style>
</head>
<body>
  <header>
    <div class="nav">
      <div class="brand">
        <div class="logo">G</div>
        <div>
          <div style="font-weight:800">Global File Converter</div>
          <div class="small">Simple, fast, secure â€” convert files online</div>
        </div>
      </div>

      <nav style="margin-left:24px">
        <a href="#/" data-nav class="small" style="color:var(--muted);text-decoration:none;margin-right:12px">Home</a>
        <a href="#/privacy" data-nav class="small" style="color:var(--muted);text-decoration:none;margin-right:12px">Privacy Policy</a>
        <a href="#/contact" data-nav class="small" style="color:var(--muted);text-decoration:none">Contact</a>
      </nav>

      <div class="langbar" title="Change language">
        <label class="small" style="margin-right:6px">Language</label>
        <select id="langSelect" class="lang" aria-label="Select language"></select>
      </div>
    </div>
  </header>

  <main class="tools" id="app">
    <!-- Splash / language prompt area -->
    <section id="splash" class="hero">
      <div class="hero-left">
        <h2 data-i18n="splash_title">Welcome to Global File Converter</h2>
        <p class="muted" data-i18n="splash_sub">Main language: English. Free: 3 files/day. Try a 7-day trial of Premium.</p>
        <div style="margin-top:12px">
          <button class="btn" id="startBtn" data-i18n="start_btn">Select Language & Start</button>
          <button class="btn-ghost" id="trialBtn" style="margin-left:10px">Start 7-Day Trial</button>
        </div>
        <div style="margin-top:10px">
          <span class="pill">Monthly: $9.99</span>
          <span class="small" style="margin-left:8px">3 months -10% | 6 months -18% | 1 year -27%</span>
        </div>
      </div>
      <div class="hero-right card">
        <div style="font-weight:700;margin-bottom:8px" data-i18n="popular_tools">Popular tools</div>
        <div class="small">PDF to Word<br>PDF to Excel<br>Image to Text (OCR)</div>
      </div>
    </section>

    <!-- Main dashboard -->
    <section id="dashboard" class="hidden">
      <div style="display:flex;align-items:center;gap:16px;margin-bottom:12px">
        <h2 data-i18n="dashboard_title">Convert files â€” pick a tool</h2>
        <div class="muted">(<span id="usageInfo">0</span>/3 free today)</div>
      </div>

      <div class="tool-grid">
        <!-- PDF -> Word/Excel card -->
        <div class="card">
          <h3 data-i18n="pdf_tools">PDF Tools</h3>
          <div class="muted" data-i18n="pdf_sub">Convert PDF to Word, Excel, Text, and more.</div>
          <div style="margin-top:12px" class="file-input">
            <input id="pdfFile" type="file" accept="application/pdf" />
            <select id="pdfOutput">
              <optgroup label="Word"><option value="docx">.docx</option><option value="doc">.doc</option><option value="rtf">.rtf</option></optgroup>
              <optgroup label="Excel"><option value="xlsx">.xlsx</option><option value="csv">.csv</option></optgroup>
            </select>
            <button class="btn" id="pdfConvert">Convert</button>
          </div>
          <div id="pdfStatus" class="small muted" style="margin-top:8px"></div>
        </div>

        <!-- Image -> OCR card -->
        <div class="card">
          <h3 data-i18n="img_tools">Image Tools (OCR)</h3>
          <div class="muted" data-i18n="img_sub">Extract text from images or convert image formats.</div>
          <div style="margin-top:12px" class="file-input">
            <input id="imgFile" type="file" accept="image/*,application/pdf" />
            <select id="imgOutput"><option value="txt">.txt</option><option value="docx">.docx</option><option value="xlsx">.xlsx</option></select>
            <button class="btn" id="imgConvert">Convert</button>
          </div>
          <div id="imgStatus" class="small muted" style="margin-top:8px"></div>
        </div>

        <!-- Image resize / passport -->
        <div class="card">
          <h3 data-i18n="resize_tools">Image Resize & Passport</h3>
          <div class="muted" data-i18n="resize_sub">Resize, compress, and crop to passport sizes.</div>
          <div style="margin-top:12px" class="file-input">
            <input id="resizeFile" type="file" accept="image/*" />
            <select id="passportPreset"><option value="none">None</option><option value="uk">UK Passport</option><option value="us">US Passport</option><option value="pak">Pakistan Passport</option><option value="ind">India Passport</option></select>
            <button class="btn" id="resizeConvert">Process</button>
          </div>
          <div id="resizeStatus" class="small muted" style="margin-top:8px"></div>
        </div>

        <!-- Any -> PDF -->
        <div class="card">
          <h3 data-i18n="any_tools">Any â†’ PDF</h3>
          <div class="muted" data-i18n="any_sub">Convert Word, Excel, images, or text to PDF.</div>
          <div style="margin-top:12px" class="file-input">
            <input id="anyFile" type="file" />
            <button class="btn" id="anyConvert">Convert</button>
          </div>
          <div id="anyStatus" class="small muted" style="margin-top:8px"></div>
        </div>

      </div>

      <div style="margin-top:22px;display:flex;gap:10px;align-items:center">
        <button id="changeLangBtn" class="btn-ghost">Change Language</button>
        <a id="downloadHint" class="small muted">After a successful conversion, a "Download Result" button will appear.</a>
        <button id="openPricing" class="btn" style="margin-left:auto">Upgrade / Pricing</button>
      </div>

      <!-- Free-file quick access (3 free) -->
      <div style="margin-top:18px" class="card">
        <h3>Free conversions (3 per day)</h3>
        <div class="small muted">Use the three free conversion slots below. Clicking any opens a file chooser for that free slot.</div>
        <div style="margin-top:10px;display:flex;gap:8px;flex-wrap:wrap">
          <button class="btn" id="freeBtn1">Free File 1</button>
          <button class="btn" id="freeBtn2">Free File 2</button>
          <button class="btn" id="freeBtn3">Free File 3</button>
        </div>
      </div>

    </section>

    <!-- Privacy page -->
    <section id="privacy" class="hidden card" style="margin-top:18px">
      <h2>Privacy Policy</h2>
      <p>This Privacy Policy explains how <strong>Kashif Ilyas Limited</strong> ("we", "our") handles files and personal data uploaded to Global File Converter.</p>
      <h4>Company</h4>
      <p>Kashif Ilyas Limited â€” Registered Address: 128 City Road, London, EC1V 2NX, United Kingdom. Company Number: 16783493.</p>
      <h4>File handling</h4>
      <p>Uploaded files are stored temporarily for processing. Files are deleted automatically according to the retention policy; we recommend not uploading sensitive personal data. We use virus scanning and secure storage when available.</p>
      <h4>Cookies & Analytics</h4>
      <p>We use cookies for session management and analytics. We comply with GDPR data subject requests â€” contact us at mkkilyas1@gmail.com.</p>

      <hr style="margin:14px 0" />
      <div class="small muted">
        Pricing summary (shown here for transparency):
        <ul>
          <li>Monthly: <strong>$9.99 / month</strong>.</li>
          <li>3-month plan: <strong>10% discount</strong> (applies to the total 3-month charge).</li>
          <li>6-month plan: <strong>18% discount</strong> (applies to the total 6-month charge).</li>
          <li>1-year plan: <strong>27% discount</strong> (applies to the total 12-month charge).</li>
        </ul>
        Registered address: <strong>128 City Road, London, EC1V 2NX, United Kingdom</strong>.
      </div>
    </section>

    <!-- Contact page -->
    <section id="contact" class="hidden card" style="margin-top:18px">
      <h2>Contact</h2>
      <p>Email: <a href="mailto:mkkilyas1@gmail.com">mkkilyas1@gmail.com</a></p>
      <p>WhatsApp: +92 321 9412586</p>
      <p>Address: 128 City Road, London, EC1V 2NX, United Kingdom</p>
    </section>

  </main>

  <footer>
    <div style="max-width:1100px;margin:0 auto;display:flex;justify-content:space-between;align-items:center">
      <div>Â© 2025 Kashif Ilyas Limited</div>
      <div class="small">Built for file conversion. <a href="#/privacy" class="small" style="color:var(--primary);text-decoration:none">Privacy Policy</a></div>
    </div>
  </footer>

  <a id="globalDownloadBtn">Download Result</a>

  <!-- Pricing modal (overlay) -->
  <div class="overlay" id="pricingOverlay" aria-hidden="true">
    <div class="modal-card" role="dialog" aria-modal="true" id="pricingCard">
      <button id="closePricing" style="float:right;background:none;border:none;font-size:20px;cursor:pointer;color:var(--muted)">&times;</button>
      <h3>Upgrade to Premium</h3>
      <p class="small">Unlimited conversions, priority processing, no limits. Choose a billing option below.</p>

      <div class="pricing-row">
        <div class="pricing-card">
          <strong>Monthly</strong>
          <div style="font-size:18px;margin-top:8px">$9.99 / month</div>
          <div class="small" style="margin-top:6px">Billed monthly. Cancel anytime.</div>
          <button class="btn" style="margin-top:10px" id="monthlyPay">Pay Monthly</button>
        </div>

        <div class="pricing-card">
          <strong>3 months</strong>
          <div style="font-size:18px;margin-top:8px"><span class="strike">$29.97</span></div>
          <div style="font-size:18px;margin-top:6px">$26.97 (10% off)</div>
          <div class="small" style="margin-top:6px">Billed every 3 months.</div>
          <button class="btn" style="margin-top:10px" id="qtrPay">Pay 3 months</button>
        </div>
      </div>

      <div class="pricing-row" style="margin-top:12px">
        <div class="pricing-card">
          <strong>6 months</strong>
          <div style="font-size:18px;margin-top:8px"><span class="strike">$59.94</span></div>
          <div style="font-size:18px;margin-top:6px">$49.15 (18% off)</div>
          <div class="small" style="margin-top:6px">Billed every 6 months.</div>
          <button class="btn" style="margin-top:10px" id="sixPay">Pay 6 months</button>
        </div>

        <div class="pricing-card">
          <strong>1 year</strong>
          <div style="font-size:18px;margin-top:8px"><span class="strike">$119.88</span></div>
          <div style="font-size:18px;margin-top:6px">$87.58 (27% off)</div>
          <div class="small" style="margin-top:6px">Billed yearly â€” best value.</div>
          <button class="btn" style="margin-top:10px" id="yearPay">Pay Yearly</button>
        </div>
      </div>

      <div style="text-align:right;margin-top:14px">
        <button id="closePricingBottom" class="btn-ghost">Close</button>
      </div>
    </div>
  </div>

  <!-- Simple hidden file inputs used by free-file buttons -->
  <input type="file" id="freeFileInput1" class="hidden" />
  <input type="file" id="freeFileInput2" class="hidden" />
  <input type="file" id="freeFileInput3" class="hidden" />

  <script>
    // --- Translations & language list ---
    const TRANSLATIONS = {
      en: {
        splash_title: 'Welcome to Global File Converter',
        splash_sub: 'Select your language below to start converting files. Free: 3 files/day.',
        start_btn: 'Select Language & Start',
        popular_tools: 'Popular tools',
        dashboard_title: 'Convert files â€” pick a tool',
        pdf_tools: 'PDF Tools',
        pdf_sub: 'Convert PDF to Word, Excel, Text, and more.',
        img_tools: 'Image Tools (OCR)',
        img_sub: 'Extract text from images or convert image formats.',
        resize_tools: 'Image Resize & Passport',
        resize_sub: 'Resize, compress, and crop to passport sizes.',
        any_tools: 'Any â†’ PDF',
        any_sub: 'Convert Word, Excel, images, or text to PDF.'
      },
      ur: {
        splash_title: 'Ú¯Ù„ÙˆØ¨Ù„ ÙØ§Ø¦Ù„ Ú©Ù†ÙˆØ±Ù¹Ø± Ù…ÛŒÚº Ø®ÙˆØ´ Ø¢Ù…Ø¯ÛŒØ¯',
        splash_sub: 'ÙØ§Ø¦Ù„ÛŒÚº ØªØ¨Ø¯ÛŒÙ„ Ú©Ø±Ù†Û’ Ú©Û’ Ù„ÛŒÛ’ Ø§Ù¾Ù†ÛŒ Ø²Ø¨Ø§Ù† Ù…Ù†ØªØ®Ø¨ Ú©Ø±ÛŒÚºÛ” Ù…ÙØª: ÛŒÙˆÙ…ÛŒÛ 3 ÙØ§Ø¦Ù„ÛŒÚºÛ”',
        start_btn: 'Ø²Ø¨Ø§Ù† Ù…Ù†ØªØ®Ø¨ Ú©Ø±ÛŒÚº Ø§ÙˆØ± Ø´Ø±ÙˆØ¹ Ú©Ø±ÛŒÚº',
        popular_tools: 'Ù…Ù‚Ø¨ÙˆÙ„ Ù¹ÙˆÙ„Ø²',
        dashboard_title: 'ÙØ§Ø¦Ù„ÛŒÚº ØªØ¨Ø¯ÛŒÙ„ Ú©Ø±ÛŒÚº â€” Ø§ÛŒÚ© Ù¹ÙˆÙ„ Ù…Ù†ØªØ®Ø¨ Ú©Ø±ÛŒÚº',
        pdf_tools: 'Ù¾ÛŒ ÚˆÛŒ Ø§ÛŒÙ Ù¹ÙˆÙ„Ø²',
        pdf_sub: 'PDF Ú©Ùˆ WordØŒ ExcelØŒ Text Ø§ÙˆØ± Ù…Ø²ÛŒØ¯ Ù…ÛŒÚº ØªØ¨Ø¯ÛŒÙ„ Ú©Ø±ÛŒÚºÛ”',
        img_tools: 'Ø§Ù…ÛŒØ¬ Ù¹ÙˆÙ„Ø² (OCR)',
        img_sub: 'ØªØµØ§ÙˆÛŒØ± Ø³Û’ Ù…ØªÙ† Ù†Ú©Ø§Ù„ÛŒÚº ÛŒØ§ ØªØµÙˆÛŒØ±ÛŒ ÙØ§Ø±Ù…ÛŒÙ¹Ø³ ØªØ¨Ø¯ÛŒÙ„ Ú©Ø±ÛŒÚºÛ”',
        resize_tools: 'Ø§Ù…ÛŒØ¬ Ø±ÛŒ Ø³Ø§Ø¦Ø² Ø§ÙˆØ± Ù¾Ø§Ø³Ù¾ÙˆØ±Ù¹',
        resize_sub: 'Ø±ÛŒ Ø³Ø§Ø¦Ø²ØŒ Ú©Ù…Ù¾Ø±ÛŒØ³ Ø§ÙˆØ± Ù¾Ø§Ø³Ù¾ÙˆØ±Ù¹ Ø³Ø§Ø¦Ø² Ù…ÛŒÚº Ú©Ø±Ø§Ù¾ Ú©Ø±ÛŒÚºÛ”',
        any_tools: 'Ú©Ø³ÛŒ Ø¨Ú¾ÛŒ Ú†ÛŒØ² Ú©Ùˆ PDF Ù…ÛŒÚº ØªØ¨Ø¯ÛŒÙ„ Ú©Ø±ÛŒÚº',
        any_sub: 'WordØŒ ExcelØŒ ØªØµØ§ÙˆÛŒØ± ÛŒØ§ Ù…ØªÙ† Ú©Ùˆ PDF Ù…ÛŒÚº ØªØ¨Ø¯ÛŒÙ„ Ú©Ø±ÛŒÚºÛ”'
      },
      pa: {
        splash_title: 'à¨—à¨²à©‹à¨¬à¨² à¨«à¨¼à¨¾à¨‡à¨² à¨•à¨¨à¨µà¨°à¨Ÿà¨° à¨µà¨¿à©±à¨š à¨¸à¨µà¨¾à¨—à¨¤ à¨¹à©ˆ',
        splash_sub: 'à¨«à¨¾à¨ˆà¨²à¨¾à¨‚ à¨¬à¨¦à¨²à¨£ à¨²à¨ˆ à¨†à¨ªà¨£à©€ à¨­à¨¾à¨¸à¨¼à¨¾ à¨šà©à¨£à©‹Û” à¨®à©à¨«à¨¼à¨¤: 3 à¨«à¨¾à¨ˆà¨²à¨¾à¨‚/à¨¦à¨¿à¨¨à¥¤',
        start_btn: 'à¨­à¨¾à¨¸à¨¼à¨¾ à¨šà©à¨£à©‹ à¨…à¨¤à©‡ à¨¸à¨¼à©à¨°à©‚ à¨•à¨°à©‹',
        popular_tools: 'à¨ªà¨¸à©°à¨¦à©€à¨¦à¨¾ à¨Ÿà©‚à¨²',
        dashboard_title: 'à¨«à¨¾à¨ˆà¨²à¨¾à¨‚ à¨¬à¨¦à¨²à©‹ â€” à¨•à©‹à¨ˆ à¨Ÿà©‚à¨² à¨šà©à¨£à©‹',
        pdf_tools: 'PDF à¨Ÿà©‚à¨²',
        pdf_sub: 'PDF à¨¨à©‚à©° Word, Excel, Text à¨…à¨¤à©‡ à¨¹à©‹à¨° à¨µà¨¿à©±à¨š à¨¬à¨¦à¨²à©‹à¥¤',
        img_tools: 'à¨šà¨¿à©±à¨¤à¨° à¨Ÿà©‚à¨² (OCR)',
        img_sub: 'à¨šà¨¿à©±à¨¤à¨°à¨¾à¨‚ à¨¤à©‹à¨‚ à¨²à¨¿à¨–à¨¤ à¨¨à¨¿à¨•à¨¾à¨²à©‹ à¨œà¨¾à¨‚ à¨šà¨¿à©±à¨¤à¨° à¨«à¨¾à¨°à¨®à©ˆà¨Ÿ à¨¬à¨¦à¨²à©‹à¥¤',
        resize_tools: 'à¨šà¨¿à©±à¨¤à¨° à¨°à©€à¨¸à¨¾à¨ˆà¨œà¨¼ à¨…à¨¤à©‡ à¨ªà¨¾à¨¸à¨ªà©‹à¨°à¨Ÿ',
        resize_sub: 'à¨°à©€à¨¸à¨¾à¨ˆà¨œà¨¼, à¨•à©à©°à¤ªà¥à¤°à©ˆà¨¸ à¨…à¨¤à©‡ à¨ªà¨¾à¨¸à¨ªà©‹à¨°à¨Ÿ à¨¸à¨¾à¨ˆà¨œà¨¼ à¨µà¨¿à©±à¨š à¨•à©à¨°à©Œà¨ª à¨•à¨°à©‹à¥¤',
        any_tools: 'à¨•à¨¿à¨¸à©‡ à¨µà©€ à¨¨à©‚à©° PDF à¨µà¨¿à©±à¨š à¨¬à¨¦à¨²à©‹',
        any_sub: 'Word, Excel, à¨šà¨¿à©±à¨¤à¨° à¨œà¨¾à¨‚ à¨Ÿà©ˆà¨•à¨¸à¨Ÿ à¨¨à©‚à©° PDF à¨µà¨¿à©±à¨š à¨¬à¨¦à¨²à©‹à¥¤'
      }
    };

    const LANGS = [
      {code:'en',label:'English',flag:'ðŸ‡¬ðŸ‡§'},
      {code:'zh',label:'Chinese',flag:'ðŸ‡¨ðŸ‡³'},
      {code:'ja',label:'Japanese',flag:'ðŸ‡¯ðŸ‡µ'},
      {code:'ko',label:'Korean',flag:'ðŸ‡°ðŸ‡·'},
      {code:'hi',label:'Hindi',flag:'ðŸ‡®ðŸ‡³'},
      {code:'ur',label:'Urdu',flag:'ðŸ‡µðŸ‡°'},
      {code:'pa',label:'Punjabi',flag:'ðŸ‡®ðŸ‡³'},
      {code:'fr',label:'French',flag:'ðŸ‡«ðŸ‡·'},
      {code:'es',label:'Spanish',flag:'ðŸ‡ªðŸ‡¸'}
    ];

    const langSelect = document.getElementById('langSelect');
    LANGS.forEach(l=>{ const o = document.createElement('option'); o.value = l.code; o.textContent = l.flag + ' ' + l.label; langSelect.appendChild(o); });

    function applyTranslations(code){
      const dict = TRANSLATIONS[code] || TRANSLATIONS['en'];
      document.querySelectorAll('[data-i18n]').forEach(el=>{
        const key = el.getAttribute('data-i18n');
        if(dict[key]) el.textContent = dict[key];
      });
    }

    // default to English
    langSelect.value = 'en';
    applyTranslations('en');

    langSelect.addEventListener('change', (e)=>{
      const code = e.target.value;
      applyTranslations(code);
    });

    // --- simple routing ---
    function showSection(hash){
      document.querySelectorAll('main section').forEach(s=>s.classList.add('hidden'));
      if(!hash || hash === '#/' ){ document.getElementById('splash').classList.remove('hidden'); }
      else if(hash === '#/privacy'){ document.getElementById('privacy').classList.remove('hidden'); }
      else if(hash === '#/contact'){ document.getElementById('contact').classList.remove('hidden'); }
      else if(hash === '#/dashboard'){ document.getElementById('dashboard').classList.remove('hidden'); }
      else { document.getElementById('splash').classList.remove('hidden'); }
    }
    window.addEventListener('hashchange', ()=> showSection(location.hash));
    showSection(location.hash || '#/');

    // --- Usage tracking & free 3 per day ---
    const USAGE_KEY = 'gfc_usage';
    const USAGE_LIMIT = 3;
    function todayStr(){ const d=new Date(); return d.getFullYear()+'-'+(d.getMonth()+1)+'-'+d.getDate(); }
    function getUsage(){ try{ const raw = localStorage.getItem(USAGE_KEY); if(!raw) return {count:0,day:todayStr()}; const obj = JSON.parse(raw); if(obj.day !== todayStr()) return {count:0,day:todayStr()}; return obj;}catch(e){return {count:0,day:todayStr()}} }
    function saveUsage(u){ localStorage.setItem(USAGE_KEY, JSON.stringify(u)); }
    function incrementUsage(){ const u=getUsage(); if(u.day !== todayStr()){u.count=0;u.day=todayStr();} u.count=(u.count||0)+1; saveUsage(u); updateUsageInfo(); return u.count; }
    function freeLimitReached(){ return (getUsage().count||0) >= USAGE_LIMIT; }
    function updateUsageInfo(){ const u=getUsage(); document.getElementById('usageInfo').textContent = (u.count||0) }

    document.getElementById('startBtn').addEventListener('click', ()=>{
      document.getElementById('splash').classList.add('hidden');
      document.getElementById('dashboard').classList.remove('hidden');
      updateUsageInfo();
    });

    document.getElementById('changeLangBtn').addEventListener('click', ()=>{
      document.getElementById('dashboard').classList.add('hidden');
      document.getElementById('splash').classList.remove('hidden');
    });

    // show trial
    document.getElementById('trialBtn').addEventListener('click', ()=>{
      alert('Seven-day trial activated (UI only). To enable real trial tracking, connect payment/auth backend.');
    });

    // --- Pricing modal logic (click outside to close anywhere) ---
    const pricingOverlay = document.getElementById('pricingOverlay');
    const pricingCard = document.getElementById('pricingCard');
    function openPricing(){ pricingOverlay.style.display = 'flex'; pricingOverlay.setAttribute('aria-hidden','false'); }
    function closePricing(){ pricingOverlay.style.display = 'none'; pricingOverlay.setAttribute('aria-hidden','true'); }
    document.getElementById('openPricing').addEventListener('click', openPricing);
    document.getElementById('closePricing').addEventListener('click', closePricing);
    document.getElementById('closePricingBottom').addEventListener('click', closePricing);

    // clicking outside the modal closes it (global "click anywhere revoke price list")
    pricingOverlay.addEventListener('click', (e)=>{
      if(!pricingCard.contains(e.target)) closePricing();
    });

    // wire up fake pay buttons
    document.getElementById('monthlyPay').addEventListener('click', ()=> alert('Checkout path not configured. Integrate Stripe/Pay endpoint to process payments.'));
    document.getElementById('qtrPay').addEventListener('click', ()=> alert('Checkout path not configured. 3-month plan (10% off) â€” integrate backend to charge $26.97.'));
    document.getElementById('sixPay').addEventListener('click', ()=> alert('Checkout path not configured. 6-month plan (18% off) â€” integrate backend to charge $49.15.'));
    document.getElementById('yearPay').addEventListener('click', ()=> alert('Checkout path not configured. Annual plan (27% off) â€” integrate backend to charge $87.58.'));

    // --- Conversion & fallback (client-side placeholder) ---
    function changeExtension(filename, ext){
      const base = filename ? filename.replace(/\.[^/.]+$/, '') : 'converted';
      return base + '.' + ext;
    }

    async function fakeConvertToBlob(file, targetExt){
      if(targetExt === 'txt'){
        const txt = 'Extracted text from ' + (file.name||'file') + '\n\n(placeholder)';
        return new Blob([txt], {type:'text/plain'});
      }
      const arrayBuffer = await file.arrayBuffer();
      const mime = file.type || 'application/octet-stream';
      return new Blob([arrayBuffer], {type: mime});
    }

    async function convertWithFallback(endpoint, fileInput, targetExt, statusEl){
      if(freeLimitReached()){
        openPricing();
        return;
      }
      const f = fileInput.files[0];
      if(!f){ alert('Please choose a file.'); return; }
      statusEl.textContent = 'Uploading...';
      const form = new FormData(); form.append('file', f);
      try{
        const res = await fetch(endpoint, {method:'POST', body: form});
        if(res.ok){
          const blob = await res.blob();
          const filename = changeExtension(f.name, targetExt);
          showDownload(blob, filename);
          statusEl.textContent = 'Conversion completed.';
          incrementUsage();
          return;
        } else {
          console.warn('Server conversion failed, using client fallback');
        }
      }catch(e){
        console.warn('Server call failed, using client fallback', e);
      }

      statusEl.textContent = 'Processing (client)...';
      const blob = await fakeConvertToBlob(f, targetExt);
      const filename = changeExtension(f.name, targetExt);
      showDownload(blob, filename);
      statusEl.textContent = 'Conversion completed (client).';
      incrementUsage();
    }

    function showDownload(blob, filename){
      const btn = document.getElementById('globalDownloadBtn');
      const url = URL.createObjectURL(blob);
      btn.href = url; btn.download = filename; btn.style.display = 'inline-block';
      // open in new tab as a preview
      window.open(url, '_blank');
    }

    // Wire up convert buttons
    document.getElementById('pdfConvert').addEventListener('click', ()=>{
      const out = document.getElementById('pdfOutput').value;
      convertWithFallback('/api/convert/pdf-to-docx', document.getElementById('pdfFile'), out, document.getElementById('pdfStatus'));
    });
    document.getElementById('imgConvert').addEventListener('click', ()=>{
      const out = document.getElementById('imgOutput').value;
      convertWithFallback('/api/convert/image-ocr', document.getElementById('imgFile'), out, document.getElementById('imgStatus'));
    });
    document.getElementById('resizeConvert').addEventListener('click', ()=>{
      convertWithFallback('/api/convert/image-resize', document.getElementById('resizeFile'), 'jpg', document.getElementById('resizeStatus'));
    });
    document.getElementById('anyConvert').addEventListener('click', ()=>{
      convertWithFallback('/api/convert/any-to-pdf', document.getElementById('anyFile'), 'pdf', document.getElementById('anyStatus'));
    });

    // free-file quick buttons (open hidden file inputs)
    const freeBtn1 = document.getElementById('freeBtn1');
    const freeBtn2 = document.getElementById('freeBtn2');
    const freeBtn3 = document.getElementById('freeBtn3');
    const freeInput1 = document.getElementById('freeFileInput1');
    const freeInput2 = document.getElementById('freeFileInput2');
    const freeInput3 = document.getElementById('freeFileInput3');

    function handleFreeInput(input, statusElId, defaultExt='pdf'){
      input.addEventListener('change', async ()=>{
        const f = input.files[0];
        if(!f) return;
        if(freeLimitReached()){ openPricing(); return; }
        const blob = await fakeConvertToBlob(f, defaultExt);
        const filename = changeExtension(f.name, defaultExt);
        showDownload(blob, filename);
        incrementUsage();
        alert('Free conversion used for ' + f.name);
      });
    }
    handleFreeInput(freeInput1, 'pdfStatus');
    handleFreeInput(freeInput2, 'imgStatus');
    handleFreeInput(freeInput3, 'anyStatus');

    freeBtn1.addEventListener('click', ()=> freeInput1.click());
    freeBtn2.addEventListener('click', ()=> freeInput2.click());
    freeBtn3.addEventListener('click', ()=> freeInput3.click());

    // initial usage
    updateUsageInfo();

    // Accessibility: hide pricing modal by default
    pricingOverlay.style.display = 'none';

    // Prevent accidental navigation during conversion - minimal
    window.addEventListener('beforeunload', (e) => {
      // If more advanced conversion state exists, present a confirmation.
      // For now we don't block; this is a placeholder for future backend state.
    });

    // small helper: open pricing on top right nav click
    document.querySelectorAll('[data-nav]').forEach(a=> a.addEventListener('click', (e)=>{
      const href = a.getAttribute('href');
      if(href === '#/privacy' || href === '#/contact' || href === '#/dashboard' || href === '#/'){
        // allow routing
      } else {
        e.preventDefault();
        openPricing();
      }
    }));

    // Ensure main language English is used on load (already set) â€” keep persistent if desired
  </script>
</body>
</html>
<script>
  // === TRIAL SYSTEM ===
  const TRIAL_KEY = 'gfc_trial';
  function startTrial() {
    const now = Date.now();
    const expiry = now + 7 * 24 * 60 * 60 * 1000; // 7 days in ms
    localStorage.setItem(TRIAL_KEY, JSON.stringify({ active: true, started: now, expires: expiry }));
    updateTrialUI();
    alert('7-day trial started! Unlimited conversions unlocked until expiration.');
  }

  function getTrial() {
    try {
      const obj = JSON.parse(localStorage.getItem(TRIAL_KEY));
      if (!obj) return { active: false };
      if (Date.now() > obj.expires) {
        localStorage.removeItem(TRIAL_KEY);
        return { active: false };
      }
      return obj;
    } catch (e) {
      return { active: false };
    }
  }

  function trialDaysLeft(expiry) {
    const diff = expiry - Date.now();
    return Math.ceil(diff / (1000 * 60 * 60 * 24));
  }

  function updateTrialUI() {
    const infoBarId = 'trialBanner';
    let banner = document.getElementById(infoBarId);
    const trial = getTrial();
    if (trial.active) {
      const days = trialDaysLeft(trial.expires);
      if (!banner) {
        banner = document.createElement('div');
        banner.id = infoBarId;
        banner.style.background = '#10b981';
        banner.style.color = 'white';
        banner.style.padding = '8px';
        banner.style.textAlign = 'center';
        banner.style.fontWeight = '600';
        banner.style.borderRadius = '8px';
        banner.style.marginBottom = '12px';
        document.getElementById('dashboard').prepend(banner);
      }
      banner.textContent = `Trial active â€” ${days} day${days!==1?'s':''} left (Unlimited conversions)`;
      banner.style.display = 'block';
    } else if (banner) {
      banner.remove();
    }
  }

  // override freeLimitReached() if trial active
  const origFreeLimit = freeLimitReached;
  function freeLimitReached() {
    const trial = getTrial();
    if (trial.active) return false;
    return origFreeLimit();
  }

  // handle start button
  document.getElementById('trialBtn').addEventListener('click', startTrial);

  // update trial banner periodically
  setInterval(updateTrialUI, 60 * 1000);
  updateTrialUI();
</script>
