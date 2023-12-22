---
keywords: Experience Platform;página inicial;tópicos populares;serviço de consulta;serviço de consulta;consulta;;home;popular topics;query service;Query service;query
solution: Experience Platform
title: Visão geral do serviço de consulta
description: Saiba mais sobre a função do Serviço de consulta no Experience Platform.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: e06519978ed9c6128be53a15cef3046a0dbc2a16
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 0%

---

# Visão geral do Serviço de consulta

O Adobe Experience Platform assimila dados de várias fontes. Um grande desafio para os profissionais de marketing é utilizar esses dados para obter insights sobre seus clientes. Para consultar dados na Platform, você pode usar o SQL padrão e o Serviço de consulta da Adobe Experience Platform. Você pode usar o Serviço de consulta para ingressar em qualquer conjunto de dados no data lake e capturar os resultados da consulta como um novo conjunto de dados para usar em relatórios, aprendizado de máquina ou para assimilação em [!DNL Real-Time Customer Profile]. Este documento fornece uma visão geral da função do Serviço de consulta no Experience Platform.

Você pode usar o Serviço de consulta para conectar a jornada de cliente online a offline e entender a atribuição omnicanal para sua marca. O vídeo a seguir mostra como uma empresa baseada em experiências pode usar o Serviço de consulta para tratar dos principais casos de uso e como esse Serviço funciona.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Uso do Serviço de consulta {#usage}

Para analisar seus dados, você pode usar a interface do usuário do Serviço de consulta e uma API RESTful, a partir da qual você pode criar consultas SQL. Com a interface do usuário do, você pode gravar e executar consultas, visualizar consultas executadas anteriormente e acessar consultas salvas por usuários em sua organização. Você pode usar o Editor de consultas como uma sandbox para testar suas consultas antes de executá-las em seu conjunto de dados mais amplo. Consulte a [Guia da interface do usuário do Serviço de consulta](ui/overview.md) para obter mais informações sobre o uso da interface do usuário. A API RESTful fornece uma experiência semelhante. Você pode usar a API do Serviço de consulta para gravar e executar consultas de forma programática, agendar consultas para uso e repetição futuros, bem como criar modelos para consultas que deseja gravar. Mais informações sobre como usar a API do Serviço de consulta podem ser encontradas no [Guia do desenvolvedor do Serviço de consulta](api/getting-started.md).

## Serviço de consulta e serviços Experience Platform {#experience-platform-services}

O Serviço de consulta interage e pode ser usado com vários serviços de Experience Platform. Para aproveitar ao máximo os recursos do Serviço de consulta, você deve se familiarizar com esses serviços e como eles interagem com o Serviço de consulta. A variável [Página de aterrissagem da documentação do Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=pt-BR) O fornece resumos e links para os recursos da plataforma.

### [!DNL Data Science Workspace] {#data-science-workspace}

Adobe Experience Platform [!DNL Data Science Workspace] O usa aprendizagem de máquina e inteligência artificial para obter insights dos dados armazenados no Experience Platform. Os cientistas de dados podem usar o [!DNL Data Science Workspace] para criar receitas com base em dados de registro e série temporal sobre clientes e suas atividades. Essas receitas facilitam previsões, como propensão de compra e ofertas recomendadas que o indivíduo provavelmente apreciará e usará. Você pode usar SQL dentro de [!DNL Data Science Workspace] por meio da integração do Serviço de consulta em [!DNL JupyterLab] para explorar, transformar e analisar dados do Adobe Analytics. Leia o [[!DNL Data Science Workspace] visão geral](../data-science-workspace/home.md) e a variável [Guia de conexão do Notebook Jypiter](./clients/jupyter-notebook.md) para obter mais informações sobre como [!DNL Data Science Workspace] O interage com o Serviço de consulta.

### [!DNL Segmentation Service] {#segmentation}

Use o Serviço de segmentação da Adobe Experience Platform para dividir seus clientes em grupos menores que compartilhem características semelhantes. Esses públicos-alvo podem ser avaliados para fornecer uma análise melhor dos dados do Perfil do cliente em tempo real. Você pode usar o Serviço de consulta para executar consultas nesses dados de público-alvo no data lake e fornecer a análise. Leia o [Visão geral do serviço de segmentação](../segmentation/home.md) e a variável [[!DNL Profile Query Language] Guia do (PQL)](../segmentation/pql/overview.md) para obter mais informações sobre como analisar públicos-alvo.

## Casos de uso {#use-cases}

O Serviço de consulta oferece uma abordagem flexível para o processamento de dados, que serve a várias finalidades. Entre outros, pode aliviar o fardo da segmentação dos profissionais de marketing e ajudar a gerar públicos acionáveis e insights comerciais significativos. Os seguintes casos de uso oferecem exemplos mais detalhados do poder do Serviço de consulta.

### Abandono de navegação do Adobe Analytics {#abandon-browse}

Este [o exemplo de abandono de navegação se concentra no uso do Adobe [!DNL Analytics]](./use-cases/abandoned-browse.md) para criar um público-alvo acionável específico. O Serviço de consulta acomoda uma lógica complexa para segmentação, a fim de calcular vários atributos personalizados para uso downstream ou para simplificar muito a criação de públicos-alvo.

## Gerar insights com painéis personalizados {#custom-dashboards}

Com o Adobe Experience Platform, você pode assimilar, armazenar, estruturar e obter todos os conjuntos de dados armazenados, incluindo dados comportamentais, de CRM e de ponto de venda. Usar [!DNL Experience Platform's Query Service], você pode consultar esses conjuntos de dados, responder perguntas específicas sobre os negócios e começar a gerar insights de impacto. Saiba como criar e gerenciar painéis personalizados onde você pode criar, adicionar e editar widgets personalizados para visualizar as métricas principais com o [painéis definidos pelo usuário](../dashboards/user-defined-dashboards.md). Você pode até [personalizar seus próprios relatórios do Real-Time CDP](../dashboards/cdp-insights-data-model.md) para seus casos de uso de marketing e KPI usando consultas SQL com os Modelos de dados do Real-time Customer Data Platform Insights.

## Próximas etapas e recursos adicionais

Ao ler este documento, você foi apresentado ao Serviço de consulta e como ele funciona dentro do escopo maior do Experience Platform. Para continuar aprendendo sobre os recursos do Serviço de consulta, é recomendável ler os seguintes documentos:

- A variável [Guia do desenvolvedor do Serviço de consulta](api/getting-started.md): para obter mais informações sobre como interagir com vários endpoints na API do Serviço de consulta.
- A variável [Guia da interface do usuário do Serviço de consulta](ui/overview.md): Para obter mais informações sobre o uso do Editor de consultas e da interface do usuário.
- A variável [Visão geral dos clientes do Serviço de consulta](clients/overview.md): para obter uma lista abrangente de clientes externos para se conectar ao Serviço de consulta.

Para preparar-se melhor para executar consultas, assista ao vídeo a seguir. Este vídeo compartilha dicas e práticas recomendadas para executar consultas na interface do editor de consultas, clientes PSQL, soluções de business intelligence (BI) e a API HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
