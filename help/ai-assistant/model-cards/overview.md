---
title: Cartões modelo para transparência do modelo de IA no Adobe Experience Platform
description: Saiba mais sobre cartões de modelo no Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: 21a95bd678cf83c72a08213b647ef778cfb49cfc
workflow-type: tm+mt
source-wordcount: '2386'
ht-degree: 0%

---

# Modelos de cartões para a transparência do modelo de IA no Adobe Experience Platform

Os cartões modelo são os formatos padrão pelos quais a transparência do modelo de IA é comunicada. Os cartões-modelo são públicos e têm como objetivo melhorar a compreensão dos clientes atuais e em potencial dos modelos de IA que o Adobe usa. As placas-modelo são geralmente estáticas. No entanto, há vários aspectos dos modelos de IA que podem mudar com o tempo, incluindo linhagem, viés e outros atributos de transparência.

Leia este documento para saber mais sobre cartões de modelo no Adobe Experience Platform.

## Seções do cartão de modelo {#model-card-sections}

Leia o seguinte para obter um guia sobre as diferentes seções de um cartão modelo, incluindo informações sobre as perguntas abordadas.

### Visão geral do modelo {#model-overview}

+++Exibir perguntas e exemplos de respostas

| Pergunta | Informações necessárias | Exemplo de resposta |
| --- | --- | --- |
| Qual é o nome do modelo? | O nome oficial e a versão do modelo de IA | **Modelo de Pontuação de Propensão do CustomerAI v2.0** <br>O CustomerAI é um modelo alimentado por IA projetado para gerar pontuações de propensão para usuários com base em seus comportamentos e interações anteriores com uma empresa. Ele ajuda a prever a probabilidade de um cliente realizar ações específicas, como fazer uma compra, participar de conteúdo ou churning. Esse modelo é implantado no Adobe Experience Platform e integra-se a vários fluxos de trabalho de marketing e análise de clientes.</br> |
| Qual é a finalidade do modelo? | Uma breve descrição do que o modelo foi projetado para fazer. | O modelo foi projetado para fornecer insights acionáveis aos profissionais de marketing e equipes de engajamento do cliente, prevendo a probabilidade de um cliente executar determinada ação, como fazer uma compra, se inscrever em uma assinatura ou se envolver em uma campanha de email. As saídas permitem que as empresas otimizem a segmentação de público e personalizem as interações do cliente com base nos comportamentos previstos. |
| Que tipo de modelo é este? | O tipo do modelo, como classificação, regressão, generativo etc. | Este é um s **modelo de classificação de aprendizado supervisionado** que prevê a probabilidade de um evento ocorrer (por exemplo, compra, churn, envolvimento) de acordo com os dados históricos do cliente. Ele é treinado usando árvores de decisão de aumento de gradiente (GBDT) com regressão logística para pontuações de propensão do modelo. |
| Quem são os usuários pretendidos? | Os grupos de usuários internos e externos aos quais o modelo se destina. | Os principais usuários desse modelo são profissionais de marketing, analistas de dados e equipes de envolvimento do cliente que usam o Adobe Experience Platform para impulsionar estratégias de marketing orientadas por dados. |
| Como esse modelo se integra ao Adobe Experience Platform? | Os detalhes da integração e as APIs usadas, bem como a forma como elas se encaixam nos workflows. | A IA do cliente integra-se diretamente aos **serviços de IA da Adobe Experience Platform**, permitindo que os usuários acessem saídas do modelo por meio de APIs e painéis pré-criados. As pontuações de propensão geradas pelo modelo podem ser usadas no **Adobe Journey Optimizer**, **e Adobe Real-Time CDP** para refinar a segmentação de público e adaptar as estratégias de marketing. |

{style="table-layout:auto"}

+++

### Uso previsto {#intended-use}

+++Exibir perguntas e exemplos de respostas

