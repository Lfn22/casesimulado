<div align="center">

# 📡 Negreiros NET — Dashboard de Monitoramento

**Dashboard interativo para monitoramento de clientes de provedor de internet local em Petrolina, PE.**

[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)](https://streamlit.io/)
[![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![Plotly](https://img.shields.io/badge/Plotly-3F4F75?style=for-the-badge&logo=plotly&logoColor=white)](https://plotly.com/)

</div>

---

## 📋 Sobre o projeto

O **Negreiros NET Dashboard** é um sistema de monitoramento desenvolvido para provedores locais de internet, com foco na realidade de pequenas e médias ISPs do interior do Nordeste.

A solução permite que gestores e técnicos visualizem em tempo real o consumo de banda dos clientes, identifiquem situações críticas de uso, filtrem por bairro e plano, e exportem relatórios — tudo em uma interface web responsiva, sem necessidade de infraestrutura complexa.

> **Contexto real:** Desenvolvido como case simulado baseado nas necessidades reais de um provedor de internet da região de Petrolina/PE — cidade com crescente demanda por soluções de TI no segmento de telecomunicações.

---

## ✨ Funcionalidades

### 📊 KPIs e métricas principais
- Total de clientes ativos na base
- Número de clientes em situação crítica de consumo (≥ 50% de excedente)
- Consumo médio de banda por cliente (Mbps)
- Indicadores resilientes — funcionam mesmo com filtros que resultam em conjuntos vazios

### 🔍 Filtros avançados
- Filtro por **bairro** (múltipla seleção)
- Filtro por **plano de internet** (básico, intermediário, premium)
- Filtro por **criticidade** do consumo
- Filtro por **consumo mínimo** em Mbps
- Todos os filtros são sincronizados com KPIs, gráficos e mapa em tempo real

### 📈 Visualizações interativas (Plotly)
- **Pizza** — distribuição de clientes por tipo de plano
- **Barras** — consumo médio por bairro
- **Ranking** — top clientes por consumo
- **Tendência mensal** — evolução do consumo ao longo do tempo
- **Mapa interativo** — geolocalização de clientes por bairro em Petrolina

### 💾 Exportação de dados
- Tabela completa dos clientes filtrados
- Download em CSV com um clique

### ⚡ Performance
- Cache de dados com `st.cache_data` para carregamento rápido
- Geração de séries temporais cacheada
- Fallback automático para dados simulados quando o CSV não está disponível

---

## 🖥️ Screenshots

> **Dashboard principal com KPIs e filtros**
>
> *Adicione uma screenshot aqui após o primeiro deploy:*
> `![Dashboard Principal](docs/screenshot-dashboard.png)`

> **Mapa interativo de clientes por bairro**
>
> `![Mapa de Clientes](docs/screenshot-mapa.png)`

> **Gráficos de consumo e ranking**
>
> `![Gráficos](docs/screenshot-graficos.png)`

---

## 🚀 Como rodar localmente

### Pré-requisitos

- Python **3.9+**
- pip
- (Opcional) Ambiente virtual — recomendado

### 1. Clone o repositório

```bash
git clone https://github.com/Lfn22/casesimulado.git
cd casesimulado
```

### 2. Crie e ative o ambiente virtual

```bash
# Linux / macOS
python -m venv .venv
source .venv/bin/activate

# Windows (CMD)
python -m venv .venv
.venv\Scripts\activate

# Windows (PowerShell)
python -m venv .venv
.venv\Scripts\Activate.ps1
```

### 3. Instale as dependências

```bash
pip install streamlit pandas numpy plotly
```

> Ou, se o `requirements.txt` existir:
> ```bash
> pip install -r requirements.txt
> ```

### 4. Execute o dashboard

```bash
streamlit run datacase.py
```

O navegador abrirá automaticamente em **`http://localhost:8501`**

---

## 📁 Estrutura do projeto

```
casesimulado/
├── datacase.py              # Aplicação Streamlit principal
├── clientes_petrolina.csv   # Dataset de clientes (com fallback automático)
├── teste.txt                # Arquivo auxiliar de testes
└── README.md                # Documentação do projeto
```

### Arquitetura do código (`datacase.py`)

| Função / Componente | Responsabilidade |
|---|---|
| `load_data()` | Carrega CSV ou gera dados simulados como fallback |
| `compute_kpis()` | Calcula todos os indicadores principais |
| `render_hero()` | Renderiza o banner com KPIs sincronizados aos filtros |
| `render_filters()` | Sidebar com filtros responsivos em duas linhas |
| `render_charts()` | Renderiza todos os gráficos Plotly |
| `render_map()` | Mapa interativo com geolocalização por bairro |
| `BAIRRO_COORDS` | Dicionário de coordenadas geográficas dos bairros |

---

## 🗺️ Dataset — `clientes_petrolina.csv`

O arquivo CSV contém dados simulados de clientes de um provedor de internet de Petrolina/PE.

| Coluna | Tipo | Descrição |
|---|---|---|
| `cliente_id` | int | Identificador único do cliente |
| `nome` | string | Nome do cliente |
| `bairro` | string | Bairro em Petrolina/PE |
| `plano` | string | Tipo de plano (básico / intermediário / premium) |
| `consumo_mbps` | float | Consumo atual em Mbps |
| `limite_mbps` | float | Limite contratado em Mbps |
| `data_cadastro` | date | Data de início do contrato |

> **Fallback automático:** Se o CSV não for encontrado, o sistema gera automaticamente um dataset simulado com dados coerentes para demonstração.

---

## 🛠️ Tecnologias

| Tecnologia | Versão | Uso |
|---|---|---|
| Python | 3.9+ | Linguagem principal |
| Streamlit | latest | Interface web e componentes interativos |
| Pandas | latest | Manipulação e filtragem de dados |
| NumPy | latest | Geração de dados simulados e cálculos |
| Plotly | latest | Gráficos interativos e mapa geográfico |

---

## ⚙️ Personalização

### Adicionar novos bairros ao mapa

Edite o dicionário `BAIRRO_COORDS` em `datacase.py`:

```python
BAIRRO_COORDS = {
    "Centro": {"lat": -9.3891, "lon": -40.5028},
    "Novo Horizonte": {"lat": -9.3950, "lon": -40.5100},
    # Adicione novos bairros aqui:
    "Seu Bairro": {"lat": -9.XXXX, "lon": -40.XXXX},
}
```

### Adicionar novos KPIs

Edite a função `compute_kpis()` — ela é o ponto central de todas as métricas do dashboard.

### Adicionar novos gráficos

Adicione novas visualizações Plotly dentro da função `render_charts()`.

---

## 📦 Gerando o `requirements.txt`

Após instalar as dependências no ambiente virtual:

```bash
pip freeze > requirements.txt
```

---

## 🔎 Validação rápida do código

```bash
python -m compileall datacase.py
```

Verifica erros de sintaxe sem executar o app completo.

---

## 🗺️ Roadmap — próximas melhorias

- [ ] Autenticação de usuário (login para o provedor)
- [ ] Alertas automáticos para clientes críticos
- [ ] Integração com banco de dados PostgreSQL
- [ ] API REST para atualização de dados em tempo real
- [ ] Painel de inadimplência e cobrança
- [ ] Deploy em produção (Streamlit Cloud ou VPS)
- [ ] Exportação em PDF além de CSV

---

## 💡 Contexto de negócio

Este dashboard resolve um problema real e frequente em pequenas ISPs do interior do Nordeste: **gestores não têm visibilidade do consumo dos clientes em tempo real**, tomam decisões baseadas em planilhas desatualizadas e perdem receita por não identificar clientes em excedente.

Com este sistema, um provedor local de Petrolina consegue:
- Identificar quais bairros têm maior demanda de banda
- Priorizar upgrades de infraestrutura por região
- Abordar proativamente clientes em consumo crítico para upgrade de plano
- Gerar relatórios em CSV para reuniões comerciais

---

## 👨‍💻 Autor

**Lindomar Negreiros** — Engenheiro de Software | Fundador da [Negreiros Tech](https://github.com/Lfn22)

> *Desenvolvendo soluções de tecnologia para PMEs do interior do Nordeste.*

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/lindomar-lopes-de-negreiros-filho-4540b8220/)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat&logo=github&logoColor=white)](https://github.com/Lfn22)
[![Petrolina](https://img.shields.io/badge/📍_Petrolina,_PE-Nordeste-0D2150?style=flat)](https://github.com/Lfn22)

---

## 📄 Licença

Este projeto está sob a licença MIT. Desenvolvido como case de portfólio — livre para uso e adaptação com atribuição ao autor.

---

<div align="center">

**Negreiros Tech** · Petrolina, PE · 2025

</div>
