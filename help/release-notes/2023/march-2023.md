---
title: Notas de versão da Adobe Experience Platform de março de 2023
description: As notas de versão de março de 2023 para o Adobe Experience Platform.
source-git-commit: 38c3461f1d84fca83fd04eef57aae28de4744e17
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 4%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 29 de março de 2023**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Coleta de dados](#data-collection)
- [Preparação de dados](#data-prep)
- [Destinos](#destinations)
- [Serviço de segmentação](#segmentation)
- [Fontes](#sources)

## Coleta de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente e enviá-los para a Adobe Experience Platform Edge Network, onde podem ser enriquecidos, transformados e distribuídos para destinos Adobe ou não-Adobe.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Novo fluxo de trabalho de início rápido para a API Meta conversões (Beta) | Acesse novos fluxos de trabalho de início rápido em &quot;Introdução&quot; na tela inicial da Coleta de dados! O [fluxo de trabalho de início rápido para a API de Meta conversões](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) permite que os clientes coletem e encaminhem rapidamente os dados do evento, do lado do servidor para o Meta para conversões de anúncios em apenas algumas etapas simples. |
| Novo fluxo de trabalho de início rápido para o SDK móvel (Beta) | Acesse novos fluxos de trabalho de início rápido em &quot;Introdução&quot; na tela inicial da Coleta de dados! O [fluxo de trabalho de início rápido para o Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) O permite implementar rapidamente o SDK móvel e validar eventos móveis básicos em apenas algumas etapas simples. |
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

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, anúncios direcionados e muitos outros casos de uso.

**Novos destinos** {#new-destinations}

| Destino | Descrição |
| ----------- | ----------- |
| [[!DNL Adobe Commerce] conexão GA](../../destinations/catalog/personalization/adobe-commerce.md) | O [!DNL Adobe Commerce] o conector de destino (agora disponível geralmente) permite selecionar um ou mais públicos-alvo do Real-Time CDP para ativar em seu [!DNL Adobe Commerce] conta para fornecer uma experiência personalizada dinâmica para seus compradores. |
| [[!DNL Snap Inc] conexão GA](../../destinations/catalog/advertising/snap-inc.md) | O [!DNL Snap Inc] o conector de destino (agora disponível no geral) permite que os profissionais de marketing importem segmentos de usuários criados no Experience Platform para [!DNL Snapchat Ads] e use-as para direcionar seus anúncios. |
| [Conexão Eloqua do Oracle (API)](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | Use a conexão baseada em API para [!DNL Oracle Eloqua] para planejar e executar campanhas, fornecendo uma experiência personalizada do cliente para seus prospetos em [!DNL Oracle Eloqua]. |
| [(Beta) [!DNL Amazon Ads] conexão](../../destinations/catalog/advertising/amazon-ads.md) | O [!DNL Amazon Ads] a integração com o Adobe Experience Platform fornece integração completa para [!DNL Amazon Ads] , incluindo a [!DNL Amazon DSP (ADSP)]. Usar o [!DNL Amazon Ads] no Adobe Experience Platform, os usuários podem definir públicos do anunciante para direcionamento e ativação no [!DNL Amazon DSP]. |
| [[!DNL Marketo Measure Ultimate] conexão](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] (anteriormente Bizible) fornece aos profissionais de marketing informações sobre quais esforços de marketing são os mais eficazes na geração de receita e na maximização do retorno sobre o investimento de sua empresa. O destino habilita os fluxos de dados B2B (B2B) de negócios para o Adobe Experience Platform [!DNL Marketo Measure]. O cartão só está disponível para [!DNL Marketo Measure Ultimate] clientes. |
| [Conexão TikTok](../../destinations/catalog/social/tiktok.md) | Crie públicos personalizados no TikTok com seus dados para segmentação com suas campanhas de publicidade. |
| [Conexão com o Zendesk](../../destinations/catalog/crm/zendesk.md) | Usar este destino para criar e atualizar identidades em um segmento como contatos dentro de [!DNL Zendesk]. |

{style="table-layout:auto"}

**Funcionalidade nova ou atualizada** {#destinations-new-updated-functionality}

| Funcionalidade | Descrição |
| ----------- | ----------- |
| Nova permissão de controle de acesso para destinos: [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | A nova permissão oferece aos usuários a capacidade de ativar segmentos para destinos existentes, sem exibir a variável [etapa de mapeamento](../../destinations/ui/activate-batch-profile-destinations.md#mapping). Os usuários podem adicionar e remover segmentos em workflows de ativação, mas não podem adicionar ou remover atributos ou identidades mapeadas. |

{style="table-layout:auto"}

**Correções e aprimoramentos** {#destinations-fixes-and-enhancements}

Estamos lançando uma correção de erro para criptografia PGP/GPG em destinos com base em arquivo para CDP em tempo real. Com essa alteração, os destinos existentes baseados em arquivos que atualmente usam criptografia gerarão um nome de arquivo com uma extensão diferente de antes.

- Extensão atual ao usar criptografia: `filename.csv`
- Extensão futura ao usar criptografia: `filename.csv.gpg`

Para obter informações mais gerais sobre destinos, consulte [visão geral dos destinos](../../destinations/home.md).

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
