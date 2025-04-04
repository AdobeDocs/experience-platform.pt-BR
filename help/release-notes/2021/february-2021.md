---
title: Notas da versão de fevereiro de 2021 da Adobe Experience Platform
description: Notas da versão de fevereiro de 2021 da Adobe Experience Platform.
doc-type: release notes
last-update: February 24, 2021
author: ens70167
exl-id: 8c3142af-4021-4f7e-acbd-c5277dd188d1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 22%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: quinta-feira, 24 de fevereiro de 2021**

Novos recursos na Adobe Experience Platform:

- [Painéis do (Beta)](#dashboards)

Atualizações dos recursos já existentes na Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Painéis do (Beta) {#dashboards}

O Adobe Experience Platform fornece vários painéis por meio dos quais você pode exibir informações importantes sobre os dados de sua organização, conforme capturados durante os instantâneos diários.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Perfis, segmentos, destinos e painéis de uso de licença (Beta) | **Observação: a funcionalidade do painel está atualmente na versão beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.**<br/><br/> Os painéis fornecem relatórios prontos para uso sobre os dados da sua organização e são criados diretamente no fluxo de trabalho do profissional de marketing no Experience Platform. Esses painéis estão disponíveis sem a necessidade de suporte de TI adicional ou o tempo e esforço que seriam necessários para exportar e processar dados com projeto e implementação adicionais de data warehouse. |

## [!DNL Data Science Workspace] {#dsw}

O Data Science Workspace usa aprendizagem de máquina e inteligência artificial para criar insights a partir de seus dados. Integrado à Adobe Experience Platform, o Data Science Workspace ajuda a fazer previsões usando seus ativos de conteúdo e dados nas soluções da Adobe.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Notebook JupyterLab EDA | O notebook Python para análise exploratória de dados (EDA) agora está disponível em Jupyterlab. Esse notebook foi projetado para ajudá-lo a descobrir padrões de dados, verificar a integridade dos dados e resumir os dados relevantes para modelos preditivos. Consulte o tutorial em [exploração de dados baseados na Web para modelos preditivos](../../data-science-workspace/jupyterlab/eda-notebook.md) para obter mais informações. |

Para obter mais informações sobre o Data Science Workspace, consulte a [visão geral do Data Science Workspace](../../data-science-workspace/home.md).

## [!DNL Dataflows] {#dataflows}

No Adobe Experience Platform, os dados são assimilados de uma grande variedade de fontes, analisados no Experience Platform e ativados para uma grande variedade de destinos. O Experience Platform facilita o processo de rastreamento desse fluxo de dados potencialmente não linear, fornecendo transparência aos fluxos de dados.

Os fluxos de dados são uma representação de trabalhos de dados que movem dados pelo Experience Platform. Esses fluxos de dados são configurados em diferentes serviços, ajudando a mover dados dos conectores de origem para os conjuntos de dados de destino, nos quais eles são utilizados por [!DNL Identity Service] e [!DNL Real-Time Customer Profile] antes de serem ativados para [!DNL Destinations].

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Novo painel de monitoramento | Agora você pode usar o painel de monitoramento para transparência entre serviços e insights acionáveis para assimilações de dados de origem. O novo painel de monitoramento fornece uma visão abrangente dos dados processados de [!DNL Data Lake] a [!DNL Identity Service] e a [!DNL Profile], além de permitir que você monitore as taxas de assimilação, os sucessos e as falhas. Consulte o tutorial sobre [monitoramento de fluxos de dados de origem na interface](../../dataflows/ui/monitor-sources.md) para obter mais informações. |

Para obter mais informações sobre fluxos de dados, consulte a [visão geral sobre fluxos de dados](../../dataflows/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Novos destinos**

| Destino | Descrição |
| ----------- | ----------- |
| [[!DNL LinkedIn Matched Audiences]](../../destinations/catalog/social/linkedin.md) | A conexão [!DNL LinkedIn Matched Audiences] permite ativar públicos na plataforma social [!DNL LinkedIn]. |

Para obter informações mais gerais sobre destinos, consulte a [visão geral de destinos](../../destinations/home.md).

## [!DNL Experience Data Model (XDM) System] {#xdm}

A padronização e a interoperabilidade são os principais conceitos por trás do [!DNL Experience Platform]. O [!DNL Experience Data Model] (XDM), orientado pela Adobe, é um esforço para padronizar os dados de experiência do cliente e definir esquemas para o gerenciamento da experiência do cliente.

O XDM é uma especificação documentada publicamente projetada para melhorar o potencial das experiências digitais. Ele fornece estruturas e definições comuns para que qualquer aplicativo se comunique com os serviços na Adobe Experience Platform. Seguindo os padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum, fornecendo insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Interface de pesquisa atualizada | Os recursos de pesquisa aprimorados agora estão disponíveis na guia [!UICONTROL Procurar] no espaço de trabalho [!UICONTROL Esquemas] e na caixa de diálogo de seleção do grupo de campos de esquema no [!DNL Schema Editor].<br><br>Ao pesquisar por um termo anteriormente, os resultados incluiriam apenas recursos XDM cujo nome correspondesse à consulta de pesquisa. Agora, além dos recursos cujo nome corresponde à consulta, os recursos que contêm atributos individuais que correspondem ao termo também serão incluídos. Isso permite pesquisar recursos XDM com base nos atributos que eles contêm, em vez de pelo nome do recurso.<br><br>Consulte os documentos em [explorando recursos XDM](../../xdm/ui/explore.md) e [gerenciando esquemas](../../xdm/ui/resources/schemas.md) na interface do usuário para obter mais informações. |

Para obter informações mais gerais sobre o XDM, consulte a [visão geral do sistema XDM](../../xdm/home.md).

## [!DNL Identity Service] {#identity}

Para fornecer experiências digitais relevantes, é necessário ter uma compreensão completa do cliente. Isso se torna mais difícil quando os dados do cliente são fragmentados em sistemas diferentes, fazendo com que cada cliente individual pareça ter várias &quot;identidades&quot;.

O Adobe Experience Platform [!DNL Identity Service] ajuda você a ter uma melhor visão do seu cliente e do comportamento dele unindo identidades de vários dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e impactantes em tempo real.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Visualizador de gráficos de identidade | O visualizador de gráficos de identidade permite validar e visualizar identidades que são compiladas na interface do usuário, permitindo uma depuração e transparência aprimoradas. Consulte o [documento do visualizador de gráficos de identidade](../../identity-service/features/identity-graph-viewer.md) para obter mais informações. |

Para obter informações mais gerais sobre [!DNL Identity Service], consulte a [visão geral do Serviço de Identidade](../../identity-service/home.md).

## Perfil do cliente em tempo real {#profile}

A Adobe Experience Platform permite gerar experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagem com sua marca. Com o Perfil do cliente em tempo real, é possível ter uma visão integral de cada cliente ao combinar dados de vários canais, incluindo online, offline, CRM e de terceiros. O [!DNL Profile] permite consolidar os dados do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Atributos computados (Alpha) | ***Observação: esta funcionalidade está atualmente em alfa e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.*** <br/><br/>Atributos computados são funções usadas para agregar dados de nível de evento em atributos de nível de perfil. Você pode usar as agregações na segmentação, ativação e personalização. Alguns exemplos dessas funções incluem count, sum, average, min, max, true/false. Atualmente, os atributos computados estão disponíveis somente por meio da API. |

Para obter mais informações sobre o Perfil do cliente em tempo real, incluindo tutoriais e práticas recomendadas para trabalhar com dados do [!DNL Profile], comece lendo a [Visão geral do Perfil do cliente em tempo real](../../profile/home.md).

## [!DNL Sources] {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, estruturar, rotular e aprimorar esses dados usando os serviços da Experience Platform. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Novas fontes**

| Recurso | Descrição |
| --- | --- |
| [!DNL Google PubSub] | Agora você pode conectar [!DNL Google PubSub] a [!DNL Experience Platform] usando a API [!DNL Flow Service] ou a interface do usuário. Consulte a [[!DNL Google PubSub] visão geral do conector](../../sources/connectors/cloud-storage/google-pubsub.md) para obter mais informações. |
| [!DNL Oracle Object Storage] | Agora você pode conectar [!DNL Oracle Object Storage] a [!DNL Experience Platform] usando a API [!DNL Flow Service] ou a interface do usuário. Consulte a [[!DNL Oracle Object Storage] visão geral do conector](../../sources/connectors/cloud-storage/oracle-object-storage.md) para obter mais informações. |

Para obter informações mais gerais sobre fontes, consulte a [visão geral das fontes](../../sources/home.md).
