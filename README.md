# Rocket Lemon

Jogo arcade estilo **Lunar Lander** em HTML5. Controle um foguete da Terra até a Lua: colete limões para reabastecer, desvie de obstáculos, pouse nas plataformas intermediárias e, no final, use um **estilingue** no planeta para acertar a Lua.

Durante a subida você também pode coletar **moedas** opcionais (progressão meta persistente) e gastar na **loja de cosméticos** — skins de nave, trilhas e acessórios.

Sem dependências, sem build — basta abrir no navegador. Funciona no desktop e no mobile.

## Como jogar

1. Abra `index.html` no navegador (Chrome, Firefox ou Safari recomendados).
2. Pressione **Enter** (ou toque) na tela inicial. Opcional: abra a **loja** com o botão LOJA ou a tecla **L**.
3. Escolha um **piloto** (Alex Lira, Tabata Ruiz, Kaique Costa ou Weslley Araujo). No menu de piloto, **L** também abre a loja.
4. Escolha a dificuldade (**Fácil**, **Médio** ou **Difícil**).
5. Decole da Terra com **↑** (ou segure a tela no mobile), navegue pelas plataformas e colete todos os limões.
6. Colete moedas pelo caminho se quiser — elas vão direto para o saldo persistente.
7. Pouso suave no **planeta** final para entrar no modo estilingue.
8. Arremesse o foguete e **acerte a Lua** para vencer.

## Objetivo

- Coletar o limão de cada plataforma intermediária (+60 de combustível).
- Pousar com velocidade e inclinação dentro dos limites seguros.
- Desviar de obstáculos espaciais durante a subida.
- Coletar moedas opcionais para comprar cosméticos na loja.
- No planeta final, mirar no estilingue e **colidir com a Lua** (não é pouso — é impacto).

## Controles

### Voo

| Tecla | Ação |
|-------|------|
| **← / →** | Rotacionar o foguete |
| **↑** | Empuxo (consome combustível) |
| **Esc** | Pausar |
| **M** | Silenciar / ativar som |

### Menus

| Tecla | Ação |
|-------|------|
| **Enter / Espaço** | Confirmar / iniciar |
| **Esc** | Voltar / pausar (em voo) |
| **↑ / ↓ / ← / →** | Selecionar piloto (grid) ou dificuldade |
| **1 / 2 / 3 / 4** | Atalho para piloto (Alex / Tabata / Kaique / Weslley) |
| **1 / 2 / 3** | Atalho Fácil / Médio / Difícil (tela de dificuldade) |
| **L** | Abrir loja (tela inicial ou menu de piloto) |
| **R** | Tentar novamente (após vitória ou derrota) |
| **Enter / Esc** | Voltar ao título (após vitória ou derrota) |

### Pausa

| Tecla | Ação |
|-------|------|
| **Esc** | Pausar durante o voo |
| **Enter / Esc / Espaço** | Retomar (countdown de 2 s) |
| **Q** | Sair para o menu de piloto |

### Loja

| Tecla | Ação |
|-------|------|
| **L** | Abrir (a partir do título ou do menu de piloto) |
| **Q / E** (ou **Tab**) | Trocar abas (Naves / Trilhas / Acessórios) |
| **← / → / ↑ / ↓** | Navegar no grid de itens |
| **Enter / Espaço** | Comprar ou equipar o item selecionado |
| **Esc** | Voltar à tela anterior |
| **Backspace** | Ir ao título |

### Mobile

| Entrada | Ação |
|---------|------|
| **Inclinar o aparelho** | Girar o foguete |
| **Segurar a tela** | Empuxo |
| **Toque** | Confirmar menus, escolher piloto/dificuldade, abrir loja |
| **Toque e arraste** | Estilingue (puxar o foguete para trás e soltar) |
| **Metade de baixo da tela** | Voltar ao menu (após vitória ou derrota) |

### Pilotos

| Piloto | Área | Bônus | Descrição |
|--------|------|-------|-----------|
| Alex Lira | Dev | Rotação +20% | Quebrou prod três vezes hoje. Mesmo assim confia no empuxo. |
| Tabata Ruiz | Dev | Auto-estabilização +35% | Transforma crash em sprint. Se caiu, virou retro. |
| Kaique Costa | Dados | Combustível 120, limão +70 | Só mais um pastel. |
| Weslley Araujo | Produto | HUD estendido (ângulo, %, margens de pouso) | Previu 99% de chance de explosão. Você está no 1%. |