| Pergunta | Informações necessárias | Exemplo de resposta |
| --- | --- | --- |
| Quais são os principais casos de uso? | Os cenários em que se espera que o modelo seja usado. | Este modelo é usado principalmente para **segmentação de clientes, marketing direcionado e previsão de churn**. As empresas usam esse modelo para **prever a intenção de compra do cliente, otimizar campanhas de marketing e aprimorar os esforços de personalização**. Por exemplo, uma empresa de comércio eletrônico pode usar o modelo para identificar compradores de alta intenção e oferecer promoções exclusivas. |
| Que problemas esse modelo resolve? | Os principais pontos problemáticos abordados pelo modelo. | Os profissionais de marketing geralmente têm dificuldades em **identificar os clientes certos a serem direcionados** e **otimizar os esforços de engajamento**. Este modelo **reduz a adivinhação** ao fornecer uma **abordagem orientada por dados** para o direcionamento de clientes, garantindo que os recursos de marketing sejam alocados com eficiência. |
| Para quais setores ou domínios esse modelo é relevante? | Uma lista de setores aplicáveis. | O modelo é aplicável em vários setores, incluindo **comércio eletrônico, varejo, serviços financeiros, telecomunicações e mídia**. Qualquer empresa que dependa do engajamento do cliente e do marketing personalizado pode se beneficiar desse modelo. |
| Como esse modelo não deve ser usado? | Quaisquer casos de uso incorreto que devem ser evitados. | O modelo **não deve ser usado para tomada de decisão de alto risco**, como **pontuação de crédito financeiro, diagnóstico médico ou avaliações legais**. Além disso, não é destinado ao uso na **previsão de comportamentos pessoalmente sensíveis** (como condições de saúde, preferências políticas) devido a possíveis preocupações éticas. |

{style="table-layout:auto"}

+++

### Entradas e saídas do modelo {#model-inputs-and-outputs}

+++Exibir perguntas e exemplos de respostas

| Pergunta | Informações necessárias | Exemplo de resposta |
| --- | --- | --- |
| Que tipos de dados o modelo usa como entrada? | Os tipos de dados que o modelo usa como entrada, isso inclui: recursos de dados, formatos e fontes. | O modelo processa **dados comportamentais do cliente, atributos demográficos e interações históricas**. Isso inclui dados como frequência de visita ao site, histórico de compras anteriores, envolvimento com emails de marketing e informações demográficas. |
| Em que formato as entradas devem estar? | Os formatos de entrada aceitos. | Os dados de entrada devem ser estruturados como **objetos JSON** contendo atributos do cliente e sinais comportamentais. Para processamento em lote, o modelo aceita **arquivos CSV** formatados de acordo com os padrões de assimilação de dados da Adobe Experience Platform. |
| Qual é a saída do modelo? | O tipo de saída gerado pelo modelo. | O modelo gera uma pontuação de propensão entre 0 e 1, em que valores mais altos indicam uma probabilidade mais alta de ocorrência do evento previsto. Além disso, fornece pontuações de importância de recursos, permitindo que os usuários entendam quais fatores influenciaram a previsão. |
| Quais são algumas entradas e saídas de exemplo? | Um exemplo de entrada e saída correspondente. | <ul><li>**Exemplo de entrada:** json { &quot;customer_id&quot;: 12345, &quot;past_purchases&quot;: 3, &quot;last_visit_days&quot;: 7, &quot;email_click_rate&quot;: 0.4 }</li><li>**Exemplo de saída:** json { &quot;customer_id&quot;: 12345, &quot;propensity_score&quot;: 0.82 }</li></ul> |

{style="table-layout:auto"}

+++

### Dados de treinamento {#training-data}

+++Exibir perguntas e exemplos de respostas

