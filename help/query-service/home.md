---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Serviço de Query Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: cfd767a05ad4c1dd43ac2bdde1966f9c89f5d219
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---


# Visão geral do Serviço de Query

Adobe Experience Platform ingere dados de uma grande variedade de fontes. Um grande desafio para os profissionais de marketing é entender esses dados para obter insights sobre seus clientes. O Serviço de Query de Adobe Experience Platform facilita isso ao permitir o uso de SQL padrão para dados de query no Platform. Usando o Serviço de Query, você pode associar qualquer conjunto de dados no Data Lake e capturar os resultados do query como um novo conjunto de dados para uso em relatórios, aprendizado de máquina ou para ingestão no Perfil de cliente em tempo real. Este documento fornece uma visão geral da função do Serviço de Query dentro do Experience Platform.

O Serviço de Query possibilita que as marcas conectem a jornada on-line ao cliente e entendam a atribuição do canal onni. O vídeo a seguir mostra como uma empresa de experiência pode aproveitar o Serviço de Query para resolver os principais casos de uso e como o Serviço de Query funciona.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Uso do serviço de Query

O Query Service fornece uma interface de usuário e uma RESTful API a partir da qual você pode criar query SQL para analisar melhor seus dados. Com a interface do usuário, você pode gravar e executar query, visualização query executados anteriormente e acessar query salvos por usuários na organização IMS. A interface do usuário deve ser usada como uma caixa de proteção para testar seus query antes de executá-los no conjunto de dados mais amplo. Para obter mais informações sobre como usar o serviço interativo no Platform, consulte o guia [da interface do usuário do Serviço de](ui/overview.md)Query. A RESTful API fornece uma experiência semelhante, permitindo que você escreva e execute query programaticamente, programe query para uso e repetição futuros, bem como crie modelos para query que deseja gravar. Para obter mais informações sobre como usar a API de serviço de Query, consulte o guia [do desenvolvedor do serviço de](api/getting-started.md)Query.

## Serviços de Query e serviços de Experience Platform

O Serviço de Query interage e pode ser usado em conjunto com vários serviços de Experience Platform. Para aproveitar ao máximo os recursos do Serviço de Query, é recomendável que você se familiarize com esses serviços e como eles interagem com o Serviço de Query.

### Área de trabalho da ciência de dados

A Adobe Experience Platform Data Science Workspace usa o aprendizado de máquina e a inteligência artificial para obter insights dos dados armazenados no Experience Platform. A Data Science Workspace permite que os cientistas de dados construam receitas com base em dados de registro e séries de tempo sobre clientes e suas atividades, facilitando previsões como a propensão de compra e ofertas recomendadas que o indivíduo provavelmente apreciará e usará. Você pode usar o SQL na Data Science Workspace integrando o Serviço de Query ao JupyterLab, permitindo explorar, transformar e analisar dados da Adobe Analytics. Leia a visão geral da Data Science Workspace para obter mais informações sobre a Data Science Workspace e o guia de integração do Serviço de Query para obter mais informações sobre como a Data Science Workspace interage com o Serviço de Query.

### Serviço de segmentação

O Serviço de segmentação de Adobe Experience Platform permite que os usuários dividam seus clientes em grupos menores que compartilham características semelhantes. Esses segmentos podem ser avaliados posteriormente para fornecer melhor análise sobre os dados do Perfil do cliente em tempo real. O Serviço de Query pode ser usado para fornecer essa análise executando query nos dados desse segmento no Data Lake. Leia a visão geral do Serviço de segmentação para obter mais informações sobre segmentação e o guia Linguagem do Query do Perfil (PQL) para obter mais informações sobre como analisar segmentos.

### Caso de uso do Looker BI

Com o Adobe Experience Platform, você pode assimilar, armazenar, estruturar e extrair todos os conjuntos de dados armazenados. incluindo dados comportamentais, CRM e de ponto de venda. Usando [!DNL Experience Platform's Query Service], você pode query nesses conjuntos de dados e responder a perguntas específicas sobre os negócios e, em seguida, gerar start que geram insights impactantes. O vídeo a seguir demonstra o valor de criar painéis em ferramentas de inteligência empresarial (BI) usando [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Próximos passos e recursos adicionais

Ao ler este documento, você foi apresentado ao Query Service e como ele funciona dentro do maior escopo do Experience Platform. Para obter mais informações sobre como interagir com vários pontos de extremidade na API de serviço do Query, leia o guia [do desenvolvedor do serviço do](api/getting-started.md)Query. Para obter mais informações sobre como usar o serviço interativo no Platform, leia o guia [da interface do usuário do Serviço de](ui/overview.md)Query. Para obter uma lista abrangente sobre como conectar clientes externos ao Query Service, leia a visão geral [](clients/overview.md)dos clientes do Query Service.

Para se preparar melhor para executar query, assista ao vídeo a seguir. Este vídeo compartilha dicas e práticas recomendadas para executar query na interface do editor de query, clientes PSQL, soluções de business intelligence (BI) e API HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
