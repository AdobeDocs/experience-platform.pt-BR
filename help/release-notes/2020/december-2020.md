---
title: Notas de versão da Adobe Experience Platform de dezembro de 2020
description: As notas de versão de dezembro de 2020 para o Adobe Experience Platform.
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
exl-id: 89d631f1-1b11-4a18-98e1-08e1d5bd8b0d
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 8%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 9 de dezembro de 2020**

Novos recursos no Adobe Experience Platform:

- [[!DNL Dataflows]](#dataflows)

Atualizações dos recursos existentes na Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Dataflows] {#dataflows}

Os fluxos de dados são uma representação de trabalhos de dados que movem os dados pela Plataforma. Esses fluxos de dados são configurados em diferentes serviços, ajudando a mover dados de conectores de origem para conjuntos de dados de destino, para Serviço de identidade e perfil e para destinos.

**Recurso principal**

| Recurso | Descrição |
| ------- | ----------- |
| Transparência dos fluxos de dados | Você pode monitorar fluxos de dados para fontes e destinos. Para obter mais informações, leia o [tutorial sobre fontes de monitoramento](../../dataflows/ui/monitor-sources.md) ou [tutorial sobre monitoramento de destinos](../../dataflows/ui/monitor-destinations.md). |

Para saber mais sobre fluxos de dados, leia a [visão geral dos fluxos de dados](../../dataflows/home.md).

## [!DNL Data Science Workspace] {#dsw}

O Data Science Workspace usa o aprendizado de máquina e a inteligência artificial para criar insights de seus dados. Integrado ao Adobe Experience Platform, o Data Science Workspace ajuda você a fazer previsões usando seus ativos de conteúdo e dados nas soluções de Adobe.

**Principais recursos**

| Recurso | Descrição |
| --- | ---|
| Aditamento de pacote Adobe Experience Platform Intelligence | O complemento do pacote Adobe Experience Platform Intelligence é uma atualização do Data Science Workspace que desbloqueia recursos principais adicionais, como: <li> Experimentação e avaliação de modelo orientada pela interface do usuário.</li><li> Capacidade de implantar e operacionalizar modelos com treinamento programado e trabalhos de inferência.</li><li> Suporte para aprendizado profundo em modelos de Tensorflow (GPU Compute).</li><li> Computação distribuída com base em Spark para treinar e pontuar em relação a grandes conjuntos de dados (10MM + linhas).</li><li>E mais</li> |

Para saber mais sobre o pacote Adobe Experience Platform Intelligence, consulte a documentação em [Acesso e recursos da Data Science Workspace](../../data-science-workspace/access-features-dsw.md).

## [!DNL Sources] {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos de Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

[!DNL Experience Platform] O fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Atualizar detalhes de conta e conexão para fontes de transmissão | Agora você pode atualizar os nomes, as descrições e as credenciais das conexões de transmissão existentes usando o [!DNL Flow Service] API e a interface do usuário. Para obter mais informações, consulte o tutorial em [atualização de conexões usando a API](../../sources/tutorials/api/update.md) e [editar detalhes da conta usando a interface do usuário](../../sources/tutorials/ui/monitor.md). |
| Excluir fluxos de dados | Fluxos de dados de fluxo que contêm erros ou se tornaram desnecessários agora podem ser excluídos usando o [!DNL Flow Service] API e a interface do usuário. Para obter mais informações, consulte o tutorial em [exclusão de fluxos de dados usando a API](../../sources/tutorials/api/delete-dataflows.md) e [exclusão de fluxos de dados usando a interface do usuário](../../sources/tutorials/ui/delete.md). |

Para saber mais sobre fontes, consulte o [visão geral das fontes](../../sources/home.md).
