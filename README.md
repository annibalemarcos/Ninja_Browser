# 🥷 Inspector Ninja Browser

**Inspector Ninja Browser** é um navegador desktop leve feito com **Electron**, criado para inspecionar páginas, capturar seletores, listar elementos HTML e medir distância entre componentes visuais direto na tela.

A ideia é simples e poderosa: abrir uma página, clicar nos elementos e copiar rapidamente informações úteis para desenvolvimento, automação, scraping, QA, testes visuais ou documentação técnica.

> Status: projeto funcional em versão inicial/experimental. Ainda pode evoluir bastante, mas já entrega uma caixa de ferramentas bem útil para inspeção visual e técnica de páginas.

---

## ✨ O que ele faz

- 🌐 Abre páginas em uma janela desktop própria usando Electron.
- 🔎 Inspeciona elementos com clique direito dentro da página carregada.
- 📋 Copia dados do elemento para a área de transferência.
- 🎯 Gera seletores úteis como CSS Selector, CSS Path e XPath.
- 🧱 Lista todos os elementos visíveis/coletáveis da página.
- 💾 Exporta a lista de elementos para um arquivo `.txt`.
- 📐 Mede distância, posição e tamanho entre dois elementos usando uma régua visual.
- 📟 Possui console interno para mensagens, eventos e logs do app.
- 🧭 Inclui navegação básica: voltar, avançar, recarregar e barra de endereço/busca.

---

## 🧰 Tecnologias usadas

- **Electron**
- **JavaScript**
- **HTML5**
- **CSS3**
- **Electron Builder** para empacotamento

---

## 📸 Visão geral da interface

A interface é composta por:

- uma barra superior com logo, navegação e campo de URL;
- botão **Element Inspector** para listar elementos da página;
- botão de **régua** para medir entre dois elementos;
- botão de **console** para abrir/fechar logs internos;
- painel lateral de inspeção;
- área principal com o navegador embutido.

Visualmente, o projeto usa um tema escuro com detalhes roxos/neon. Ninja raiz, mas sem virar carnaval de CSS.

---

## 🚀 Como rodar em modo desenvolvimento

### 1. Clone o repositório

```bash
git clone https://github.com/SEU-USUARIO/SEU-REPOSITORIO.git
cd SEU-REPOSITORIO
```

### 2. Instale as dependências

```bash
npm install
```

### 3. Rode o app

```bash
npm start
```

Ou, para abrir com DevTools do Electron:

```bash
npm run dev
```

> Observação: este projeto é um app desktop Electron. Ele não roda em uma porta HTTP como `3030`, `5442` ou similares. Ele abre uma janela própria do navegador.

---

## 📦 Como gerar executável

### Windows

```bash
npm run build:win
```

Os arquivos finais serão gerados na pasta:

```bash
dist/
```

A configuração atual gera dois formatos para Windows:

- instalador **NSIS**;
- versão **portable**.

---

### macOS

```bash
npm run build:mac
```

Gera um pacote `.dmg`.

---

### Linux

```bash
npm run build:linux
```

Gera pacotes nos formatos:

- `AppImage`;
- `.deb`.

---

### Todos os sistemas

```bash
npm run build:all
```

---

## 🎮 Como usar

### Navegar

Digite uma URL ou termo de busca na barra superior.

Exemplos:

```text
https://example.com
```

```text
botões bootstrap
```

Se o texto não parecer uma URL, o app transforma em busca no Google.

---

### Inspecionar um elemento individual

1. Abra uma página.
2. Clique com o botão direito sobre qualquer elemento.
3. O painel lateral abrirá com dados técnicos do item.

O painel pode mostrar:

- texto visível;
- link direto ou link do elemento pai;
- `src` de imagens;
- `alt`, `title`, `value` e `placeholder`;
- XPath relativo;
- XPath absoluto;
- CSS Selector;
- CSS Path;
- tag HTML;
- classes;
- ID;
- HTML completo do elemento.

Cada campo possui botão de copiar.

---

### Listar todos os elementos da página

Clique em:

```text
🥷 Element Inspector
```

