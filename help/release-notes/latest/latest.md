---
title: Notas de versão da Adobe Experience Platform
description: As notas de versão de março de 2023 para o Adobe Experience Platform.
source-git-commit: c5061a759f1098ce1dcc7e3f00c52e064239d7c5
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 5%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 29 de março de 2023**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Coleta de dados](#data-collection)
- [Preparação de dados](#data-prep)
- [Serviço de segmentação](#segmentation)
- [Fontes](#sources)

## Coleta de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente e enviá-los para a Adobe Experience Platform Edge Network, onde podem ser enriquecidos, transformados e distribuídos para destinos Adobe ou não-Adobe.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Novo fluxo de trabalho de início rápido para a API Meta conversões (Beta) | Acesse novos fluxos de trabalho de início rápido em &quot;Introdução&quot; na tela inicial da Coleta de dados! O [fluxo de trabalho de início rápido para a API de Meta conversões](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) permite que os clientes coletem e encaminhem rapidamente os dados do evento, do lado do servidor para o Meta para conversões de anúncios em apenas algumas etapas simples. |
| [!DNL Braze] extensão de encaminhamento de eventos | O [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) a extensão de encaminhamento de eventos permite aproveitar os dados capturados na Rede de borda do Adobe Experience Platform e enviá-los para [!DNL Braze] na forma de eventos do lado do servidor usando o [!DNL Braze] APIs de rastreamento de usuário. |
| [!DNL Mixpanel] extensão de encaminhamento de eventos | O [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) A extensão permite que os clientes aproveitem o encaminhamento do evento para capturar informações do evento na Rede de borda do Adobe Experience Platform e enviá-las para o Mixpanel usando a API de rastreamento de eventos. |

{style="table-layout:auto"}

## Preparação de dados {#data-prep}

A Preparação de dados permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Novas funções para codificação e decodificação de strings de URL | <ul><li>O `get_url_encoded` assume um URL como entrada e substitui ou codifica caracteres especiais com caracteres ASCII.</li><li>O `get_url_decoded` assume um URL como entrada e decodifica caracteres ASCII em caracteres especiais.</li></ul> Para obter mais informações, leia a [Guia de funções de Preparação de dados](../../data-prep/functions.md). Para obter uma lista abrangente de caracteres reservados e seus caracteres codificados correspondentes, leia o guia em [caracteres especiais](../../data-prep/functions.md#special-characters). |

Para obter mais informações sobre Preparação de dados, leia a [Visão geral da preparação de dados](../../data-prep/home.md).

## Serviço de segmentação {#segmentation}

[!DNL Segmentation Service] O define um subconjunto específico de perfis ao descrever os critérios que distinguem um grupo comercializável de pessoas dentro da base do cliente. Os segmentos podem se basear em dados de registro (como informações demográficas) ou em eventos de séries cronológicas que representem as interações do cliente com sua marca.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Métricas de perfil | Para fornecer uma representação mais precisa das métricas de perfil, o detalhamento da associação e as métricas de rotatividade estão sendo combinados e agora são calculadas por um período de 24 horas. Mais informações estão disponíveis na [Guia da interface do usuário de segmentação](../../segmentation/ui/overview.md#browse) |

{style="table-layout:auto"}

Para obter mais informações sobre [!DNL Segmentation Service]consulte o [Visão geral da segmentação](../../segmentation/home.md).

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e permite estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Disponibilidade beta de [!DNL Chatlio] | O [!DNL Chatlio] A fonte agora está disponível em beta. Use o [!DNL Chatlio] origem para transmitir [!DNL Chatlio] dados de eventos para o Experience Platform. Para obter mais informações, leia a [[!DNL Chatlio] visão geral](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| Disponibilidade beta de [!DNL Customer.io] | O [!DNL Customer.io] A fonte agora está disponível em beta. Use o [!DNL Customer.io] fonte para transmitir os dados de eventos do cliente para o Experience Platform. Para obter mais informações, leia a [[!DNL Customer.io] visão geral](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| Disponibilidade beta de [!DNL Pendo] | O [!DNL Pendo] A fonte agora está disponível em beta. Use o [!DNL Pendo] fonte para transmitir os dados de análise do produto para o Experience Platform. Para obter mais informações, leia a [[!DNL Pendo] visão geral](../../sources/connectors/analytics/pendo-webhook.md). |
| Suporte para fluxos de dados de rascunho | Agora é possível usar a API do Serviço de fluxo para definir os fluxos de dados para um estado de rascunho. Fluxos de dados preparados podem ser atualizados e publicados posteriormente com novas informações. Para obter mais informações, leia o guia sobre [definição dos fluxos de dados de origens como rascunhos](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

Para saber mais sobre fontes, leia a [visão geral das fontes](../../sources/home.md).
