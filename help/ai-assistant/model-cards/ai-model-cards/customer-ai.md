---
title: Cartão do modelo de pontuação de propensão da IA do cliente
description: Saiba mais sobre o modelo de IA usado para a IA do cliente.
hide: true
hidefromtoc: true
source-git-commit: 21a95bd678cf83c72a08213b647ef778cfb49cfc
workflow-type: tm+mt
source-wordcount: '1629'
ht-degree: 0%

---

# Cartão do modelo de pontuação de propensão da IA do cliente

Como parte dos [Serviços inteligentes na Adobe Experience Platform](../../../intelligent-services/home.md), você pode usar a [IA do cliente](../../../intelligent-services/customer-ai/overview.md) para gerar previsões e explicações de clientes individualmente.

Com a ajuda de fatores influentes, você pode usar a IA do cliente para informar o que um cliente deve fazer e por quê. Além disso, você pode se beneficiar das previsões e insights da IA do cliente para personalizar as experiências do cliente, disponibilizando as ofertas e mensagens mais apropriadas.

Leia este cartão de modelo para obter informações sobre o modelo de IA usado para alimentar a IA do cliente.

## Visão geral do modelo {#model-overview}

* A IA do cliente é um modelo alimentado por IA projetado para gerar pontuações de propensão para usuários com base em seus comportamentos e interações anteriores com uma empresa. Use a IA do cliente para prever a probabilidade de um cliente realizar ações específicas, como fazer uma compra, participar de conteúdo ou churning. Esse modelo é implantado no Experience Platform e integra-se a vários workflows de marketing e de análise do cliente.
* O modelo foi projetado para fornecer insights acionáveis aos profissionais de marketing e equipes de engajamento do cliente, prevendo a probabilidade de um cliente executar determinada ação, como fazer uma compra, se inscrever em uma assinatura ou se envolver em uma campanha de email. As saídas permitem que as empresas otimizem a segmentação de público e personalizem as interações do cliente com base nos comportamentos previstos.
* Este é um **modelo de classificação de aprendizado supervisionado** que prevê a probabilidade de um evento ocorrer (compra, churn, envolvimento) de acordo com os dados históricos do cliente. Ele é treinado usando árvores de decisão de aumento de gradiente (GBDT) com regressão logística para pontuações de propensão do modelo.
* Os principais usuários desse modelo são profissionais de marketing, analistas de dados e equipes de envolvimento do cliente que usam o Experience Platform para impulsionar estratégias de marketing orientadas por dados.
* A IA do cliente integra-se diretamente aos serviços de IA da Experience Platform, permitindo que os usuários acessem as saídas do modelo por meio de APIs e painéis pré-criados. As pontuações de propensão geradas pelo modelo podem ser usadas no [Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/get-started) e no [Real-Time CDP](../../../rtcdp/home.md) para refinar a segmentação de público e adaptar as estratégias de marketing.

## Uso previsto {#intended-use}

* Este modelo é usado principalmente para **segmentação de clientes, marketing direcionado e previsão de churn**. As empresas usam esse modelo para **prever a intenção de compra do cliente, otimizar campanhas de marketing e aprimorar os esforços de personalização**. Por exemplo, uma empresa de comércio eletrônico pode usar o modelo para identificar compradores de alta intenção e oferecer promoções exclusivas.
* Os profissionais de marketing geralmente têm dificuldades em **identificar os clientes certos a serem direcionados** e **otimizar os esforços de engajamento**. Este modelo **reduz as suposições** ao fornecer uma abordagem orientada por dados para o direcionamento do cliente, garantindo que os recursos de marketing sejam alocados com eficiência.
* O modelo é aplicável em vários setores, incluindo comércio eletrônico, varejo, serviços financeiros, telecomunicações e mídia. Qualquer empresa que dependa do engajamento do cliente e do marketing personalizado pode se beneficiar desse modelo.
* O modelo **não deve ser usado para tomada de decisão de alto risco**, como pontuação de crédito financeiro, diagnóstico médico ou avaliações legais. Além disso, não se destina a ser usado na previsão de comportamentos pessoalmente sensíveis (condições de saúde, preferências políticas) devido a possíveis preocupações éticas.

## Entradas e saídas do modelo {#model-inputs-and-outputs}

