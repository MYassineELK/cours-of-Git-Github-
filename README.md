# cours-of-Git-Github-
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>درس Git & GitHub الكامل</title>
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@400;600&family=Tajawal:wght@300;400;500;700;800&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0d1117;--bg2: #161b22;--bg3: #1c2128;--border: #30363d;
    --green: #3fb950;--green2: #238636;--blue: #58a6ff;--purple: #bc8cff;
    --orange: #ffa657;--red: #f85149;--yellow: #e3b341;
    --text: #e6edf3;--muted: #8b949e;
    --mono: 'IBM Plex Mono', monospace;--body: 'Tajawal', sans-serif;
  }
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body { background: var(--bg); color: var(--text); font-family: var(--body); min-height: 100vh; overflow-x: hidden; }
  body::before { content: ''; position: fixed; inset: 0; background-image: linear-gradient(rgba(48,54,61,0.3) 1px, transparent 1px), linear-gradient(90deg, rgba(48,54,61,0.3) 1px, transparent 1px); background-size: 40px 40px; pointer-events: none; z-index: 0; }
  .header { position: relative; z-index: 1; text-align: center; padding: 60px 20px 40px; border-bottom: 1px solid var(--border); background: linear-gradient(to bottom, rgba(63,185,80,0.05), transparent); }
  .header-badge { display: inline-flex; align-items: center; gap: 8px; background: rgba(63,185,80,0.1); border: 1px solid rgba(63,185,80,0.3); border-radius: 20px; padding: 6px 16px; font-size: 13px; color: var(--green); margin-bottom: 20px; font-family: var(--mono); }
  .header h1 { font-size: clamp(2.5rem, 6vw, 4.5rem); font-weight: 800; line-height: 1.1; margin-bottom: 16px; }
  .header h1 .git { color: var(--orange); } .header h1 .hub { color: var(--blue); }
  .header p { font-size: 1.1rem; color: var(--muted); max-width: 600px; margin: 0 auto 30px; line-height: 1.8; }
  .nav { position: sticky; top: 0; z-index: 100; background: rgba(13,17,23,0.95); backdrop-filter: blur(12px); border-bottom: 1px solid var(--border); padding: 0 20px; display: flex; justify-content: center; gap: 4px; overflow-x: auto; }
  .nav-btn { padding: 12px 18px; background: none; border: none; color: var(--muted); font-family: var(--body); font-size: 14px; cursor: pointer; white-space: nowrap; border-bottom: 2px solid transparent; transition: all 0.2s; }
  .nav-btn:hover { color: var(--text); } .nav-btn.active { color: var(--green); border-bottom-color: var(--green); }
  .container { position: relative; z-index: 1; max-width: 900px; margin: 0 auto; padding: 40px 20px 80px; }
  .section { display: none; } .section.active { display: block; animation: fadeIn 0.3s ease; }
  @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
  .section-title { font-size: 1.8rem; font-weight: 700; margin-bottom: 8px; display: flex; align-items: center; gap: 12px; }
  .section-subtitle { color: var(--muted); margin-bottom: 32px; font-size: 1rem; line-height: 1.7; }
  .card { background: var(--bg2); border: 1px solid var(--border); border-radius: 12px; padding: 24px; margin-bottom: 20px; transition: border-color 0.2s; }
  .card:hover { border-color: var(--green); }
  .card-title { font-size: 1.1rem; font-weight: 700; margin-bottom: 10px; display: flex; align-items: center; gap: 8px; }
  .card p { color: var(--muted); line-height: 1.8; font-size: 0.95rem; }
  .code-block { background: var(--bg3); border: 1px solid var(--border); border-radius: 10px; margin: 16px 0; overflow: hidden; direction: ltr; }
  .code-header { background: var(--bg2); border-bottom: 1px solid var(--border); padding: 10px 16px; display: flex; justify-content: space-between; align-items: center; font-family: var(--mono); font-size: 12px; color: var(--muted); }
  .code-header .dots { display: flex; gap: 6px; }
  .code-header .dot { width: 10px; height: 10px; border-radius: 50%; }
  .dot-r { background: #ff5f56; } .dot-y { background: #ffbd2e; } .dot-g { background: #27c93f; }
  .code-body { padding: 20px; font-family: var(--mono); font-size: 0.85rem; line-height: 1.8; overflow-x: auto; }
  .code-body .cmd { color: var(--green); } .code-body .comment { color: var(--muted); }
  .code-body .arg { color: var(--blue); } .code-body .flag { color: var(--orange); }
  .code-body .str { color: var(--yellow); } .code-body .out { color: var(--purple); }
  .copy-btn { background: rgba(88,166,255,0.1); border: 1px solid rgba(88,166,255,0.2); color: var(--blue); border-radius: 6px; padding: 4px 10px; font-size: 11px; cursor: pointer; font-family: var(--mono); transition: all 0.2s; }
  .copy-btn:hover { background: rgba(88,166,255,0.2); }
  .info-box { border-radius: 10px; padding: 16px 20px; margin: 16px 0; display: flex; gap: 12px; font-size: 0.9rem; line-height: 1.7; }
  .info-box.tip { background: rgba(63,185,80,0.08); border: 1px solid rgba(63,185,80,0.2); }
  .info-box.warn { background: rgba(227,179,65,0.08); border: 1px solid rgba(227,179,65,0.2); }
  .info-box.note { background: rgba(88,166,255,0.08); border: 1px solid rgba(88,166,255,0.2); }
  .info-icon { font-size: 1.2rem; flex-shrink: 0; margin-top: 2px; }
  .steps { counter-reset: step; }
  .step { display: flex; gap: 20px; margin-bottom: 28px; position: relative; }
  .step::before { content: ''; position: absolute; right: 19px; top: 40px; bottom: -28px; width: 1px; background: var(--border); }
  .step:last-child::before { display: none; }
  .step-num { width: 40px; height: 40px; border-radius: 50%; background: var(--bg2); border: 2px solid var(--green); display: flex; align-items: center; justify-content: center; font-family: var(--mono); font-size: 14px; color: var(--green); flex-shrink: 0; }
  .step-content { flex: 1; padding-top: 8px; }
  .step-content h3 { font-size: 1rem; margin-bottom: 6px; }
  .step-content p { color: var(--muted); font-size: 0.9rem; line-height: 1.7; }
  .flow-diagram { background: var(--bg2); border: 1px solid var(--border); border-radius: 12px; padding: 30px; margin: 24px 0; overflow-x: auto; }
  .flow-row { display: flex; align-items: center; gap: 8px; margin-bottom: 16px; direction: ltr; flex-wrap: wrap; justify-content: center; }
  .flow-box { padding: 8px 16px; border-radius: 8px; font-family: var(--mono); font-size: 12px; white-space: nowrap; text-align: center; min-width: 110px; }
  .flow-box.work { background: rgba(255,166,87,0.15); border: 1px solid rgba(255,166,87,0.4); color: var(--orange); }
  .flow-box.stage { background: rgba(227,179,65,0.15); border: 1px solid rgba(227,179,65,0.4); color: var(--yellow); }
  .flow-box.local { background: rgba(63,185,80,0.15); border: 1px solid rgba(63,185,80,0.4); color: var(--green); }
  .flow-box.remote { background: rgba(88,166,255,0.15); border: 1px solid rgba(88,166,255,0.4); color: var(--blue); }
  .flow-arrow { color: var(--muted); font-size: 1.2rem; flex-shrink: 0; }
  .flow-label { font-family: var(--mono); font-size: 11px; color: var(--green); padding: 3px 8px; background: rgba(63,185,80,0.08); border-radius: 4px; white-space: nowrap; }
  .cmd-table { width: 100%; border-collapse: collapse; margin: 16px 0; font-size: 0.88rem; }
  .cmd-table th { background: var(--bg3); padding: 12px 16px; text-align: right; font-weight: 600; border-bottom: 1px solid var(--border); color: var(--muted); }
  .cmd-table td { padding: 12px 16px; border-bottom: 1px solid rgba(48,54,61,0.5); vertical-align: middle; }
  .cmd-table tr:hover td { background: rgba(255,255,255,0.02); }
  .cmd-table td:first-child { font-family: var(--mono); color: var(--green); direction: ltr; text-align: left; }
  .cmd-table td:last-child { color: var(--muted); }
  .branch-visual { background: var(--bg2); border: 1px solid var(--border); border-radius: 12px; padding: 24px; margin: 20px 0; direction: ltr; overflow-x: auto; }
  .commit { width: 18px; height: 18px; border-radius: 50%; border: 2px solid; flex-shrink: 0; display:inline-block; }
  .commit.main { border-color: var(--green); background: rgba(63,185,80,0.3); }
  .commit.feature { border-color: var(--blue); background: rgba(88,166,255,0.3); }
  .commit.merge { border-color: var(--purple); background: rgba(188,140,255,0.3); }
  .branch-tag { font-size: 11px; padding: 2px 8px; border-radius: 4px; margin-right: 8px; font-family: var(--mono); }
  .tag-main { background: rgba(63,185,80,0.15); color: var(--green); }
  .tag-feature { background: rgba(88,166,255,0.15); color: var(--blue); }
  .quiz-card { background: var(--bg2); border: 1px solid var(--border); border-radius: 12px; padding: 24px; margin-bottom: 20px; }
  .quiz-q { font-size: 1rem; font-weight: 600; margin-bottom: 16px; line-height: 1.6; }
  .quiz-opts { display: grid; gap: 10px; }
  .quiz-opt { padding: 12px 16px; background: var(--bg3); border: 1px solid var(--border); border-radius: 8px; cursor: pointer; font-size: 0.9rem; text-align: right; transition: all 0.2s; font-family: var(--body); color: var(--text); width: 100%; }
  .quiz-opt:hover { border-color: var(--blue); }
  .quiz-opt.correct { background: rgba(63,185,80,0.1); border-color: var(--green); color: var(--green); }
  .quiz-opt.wrong { background: rgba(248,81,73,0.1); border-color: var(--red); color: var(--red); }
  .quiz-feedback { margin-top: 12px; padding: 10px 14px; border-radius: 8px; font-size: 0.88rem; display: none; }
  .quiz-feedback.show { display: block; }
  .quiz-feedback.ok { background: rgba(63,185,80,0.1); color: var(--green); }
  .quiz-feedback.fail { background: rgba(248,81,73,0.1); color: var(--red); }
  .score-board { text-align: center; padding: 30px; background: var(--bg2); border: 1px solid var(--border); border-radius: 12px; margin-top: 24px; }
  .score-num { font-size: 3rem; font-weight: 800; font-family: var(--mono); color: var(--green); }
  .progress-bar-wrap { background: var(--bg3); height: 6px; border-radius: 3px; margin: 8px 0 4px; overflow: hidden; }
  .progress-bar { height: 100%; background: linear-gradient(90deg, var(--green), var(--blue)); border-radius: 3px; transition: width 0.5s ease; }
  @media(max-width: 600px) { .header h1 { font-size: 2rem; } .cmd-table { font-size: 0.78rem; } }
</style>
</head>
<body>
<div class="header">
  <div class="header-badge"><span>🎓</span><span>دورة تعليمية كاملة</span></div>
  <h1><span class="git">Git</span> <span style="color:var(--muted)">&</span> <span class="hub">GitHub</span></h1>
  <p>من الصفر إلى الاحتراف — تحكم في الكود، تعاون مع الفريق، ونشر مشاريعك بثقة</p>
</div>
<nav class="nav">
  <button class="nav-btn active" onclick="showSection('intro')">١ · المقدمة</button>
  <button class="nav-btn" onclick="showSection('setup')">٢ · الإعداد</button>
  <button class="nav-btn" onclick="showSection('basics')">٣ · الأساسيات</button>
  <button class="nav-btn" onclick="showSection('branches')">٤ · الفروع</button>
  <button class="nav-btn" onclick="showSection('github')">٥ · GitHub</button>
  <button class="nav-btn" onclick="showSection('collab')">٦ · التعاون</button>
  <button class="nav-btn" onclick="showSection('quiz')">٧ · اختبر نفسك</button>
</nav>
<div class="container">

<!-- INTRO -->
<div class="section active" id="intro">
  <div class="section-title">🌱 ما هو Git؟</div>
  <p class="section-subtitle">Git هو نظام التحكم في الإصدارات (Version Control System) الأشهر في العالم. يمكّنك من تتبع تغييرات الكود مع الزمن والرجوع لأي نقطة سابقة.</p>
  <div class="card"><div class="card-title">🤔 لماذا نحتاج Git؟</div><p>تخيل أنك تعمل على مشروع وقمت بتعديل خاطئ حذف كل شيء — بدون Git أنت في ورطة! مع Git يمكنك الرجوع لأي نقطة سابقة بأمر واحد فقط.</p></div>
  <div class="card"><div class="card-title">🌐 وما هو GitHub؟</div><p>GitHub هو منصة استضافة للمشاريع المبنية بـ Git. يتيح لك حفظ كودك على السحابة، التعاون مع فريق، ونشر مشاريعك للعالم. فكّر فيه كـ "Facebook للمطورين".</p></div>
  <div style="background:var(--bg2);border:1px solid var(--border);border-radius:12px;padding:24px;margin:20px 0;">
    <div style="font-size:1rem;font-weight:700;margin-bottom:20px;color:var(--muted);">الفرق بين Git و GitHub</div>
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:16px;">
      <div style="background:rgba(255,166,87,0.08);border:1px solid rgba(255,166,87,0.2);border-radius:10px;padding:20px;text-align:center;">
        <div style="font-size:2rem;margin-bottom:8px;">🔧</div>
        <div style="font-size:1.1rem;font-weight:700;color:var(--orange);margin-bottom:8px;">Git</div>
        <div style="font-size:0.85rem;color:var(--muted);line-height:1.7;">برنامج مثبت على جهازك<br>يعمل بدون إنترنت<br>يتتبع تاريخ الكود محلياً</div>
      </div>
      <div style="background:rgba(88,166,255,0.08);border:1px solid rgba(88,166,255,0.2);border-radius:10px;padding:20px;text-align:center;">
        <div style="font-size:2rem;margin-bottom:8px;">☁️</div>
        <div style="font-size:1.1rem;font-weight:700;color:var(--blue);margin-bottom:8px;">GitHub</div>
        <div style="font-size:0.85rem;color:var(--muted);line-height:1.7;">موقع ويب على الإنترنت<br>يستضيف مشاريع Git<br>للتعاون والنشر</div>
      </div>
    </div>
  </div>
  <div class="info-box tip"><div class="info-icon">💡</div><div><strong>تشبيه مفيد:</strong> Git مثل تاريخ الحفظ في لعبة فيديو — يمكنك الرجوع لأي نقطة. GitHub مثل السحابة التي تحفظ هذا التاريخ وتشاركه مع أصدقائك.</div></div>
  <div class="card">
    <div class="card-title">📚 المفاهيم الأساسية</div>
    <table class="cmd-table" style="margin:12px 0 0;">
      <tr><th>المصطلح</th><th>المعنى</th></tr>
      <tr><td>Repository (Repo)</td><td>مجلد المشروع المُتتبَّع بـ Git</td></tr>
      <tr><td>Commit</td><td>لقطة محفوظة من الكود في لحظة معينة</td></tr>
      <tr><td>Branch</td><td>فرع منفصل للعمل دون التأثير على الكود الرئيسي</td></tr>
      <tr><td>Merge</td><td>دمج فرع مع فرع آخر</td></tr>
      <tr><td>Clone</td><td>نسخ مستودع كامل من GitHub</td></tr>
      <tr><td>Push</td><td>رفع التغييرات من جهازك إلى GitHub</td></tr>
      <tr><td>Pull</td><td>جلب التغييرات من GitHub إلى جهازك</td></tr>
    </table>
  </div>
  <div style="text-align:center;margin-top:28px;"><button onclick="showSection('setup')" style="background:var(--green2);border:none;color:white;padding:14px 32px;border-radius:8px;font-size:1rem;cursor:pointer;font-family:var(--body);font-weight:600;">التالي: الإعداد ←</button></div>
</div>

<!-- SETUP -->
<div class="section" id="setup">
  <div class="section-title">⚙️ الإعداد والتثبيت</div>
  <p class="section-subtitle">قبل استخدام Git، نحتاج لتثبيته وإعداده بمعلوماتنا الشخصية.</p>
  <div class="steps">
    <div class="step">
      <div class="step-num">1</div>
      <div class="step-content">
        <h3>تثبيت Git</h3>
        <p>قم بتحميل Git من الموقع الرسمي وتثبيته حسب نظام تشغيلك:</p>
        <div class="code-block" style="margin-top:12px;">
          <div class="code-header"><div class="dots"><div class="dot dot-r"></div><div class="dot dot-y"></div><div class="dot dot-g"></div></div><span>Terminal</span><button class="copy-btn" onclick="copyCode(this)">نسخ</button></div>
          <div class="code-body"><span class="comment"># Windows → حمّل من: https://git-scm.com</span>

<span class="comment"># macOS</span>
<span class="cmd">brew install git</span>

<span class="comment"># Ubuntu / Debian</span>
<span class="cmd">sudo apt install git</span>

<span class="comment"># التحقق من التثبيت</span>
<span class="cmd">git</span> <span class="flag">--version</span>
<span class="out">git version 2.43.0</span></div>
        </div>
      </div>
    </div>
    <div class="step">
      <div class="step-num">2</div>
      <div class="step-content">
        <h3>إعداد الهوية</h3>
        <p>أول شيء نفعله هو إخبار Git من نحن — هذه المعلومات ستظهر في كل Commit:</p>
        <div class="code-block" style="margin-top:12px;">
          <div class="code-header"><div class="dots"><div class="dot dot-r"></div><div class="dot dot-y"></div><div class="dot dot-g"></div></div><span>إعداد المستخدم</span><button class="copy-btn" onclick="copyCode(this)">نسخ</button></div>
          <div class="code-body"><span class="cmd">git config</span> <span class="flag">--global</span> user.name <span class="str">"Yassin"</span>
<span class="cmd">git config</span> <span class="flag">--global</span> user.email <span class="str">"yassin@example.com"</span>
<span class="cmd">git config</span> <span class="flag">--global</span> core.editor <span class="str">"code --wait"</span>
<span class="cmd">git config</span> <span class="flag">--list</span></div>
        </div>
      </div>
    </div>
    <div class="step">
      <div class="step-num">3</div>
      <div class="step-content">
        <h3>إنشاء حساب GitHub</h3>
        <p>توجه إلى <strong style="color:var(--blue);">github.com</strong> وأنشئ حساباً مجانياً باستخدام نفس البريد الإلكتروني.</p>
      </div>
    </div>
    <div class="step">
      <div class="step-num">4</div>
      <div class="step-content">
        <h3>إنشاء أول مستودع محلي</h3>
        <div class="code-block" style="margin-top:12px;">
          <div class="code-header"><div class="dots"><div class="dot dot-r"></div><div class="dot dot-y"></div><div class="dot dot-g"></div></div><span>إنشاء Repo</span><button class="copy-btn" onclick="copyCode(this)">نسخ</button></div>
          <div class="code-body"><span class="cmd">mkdir</span> <span class="arg">my-project</span>
<span class="cmd">cd</span> <span class="arg">my-project</span>
<span class="cmd">git init</span>
<span class="out">Initialized empty Git repository in .../my-project/.git/</span></div>
        </div>
        <div class="info-box note" style="margin-top:12px;"><div class="info-icon">📌</div><div><code style="color:var(--blue);">git init</code> ينشئ مجلداً مخفياً اسمه <code style="color:var(--blue);">.git</code> يحتوي على كل تاريخ المشروع.</div></div>
      </div>
    </div>
  </div>
  <div style="text-align:center;margin-top:28px;"><button onclick="showSection('basics')" style="background:var(--green2);border:none;color:white;padding:14px 32px;border-radius:8px;font-size:1rem;cursor:pointer;font-family:var(--body);font-weight:600;">التالي: الأوامر الأساسية ←</button></div>
</div>

<!-- BASICS -->
<div class="section" id="basics">
  <div class="section-title">📦 الأوامر الأساسية</div>
  <p class="section-subtitle">هذه الأوامر هي التي ستستخدمها يومياً في كل مشروع. تعلّمها جيداً!</p>
  <div class="flow-diagram">
    <div style="color:var(--muted);font-size:13px;margin-bottom:16px;text-align:center;">دورة حياة الملف في Git</div>
    <div class="flow-row">
      <div class="flow-box work">Working Directory<br><small>ملفاتك المحلية</small></div>
      <div style="display:flex;flex-direction:column;align-items:center;gap:4px;"><div class="flow-label">git add</div><div class="flow-arrow">→</div></div>
      <div class="flow-box stage">Staging Area<br><small>منطقة التجهيز</small></div>
      <div style="display:flex;flex-direction:column;align-items:center;gap:4px;"><div class="flow-label">git commit</div><div class="flow-arrow">→</div></div>
      <div class="flow-box local">Local Repo<br><small>المستودع المحلي</small></div>
      <div style="display:flex;flex-direction:column;align-items:center;gap:4px;"><div class="flow-label">git push</div><div class="flow-arrow">→</div></div>
      <div class="flow-box remote">GitHub<br><small>المستودع البعيد</small></div>
    </div>
  </div>
  <div class="code-block">
    <div class="code-header"><div class="dots"><div class="dot dot-r"></div><div class="dot dot-y"></div><div class="dot dot-g"></div></div><span>سيناريو كامل من البداية للنهاية</span><button class="copy-btn" onclick="copyCode(this)">نسخ</button></div>
    <div class="code-body"><span class="comment"># ١. إنشاء ملف جديد</span>
<span class="cmd">echo</span> <span class="str">"Hello World"</span> > index.html

<span class="comment"># ٢. فحص حالة المستودع</span>
<span class="cmd">git status</span>
<span class="out">Untracked files: index.html</span>

<span class="comment"># ٣. إضافة ملف لمنطقة التجهيز</span>
<span class="cmd">git add</span> <span class="arg">index.html</span>
<span class="comment"># أو لإضافة كل الملفات:</span>
<span class="cmd">git add</span> <span class="flag">.</span>

<span class="comment"># ٤. حفظ التغييرات (Commit)</span>
<span class="cmd">git commit</span> <span class="flag">-m</span> <span class="str">"إضافة الصفحة الرئيسية"</span>
<span class="out">[main (root-commit) a1b2c3d] إضافة الصفحة الرئيسية</span>

<span class="comment"># ٥. عرض تاريخ الـ Commits</span>
<span class="cmd">git log</span> <span class="flag">--oneline</span>
<span class="out">a1b2c3d إضافة الصفحة الرئيسية</span></div>
  </div>
  <div class="info-box tip"><div class="info-icon">✏️</div><div><strong>رسائل Commit جيدة:</strong> مثال جيد: <code style="color:var(--green);">"إضافة نموذج تسجيل الدخول"</code> — مثال سيء: <code style="color:var(--red);">"تعديلات"</code></div></div>
  <div class="card">
    <div class="card-title">🔍 أوامر مفيدة أخرى</div>
    <div class="code-block" style="margin-top:12px;">
      <div class="code-header"><div class="dots"><div class="dot dot-r"></div><div class="dot dot-y"></div><div class="dot dot-g"></div></div><span>أوامر الفحص</span><button class="copy-btn" onclick="copyCode(this)">نسخ</button></div>
      <div class="code-body"><span class="comment"># حالة المستودع</span>
<span class="cmd">git status</span>

<span class="comment"># عرض التغييرات قبل الإضافة</span>
<span class="cmd">git diff</span>

<span class="comment"># عرض تاريخ مختصر وبياني</span>
<span class="cmd">git log</span> <span class="flag">--oneline --graph</span>

<span class="comment"># التراجع عن تغيير غير محفوظ</span>
<span class="cmd">git restore</span> <span class="arg">index.html</span></div>
    </div>
  </div>
  <div class="card">
    <div class="card-title">🚫 ملف .gitignore</div>
    <p style="margin-bottom:12px;">يستخدم لإخبار Git بتجاهل ملفات معينة كملفات كلمات المرور وملفات النظام</p>
    <div class="code-block">
      <div class="code-header"><div class="dots"><div class="dot dot-r"></div><div class="dot dot-y"></div><div class="dot dot-g"></div></div><span>.gitignore</span><button class="copy-btn" onclick="copyCode(this)">نسخ</button></div>
      <div class="code-body"><span class="str">vendor/</span>
<span class="str">.env</span>
<span class="str">.DS_Store</span>
<span class="str">*.log</span></div>
    </div>
  </div>
  <div style="text-align:center;margin-top:28px;"><button onclick="showSection('branches')" style="background:var(--green2);border:none;color:white;padding:14px 32px;border-radius:8px;font-size:1rem;cursor:pointer;font-family:var(--body);font-weight:600;">التالي: الفروع ←</button></div>
</div>

<!-- BRANCHES -->
<div class="section" id="branches">
  <div class="section-title">🌿 الفروع (Branches)</div>
  <p class="section-subtitle">الفروع هي من أقوى ميزات Git. تتيح لك تجربة أفكار جديدة دون المساس بالكود الرئيسي.</p>
  <div class="branch-visual">
    <div style="color:var(--muted);font-size:12px;margin-bottom:20px;">مثال على الفروع — تطوير ميزة جديدة بشكل منفصل</div>
    <div style="font-family:var(--mono);font-size:13px;line-height:2.5;">
      <div style="display:flex;align-items:center;gap:6px;margin-bottom:4px;">
        <span class="commit main"></span>
        <span style="display:inline-block;width:40px;height:2px;background:var(--green);"></span>
        <span class="commit main"></span>
        <span style="display:inline-block;width:40px;height:2px;background:var(--green);"></span>
        <span class="commit main"></span>
        <span style="display:inline-block;width:40px;height:2px;background:var(--green);"></span>
        <span class="commit merge"></span>
        <span style="display:inline-block;width:40px;height:2px;background:var(--green);"></span>
        <span class="commit main"></span>
        <span class="branch-tag tag-main" style="margin-right:12px;">main</span>
      </div>
      <div style="display:flex;align-items:center;gap:6px;margin-right:94px;">
        <span class="commit feature"></span>
        <span style="display:inline-block;width:40px;height:2px;background:var(--blue);"></span>
        <span class="commit feature"></span>
        <span style="display:inline-block;width:40px;height:2px;background:var(--blue);"></span>
        <span class="commit feature"></span>
        <span class="branch-tag tag-feature" style="margin-right:12px;">feature/login</span>
      </div>
    </div>
  </div>
  <div class="code-block">
    <div class="code-header"><div class="dots"><div class="dot dot-r"></div><div class="dot dot-y"></div><div class="dot dot-g"></div></div><span>أوامر الفروع</span><button class="copy-btn" onclick="copyCode(this)">نسخ</button></div>
    <div class="code-body"><span class="comment"># عرض كل الفروع</span>
<span class="cmd">git branch</span>

<span class="comment"># إنشاء فرع والانتقال إليه مباشرة</span>
<span class="cmd">git checkout</span> <span class="flag">-b</span> <span class="arg">feature/login</span>

<span class="comment"># الرجوع للفرع الرئيسي</span>
<span class="cmd">git checkout</span> <span class="arg">main</span>

<span class="comment"># دمج الفرع مع main</span>
<span class="cmd">git merge</span> <span class="arg">feature/login</span>
<span class="out">Merge made by the 'ort' strategy.</span>

<span class="comment"># حذف الفرع بعد الدمج</span>
<span class="cmd">git branch</span> <span class="flag">-d</span> <span class="arg">feature/login</span></div>
  </div>
  <div class="info-box warn"><div class="info-icon">⚠️</div><div><strong>تعارض الدمج (Merge Conflict):</strong> يحدث عندما يعدّل شخصان نفس السطر في ملف واحد. Git يخبرك بالمشكلة وتحلها يدوياً ثم تعمل <code style="color:var(--yellow);">git add ثم git commit</code>.</div></div>
  <div class="card">
    <div class="card-title">📋 استراتيجية تسمية الفروع</div>
    <table class="cmd-table" style="margin-top:12px;">
      <tr><th>النوع</th><th>الاستخدام</th></tr>
      <tr><td>feature/...</td><td>ميزة جديدة</td></tr>
      <tr><td>fix/...</td><td>إصلاح خطأ</td></tr>
      <tr><td>hotfix/...</td><td>إصلاح عاجل في الإنتاج</td></tr>
      <tr><td>release/...</td><td>إصدار جديد</td></tr>
      <tr><td>docs/...</td><td>تحديث التوثيق</td></tr>
    </table>
  </div>
  <div style="text-align:center;margin-top:28px;"><button onclick="showSection('github')" style="background:var(--green2);border:none;color:white;padding:14px 32px;border-radius:8px;font-size:1rem;cursor:pointer;font-family:var(--body);font-weight:600;">التالي: GitHub ←</button></div>
</div>

<!-- GITHUB -->
<div class="section" id="github">
  <div class="section-title">☁️ GitHub</div>
  <p class="section-subtitle">الآن نتعلم كيف نربط مستودعنا المحلي بـ GitHub ونشارك كودنا مع العالم.</p>
  <div class="steps">
    <div class="step"><div class="step-num">1</div><div class="step-content"><h3>إنشاء مستودع جديد على GitHub</h3><p>اذهب إلى github.com، انقر على <strong style="color:var(--green);">New</strong> ثم أدخل اسم المستودع وانقر <strong style="color:var(--green);">Create repository</strong>.</p></div></div>
    <div class="step">
      <div class="step-num">2</div>
      <div class="step-content">
        <h3>ربط المستودع المحلي بـ GitHub</h3>
        <div class="code-block" style="margin-top:12px;">
          <div class="code-header"><div class="dots"><div class="dot dot-r"></div><div class="dot dot-y"></div><div class="dot dot-g"></div></div><span>ربط Remote</span><button class="copy-btn" onclick="copyCode(this)">نسخ</button></div>
          <div class="code-body"><span class="cmd">git remote add</span> <span class="arg">origin</span> <span class="str">https://github.com/yassin/my-project.git</span>
<span class="cmd">git remote</span> <span class="flag">-v</span>
<span class="out">origin  https://github.com/yassin/my-project.git (fetch)
origin  https://github.com/yassin/my-project.git (push)</span></div>
        </div>
      </div>
    </div>
    <div class="step">
      <div class="step-num">3</div>
      <div class="step-content">
        <h3>رفع الكود وجلبه</h3>
        <div class="code-block" style="margin-top:12px;">
          <div class="code-header"><div class="dots"><div class="dot dot-r"></div><div class="dot dot-y"></div><div class="dot dot-g"></div></div><span>Push & Pull & Clone</span><button class="copy-btn" onclick="copyCode(this)">نسخ</button></div>
          <div class="code-body"><span class="comment"># أول رفع</span>
<span class="cmd">git push</span> <span class="flag">-u</span> <span class="arg">origin main</span>

<span class="comment"># رفع في المرات القادمة</span>
<span class="cmd">git push</span>

<span class="comment"># جلب آخر التغييرات من GitHub</span>
<span class="cmd">git pull</span>

<span class="comment"># نسخ مستودع موجود على GitHub</span>
<span class="cmd">git clone</span> <span class="str">https://github.com/username/repo.git</span></div>
        </div>
      </div>
    </div>
  </div>
  <div class="card">
    <div class="card-title">🏷️ أهم ميزات GitHub</div>
    <table class="cmd-table" style="margin-top:12px;">
      <tr><th>الميزة</th><th>الاستخدام</th></tr>
      <tr><td>Issues</td><td>تتبع المشاكل والمهام</td></tr>
      <tr><td>Pull Request</td><td>طلب دمج فرعك مع الكود الرئيسي</td></tr>
      <tr><td>Actions</td><td>أتمتة الاختبار والنشر (CI/CD)</td></tr>
      <tr><td>Pages</td><td>استضافة مجانية لمواقع الويب</td></tr>
      <tr><td>README.md</td><td>وصف المشروع يظهر في الصفحة الرئيسية</td></tr>
    </table>
  </div>
  <div class="info-box note"><div class="info-icon">📌</div><div><strong>README.md</strong> هو أهم ملف في مشروعك. اجعله يشرح: ما المشروع، كيف تثبته، وكيف تستخدمه.</div></div>
  <div style="text-align:center;margin-top:28px;"><button onclick="showSection('collab')" style="background:var(--green2);border:none;color:white;padding:14px 32px;border-radius:8px;font-size:1rem;cursor:pointer;font-family:var(--body);font-weight:600;">التالي: التعاون ←</button></div>
</div>

<!-- COLLAB -->
<div class="section" id="collab">
  <div class="section-title">🤝 العمل الجماعي</div>
  <p class="section-subtitle">هذا ما يجعل Git وGitHub لا غنى عنهما — التعاون بين المطورين بشكل سلس.</p>
  <div class="card">
    <div class="card-title">🔄 سيناريو التعاون النموذجي</div>
    <div class="steps" style="margin-top:16px;">
      <div class="step"><div class="step-num" style="font-size:11px;">١</div><div class="step-content"><h3>Fork المشروع</h3><p>انقر Fork على GitHub لتنسخ المستودع لحسابك الشخصي.</p></div></div>
      <div class="step">
        <div class="step-num" style="font-size:11px;">٢</div>
        <div class="step-content">
          <h3>Clone على جهازك</h3>
          <div class="code-block" style="margin-top:8px;">
            <div class="code-header"><div class="dots"><div class="dot dot-r"></div><div class="dot dot-y"></div><div class="dot dot-g"></div></div><span>Clone</span><button class="copy-btn" onclick="copyCode(this)">نسخ</button></div>
            <div class="code-body"><span class="cmd">git clone</span> <span class="str">https://github.com/your-user/project.git</span>
<span class="cmd">cd</span> <span class="arg">project</span></div>
          </div>
        </div>
      </div>
      <div class="step">
        <div class="step-num" style="font-size:11px;">٣</div>
        <div class="step-content">
          <h3>أنشئ فرعاً وقم بتعديلاتك</h3>
          <div class="code-block" style="margin-top:8px;">
            <div class="code-header"><div class="dots"><div class="dot dot-r"></div><div class="dot dot-y"></div><div class="dot dot-g"></div></div><span>Branch & Push</span><button class="copy-btn" onclick="copyCode(this)">نسخ</button></div>
            <div class="code-body"><span class="cmd">git checkout</span> <span class="flag">-b</span> <span class="arg">fix/navbar-bug</span>
<span class="comment"># قم بتعديلاتك...</span>
<span class="cmd">git add</span> <span class="flag">.</span>
<span class="cmd">git commit</span> <span class="flag">-m</span> <span class="str">"إصلاح خطأ في شريط التنقل"</span>
<span class="cmd">git push origin</span> <span class="arg">fix/navbar-bug</span></div>
          </div>
        </div>
      </div>
      <div class="step"><div class="step-num" style="font-size:11px;">٤</div><div class="step-content"><h3>افتح Pull Request</h3><p>على GitHub، انقر <strong style="color:var(--green);">Compare & pull request</strong> واكتب وصفاً للتغييرات.</p></div></div>
      <div class="step"><div class="step-num" style="font-size:11px;">٥</div><div class="step-content"><h3>Code Review والدمج</h3><p>يراجع المشرف الكود ويقدم تعليقات، وعند الموافقة ينقر <strong style="color:var(--purple);">Merge pull request</strong>.</p></div></div>
    </div>
  </div>
  <div class="card">
    <div class="card-title">⚡ أوامر متقدمة مفيدة</div>
    <div class="code-block" style="margin-top:12px;">
      <div class="code-header"><div class="dots"><div class="dot dot-r"></div><div class="dot dot-y"></div><div class="dot dot-g"></div></div><span>أوامر متقدمة</span><button class="copy-btn" onclick="copyCode(this)">نسخ</button></div>
      <div class="code-body"><span class="comment"># تخزين التغييرات مؤقتاً دون Commit</span>
<span class="cmd">git stash</span>
<span class="cmd">git stash pop</span>

<span class="comment"># إلغاء آخر Commit مع الإبقاء على التغييرات</span>
<span class="cmd">git reset</span> <span class="flag">--soft</span> <span class="arg">HEAD~1</span>

<span class="comment"># تعديل رسالة آخر Commit</span>
<span class="cmd">git commit</span> <span class="flag">--amend -m</span> <span class="str">"الرسالة الصحيحة"</span>

<span class="comment"># تطبيق Commit معين من فرع آخر</span>
<span class="cmd">git cherry-pick</span> <span class="arg">a1b2c3d</span></div>
    </div>
  </div>
  <div class="info-box tip"><div class="info-icon">🎯</div><div><strong>نصيحة للمشاريع الجماعية:</strong> اتفق مع فريقك مسبقاً على نمط تسمية الفروع وكيفية كتابة رسائل Commit. هذا يوفر ساعات من الفوضى!</div></div>
  <div style="text-align:center;margin-top:28px;"><button onclick="showSection('quiz')" style="background:var(--green2);border:none;color:white;padding:14px 32px;border-radius:8px;font-size:1rem;cursor:pointer;font-family:var(--body);font-weight:600;">اختبر معلوماتك ←</button></div>
</div>

<!-- QUIZ -->
<div class="section" id="quiz">
  <div class="section-title">🎯 اختبر نفسك</div>
  <p class="section-subtitle">٧ أسئلة لاختبار ما تعلمته. هل أنت جاهز؟</p>
  <div id="quiz-container"></div>
  <div class="score-board" id="score-board" style="display:none;">
    <div style="font-size:1.1rem;margin-bottom:12px;color:var(--muted);">نتيجتك النهائية</div>
    <div class="score-num" id="score-display">0/7</div>
    <div class="progress-bar-wrap" style="max-width:300px;margin:16px auto;"><div class="progress-bar" id="score-bar" style="width:0%;"></div></div>
    <div id="score-msg" style="color:var(--muted);margin-top:8px;"></div>
    <button onclick="resetQuiz()" style="margin-top:20px;background:transparent;border:1px solid var(--border);color:var(--text);padding:10px 24px;border-radius:8px;cursor:pointer;font-family:var(--body);">إعادة الاختبار 🔄</button>
  </div>
</div>

</div>
<script>
const questions=[
  {q:"ما الأمر المستخدم لإنشاء مستودع Git جديد في مجلد موجود؟",opts:["git start","git new","git init","git create"],ans:2,exp:"✅ صحيح! git init يحول المجلد الحالي إلى مستودع Git بإنشاء مجلد .git مخفي."},
  {q:"ما الفرق بين git add و git commit؟",opts:["لا فرق، كلاهما يحفظ التغييرات","git add يضيف الملفات لمنطقة التجهيز، git commit يحفظها في التاريخ","git add يرفع للـ GitHub، git commit يحفظ محلياً","git commit يأتي قبل git add دائماً"],ans:1,exp:"✅ صحيح! git add يجهّز الملفات للحفظ، وgit commit هو الحفظ الفعلي في تاريخ المستودع."},
  {q:'ماذا يفعل هذا الأمر: git checkout -b feature/signup ؟',opts:["ينتقل لفرع موجود اسمه feature/signup","يحذف الفرع feature/signup","ينشئ فرعاً جديداً اسمه feature/signup وينتقل إليه","يدمج الفرع feature/signup مع main"],ans:2,exp:"✅ صحيح! الـ flag -b يعني 'أنشئ وانتقل' — اختصار لأمرين: git branch + git checkout."},
  {q:"ما هو ملف .gitignore ويستخدم لـ؟",opts:["حفظ إعدادات Git العالمية","تخزين رسائل الـ Commits","إخبار Git بتجاهل ملفات ومجلدات معينة","تسجيل أسماء المساهمين في المشروع"],ans:2,exp:"✅ صحيح! .gitignore يحدد الملفات التي يجب ألا يتتبعها Git، مثل .env وnode_modules."},
  {q:"ما الفرق بين git pull و git fetch؟",opts:["git pull أسرع من git fetch","git fetch يجلب التغييرات ويدمجها، git pull يجلبها فقط","git fetch يجلب التغييرات دون دمجها، git pull يجلبها ويدمجها","كلاهما متطابقان تماماً"],ans:2,exp:"✅ صحيح! git fetch = تحقق من التغييرات فقط. git pull = fetch + merge في أمر واحد."},
  {q:"ما هو Pull Request في GitHub؟",opts:["أمر لجلب الكود من الـ Remote","طلب لدمج فرعك مع الفرع الرئيسي بعد مراجعة الكود","ميزة لطلب صلاحيات الوصول للمستودع","أمر لتحديث الـ README"],ans:1,exp:"✅ صحيح! Pull Request هو طلب مراجعة ودمج كودك — قلب التعاون على GitHub!"},
  {q:"ما الأمر الصحيح لرفع التغييرات لأول مرة لـ GitHub؟",opts:["git upload origin main","git send -u origin main","git push -u origin main","git remote push main"],ans:2,exp:"✅ صحيح! git push -u origin main — الـ -u تحفظ الإعدادات حتى تكتب git push فقط في المرات القادمة."}
];
let answers=new Array(questions.length).fill(null),score=0;
function buildQuiz(){
  const c=document.getElementById('quiz-container');c.innerHTML='';
  questions.forEach((q,i)=>{
    const d=document.createElement('div');d.className='quiz-card';d.id='q'+i;
    d.innerHTML=`<div class="quiz-q">السؤال ${i+1}/${questions.length}: ${q.q}</div><div class="quiz-opts">${q.opts.map((o,j)=>`<button class="quiz-opt" onclick="answer(${i},${j})">${o}</button>`).join('')}</div><div class="quiz-feedback" id="fb${i}"></div>`;
    c.appendChild(d);
  });
}
function answer(qi,oi){
  if(answers[qi]!==null)return;
  answers[qi]=oi;
  const opts=document.querySelectorAll(`#q${qi} .quiz-opt`),fb=document.getElementById('fb'+qi),q=questions[qi];
  opts.forEach((b,j)=>{b.disabled=true;if(j===q.ans)b.classList.add('correct');else if(j===oi&&oi!==q.ans)b.classList.add('wrong');});
  if(oi===q.ans){score++;fb.className='quiz-feedback show ok';fb.textContent=q.exp;}
  else{fb.className='quiz-feedback show fail';fb.textContent=`❌ الإجابة الصحيحة: "${q.opts[q.ans]}"`;}
  if(answers.every(a=>a!==null))showScore();
}
function showScore(){
  const b=document.getElementById('score-board');b.style.display='block';
  document.getElementById('score-display').textContent=`${score}/${questions.length}`;
  const p=Math.round(score/questions.length*100);
  setTimeout(()=>{document.getElementById('score-bar').style.width=p+'%';},100);
  const msgs=[[0,3,"😅 راجع الدرس مرة أخرى، أنت تستطيع!"],[3,5,"👍 جيد! راجع المفاهيم الأساسية أكثر."],[5,6,"🎉 ممتاز! أنت على الطريق الصحيح!"],[6,8,"🏆 رائع جداً! أنت متقن لـ Git وGitHub!"]];
  const m=msgs.find(x=>score>=x[0]&&score<x[1]);
  document.getElementById('score-msg').textContent=m?m[2]:'';
}
function resetQuiz(){answers=new Array(questions.length).fill(null);score=0;document.getElementById('score-board').style.display='none';buildQuiz();}
function showSection(id){
  document.querySelectorAll('.section').forEach(s=>s.classList.remove('active'));
  document.querySelectorAll('.nav-btn').forEach(b=>b.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  const order=['intro','setup','basics','branches','github','collab','quiz'];
  document.querySelectorAll('.nav-btn')[order.indexOf(id)].classList.add('active');
  window.scrollTo({top:0,behavior:'smooth'});
}
function copyCode(btn){
  const code=btn.closest('.code-block').querySelector('.code-body').innerText;
  navigator.clipboard.writeText(code).then(()=>{btn.textContent='✓ تم';setTimeout(()=>btn.textContent='نسخ',2000);});
}
buildQuiz();
</script>
</body>
</html>
