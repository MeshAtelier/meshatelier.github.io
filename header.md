<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Mesh Atelier</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@400;500;600&family=Inter:wght@400;500&display=swap" rel="stylesheet">
  <style>
    :root {
      --bg: #120a1c;
      --text: #f3f0f8;
      --muted: #d6cfe0;
      --button-bg: #c8b3df;
      --button-text: #4a3160;
      --nav-text: rgba(255, 255, 255, 0.88);
      --top-fade: rgba(239, 234, 244, 0.96);
      --top-fade-soft: rgba(239, 234, 244, 0.5);
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    html, body {
      min-height: 100%;
      background: radial-gradient(circle at center, #1a0d24 0%, #0b0610 70%);
      color: var(--text);
      overflow-x: hidden;
    }

    body {
      font-family: 'Inter', sans-serif;
    }

    .hero {
      position: relative;
      min-height: 100vh;
      isolation: isolate;
      background:
        radial-gradient(circle at center, rgba(86, 53, 112, 0.28), transparent 42%),
        linear-gradient(180deg, rgba(12, 7, 17, 0.15) 0%, rgba(12, 7, 17, 0.48) 100%),
        #0b0610;
      overflow: hidden;
    }

    .hero::before {
      content: "";
      position: absolute;
      inset: 0 0 auto 0;
      height: 108px;
      background: linear-gradient(
        180deg,
        var(--top-fade) 0%,
        var(--top-fade-soft) 38%,
        rgba(239, 234, 244, 0) 100%
      );
      z-index: 3;
      pointer-events: none;
    }

    .hero::after {
      content: "";
      position: absolute;
      inset: 0;
      background: radial-gradient(circle at 50% 44%, rgba(70, 39, 97, 0.16), transparent 38%);
      z-index: 1;
      pointer-events: none;
    }

    .navbar {
      position: relative;
      z-index: 5;
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 34px 66px;
    }

    .brand {
      font-family: 'Cormorant Garamond', serif;
      font-size: 2.1rem;
      font-weight: 500;
      color: var(--nav-text);
      letter-spacing: -0.02em;
    }

    .nav-links {
      display: flex;
      gap: 38px;
      align-items: center;
    }

    .nav-links a {
      color: var(--nav-text);
      text-decoration: none;
      font-size: 1rem;
      transition: opacity 0.25s ease, transform 0.25s ease;
      position: relative;
    }

    .nav-links a:hover {
      opacity: 0.85;
      transform: translateY(-1px);
    }

    .nav-links a.active::after {
      content: "";
      position: absolute;
      left: 0;
      bottom: -7px;
      width: 100%;
      height: 1px;
      background: currentColor;
      opacity: 0.85;
    }

    .content-wrap {
      position: relative;
      z-index: 4;
      min-height: calc(100vh - 110px);
      display: grid;
      place-items: center;
      padding: 24px;
    }

    .figure {
      position: absolute;
      inset: 0;
      display: flex;
      align-items: flex-start;
      justify-content: center;
      z-index: 2;
      pointer-events: none;
    }

    .figure img {
      width: min(74vw, 1120px);
      max-width: none;
      transform: translateY(-24px);
      object-fit: contain;
      filter: drop-shadow(0 0 26px rgba(255, 245, 255, 0.11));
      user-select: none;
      -webkit-user-drag: none;
    }

    .copy {
      position: relative;
      z-index: 4;
      width: min(1100px, 100%);
      text-align: center;
      padding-top: 88px;
    }

    h1 {
      font-family: 'Cormorant Garamond', serif;
      font-size: clamp(4rem, 6vw, 6.8rem);
      line-height: 0.95;
      font-weight: 500;
      letter-spacing: -0.03em;
      max-width: 1100px;
      margin: 0 auto;
      text-wrap: balance;
      text-shadow: 0 6px 24px rgba(0, 0, 0, 0.16);
    }

    .subtitle {
      margin-top: 24px;
      font-size: 1.2rem;
      color: rgba(255, 255, 255, 0.92);
      text-shadow: 0 2px 14px rgba(0, 0, 0, 0.18);
    }

    .actions {
      margin-top: 60px;
      display: flex;
      gap: 18px;
      justify-content: center;
      flex-wrap: wrap;
    }

    .btn {
      min-width: 270px;
      padding: 24px 34px;
      border-radius: 999px;
      text-decoration: none;
      font-size: 1.05rem;
      color: var(--button-text);
      background: var(--button-bg);
      box-shadow: 0 12px 30px rgba(39, 20, 55, 0.25);
      transition: transform 0.25s ease, opacity 0.25s ease, box-shadow 0.25s ease;
    }

    .btn:hover {
      transform: translateY(-2px);
      opacity: 0.96;
      box-shadow: 0 16px 34px rgba(39, 20, 55, 0.32);
    }

    @media (max-width: 1024px) {
      .navbar {
        padding: 28px 30px;
      }

      .nav-links {
        gap: 22px;
      }

      .figure img {
        width: min(108vw, 980px);
        transform: translateY(40px);
      }

      .copy {
        padding-top: 120px;
      }

      .subtitle {
        font-size: 1.02rem;
      }
    }

    @media (max-width: 768px) {
      .navbar {
        flex-direction: column;
        gap: 18px;
        padding: 24px 20px;
      }

      .brand {
        font-size: 1.8rem;
      }

      .nav-links {
        flex-wrap: wrap;
        justify-content: center;
        gap: 14px 20px;
      }

      .content-wrap {
        min-height: auto;
        padding: 10px 16px 48px;
      }

      .figure {
        position: relative;
        inset: auto;
        margin-top: 10px;
      }

      .figure img {
        width: min(138vw, 860px);
        transform: translateY(0);
      }

      .copy {
        margin-top: -70px;
        padding-top: 0;
      }

      h1 {
        font-size: clamp(2.9rem, 14vw, 4.4rem);
        line-height: 0.98;
      }

      .subtitle {
        margin-top: 16px;
        font-size: 0.98rem;
      }

      .actions {
        margin-top: 34px;
        gap: 14px;
      }

      .btn {
        min-width: min(100%, 330px);
        width: 100%;
        padding: 18px 24px;
      }
    }
  </style>
</head>
<body>
  <main class="hero">
    <header class="navbar">
      <div class="brand">Mesh Atelier</div>
      <nav class="nav-links">
        <a href="#" class="active">Home</a>
        <a href="#outfit-packs">Outfit Packs</a>
        <a href="#about">About</a>
        <a href="#contact">Contact</a>
      </nav>
    </header>

    <div class="content-wrap">
      <div class="figure">
        <img src="hero-character.png" alt="3D fashion character" />
      </div>

      <section class="copy">
        <h1>Digital Fashion for Real-Time Characters</h1>
        <p class="subtitle">Crafted for MetaHumans, Games and Virtual Worlds.</p>

        <div class="actions">
          <a class="btn" href="#shop">Shop on Fab</a>
          <a class="btn" href="#about">About the Atelier</a>
        </div>
      </section>
    </div>
  </main>
</body>
</html>

