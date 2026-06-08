
---

## 🏗️ Passo 1: Estruturando o HTML (`index.html`)

O HTML funciona como o esqueleto da nossa aplicação. Ele define onde cada elemento vai ficar antes de aplicarmos os estilos e a lógica.

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Mini E-commerce</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

    <header>
        <h1>Loja Virtual JS</h1>
        <div id="carrinho-info">
            🛒 Itens: <span id="quantidade">0</span>
        </div>
    </header>

    <main>
        <section id="produtos"></section>

        <aside>
            <h2>Carrinho</h2>
            <ul id="lista-carrinho"></ul>

            <div class="total-box">
                <h3>Total</h3>
                <strong>R$ <span id="total">0.00</span></strong>
            </div>
        </aside>
    </main>

    <script src="script.js"></script>

</body>
</html>

```

---

## 🎨 Passo 2: Estilizando com CSS (`style.css`)

O CSS aplica a identidade visual do projeto, utilizando variáveis para manter a paleta de cores organizada, Flexbox/Grid para o layout responsivo e pequenas animações para melhorar a experiência do usuário.

```css
/* Importação de fontes externas do Google Fonts */
@import url('https://fonts.googleapis.com/css2?family=Sora:wght@400;600;700&family=DM+Sans:wght@400;500&display=swap');

/* Reset básico para remover margens padrão e configurar o box-sizing */
*, *::before, *::after {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

/* Definição de variáveis globais (Custom Properties) para fácil manutenção de cores e padrões */
:root {
    --blue:       #1e88e5;
    --blue-dark:  #1565c0;
    --green:      #2e7d32;
    --green-light:#43a047;
    --bg:         #eef2f7;
    --white:      #ffffff;
    --text:       #1a1a2e;
    --muted:      #6b7280;
    --radius:     14px;
    --shadow:     0 4px 20px rgba(0,0,0,.09);
    --transition: .2s ease;
}

body {
    font-family: 'DM Sans', sans-serif;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
}

/* ── HEADER ── */
header {
    background: linear-gradient(135deg, var(--blue-dark), var(--blue));
    color: #fff;
    padding: 18px 32px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    box-shadow: 0 2px 12px rgba(30,136,229,.4);
    position: sticky; /* Mantém o cabeçalho fixo no topo ao rolar a página */
    top: 0;
    z-index: 100;
}

header h1 {
    font-family: 'Sora', sans-serif;
    font-size: 1.5rem;
    font-weight: 700;
    letter-spacing: -.3px;
}

#carrinho-info {
    display: flex;
    align-items: center;
    gap: 8px;
    background: rgba(255,255,255,.15);
    border: 1px solid rgba(255,255,255,.25);
    padding: 8px 16px;
    border-radius: 99px;
    font-size: .9rem;
    font-weight: 500;
    backdrop-filter: blur(6px); /* Efeito de vidro borrado atrás do elemento */
    transition: background var(--transition);
}

#carrinho-info:hover {
    background: rgba(255,255,255,.25);
}

#quantidade {
    background: #fff;
    color: var(--blue-dark);
    font-weight: 700;
    font-size: .78rem;
    width: 22px;
    height: 22px;
    border-radius: 50%;
    display: inline-flex;
    align-items: center;
    justify-content: center;
}

/* ── LAYOUT PRINCIPAL ── */
main {
    display: flex;
    padding: 28px 32px;
    gap: 24px;
    align-items: flex-start;
}

/* ── VITRINE DE PRODUTOS ── */
#produtos {
    flex: 3; /* Ocupa 3/4 do espaço disponível */
    display: grid;
    /* Cria colunas dinâmicas que se ajustam sozinhas com tamanho mínimo de 200px */
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 20px;
}

.card {
    background: var(--white);
    padding: 20px;
    border-radius: var(--radius);
    box-shadow: var(--shadow);
    display: flex;
    flex-direction: column;
    gap: 10px;
    transition: transform var(--transition), box-shadow var(--transition);
}

.card:hover {
    transform: translateY(-4px); /* Efeito sutil de flutuação ao passar o mouse */
    box-shadow: 0 10px 30px rgba(0,0,0,.13);
}

.card h3 {
    font-family: 'Sora', sans-serif;
    font-size: 1rem;
    font-weight: 600;
    color: var(--text);
}

.card p {
    font-size: .95rem;
    font-weight: 500;
    color: var(--blue-dark);
}

.card button {
    margin-top: auto; /* Empurra o botão sempre para o final do card, alinhando-os */
    width: 100%;
    padding: 10px;
    background: var(--green);
    color: #fff;
    border: none;
    border-radius: 8px;
    font-family: 'DM Sans', sans-serif;
    font-size: .88rem;
    font-weight: 500;
    cursor: pointer;
    transition: background var(--transition), transform var(--transition);
}

.card button:hover {
    background: var(--green-light);
    transform: scale(1.02);
}

.card button:active {
    transform: scale(.98);
}

/* ── LATERAL DO CARRINHO ── */
aside {
    flex: 1; /* Ocupa 1/4 do espaço disponível */
    min-width: 260px;
    background: var(--white);
    border-radius: var(--radius);
    box-shadow: var(--shadow);
    padding: 24px;
    position: sticky; /* O carrinho acompanha a rolagem da tela */
    top: 80px;
}

aside h2 {
    font-family: 'Sora', sans-serif;
    font-size: 1.15rem;
    font-weight: 700;
    margin-bottom: 16px;
    padding-bottom: 12px;
    border-bottom: 2px solid var(--bg);
    color: var(--text);
}

#lista-carrinho {
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: 10px;
    min-height: 40px;
    margin-bottom: 20px;
}

