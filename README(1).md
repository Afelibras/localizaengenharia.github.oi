# 🏢 NavInterna — Navegação de Ambientes Internos

> App de navegação indoor baseado em planta baixa, com rota animada via SVG, modo debug para calibração e pronto para deploy no GitHub Pages — tudo em um único arquivo HTML.

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=flat&logo=tailwind-css&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![GitHub Pages](https://img.shields.io/badge/GitHub_Pages-222222?style=flat&logo=github&logoColor=white)

---

## ✨ Funcionalidades

- **Upload de planta baixa** — arraste ou clique para carregar `.jpg` / `.png`
- **Seleção de origem** — escolha o QR Code / placa onde o usuário está
- **Seleção de destino** — escolha a sala ou local de chegada
- **Rota SVG animada** — linha Bezier com gradiente, marcadores de origem e destino
- **Referência de localização** — cada QR Code exibe "Você está perto de…"
- **Instruções passo a passo** — listagem textual da rota no painel lateral
- **Modo Debug** — clique na imagem para capturar coordenadas `x, y` e calibrar novos pontos
- **Totalmente responsivo** — funciona em desktop e mobile

---

## 🚀 Deploy no GitHub Pages

### 1. Fork ou clone este repositório

```bash
git clone https://github.com/seu-usuario/navinterna.git
cd navinterna
```

### 2. Confirme que o arquivo está na raiz

```
navinterna/
└── index.html   ← único arquivo necessário
└── README.md
```

### 3. Ative o GitHub Pages

1. Vá em **Settings → Pages** no seu repositório
2. Em *Source*, selecione **Deploy from a branch**
3. Escolha a branch `main` e pasta `/ (root)`
4. Clique em **Save**

Em alguns minutos o site estará disponível em:
```
https://seu-usuario.github.io/navinterna/
```

---

## 🗺️ Como usar o app

1. **Carregue a planta** do andar clicando na área de upload ou arrastando a imagem
2. **Selecione o QR Code** que o usuário escaneou (ponto de origem)
3. **Selecione o destino** (sala ou local)
4. Clique em **Traçar Rota**
5. Acompanhe a rota animada no mapa e as instruções no painel lateral

---

## 🔧 Calibração de Coordenadas (Modo Debug)

As coordenadas dos pontos são armazenadas em **pixels naturais da imagem** — funcionam independentemente do tamanho de tela.

### Passo a passo

1. Suba a planta real no app
2. Ative o **Modo Debug** (botão no canto superior direito do header)
3. Clique em cada ponto que deseja mapear (porta, QR Code, sala)
4. As coordenadas aparecem:
   - **No console do navegador** (`F12 → Console`)
   - **No painel lateral** (seção Debug)
   - **Flutuando na tela** por 3 segundos
5. Copie os valores `{ x, y }` e cole no objeto `LOCATIONS` dentro do `<script>`

```
🎯 x: 380  y: 180  (natural)   rx: 190  ry: 90 (rendered)
     ↑ use estes                ↑ ignore (dependem do zoom)
```

---

## ⚙️ Configuração do objeto `LOCATIONS`

Abra o `index.html` em qualquer editor e localize o objeto `LOCATIONS` dentro da tag `<script>`:

```js
const LOCATIONS = {
  origins: [
    {
      id: "qr_recepcao",          // identificador único
      name: "QR – Recepção",      // nome exibido no select
      x: 120,                     // coordenada X (pixel natural)
      y: 200,                     // coordenada Y (pixel natural)
      ref: "📶 Você está perto da Recepção",  // referência de localização
      instruction: "Texto exibido ao usuário após escanear.",
    },
    // adicione mais origens...
  ],

  destinations: [
    {
      id: "sala_reuniao_a",
      name: "Sala de Reunião A",
      x: 180,
      y: 120,
      instruction: "Sala de Reunião A – Capacidade 8 pessoas",
      steps: [
        "Vire à direita saindo do ponto de origem",
        "Siga pelo corredor principal ~15m",
        "A Sala A fica na primeira porta à esquerda",
      ],
    },
    // adicione mais destinos...
  ],
};
```

### Propriedades

| Propriedade | Tipo | Descrição |
|---|---|---|
| `id` | `string` | Identificador único (sem espaços) |
| `name` | `string` | Rótulo exibido nos dropdowns |
| `x` | `number` | Posição horizontal em pixels naturais |
| `y` | `number` | Posição vertical em pixels naturais |
| `ref` | `string` | *(só origins)* Referência próxima exibida no card |
| `instruction` | `string` | Texto de apoio exibido ao selecionar |
| `steps` | `string[]` | *(só destinations)* Lista de instruções da rota |

---

## 🛠️ Tecnologias

| Tecnologia | Uso |
|---|---|
| HTML5 | Estrutura e Canvas/SVG |
| Tailwind CSS (CDN) | Estilização utilitária |
| JavaScript Vanilla | Lógica de rota e interação |
| SVG | Overlay animado da rota |
| Google Fonts | DM Sans + DM Mono |

Nenhum framework, nenhum bundler, nenhuma dependência instalada. Zero configuração de build.

---

## 📁 Estrutura do Projeto

```
navinterna/
├── index.html    # App completo (HTML + CSS + JS em um único arquivo)
└── README.md     # Esta documentação
```

---

## 🤝 Contribuindo

1. Fork o projeto
2. Crie uma branch: `git checkout -b feature/minha-melhoria`
3. Commit suas mudanças: `git commit -m 'feat: adiciona roteamento por waypoints'`
4. Push: `git push origin feature/minha-melhoria`
5. Abra um Pull Request

### Melhorias sugeridas

- [ ] Roteamento com waypoints intermediários
- [ ] Suporte a múltiplos andares / plantas
- [ ] QR Code gerado dinamicamente para cada origem
- [ ] Exportar configuração de pontos como JSON
- [ ] Modo de edição visual com drag-and-drop dos pontos

---

## 📄 Licença

MIT © 2025 — livre para uso pessoal e comercial.
