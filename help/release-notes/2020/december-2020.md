---
title: Notas de versão da Adobe Experience Platform
description: Notas de versão de Experience Platform 9 de dezembro de 2020
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
translation-type: tm+mt
source-git-commit: ae353e6dda3f92647c32ee8e731be5785d24e5cb
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 6%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 9 de dezembro de 2020**

Novos recursos no Adobe Experience Platform:

- [[!DNL Dataflows]](#dataflows)

Atualizações dos recursos existentes na Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Dataflows] {#dataflows}

Os fluxos de dados são uma representação de trabalhos de dados que movem os dados pela Plataforma. Esses fluxos de dados são configurados em diferentes serviços, ajudando a mover dados de conectores de origem para conjuntos de dados de público alvo, para Serviço de identidade e Perfil e para destinos.

**Recurso principal**

| Recurso | Descrição |
| ------- | ----------- |
| Transparência para fluxos de dados | Você pode monitorar fluxos de dados para fontes e destinos. Para obter mais informações, leia o [tutorial sobre fontes](../../dataflows/ui/monitor-sources.md) de monitoramento ou o [tutorial sobre como monitorar destinos](../../dataflows/ui/monitor-destinations.md). |

Para saber mais sobre os fluxos de dados, leia a visão geral [dos](../../dataflows/home.md)fluxos de dados.

## [!DNL Data Science Workspace] {#dsw}

A Data Science Workspace usa o aprendizado de máquina e a inteligência artificial para criar insights de seus dados. Integrado ao Adobe Experience Platform, o Data Science Workspace ajuda você a fazer previsões usando seu conteúdo e ativos de dados nas soluções de Adobe.

**Principais recursos**

| Recurso | Descrição |
| --- | ---|
| Anúncio de pacote do Adobe Experience Platform Intelligence | O complemento do pacote Adobe Experience Platform Intelligence é uma atualização da Data Science Workspace que desbloqueia recursos principais adicionais, como: <li> Experimentação e avaliação de modelos orientados pela interface do usuário.</li><li> Capacidade de implantar e operacionalizar modelos com treinamentos programados e trabalhos de dedução.</li><li> Suporte para o aprendizado profundo em modelos de fluxo de dados (GPU Compute).</li><li> Computação distribuída com base em faísca para treinar e pontuar com base em grandes conjuntos de dados (10MM + linhas).</li><li>E mais</li> |

Para saber mais sobre o complemento do pacote Adobe Experience Platform Intelligence, consulte a documentação sobre acesso e recursos [da](../../data-science-workspace/access-features-dsw.md)Data Science Workspace.

## [!DNL Sources] {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas, permitindo que você estruture, rotule e aprimore esses dados usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos de Adobe, armazenamentos baseados em nuvem, software de terceiros e seu sistema de CRM.

[!DNL Experience Platform] fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem que você se autentique e se conecte a sistemas de armazenamentos externos e serviços CRM, defina horários para execuções de ingestão e gerencie a throughput de ingestão de dados.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Atualizar detalhes de conta e conexão para fontes de transmissão | Agora você pode atualizar os nomes, as descrições e as credenciais das conexões de streaming existentes usando a [!DNL Flow Service] API e a interface do usuário. Para obter mais informações, consulte o tutorial sobre como [atualizar conexões usando a API](../../sources/tutorials/api/update.md) e [editar detalhes da conta usando a interface do usuário](../../sources/tutorials/ui/monitor.md). |
| Excluir fluxos de dados | Fluxos de dados de fluxo que contêm erros ou se tornaram desnecessários agora podem ser excluídos usando a [!DNL Flow Service] API e a interface do usuário. Para obter mais informações, consulte o tutorial sobre como [excluir fluxos de dados usando a API](../../sources/tutorials/api/delete-dataflows.md) e [excluir fluxos de dados usando a interface do usuário](../../sources/tutorials/ui/delete.md). |

Para saber mais sobre fontes, consulte a visão geral [das](../../sources/home.md)fontes.


