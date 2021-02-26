---
title: Notas de versão da Adobe Experience Platform
description: Notas de versão de Experience Platform para 24 de fevereiro de 2021.
doc-type: release notes
last-update: February 24, 2021
author: ens70167
translation-type: tm+mt
source-git-commit: 2eea954217a8f0cca605cd0435bace59200cacda
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 7%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 24 de fevereiro de 2021**

Novos recursos no Adobe Experience Platform:

- [painéis (Beta)](#dashboards)

Atualizações dos recursos existentes na Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## (Beta) Painéis {#dashboards}

A Adobe Experience Platform fornece vários painéis através dos quais você pode visualização informações importantes sobre os dados de sua organização, como capturados durante os instantâneos diários.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Perfis, segmentos, destinos e Painéis de uso de licença (Beta) | **Observação: A funcionalidade do painel está atualmente em beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.**<br/><br/> Os painéis fornecem relatórios prontos para uso nos dados de sua organização e são incorporados diretamente no fluxo de trabalho do comerciante dentro da Plataforma. Esses painéis estão disponíveis sem a necessidade de suporte adicional de TI ou o tempo e o esforço necessários para exportar e processar dados com projeto e implementação adicionais do data warehouse. |

## [!DNL Data Science Workspace] {#dsw}

A Data Science Workspace usa o aprendizado de máquina e a inteligência artificial para criar insights de seus dados. Integrado ao Adobe Experience Platform, o Data Science Workspace ajuda você a fazer previsões usando seu conteúdo e ativos de dados nas soluções de Adobe.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Notebook JupyterLab EDA | O notebook da análise de dados exploratórios (EDA) Python agora está disponível em Jupyterlab. Este notebook foi projetado para ajudá-lo a descobrir padrões nos dados, verificar a integridade dos dados e resumir os dados relevantes para modelos preditivos. Consulte o tutorial em [exploração de dados baseados na Web para modelos preditivos](../../data-science-workspace/jupyterlab/eda-notebook.md) para obter mais informações. |

Para obter informações mais gerais sobre a Data Science Workspace, consulte a [visão geral da Data Science Workspace](../../data-science-workspace/home.md).

## [!DNL Dataflows] {#dataflows}

No Adobe Experience Platform, os dados são ingeridos de uma grande variedade de fontes, analisados dentro do Experience Platform e ativados para uma grande variedade de destinos. A plataforma facilita o processo de rastreamento desse fluxo potencialmente não linear de dados ao fornecer transparência com fluxos de dados.

Os fluxos de dados são uma representação de trabalhos de dados que movem os dados pela Plataforma. Esses fluxos de dados são configurados em diferentes serviços, ajudando a mover dados de conectores de origem para conjuntos de dados de público alvo, onde são utilizados por [!DNL Identity Service] e [!DNL Real-time Customer Profile] antes de serem ativados para [!DNL Destinations].

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Novo painel de monitoramento | Agora você pode usar o painel de monitoramento para transparência entre serviços e insights acionáveis para ingestões de dados de origem. O novo painel de monitoramento fornece uma visualização abrangente dos dados processados de [!DNL Data Lake] para [!DNL Identity Service] e para [!DNL Profile], ao mesmo tempo em que permite que você monitore taxas de ingestão, sucessos e falhas. Consulte o tutorial em [fluxos de dados de origem de monitoramento na interface do usuário](../../dataflows/ui/monitor-sources.md) para obter mais informações. |

Para obter informações mais gerais sobre fluxos de dados, consulte a [visão geral dos fluxos de dados](../../dataflows/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados da Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, publicidade direcionada e muitos outros casos de uso.

**Novos destinos**

| Destino | Descrição |
| ----------- | ----------- |
| [[!DNL LinkedIn Matched Audiences]](destinations/catalog/social/linkedin.md) | A conexão [!DNL LinkedIn Matched Audiences] permite ativar o audiência na plataforma social [!DNL LinkedIn]. |

## [!DNL Experience Data Model (XDM) System] {#xdm}

A normalização e a interoperabilidade são conceitos-chave por trás [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), impulsionado pelo Adobe, é um esforço para padronizar os dados de experiência do cliente e definir schemas para o gerenciamento da experiência do cliente.

A XDM é uma especificação publicamente documentada projetada para melhorar o poder das experiências digitais. Fornece estruturas e definições comuns para qualquer aplicativo que se comunique com os serviços da Adobe Experience Platform. Ao aderir aos padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum, fornecendo insights de forma mais rápida e integrada. Você pode obter informações importantes das ações do cliente, definir audiências do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Interface de usuário de pesquisa atualizada | Os recursos de pesquisa aprimorados agora estão disponíveis na guia [!UICONTROL Procurar] no espaço de trabalho [!UICONTROL Schemas] e na caixa de diálogo de seleção de mixin no [!DNL Schema Editor].<br><br>Ao pesquisar um termo anteriormente, os resultados incluiriam somente recursos XDM cujo nome corresponda ao query de pesquisa. Agora, além dos recursos cujo nome corresponda ao query, os recursos que contêm atributos individuais que correspondem ao termo também serão incluídos. Isso permite pesquisar recursos XDM com base nos atributos que eles contêm, em vez de por nome de recurso.<br><br>Consulte os documentos sobre  [exploração de ](../../xdm/ui/explore.md) recursos XDM e  [gerenciamento de ](../../xdm/ui/resources/schemas.md) esquemas na interface do usuário para obter mais informações. |

Para obter informações mais gerais sobre o XDM, consulte a [visão geral do sistema XDM](../../xdm/home.md).

## [!DNL Identity Service] {#identity}

Fornecer experiências digitais relevantes requer uma compreensão completa do cliente. Isso fica mais difícil quando os dados do cliente são fragmentados em sistemas diferentes, fazendo com que cada cliente individual pareça ter várias &quot;identidades&quot;.

A Adobe Experience Platform [!DNL Identity Service] ajuda você a obter uma melhor visualização de seu cliente e de seu comportamento ao unir identidades entre dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e de impacto em tempo real.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Visualizador de gráfico de identidade | O visualizador de gráficos de identidade permite que você valide e visualize identidades que são unidas na interface do usuário, permitindo uma depuração e transparência aprimoradas. Consulte [documento do visualizador de gráficos de identidade](../../identity-service/ui/identity-graph-viewer.md) para obter mais informações. |

Para obter informações mais gerais sobre [!DNL Identity Service], consulte a [visão geral do serviço de identidade](../../identity-service/home.md).

## Perfil do cliente em tempo real {#profile}

A Adobe Experience Platform permite que você direcione experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagem com sua marca. Com o Perfil do cliente em tempo real, você pode ver uma visualização holística de cada cliente individual que combina dados de vários canais, incluindo dados online, offline, CRM e de terceiros. [!DNL Profile] permite consolidar os dados do cliente em uma visualização unificada que oferece uma conta acionável e com carimbos de data e hora de cada interação do cliente.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Atributos calculados (alfa) | ***Observação: Esta funcionalidade está atualmente em alfa e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.*** <br/><br/>Atributos calculados são funções usadas para agregação de dados no nível do evento em atributos no nível do perfil. Você pode usar as agregações na segmentação, ativação e personalização. Alguns exemplos dessas funções incluem contagem, soma, média, mín, máx, true/false. Atributos calculados estão disponíveis atualmente apenas por API. Para obter mais informações, consulte [visão geral dos atributos calculados](../../profile/computed-attributes/overview.md). |

Para obter mais informações sobre o Perfil do cliente em tempo real, incluindo tutoriais e práticas recomendadas para trabalhar com [!DNL Profile] dados, comece lendo a [visão geral do Perfil do cliente em tempo real](../../profile/home.md).

## [!DNL Sources] {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas, permitindo que você estruture, rotule e aprimore esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos de Adobe, armazenamentos baseados em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem que você se autentique e se conecte a sistemas de armazenamentos externos e serviços CRM, defina horários para execuções de ingestão e gerencie a throughput de ingestão de dados.

**Novas fontes**

| Recurso | Descrição |
| --- | --- |
| [!DNL Google PubSub] | Agora é possível conectar [!DNL Google PubSub] a [!DNL Experience Platform] usando a API [!DNL Flow Service] ou a interface do usuário. Consulte a [[!DNL Google PubSub] visão geral do conector](../../sources/connectors/cloud-storage/google-pubsub.md) para obter mais informações. |
| [!DNL Oracle Object Storage] | Agora é possível conectar [!DNL Oracle Object Storage] a [!DNL Experience Platform] usando a API [!DNL Flow Service] ou a interface do usuário. Consulte a [[!DNL Oracle Object Storage] visão geral do conector](../../sources/connectors/cloud-storage/oracle-object-storage.md) para obter mais informações. |

Para obter informações mais gerais sobre fontes, consulte a [visão geral das fontes](../../sources/home.md).
