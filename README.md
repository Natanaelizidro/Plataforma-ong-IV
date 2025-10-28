index.html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Instituto Arara Azul</title>
  <link rel="stylesheet" href="css/style.css">
</head>
<body>
  <header>
    <img src="img/logo.png" alt="Logo Instituto Arara Azul" class="logo">

    <nav>
      <div class="hamburger" onclick="toggleMenu()" tabindex="0" aria-label="Abrir menu">
        <span></span><span></span><span></span>
      </div>
      <ul id="nav-links">
        <li><a href="index.html">Início</a></li>
        <li><a href="projetos.html">Projetos</a></li>
        <li><a href="cadastro.html">Cadastro</a></li>
      </ul>
    </nav>

    <div class="modo-acessibilidade">
      <button onclick="toggleDarkMode()">🌙 Modo Escuro</button>
      <button onclick="toggleHighContrast()">🔳 Alto Contraste</button>
    </div>
  </header>

  <main id="conteudo">
    <!-- SPA - conteúdo carregado dinamicamente -->
  </main>

  <footer>
    <p>&copy; 2025 Instituto Arara Azul. Todos os direitos reservados.</p>
  </footer>

  <script src="js/script.js" defer></script>
</body>
</html>
css/style.css
:root {
  --azul-escuro: #003366;
  --azul-claro: #3399ff;
  --branco: #ffffff;
  --cinza: #f4f4f4;
  --preto: #000000;
}

body {
  font-family: Arial, sans-serif;
  margin: 0;
  background: var(--cinza);
  color: var(--azul-escuro);
}

header, footer {
  background: var(--azul-escuro);
  color: var(--branco);
  padding: 10px 20px;
}

.logo {
  height: 60px;
}

header nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

header nav ul {
  list-style: none;
  display: flex;
  gap: 15px;
  margin: 0;
  padding: 0;
}

header nav ul li a {
  color: var(--branco);
  text-decoration: none;
  font-weight: bold;
}

.hamburger {
  display: none;
  flex-direction: column;
  cursor: pointer;
}

.hamburger span {
  height: 3px;
  width: 25px;
  background: var(--branco);
  margin-bottom: 5px;
  border-radius: 2px;
}

main {
  padding: 20px;
}

.card {
  background: var(--branco);
  padding: 15px;
  margin: 10px 0;
  border-radius: 5px;
  box-shadow: 0 0 5px rgba(0,0,0,0.2);
}

.card img {
  width: 100%;
  height: auto;
  border-radius: 5px;
}

form {
  background: var(--branco);
  padding: 20px;
  border-radius: 5px;
  box-shadow: 0 0 5px rgba(0,0,0,0.1);
}

input, button {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
  border-radius: 4px;
  border: 1px solid #ccc;
}

button {
  background: var(--azul-claro);
  color: var(--branco);
  border: none;
  cursor: pointer;
  font-weight: bold;
}

button:hover {
  background: #0077cc;
}

.modo-acessibilidade {
  display: flex;
  gap: 10px;
  margin-top: 10px;
}

/* Responsividade */
@media (max-width: 768px) {
  header nav ul {
    display: none;
    flex-direction: column;
    position: absolute;
    top: 80px;
    right: 0;
    background: var(--azul-escuro);
    width: 200px;
    padding: 10px;
  }

  header nav ul.show {
    display: flex;
  }

  .hamburger {
    display: flex;
  }
}

/* Modo Escuro */
body.dark-mode {
  background: #1c1c1c;
  color: var(--branco);
}

body.dark-mode header, body.dark-mode footer {
  background: #000;
}

/* Alto Contraste */
body.high-contrast {
  background: var(--preto);
  color: var(--branco);
}

body.high-contrast a {
  color: yellow;
}

body.high-contrast header, body.high-contrast footer {
  background: var(--preto);
  color: yellow;
}
js/script.js
// =============================
// MENU HAMBÚRGUER
// =============================
function toggleMenu() {
  const navLinks = document.getElementById("nav-links");
  navLinks.classList.toggle("show");
}

// =============================
// MODO ESCURO / ALTO CONTRASTE
// =============================
function toggleDarkMode() {
  document.body.classList.toggle("dark-mode");
  localStorage.setItem("darkMode", document.body.classList.contains("dark-mode"));
}

