---
keywords: Experience Platform;home;popular topics;query service;Query service;query
solution: Experience Platform
title: Serviço de Query Adobe Experience Platform
topic: overview
description: Este documento fornece uma visão geral da função do Serviço de Query dentro do Experience Platform.
translation-type: tm+mt
source-git-commit: 23516c66a67ae5663dcf90a40ccba98bfd266ab0
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 0%

---


# [!DNL Query Service]visão geral

A Adobe Experience Platform ingere dados de uma grande variedade de fontes. Um grande desafio para os profissionais de marketing é entender esses dados para obter insights sobre seus clientes. A Adobe Experience Platform [!DNL Query Service] facilita isso ao permitir que você use SQL padrão para query de dados em [!DNL Platform]. Usando [!DNL Query Service], você pode ingressar em qualquer conjunto de dados no [!DNL Data Lake] e capturar os resultados do query como um novo conjunto de dados para uso em relatórios, aprendizado de máquina ou para ingestão no [!DNL Real-time Customer Profile]. Este documento fornece uma visão geral da função do [!DNL Query Service] dentro do [!DNL Experience Platform].

[!DNL Query Service] possibilita que as marcas conectem a jornada on-line ao cliente offline e entendam a atribuição de canal onni. O vídeo a seguir mostra como uma empresa de experiência pode aproveitar [!DNL Query Service] para resolver os principais casos de uso e como [!DNL Query Service] funciona.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Using [!DNL Query Service]

[!DNL Query Service] fornece uma interface de usuário e uma RESTful API a partir da qual você pode criar query SQL para analisar melhor seus dados. Com a interface do usuário, você pode gravar e executar query, visualização query executados anteriormente e acessar query salvos por usuários na organização IMS. A interface do usuário deve ser usada como uma caixa de proteção para testar seus query antes de executá-los no conjunto de dados mais amplo. Para obter mais informações sobre como usar o serviço interativo em [!DNL Platform] Query, consulte o guia [da interface do usuário do Serviço de](ui/overview.md). A RESTful API fornece uma experiência semelhante, permitindo que você escreva e execute query programaticamente, programe query para uso e repetição futuros, bem como crie modelos para query que deseja gravar. Para obter mais informações sobre como usar a [!DNL Query Service] API, consulte o guia [do desenvolvedor do Serviço de](api/getting-started.md)Query.

## [!DNL Query Service] e [!DNL Experience Platform] serviços

[!DNL Query Service] interage e pode ser usado em conjunto com vários [!DNL Experience Platform] serviços. Para aproveitar ao máximo [!DNL Query Service's] os recursos, é recomendável que você se familiarize com esses serviços e com como eles interagem [!DNL Query Service].

### [!DNL Data Science Workspace]

A Adobe Experience Platform [!DNL Data Science Workspace] usa o aprendizado de máquina e a inteligência artificial para obter insights dos dados armazenados no [!DNL Experience Platform]. [!DNL Data Science Workspace] permite que os cientistas de dados construam receitas com base em dados de registros e séries de tempo sobre clientes e suas atividades, facilitando previsões como a propensão de compra e ofertas recomendadas que o indivíduo provavelmente apreciará e usará. Você pode usar o SQL dentro [!DNL Data Science Workspace] integrando- [!DNL Query Service] se a [!DNL JupyterLab]ele, permitindo explorar, transformar e analisar dados da Adobe Analytics. Leia a [!DNL Data Science Workspace] visão geral para obter mais informações sobre [!DNL Data Science Workspace]e o guia de [!DNL Query Service] integração para obter mais informações sobre como [!DNL Data Science Workspace] interagir com [!DNL Query Service].

### [!DNL Segmentation Service]

A Adobe Experience Platform [!DNL Segmentation Service] permite que os usuários dividam seus clientes em grupos menores que compartilham características semelhantes. Esses segmentos podem ser avaliados posteriormente para proporcionar melhor análise aos seus [!DNL Real-time Customer Profile] dados. [!DNL Query Service] pode ser usado para fornecer essa análise executando query nos dados desse segmento dentro do [!DNL Data Lake]. Leia a [!DNL Segmentation Service] visão geral para obter mais informações sobre a segmentação e o guia [!DNL Profile Query Language] (PQL) para obter mais informações sobre como analisar segmentos.

### Caso de uso do Looker BI

Com a Adobe Experience Platform, você pode assimilar, armazenar, estruturar e extrair todos os conjuntos de dados armazenados. incluindo dados comportamentais, CRM e de ponto de venda. Usando [!DNL Experience Platform's Query Service], você pode query nesses conjuntos de dados e responder a perguntas específicas sobre os negócios e, em seguida, gerar start que geram insights impactantes. O vídeo a seguir demonstra o valor de criar painéis em ferramentas de inteligência empresarial (BI) usando [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Próximos passos e recursos adicionais

Ao ler este documento, você foi apresentado a [!DNL Query Service] e como ele funciona dentro de um escopo maior de [!DNL Experience Platform]. Para obter mais informações sobre como interagir com vários pontos de extremidade dentro da [!DNL Query Service] API, leia o guia [do desenvolvedor do Serviço de](api/getting-started.md)Query. Para obter mais informações sobre como usar o serviço interativo em [!DNL Platform], leia o guia [da interface do usuário do Serviço de](ui/overview.md)Query. Para obter uma lista abrangente sobre como conectar clientes externos com [!DNL Query Service], leia a visão geral [](clients/overview.md)dos clientes do Query Service.

Para se preparar melhor para executar query, assista ao vídeo a seguir. Este vídeo compartilha dicas e práticas recomendadas para executar query na interface do editor de query, clientes PSQL, soluções de business intelligence (BI) e API HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
