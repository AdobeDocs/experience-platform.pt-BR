---
keywords: Experience Platform;página inicial;tópicos populares;serviço de consulta;serviço de consulta;consulta;;home;popular topics;query service;Query service;query
solution: Experience Platform
title: Visão geral do serviço de consulta
description: Este documento fornece uma visão geral da função do Serviço de consulta no Experience Platform.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 1%

---

# Visão geral do [!DNL Query Service]

O Adobe Experience Platform assimila dados de várias fontes. Um grande desafio para os profissionais de marketing é utilizar esses dados para obter insights sobre seus clientes. Adobe Experience Platform [!DNL Query Service] facilita isso permitindo que você use o SQL padrão para consultar dados no [!DNL Platform]. Usar [!DNL Query Service], você pode associar qualquer conjunto de dados na [!DNL Data Lake] e capture os resultados da consulta como um novo conjunto de dados para usar em relatórios, aprendizado de máquina ou para assimilação em [!DNL Real-Time Customer Profile]. Este documento fornece uma visão geral da função do [!DNL Query Service] no prazo de [!DNL Experience Platform].

[!DNL Query Service] O permite que as marcas conectem a jornada de cliente online a offline e entendam a atribuição omnicanal. O vídeo a seguir mostra como uma empresa baseada em experiências pode aproveitar [!DNL Query Service] para lidar com os principais casos de uso e como [!DNL Query Service] funciona.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Usar [!DNL Query Service]

[!DNL Query Service] O fornece uma interface de usuário e uma API RESTful a partir da qual você pode criar consultas SQL para analisar melhor seus dados. Com a interface do usuário do, é possível gravar e executar consultas, exibir consultas executadas anteriormente e acessar consultas salvas por usuários em sua Organização IMS. A interface do usuário deve ser usada como uma sandbox para testar suas consultas antes de executá-las em seu conjunto de dados mais amplo. Mais informações sobre o uso do serviço interativo no [!DNL Platform] pode ser encontrado no [Guia da interface do usuário do Serviço de consulta](ui/overview.md). A API RESTful fornece uma experiência semelhante, permitindo que você escreva e execute programaticamente consultas, agende consultas para uso futuro e repetição, bem como crie modelos para consultas que você deseja gravar. Mais informações sobre como usar o [!DNL Query Service] A API pode ser encontrada no [Guia do desenvolvedor do Serviço de consulta](api/getting-started.md).

## Serviços do [!DNL Query Service] e da [!DNL Experience Platform]

[!DNL Query Service] O interage e pode ser usado em conjunto com vários [!DNL Experience Platform] serviços. Para aproveitar ao máximo o [!DNL Query Service's] recomendamos que você se familiarize com esses serviços e como eles interagem com [!DNL Query Service].

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] O usa aprendizagem de máquina e inteligência artificial para obter insights de dados armazenados no [!DNL Experience Platform]. [!DNL Data Science Workspace] O permite que os cientistas de dados criem receitas com base em dados registrados e de séries temporais sobre os clientes e suas atividades, facilitando previsões, como propensão de compra e ofertas recomendadas que o indivíduo provavelmente apreciará e usará. Você pode usar SQL dentro de [!DNL Data Science Workspace] ao integrar [!DNL Query Service] em [!DNL JupyterLab], permitindo explorar, transformar e analisar dados do Adobe Analytics. Leia as [!DNL Data Science Workspace] visão geral para obter mais informações sobre [!DNL Data Science Workspace], e o [!DNL Query Service] para obter mais informações sobre como [!DNL Data Science Workspace] interage com [!DNL Query Service].

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] O permite que os usuários dividam seus clientes em grupos menores que compartilham características semelhantes. Esses segmentos podem ser avaliados posteriormente para fornecer uma melhor análise sobre [!DNL Real-Time Customer Profile] dados. [!DNL Query Service] pode ser usado para fornecer essa análise executando consultas nesses dados de segmento na [!DNL Data Lake]. Leia as [!DNL Segmentation Service] visão geral para obter mais informações sobre segmentação e a [!DNL Profile Query Language] (PQL) para obter mais informações sobre como analisar segmentos.

## Casos de uso

[!DNL Query Service] O oferece uma abordagem flexível para o processamento de dados, com muitas finalidades. Entre outros, pode aliviar o fardo da segmentação dos profissionais de marketing e ajudar a gerar públicos acionáveis e insights comerciais significativos. Os seguintes casos de uso oferecem exemplos mais aprofundados do poder da [!DNL Query Service].

### Abandono de navegação do Adobe Analytics

Este [o exemplo de abandono de navegação se concentra no uso do Adobe [!DNL Analytics]](./use-cases/abandoned-browse.md) para criar um público-alvo acionável específico. [!DNL Query Service] O acomoda uma lógica complexa para segmentação, a fim de calcular vários atributos personalizados para uso downstream ou para simplificar muito a criação de segmentos.

### Painéis do Looker BI

Com o Adobe Experience Platform, você pode assimilar, armazenar, estruturar e obter todos os conjuntos de dados armazenados, incluindo dados comportamentais, de CRM e de ponto de venda. Usar [!DNL Experience Platform's Query Service], você pode consultar esses conjuntos de dados, responder perguntas específicas sobre os negócios e começar a gerar insights de impacto. O vídeo a seguir demonstra o valor da criação de painéis em ferramentas de BI (Business Intelligence) usando o [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Próximas etapas e recursos adicionais

Ao ler este documento, você foi apresentado a [!DNL Query Service] e como funciona dentro do âmbito mais amplo da [!DNL Experience Platform]. Para obter mais informações sobre como interagir com vários endpoints na [!DNL Query Service] API, leia as [Guia do desenvolvedor do Serviço de consulta](api/getting-started.md). Para obter mais informações sobre como usar o serviço interativo no [!DNL Platform], leia o [Guia da interface do usuário do Serviço de consulta](ui/overview.md). Para obter uma lista abrangente sobre como conectar clientes externos com o [!DNL Query Service], leia o [Visão geral dos clientes do Serviço de consulta](clients/overview.md).

Para preparar-se melhor para executar consultas, assista ao vídeo a seguir. Este vídeo compartilha dicas e práticas recomendadas para executar consultas na interface do editor de consultas, clientes PSQL, soluções de business intelligence (BI) e a API HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
