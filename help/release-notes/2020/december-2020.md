---
title: Notas de versão da Adobe Experience Platform de dezembro de 2020
description: As notas de versão de dezembro de 2020 para o Adobe Experience Platform.
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
exl-id: 89d631f1-1b11-4a18-98e1-08e1d5bd8b0d
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 11%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 9 de dezembro de 2020**

Novos recursos na Adobe Experience Platform:

- [[!DNL Dataflows]](#dataflows)

Atualizações dos recursos já existentes na Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Dataflows] {#dataflows}

Os fluxos de dados são uma representação de trabalhos de dados que movem os dados pela Plataforma. Esses fluxos de dados são configurados em diferentes serviços, ajudando a mover dados dos conectores de origem para conjuntos de dados de destino, para o Serviço de identidade e perfil e para destinos.

**Recurso de chave**

| Recurso | Descrição |
| ------- | ----------- |
| Transparência para fluxos de dados | Você pode monitorar fluxos de dados de origens e destinos. Para obter mais informações, leia o [tutorial sobre fontes de monitoramento](../../dataflows/ui/monitor-sources.md) ou o [tutorial sobre destinos de monitoramento](../../dataflows/ui/monitor-destinations.md). |

Para saber mais sobre fluxos de dados, leia a [visão geral sobre fluxos de dados](../../dataflows/home.md).

## [!DNL Data Science Workspace] {#dsw}

O Data Science Workspace usa aprendizagem de máquina e inteligência artificial para criar insights a partir de seus dados. Integrado à Adobe Experience Platform, o Data Science Workspace ajuda a fazer previsões usando seus ativos de conteúdo e dados nas soluções da Adobe.

**Principais recursos**

| Recurso | Descrição |
| --- | ---|
| Complemento de pacote do Adobe Experience Platform Intelligence | O complemento Adobe Experience Platform Intelligence package é uma atualização do Data Science Workspace que desbloqueia recursos principais adicionais, como: <li> Experimentação e avaliação de modelos orientados pela interface.</li><li> Capacidade de implantar e operacionalizar modelos com treinamentos programados e tarefas de inferência.</li><li> Suporte para deep learning em modelos de fluxo de sensor (GPU Compute).</li><li> Computação distribuída baseada no Spark para treinar e pontuar em relação a grandes conjuntos de dados (10 MM + linhas).</li><li>E muito mais</li> |

Para saber mais sobre o complemento de pacote do Adobe Experience Platform Intelligence, consulte a documentação sobre [acesso e recursos do Data Science Workspace](../../data-science-workspace/access-features-dsw.md).

## [!DNL Sources] {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir que você estruture, rotule e aprimore esses dados usando os serviços do [!DNL Platform]. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O [!DNL Experience Platform] fornece uma API RESTful e uma interface do usuário interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Atualizar detalhes da conta e da conexão para fontes de transmissão | Agora você pode atualizar os nomes, as descrições e as credenciais das conexões de streaming existentes usando a API [!DNL Flow Service] e a interface do usuário. Para obter mais informações, consulte o tutorial sobre [atualização de conexões usando a API](../../sources/tutorials/api/update.md) e [edição de detalhes da conta usando a interface](../../sources/tutorials/ui/monitor.md). |
| Excluir fluxos de dados | Os fluxos de dados de transmissão que contêm erros ou se tornaram desnecessários agora podem ser excluídos usando a API [!DNL Flow Service] e a interface do usuário. Para obter mais informações, consulte o tutorial sobre [exclusão de fluxos de dados usando a API](../../sources/tutorials/api/delete-dataflows.md) e [exclusão de fluxos de dados usando a interface](../../sources/tutorials/ui/delete.md). |

Para saber mais sobre fontes, consulte a [visão geral das fontes](../../sources/home.md).
