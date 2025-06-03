---
title: Cartão do modelo de pontuação de propensão da IA do cliente
description: Saiba mais sobre o modelo de IA usado para a IA do cliente.
hide: true
hidefromtoc: true
exl-id: b2eeb1d2-3c2b-40a0-b5cd-91e99d99a906
source-git-commit: dddd699f231d54ee44b33f86a5c9e59c0aedc30c
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 0%

---

# Cartão do modelo de pontuação de propensão da IA do cliente

## Visão geral do modelo {#model-overview}

* O Modelo de pontuação de propensão da IA do cliente foi projetado para fornecer insights acionáveis aos profissionais de marketing e equipes de envolvimento do cliente, prevendo a probabilidade de um cliente executar uma determinada ação, como fazer uma compra, se inscrever em uma assinatura ou se envolver em uma campanha de email. As saídas permitem que as empresas otimizem a segmentação de público e personalizem as interações do cliente com base nos comportamentos previstos.
* Os principais usuários deste modelo são profissionais de marketing, analistas de dados e equipes de engajamento do cliente que usam o [Real-Time CDP](../../../rtcdp/home.md) para impulsionar estratégias de marketing orientadas por dados.
* Esse modelo é usado principalmente para segmentação de clientes, marketing direcionado e previsão de churn. As empresas usam esse modelo para prever a intenção de compra do cliente, otimizar campanhas de marketing e aprimorar os esforços de personalização. Por exemplo, uma empresa de comércio eletrônico pode usar o modelo para identificar compradores de alta intenção e oferecer promoções exclusivas.
* Os profissionais de marketing geralmente lutam para identificar os clientes certos e otimizar os esforços de engajamento. Esse modelo reduz as suposições ao fornecer uma abordagem orientada por dados para o direcionamento do cliente, garantindo que os recursos de marketing sejam alocados com eficiência.
* O modelo não deve ser usado para tomadas de decisão de alto risco, como pontuação de crédito financeiro, diagnósticos médicos ou avaliações legais. Além disso, não se destina a ser usado na previsão de comportamentos pessoalmente sensíveis (por exemplo, condições de saúde, preferências políticas) devido a possíveis preocupações éticas.

## Detalhes do modelo {#model-details}

* Este é um modelo de classificação de aprendizado supervisionado que prevê a probabilidade de um evento ocorrer (compra, churn, envolvimento) de acordo com os dados históricos do cliente. Ele é treinado usando árvores de decisão de aumento de gradiente (GBDT) com regressão logística para pontuações de propensão do modelo.
* O modelo processa dados comportamentais do cliente, atributos demográficos e interações históricas. Isso inclui dados como frequência de visita ao site, histórico de compras anteriores, envolvimento com emails de marketing e informações demográficas.
* O modelo gera uma pontuação entre 0 e 100, em que valores mais altos indicam uma probabilidade mais alta de o evento previsto ocorrer entre o coorte de população pontuada. Além disso, fornece pontuações de importância de recursos, permitindo que os usuários entendam quais fatores influenciaram a previsão.

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

* O conjunto de dados de treinamento para cada cliente é originado diretamente de seus próprios dados na Experience Platform. Isso inclui as interações históricas do cliente, registros transacionais, logs de envolvimento comportamental e informações demográficas, conforme coletadas e armazenadas na instância do Experience Platform. O conjunto de dados aproveita dados específicos do cliente ao longo do período escolhido, capturando suas tendências sazonais exclusivas e os padrões de engajamento. Antes de usar, o conjunto de dados de cada cliente passa por um pré-processamento adaptado às suas características de dados, incluindo manipulação de valor ausente, codificação categórica, dimensionamento de recursos, detecção de valores atípicos e engenharia de recursos para garantir a qualidade e a usabilidade ideais para seu caso de uso específico.
* O modelo aproveita o [!DNL LightGBM] usando o [!DNL GBM], otimizado para dados estruturados. Ele é treinado em sequências históricas de eventos do cliente para identificar padrões comportamentais preditivos.
* O modelo foi desenvolvido usando o [!DNL LightGBM] e o [!DNL scikit-learn] e é treinado em infraestrutura em nuvem da IA do Adobe.
* Os recursos de computador usados para o treinamento de modelo são clusters [!DNL Databricks].

## Avaliação do modelo {#model-evaluation}

