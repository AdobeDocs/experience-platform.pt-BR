---
title: Notas de versão da Adobe Experience Platform de junho de 2022
description: As notas de versão de junho de 2022 para o Adobe Experience Platform.
source-git-commit: 98b9e79fadecc6e0d5ee8e86b785fd905643f725
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 6%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 22 de junho de 2022**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [Serviço de query](#query-service)
- [Fontes](#sources)

## [!DNL Data Science Workspace] {#dsw}

O Data Science Workspace usa aprendizagem de máquina e inteligência artificial para liberar insights de seus dados. Integrado ao Adobe Experience Platform, o Data Science Workspace ajuda você a fazer previsões usando seus ativos de conteúdo e dados nas soluções de Adobe. Uma das maneiras como o Data Science Workspace consegue isso é usando o JupyterLab. O JupyterLab é uma interface de usuário baseada na Web para <a href="https://jupyter.org/" target="_blank">Jupyter do projeto</a> e é totalmente integrado ao Adobe Experience Platform. Ele fornece um ambiente de desenvolvimento interativo para os cientistas de dados trabalharem com notebooks, códigos e dados do Júpiter.

| Recurso | Descrição |
| --- | --- |
| Iniciador do JupyterLab | O JupyterLab Launcher agora inclui iniciadores para notebooks Spark 3.2. As inicializações do notebook Spark 2.4 agora são substituídas pelos notebooks Spark 3.2 e farão parte desta versão. |
| Spark 3.2 | As novas receitas do Scala (Spark) e do PySpark agora usam o Spark 3.2 |
| Kernels | Os notebooks Scala (Spark) agora são criados por meio do kernel Scala. Os notebooks PySpark agora são criados por meio do kernel Python. Os kernel Spark e PySpark estão obsoletos e configurados para serem removidos em uma versão subsequente. |
| Receitas | As novas receitas PySpark e Spark agora seguem o fluxo de trabalho Docker semelhante às receitas Python e R. |

{style=&quot;table-layout:auto&quot;}

Para obter informações mais gerais sobre o Data Science Workspace, consulte o [documentação de visão geral](../../data-science-workspace/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, anúncios direcionados e muitos outros casos de uso.

**Novos destinos**

| Destino | Descrição |
| ----------- | ----------- |
| [[!DNL Medallia]](/help/destinations/catalog/voice/medallia-connector.md) | Ative perfis para pesquisas direcionadas da Medallia e coleta de feedback para entender melhor as necessidades e expectativas do cliente. |

{style=&quot;table-layout:auto&quot;}

Para obter informações mais gerais sobre destinos, consulte [visão geral dos destinos](../../destinations/home.md).

## Serviço de query {#query-service}

O Serviço de Consulta permite que você use o SQL padrão para consultar dados no Adobe Experience Platform [!DNL Data Lake]. É possível unir qualquer conjunto de dados da [!DNL Data Lake] e capture os resultados do query como um novo conjunto de dados para usar nos relatórios, no Data Science Workspace ou para assimilação no Perfil do cliente em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Rotulação de esquema ad hoc | Gerencie o acesso a dados confidenciais aplicando rótulos a campos de dados de esquemas ad hoc que são automaticamente gerados por meio de consultas CTAS do Serviço de query. Você pode restringir o uso de determinados campos ou conjuntos de dados de esquemas ad hoc para controlar o acesso a dados pessoais confidenciais e a informações de identificação pessoal. Ao usar o recurso de controle de acesso baseado em atributos, você pode rotular campos de esquema ad hoc por meio da interface do usuário da plataforma. |
| `FLATTEN` definição | Ao se conectar a um banco de dados por meio de ferramentas de BI de terceiros, a variável `FLATTEN` a configuração nivela estruturas de dados aninhadas em colunas separadas, onde o nome do atributo se torna o nome da coluna que retém os valores da linha. Isso melhora a usabilidade de esquemas ad hoc e reduz a carga de trabalho necessária para recuperar, analisar, transformar e relatar dados em ferramentas de BI que não suportam estruturas de dados aninhadas. |

{style=&quot;table-layout:auto&quot;}

Para obter mais informações sobre Serviços de query, consulte [Visão geral do Serviço de query](../../query-service/home.md).

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

| Recurso | Descrição |
| --- | --- |
| Versão beta de [!DNL Mixpanel] source | Agora você pode usar o [!DNL Mixpanel] fonte para assimilar dados de análise da sua [!DNL Mixpanel] para o Experience Platform. Consulte a [[!DNL Mixpanel] documentação de origem](../../sources/connectors/analytics/mixpanel.md) para obter mais informações. |

{style=&quot;table-layout:auto&quot;}

Para saber mais sobre fontes, consulte o [visão geral das fontes](../../sources/home.md).