| Pergunta | Informações necessárias | Exemplo de resposta |
| --- | --- | --- |
| Quais conjuntos de dados foram usados para treinar o modelo? | Uma descrição das fontes de dados. | O modelo foi treinado com dados de interação com o cliente primários e anônimos coletados pelo Adobe Experience Platform. Ele inclui dados comportamentais históricos do cliente, registros de transações, interações de email e métricas de engajamento em vários setores. |
| Qual é o tamanho e a fonte dos dados? | Volume e origem do conjunto de dados de treinamento. | O conjunto de dados de treinamento consiste em 10 milhões de registros de clientes provenientes de um conjunto diverso de clientes da Adobe Experience Platform. Esses registros incluem interações históricas com clientes, dados transacionais, registros de envolvimento comportamental e informações demográficas de vários setores, como varejo, comércio eletrônico, telecomunicações e finanças. Os dados foram coletados por um período de 24 meses, garantindo uma representação suficiente das tendências sazonais e dos padrões de engajamento de longo prazo. |
| Há alguma distorção conhecida no conjunto de dados? | Considerações sobre polarização e esforços de mitigação. | O conjunto de dados é predominantemente proveniente de usuários altamente engajados, o que pode introduzir viés de seleção. Para atenuar isso, o modelo aplica amostragem estratificada, técnicas de auditoria de polarização e estratégias de aumento de dados. |
| Como os dados são pré-processados? | Etapas executadas para limpar e preparar os dados. | O conjunto de dados passa por um extenso pré-processamento para garantir a consistência, a qualidade e a usabilidade dos dados. <ol><li>**Tratamento de Valores Ausentes**: os valores ausentes são abordados usando uma combinação de imputação média (para campos numéricos), imputação de modo (para campos categóricos) e modelagem preditiva (para casos ausentes complexos).</li><li>**Codificação Categórica:** variáveis categóricas, como segmentos de clientes e categorias de compras, são convertidas em representações numéricas por meio de codificação única e técnicas de codificação de destino.</li><li>**Escala e Normalização de Recursos:** A escala mín-máx é aplicada às variáveis associadas (por exemplo, idade, renda), enquanto a padronização de pontuação z é usada para recursos normalmente distribuídos.</li><li>**Pré-processamento Adicional:** O pipeline inclui detecção e remoção de exceção, filtragem de duplicatas, padronização de carimbo de data/hora e engenharia de recursos para melhorar a preditiva.</li></ol> |

{style="table-layout:auto"}

+++

### Arquitetura de modelos e treinamento {#model-architecture-and-training}

+++Exibir perguntas e exemplos de respostas

| Pergunta | Informações necessárias | Exemplo de resposta |
| --- | --- | --- |
| Qual arquitetura é usada pelo modelo? | O tipo de rede neural, método de conjunto etc. | O modelo usa o Gradient Boosting Decision Trees (GBDT) usando o XGBoost, otimizado para dados estruturados. Ele é treinado em sequências históricas de eventos do cliente para identificar padrões comportamentais preditivos. |
| Quais algoritmos foram aplicados? | As técnicas de aprendizado de máquina usadas. | O modelo é construído usando uma abordagem de aprendizado supervisionada, aproveitando o Gradient Boosting Decision Trees (GBDT) com o XGBoost como o algoritmo de aprendizado principal. Além disso, a regressão logística é incorporada como um modelo de linha de base para a avaliação de referência da precisão preditiva. |
| Quais estruturas de treinamento foram usadas? | As bibliotecas ou plataformas usadas para treinamento. | O modelo foi desenvolvido usando TensorFlow, XGBoost e scikit-learn. O treinamento é executado na infraestrutura em nuvem da IA da Adobe usando GPUs NVIDIA V100, que oferecem suporte a conjuntos de dados em grande escala. |
| Quais recursos de computação foram usados para treinamento? | Os recursos de hardware e nuvem usados para treinamento. | GPUs NVIDIA V100, treinadas em infraestrutura em nuvem Google. |
| Que métodos de avaliação foram utilizados? | As métricas e os procedimentos de teste usados para a avaliação. | AUC-ROC, recuperação de precisão e validação cruzada. |

{style="table-layout:auto"}

+++

### Desempenho e avaliação {#performance-and-evaluation}

+++Exibir perguntas e exemplos de respostas

| Pergunta | Informações necessárias | Exemplo de resposta |
| --- | --- | --- |
| Como o modelo foi testado? | Os métodos usados para validar o desempenho. | O modelo foi testado usando uma abordagem de validação de validação de validação, onde 80% dos dados foram usados para treinamento e 20% foram reservados para avaliação. |
| Quais métricas de avaliação foram usadas? | Os indicadores-chave de desempenho. | A eficácia do modelo é medida usando **AUC-ROC (0,85)**, **precision-recall (0,78)** e **F1-score (0,80)**. Essas métricas ajudam a avaliar a capacidade preditiva do modelo em diferentes segmentos. |
| Como o desempenho varia entre diferentes cenários? | As variações de desempenho específicas do contexto. | Menor precisão para novos segmentos de clientes com dados históricos limitados. |
| Existem deficiências conhecidas ou casos de falha? | Quaisquer limitações ou pontos de falha. | O modelo pode ter um desempenho inferior para clientes com dados históricos limitados (problema de inicialização a frio). Além disso, os efeitos da sazonalidade, como as tendências de compras de feriados, podem exigir retreinamento frequente para manter a precisão. |