* A eficácia do modelo é medida usando [!DNL AUC-ROC]. Como a IA do cliente está direcionando uma grande variedade de casos de uso de clientes, o intervalo operacional não pode ser conhecido. Portanto, a métrica [!DNL AUC] é usada porque não depende de alcance e orçamento.
* Os dados de avaliação incluem registros de clientes independentes e são pré-processados de forma semelhante aos dados de treinamento com normalização de recursos, codificação e etapas de limpeza para corresponder às expectativas de formato de entrada. Depois que a janela de resultados passar, a avaliação final de desempenho poderá ser realizada.

## Implantação do modelo {#model-deployment}

* O modelo é hospedado em serviços de IA da Experience Platform e integrado a vários aplicativos da Adobe. Ele está disponível por meio de endpoints de API, permitindo acesso perfeito para previsões em tempo real e processamento em lote em fluxos de trabalho de marketing e de envolvimento do cliente.
* O modelo é continuamente monitorado por meio do monitoramento do modelo para ver o desvio em relação à configuração do treinamento. Treinos periódicos (uma vez a cada 3 meses) são executados automaticamente.
* O modelo é treinado novamente uma vez a cada vários meses (no máximo uma vez a cada seis meses) usando dados atualizados de interação com o cliente para garantir relevância contínua. O novo treinamento periódico ajuda a reduzir a deriva de dados e as flutuações sazonais que podem afetar a precisão preditiva.

## Explicabilidade {#explainability}

O modelo usa o [!DNL SHapley Additive Explanations] (SHAP) para quantificar o impacto de cada recurso de entrada em suas previsões, fornecendo transparência em como os atributos do cliente influenciam as pontuações de propensão. Os valores SHAP permitem a interpretação global, identificando os fatores mais influentes em todas as previsões, e a interpretação local, explicando previsões individuais para clientes específicos. O modelo também oferece suporte a [!DNL Local Interpretable Model-Agnostic Explanations] (LIME).

## Equidade e viés {#fairness-and-bias}

* Esse modelo é treinado em dados comportamentais anônimos associados a IDs de cookie, sem acesso a atributos demográficos protegidos, como idade, gênero ou etnia. Como tal, a medição direta da equidade entre grupos sensíveis não é viável. Os esforços de mitigação de polarização incluem a normalização da frequência de atividade do usuário, a supressão de recursos excessivamente dominantes e a realização de verificações de calibração de pontuação entre coortes.
* O modelo leva em conta o viés de recenticidade e monitora o viés de exposição avaliando as previsões do modelo no tráfego de validação aleatório. As avaliações contínuas estão em vigor para detectar e reduzir a amplificação de polarização e os loops de feedback durante a implantação do modelo.
* O conjunto de dados é predominantemente proveniente de usuários altamente engajados, o que pode introduzir viés de seleção. Para atenuar isso, o modelo aplica estratégias de amostragem.

## Robustez {#robustness}

O modelo mantém uma forte generalização para novos registros de clientes. O desempenho permanece estável em diferentes segmentos de clientes, mas mostra uma pequena degradação quando o comportamento do usuário se desvia significativamente dos padrões históricos.

## Considerações de privacidade e segurança {#privacy-and-security-considerations}

* O modelo não processa nem retém informações de identificação pessoal (PII) e todos os dados usados para treinamento são anonimizados e agregados. Ela segue a estrita conformidade com o GDPR, a CCPA e as políticas internas de privacidade da Adobe. O modelo incorpora técnicas de privacidade diferencial, hash, anonimização e tokenização para garantir a privacidade.
* A IA do cliente respeita suas preferências de consentimento. Depois de [configurar e habilitar sua política de consentimento](../../../data-governance/policies/user-guide.md#create-a-consent-policy), a IA do cliente respeitará os dados de consentimento coletados de você. Somente dados consentidos são usados para pontuar o modelo em execuções subsequentes do modelo. As novas pontuações substituirão as pontuações antigas e poderão ser usadas na segmentação. No momento, esse recurso está disponível apenas para clientes do HealthCare Shield e clientes do Privacy and Security Shield.

## Considerações éticas {#ethical-considerations}

O modelo poderia potencialmente introduzir preconceitos na tomada de decisões. Como esforço para evitar isso, a Experience Platform segue as diretrizes da IA responsável, garantindo que os modelos sejam submetidos a auditorias de viés, testes de equidade e supervisão humana antes da implantação.
