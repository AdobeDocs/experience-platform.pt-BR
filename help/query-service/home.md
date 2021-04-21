---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, serviço de consulta, query
solution: Experience Platform
title: Visão geral do serviço de query
topic-legacy: overview
description: Este documento fornece uma visão geral da função do Serviço de query no Experience Platform.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# [!DNL Query Service]visão geral

O Adobe Experience Platform assimila dados de uma grande variedade de fontes. Um grande desafio para os profissionais de marketing é fazer sentido com esses dados para obter insights sobre seus clientes. O Adobe Experience Platform [!DNL Query Service] facilita isso permitindo que você use o SQL padrão para consultar dados em [!DNL Platform]. Usando [!DNL Query Service], você pode ingressar em qualquer conjunto de dados no [!DNL Data Lake] e capturar os resultados da consulta como um novo conjunto de dados para uso em relatórios, aprendizado de máquina ou para assimilação em [!DNL Real-time Customer Profile]. Este documento fornece uma visão geral da função de [!DNL Query Service] em [!DNL Experience Platform].

[!DNL Query Service] possibilita que as marcas se conectem à jornada do cliente online para offline e entendam a atribuição omnicanal. O vídeo a seguir mostra como uma empresa de experiência pode aproveitar [!DNL Query Service] para lidar com casos de uso principais e como [!DNL Query Service] funciona.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Usando [!DNL Query Service]

[!DNL Query Service] O fornece uma interface de usuário e uma RESTful API a partir da qual você pode criar consultas SQL para analisar melhor seus dados. Com a interface do usuário, você pode gravar e executar consultas, exibir consultas executadas anteriormente e acessar consultas salvas por usuários em sua Organização IMS. A interface do usuário do deve ser usada como sandbox para testar seus queries antes de executá-los em seu conjunto de dados mais amplo. Mais informações sobre o uso do serviço interativo em [!DNL Platform] podem ser encontradas no [Guia da interface do usuário do Serviço de query](ui/overview.md). A RESTful API fornece uma experiência semelhante, permitindo que você grave e execute consultas programaticamente, agende consultas para uso e repetição futuros, bem como crie modelos para consultas que deseja gravar. Mais informações sobre como usar a API [!DNL Query Service] podem ser encontradas no [Guia do desenvolvedor do Serviço de query](api/getting-started.md).

## [!DNL Query Service] e  [!DNL Experience Platform] serviços

[!DNL Query Service] interage e pode ser usado junto com vários  [!DNL Experience Platform] serviços. Para aproveitar ao máximo os recursos [!DNL Query Service's], é recomendável que você se familiarize com esses serviços e como eles interagem com [!DNL Query Service].

### [!DNL Data Science Workspace]

O Adobe Experience Platform [!DNL Data Science Workspace] usa o aprendizado de máquina e a inteligência artificial para obter insights dos dados armazenados em [!DNL Experience Platform]. [!DNL Data Science Workspace] O permite que os cientistas de dados criem receitas com base em dados de registro e de séries de tempo sobre os clientes e suas atividades, facilitando previsões como comprar propensão e ofertas recomendadas que o indivíduo provavelmente apreciará e usará. Você pode usar o SQL em [!DNL Data Science Workspace] integrando [!DNL Query Service] em [!DNL JupyterLab], permitindo explorar, transformar e analisar dados do Adobe Analytics. Leia a [!DNL Data Science Workspace] visão geral para obter mais informações sobre [!DNL Data Science Workspace] e o [!DNL Query Service] guia de integração para obter mais informações sobre como [!DNL Data Science Workspace] interage com [!DNL Query Service].

### [!DNL Segmentation Service]

O Adobe Experience Platform [!DNL Segmentation Service] permite que os usuários dividam seus clientes em grupos menores que compartilham características semelhantes. Esses segmentos podem ser avaliados posteriormente para fornecer uma melhor análise dos dados [!DNL Real-time Customer Profile]. [!DNL Query Service] O pode ser usado para fornecer essa análise executando consultas sobre esses dados de segmento no  [!DNL Data Lake]. Leia a [!DNL Segmentation Service] visão geral para obter mais informações sobre a segmentação e o guia [!DNL Profile Query Language] (PQL) para obter mais informações sobre como analisar segmentos.

### Caso de uso do Looker BI

Com o Adobe Experience Platform, você pode assimilar, armazenar, estruturar e extrair todos os conjuntos de dados armazenados, incluindo dados comportamentais, CRM e de ponto de venda. Usando [!DNL Experience Platform's Query Service], você pode consultar esses conjuntos de dados e responder perguntas específicas sobre os negócios e começar a gerar insights impactantes. O vídeo a seguir demonstra o valor da criação de painéis nas ferramentas de inteligência empresarial (BI) usando [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Próximas etapas e recursos adicionais

Ao ler este documento, você foi introduzido em [!DNL Query Service] e como ele funciona dentro do maior escopo de [!DNL Experience Platform]. Para obter mais informações sobre como interagir com vários endpoints na API [!DNL Query Service], leia o [Guia do desenvolvedor do Serviço de query](api/getting-started.md). Para obter mais informações sobre como usar o serviço interativo em [!DNL Platform], leia o [Guia da interface do usuário do Serviço de query](ui/overview.md). Para obter uma lista abrangente sobre como conectar clientes externos com [!DNL Query Service], leia a [Visão geral dos clientes do Serviço de query](clients/overview.md).

Para se preparar melhor para executar consultas, assista ao vídeo a seguir. Este vídeo compartilha dicas e práticas recomendadas para executar consultas na interface do Editor de consultas, clientes PSQL, soluções de business intelligence (BI) e a API HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