O app coleta elementos da página e exibe uma lista com:

- tag;
- ID;
- classes;
- CSS Path;
- índice do elemento;
- botão para copiar individualmente.

Por segurança/performance, a coleta é limitada a até **2000 elementos**.

---

### Exportar elementos para TXT

Depois de listar os elementos, clique em:

```text
💾 Salvar todos os elementos em TXT
```

O arquivo exportado inclui:

- URL da página;
- título da página;
- data/hora da exportação;
- quantidade de elementos;
- CSS Path;
- texto;
- trecho de HTML.

---

### Usar a régua

1. Clique no botão **📐**.
2. Clique com o botão direito no primeiro elemento.
3. Clique com o botão direito no segundo elemento.
4. Veja as medidas no painel flutuante.

A régua mostra:

- distância horizontal entre elementos;
- distância vertical entre elementos;
- diferença de posição `left` e `top`;
- distância entre centros;
- tamanho do elemento A;
- tamanho do elemento B.

Também é possível copiar o resultado da medição.

---

### Console interno

Clique no botão:

```text
📟
```

Ele abre ou oculta o console interno do app, usado para logs como:

- página carregada;
- erro de navegação;
- elemento copiado;
- régua ativada/desativada;
- exportação concluída.

---

## 📁 Estrutura do projeto

```text
.
├── assets/
│   └── icon.png
├── src/
│   ├── index.html
│   ├── renderer.js
│   └── style.css
├── main.js
├── preload.js
├── package.json
├── package-lock.json
├── yarn.lock
└── README.md
```

### Arquivos principais

| Arquivo | Função |
|---|---|
| `main.js` | Inicializa o Electron e cria a janela principal. |
| `preload.js` | Expõe APIs seguras para o renderer, como copiar para clipboard. |
| `src/index.html` | Estrutura visual do app. |
| `src/renderer.js` | Controla navegação, inspeção, exportação, console e régua. |
| `src/style.css` | Estilos da interface. |
| `package.json` | Scripts, dependências e configuração de build. |

---

## 📜 Scripts disponíveis

```bash
npm start
```

Inicia o app.

```bash
npm run dev
```

Inicia o app e abre o DevTools do Electron em modo separado.

```bash
npm run build:win
```

Gera build para Windows.

```bash
npm run build:mac
```

Gera build para macOS.

```bash
npm run build:linux
```

Gera build para Linux.

```bash
npm run build:all
```

Gera builds para múltiplas plataformas.

---

## ⚠️ Limitações conhecidas

- Algumas páginas podem bloquear execução, inspeção ou carregamento por políticas de segurança.
- O app depende do comportamento do `<webview>` do Electron.
- A coleta de todos os elementos é limitada a 2000 itens para evitar travamentos.
- Ainda não há sistema de abas.
- Ainda não há favoritos, histórico avançado ou gerenciamento de perfis.
- O projeto ainda não possui testes automatizados.

---

## 🧭 Ideias para próximas versões

- Sistema de abas.
- Favoritos e histórico local.
- Exportação em JSON/CSV além de TXT.
- Busca/filtro dentro da lista de elementos.
- Destaque visual do elemento selecionado na página.
- Modo claro/escuro.
- Captura de screenshot com marcações.
- Copiar seletores em formato Playwright, Puppeteer ou Selenium.
- Painel de atributos editável.
- Suporte a múltiplas janelas/instâncias.

---

## 🛡️ Segurança

O projeto usa boas práticas básicas do Electron:

- `contextIsolation: true`
- `nodeIntegration: false`
- `preload.js` para expor apenas APIs necessárias

Mesmo assim, como o app carrega páginas externas dentro de um `webview`, é importante revisar permissões e políticas antes de usar em ambiente sensível.

---

## 📄 Licença

Este projeto está licenciado sob a licença **MIT**.

---

## 👤 Autor

Projeto desenvolvido por **Inspector Ninja Team**.

---

## 🥷 Resumo em uma frase

Um navegador desktop para quem precisa inspecionar, copiar, medir e mapear elementos de páginas sem ficar brigando com DevTools tradicional toda hora.
