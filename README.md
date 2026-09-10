# 🏃 Strava Dashboard

Dashboard pessoal de atividades físicas construído com HTML, CSS e JavaScript puro — sem frameworks, sem backend, sem build.

Lê dados diretamente do Google Sheets em tempo real e renderiza gráficos interativos com filtros estilo Power BI.

**[→ Ver ao vivo](https://andrescultori.github.io/stravadashboard)**

---

## Funcionalidades

- Login com Google (OAuth2)
- Dados carregados em tempo real do Google Sheets
- Filtros interativos por ano e tipo de atividade — clicando nos gráficos também filtra
- KPIs em destaque: Distância total e Tempo total
- Gráficos: distância mensal, distribuição por tipo, distância anual, pace médio, BPM
- Tabela paginada com todas as atividades
- Link direto para cada atividade no Strava
- Responsivo para mobile

## Stack

| Camada | Tecnologia |
|---|---|
| Frontend | HTML + CSS + Vanilla JS |
| Gráficos | [Chart.js 4](https://www.chartjs.org/) |
| Autenticação | Google Identity Services |
| Dados | Google Sheets API v4 |
| Hospedagem | GitHub Pages / Netlify |

## Estrutura

```
index.html   ← tudo em um arquivo só
README.md
```

## Como usar (fork)

1. Faça um fork deste repositório
2. Crie um projeto no [Google Cloud Console](https://console.cloud.google.com)
3. Ative a **Google Sheets API**
4. Crie credenciais **OAuth 2.0** (Aplicativo da Web)
5. Adicione seu domínio em **Origens JavaScript autorizadas**
6. Substitua `CLIENT_ID` e `SHEET_ID` no `index.html`
7. Configure a planilha conforme o esquema abaixo
8. Faça deploy no GitHub Pages ou Netlify

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

## Sobre

Desenvolvido por [André Scultori](https://www.strava.com/athletes/13751526) · Maringá, BR

---

*Dados sincronizados via Google Apps Script direto do Strava API*
