NPS Preditivo em E-commerce
Visão Geral do Projeto

Este projeto tem como objetivo analisar e prever clientes com alto risco de se tornarem detratores de NPS (Net Promoter Score) em um e-commerce.

A proposta combina Análise Exploratória de Dados (EDA) com modelos de Machine Learning, buscando identificar os principais fatores operacionais que impactam negativamente a experiência do cliente.

Objetivo
Identificar fatores que influenciam a insatisfação do cliente
Entender padrões de comportamento de detratores
Criar um modelo preditivo para classificar clientes em:
Detrator (NPS ≤ 6)
Não detrator (NPS > 6)
Gerar insights acionáveis para melhoria da operação
Estrutura do Projeto
📁 projeto-nps
│
├── eda_spark.ipynb          # Análise exploratória com Spark SQL
├── modelagem_ml.ipynb       # Random Forest e Regressão Linear
├── dataset.csv              # Base de dados
└── README.md                # Documentação
Dataset

A base contém 2.500 registros e 19 variáveis, incluindo:

Dados de cliente (idade, região, tempo de relacionamento)
Dados de pedido (valor, itens, desconto)
Indicadores logísticos (atraso, tentativas de entrega)
Indicadores de suporte (contatos, reclamações, tempo de resolução)
NPS score (variável alvo)
Preparação dos Dados

Foram realizadas as seguintes etapas:

Remoção de variáveis com risco de data leakage:
nps_score
customer_id
order_id
Criação da variável alvo:
is_detrator = 1 (NPS ≤ 6)
Encoding de variáveis categóricas com Label Encoding
Engenharia de atributos com foco em risco operacional
Análise Exploratória (EDA)

A análise foi realizada com Spark SQL, Pandas e Seaborn.

Principais insights:

74% dos clientes são detratores
Atrasos acima de 3 dias aumentam fortemente a insatisfação
Mais de 3 contatos com suporte indicam alto risco de detratação
5 ou mais reclamações representam nível crítico de insatisfação
Resolução acima de 10 dias reduz significativamente o NPS
Fatores operacionais têm impacto maior que fatores demográficos
Pontos de Ruptura Identificados
Fator	Ponto crítico	Impacto
Atraso de entrega	3+ dias	Forte aumento de detratores
Suporte	3+ contatos	Alto risco de insatisfação
Reclamações	5+	Nível crítico
Resolução	10+ dias	Queda significativa de NPS
Modelagem Preditiva

Foram utilizados dois modelos:

Random Forest (modelo principal)
Captura relações não lineares
Melhor performance geral
ROC-AUC: ~0.86
F1-score: ~0.89
Regressão Linear (baseline)
Modelo simples e interpretável
Usado apenas como referência de comparação
Resultados do Modelo
Melhor modelo: Random Forest
Boa capacidade de identificar detratores
Variáveis mais importantes:
complaints_count
delivery_delay_days
risco_operacional_score
customer_service_contacts
resolution_time_days
Feature Engineering

Foi criado um score de risco operacional baseado em sinais críticos:

Atraso ≥ 3 dias
≥ 3 contatos com suporte
≥ 5 reclamações
Resolução ≥ 10 dias

Esse score permite identificar clientes em risco antes da perda de satisfação.

Conclusões
O problema de NPS está mais ligado a falhas operacionais do que ao perfil do cliente
Logística e suporte são os principais fatores de insatisfação
Pequenos atrasos já impactam fortemente a experiência
Existe um grupo de clientes de alto risco que pode ser prevenido com ações antecipadas
Recomendações de Negócio
Criar alertas para pedidos com risco de 3+ dias de atraso
Escalonar atendimento no segundo contato com suporte
Priorizar casos com 5+ reclamações
Monitorar SLA acima de 10 dias de resolução
Utilizar o score de risco operacional para ações preventivas
Tecnologias Utilizadas
Python
PySpark
Pandas / NumPy
Scikit-learn
Seaborn / Matplotlib
