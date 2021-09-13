---
title: Notas de versão da Adobe Experience Platform
description: As notas de versão mais recentes do Adobe Experience Platform.
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: e9d5f24bec8cd2793ce30245b46c1d912bf17cc7
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 8%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 25 de agosto de 2021**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Destinos](#destinations)
- [Insights de capacidade de observação](#observability)
- [Perfil do cliente em tempo real](#profile)
- [Fontes](#sources)

## Destinos {#destinations}

Os destinos são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, anúncios direcionados e muitos outros casos de uso.

**Novos destinos**

| Destino | Descrição |
| ----------- | ----------- |
| [[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md) | O destino dos Atributos de nave, anteriormente em beta, agora está disponível no geral. |
| [[!DNL Airship Tags]](../../destinations/catalog/mobile-engagement/airship-tags.md) | O destino das Tags de nave, anteriormente em beta, agora está disponível no geral. |
| [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md) | O destino brasileiro, antes beta, já está disponível no geral. |
| [[!DNL Pinterest Customer List]](../../destinations/catalog/advertising/pinterest.md) | Com o destino da Lista de clientes do Pinterest , é possível criar públicos-alvo a partir de suas listas de clientes, pessoas que visitaram seu site ou pessoas que já interagiram com seu conteúdo no Pinterest. |
| [[!DNL Twitter Custom Audiences]](../../destinations/catalog/social/twitter.md) | Direcione seus seguidores e clientes existentes no Twitter e crie campanhas de re-marketing relevantes ativando seus públicos-alvo criados no Adobe Experience Platform. |
| [[!DNL Verizon Media/Yahoo DataX]](../../destinations/catalog/advertising/datax.md) | O DataX é uma infraestrutura agregada da Verizon Media/Yahoo que hospeda vários componentes que permitem que o Verizon Media/Yahoo troque dados com seus parceiros externos de forma segura, automatizada e escalável. |

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| [[!DNL Destination SDK]](../../destinations/destination-sdk/overview.md) | O Adobe Experience Platform Destination SDK é um conjunto de APIs de configuração que permitem configurar padrões de integração de destino para o Experience Platform para fornecer dados de público-alvo e perfil ao seu terminal, com base em dados e formatos de autenticação de sua escolha. As configurações são armazenadas no Experience Platform e podem ser recuperadas por meio da API para obter atualizações adicionais. |
| [Aprimoramentos de usabilidade para destinos](../../destinations/ui/activation-overview.md) | As melhorias de usabilidade para destinos permitem que os profissionais de marketing ativem segmentos com facilidade para destinos existentes. |

Para obter informações mais gerais sobre destinos, consulte a [visão geral de destinos](../../destinations/home.md).

## Insights de capacidade de observação {#observability}

Os Insights de capacidade de observação permitem monitorar as atividades da plataforma por meio do uso de métricas estatísticas e notificações de eventos.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Alertas | Agora você pode assinar alertas importantes relacionados a fluxos de trabalho em execução na plataforma. Após assinar regras de alerta específicas, você receberá notificações e emails na interface do usuário quando um evento importante do ciclo de vida ocorrer (como assimilação de dados bem-sucedida) ou se houver problemas que precisem de sua atenção (como uma falha no fluxo de assimilação ou uma tarefa de segmento que leva mais tempo do que o esperado). Para obter mais informações, consulte a [visão geral de alertas](../../observability/alerts/overview.md). |

Consulte a [Visão geral dos Insights de capacidade de observação](../../observability/home.md) para obter mais informações sobre o serviço.

## Perfil do cliente em tempo real {#profile}

O Adobe Experience Platform permite que você conduza experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagirem com sua marca. Com o Perfil do cliente em tempo real, você pode ver uma visualização holística de cada cliente individual que combina dados de vários canais, incluindo dados online, offline, CRM e de terceiros. O Perfil permite consolidar os dados do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

| Recurso | Descrição |
| ------- | ----------- |
| Procurar perfis por política de mesclagem ou identidade | Ao navegar pelos perfis no Experience Platform, agora é possível navegar pela política de mesclagem para visualizar 20 perfis de amostra com base na política de mesclagem selecionada. Você também pode navegar por identidade para procurar por um perfil específico usando um namespace de identidade e valor de identidade relacionado. Para obter mais informações, consulte o [Guia da interface do usuário do perfil do cliente em tempo real](../../profile/ui/user-guide.md). |

Para saber mais sobre o Perfil do cliente em tempo real, incluindo tutoriais e práticas recomendadas para trabalhar com dados de perfil, comece lendo a [Visão geral do perfil do cliente em tempo real](../../profile/home.md).

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

| Recurso | Descrição |
| ------- | ----------- |
| Conector de origem de carregamento de arquivo local | A categoria de assimilação de arquivo foi renomeada para sistema local, permitindo trazer arquivos locais diretamente para a Platform usando o conector de upload de arquivo local. Os dados assimilados por meio desse conector podem ser monitorados pelo Painel de monitoramento. Consulte a [visão geral da fonte de upload de arquivo local](../../sources/connectors/local-system/local-file-upload.md) para obter mais informações. |

Para saber mais sobre fontes, consulte a [visão geral das fontes](../../sources/home.md).