### Modo estilingue

| Entrada | Ação |
|---------|------|
| **← / →** | Ajustar ângulo |
| **↑ / ↓** | Aumentar / diminuir potência |
| **Espaço / Enter** | Lançar |
| **Mouse / toque** | Arrastar o foguete para trás e soltar para lançar |

## Moedas

Economia **meta** separada dos limões: moedas são opcionais, flutuam entre plataformas e não bloqueiam o avanço.

- **Coleta imediata:** o valor entra no saldo assim que você toca a moeda, mesmo se morrer depois.
- **Persistência:** salvo em `localStorage` (`rocket_lemon_save_v1`), schema v2 (moedas + inventário da loja).
- **Valores:** **1** moeda no caminho normal; **3** moedas perto de obstáculos ou na zona balística (entre o planeta e a Lua).
- **Spawn por dificuldade** (por segmento entre plataformas):

| Dificuldade | Moedas por segmento |
|-------------|---------------------|
| Fácil | 0–1 |
| Médio | 0–2 |
| Difícil | 1–2 |

Além disso, **1–2** moedas de valor 3 aparecem entre o planeta e a Lua.

O saldo aparece no HUD durante o voo, na tela inicial e nas telas de vitória/derrota.

## Loja de cosméticos

Acesse pela tela inicial (botão **LOJA** ou tecla **L**) ou pelo menu de piloto (**L**). Itens comprados e equipados são persistidos no mesmo save das moedas.

### Naves

| Item | Preço |
|------|-------|
| Clássico Capim | 0 (padrão) |
| Limonada Orbital | 25 |
| Neon Synthwave | 40 |
| Furtivo Noturno | 35 |
| Edição Ouro | 60 |

### Trilhas

| Item | Preço |
|------|-------|
| Chama Padrão | 0 (padrão) |
| Exaustor Ácido | 20 |
| Plasma Azul | 35 |
| Brasa Intensa | 30 |
| Arco-íris | 50 |

### Acessórios

| Item | Preço |
|------|-------|
| Sem acessório | 0 (padrão) |
| Antena VHF | 15 |
| Bandeira Limão | 20 |
| Auréola Dourada | 25 |
| Asas Mini | 35 |

Skins e acessórios alteram o visual do foguete; trilhas mudam as cores da chama e das partículas de empuxo. A tela inicial mostra a nave equipada.

## Mecânicas

### Combustível

- Tanque máximo: **100**
- Consumo: **8/s** com empuxo ativo
- Cada limão coletado: **+60**
- Combustível é **reabastecido ao máximo** ao entrar no modo estilingue

### Pouso seguro

O pouso em plataformas e no planeta só é válido se:

- Velocidade horizontal ≤ **5.5 m/s**
- Velocidade vertical ≤ **8.0 m/s**
- Inclinação ≤ **30°**

Fora desses limites, o foguete explode.

### Progressão

As plataformas são desbloqueadas em sequência. Só a plataforma atual (e as anteriores) colidem com o foguete; as futuras aparecem semitransparentes até o limão anterior ser coletado.

A última parada antes da Lua é um **planeta** com faixa de pouso. Após coletar todos os limões e pousar nele, o jogo entra no **modo estilingue**.

### Modo estilingue e voo balístico

- O foguete é puxado por elásticos; a UI mostra **preview da trajetória**.
- Ao lançar, o foguete entra em voo **balístico** (sem empuxo nem rotação manual).
- **Vitória:** colidir com a Lua (raio de impacto ~33 px).
- **Erro:** se o foguete cair abaixo do planeta sem acertar a Lua, o controle normal é restaurado (`MISSED! CONTROL RESTORED`) — ainda dá para tentar de novo com combustível cheio.
- Na vitória, a Lua pequena se transforma na Lua grande e o astronauta planta a bandeira. Toca o refrão de *We Are the Champions*.

### Obstáculos

