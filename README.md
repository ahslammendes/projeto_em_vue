# Museu 3D de PCs Retrô

Visualizador 3D interativo, no navegador, de quatro computadores clássicos (1984–2001). Clique em um PC para ver a câmera aproximar e ler a história dele.

## Resumo

Projeto Vue 3 + Vite + TypeScript que serve a página `viewer.html`, onde um modelo 3D com quatro computadores históricos pode ser girado, ampliado, ligado e desligado individualmente. Ao clicar em um PC, a câmera se aproxima dele e um painel lateral mostra a história da máquina.

| PC | Ano |
|----|-----|
| IBM 3178 Coax Terminal | 1983–1984 |
| Apple Macintosh SE | 1987 |
| Windows 95 PC (genérico) | 1995 |
| Windows XP PC (genérico) | 2001 |

## Descrição detalhada

### Funcionalidades

- **Visualização 3D:** o modelo `.glb` é renderizado com [three.js](https://threejs.org/). É possível girar (arrastar), dar zoom (scroll) e mover a câmera (`OrbitControls`).
- **Ligar/desligar a tela de cada PC:** cada PC tem um botão flutuante acima dele, que acompanha o modelo em 3D. Desligar apaga apenas a tela; carcaça, teclado e mouse não mudam.
- **Zoom ao clicar:** clicar em um PC move a câmera suavemente até ele, mantendo o ângulo atual. Ao fechar o painel, a câmera volta à vista geral.
- **Painel de história:** um painel lateral, sem bloquear a cena, mostra o contexto histórico e as características técnicas do PC. Dá para continuar girando a câmera ou clicar em outro PC com ele aberto.
- **Créditos:** a atribuição do modelo aparece no rodapé da página.

### Como a tela desliga

O modelo usa um único material, com um atlas de textura que contém as imagens das quatro telas. Para apagar só uma tela, o código clona o material da malha onde a tela está e troca a textura por uma cópia em que a região da tela foi pintada de preto. O brilho emissivo também é zerado.

### Estrutura do projeto

```
.
├── public/
│   ├── viewer.html          # Visualizador 3D (three.js via CDN, sem build)
│   └── models/
│       └── computer.glb     # Modelo 3D (CC BY 4.0)
├── src/                     # Aplicação Vue base gerada pelo create-vue
├── index.html
├── package.json
└── vite.config.ts
```

> O visualizador está em `public/viewer.html` e é uma página independente do app Vue. Ela carrega o three.js de um CDN (jsDelivr), então precisa de internet.

### Tecnologias

- [Vue 3](https://vuejs.org/) + [Vite](https://vite.dev/) + TypeScript
- [three.js](https://threejs.org/) 0.170 (`GLTFLoader`, `OrbitControls`, `RoomEnvironment`)

## Como executar

Requisitos: [Node.js](https://nodejs.org/) 22.22+ ou 24.15+ e npm.

```sh
npm install
npm run dev
```

Abra `http://localhost:5173/viewer.html` (a porta pode mudar; veja a saída do terminal).

> Abrir `viewer.html` com duplo clique (`file://`) não funciona, porque o navegador bloqueia o carregamento do `.glb`. Use o servidor de desenvolvimento.

### Outros comandos

```sh
npm run build      # build de produção
npm run preview    # servir o build localmente
```

## Créditos

- **Modelo 3D:** [80s / 90s Computer Pack - Cartoon Stylized](https://sketchfab.com/3d-models/80s-90s-computer-pack-cartoon-stylized-6b45ad8c7d1d44f0987acb54c46975cd), de [TheAlex](https://sketchfab.com/TheAlex), licenciado sob [CC BY 4.0](http://creativecommons.org/licenses/by/4.0/).
- **Textos históricos:** resumos escritos a partir de pesquisa em fontes públicas (Wikipedia, Low End Mac, Carleton University, entre outras). Podem conter imprecisões e vale conferir as fontes originais.
