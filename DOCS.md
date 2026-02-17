# DOCS — DevLinks (Projeto Discovery)

## ✨ Visão geral

Um cartão de visitas online simples e responsivo que reúne links e redes sociais. Implementa alternância de tema (claro/escuro) via `class` no elemento `html`, CSS variables e uma pequena lógica em JavaScript para trocar o avatar.

---

## 📁 Estrutura do projeto

- `index.html` — marcação principal, inclui `#switch`, `#profile`, lista de links e `#social-links` (Ionicons).
- `style.css` — variáveis CSS, tema (`:root` + `html.light`), responsividade e animações do switch.
- `script.js` — função `toggleMode()` que alterna o tema e troca a imagem do perfil.
- `assets/` — imagens (backgrounds, avatar, ícones SVG usados no switch).
- `README.md`, `LICENSE` — documentação e licença do projeto.

---

## ✅ Funcionalidades

- Tema claro/escuro com transições suaves.
- Troca de avatar conforme tema.
- Layout responsivo (mobile → desktop).
- Links com target="\_blank" para abrir em nova aba.
- Íconescomm via Ionicons.

---

## 🔧 Como o tema funciona (técnico)

- Variáveis CSS definidas em `:root` e sobrescritas em `html.light`.
- `toggleMode()` adiciona/remove `class="light"` no `document.documentElement`.
- A imagem do perfil é atualizada no JS para manter consistência visual.

Exemplo (trecho atual em `script.js`):

```javascript
function toggleMode() {
  const html = document.documentElement;
  html.classList.toggle("light");

  const image = document.querySelector("#profile img");
  if (html.classList.contains("light")) {
    image.setAttribute("src", "./assets/avatar-light.png");
  } else {
    image.setAttribute("src", "./assets/avatar.png");
  }
}
```

---

## ▶️ Rodando localmente (Windows)

- Abrir `index.html` diretamente ou usar Live Server (VS Code).
- Servidor simples com Python:

```powershell
python -m http.server 5500
# abrir http://localhost:5500
```

- Ou usar `npx serve` / `npx http-server`.

---

## ♻️ Reaplicando esse padrão em outro projeto (passo a passo)

1. Copie `index.html`, `style.css`, `script.js` e a pasta `assets/` para o novo projeto.
2. Mantenha os IDs `#switch` e `#profile` (são usados no CSS/JS).
3. Atualize as imagens em `assets/` e os links dentro do `ul`/`#social-links`.
4. Teste a alternância de tema e verifique a troca do avatar.
5. Ajuste cores e textos conforme sua identidade visual.

---

## 💡 Melhorias recomendadas (próximos passos de estudo)

- Persistir escolha do tema no `localStorage` (mantém preferência do usuário).
- Tornar o switch acessível (ARIA, suporte a teclado e foco visível).
- Permitir edição dinâmica dos links (salvar em `localStorage`).
- Validar contraste e aprimorar acessibilidade.

Trecho para persistir tema (exemplo):

```javascript
// após carregar a página
if (localStorage.getItem("theme") === "light") {
  document.documentElement.classList.add("light");
  document.querySelector("#profile img").src = "./assets/avatar-light.png";
}

function toggleMode() {
  document.documentElement.classList.toggle("light");
  const isLight = document.documentElement.classList.contains("light");
  localStorage.setItem("theme", isLight ? "light" : "dark");
  document.querySelector("#profile img").src = isLight
    ? "./assets/avatar-light.png"
    : "./assets/avatar.png";
}
```

Sugestão de markup acessível para o switch:

```html
<div
  id="switch"
  role="switch"
  tabindex="0"
  aria-checked="false"
  onclick="toggleMode()"
  onkeydown="if(event.key==='Enter'||event.key===' ') toggleMode()"
>
  <button aria-hidden="true"></button>
  <span></span>
</div>
```

No JS, atualize `aria-checked` sempre que trocar o tema.

---

## 🔎 Checklist rápido antes de reaplicar

- [ ] Testar responsividade (mobile/desktop).
- [ ] Verificar atributos `alt` das imagens.
- [ ] Testar navegação por teclado e ARIA do switch.
- [ ] Validar contraste das cores (acessibilidade).
- [ ] Garantir que links externos usem `target="_blank"` com `rel="noopener"` se desejar segurança.

---

## 📦 Comandos Git úteis

```bash
git add DOCS.md
git commit -m "Add DOCS.md — documentação do projeto"
git push
```

---

## Créditos

Feito como exercício do curso Rocketseat. Autor: `Thiago Fernandes`.

---

Se quiser, eu também posso: atualizar o `README.md` com um link para o `DOCS.md` e/ou commitar e dar push para você. Deseja que eu faça isso agora?