| Tipo | Comportamento |
|------|---------------|
| Asteroide | Move-se horizontalmente |
| Satélite | Move-se horizontalmente |
| Lixo espacial | Oscila verticalmente |
| Raio tóxico | Pisca; move-se horizontalmente |
| Dentista espacial | Oscila verticalmente |
| Cachorro espacial | Oscila verticalmente |
| Limão voador | Oscila verticalmente |
| Dente voador | Oscila verticalmente |

## Dificuldades

| Nível | Plataformas | Obstáculos por segmento | Velocidade |
|-------|-------------|-------------------------|------------|
| **Fácil** | 3 | 1–2 | 30–55 |
| **Médio** | 8 | 2–3 | 60–100 |
| **Difícil** | 12 | 3–5 | 95–150 |

O mapa é gerado proceduralmente a cada partida: posição das plataformas e obstáculos muda, mas a estrutura (N pads + planeta + Lua acima) permanece conforme a dificuldade.

## HUD

Durante o voo:

- Saldo de **moedas** (persistente)
- Barra de combustível (pisca em vermelho quando ≤ 20)
- Distância até o próximo alvo (limão, planeta ou Lua)
- Velocidades **VX** e **VY** (verde = seguro, vermelho = perigoso)
- Progresso (pad atual / total ou alvo planeta/Lua)
- Número da tentativa e dificuldade
- Nome do piloto
- Seta indicadora quando o alvo está acima da tela
- Dica de controles (inclui pausa com Esc)

No modo estilingue:

- Distância até a Lua
- **ANGLE** (graus) e **POWER** (%)

## Tecnologias

- **HTML5 Canvas** — renderização 2D pixel art (1180×720)
- **Web Audio API** — música procedural, ruído de motor e efeitos sonoros
- **HTMLAudioElement** — música de vitória (`assets/we-are-the-champions.mp3`)
- **localStorage** — saldo de moedas, inventário e cosméticos equipados
- **DeviceOrientation** — controle por inclinação no mobile
- **JavaScript vanilla** — física, geração de mundo e game loop

Sprites gerados em runtime a partir de matrizes de caracteres. Avatares dos pilotos são PNGs pixel em `assets/avatars/` (a partir das fotos em `assets/`).

## Assets

| Pasta / arquivo | Conteúdo |
|-----------------|----------|
| `assets/` | Fotos originais dos pilotos |
| `assets/avatars/` | Sprites pixel usados no menu e no HUD |
| `assets/we-are-the-champions.mp3` | Música de vitória |

## Estrutura do projeto

```
jogo/
├── index.html              # Jogo completo (HTML + CSS + JS)
├── assets/                 # Fotos dos pilotos + áudio de vitória
│   └── avatars/            # Avatares pixel
├── docs/
│   └── superpowers/specs/  # Specs de moedas e loja
├── .gitignore
└── README.md
```

## API de debug

Para testes automatizados, o jogo expõe `window.__rl` no console:

```js
__rl.state              // 'title' | 'character' | 'difficulty' | 'shop' | 'playing' | 'paused' | ...
__rl.rocket             // posição, velocidade, ângulo, combustível
__rl.platforms          // plataformas e planeta gerados
__rl.obstacles          // obstáculos ativos
__rl.moon               // posição da Lua
__rl.targetIndex        // índice da plataforma/limão alvo
__rl.ballistic          // true durante voo pós-estilingue
__rl.slingAngle         // ângulo do estilingue (rad)
__rl.slingPower         // potência do estilingue (0.25–1)
__rl.launchSlingshot()  // dispara o foguete no modo estilingue
__rl.startGame('easy', false)
__rl.CONFIG
__rl.DIFFICULTIES

// Economia e loja
__rl.wallet             // save completo (coins, inventory, equipped)
__rl.coins              // moedas no mapa da partida atual
__rl.addCoins(n)        // credita moedas e persiste
__rl.resetWallet()      // zera save para o padrão
__rl.SHOP               // catálogos (ROCKET_SKINS, TRAILS, ACCESSORIES, …)
__rl.purchaseItem('rocketSkins', 'neon')
__rl.equipItem('trails', 'plasma')
__rl.equipped
__rl.inventory
__rl.openShop('title')

// Mobile
__rl.isMobile
__rl.enableTilt()
__rl.tiltEnabled
__rl.neutralGamma
```

## Licença

Projeto de código aberto. Consulte o repositório para detalhes de licenciamento.
