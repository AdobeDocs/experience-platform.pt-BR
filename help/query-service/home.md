---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, serviço de consulta, query
solution: Experience Platform
title: Visão geral do serviço de consulta
topic-legacy: overview
description: Este documento fornece uma visão geral da função do Serviço de query no Experience Platform.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: 796460be52b465216cdc69d45aa38ac80aa3516d
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 0%

---

# [!DNL Query Service] visão geral

O Adobe Experience Platform assimila dados de uma grande variedade de fontes. Um grande desafio para os profissionais de marketing é fazer sentido com esses dados para obter insights sobre seus clientes. Adobe Experience Platform [!DNL Query Service] facilita isso ao permitir o uso do SQL padrão para consultar dados no [!DNL Platform]. Usando [!DNL Query Service], é possível ingressar em qualquer conjunto de dados no [!DNL Data Lake] e capturar os resultados da consulta como um novo conjunto de dados para uso em relatórios, aprendizado de máquina ou para assimilação em [!DNL Real-time Customer Profile]. Este documento fornece uma visão geral da função de [!DNL Query Service] within [!DNL Experience Platform].

[!DNL Query Service] possibilita que as marcas se conectem à jornada do cliente online para offline e entendam a atribuição omnicanal. O vídeo a seguir mostra como uma empresa de experiência pode aproveitar [!DNL Query Service] para solucionar os principais casos de uso e como [!DNL Query Service] funciona.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Usar [!DNL Query Service]

[!DNL Query Service] O fornece uma interface de usuário e uma RESTful API a partir da qual você pode criar consultas SQL para analisar melhor seus dados. Com a interface do usuário, você pode gravar e executar consultas, exibir consultas executadas anteriormente e acessar consultas salvas por usuários em sua Organização IMS. A interface do usuário do deve ser usada como sandbox para testar seus queries antes de executá-los em seu conjunto de dados mais amplo. Mais informações sobre o uso do serviço interativo em [!DNL Platform] podem ser encontradas no [Guia da interface do usuário do Serviço de query](ui/overview.md). A RESTful API fornece uma experiência semelhante, permitindo que você grave e execute consultas programaticamente, agende consultas para uso e repetição futuros, bem como crie modelos para consultas que deseja gravar. Mais informações sobre o uso da variável [!DNL Query Service] A API pode ser encontrada no [Guia do desenvolvedor do Serviço de query](api/getting-started.md).

## [!DNL Query Service] e [!DNL Experience Platform] serviços

[!DNL Query Service] interage e pode ser usado junto com vários [!DNL Experience Platform] serviços. Para aproveitar ao máximo os [!DNL Query Service's] , recomenda-se que você se familiarize com esses serviços e como eles interagem com [!DNL Query Service].

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] O usa o aprendizado de máquina e a inteligência artificial para obter insights dos dados armazenados no [!DNL Experience Platform]. [!DNL Data Science Workspace] O permite que os cientistas de dados criem receitas com base em dados de registro e de séries de tempo sobre os clientes e suas atividades, facilitando previsões como comprar propensão e ofertas recomendadas que o indivíduo provavelmente apreciará e usará. Você pode usar o SQL no [!DNL Data Science Workspace] integrando [!DNL Query Service] em [!DNL JupyterLab], permitindo explorar, transformar e analisar dados do Adobe Analytics. Leia o [!DNL Data Science Workspace] visão geral para obter mais informações sobre [!DNL Data Science Workspace]e o [!DNL Query Service] guia de integração para obter mais informações sobre como [!DNL Data Science Workspace] interage com [!DNL Query Service].

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] O permite que os usuários dividam seus clientes em grupos menores que compartilham características semelhantes. Esses segmentos podem ser avaliados posteriormente para fornecer uma melhor análise sobre seus [!DNL Real-time Customer Profile] dados. [!DNL Query Service] pode ser usada para fornecer essa análise executando consultas sobre esses dados de segmento no [!DNL Data Lake]. Leia o [!DNL Segmentation Service] visão geral para obter mais informações sobre a segmentação e o [!DNL Profile Query Language] Guia (PQL) para obter mais informações sobre como analisar segmentos.

## Casos de uso

[!DNL Query Service] O fornece uma abordagem flexível para o processamento de dados, que atende a vários propósitos. Entre outros, pode aliviar a carga da segmentação de profissionais de marketing e ajudar a gerar públicos acionáveis e insights de negócios significativos. Os casos de uso a seguir oferecem exemplos mais aprofundados do poder da [!DNL Query Service].

### Abandono de navegador do Adobe Analytics

Essa [navegue pelos centros de exemplo de abandono do Adobe [!DNL Analytics]](./use-cases/abandoned-cart.md) dados para criar um público-alvo acionável específico. [!DNL Query Service] O acomoda uma lógica complexa de segmentação para calcular vários atributos personalizados para uso em downstream ou para simplificar bastante a criação de seus segmentos.

### Painéis BI do Looker

Com o Adobe Experience Platform, você pode assimilar, armazenar, estruturar e extrair todos os conjuntos de dados armazenados, incluindo dados comportamentais, CRM e de ponto de venda. Usando [!DNL Experience Platform's Query Service], você pode consultar esses conjuntos de dados e responder perguntas específicas sobre os negócios e começar a gerar insights impactantes. O vídeo a seguir demonstra o valor da criação de painéis nas ferramentas de inteligência empresarial (BI) usando [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Próximas etapas e recursos adicionais

Ao ler este documento, você foi apresentado a [!DNL Query Service] e como ele funciona dentro do maior escopo de [!DNL Experience Platform]. Para obter mais informações sobre a interação com vários endpoints do [!DNL Query Service] Leia a API [Guia do desenvolvedor do Serviço de query](api/getting-started.md). Para obter mais informações sobre como usar o serviço interativo no [!DNL Platform]Por favor leia o [Guia da interface do usuário do Serviço de query](ui/overview.md). Para obter uma lista abrangente de conexão de clientes externos com o [!DNL Query Service]Por favor leia o [Visão geral dos clientes do Serviço de query](clients/overview.md).

Para se preparar melhor para executar consultas, assista ao vídeo a seguir. Este vídeo compartilha dicas e práticas recomendadas para executar consultas na interface do Editor de consultas, clientes PSQL, soluções de business intelligence (BI) e a API HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
