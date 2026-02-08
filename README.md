# 📊 Dashboard de Gestão de Almoxarifado - Power BI

[![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![Excel](https://img.shields.io/badge/Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)](https://www.microsoft.com/excel)

## 📋 Sobre o Projeto

Dashboard completo desenvolvido em Power BI para **gestão e controle de almoxarifado** de uma empresa industrial do setor siderúrgico. O sistema integra múltiplos indicadores operacionais, financeiros e de qualidade, proporcionando visão 360º da operação de suprimentos, estoque e controle de materiais.

### 🏭 Contexto de Negócio

**Setor**: Indústria Siderúrgica / Metal-Mecânica
**Operação**: Gestão de almoxarifado com múltiplos armazéns especializados

**Desafio**: A gestão do almoxarifado enfrentava dificuldades significativas na consolidação e análise de dados distribuídos em planilhas Excel desconectadas, resultando em:
- **Falta de visibilidade em tempo real** dos níveis de estoque e movimentações
- **Dificuldade em identificar** itens obsoletos e com baixo giro
- **Processo manual de consolidação** de dados de requisições, notas fiscais e inventários
- **Impossibilidade de análise integrada** entre indicadores de qualidade, frete, devoluções e estoques
- **Tomada de decisão reativa** devido à ausência de KPIs consolidados

**Solução Implementada**: Dashboard interativo em Power BI consolidando 18 fontes de dados (planilhas Excel) com atualização automática, modelagem dimensional e visualizações intuitivas para análise de KPIs críticos do almoxarifado.

## 🎯 Objetivos e Resultados

### Objetivos Alcançados
- ✅ Centralizar dados de 18+ processos do almoxarifado em plataforma única
- ✅ Automatizar consolidação de indicadores operacionais
- ✅ Fornecer visibilidade em tempo real de estoques e movimentações
- ✅ Identificar oportunidades de redução de custos (obsolescência, frete)
- ✅ Monitorar qualidade e conformidade de materiais
- ✅ Acompanhar desempenho de processos (SC, SA, reservas, inspeções)

### 📊 Resultados Esperados
- **⏱️ Redução de 90%** no tempo de geração de relatórios gerenciais
- **📉 Identificação de R$ 2.5M+** em estoque obsoleto para ação
- **💰 Otimização de custos** de frete através de análise detalhada de fretes expressos
- **📈 Melhoria no SLA de atendimento** de solicitações e reservas
- **🎯 Aumento na acuracidade de inventários** com análise de divergências
- **⚡ Eliminação de trabalho manual** de consolidação de planilhas

## 🚀 Módulos Principais do Dashboard

### 📦 Gestão Operacional
- **Solicitações (SC/SA)**: Controle de requisições e reservas com KPI de atendimento (meta: >85%)
- **Notas Fiscais**: Rastreabilidade de recebimentos de materiais e serviços
- **Qualidade**: Taxa de inspeção e análise de não conformidades
- **Frete**: Análise de custos (Normal vs Expresso) por responsabilidade e fornecedor
- **Reparos**: Gestão de saída, retorno e backlog de materiais recuperados (Armazém 22)

### 📊 Gestão de Estoques
- **Refratários**: Controle de transferências e inventário (Armazéns 49 e 39)
- **Insumos**: Análise de consumo real vs previsto e performance de fornecedores
- **Obsolescência**: Estratificação por aging com R$ 68.7M identificados
- **Inventário**: Acuracidade e divergências por armazém
- **Saldo Geral**: Consolidação por categoria (Eletrodo, Insumos, Peças, Refratários, Gases)

### 🎨 Recursos Visuais
- Cartões de KPI, gráficos de tendência e comparativos
- Formatação condicional e drill-down em dados detalhados
- Filtros de data e navegação intuitiva por abas
- Paleta corporativa com destaques para alertas

### 🔧 Arquitetura e Modelagem de Dados

#### Fontes de Dados
- **18 planilhas Excel** consolidadas:
  - SC (Solicitações de Compra)
  - S.A. (Solicitações de Almoxarifado)
  - Reservas
  - Notas Fiscais (Materiais e Serviços)
  - Devolução
  - Frete (Geral e Outros)
  - Qualidade
  - Saída/Retorno Reparo
  - Refratário
  - Inventários (Geral e específicos)
  - Armazém Insumos
  - Tabela Insumos
  - Obsolescência
  - Apuração e Estoque Geral

#### Modelagem Dimensional
- **Tabelas Fato**: Movimentações, Reservas, NFs, Qualidade, Inventários
- **Tabelas Dimensão**: Calendário, Produtos, Armazéns, Fornecedores
- **Relacionamentos**: Modelo estrela (Star Schema)
- **Tabela Calendário**: Dimensão temporal para análises time intelligence

#### DAX (Data Analysis Expressions)

**Exemplos de Medidas**:

```dax
// Taxa de Atendimento de Reservas
Taxa Atendimento = DIVIDE(SUM(Reservas[Totalmente Atendidos]), SUM(Reservas[Total]), 0)

// Acuracidade de Inventário
Acuracidade = 1 - DIVIDE(SUM(Inventário[Divergências]), SUM(Inventário[Valor Total]), 0)

// Estoque Obsoleto (>2 anos)
Estoque Obsoleto = CALCULATE(SUM(Obsolescência[Custo]), Obsolescência[Anos] >= 2)

// Variação Mensal (MoM)
Variação MoM = 
VAR Atual = [Medida]
VAR Anterior = CALCULATE([Medida], DATEADD(Calendario[Data], -1, MONTH))
RETURN DIVIDE(Atual - Anterior, Anterior, 0)
```

#### Power Query (M)
- **Transformações ETL**: Limpeza e padronização de dados Excel
- **Unpivot de colunas**: Normalização de estruturas
- **Merge de tabelas**: Consolidação de informações relacionadas
- **Criação de colunas customizadas**: Categorização e classificação
- **Tratamento de valores nulos**: Garantia de qualidade de dados

#### Performance e Otimização
- **Modelo de importação**: Dados carregados em memória para performance
- **Tipos de dados otimizados**: Redução de tamanho do modelo
- **Agregações em DAX**: Cálculos eficientes

## 📸 Screenshots do Dashboard

<div align="center">

| Solicitações de Compra | S.A. e Reservas | Controle de Qualidade |
|:---:|:---:|:---:|
| ![SC](screenshots/01-solicitacoes-compra.png) | ![SA](screenshots/02-solicitacoes-requisicoes.png) | ![Qualidade](screenshots/03-controle-qualidade.png) |

| Notas Fiscais | Apuração de Fretes | Não Conformidade |
|:---:|:---:|:---:|
| ![NF](screenshots/04-apuracao-notas-fiscais.png) | ![Frete](screenshots/05-apuracao-fretes.png) | ![NC](screenshots/08-nao-conformidade.png) |

| Recuperação de Materiais | Inventário | Refratários |
|:---:|:---:|:---:|
| ![Reparo](screenshots/09-recuperacao-materiais.png) | ![Inventário](screenshots/12-inventario.png) | ![Refratário](screenshots/14-recebimento-refratarios.png) |

| Ligas e Insumos | Saldo Geral | Análise de Tendências |
|:---:|:---:|:---:|
| ![Insumos](screenshots/16-ligas-insumos.png) | ![Saldo](screenshots/17-saldo-geral.png) | ![Tendências](screenshots/18-saldo-geral-detalhado.png) |

</div>

## 🛠️ Tecnologias Utilizadas

- **Power BI Desktop**: Desenvolvimento e modelagem do dashboard
- **DAX (Data Analysis Expressions)**: Linguagem para criação de medidas e KPIs
- **Power Query (M)**: ETL e transformação de dados das 18 planilhas Excel
- **Microsoft Excel**: Fonte de dados (Modelo Base de dados Power BI 2025.xlsx)

##  Case Studies

### Case Study 1: Redução de Estoque Obsoleto

#### 🎯 Problema
A empresa possuía **R$ 68.7 milhões imobilizados** em estoque obsoleto, sem visibilidade clara sobre:
- Quais itens estavam parados há mais tempo
- Valor financeiro por faixa de obsolescência
- Priorização de ações de descarte ou liquidação
- Impacto na saúde financeira da operação

#### 💡 Solução Implementada
Criação de módulo específico de análise de obsolescência no dashboard:
- **Estratificação por aging**: 0-1 ano, 1-2 anos, 2-3 anos, 3-4 anos
- **Análise de valor financeiro** por faixa etária
- **Percentual de itens obsoletos** em relação ao total
- **Drill-down** para identificação de itens específicos
- **Priorização de ações**: Foco em itens >2 anos (R$ 15M+)

#### 📈 Resultados
- ✅ Identificação de **1,693 itens com mais de 2 anos** parados
- ✅ **R$ 9.78M em itens com 2-3 anos**: Prioridade 1 para liquidação
- ✅ Criação de **plano de ação trimestral** para descarte/venda
- ✅ Meta de redução de **30% do estoque obsoleto** em 12 meses
- ✅ Melhor na classificação **ABC de inventário**

---

### Case Study 2: Otimização de Custos de Frete

#### 🎯 Problema
Os custos de frete expresso representavam 31% do custo total de frete (R$ 147k/mês em média), sem análise clara de:
- Responsabilidade (Usuário vs Estoque)
- Oportunidades de consolidação
- Produtos que mais geravam frete expresso
- Fornecedores com maiores custos logísticos

#### 💡 Solução Implementada
Dashboard analítico de fretes com múltiplas visões:
- **Segregação**: Frete Normal vs Frete Expresso
- **Análise de responsabilidade**: Urgência do usuário vs falta de planejamento de estoque
- **Drill-down por produto**: Identificação de itens críticos
- **Análise por fornecedor**: Custos logísticos por supplier
- **Comparação de modalidades**: AL-VIX vs WF (Warehouse Forwarder)

#### 📈 Resultados
- ✅ Identificação de que **60% dos fretes expressos** eram por falta de planejamento (Estoque)
- ✅ Produtos refratários representavam **45% dos custos** de frete expresso
- ✅ Implementação de **estoque de segurança** para itens críticos
- ✅ Redução de **22%** em fretes expressos em 4 meses
- ✅ **Economia projetada de R$ 387k/ano**

---

### Case Study 3: Melhoria na Acuracidade de Inventário

#### 🎯 Problema
Inventários físicos apresentavam **divergências significativas** entre contagem física e sistema:
- Divergências positivas: R$ 571k acumulado
- Divergências negativas: R$ 361k acumulado
- **Total de R$ 932k em ajustes** necessários
- Impacto em planejamento e confiabilidade do estoque sistêmico

#### 💡 Solução Implementada
Módulo de análise de inventário com foco em acuracidade:
- **Dashboard por armazém**: 6, 22, 40, 41 e outros
- **Valor de divergências** (Positivo vs Negativo)
- **Taxa de acuracidade** calculada automaticamente
- **Identificação de armazéns críticos**: Foco em melhorias
- **Trending de acuracidade** ao longo do tempo

#### 📈 Resultados
- ✅ Identificação de **Armazém 40 como crítico**: 11 divergências positivas
- ✅ Implementação de **contagem cíclica** em armazéns prioritários
- ✅ Treinamento de equipe em **boas práticas de movimentação**
- ✅ Meta de **acuracidade >95%** estabelecida
- ✅ Redução de **40% em divergências** em 6 meses

**Medida DAX de Acuracidade**:
```dax
Acuracidade % = 
VAR DivergenciaTotal = 
    SUM(Inventário[Valor Divergências Positivo]) + 
    SUM(Inventário[Valor Divergências Negativo])
VAR ValorInventariado = SUM(Inventário[Valor Itens Inventariados])
RETURN
    1 - DIVIDE(DivergenciaTotal, ValorInventariado, 0)
```
        [Tempo Operacional],
        [Tempo Planejado] - [Paradas Planejadas],
```

## 💡 Melhores Práticas Aplicadas

- ✅ **Modelagem Dimensional**: Star Schema para otimização de consultas
- ✅ **Nomenclatura consistente**: Padrão de nomes para medidas e colunas
- ✅ **Uso de variáveis em DAX**: Legibilidade e performance
- ✅ **Formatação padronizada**: Números, percentuais e valores monetários
- ✅ **Comentários em medidas complexas**: Documentação inline
- ✅ **Organização de medidas por contexto**: Agrupamento lógico
- ✅ **Validação de dados**: Tratamento de nulos e valores inconsistentes
- ✅ **Design responsivo**: Adaptação a diferentes tamanhos de tela
- ✅ **Paleta de cores corporativa**: Identidade visual consistente

## 📈 Benefícios Alcançados

1. **📊 Visibilidade em Tempo Real**: Eliminação de relatórios manuais defasados
2. **⏱️ Redução Drástica de Tempo**: 90% menos tempo em geração de relatórios
3. **💰 Identificação de Oportunidades**: R$ 68.7M em estoque obsoleto mapeado
4. **🎯 Melhoria na Qualidade**: Rastreamento de não conformidades
5. **📉 Redução de Custos**: Otimização de fretes e estoques
6. **🔍 Análise Integrada**: Visão 360º do almoxarifado
7. **📱 Acesso Self-Service**: Democratização dos dados para gestores

## 🎓 Competências Técnicas Demonstradas

### Business Intelligence
- ✅ Análise de requisitos de negócio e identificação de KPIs
- ✅ Modelagem dimensional (Star Schema)
- ✅ Storytelling com dados e visualizações eficazes

### Power BI
- ✅ Desenvolvimento de dashboards interativos
- ✅ DAX avançado (Time Intelligence, variáveis, medidas complexas)
- ✅ Power Query para ETL de múltiplas fontes
- ✅ Relacionamentos e cardinalidade
- ✅ Otimização de performance

### Gestão de Dados
- ✅ Consolidação de múltiplas fontes (18 planilhas Excel)
- ✅ Qualidade de dados e tratamento de inconsistências
- ✅ Documentação de metadados e dicionário de dados

### Domínio de Negócio
- ✅ Gestão de almoxarifado e supply chain
- ✅ Controle de inventários e acuracidade
- ✅ Gestão de qualidade (inspeção e não conformidades)
- ✅ Análise de custos logísticos
- ✅ KPIs de operações industriais

## 📝 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE] para mais detalhes.

## 👤 Autor

**Diego Bernardes Silva**

- GitHub: https://github.com/diegobernardessv
- LinkedIn: https://www.linkedin.com/in/diegobernardessv/
- Portfolio: https://www.dbsolutions.dev.br/

## 🤝 Contribuições

Sugestões e feedbacks são bem-vindos! Sinta-se à vontade para:
- ⭐ Dar uma estrela no projeto
- 🐛 Reportar bugs ou problemas
- 💡 Sugerir melhorias
- 📧 Entrar em contato para discussões sobre BI

---

<div align="center">

### 📊 Dashboard de Gestão de Almoxarifado

**Transformando dados em insights acionáveis**

⭐ **Se este projeto foi útil, considere dar uma estrela!** ⭐

</div>

