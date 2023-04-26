---
title: Notas de versão da Adobe Experience Platform
description: As notas de versão de março de 2023 para o Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 938b4ba7affadc7ad0eca086d7cc2c9ce1a54a83
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 6%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 26 de abril de 2023**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Painéis](#dashboards)
- [Preparação de dados](#data-prep)
- [Experience Data Model](#xdm)
- [Perfil do cliente em tempo real](#profile)
- [Fontes](#sources)

## Painéis {#dashboards}

O Adobe Experience Platform fornece vários painéis através dos quais você pode visualizar informações importantes sobre os dados de sua organização, como capturados durante os instantâneos diários.

**Recursos novos ou atualizados** {#dashboards-new-updated-features}

| Recurso | Descrição |
| --- | --- |
| Painéis definidos pelo usuário | Agora você pode **filtrar dados históricos** dos seus insights de widget e use dados recentes ou um período de análise personalizado.<br>Você também pode **duplicar os widgets existentes**. Ao personalizar uma duplicata e editar seus atributos, você pode evitar a reinicialização a partir do início ao criar um novo widget exclusivo. |

{style="table-layout:auto"}

Para obter mais informações sobre painéis, incluindo como conceder permissões de acesso e criar widgets personalizados, comece lendo o [visão geral dos painéis](../../dashboards/home.md).

## Preparação de dados {#data-prep}

A Preparação de dados permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Atualizações do período de preenchimento retroativo para Adobe Analytics em sandboxes de não produção | O período de preenchimento retroativo para Adobe Analytics em sandboxes de não produção foi reduzido para três meses. O preenchimento retroativo de sandboxes de produção permanece o mesmo em 13 meses. Essa alteração se aplica somente a novos fluxos e não afetará os fluxos existentes. Para obter mais informações, leia a [Visão geral do Adobe Analytics](../../sources/connectors/adobe-applications/analytics.md). |
| Nova função mapeadora para converter strings FPID em ECID | Use o `fpid_to_ecid` para converter strings FPID em ECID para uso em aplicativos Experience Platform e Experience Cloud. Para obter mais informações, leia a [Guia de funções de Preparação de dados](../../data-prep/functions.md). |

{style="table-layout:auto"}

Para obter mais informações sobre Preparação de dados, leia a [Visão geral da preparação de dados](../../data-prep/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Adobe Experience Platform. Ao seguir os padrões XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de uma maneira mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Alternar nomes para exibição | O Editor de esquema agora oferece um botão para alterar os nomes dos campos originais e os nomes de exibição legíveis em humanos. Essa flexibilidade permite uma melhor descoberta de campo e edição de seus esquemas. Os nomes de exibição para grupos de campos padrão são gerados pelo sistema, mas também podem ser personalizados por meio da interface do usuário, se necessário. |

{style="table-layout:auto"}

Para obter mais informações sobre o XDM na Platform, leia o [Visão geral do sistema XDM](../../xdm/home.md).

## Perfil do cliente em tempo real {#profile}

O Adobe Experience Platform permite que você conduza experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagirem com sua marca. Com o Perfil do cliente em tempo real, você pode ver uma visualização holística de cada cliente individual que combina dados de vários canais, incluindo dados online, offline, CRM e de terceiros. O Perfil permite consolidar os dados do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

**Recursos atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Expiração de dados de perfil pseudônimo | O prazo de validade dos dados de perfil pseudônimo está agora disponível! Esta versão removerá continuamente perfis pseudônimos obsoletos da sua instância do Experience Platform depois de ativados. Para saber mais sobre esse recurso e Perfis pseudônimos, leia o [Guia de expiração de dados de perfil pseudônimo](../../profile/pseudonymous-profiles.md). |

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e permite estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Suporte a API para filtrar dados em nível de linha para Microsoft Dynamics, Salesforce CRM e Salesforce Marketing Cloud | Use operadores lógicos e de comparação para filtrar dados no nível da linha para as fontes de Marketing Cloud do Microsoft Dynamics, Salesforce CRM e Salesforce. Leia o guia em [filtragem de dados de uma fonte usando a API](../../sources/tutorials/api/filter.md) para obter mais informações. |
| Disponibilidade beta do Shopify Streaming | O [Comprar fonte de transmissão](../../sources/connectors/ecommerce/shopify-streaming.md) O agora está disponível em beta. Use a fonte de transmissão Shopify para transmitir dados da sua conta de parceiros Shopify para o Experience Platform. |
| Disponibilidade geral da integração do OneTrust | O [Origem de Integração do OneTrust](../../sources/connectors/consent-and-preferences/onetrust.md) agora está pronta. Use a fonte de integração do OneTrust para trazer os dados de consentimento e preferências da sua conta de Integração do OneTrust para o Experience Platform. |
| Disponibilidade geral da Oracle Service Cloud | O [Origem da nuvem do Oracle Service](../../sources/connectors/customer-success/oracle-service-cloud.md) agora está pronta. Use a fonte da nuvem do Oracle Service para trazer seus dados da nuvem do Oracle Service para o Experience Platform. |

{style="table-layout:auto"}

Para saber mais sobre fontes, leia a [visão geral das fontes](../../sources/home.md).