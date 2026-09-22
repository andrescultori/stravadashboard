🇧🇷 Português | [🇺🇸 English](README.en.md)

# 🏃 Strava Dashboard
Dashboard pessoal de atividades físicas, com dados sincronizados do Strava em tempo real — sem backend, sem build, só abrir e usar.

Lê os dados direto de uma planilha do Google Sheets e renderiza gráficos interativos com filtros estilo Power BI: por ano, por tipo de atividade, e clicando direto nos gráficos.

**[→ Ver ao vivo](https://andrescultori.github.io/stravadashboard)**

> Este é o meu dashboard pessoal — os dados exibidos são reais, sincronizados automaticamente das minhas atividades no Strava.

## O problema original

O app do Strava mostra atividade por atividade, mas não dá uma visão consolidada: comparar evolução de pace, volume mensal por esporte, ou cruzar BPM com distância ao longo do tempo exigia exportar tudo manualmente e montar gráfico na mão.

## A solução

```
Strava (atividades registradas)
        ↓
Google Apps Script (sincroniza periodicamente)
        ↓
Google Sheets (planilha "STRAVA")
        ↓
index.html (leitura direta via Sheets API)
        ↓
Chart.js (gráficos interativos e filtráveis)
```

O resultado: abro o link e já vejo o histórico completo e atualizado, sem exportar nada manualmente.

## O dashboard em si

- Filtros interativos por ano e tipo de atividade — clicar num gráfico também filtra os outros
- KPIs em destaque: distância total e tempo total
- Gráficos: distância mensal, distribuição por tipo, distância anual, pace médio, BPM
- Tabela paginada com todas as atividades, com link direto pra cada uma no Strava
- Tema claro/escuro, com preferência salva
- Responsivo para mobile

## Stack técnica

| Camada | Tecnologia |
|---|---|
| Frontend | HTML + CSS + JavaScript puro |
| Gráficos | [Chart.js 4](https://www.chartjs.org/) |
| Dados | Google Sheets API v4 |
| Sincronização | Google Apps Script (Strava API → Sheets) |
| Hospedagem | GitHub Pages / Netlify |

## Por que sem framework e sem backend

O dashboard inteiro roda em um único `index.html`, sem passo de build. Para um projeto pessoal desse escopo — ler uma planilha e desenhar gráficos — um framework ou uma API própria adicionariam complexidade sem benefício real: não há estado complexo pra gerenciar, nem rotas, nem necessidade de SSR. A troca é simplicidade e zero manutenção de infraestrutura.

## Arquitetura

- [`index.html`](./index.html) — todo o front-end: fetch dos dados, parsing, renderização dos gráficos e da tabela

## Rodando localmente

1. Clone o repositório
2. Abra o `index.html` direto no navegador (não precisa de servidor)

## Como usar com seus próprios dados (fork)

1. Faça um fork deste repositório
2. Crie um projeto no [Google Cloud Console](https://console.cloud.google.com) e ative a **Google Sheets API**
3. Crie uma **API Key** e restrinja por referrer HTTP ao seu domínio
4. Substitua `API_KEY` e `SID` no `index.html` pelos seus
5. Configure sua planilha conforme o esquema abaixo
6. Faça deploy no GitHub Pages ou Netlify

## Esquema da planilha

A planilha deve ter uma aba chamada `STRAVA` com as seguintes colunas:

| Col | Campo | Tipo |
|---|---|---|
| A | ID | Texto (ID da atividade no Strava) |
| B | DATA | Data (DD/MM/YYYY HH:MM) |
| C | ATIV | Texto (Run, Walk, Ride, Hike...) |
| D | KM | Número |
| E | TEMPO | Duração (fração de dia) |
| F | PACE | Duração (fração de dia, min/km) |
| G | VEL | Número (km/h) |
| ... | ... | ... |
| M | BPM AVG | Número |
| O | GEAR | Texto |
| Q | LOCAL | Texto (cidade) |
| R | ELEV | Número (metros) |
| S | CALORIAS | Número |
| T | NOME | Texto (nome da atividade) |
| W | LINK | URL (link Strava) |

---

Desenvolvido por [André Scultori](https://github.com/andrescultori) · © 2026 · [GitHub](https://github.com/andrescultori/stravadashboard)

*Dashboard pessoal — dados reais, sincronizados automaticamente do Strava via Google Apps Script.*
