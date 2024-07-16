---
title: Notas de versão da Adobe Experience Platform de agosto de 2021
description: As notas de versão de agosto de 2021 para Adobe Experience Platform.
doc-type: release notes
last-update: August 25, 2021
author: ens28527
exl-id: 0513b9dc-b16c-43b3-8e17-4be4499308d4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 35%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: quinta-feira, 25 de agosto de 2021**

Atualizações dos recursos já existentes na Adobe Experience Platform:

- [Destinos](#destinations)
- [Insights de capacidade de observação](#observability)
- [Perfil do cliente em tempo real](#profile)
- [Origens](#sources)

## Destinos {#destinations}

Os destinos são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Novos destinos**

| Destino | Descrição |
| ----------- | ----------- |
| [[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md) | O destino de Atributos do dirigível, anteriormente em beta, agora está geralmente disponível. |
| [[!DNL Airship Tags]](../../destinations/catalog/mobile-engagement/airship-tags.md) | O destino Airship Tags, anteriormente na versão beta, agora está geralmente disponível. |
| [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md) | O destino Braze, anteriormente em beta, agora está disponível em geral. |
| [[!DNL Pinterest Customer List]](../../destinations/catalog/advertising/pinterest.md) | Com o destino da Lista de clientes do Pinterest, você pode criar públicos-alvo a partir de suas listas de clientes, pessoas que visitaram seu site ou pessoas que já interagiram com seu conteúdo no Pinterest. |
| [[!DNL Twitter Custom Audiences]](../../destinations/catalog/social/twitter.md) | Direcione seus seguidores e clientes existentes no Twitter e crie campanhas de re-marketing relevantes ativando seus públicos-alvo criados no Adobe Experience Platform. |
| [[!DNL Verizon Media/Yahoo DataX]](../../destinations/catalog/advertising/datax.md) | DataX é uma infraestrutura agregada da Verizon Media/Yahoo que hospeda vários componentes que permitem à Verizon Media/Yahoo trocar dados com seus parceiros externos de maneira segura, automatizada e escalável. |

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| [[!DNL Destination SDK]](../../destinations/destination-sdk/overview.md) | O Adobe Experience Platform Destination SDK é um conjunto de APIs de configuração que permitem configurar padrões de integração de destino para que o Experience Platform forneça dados de público-alvo e perfil para o seu endpoint, com base nos formatos de dados e autenticação de sua escolha. As configurações são armazenadas em Experience Platform e podem ser recuperadas por meio da API para atualizações adicionais. |
| [Melhorias de usabilidade nos Destinos](../../destinations/ui/activation-overview.md) | Os aprimoramentos de usabilidade nos destinos permitem que os profissionais de marketing ativem segmentos para destinos existentes. |

Para obter informações mais gerais sobre destinos, consulte a [visão geral de destinos](../../destinations/home.md).

## Insights de capacidade de observação {#observability}

Os Insights de capacidade de observação permitem monitorar as atividades da Platform por meio do uso de métricas estatísticas e notificações de eventos.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Alertas | Agora você pode assinar alertas importantes relacionados a fluxos de trabalho em execução na Platform. Depois de se inscrever em regras de alerta específicas, você receberá notificações e emails na interface do usuário quando ocorrer um evento importante do ciclo de vida (como uma assimilação de dados bem-sucedida) ou se houver problemas que precisem de sua atenção (como uma falha de fluxo de assimilação ou um trabalho de segmento que está demorando mais do que o esperado). Para obter mais informações, consulte a [visão geral dos alertas](../../observability/alerts/overview.md). |

Consulte a [Visão geral dos Insights de Observabilidade](../../observability/home.md) para obter mais informações sobre o serviço.

## Perfil do cliente em tempo real {#profile}

A Adobe Experience Platform permite gerar experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagem com sua marca. Com o Perfil do cliente em tempo real, é possível ter uma visão integral de cada cliente ao combinar dados de vários canais, incluindo online, offline, CRM e de terceiros. O Perfil permite consolidar os dados do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

| Recurso | Descrição |
| ------- | ----------- |
| Procurar perfis por política de mesclagem ou identidade | Ao navegar pelos perfis no Experience Platform, agora é possível navegar por política de mesclagem para visualizar 20 perfis de amostra com base na política de mesclagem selecionada. Você também pode procurar por identidade para procurar um perfil específico usando um namespace de identidade e um valor de identidade relacionado. Para obter mais informações, consulte o [Guia da Interface do Usuário do Perfil do Cliente em Tempo Real](../../profile/ui/user-guide.md). |

Para saber mais sobre o Perfil de cliente em tempo real, incluindo tutoriais e práticas recomendadas para trabalhar com dados de perfil, comece lendo a [Visão geral do Perfil do cliente em tempo real](../../profile/home.md).

## Origens {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. É possível assimilar dados de várias origens, como aplicativos da Adobe, do armazenamento na nuvem, um software de terceiros e do seu sistema de CRM.

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

| Recurso | Descrição |
| ------- | ----------- |
| Conector de origem de carregamento de arquivo local | A categoria de assimilação de arquivo foi renomeada para sistema local, permitindo que você traga arquivos locais diretamente para a Platform usando o conector de upload de arquivo local. Os dados assimilados por meio desse conector podem ser monitorados por meio do Painel de monitoramento. Consulte a [visão geral da origem de carregamento do arquivo local](../../sources/connectors/local-system/local-file-upload.md) para obter mais informações. |

Para saber mais sobre fontes, consulte a [visão geral das fontes](../../sources/home.md).
