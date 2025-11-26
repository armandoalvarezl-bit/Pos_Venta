<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Iniciar sesión — POS</title>

  <style>
    /* ========== Variables / Tema ========== */
    :root{
      --accent:#e50914;
      --bg-dark: #0b0b0b;
      --card-bg: rgba(0,0,0,0.55);
      --glass: rgba(255,255,255,0.04);
      --text-light: #ffffff;
      --muted: rgba(255,255,255,0.8);
      --radius: 8px;
      --max-width: 420px;
      --transition: 200ms ease;
    }

    /* ========== Reset / Base ========== */
    *{ box-sizing:border-box }
    html,body{ height:100% }
    body{
      margin:0;
      font-family:"Inter",system-ui,Arial;
      color:var(--text-light);
      background:#8f8f8f; /* Fondo base más claro */
      overflow:hidden;
    }

    /* ========== VIDEO DE FONDO ========== */
    .video-bg{
      position:fixed;
      top:0;left:0;
      width:100%;
      height:100%;
      object-fit:cover;
      z-index:-2;
      opacity:0.25; /* MÁS CLARO */
    }

    /* overlay aclarado */
    .bg-overlay{
      position:fixed;
      inset:0;
      background:linear-gradient(
        180deg,
        rgba(255,255,255,0.15),
        rgba(0,0,0,0.35)
      );
      z-index:-1;
    }

    /* ========== HERO (centro) ========== */
    .hero{
      position:relative;
      min-height:100vh;
      display:flex;
      align-items:center;
      justify-content:center;
    }

    /* top nav */
    .topbar{
      position:absolute;
      top:18px;
      left:24px;
      right:24px;
      display:flex;
      justify-content:space-between;
      align-items:center;
      z-index:5;
    }
    .brand{
      font-weight:800;
      letter-spacing:1px;
      color:var(--text-light);
      font-size:20px;
      text-shadow:0 2px 6px rgba(0,0,0,0.5);
    }
    .help-link{
      color:var(--muted);
      text-decoration:none;
      font-size:14px;
      padding:8px 12px;
      border-radius:6px;
      transition:  background var(--transition), color var(--transition);
    }
    .help-link:hover{
      background:rgba(255,255,255,0.04);
      color:var(--text-light);
    }

    /* ========== TARJETA LOGIN ========== */
    .login-wrap{
      position:relative;
      z-index:6;
      width:100%;
      max-width:var(--max-width);
      padding:36px;
      background:linear-gradient(180deg, rgba(0,0,0,0.55), rgba(0,0,0,0.45));
      border-radius:12px;
      box-shadow:0 10px 30px rgba(0,0,0,0.6);
      border:1px solid rgba(255,255,255,0.06);
      backdrop-filter:blur(6px);
    }

    /* LOGO TIPO PERFIL */
    .profile-logo {
      width: 110px;
      height: 110px;
      margin: 0 auto 20px auto;
      border-radius: 50%;
      overflow: hidden;
      border: 3px solid rgba(255, 255, 255, 0.4);
      box-shadow: 0 0 12px rgba(0,0,0,0.4);
    }
    .profile-logo img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    h1{
      margin:0 0 8px;
      font-size:28px;
      font-weight:700;
      color:var(--text-light);
      text-align:center;
    }
    p.lead{
      margin:0 0 18px;
      color:var(--muted);
      font-size:14px;
      text-align:center;
    }

    form{ display:block }
    .field{ margin-bottom:12px }
    label{
      display:block;
      font-size:13px;
      color:rgba(255,255,255,0.85);
      margin-bottom:6px;
      font-weight:600;
    }

    input[type="email"],
    input[type="password"]{
      width:100%;
      padding:12px 14px;
      border-radius:8px;
      border:1px solid rgba(255,255,255,0.08);
      background:rgba(255,255,255,0.02);
      color:var(--text-light);
      font-size:15px;
      transition:border-color var(--transition), box-shadow var(--transition);
    }
    input::placeholder{ color:rgba(255,255,255,0.45) }
    input:focus{
      outline:none;
      border-color:rgba(255,255,255,0.18);
      box-shadow:0 6px 18px rgba(0,0,0,0.6),
                 0 0 0 4px rgba(229,9,20,0.07);
    }

    .row{
      display:flex;
      gap:12px;
      align-items:center;
      justify-content:space-between;
    }
    .checkbox{
      display:flex;
      align-items:center;
      gap:8px;
      color:var(--muted);
      font-size:14px;
    }

    .btn{
      display:inline-block;
      width:100%;
      padding:12px 14px;
      border-radius:8px;
      border:none;
      font-size:16px;
      font-weight:700;
      cursor:pointer;
      box-shadow:0 6px 18px rgba(229,9,20,0.12);
      background:linear-gradient(180deg, var(--accent), #b30b12);
      color:white;
      transition:transform var(--transition), box-shadow var(--transition);
    }
    .btn:active{ transform:translateY(1px) }

    .error{
      margin:10px 0 0;
      padding:10px 12px;
      border-radius:8px;
      background:rgba(229,9,20,0.08);
      color:#ffd6d8;
      border:1px solid rgba(229,9,20,0.12);
      display:none;
      font-size:13px;
    }

    .meta{
      margin-top:14px;
      display:flex;
      justify-content:space-between;
      color:var(--muted);
      font-size:13px;
    }

    /* responsive */
    @media(max-width:520px){
      .login-wrap{ padding:24px; margin:16px; }
      h1{ font-size:22px }
    }
  </style>
</head>

<body>

  <!-- VIDEO DE FONDO -->
  <video class="video-bg" autoplay muted loop>
    <source src="img/Diseño sin título.mp4" type="video/mp4">
  </video>

  <div class="bg-overlay"></div>

  <div class="hero" role="main" aria-labelledby="loginTitle">

    <div class="topbar">
      <div class="brand">POS CORPORATIVO</div>
      <a class="help-link" href="soporte.html">¿Necesitas ayuda?</a>
    </div>

    <main class="login-wrap" role="form" aria-labelledby="loginTitle" aria-describedby="loginDesc">

      <!-- LOGO PERFIL -->
      <div class="profile-logo">
        <img src="img/logo.png" alt="Logo Perfil">
      </div>

      <h1 id="loginTitle">Pos Corporativo</h1>
      <p id="loginDesc" class="lead">Accede a tu punto de venta. Ingresa tu correo y contraseña para continuar.</p>

      <form id="signin" novalidate>

        <div class="field">
          <label for="email">Correo electrónico</label>
          <input id="email" type="email" placeholder="tucorreo@ejemplo.com" autocomplete="username" required>
        </div>

        <div class="field">
          <label for="password">Contraseña</label>
          <input id="password" type="password" placeholder="••••••••" autocomplete="current-password" required minlength="6">
        </div>

        <div class="row" style="margin-top:8px">
          <label class="checkbox"><input type="checkbox" id="remember"> Mantener sesión</label>
        </div>

        <div style="margin-top:14px">
          <button class="btn" type="submit">Entrar</button>
        </div>

        <div class="error" id="errorBox"></div>

        

      </form>
    </main>
  </div>

  <script>
    (function(){
      const form = document.getElementById('signin');
      const email = document.getElementById('email');
      const pass = document.getElementById('password');
      const errorBox = document.getElementById('errorBox');

      const DEMO = { user:'admin@ifobe.com', pass:'admin_root2024@' };

      function showError(msg){
        errorBox.style.display='block';
        errorBox.textContent=msg;
      }
      function hideError(){
        errorBox.style.display='none';
        errorBox.textContent='';
      }

      form.addEventListener('submit', function(e){
        e.preventDefault();
        hideError();

        if(!email.checkValidity()){
          showError('Ingresa un correo válido.');
          email.focus();
          return;
        }
        if(!pass.value || pass.value.length < 6){
          showError('La contraseña debe tener al menos 6 caracteres.');
          pass.focus();
          return;
        }

        if(email.value.toLowerCase()===DEMO.user && pass.value===DEMO.pass){
          const remember = document.getElementById('remember').checked;
          if(remember){
            localStorage.setItem('pos_auth_demo', JSON.stringify({user:DEMO.user, ts:Date.now()}));
          }
          window.location.href='home.html';
        }else{
          showError('Correo o contraseña incorrectos. Verifica e intenta de nuevo.');
        }
      });

      [email, pass].forEach(el => el.addEventListener('input', hideError));
    })();
  </script>

</body>
</html>
