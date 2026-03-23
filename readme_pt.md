# 📊 Dashboard de Análise de Suporte ao Cliente

> Dashboard desenvolvido em Power BI para fins de portfolio, com análise de dados de tickets de suporte ao cliente a partir de um dataset do Kaggle. O projeto cobre o fluxo analítico completo — da avaliação da qualidade dos dados até insights acionáveis para tomadores de decisão.

---

## 📁 Estrutura do Projeto

```
Customer Support Ticket Dataset/
├── Backgrounds/        # Backgrounds PNG utilizados nas páginas do Power BI
├── Dashboard/          # Arquivo Power BI (.pbix)
├── Data/               # Dataset original (CSV)
├── Images/             # Prints do dashboard
└── README.md
```

---

## 🗂️ Páginas do Dashboard

| Página | Descrição |
|--------|-----------|
| **Overview** | Visão executiva com KPIs principais, tendência mensal e navegação |
| **Tickets** | Análise operacional — volume, status, prioridade e SLA |
| **CSAT** | Análise de satisfação do cliente — escala de 1 a 5 |
| **Produtos** | Análise de atrito e experiência por produto |
| **Clientes** | Análise individual — volume e satisfação por cliente |
| **Insights & Próximos Passos** | Lacunas de dados e recomendações para os times |

---

## 📸 Preview do Dashboard

### Overview
![Overview](Images/01_Overview.png)

### Tickets
![Tickets](Images/02_Tickets.png)

### CSAT
![CSAT](Images/03_CSAT.png)

### Produtos
![Produtos](Images/04_Products.png)

### Clientes
![Clientes](Images/05_Customers.png)

### Insights & Próximos Passos
![Insights](Images/06_Insights&Next_Steps.png)

---

## 🛠️ Ferramentas e Tecnologias

- **Power BI Desktop** — desenvolvimento do dashboard
- **DAX** — medidas e colunas calculadas
- **Power Query (M)** — transformação de dados
- **PowerPoint** — design dos backgrounds

---

## 📐 Modelo de Dados

O dataset é uma tabela única desnormalizada contendo todas as informações dos tickets. Uma **tabela Calendário** foi criada via DAX (`CALENDARAUTO()`) e conectada à tabela fato através da coluna `Date of Purchase`.

Uma tabela `_Measures` foi criada para organizar todas as medidas DAX.

**Principais medidas criadas:**

| Medida | Descrição |
|--------|-----------|
| `01 Total Tickets` | Contagem total de linhas |
| `02 Open Tickets` | Tickets com status = Open |
| `03 Closed Tickets` | Tickets com status = Closed |
| `04 Pending Tickets` | Tickets com status = Pending Customer Response |
| `05 AVG CSAT` | Média de satisfação do cliente |
| `06 AVG Ticket Duration` | Tempo médio de resolução (apenas valores positivos) |
| `07 SLA %` | % de tickets fechados dentro do prazo de SLA |
| `08 Tickets Not Initialized` | Tickets sem First Response Time registrado |
| `09 Tickets +X Days Without Resolution` | Contagem dinâmica baseada no slicer de threshold |

---

## ⚠️ Problemas de Qualidade dos Dados

Durante a análise, diversos problemas de qualidade foram identificados e documentados:

1. **~49% dos tickets fechados com duração negativa** — o Time to Resolution é anterior ao First Response Time, indicando erros de input no sistema de origem.
2. **Ausência de data de abertura do ticket** — toda análise temporal está ancorada na `Date of Purchase`, não no momento real do contato com o suporte.
3. **33% dos tickets abertos sem nenhuma primeira resposta** — 2.819 tickets nunca foram atendidos.
4. **CSAT restrito a tickets fechados** — 67% da base (5.700 tickets) não tem avaliação de satisfação.
5. **Ausência do status "In Progress"** — o ciclo de vida do ticket está incompleto, impossibilitando análise de tempo por etapa.
6. **Sem ID único de cliente** — o e-mail foi usado como chave substituta com ressalvas documentadas.
7. **Tabela única desnormalizada** — sem modelagem dimensional; IDs de produto, cliente e canal estão ausentes.
8. **Sem dados de NPS** — apenas CSAT transacional disponível; lealdade do cliente não pode ser medida.
9. **Confiabilidade do SLA** — 0 violações registradas, mas ~49% dos dados de tempo são inconsistentes, tornando essa métrica não confiável.

---

## 📋 Ações Recomendadas por Time

| Time | Ação |
|------|------|
| **Suporte** | Investigar inputs de duração negativa · Priorizar os 2.819 tickets sem primeira resposta |
| **CS** | Expandir coleta de CSAT para além dos tickets fechados · Implementar pesquisa NPS periódica |
| **Produto / Engenharia** | Adicionar Ticket Open Date e status "In Progress" · Criar IDs únicos de cliente e produto |
| **Dados** | Normalizar dataset em tabelas fato e dimensão |
| **CS / CRM** | Enriquecer dataset com valor de contrato e tier do cliente para análise por conta estratégica |

---

## 🗺️ Roadmap do Dashboard

| Fase | Objetivo |
|------|----------|
| **Fase 1** | Adicionar Ticket Open Date — habilitar análise real de tempo de primeira resposta |
| **Fase 2** | ID único de cliente — rastreamento completo da jornada do cliente |
| **Fase 3** | Integração com NPS — dashboard de lealdade separado do CSAT |
| **Fase 4** | Monitoramento em tempo real — alertas para violações de SLA e thresholds de resposta |

---

## 📦 Dataset

- **Fonte:** [Customer Support Ticket Dataset — Kaggle](https://www.kaggle.com/datasets/suraj520/customer-support-ticket-dataset)
- **Período:** 2020–2021
- **Volume:** 8.469 tickets · 26 produtos · 4 canais de suporte
- **Autor do dataset:** suraj520

---

## 👤 Autor

**Marcelo Nepomuceno Marcos** — Portfolio de Data Analytics  
https://www.linkedin.com/in/marcelonepomuceno/ 
·https://github.com/MarceloNMarcos

> *Este projeto foi desenvolvido para fins de aprendizado e portfolio. Todas as decisões analíticas, identificação de problemas de qualidade e recomendações foram desenvolvidas de forma independente a partir da exploração dos dados.*