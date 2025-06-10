---
title: Detalhes do modelo de pontuação de propensão da IA do cliente
description: Saiba mais sobre o modelo de IA usado para a IA do cliente.
hide: true
hidefromtoc: true
exl-id: b2eeb1d2-3c2b-40a0-b5cd-91e99d99a906
source-git-commit: 8230c71c9b7896dfb71506632754d48583d0dc21
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 0%

---

# Detalhes do modelo de pontuação de propensão da IA do cliente

## Visão geral do modelo {#model-overview}

* **Nome e versão do modelo**: modelo de pontuação de propensão da IA do cliente
* **Finalidade do modelo**: o modelo foi criado para fornecer insights acionáveis aos profissionais de marketing e às equipes de engajamento do cliente, prevendo a probabilidade de um consumidor executar determinada ação, como fazer uma compra, se inscrever em uma assinatura ou participar de uma campanha por email. As saídas permitem que as empresas otimizem a segmentação de público e personalizem as interações do consumidor com base nos comportamentos previstos.
* **Usuários pretendidos**: os principais usuários deste modelo são profissionais de marketing, analistas de dados e equipes de engajamento do cliente que usam o [Real-Time CDP](../../../rtcdp/home.md) para impulsionar estratégias de marketing orientadas por dados.
* **Casos de uso**: esse modelo é usado principalmente para segmentação do consumidor, marketing direcionado e previsão de churn. As empresas usam esse modelo para prever a intenção de compra do consumidor, otimizar campanhas de marketing e aprimorar os esforços de personalização. Por exemplo, uma empresa de comércio eletrônico pode usar o modelo para identificar compradores de alta intenção e oferecer promoções exclusivas.
* **Pontos problemáticos**: os profissionais de marketing geralmente têm dificuldades em identificar os consumidores certos e em otimizar os esforços de engajamento. Esse modelo reduz as suposições ao fornecer uma abordagem orientada por dados para o direcionamento do consumidor, garantindo que os recursos de marketing sejam alocados com eficiência.
* **Possível uso incorreto**: o modelo não deve ser usado para casos de uso de alto risco, como pontuação de crédito financeiro, diagnóstico médico ou avaliações legais. Além disso, o modelo não deve ser usado na previsão de comportamentos pessoalmente sensíveis (como condições de saúde, preferências políticas).

## Detalhes do modelo {#model-details}

* **Tipo de modelo**: este é um modelo de classificação de aprendizado supervisionado que prevê a probabilidade de ocorrência de um evento (como compra, churn, envolvimento) de acordo com os dados históricos do consumidor. Ele é treinado usando árvores de decisão de aumento de gradiente (GBDT) com regressão logística para pontuações de propensão do modelo.
* **Entrada**: o modelo processa dados comportamentais do consumidor, atributos demográficos e interações históricas. Isso inclui dados como frequência de visita ao site, histórico de compras anteriores, envolvimento com emails de marketing e informações demográficas.
* **Saída**: o modelo gera uma pontuação entre 0 e 100, em que valores mais altos indicam uma probabilidade maior de o evento previsto ocorrer entre o coorte de população pontuado. Além disso, fornece pontuações de importância de recursos, permitindo que os profissionais de marketing entendam quais fatores influenciaram a previsão.

**Exemplo de entrada**

```json
{ 
  "customer_id": 12345, 
  "past_purchases": 3, 
  "last_visit_days": 7,
  "email_click_rate": 0.4 
}
```

**Exemplo de saída**

```json
{ 
  "customer_id": 12345,
  "SCORE": 89 
}
```

## Treinamento de modelo {#model-training}

* **Dados de treinamento e pré-processamento**: o conjunto de dados de treinamento para cada cliente é originado diretamente de seus próprios dados na Adobe Experience Platform. Isso inclui interações históricas do cliente, registros transacionais, logs de envolvimento comportamental e informações demográficas, conforme coletadas e armazenadas na instância do Adobe Experience Platform. O conjunto de dados aproveita dados específicos do cliente ao longo do período escolhido, capturando suas tendências sazonais exclusivas e os padrões de engajamento. Antes de usar, o conjunto de dados de cada cliente passa por um pré-processamento adaptado às suas características de dados, incluindo manipulação de valor ausente, codificação categórica, dimensionamento de recursos, detecção de valores atípicos e engenharia de recursos para garantir a qualidade e a usabilidade ideais para seu caso de uso específico.
   * Os dados do consumidor usados para treinamento não são usados entre clientes.
* **Especificações de treinamento**: o modelo aproveita [!DNL LightGBM] usando [!DNL GBM], otimizado para dados estruturados. Ele é treinado em sequências históricas de eventos do cliente para identificar padrões comportamentais preditivos.
* **Estruturas de treinamento**: o modelo foi desenvolvido com o [!DNL LightGBM] e o [!DNL scikit-learn] e está hospedado na infraestrutura em nuvem da IA do Adobe.
* **Infraestrutura de treinamento**: [!DNL Databricks] clusters.