{style="table-layout:auto"}

+++

### Equidade e viés {#fairness-and-bias}

+++Exibir perguntas e exemplos de respostas

| Pergunta | Informações necessárias | Exemplo de resposta |
| --- | --- | --- |
| Que verificações de equidade foram realizadas? | Os processos de análise e mitigação de polarização executados. | O modelo foi submetido a testes de paridade demográfica e avaliações de equidade adversária para detectar disparidades de desempenho entre diferentes segmentos de usuários. |
| O modelo afeta certos grupos de forma desproporcional? | Quaisquer disparidades no desempenho identificadas. | A análise revelou uma queda de desempenho de 5% para usuários com dados históricos de interação baixos. Para resolver isso, o modelo incorpora técnicas de reponderação durante o treinamento. |
| Como o modelo atenua os benefícios? | As técnicas usadas para lidar com o viés. | O conjunto de dados é estratificado para garantir a representação proporcional de diferentes dados demográficos do cliente, e restrições de equidade são introduzidas durante o treinamento para evitar que o modelo favoreça qualquer grupo específico. Auditorias de viés regulares são realizadas usando análise de paridade demográfica, permitindo ajustes se forem detectadas disparidades de desempenho. |

{style="table-layout:auto"}

+++

### Explicabilidade e interpretabilidade {#explainability-and-interpretability}

+++Exibir perguntas e exemplos de respostas

| Pergunta | Informações necessárias | Exemplo de resposta |
| --- | --- | --- |
| Os usuários podem entender por que o modelo toma determinadas decisões? | Os métodos de interpretação usados pelo modelo. | O modelo usa as **SHapley Additive Explanations (SHAP)** para quantificar o impacto de cada recurso de entrada em suas previsões, fornecendo transparência em como os atributos do cliente influenciam as pontuações de propensão. Os valores SHAP permitem a interpretação global, identificando os fatores mais influentes em todas as previsões, e a interpretação local, explicando previsões individuais para clientes específicos. |
| Quais ferramentas ou técnicas estão disponíveis para interpretação? | As ferramentas de explicabilidade disponíveis. | O modelo oferece suporte a **LIME (Model-Agnostic Explanations)** interpretáveis localmente e SHAP para fornecer insights sobre como os recursos de entrada influenciam as previsões. LIME gera explicações locais criando versões perturbadas dos dados de entrada e observando mudanças nas previsões, enquanto SHAP atribui valores de contribuição para cada recurso, oferecendo tanto a interpretabilidade global quanto local das decisões do modelo. |

{style="table-layout:auto"}

+++

### Robustez e generalização {#robustness-and-generalization}

+++Exibir perguntas e exemplos de respostas

| Pergunta | Informações necessárias | Exemplo de resposta |
| --- | --- | --- |
| Qual é o desempenho do modelo em dados invisíveis? | As descobertas sobre testes de desempenho de generalização. | O modelo mantém **80% de AUC-ROC** quando testado em conjuntos de dados inéditos, demonstrando forte generalização para novos registros de clientes. O desempenho permanece estável em diferentes segmentos de clientes, mas mostra uma pequena degradação quando o comportamento do usuário se desvia significativamente dos padrões históricos. |
| O modelo foi submetido a testes de esforço para entradas contraditórias? | Os detalhes da avaliação de robustez. | O modelo tem sido avaliado contra entradas perturbadas e adversárias, incluindo dados ausentes, injeção de valores anômalos e erro intencional de rotulagem. Embora o desempenho permaneça robusto em condições normais, uma pequena degradação da precisão (aproximadamente 3-5%) foi observada sob modificações adversárias extremas. |

{style="table-layout:auto"}

+++

### Considerações de segurança e privacidade {#security-and-privacy-considerations}

+++Exibir perguntas e exemplos de respostas