* O modelo processa dados comportamentais do cliente, atributos demográficos e interações históricas. Isso inclui dados como frequência de visita ao site, histórico de compras anteriores, envolvimento com emails de marketing e informações demográficas.
* Os dados de entrada devem ser estruturados como objetos JSON contendo atributos do cliente e sinais comportamentais. Para processamento em lote, o modelo aceita arquivos CSV formatados de acordo com os padrões de assimilação de dados da Experience Platform.
* O modelo gera uma pontuação de propensão entre 0 e 1, em que valores mais altos indicam uma probabilidade mais alta de ocorrência do evento previsto. Além disso, fornece pontuações de importância de recursos, permitindo que os usuários entendam quais fatores influenciaram a previsão.

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
  "propensity_score": 0.82
}
```

## Dados de treinamento

* O modelo foi treinado em **dados próprios e anônimos de interação com o cliente** coletados pelo Experience Platform. Inclui dados históricos de **comportamento do cliente, registros de transações, interações por email e métricas de engajamento** em vários setores.
* O conjunto de dados de treinamento consiste em **10 milhões de registros de clientes** originados de um conjunto diverso de clientes da Experience Platform. Esses registros incluem **interações históricas com clientes, dados transacionais, logs de engajamento comportamental e informações demográficas** de vários setores, como varejo, comércio eletrônico, telecomunicações e finanças. Os dados foram coletados por um período de 24 meses, garantindo uma representação suficiente das tendências sazonais e dos padrões de engajamento de longo prazo.
* O conjunto de dados é predominantemente proveniente de usuários altamente engajados, o que pode introduzir viés de seleção. Para atenuar isso, o modelo aplica amostragem estratificada, técnicas de auditoria de polarização e estratégias de aumento de dados.
* O conjunto de dados passa por um extenso pré-processamento para garantir a consistência, a qualidade e a usabilidade dos dados.
   * **Tratamento de Valores Ausentes**: os valores ausentes são abordados usando uma combinação de imputação média (para campos numéricos), imputação de modo (para campos categóricos) e modelagem preditiva (para casos ausentes complexos).
   * **Codificação Categórica**: variáveis categóricas, como segmentos de clientes e categorias de compras, são convertidas em representações numéricas por meio de codificações instantâneas e técnicas de codificação de destino.
   * **Escala e Normalização de Recursos**: a escala mín-máx é aplicada às variáveis associadas (idade, renda), enquanto a padronização de pontuação z é usada para recursos distribuídos normalmente.
   * **Pré-processamento Adicional**: o pipeline inclui detecção e remoção de exceção, filtragem de duplicatas, padronização de carimbo de data/hora e engenharia de recursos para aprimorar a modelagem preditiva.

## Arquitetura de modelos e treinamento

* O modelo aproveita o **[!DNL Gradient Boosting Decision Trees](GBDT) usando o[!DNL XGBoost]**, otimizado para dados estruturados. Ele é treinado em sequências históricas de eventos do cliente para identificar padrões comportamentais preditivos.
* O modelo é construído usando uma abordagem de aprendizado supervisionada, aproveitando o GBDT com [!DNL XGBoost] como o algoritmo de aprendizado principal. Além disso, a regressão logística é incorporada como um modelo de linha de base para a avaliação de referência da precisão preditiva.
* O modelo foi desenvolvido usando **[!DNL TensorFlow]**, **[!DNL XGBoost]** e **[!DNL scikit-learn]**. O treinamento é executado na infraestrutura em nuvem da IA da Adobe usando **[!DNL NVIDIA V100]GPUs**, com suporte para conjuntos de dados em larga escala.
* [!DNL NVIDIA V100 GPUs], treinado em infraestrutura na Google Cloud.
* [!DNL AUC-ROC], recuperação de precisão e validação cruzada.

## Desempenho e avaliação

* O modelo foi testado usando uma abordagem de validação de validação de validação, onde 80% dos dados foram usados para treinamento e 20% foram reservados para avaliação.
* A eficácia do modelo é medida usando [!DNL AUC-ROC] (0,85), precision-recall (0,78) e F1-score (0,80). Essas métricas ajudam a avaliar a capacidade preditiva do modelo em diferentes segmentos.
* Menor precisão para novos segmentos de clientes com dados históricos limitados.
* O modelo pode ter um desempenho inferior para clientes com dados históricos limitados (problema de inicialização a frio). Além disso, os efeitos de sazonalidade (tendências de compras de feriados) podem exigir retreinamento frequente para manter a precisão.

## Equidade e viés

* O modelo foi submetido a **testes de paridade demográfica** e **avaliações de imparcialidade adversárias** para detectar disparidades de desempenho entre diferentes segmentos de usuários.
* A análise revelou uma queda de desempenho de **5% para usuários com dados históricos de interação baixos**. Para resolver isso, o modelo incorpora técnicas de reponderação durante o treinamento.
* O conjunto de dados é estratificado para garantir a representação proporcional de diferentes dados demográficos do cliente, e restrições de equidade são introduzidas durante o treinamento para evitar que o modelo favoreça qualquer grupo específico. Auditorias de viés regulares são realizadas usando análise de paridade demográfica, permitindo ajustes se forem detectadas disparidades de desempenho.

## Explicabilidade e interpretabilidade

* O modelo usa o **[!DNL SHapley Additive Explanations](SHAP)** para quantificar o impacto de cada recurso de entrada em suas previsões, fornecendo transparência em como os atributos do cliente influenciam as pontuações de propensão. Os valores SHAP permitem a interpretação global, identificando os fatores mais influentes em todas as previsões, e a interpretação local, explicando previsões individuais para clientes específicos.
* O modelo oferece suporte a **[!DNL Local Interpretable Model-Agnostic Explanations](LIME)** e SHAP para fornecer insights sobre como os recursos de entrada influenciam as previsões. LIME gera explicações locais criando versões perturbadas dos dados de entrada e observando mudanças nas previsões, enquanto SHAP atribui valores de contribuição para cada recurso, oferecendo tanto a interpretabilidade global quanto local das decisões do modelo.

## Robustez e generalização

* O modelo mantém 80% [!DNL AUC-ROC] quando testado em conjuntos de dados inéditos, demonstrando forte generalização para novos registros de clientes. O desempenho permanece estável em diferentes segmentos de clientes, mas mostra uma pequena degradação quando o comportamento do usuário se desvia significativamente dos padrões históricos.
* O modelo tem sido avaliado contra entradas perturbadas e adversárias, incluindo dados ausentes, injeção de valores anômalos e erro intencional de rotulagem. Embora o desempenho permaneça robusto em condições normais, uma pequena degradação da precisão (aproximadamente 3-5%) foi observada sob modificações adversárias extremas.

## Considerações de segurança e privacidade

* O modelo **não processa nem retém informações de identificação pessoal (PII)**, e todos os dados usados para treinamento são anônimos e agregados. Ela segue rigorosa conformidade com as políticas internas de privacidade do GDPR, CCPA e Adobe para garantir o uso responsável dos dados.
* O modelo incorpora técnicas de privacidade diferencial para adicionar ruído controlado aos dados, impedindo a reidentificação de indivíduos. Além disso, **métodos de hash, anonimização e geração de tokens são usados para remover PII** antes do treinamento e da inferência do modelo.

## Implantação e integração

* O modelo é hospedado em serviços de IA da Adobe Experience Platform e integrado a vários aplicativos da Adobe. Ele está disponível por meio de endpoints de API, permitindo acesso perfeito para previsões em tempo real e processamento em lote em fluxos de trabalho de marketing e de envolvimento do cliente.
* O modelo é executado em uma implantação baseada em **[!DNL Kubernetes]** com recursos de dimensionamento automático para lidar com cargas de trabalho variadas com eficiência. Os recursos de computação incluem [!DNL NVIDIA V100] GPUs para treinamento e inferência otimizada baseada em CPU para escalabilidade em tempo real.

## Monitoramento e manutenção

* O modelo é continuamente **monitorado por[!DNL WatsonX]**, rastreando indicadores chave de desempenho, como desvio de precisão, deslocamentos de importância de recursos e estabilidade de previsão. Os mecanismos de detecção e alerta de anomalias notificam a equipe quando ocorrem desvios significativos do comportamento esperado.
* O modelo é retreinado mensalmente usando dados atualizados de interação com o cliente para garantir relevância contínua. O novo treinamento periódico ajuda a reduzir a deriva de dados e as flutuações sazonais que podem afetar a precisão preditiva

## Preocupações éticas e IA responsável

* O modelo poderia potencialmente introduzir distorções na tomada de decisões se não fosse monitorizado corretamente. Por exemplo, se certos dados demográficos estiverem superrepresentados nos dados de treinamento, o modelo pode favorecer injustamente grupos específicos de clientes.
* A Experience Platform segue as diretrizes de IA responsáveis, garantindo que os modelos sejam submetidos a **auditorias de viés, testes de integridade e supervisão humana** antes da implantação.

## Limitações conhecidas

* O modelo pode ter dificuldades para prever com precisão os resultados de produtos recém-lançados ou segmentos de clientes nos quais os dados históricos insuficientes estão disponíveis. Além disso, variações sazonais no comportamento do cliente podem causar flutuações na precisão preditiva se não forem consideradas durante o novo treinamento.
* O desempenho diminui quando o histórico do cliente é escasso, como para compradores pela primeira vez ou usuários com dados mínimos de engajamento. Além disso, se o comportamento do cliente **mudar devido a fatores externos, como recessões econômicas ou tendências do setor**, o modelo pode exigir adaptação rápida para manter a precisão.

## Melhorias futuras

* As iterações futuras incluirão técnicas de aprendizado de transferência para melhorar o desempenho para usuários de partida a frio e aprimorar a adaptabilidade a mudanças de comportamento do cliente. Além disso, a integração de dados em tempo real será introduzida para melhorar a capacidade de resposta e a precisão do modelo em ambientes de marketing dinâmicos.