#lista-carrinho li {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 8px;
    background: var(--bg);
    padding: 10px 12px;
    border-radius: 8px;
    font-size: .88rem;
    font-weight: 500;
    color: var(--text);
    animation: slideIn .2s ease; /* Animação ao surgir um novo item */
}

/* Keyframes para a animação de entrada de itens no carrinho */
@keyframes slideIn {
    from { opacity: 0; transform: translateX(10px); }
    to   { opacity: 1; transform: translateX(0); }
}

#lista-carrinho li button {
    background: #fee2e2;
    color: #dc2626;
    border: none;
    border-radius: 6px;
    width: 26px;
    height: 26px;
    cursor: pointer;
    font-size: .8rem;
    font-weight: 700;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
    transition: background var(--transition);
}

#lista-carrinho li button:hover {
    background: #fca5a5;
}

/* ── CAIXA DE TOTALIZAÇÃO ── */
.total-box {
    border-top: 2px solid var(--bg);
    padding-top: 16px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.total-box h3 {
    font-family: 'Sora', sans-serif;
    font-size: .95rem;
    font-weight: 600;
    color: var(--muted);
    text-transform: uppercase;
    letter-spacing: .5px;
}

.total-box strong {
    font-family: 'Sora', sans-serif;
    font-size: 1.3rem;
    font-weight: 700;
    color: var(--blue-dark);
}

/* ── RESPONSIVIDADE (Telas menores) ── */
@media (max-width: 700px) {
    main { 
        flex-direction: column; /* Coloca o carrinho abaixo dos produtos em telas pequenas */
        padding: 16px; 
    }
    aside { 
        position: static; 
        width: 100%; 
    }
    header { 
        padding: 14px 16px; 
    }
}

```

---

## 🧠 Passo 3: Programando a Lógica (`script.js`)

O JavaScript gerencia o estado da aplicação: lê os dados salvos no navegador, renderiza a lista de produtos, processa a adição/remoção de itens e recalcula os valores dinamicamente.

```javascript
// 1. Inicialização do Estado
// Tenta buscar o carrinho salvo no LocalStorage. Se não existir, inicia como um array vazio [].
let carrinho = JSON.parse(localStorage.getItem("carrinho")) || [];

// 2. Banco de Dados Simulado
// Array de objetos representando os produtos disponíveis na loja
const produtos = [
    { id: 1, nome: "Notebook",        preco: 3500 },
    { id: 2, nome: "Mouse Gamer",     preco: 150  },
    { id: 3, nome: "Teclado Mecânico",preco: 300  },
    { id: 4, nome: "Monitor",         preco: 900  }
];

// Captura a seção do HTML onde os produtos serão inseridos
const areaProdutos = document.getElementById("produtos");

// 3. Renderização da Vitrine de Produtos
// Mapeia o array de produtos transformando cada um em um bloco HTML (card)
function renderizarProdutos() {
    areaProdutos.innerHTML = produtos.map(produto => `
        <div class="card">
            <h3>${produto.nome}</h3>
            <p>R$ ${produto.preco.toFixed(2)}</p>
            <button onclick="adicionarCarrinho(${produto.id})">Adicionar</button>
        </div>
    `).join(""); // O .join("") remove as vírgulas geradas pelo método .map()
}

// Executa a função imediatamente para desenhar a vitrine na tela
renderizarProdutos();

// 4. Adicionar Item ao Carrinho
function adicionarCarrinho(id) {
    // Procura no "banco de dados" o produto que possui o ID clicado
    const produto = produtos.find(p => p.id === id);
    // Adiciona uma cópia do produto ao array do carrinho
    carrinho.push(produto);
    // Dispara a rotina de salvamento e atualização visual
    salvarEAtualizar();
}

// 5. Remover Item do Carrinho
function removerItem(index) {
    // Remove 1 item do array com base no seu índice de posição
    carrinho.splice(index, 1);
    // Dispara a rotina de salvamento e atualização visual
    salvarEAtualizar();
}

// 6. Atualizar a Interface do Carrinho
function atualizarCarrinho() {
    const lista = document.getElementById("lista-carrinho");
    lista.innerHTML = ""; // Limpa o HTML interno antigo para evitar duplicados

    // Percorre o carrinho atual e reconstrói a lista do HTML com os novos itens
    carrinho.forEach((item, index) => {
        lista.innerHTML += `
            <li>
                ${item.nome} - R$ ${item.preco.toFixed(2)}
                <button onclick="removerItem(${index})">X</button>
            </li>
        `;
    });

    // Chama a função para recalcular o valor financeiro total
    atualizarTotal();
}

// 7. Calcular Valores de Totalização
function atualizarTotal() {
    // Usa o .reduce() para somar a propriedade 'preco' de todos os itens do carrinho
    const total = carrinho.reduce((soma, item) => soma + item.preco, 0);
    
    // Atualiza os textos do HTML com duas casas decimais fixas (.toFixed(2))
    document.getElementById("total").textContent = total.toFixed(2);
    // Atualiza a bolinha de quantidade de itens no cabeçalho
    document.getElementById("quantidade").textContent = carrinho.length;
}

// 8. Persistência de Dados e Sincronização
function salvarEAtualizar() {
    // Converte o array para texto JSON e salva no armazenamento local do navegador
    localStorage.setItem("carrinho", JSON.stringify(carrinho));
    // Redesenha o carrinho na interface visual
    atualizarCarrinho();
}

// 9. Inicialização da Interface
// Ao carregar ou recarregar a página, lê o que estava no LocalStorage e exibe em tela
atualizarCarrinho();

```