| Pergunta | Informações necessárias | Exemplo de resposta |
| --- | --- | --- |
| O modelo lida com dados confidenciais? | Qualquer conformidade das informações com as leis de privacidade. | O modelo não processa nem retém informações de identificação pessoal (PII) e todos os dados usados para treinamento são anonimizados e agregados. Ela segue rigorosa conformidade com as políticas internas de privacidade do GDPR, CCPA e Adobe para garantir o uso responsável dos dados. |
| Quais técnicas de preservação da privacidade foram usadas? | As técnicas usadas para garantir medidas de privacidade. | O modelo incorpora técnicas de privacidade diferencial para adicionar ruído controlado aos dados, impedindo a reidentificação de indivíduos. Além disso, métodos de hash, anonimização e tokenização são usados para remover PII antes do treinamento e da inferência do modelo. |

{style="table-layout:auto"}

+++

### Monitoramento e manutenção {#monitoring-and-maintenance}

+++Exibir perguntas e exemplos de respostas

| Pergunta | Informações necessárias | Exemplo de resposta |
| --- | --- | --- |
| Como o desempenho do modelo é monitorado ao longo do tempo? | Detalhes sobre os mecanismos de rastreamento usados para o modelo. | O modelo é continuamente monitorado por meio do WatsonX, rastreando indicadores-chave de desempenho, como desvio de precisão, deslocamentos de importância de recursos e estabilidade de previsão. Os mecanismos de detecção e alerta de anomalias notificam a equipe quando ocorrem desvios significativos do comportamento esperado. |
| Com que frequência o modelo é retreinado? | A frequência das atualizações no modelo. | O modelo é retreinado mensalmente usando dados atualizados de interação com o cliente para garantir relevância contínua. O novo treinamento periódico ajuda a reduzir a deriva de dados e as flutuações sazonais que podem afetar a precisão preditiva. |

{style="table-layout:auto"}

+++

### Considerações éticas e IA responsável {#ethical-considerations-and-responsible-ai}

+++Exibir perguntas e exemplos de respostas

| Pergunta | Informações necessárias | Exemplo de resposta |
| --- | --- | --- |
| Que preocupações éticas estão associadas a esse modelo? | Os riscos potenciais identificados. | O modelo poderia potencialmente introduzir distorções na tomada de decisões se não fosse monitorizado corretamente. Por exemplo, se certos dados demográficos estiverem superrepresentados nos dados de treinamento, o modelo pode favorecer injustamente grupos específicos de clientes. |
| Como o modelo se alinha aos princípios da IA responsável? | Informações sobre como o modelo está em conformidade com as diretrizes éticas de IA. | A Adobe Experience Platform segue as diretrizes da IA responsável, garantindo que os modelos sejam submetidos a auditorias de viés, testes de equidade e supervisão humana antes da implantação. |

{style="table-layout:auto"}

+++

### Limitações conhecidas {#known-limitations}

+++Exibir perguntas e exemplos de respostas

| Pergunta | Informações necessárias | Exemplo de resposta |
| --- | --- | --- |
| Quais são as limitações conhecidas do modelo? | Quaisquer restrições de desempenho ou caso de uso identificadas. | O modelo pode ter dificuldades para prever com precisão os resultados de produtos recém-lançados ou segmentos de clientes nos quais os dados históricos insuficientes estão disponíveis. Além disso, variações sazonais no comportamento do cliente podem causar flutuações na precisão preditiva se não forem consideradas durante o novo treinamento. |
| Sob quais condições o modelo funciona mal? | Quaisquer deficiências identificadas no que respeita ao modelo. | O desempenho diminui quando o histórico do cliente é escasso, como para compradores pela primeira vez ou usuários com dados mínimos de engajamento. Além disso, se os comportamentos do cliente mudarem devido a fatores externos, como recessões econômicas ou tendências do setor, o modelo pode exigir adaptação rápida para manter a precisão. |

{style="table-layout:auto"}

+++

### Melhorias futuras {#future-improvements}

+++Exibir perguntas e exemplos de respostas

| Pergunta | Informações necessárias | Exemplo de resposta |
| --- | --- | --- |
| Quais melhorias estão planejadas para iterações futuras? | O roteiro para melhorias. | As iterações futuras incluirão técnicas de aprendizado de transferência para melhorar o desempenho para usuários de partida a frio e aprimorar a adaptabilidade a mudanças de comportamento do cliente. Além disso, a integração de dados em tempo real será introduzida para melhorar a capacidade de resposta e a precisão do modelo em ambientes de marketing dinâmicos. |

{style="table-layout:auto"}

+++