## Avaliação do modelo {#model-evaluation}

* **Métricas e procedimentos de avaliação**: a eficácia do modelo é medida usando [!DNL AUC-ROC]. Como a IA do cliente está direcionando uma grande variedade de casos de uso de clientes, o intervalo operacional não pode ser conhecido. Portanto, usamos uma métrica [!DNL AUC] que é independente de alcance e orçamento.
* **Dados de avaliação e pré-processamento**: os dados de avaliação incluem registros de consumidor de controle e são pré-processados de forma semelhante aos dados de treinamento com etapas de normalização, codificação e limpeza de recursos para corresponder às expectativas de formato de entrada. Depois que a janela de resultados passar, poderemos executar uma avaliação final de desempenho.

## Implantação do modelo {#model-deployment}

* **Implantação do modelo**: o modelo está hospedado nos serviços de IA da Adobe Experience Platform e integrado a vários aplicativos da Adobe. Ele está disponível por meio de endpoints de API, permitindo acesso perfeito para previsões em tempo real e processamento em lote em fluxos de trabalho de marketing e envolvimento do consumidor.
* **Monitoramento de modelo**: o modelo é monitorado continuamente por meio do monitoramento de modelo para ver o descompasso da configuração de treinamento. Treinos periódicos (uma vez a cada 3 meses) são executados automaticamente.
* **Atualização de modelo**: o modelo é retreinado uma vez a cada vários meses (no máximo uma vez a cada 6 meses) usando dados atualizados de interação com o consumidor para garantir relevância contínua. O novo treinamento periódico ajuda a reduzir a deriva de dados e as flutuações sazonais que podem afetar a precisão preditiva.

## Explicabilidade {#explainability}

**Explicabilidade do modelo**: o modelo usa o [!DNL SHapley Additive Explanations] (SHAP) para quantificar o impacto de cada recurso de entrada em suas previsões, fornecendo transparência em como os atributos do consumidor influenciam as pontuações de propensão. Os valores SHAP permitem tanto a interpretabilidade global, identificando os fatores mais influentes em todas as previsões, quanto a interpretabilidade local, explicando previsões individuais para consumidores específicos. O modelo também oferece suporte a [!DNL Local Interpretable Model-Agnostic Explanations] (LIME).

## Equidade e viés {#fairness-and-bias}

* **Integridade do modelo**: este modelo é treinado em dados comportamentais anônimos associados a IDs de cookies, sem acesso a atributos demográficos protegidos, como idade, gênero ou etnia. Como tal, a medição direta da equidade entre grupos sensíveis não é viável. Os esforços de mitigação de polarização incluem a normalização da frequência de atividade do usuário, a supressão de recursos excessivamente dominantes e a realização de verificações de calibração de pontuação entre coortes. Consideramos o viés de recenticidade e monitoramos o viés de exposição avaliando as previsões do modelo no tráfego de validação aleatório. As avaliações contínuas estão em vigor para detectar e reduzir a amplificação de polarização e os loops de feedback durante a implantação do modelo.
* **Vieses de dados**: o conjunto de dados é predominantemente originário de usuários de alto engajamento, o que pode introduzir viés de seleção. Para atenuar isso, o modelo aplica estratégias de amostragem. Dependendo do caso de uso, os clientes devem considerar como possíveis distorções nas saídas do modelo podem se alinhar ou afetar a aplicação desejada.

## Robustez {#robustness}

**Robustez do modelo**: o modelo mantém uma forte generalização para novos registros de consumidor. O desempenho permanece estável em diferentes segmentos de consumidores, mas mostra uma pequena degradação quando o comportamento do usuário se desvia significativamente dos padrões históricos.

## Considerações éticas {#ethical-considerations}

**Considerações éticas associadas ao modelo**: este modelo destina-se a casos de uso de marketing. Os clientes devem ter mais cuidado ao aplicá-lo em domínios confidenciais ou regulamentados, como crédito ou emprego. As saídas são probabilísticas e derivadas de dados comportamentais, que podem refletir vieses históricos ou de representação. Os clientes são incentivados a aplicar a supervisão humana. A Adobe Experience Platform segue as diretrizes da IA responsável, garantindo que os modelos sejam submetidos a auditorias de viés, testes de equidade e supervisão humana antes da implantação. Para obter mais informações, reveja os [Princípios éticos da IA da Adobe](https://www.adobe.com/content/dam/cc/en/ai-ethics/pdfs/Adobe-AI-Ethics-Principles.pdf?msockid=0d85c8269eb36f0801d0ddb49fd16ebc).