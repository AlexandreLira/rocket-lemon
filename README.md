# Rocket Lemon

Jogo arcade estilo **Lunar Lander** em HTML5. Controle um foguete da Terra até a Lua: colete limões para reabastecer, desvie de obstáculos, pouse nas plataformas intermediárias e, no final, use um **estilingue** no planeta para acertar a Lua.

Sem dependências, sem build — basta abrir no navegador.

## Como jogar

1. Abra `index.html` no navegador (Chrome, Firefox ou Safari recomendados).
2. Pressione **Enter** na tela inicial.
3. Escolha a dificuldade (**Easy**, **Medium** ou **Hard**).
4. Decole da Terra com **↑**, navegue pelas plataformas e colete todos os limões.
5. Pouso suave no **planeta** final para entrar no modo estilingue.
6. Arremesse o foguete e **acerte a Lua** para vencer.

## Objetivo

- Coletar o limão de cada plataforma intermediária (+60 de combustível).
- Pousar com velocidade e inclinação dentro dos limites seguros.
- Desviar de obstáculos espaciais durante a subida.
- No planeta final, mirar no estilingue e **colidir com a Lua** (não é pouso — é impacto).

## Controles

### Voo

| Tecla | Ação |
|-------|------|
| **← / →** | Rotacionar o foguete |
| **↑** | Empuxo (consome combustível) |
| **M** | Silenciar / ativar som |

### Menus

| Tecla | Ação |
|-------|------|
| **Enter / Espaço** | Confirmar / iniciar |
| **Esc** | Voltar |
| **↑ / ↓** | Selecionar dificuldade |
| **1 / 2 / 3** | Atalho Easy / Medium / Hard |
| **R** | Tentar novamente (após vitória ou derrota) |

### Modo estilingue

| Entrada | Ação |
|---------|------|
| **← / →** | Ajustar ângulo |
| **↑ / ↓** | Aumentar / diminuir potência |
| **Espaço / Enter** | Lançar |
| **Mouse** | Arrastar o foguete para trás e soltar para lançar |

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
- Na vitória, a Lua pequena se transforma na Lua grande e o astronauta planta a bandeira.

### Obstáculos

| Tipo | Comportamento |
|------|---------------|
| Asteroide | Move-se horizontalmente |
| Satélite | Move-se horizontalmente |
| Lixo espacial | Oscila verticalmente |
| Raio tóxico | Pisca; move-se horizontalmente |
| Dentista espacial | Oscila verticalmente |
| Cachorro espacial | Oscila verticalmente |

## Dificuldades

| Nível | Plataformas | Obstáculos por segmento | Velocidade |
|-------|-------------|-------------------------|------------|
| **Easy** | 3 | 1–2 | 30–55 |
| **Medium** | 8 | 2–3 | 60–100 |
| **Hard** | 12 | 3–5 | 95–150 |

O mapa é gerado proceduralmente a cada partida: posição das plataformas e obstáculos muda, mas a estrutura (N pads + planeta + Lua acima) permanece conforme a dificuldade.

## HUD

Durante o voo:

- Barra de combustível (pisca em vermelho quando ≤ 20)
- Distância até o próximo alvo (limão, planeta ou Lua)
- Velocidades **VX** e **VY** (verde = seguro, vermelho = perigoso)
- Progresso (pad atual / total ou alvo planeta/Lua)
- Número da tentativa e dificuldade
- Seta indicadora quando o alvo está acima da tela

No modo estilingue:

- Distância até a Lua
- **ANGLE** (graus) e **POWER** (%)

## Tecnologias

- **HTML5 Canvas** — renderização 2D pixel art
- **Web Audio API** — música procedural, ruído de motor e efeitos sonoros
- **JavaScript vanilla** — física, geração de mundo e game loop

Sprites gerados em runtime a partir de matrizes de caracteres; nenhuma imagem externa é necessária.

## Estrutura do projeto

```
jogo/
├── index.html    # Jogo completo (HTML + CSS + JS)
├── .gitignore
└── README.md
```

## API de debug

Para testes automatizados, o jogo expõe `window.__rl` no console:

```js
__rl.state              // 'title' | 'difficulty' | 'playing' | 'slingshot' | 'exploding' | 'win' | 'lose'
__rl.rocket             // posição, velocidade, ângulo, combustível
__rl.platforms          // plataformas e planeta gerados
__rl.obstacles          // obstáculos ativos
__rl.moon               // posição da Lua
__rl.targetIndex        // índice da plataforma/limão alvo
__rl.ballistic          // true durante voo pós-estilingue
__rl.slingAngle         // ângulo do estilingue (rad)
__rl.slingPower         // potência do estilingue (0.25–1)
__rl.launchSlingshot()   // dispara o foguete no modo estilingue
__rl.startGame('easy', false)
__rl.CONFIG
__rl.DIFFICULTIES
```

## Licença

Projeto de código aberto. Consulte o repositório para detalhes de licenciamento.
