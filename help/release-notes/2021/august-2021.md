---
title: Notas de versão da Adobe Experience Platform
description: Notas de versão do Experience Platform de 25 de agosto de 2021.
doc-type: release notes
last-update: August 25, 2021
author: ens28527
source-git-commit: bd3d60e1960b1f4c32ade8c4070d7c1b01e5ba07
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 9%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 25 de agosto de 2021**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Insights de capacidade de observação](#observability)
- [Perfil do cliente em tempo real](#profile)
- [Fontes](#sources)

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
