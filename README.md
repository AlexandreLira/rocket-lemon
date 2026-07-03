# Rocket Lemon

Jogo arcade estilo **Lunar Lander** em HTML5. Controle um foguete da Terra até a Lua, colete limões para reabastecer combustível, desvie de obstáculos espaciais e faça pousos suaves em cada plataforma.

Sem dependências, sem build — basta abrir no navegador.

## Como jogar

1. Abra `index.html` no navegador (Chrome, Firefox ou Safari recomendados).
2. Pressione **Enter** na tela inicial.
3. Escolha a dificuldade (**Easy**, **Medium** ou **Hard**).
4. Decole da Terra com **↑**, navegue pelas plataformas e colete os limões.
5. Pouso final na Lua para vencer.

### Objetivo

- Coletar o limão de cada plataforma intermediária (reabastece +60 de combustível).
- Pousar com velocidade e inclinação dentro dos limites seguros.
- Chegar à Lua sem colidir com obstáculos.

### Controles

| Tecla | Ação |
|-------|------|
| **← / →** | Rotacionar o foguete |
| **↑** | Empuxo (consome combustível) |
| **M** | Silenciar / ativar som |
| **Enter** | Confirmar (menus, iniciar) |
| **Esc** | Voltar (menu de dificuldade) |
| **↑ / ↓** | Selecionar dificuldade |
| **1 / 2 / 3** | Atalho para Easy / Medium / Hard |
| **R** | Tentar novamente (após vitória ou derrota) |

## Mecânicas

### Combustível

- Tanque máximo: **100**
- Consumo: **8/s** com empuxo ativo
- Cada limão coletado: **+60**

### Pouso seguro

O pouso só é válido se:

- Velocidade horizontal ≤ **5.5 m/s** (55 unidades internas)
- Velocidade vertical ≤ **8.0 m/s** (80 unidades internas)
- Inclinação ≤ **30°**

Fora desses limites, o foguete explode.

### Progressão

As plataformas são desbloqueadas em sequência. Só a plataforma atual (e as anteriores) colidem com o foguete; as futuras aparecem semitransparentes até o limão anterior ser coletado.

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

O mapa é gerado proceduralmente a cada partida: posição das plataformas e obstáculos muda, mas a estrutura (número de pads + Lua no topo) permanece conforme a dificuldade escolhida.

## HUD

Durante o jogo, a interface mostra:

- Barra de combustível (pisca em vermelho quando ≤ 20)
- Distância até o próximo alvo (limão ou Lua)
- Velocidades **VX** e **VY** (verde = seguro, vermelho = perigoso)
- Progresso (pad atual / total)
- Número da tentativa e dificuldade
- Seta indicadora quando o alvo está acima da tela

## Tecnologias

- **HTML5 Canvas** — renderização 2D pixel art
- **Web Audio API** — música procedural, ruído de motor e efeitos sonoros
- **JavaScript vanilla** — física, geração de mundo e game loop

Sprites gerados em runtime a partir de matrizes de caracteres; nenhuma imagem externa é necessária.

## Estrutura do projeto

```
jogo/
├── index.html    # Jogo completo (HTML + CSS + JS)
└── README.md
```

## API de debug

Para testes automatizados, o jogo expõe `window.__rl` no console:

```js
__rl.state          // 'title' | 'difficulty' | 'playing' | 'exploding' | 'win' | 'lose'
__rl.rocket         // posição, velocidade, ângulo, combustível
__rl.platforms      // plataformas geradas
__rl.obstacles      // obstáculos ativos
__rl.targetIndex    // índice da plataforma/limão alvo
__rl.startGame('easy', false)  // inicia partida
__rl.CONFIG         // parâmetros de física e jogo
__rl.DIFFICULTIES   // configuração por dificuldade
```

## Licença

Projeto de código aberto. Consulte o repositório para detalhes de licenciamento.
