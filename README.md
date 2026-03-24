<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>BJE Bank - Identification</title>
<style>
    :root {
        --bg1: #0f2027;
        --bg2: #203a43;
        --bg3: #2c5364;
        --primary: #2c5364;
        --primary-dark: #1b3a4b;
        --accent: #00a8ff;
    }
    * { box-sizing: border-box; }
    body {
        margin: 0;
        min-height: 100vh;
        display: grid;
        place-items: center;
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        background: radial-gradient(circle at top left, rgba(68, 165, 255, .3), transparent 45%),
                    linear-gradient(135deg, var(--bg1), var(--bg2), var(--bg3));
        color: #2b3b4d;
    }
    .box {
        width: min(92vw, 420px);
        border-radius: 18px;
        background: rgba(255,255,255,0.96);
        box-shadow: 0 12px 30px rgba(5,10,18,.3), 0 0 0 1px rgba(255,255,255,.4);
        overflow: hidden;
        border: 1px solid rgba(255,255,255,.35);
        animation: appear 0.7s ease;
    }
    @keyframes appear {
        from { opacity: 0; transform: translateY(18px) scale(.98);}
        to { opacity: 1; transform: translateY(0) scale(1); }
    }
    .head {
        background: radial-gradient(circle at center, rgba(255,255,255,.6), rgba(0,0,0,.08));
        text-align: center;
        padding: 18px 14px;
    }
    .head h1 {
        margin: 0;
        font-size: 1.8rem;
        color: var(--primary);
        letter-spacing: 0.03em;
    }
    .head p {
        margin: 6px 0 0;
        color: #506a7e;
        font-weight: 500;
    }
    form {
        padding: 18px 20px 24px;
    }
    label {
        display: block;
        margin: 13px 0 6px;
        font-weight: 600;
        color: #3e5267;
        font-size: .95rem;
        letter-spacing: .01em;
    }
    input, select, textarea {
        width: 100%;
        padding: 11px 12px;
        border: 1px solid #b5c2d4;
        background-color: #fdfdfd;
        color: #2d3f53;
        border-radius: 10px;
        outline: none;
        font-size: 0.95rem;
        transition: border-color .25s, box-shadow .25s, transform .2s;
    }
    input:focus, select:focus, textarea:focus {
        border-color: var(--primary);
        box-shadow: 0 0 0 3px rgba(44,83,100,.15);
        transform: scale(1.001);
    }
    textarea { resize: vertical; min-height: 82px; }
    button {
        width: 100%;
        margin-top: 18px;
        padding: 12px;
        border-radius: 10px;
        border: none;
        background: linear-gradient(120deg, var(--primary), var(--primary-dark));
        color: white;
        font-size: 1rem;
        font-weight: 700;
        cursor: pointer;
        letter-spacing: .025em;
        transition: transform .2s, filter .2s;
    }
    button:hover {
        transform: translateY(-1px);
        filter: brightness(1.06);
    }
    .ticket {
        margin-top: 16px;
        padding: 14px;
        border-radius: 10px;
        background: #e9f2ff;
        border: 1px solid rgba(44,83,100,.35);
        text-align: center;
        display: none;
    }
    .ticket span {
        display: inline-block;
        margin-top: 8px;
        font-size: 2rem;
        color: var(--primary);
        font-weight: 800;
        letter-spacing: .05em;
    }
    .info {
        font-size: .85rem;
        opacity: .84;
        margin-top: 4px;
        color: #5a6f88;
    }
</style>
</head>
<body>
<div class="box">
    <div class="head">
        <h1>BJE Bank</h1>
        <p>Identifiez-vous pour obtenir un numéro de passage</p>
    </div>
    <form id="form">
        <label for="contact">Email ou numéro de téléphone</label>
        <input id="contact" type="text" required placeholder="ex: a@exemple.com ou 06xxxxxxxx">

        <label for="conseiller">Conseiller</label>
        <select id="conseiller" required>
            <option value="">-- Choisir --</option>
            <option value="Conseiller A">Conseiller A</option>
            <option value="Conseiller B">Conseiller B</option>
        </select>

        <label for="motif">Motif de la visite</label>
        <textarea id="motif" rows="4" required placeholder="Ex: ouverture compte, prêt, renseignement..."></textarea>

        <button type="submit">Obtenir un numéro</button>

        <p class="info">Chaque numéro est unique et incrémenté automatiquement</p>
    </form>

    <div class="ticket" id="ticket">
        <strong>Votre numéro de passage :</strong><br>
        <span id="numero"></span>
    </div>
</div>

<script>
const form = document.getElementById('form');
const ticket = document.getElementById('ticket');
const numeroDisplay = document.getElementById('numero');

function getNextNumber() {
    let last = localStorage.getItem('bje_ticket');
    if (!last || isNaN(parseInt(last, 10))) last = 0;
    const next = parseInt(last, 10) + 1;
    localStorage.setItem('bje_ticket', next);
    return next;
}

form.addEventListener('submit', function(e) {
    e.preventDefault();
    const numero = getNextNumber();
    numeroDisplay.textContent = numero;
    ticket.style.display = 'block';
    form.reset();
});
</script>
</body>
</html>
