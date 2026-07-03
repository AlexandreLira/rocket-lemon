# SPEC: Sistema de Loja — Fase 2 (Cosméticos Completos)

**Projeto:** Rocket Lemon  
**Data:** 2026-07-03  
**Status:** Implementado  
**Escopo:** F2 — loja com skins de nave + trilhas + acessórios; comprar, equipar e persistir  
**Pré-requisito:** [F1 Moedas](./2026-07-03-coin-system-design.md)

---

## Resumo

A F2 transforma moedas coletadas em cosméticos visuais: **skins de nave**, **trilhas de partículas** e **acessórios**. A loja é acessível na tela inicial (botão LOJA / tecla `L`) e no menu de personagem (`Esc`). Itens são comprados com saldo persistente e equipados por categoria.

**Arquivo principal:** [`index.html`](../../../index.html)

---

## Save schema v2

```javascript
{
  version: 2,
  coins: 0,
  totalEarned: 0,
  inventory: {
    rocketSkins: ['default'],
    trails: ['default'],
    accessories: ['none']
  },
  equipped: {
    rocketSkin: 'default',
    trail: 'default',
    accessory: 'none'
  }
}
```

Migração automática v1→v2 em `loadSave()`, preservando `coins` e `totalEarned`.

`sanitizeWallet()` no load (e na migração v1): filtra IDs fora do catálogo, remove duplicatas, garante defaults no inventário (`default` / `none`) e reseta `equipped` inválido para o default da categoria. Persistência é reescrita se o save foi corrigido.

---

## Catálogo

| Categoria | Itens | Preços |
|-----------|-------|--------|
| Naves | default, lemon, neon, stealth, golden | 0, 25, 40, 35, 60 |
| Trilhas | default, acid, plasma, ember, rainbow | 0, 20, 35, 30, 50 |
| Acessórios | none, antenna, flag, halo, wings | 0, 15, 20, 25, 35 |

---

## Navegação

- **Title:** botão LOJA ou tecla `L` → shop (`shopReturnState = 'title'`)
- **Character:** `Esc` → shop; `Backspace` ou clique `← TÍTULO` → title
- **Shop (teclado):** `Esc` volta ao estado anterior; `Q`/`E` trocam abas; setas navegam grid; `Enter` compra/equipa; `Backspace` vai ao title
- **Shop (toque):** 1º toque no card seleciona (preview); 2º toque no mesmo card ou no botão de ação confirma; `← VOLTAR` sai para `shopReturnState` (igual a `Esc`)
- **Botão de ação:** `EQUIPADO` (verde), `EQUIPAR` (amarelo), `COMPRAR (N)` (amarelo), ou `FALTAM X` (cinza, sem saldo)

---

## Integração in-game

- `drawRocket()` — skin + acessório + chama da trilha equipada
- `spawnThrustParticles()` — cores da trilha equipada
- `renderTitle()` — preview da nave equipada

---

## Debug API

```javascript
__rl.SHOP
__rl.purchaseItem('rocketSkins', 'neon')
__rl.equipItem('trails', 'plasma')
__rl.equipped
__rl.inventory
__rl.openShop('title')
```
