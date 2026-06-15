<div align="center">

<img src="https://img.shields.io/badge/LogiTrack-Dashboard-5b8dee?style=for-the-badge&logo=truck&logoColor=white" alt="LogiTrack" />

# 🚛 LogiTrack — Dashboard de Monitoramento Logístico

**Painel interativo e responsivo para análise de desempenho de entregas em tempo real.**  
Identifique atrasos, ranqueie transportadoras críticas e filtre por região com um clique.

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![Chart.js](https://img.shields.io/badge/Chart.js-FF6384?style=flat-square&logo=chartdotjs&logoColor=white)](https://www.chartjs.org/)
[![Zero Dependencies](https://img.shields.io/badge/Zero%20Build%20Step-✓-38c9a3?style=flat-square)](.)
[![License](https://img.shields.io/badge/License-MIT-a78bfa?style=flat-square)](LICENSE)

</div>

---

## 📋 Sumário

- [Visão Geral](#-visão-geral)
- [Demonstração](#-demonstração)
- [Funcionalidades](#-funcionalidades)
- [Estrutura do Projeto](#-estrutura-do-projeto)
- [Como Usar](#-como-usar)
- [Estrutura dos Dados](#-estrutura-dos-dados)
- [Arquitetura Visual](#-arquitetura-visual)
- [Customização](#-customização)
- [Tecnologias](#-tecnologias)
- [Regras de Negócio](#-regras-de-negócio)
- [Licença](#-licença)

---

## 🎯 Visão Geral

O **LogiTrack** é um dashboard de monitoramento logístico **100% client-side**, construído sem frameworks ou etapas de build. Ele permite que equipes de operações e supply chain visualizem, filtrem e analisem o desempenho de entregas em um único painel — com animações suaves, design dark profissional e gráficos interativos.

Ideal para:
- Times de **logística e operações** que precisam de visibilidade rápida sobre SLAs
- **Analistas de dados** que querem uma interface pronta para alimentar com dados reais
- Desenvolvedores buscando um **template de dashboard** elegante e sem dependências de build

---

## 🖥️ Demonstração

```
Abra o arquivo index.html diretamente no navegador.
Sem servidor. Sem instalação. Funciona offline.
```

> **Loader animado** com caminhão em CSS puro exibido durante a inicialização → transição suave para o dashboard completo.

---

## ✨ Funcionalidades

### 🔎 Filtros Interativos
- **Transportadora** — dropdown com todas as transportadoras presentes nos dados
- **Região** — dropdown com todas as regiões mapeadas
- **Status** — toggle de 3 estados: `Todas` · `Atrasadas` · `No prazo`
- **Limpar filtros** — restaura o estado inicial com um clique

### 📊 KPIs em Tempo Real
| Indicador | Descrição |
|---|---|
| Entregas analisadas | Total no recorte atual |
| Entregas atrasadas | Contagem + percentual do total |
| Atraso médio | Média de dias além do prazo |
| Pior atraso | Entrega mais crítica do recorte |

### 📈 Gráficos
- **Barras** — Taxa de atraso (%) por transportadora, com cores únicas por empresa
- **Donut** — Dias acumulados de atraso por região, com legenda interativa

### 🗺️ Tabela de Regiões Críticas
Ordenada por dias totais de atraso. Cada linha exibe:
- Total de entregas, atrasadas, taxa percentual e barra de progresso colorida por criticidade

### 🏆 Ranking — Entregas a Priorizar
Top 6 entregas mais atrasadas com:
- Posição medalha (🥇🥈🥉 para o top 3)
- ID, transportadora, região, prazo vs. real
- Badge de criticidade: `No prazo` · `Leve` · `Alto` · `Crítico`

### 📋 Tabela Completa de Detalhamento
Todos os registros do recorte com colunas de prazo, dias reais, atraso (colorido), barra de progresso e badge de status.

### ⏱️ Relógio em Tempo Real
Timestamp no header atualizado a cada segundo.

---

## 📁 Estrutura do Projeto

```
logitrack/
│
└── index.html          # Aplicação completa — HTML + CSS + JS em um único arquivo
```

> Todo o CSS está encapsulado em `<style>` e o JavaScript em `<script>` no próprio `index.html`. Não há dependências locais.

---

## 🚀 Como Usar

### 1. Clone o repositório

```bash
git clone https://github.com/seu-usuario/logitrack.git
cd logitrack
```

### 2. Abra no navegador

```bash
# Opção A — Abrir diretamente
open index.html

# Opção B — Servir localmente (recomendado para evitar CORS em alguns browsers)
npx serve .
# ou
python -m http.server 8080
```

### 3. Substitua os dados de exemplo

Localize o array `ENTREGAS` no bloco `<script>` e substitua pelos seus dados reais:

```javascript
const ENTREGAS = [
  { id_entrega: 301, transportadora: 'RotaMax',  regiao: 'Sudeste',  prazo_dias: 3, dias_reais: 7 },
  { id_entrega: 302, transportadora: 'ViaCargo', regiao: 'Sul',      prazo_dias: 5, dias_reais: 5 },
  // ... adicione quantas entregas quiser
];
```

Os filtros, gráficos, KPIs, ranking e tabelas são gerados **automaticamente** a partir do array.

---

## 🗃️ Estrutura dos Dados

Cada objeto do array `ENTREGAS` deve seguir o contrato:

| Campo | Tipo | Descrição |
|---|---|---|
| `id_entrega` | `number` | Identificador único da entrega |
| `transportadora` | `string` | Nome da transportadora responsável |
| `regiao` | `string` | Região de destino da entrega |
| `prazo_dias` | `number` | SLA acordado em dias |
| `dias_reais` | `number` | Dias reais até a entrega |

> 💡 O campo `atraso` (`dias_reais - prazo_dias`) e o flag `atrasada` são calculados automaticamente via `enriched`.

---

## 🏗️ Arquitetura Visual

```
┌─────────────────────────────────────────────────┐
│  HEADER  │ Logo · Relógio · Badge "Tempo real"   │
├─────────────────────────────────────────────────┤
│  FILTROS │ Transportadora · Região · Status      │
├──────────┬──────────┬──────────┬────────────────┤
│  KPI 1   │  KPI 2   │  KPI 3   │    KPI 4       │
│  Total   │ Atrasad. │ Ø Atraso │  Pior Atraso   │
├──────────────────────────┬──────────────────────┤
│  Barras: taxa p/ transp. │  Donut: dias p/ reg. │
├──────────────────────────┴──────────────────────┤
│  Regiões Críticas (tabela) │ Ranking Top 6       │
├─────────────────────────────────────────────────┤
│  Detalhamento Completo (tabela com todas linhas) │
└─────────────────────────────────────────────────┘
```

### Design System

| Token | Valor |
|---|---|
| Background | `#0d0f14` |
| Surface | `#13161d` |
| Card | `#181c25` |
| Primary (azul) | `#5b8dee` |
| Accent (verde) | `#38c9a3` |
| Warning (âmbar) | `#f0b429` |
| Danger (vermelho) | `#e05c5c` |
| Font principal | Inter · ui-sans-serif |
| Font mono | JetBrains Mono · Fira Code |

---

## 🎨 Customização

### Paleta de cores dos gráficos
Edite o array `COLORS` para trocar as cores das barras e do donut:

```javascript
const COLORS = [
  '#5b8dee', '#38c9a3', '#f0b429', '#e05c5c', '#a78bfa',
  // adicione mais cores se tiver muitas categorias
];
```

### Número de itens no Ranking
Ajuste o `.slice(0, 6)` no bloco de ranking:

```javascript
const ranking = [...data].filter(e => e.atrasada)
  .sort((a, b) => b.atraso - a.atraso)
  .slice(0, 10); // <- altere aqui
```

### Thresholds de criticidade
Edite a função `criticidade()` para adaptar os limiares ao seu negócio:

```javascript
function criticidade(atraso) {
  if (atraso <= 0) return { label: 'No prazo', cls: 'badge-ok'      };
  if (atraso <= 3) return { label: 'Leve',     cls: 'badge-leve'    };
  if (atraso <= 6) return { label: 'Alto',     cls: 'badge-alto'    };
  return               { label: 'Crítico',  cls: 'badge-critico' };
}
```

### Tempo mínimo do loader
```javascript
const MIN_MS = 2000; // milissegundos
```

---

## 🛠️ Tecnologias

| Tecnologia | Uso |
|---|---|
| **HTML5** | Estrutura semântica da aplicação |
| **CSS3 Custom Properties** | Design system com variáveis (tokens de cor, raio, fontes) |
| **CSS Animations** | Loader (caminhão + asfalto), pulse dot, transições de hover |
| **Vanilla JavaScript** | Lógica de filtragem, agregação, renderização dinâmica |
| **[Chart.js 4.4.1](https://www.chartjs.org/)** | Gráfico de barras e donut (via CDN — sem instalação) |
| **CSS Grid + Flexbox** | Layout responsivo adaptado para mobile e desktop |

> Nenhuma dependência local. Apenas Chart.js carregado via CDN da `cdnjs.cloudflare.com`.

---

## 📐 Regras de Negócio

> Uma entrega é considerada **atrasada** quando `dias_reais > prazo_dias`.

| Atraso (dias) | Classificação | Badge |
|---|---|---|
| ≤ 0 | No prazo | 🟢 verde |
| 1 – 3 | Leve | 🟡 âmbar |
| 4 – 6 | Alto | 🟠 laranja |
| ≥ 7 | Crítico | 🔴 vermelho |

---


<div align="center">

Feito com ☕ e atenção aos detalhes.  
Se este projeto foi útil, considere deixar uma ⭐ no repositório!

</div>