function toggleHighContrast() {
  document.body.classList.toggle("high-contrast");
  localStorage.setItem("highContrast", document.body.classList.contains("high-contrast"));
}

document.addEventListener("DOMContentLoaded", () => {
  if (localStorage.getItem("darkMode") === "true") document.body.classList.add("dark-mode");
  if (localStorage.getItem("highContrast") === "true") document.body.classList.add("high-contrast");
});

// =============================
// TEMPLATES (SPA)
// =============================
const templates = {
  inicio: `
    <section tabindex="0">
      <h1>Bem-vindo ao Instituto Arara Azul</h1>
      <p>Missão: Proteger araras-azuis e outros animais silvestres.</p>
      <p>Visão: Um mundo onde a fauna brasileira é respeitada e preservada.</p>
      <p>Valores: Ética, transparência e amor à natureza.</p>
      <img src="img/voluntario.jpg" alt="Equipe do Instituto" />
    </section>
  `,
  projetos: `
    <section tabindex="0">
      <h1>Oportunidades de Voluntariado</h1>
      <div class="card">
        <img src="img/projeto1.jpg" alt="Projeto 1" />
        <h3>Projeto de Conservação de Araras</h3>
        <p>Participe do resgate e preservação de araras-azuis.</p>
      </div>
      <div class="card">
        <img src="img/projeto1.jpg" alt="Projeto 2" />
        <h3>Campanha de Educação Ambiental</h3>
        <p>Ajude a conscientizar comunidades locais sobre fauna e flora.</p>
      </div>
    </section>
  `,
  cadastro: `
    <section tabindex="0">
      <h1>Cadastro de Voluntários / Doadores</h1>
      <form id="cadastroForm">
        <fieldset>
          <legend>Informações Pessoais</legend>
          <label for="nome">Nome:</label>
          <input type="text" id="nome" required />
          <label for="email">E-mail:</label>
          <input type="email" id="email" required />
          <label for="telefone">Telefone:</label>
          <input type="tel" id="telefone" placeholder="(00) 00000-0000" required />
        </fieldset>
        <fieldset>
          <legend>Endereço</legend>
          <label for="cidade">Cidade:</label>
          <input type="text" id="cidade" required />
          <label for="estado">Estado:</label>
          <input type="text" id="estado" required />
        </fieldset>
        <button type="submit">Cadastrar</button>
      </form>
    </section>
  `
};

function loadPage(page) {
  const main = document.getElementById("conteudo");
  main.innerHTML = templates[page];
  localStorage.setItem("ultimaPagina", page);
  if (page === "cadastro") configurarFormulario();
}

// =============================
// NAVEGAÇÃO SPA
// =============================
document.addEventListener("DOMContentLoaded", () => {
  const ultima = localStorage.getItem("ultimaPagina") || "inicio";
  loadPage(ultima);

  document.querySelectorAll("nav a").forEach(link => {
    link.addEventListener("click", function (e) {
      e.preventDefault();
      const page = this.getAttribute("href").replace(".html", "");
      loadPage(page);
      toggleMenu();
    });
  });
});

// =============================
// FORMULÁRIO + LOCAL STORAGE
// =============================
function configurarFormulario() {
  const form = document.getElementById("cadastroForm");
  form.addEventListener("submit", e => {
    e.preventDefault();

    const dados = {
      nome: form.nome.value.trim(),
      email: form.email.value.trim(),
      telefone: form.telefone.value.trim(),
      cidade: form.cidade.value.trim(),
      estado: form.estado.value.trim()
    };

    if (Object.values(dados).includes("")) {
      alert("⚠️ Preencha todos os campos!");
      return;
    }

    const emailOk = /^[^@\s]+@[^@\s]+\.[^@\s]+$/.test(dados.email);
    const telOk = /^\(\d{2}\)\s?\d{4,5}-\d{4}$/.test(dados.telefone);

    if (!emailOk) return alert("⚠️ E-mail inválido!");
    if (!telOk) return alert("⚠️ Telefone no formato (00) 00000-0000!");

    const cadastros = JSON.parse(localStorage.getItem("cadastros")) || [];
    cadastros.push(dados);
    localStorage.setItem("cadastros", JSON.stringify(cadastros));

    alert("✅ Cadastro realizado com sucesso!");
    form.reset();
  });
}
