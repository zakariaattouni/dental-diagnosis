<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>تشخيص أمراض الفم والأسنان (سحابي)</title>
    <style>
        :root { --bg: #f8fafc; --card: #ffffff; --primary: #0284c7; --primary-dark: #0369a1; --success: #10b981; --danger: #ef4444; --text: #0f172a; --muted: #64748b; --border: #e2e8f0; --radius: 14px; --shadow: 0 4px 12px rgba(0,0,0,0.06); --shadow-lg: 0 8px 24px rgba(0,0,0,0.1); }
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: system-ui, -apple-system, "Segoe UI", Roboto, sans-serif; }
        body { background: var(--bg); color: var(--text); min-height: 100vh; display: flex; flex-direction: column; }
        
        header { background: var(--card); border-bottom: 1px solid var(--border); padding: 14px 20px; display: flex; justify-content: space-between; align-items: center; position: sticky; top: 0; z-index: 100; box-shadow: 0 2px 8px rgba(0,0,0,0.04); }
        .logo { display: flex; align-items: center; gap: 10px; font-weight: 700; font-size: 1.15rem; color: var(--primary-dark); }
        .logo svg { width: 40px; height: 40px; }
        .nav-actions { display: flex; align-items: center; gap: 14px; }
        .notif-btn { background: none; border: none; cursor: pointer; padding: 8px; border-radius: 50%; position: relative; color: var(--text); }
        .notif-dot { position: absolute; top: 6px; right: 6px; width: 10px; height: 10px; background: var(--danger); border-radius: 50%; border: 2px solid white; display: none; }
        .notif-dot.show { display: block; animation: pulse 2s infinite; }
        @keyframes pulse { 0%, 100% { transform: scale(1); } 50% { transform: scale(1.2); } }
        
        .user-menu { display: flex; align-items: center; gap: 10px; }
        .avatar { width: 34px; height: 34px; background: var(--primary); color: white; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-weight: 600; }
        .uname { font-weight: 500; font-size: 0.9rem; }
        .logout-btn { background: #f1f5f9; border: none; padding: 6px 12px; border-radius: 8px; cursor: pointer; }
        
        main { flex: 1; padding: 24px 16px; max-width: 900px; margin: auto; width: 100%; }
        .view { display: none; animation: fadeIn 0.3s ease; }
        .view.active { display: block; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(8px); } to { opacity: 1; transform: translateY(0); } }

        .auth-box { max-width: 420px; margin: 30px auto; background: var(--card); padding: 32px; border-radius: var(--radius); box-shadow: var(--shadow-lg); text-align: center; }
        .auth-box h2 { color: var(--primary-dark); margin-bottom: 8px; }
        .auth-box p { color: var(--muted); margin-bottom: 24px; font-size: 0.92rem; }
        .form-group { margin-bottom: 16px; text-align: right; }
        .form-group label { display: block; margin-bottom: 6px; font-size: 0.88rem; font-weight: 500; }
        .input { width: 100%; padding: 12px; border: 1px solid var(--border); border-radius: 10px; font-size: 0.95rem; background: #fafbfc; }
        .input:focus { outline: none; border-color: var(--primary); box-shadow: 0 0 0 3px rgba(2,132,199,0.1); background: white; }
        
        .btn { width: 100%; padding: 13px; border: none; border-radius: 10px; font-size: 0.95rem; cursor: pointer; font-weight: 600; display: flex; align-items: center; justify-content: center; gap: 6px; margin-top: 8px; }
        .btn-primary { background: var(--primary); color: white; }
        .btn-success { background: var(--success); color: white; }
        .btn-outline { background: transparent; border: 1.5px solid var(--primary); color: var(--primary); }
        .btn-danger { background: var(--danger); color: white; }
        
        .card { background: var(--card); border-radius: var(--radius); box-shadow: var(--shadow); padding: 20px; margin-bottom: 20px; }
        .card h3 { color: var(--primary-dark); margin-bottom: 12px; font-size: 1.1rem; }
        .stats { display: grid; grid-template-columns: repeat(3, 1fr); gap: 12px; margin-bottom: 20px; }
        .stat { background: #f8fafc; padding: 14px; border-radius: 10px; text-align: center; border: 1px solid var(--border); }
        .stat-num { font-size: 1.5rem; font-weight: 700; color: var(--primary); }
        .stat-label { font-size: 0.8rem; color: var(--muted); margin-top: 4px; }        
        .req-list { display: flex; flex-direction: column; gap: 10px; }
        .req-item { background: #fffbeb; border: 1px solid #fcd34d; padding: 14px; border-radius: 10px; display: flex; justify-content: space-between; align-items: center; }
        .req-info strong { display: block; color: #92400e; }
        .req-info small { color: #b45309; font-size: 0.82rem; }
        .action-btn { padding: 6px 10px; border: none; border-radius: 8px; cursor: pointer; font-size: 0.82rem; font-weight: 600; }
        .action-btn.approve { background: var(--success); color: white; }
        .action-btn.reject { background: var(--danger); color: white; }

        table { width: 100%; border-collapse: separate; border-spacing: 0 6px; margin-top: 10px; font-size: 0.88rem; }
        th { padding: 10px; color: var(--muted); text-align: right; }
        td { padding: 12px; background: white; border-radius: 10px; box-shadow: 0 2px 6px rgba(0,0,0,0.04); text-align: right; }
        .badge { padding: 4px 8px; border-radius: 20px; font-size: 0.75rem; font-weight: 600; }
        .badge-active { background: #d1fae5; color: #065f46; }
        .badge-pending { background: #fef3c7; color: #92400e; }
        
        textarea { width: 100%; padding: 14px; border: 1px solid var(--border); border-radius: 10px; min-height: 120px; resize: vertical; background: #fafbfc; }
        textarea:focus { outline: none; border-color: var(--primary); box-shadow: 0 0 0 3px rgba(2,132,199,0.1); background: white; }
        .result-box { background: #f0fdf4; border: 1px solid #bbf7d0; padding: 16px; border-radius: 12px; margin: 16px 0; }
        .warning { background: #fef2f2; border: 1px solid #fecaca; color: #b91c1c; padding: 10px; border-radius: 8px; margin-top: 12px; text-align: center; }
        
        footer { background: var(--card); border-top: 1px solid var(--border); padding: 16px; text-align: center; font-size: 0.85rem; color: var(--muted); margin-top: auto; }
        .hide { display: none !important; }
        .toast { position: fixed; bottom: 20px; left: 50%; transform: translateX(-50%); background: var(--text); color: white; padding: 12px 20px; border-radius: 10px; z-index: 1000; opacity: 0; transition: opacity 0.3s; pointer-events: none; }
        .toast.show { opacity: 1; }
    </style>
</head>
<body>
    <header>
        <div class="logo">
            <svg viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
                <ellipse cx="50" cy="55" rx="35" ry="40" fill="none" stroke="#0284c7" stroke-width="2.5"/>
                <ellipse cx="38" cy="42" rx="5" ry="3" fill="#0284c7"/>
                <ellipse cx="62" cy="42" rx="5" ry="3" fill="#0284c7"/>
                <ellipse cx="50" cy="65" rx="12" ry="10" fill="#e0f2fe" stroke="#0284c7" stroke-width="2"/>
                <circle cx="50" cy="65" r="18" fill="rgba(255,255,255,0.8)" stroke="#0284c7" stroke-width="3"/>
                <line x1="63" y1="78" x2="73" y2="88" stroke="#0284c7" stroke-width="5" stroke-linecap="round"/>
                <text x="50" y="69" text-anchor="middle" fill="#0284c7" font-size="15" font-weight="bold" font-family="Arial">AI</text>
            </svg>
            <span>تشخيص أمراض الفم والأسنان</span>
        </div>
        <div class="nav-actions" id="nav" style="display:none;">
            <button class="notif-btn" id="notif-btn" style="display:none;" onclick="alert('📥 لديك طلبات جديدة!')">
                <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M18 8A6 6 0 0 0 6 8c0 7-3 9-3 9h18s-3-2-3-9"/><path d="M13.73 21a2 2 0 0 1-3.46 0"/></svg>
                <span class="notif-dot" id="notif-dot"></span>
            </button>
            <div class="user-menu">
                <div class="avatar" id="avatar">م</div>
                <span class="uname" id="uname">مستخدم</span>
                <button class="logout-btn" onclick="logout()">خروج</button>            </div>
        </div>
    </header>

    <main>
        <div id="login-view" class="view active">
            <div class="auth-box">
                <h2>تسجيل الدخول</h2>
                <p>منصة تعليمية سحابية متكاملة</p>
                <div class="form-group"><label>البريد الإلكتروني</label><input type="email" id="l-email" class="input" placeholder="example@email.com"></div>
                <div class="form-group"><label>كلمة المرور</label><input type="password" id="l-pass" class="input" placeholder="••••••••"></div>
                <button class="btn btn-primary" onclick="login()">🔐 دخول</button>
                <button class="btn btn-outline" onclick="showView('reg-view')" style="margin-top:10px">📝 إنشاء حساب جديد</button>
            </div>
        </div>

        <div id="reg-view" class="view">
            <div class="auth-box">
                <h2>طلب انضمام جديد</h2>
                <p>سيتم تفعيل حسابك يدوياً من قبل الإدارة</p>
                <div class="form-group"><label>الاسم الكامل</label><input type="text" id="r-name" class="input" placeholder="الاسم الثلاثي"></div>
                <div class="form-group"><label>البريد الإلكتروني</label><input type="email" id="r-email" class="input" placeholder="example@email.com"></div>
                <div class="form-group"><label>كلمة المرور</label><input type="password" id="r-pass" class="input" placeholder="6 أحرف على الأقل"></div>
                <button class="btn btn-success" onclick="register()">📤 إرسال الطلب</button>
                <button class="btn btn-outline" onclick="showView('login-view')" style="margin-top:8px">← العودة</button>
            </div>
        </div>

        <div id="admin-view" class="view">
            <div class="card">
                <h3>📊 لوحة التحكم الإدارية</h3>
                <div class="stats">
                    <div class="stat"><div class="stat-num" id="st-pend">0</div><div class="stat-label">طلبات معلقة</div></div>
                    <div class="stat"><div class="stat-num" id="st-act">0</div><div class="stat-label">نشط</div></div>
                    <div class="stat"><div class="stat-num" id="st-all">0</div><div class="stat-label">إجمالي</div></div>
                </div>
            </div>
            <div class="card">
                <h3>📥 طلبات التفعيل اليدوي</h3>
                <div id="pend-list" class="req-list"></div>
            </div>
            <div class="card">
                <h3>👥 سجل المستخدمين</h3>
                <div style="overflow-x:auto"><table><thead><tr><th>الاسم</th><th>البريد</th><th>الحالة</th><th>إجراء</th></tr></thead><tbody id="u-tbl"></tbody></table></div>
            </div>
        </div>

        <div id="doc-view" class="view">
            <div class="card">
                <h3>📋 وصف الحالة السريرية</h3>                <div class="form-group"><label>الأعراض والعلامات</label><textarea id="sym-txt" placeholder="اكتب الأعراض بدقة..."></textarea></div>
                <button class="btn btn-primary" onclick="diagnose()">🔍 تحليل التشخيص</button>
            </div>
            <div id="res-area"></div>
        </div>
    </main>

    <footer>© 2026 جميع الحقوق محفوظة | منصة تعليمية</footer>
    <div class="toast" id="toast"></div>

    <!-- Firebase SDKs -->
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <script>
        // 🔥 1. إعدادات Firebase (استبدل هذا الجزء ببيانات مشروعك)
        const firebaseConfig = {
            apiKey: "ضع_API_KEY_هنا",
            authDomain: "اسم_مشروعك.firebaseapp.com",
            databaseURL: "https://اسم_مشروعك-default-rtdb.firebaseio.com",
            projectId: "اسم_مشروعك",
            storageBucket: "اسم_مشروعك.appspot.com",
            messagingSenderId: "123456789",
            appId: "1:123456789:web:abcdef"
        };

        // تهيئة Firebase
        firebase.initializeApp(firebaseConfig);
        const db = firebase.database();

        const ADMIN_EMAIL = "salematto@gmail.com";
        const ADMIN_PASS = "zak959";
        let currentUser = null;

        const showToast = msg => { const t = document.getElementById('toast'); t.textContent = msg; t.classList.add('show'); setTimeout(() => t.classList.remove('show'), 3000); };
        const showView = id => { document.querySelectorAll('.view').forEach(v => v.classList.remove('active')); document.getElementById(id).classList.add('active'); };

        // 🚀 التشغيل الأولي
        window.onload = () => {
            const savedUser = localStorage.getItem('dental_session');
            if (savedUser) {
                currentUser = JSON.parse(savedUser);
                setupUI();
            }
        };

        function setupUI() {
            document.getElementById('nav').style.display = 'flex';
            document.getElementById('avatar').textContent = currentUser.name.charAt(0);
            document.getElementById('uname').textContent = currentUser.name;            
            if (currentUser.role === 'admin') {
                document.getElementById('notif-btn').style.display = 'block';
                showView('admin-view');
                listenForAdminUpdates(); // الاستماع المباشر للتغيرات من السيرفر
            } else {
                document.getElementById('notif-btn').style.display = 'none';
                showView('doc-view');
            }
        }

        function login() {
            const email = document.getElementById('l-email').value.trim().toLowerCase();
            const pass = document.getElementById('l-pass').value.trim();
            if (!email || !pass) return showToast('أكمل الحقول');

            if (email === ADMIN_EMAIL && pass === ADMIN_PASS) {
                currentUser = { name: 'الإدارة', email, role: 'admin' };
                localStorage.setItem('dental_session', JSON.stringify(currentUser));
                setupUI();
                return;
            }

            // بحث في قاعدة البيانات
            db.ref('users').orderByChild('email').equalTo(email).once('value').then(snapshot => {
                if (snapshot.exists()) {
                    let userData = null;
                    snapshot.forEach(child => { userData = { id: child.key, ...child.val() }; });
                    
                    if (userData.pass !== pass) return showToast('❌ كلمة المرور غير صحيحة');
                    if (userData.status === 'pending') return showToast('⏳ حسابك قيد المراجعة');
                    if (userData.status === 'rejected') return showToast('❌ تم رفض الطلب');

                    currentUser = { ...userData, role: 'doctor' };
                    localStorage.setItem('dental_session', JSON.stringify(currentUser));
                    setupUI();
                } else {
                    showToast('❌ هذا البريد غير مسجل');
                }
            });
        }

        function register() {
            const name = document.getElementById('r-name').value.trim();
            const email = document.getElementById('r-email').value.trim().toLowerCase();
            const pass = document.getElementById('r-pass').value;

            if (!name || !email || !pass) return showToast('أكمل الحقول');
            if (pass.length < 6) return showToast('كلمة المرور قصيرة');
            // التحقق من التكرار والحفظ في Firebase
            db.ref('users').orderByChild('email').equalTo(email).once('value').then(snapshot => {
                if (snapshot.exists()) return showToast('البريد مسجل مسبقاً');
                
                const newUserRef = db.ref('users').push();
                newUserRef.set({
                    name, email, pass, status: 'pending', date: Date.now()
                }).then(() => {
                    showToast('✅ تم إرسال الطلب بنجاح! بانتظار التفعيل');
                    showView('login-view');
                });
            });
        }

        function logout() { localStorage.removeItem('dental_session'); location.reload(); }

        // 🔔 الاستماع المباشر للتغيرات (Real-time Listener)
        function listenForAdminUpdates() {
            db.ref('users').on('value', snapshot => {
                const users = [];
                snapshot.forEach(child => { users.push({ id: child.key, ...child.val() }); });
                
                const pending = users.filter(u => u.status === 'pending');
                const active = users.filter(u => u.status === 'active').length;
                
                // تحديث الإحصائيات
                document.getElementById('st-pend').textContent = pending.length;
                document.getElementById('st-act').textContent = active;
                document.getElementById('st-all').textContent = users.length;
                
                // تحديث نقطة الإشعار
                document.getElementById('notif-dot').classList.toggle('show', pending.length > 0);

                // تحديث قائمة الطلبات
                const pendDiv = document.getElementById('pend-list');
                pendDiv.innerHTML = pending.length === 0 ? '<div class="card" style="text-align:center;color:var(--muted)">لا توجد طلبات جديدة</div>' :
                    pending.map(u => `
                        <div class="req-item">
                            <div class="req-info"><strong>${u.name}</strong><small>${u.email}</small></div>
                            <div class="req-actions">
                                <button class="action-btn approve" onclick="updateStatus('${u.id}', 'active')">✅ تفعيل</button>
                                <button class="action-btn reject" onclick="updateStatus('${u.id}', 'rejected')">❌ رفض</button>
                            </div>
                        </div>`).join('');

                // تحديث الجدول
                document.getElementById('u-tbl').innerHTML = users.map(u => {
                    const sc = u.status === 'active' ? 'badge-active' : 'badge-pending';
                    const st = u.status === 'active' ? 'نشط' : 'معلق';
                    return `<tr><td>${u.name}</td><td>${u.email}</td><td><span class="badge ${sc}">${st}</span></td><td><button onclick="delUser('${u.id}')" style="color:red;border:none;background:none;cursor:pointer">🗑️</button></td></tr>`;                }).join('');
            });
        }

        function updateStatus(id, status) {
            db.ref('users/' + id).update({ status }).then(() => showToast(status === 'active' ? '✅ تم التفعيل' : '❌ تم الرفض'));
        }
        function delUser(id) {
            if(confirm('حذف نهائي؟')) db.ref('users/' + id).remove();
        }

        // 🩺 التشخيص
        function diagnose() {
            const txt = document.getElementById('sym-txt').value.trim();
            if (!txt) return showToast('اكتب الأعراض أولاً');
            // (نفس منطق التشخيص السابق)
            const DB = [
                {k:["ألم","بارد","ساخن","تسوس"], t:"تسوس سني محتمل - راجع الطبيب للحشو."},
                {k:["نزيف","لثة","تورم"], t:"التهاب لثة - يحتاج تنظيف احترافي."},
                {k:["ألم","نابض","ليل"], t:"التهاب عصب - يحتاج علاج جذر."}
            ];
            let best = null, max = 0;
            DB.forEach(d => { let s = 0; d.k.forEach(k => { if(txt.includes(k)) s++; }); if(s>max) { max=s; best=d; } });
            
            document.getElementById('res-area').innerHTML = `
                <div class="card">
                    <div class="result-box"><h4>📚 النتيجة</h4><p>${best ? best.t : 'لم يتم العثور على تطابق دقيق. راجع الطبيب.'}</p></div>
                    <div class="warning">⚠️ للأغراض التعليمية فقط</div>
                </div>`;
        }
    </script>
</body>
</html>
