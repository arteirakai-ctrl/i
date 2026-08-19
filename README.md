<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Uma surpresa para você 💌</title>

  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      min-height: 100vh;
      overflow: hidden;
      font-family: Georgia, serif;
      background:
        radial-gradient(circle at 50% 20%, #3b123d 0%, #170d1c 45%, #08070b 100%);
      color: #fff;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    /* Fundo */

    .stars {
      position: fixed;
      inset: 0;
      pointer-events: none;
      overflow: hidden;
    }

    .star {
      position: absolute;
      width: 2px;
      height: 2px;
      background: white;
      border-radius: 50%;
      opacity: 0.7;
      animation: twinkle 3s infinite alternate;
    }

    @keyframes twinkle {
      from { opacity: 0.2; }
      to { opacity: 1; }
    }

    /* Tela inicial */

    .intro {
      position: fixed;
      inset: 0;
      z-index: 10;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      background: rgba(8, 7, 11, 0.45);
      transition: opacity 1s ease;
    }

    .intro.hidden {
      opacity: 0;
      pointer-events: none;
    }

    .intro p {
      margin-bottom: 30px;
      font-size: 17px;
      letter-spacing: 2px;
      opacity: 0.85;
      text-align: center;
      padding: 0 20px;
    }

    /* Envelope */

    .envelope {
      width: 260px;
      height: 175px;
      position: relative;
      cursor: pointer;
      filter: drop-shadow(0 15px 25px rgba(0,0,0,.5));
      transition: transform .3s ease;
    }

    .envelope:hover {
      transform: scale(1.04);
    }

    .envelope-body {
      position: absolute;
      inset: 0;
      background: linear-gradient(145deg, #8d245e, #4d123f);
      border-radius: 5px;
      overflow: hidden;
    }

    .envelope-body::before,
    .envelope-body::after {
      content: "";
      position: absolute;
      width: 190px;
      height: 190px;
      background: #70194d;
      transform: rotate(45deg);
      top: 45px;
    }

    .envelope-body::before {
      left: -115px;
    }

    .envelope-body::after {
      right: -115px;
    }

    .flap {
      position: absolute;
      top: 0;
      left: 0;
      width: 0;
      height: 0;
      border-left: 130px solid transparent;
      border-right: 130px solid transparent;
      border-top: 95px solid #a72b70;
      z-index: 3;
      transform-origin: top;
      transition: transform 1s ease;
    }

    .heart {
      position: absolute;
      z-index: 4;
      left: 50%;
      top: 55%;
      transform: translate(-50%, -50%);
      font-size: 38px;
      animation: heartbeat 1.4s infinite;
    }

    @keyframes heartbeat {
      0%, 100% { transform: translate(-50%, -50%) scale(1); }
      50% { transform: translate(-50%, -50%) scale(1.15); }
    }

    .hint {
      margin-top: 25px;
      font-size: 14px;
      opacity: .65;
      letter-spacing: 1px;
    }

    /* Cartão */

    .card {
      position: relative;
      z-index: 2;
      width: min(90%, 420px);
      min-height: 500px;
      padding: 45px 30px;
      border: 1px solid rgba(255,255,255,.15);
      border-radius: 22px;
      background: rgba(20, 12, 24, .82);
      backdrop-filter: blur(12px);
      box-shadow:
        0 25px 80px rgba(0,0,0,.55),
        0 0 50px rgba(183, 46, 130, .12);

      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;

      text-align: center;

      opacity: 0;
      transform: translateY(30px) scale(.95);
      pointer-events: none;
      transition: all 1s ease;
    }

    .card.visible {
      opacity: 1;
      transform: translateY(0) scale(1);
      pointer-events: auto;
    }

    .card .small {
      font-size: 12px;
      letter-spacing: 4px;
      text-transform: uppercase;
      opacity: .55;
      margin-bottom: 25px;
    }

    .card h1 {
      font-size: 32px;
      font-weight: normal;
      margin-bottom: 25px;
      color: #f6b4dd;
    }

    .message {
      min-height: 150px;
      line-height: 1.8;
      font-size: 17px;
      color: #eee;
    }

    .signature {
      margin-top: 25px;
      color: #e891c5;
      font-style: italic;
      opacity: 0;
      transition: opacity 1s ease;
    }

    .signature.show {
      opacity: 1;
    }

    .music-button {
      margin-top: 25px;
      padding: 10px 18px;
      border: 1px solid rgba(255,255,255,.2);
      border-radius: 30px;
      background: rgba(255,255,255,.07);
      color: white;
      cursor: pointer;
      font-size: 13px;
    }

    /* Corações */

    .floating-heart {
      position: fixed;
      bottom: -30px;
      font-size: 18px;
      pointer-events: none;
      animation: floatUp linear forwards;
      z-index: 1;
    }

    @keyframes floatUp {
      from {
        transform: translateY(0) rotate(0deg);
        opacity: 0;
      }

      10% {
        opacity: .8;
      }

      to {
        transform: translateY(-110vh) rotate(30deg);
        opacity: 0;
      }
    }

    /* Celular pequeno */

    @media (max-width: 380px) {
      .envelope {
        width: 230px;
        height: 155px;
      }

      .flap {
        border-left-width: 115px;
        border-right-width: 115px;
      }

      .card {
        min-height: 470px;
        padding: 35px 23px;
      }

      .card h1 {
        font-size: 27px;
      }
    }
  </style>
</head>

<body>

  <!-- Estrelas -->
  <div class="stars" id="stars"></div>

  <!-- Tela inicial -->
  <section class="intro" id="intro">

    <p>
      Tem uma coisinha esperando por você...
    </p>

    <div class="envelope" id="envelope">

      <div class="envelope-body"></div>

      <div class="flap" id="flap"></div>

      <div class="heart">♡</div>

    </div>

    <div class="hint">
      toque no envelope
    </div>

  </section>


  <!-- Cartão -->
  <main class="card" id="card">

    <div class="small">
      uma mensagem para você
    </div>

    <h1>Ei, você. ♡</h1>

    <div class="message" id="message"></div>

    <div class="signature" id="signature">
      — com carinho, alguém que lembrou de você
    </div>

    <button class="music-button" id="heartButton">
      ♡ tocar novamente
    </button>

  </main>


  <script>

    /* =========================
       PERSONALIZE AQUI
       ========================= */

    const mensagem =
      "Eu poderia simplesmente ter mandado uma mensagem normal, " +
      "mas achei que você merecia uma pequena surpresa. " +
      "Então fiz esse cantinho só para te lembrar que você é uma pessoa especial. " +
      "Espero que esse pequeno gesto consiga colocar pelo menos um sorriso no seu rosto. ♡";


    /* =========================
       ESTRELAS
       ========================= */

    const stars = document.getElementById("stars");

    for (let i = 0; i < 100; i++) {

      const star = document.createElement("div");

      star.classList.add("star");

      star.style.left = Math.random() * 100 + "%";
      star.style.top = Math.random() * 100 + "%";

      star.style.animationDelay =
        Math.random() * 3 + "s";

      stars.appendChild(star);
    }


    /* =========================
       ABRIR ENVELOPE
       ========================= */

    const envelope = document.getElementById("envelope");
    const intro = document.getElementById("intro");
    const flap = document.getElementById("flap");
    const card = document.getElementById("card");

    envelope.addEventListener("click", () => {

      flap.style.transform = "rotateX(180deg)";

      setTimeout(() => {

        intro.classList.add("hidden");

        setTimeout(() => {

          card.classList.add("visible");

          escreverMensagem();

          criarCoracoes();

        }, 500);

      }, 700);

    });


    /* =========================
       EFEITO DE DIGITAÇÃO
       ========================= */

    const messageElement =
      document.getElementById("message");

    const signature =
      document.getElementById("signature");

    let index = 0;

    function escreverMensagem() {

      messageElement.innerHTML = "";
      signature.classList.remove("show");

      index = 0;

      function escrever() {

        if (index < mensagem.length) {

          messageElement.innerHTML +=
            mensagem.charAt(index);

          index++;

          setTimeout(escrever, 35);

        } else {

          setTimeout(() => {
            signature.classList.add("show");
          }, 500);

        }

      }

      escrever();
    }


    /* =========================
       CORAÇÕES FLUTUANDO
       ========================= */

    function criarCoracoes() {

      setInterval(() => {

        const heart =
          document.createElement("div");

        heart.classList.add("floating-heart");

        const simbolos = ["♡", "♥", "✦", "✧"];

        heart.innerHTML =
          simbolos[Math.floor(Math.random() * simbolos.length)];

        heart.style.left =
          Math.random() * 100 + "vw";

        heart.style.animationDuration =
          (5 + Math.random() * 5) + "s";

        heart.style.fontSize =
          (12 + Math.random() * 18) + "px";

        document.body.appendChild(heart);

        setTimeout(() => {
          heart.remove();
        }, 10000);

      }, 700);
    }


    /* =========================
       BOTÃO
       ========================= */

    document
      .getElementById("heartButton")
      .addEventListener("click", () => {

        criarCoracoes();

        const button =
          document.getElementById("heartButton");

        button.innerHTML = "♡ você recebeu carinho";

        setTimeout(() => {
          button.innerHTML = "♡ tocar novamente";
        }, 2000);

      });

  </script>

</body>
</html>