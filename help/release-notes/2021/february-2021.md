---
title: Notas de versão da Adobe Experience Platform fevereiro de 2021
description: As notas de versão de fevereiro de 2021 para o Adobe Experience Platform.
doc-type: release notes
last-update: February 24, 2021
author: ens70167
exl-id: 8c3142af-4021-4f7e-acbd-c5277dd188d1
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 6%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 24 de fevereiro de 2021**

Novos recursos no Adobe Experience Platform:

- [Painéis (Beta)](#dashboards)

Atualizações dos recursos existentes na Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Painéis (Beta) {#dashboards}

O Adobe Experience Platform fornece vários painéis através dos quais você pode visualizar informações importantes sobre os dados de sua organização, conforme capturados durante os instantâneos diários.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Perfis, segmentos, destinos e painéis de uso de licença (Beta) | **Observação: A funcionalidade do painel está atualmente na versão beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.**<br/><br/> Os painéis fornecem relatórios prontos sobre os dados de sua organização e são incorporados diretamente ao fluxo de trabalho do profissional de marketing no Platform. Esses painéis estão disponíveis sem a necessidade de suporte adicional de TI ou o tempo e esforço necessários para exportar e processar dados com o projeto e a implementação adicionais do data warehouse. |

## [!DNL Data Science Workspace] {#dsw}

O Data Science Workspace usa o aprendizado de máquina e a inteligência artificial para criar insights de seus dados. Integrado ao Adobe Experience Platform, o Data Science Workspace ajuda você a fazer previsões usando seus ativos de conteúdo e dados nas soluções de Adobe.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Notebook JupyterLab EDA | O notebook de Python da EDA (análise de dados exploratória) agora está disponível em Jupyterlab. Este notebook foi projetado para ajudá-lo a descobrir padrões em dados, verificar a integridade dos dados e resumir os dados relevantes para modelos preditivos. Veja o tutorial em [explorar dados baseados na Web para modelos preditivos](../../data-science-workspace/jupyterlab/eda-notebook.md) para obter mais informações. |

Para obter informações mais gerais sobre a Data Science Workspace, consulte [Visão geral do Data Science Workspace](../../data-science-workspace/home.md).

## [!DNL Dataflows] {#dataflows}

No Adobe Experience Platform, os dados são assimilados de uma grande variedade de fontes, analisados no Experience Platform, e ativados para uma grande variedade de destinos. A Platform facilita o processo de rastreamento desse fluxo de dados potencialmente não linear ao fornecer transparência com fluxos de dados.

Os fluxos de dados são uma representação de trabalhos de dados que movem os dados pela Plataforma. Esses fluxos de dados são configurados em diferentes serviços, ajudando a mover dados de conectores de origem para conjuntos de dados de destino, onde são utilizados por [!DNL Identity Service] e [!DNL Real-Time Customer Profile] antes de ser ativado para [!DNL Destinations].

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Novo painel de monitoramento | Agora você pode usar o painel de monitoramento para transparência entre serviços e insights acionáveis para assimilações de dados de origem. O novo painel de monitoramento fornece uma visão abrangente dos dados processados do [!DNL Data Lake] para [!DNL Identity Service] e [!DNL Profile], além de permitir que você monitore taxas de ingestão, sucessos e falhas. Veja o tutorial em [monitoramento de fluxos de dados de origem na interface do usuário](../../dataflows/ui/monitor-sources.md) para obter mais informações. |

Para obter informações mais gerais sobre fluxos de dados, consulte [visão geral dos fluxos de dados](../../dataflows/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, anúncios direcionados e muitos outros casos de uso.

**Novos destinos**

| Destino | Descrição |
| ----------- | ----------- |
| [[!DNL LinkedIn Matched Audiences]](../../destinations/catalog/social/linkedin.md) | O [!DNL LinkedIn Matched Audiences] permite ativar públicos-alvo na [!DNL LinkedIn] plataforma social. |

Para obter informações mais gerais sobre destinos, consulte [visão geral dos destinos](../../destinations/home.md).

## [!DNL Experience Data Model (XDM) System] {#xdm}

A normalização e a interoperabilidade são conceitos-chave subjacentes [!DNL Experience Platform]. [!DNL Experience Data Model] O (XDM), impulsionado pelo Adobe, é um esforço para padronizar os dados de experiência do cliente e definir esquemas para o gerenciamento da experiência do cliente.

O XDM é uma especificação publicamente documentada projetada para melhorar o poder das experiências digitais. Fornece estruturas e definições comuns para qualquer aplicativo se comunicar com serviços no Adobe Experience Platform. Ao seguir os padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum, fornecendo insights de forma mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Interface do usuário de pesquisa atualizada | Os recursos de pesquisa aprimorados agora estão disponíveis no [!UICONTROL Procurar] na guia no [!UICONTROL Esquemas] espaço de trabalho e a caixa de diálogo de seleção do grupo de campos de esquema na [!DNL Schema Editor].<br><br>Ao pesquisar um termo anteriormente, os resultados incluiriam apenas recursos XDM cujo nome corresponda à consulta de pesquisa. Agora, além de recursos cujo nome corresponda ao query, os recursos contendo atributos individuais que correspondem ao termo também serão incluídos. Isso permite procurar recursos XDM com base nos atributos que eles contêm, em vez de por nome de recurso.<br><br>Veja os documentos em [exploração de recursos XDM](../../xdm/ui/explore.md) e [gerenciamento de schemas](../../xdm/ui/resources/schemas.md) na interface do usuário do para obter mais informações. |

Para obter informações mais gerais sobre o XDM, consulte [Visão geral do sistema XDM](../../xdm/home.md).

## [!DNL Identity Service] {#identity}

Fornecer experiências digitais relevantes requer ter uma compreensão completa do cliente. Isso fica mais difícil quando os dados do cliente são fragmentados em sistemas diferentes, fazendo com que cada cliente individual pareça ter várias &quot;identidades&quot;.

Adobe Experience Platform [!DNL Identity Service] O ajuda você a obter uma melhor visão de seu cliente e de seu comportamento ao unir identidades em dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e impactantes em tempo real.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Visualizador de gráfico de identidade | O visualizador de gráficos de identidade permite validar e visualizar identidades que são unidas na interface do usuário, permitindo uma depuração e transparência aprimoradas. Consulte a [documento do visualizador de gráficos de identidade](../../identity-service/ui/identity-graph-viewer.md) para obter mais informações. |

Para obter informações mais gerais sobre [!DNL Identity Service], consulte o [Visão geral do Serviço de identidade](../../identity-service/home.md).

## Perfil do cliente em tempo real {#profile}

O Adobe Experience Platform permite que você conduza experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagirem com sua marca. Com o Perfil do cliente em tempo real, você pode ver uma visualização holística de cada cliente individual que combina dados de vários canais, incluindo dados online, offline, CRM e de terceiros. [!DNL Profile] O permite consolidar os dados do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Atributos calculados (Alfa) | ***Observação: Essa funcionalidade está atualmente em alfa e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.*** <br/><br/>Atributos calculados são funções usadas para agregar dados no nível do evento em atributos no nível do perfil. Em seguida, você pode usar as agregações na segmentação, ativação e personalização. Alguns exemplos dessas funções incluem contagem, soma, média, mín, máx, true/false. Atributos calculados estão disponíveis no momento somente por API. Para obter mais informações, consulte o [visão geral dos atributos calculados](../../profile/computed-attributes/overview.md). |

Para obter mais informações sobre o Perfil do cliente em tempo real, incluindo tutoriais e práticas recomendadas para trabalhar com a [!DNL Profile] , comece lendo o [Visão geral do perfil do cliente em tempo real](../../profile/home.md).

## [!DNL Sources] {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos de Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Novas fontes**

| Recurso | Descrição |
| --- | --- |
| [!DNL Google PubSub] | Agora você pode se conectar [!DNL Google PubSub] para [!DNL Experience Platform] usando o [!DNL Flow Service] API ou a interface do usuário. Consulte a [[!DNL Google PubSub] visão geral do conector](../../sources/connectors/cloud-storage/google-pubsub.md) para obter mais informações. |
| [!DNL Oracle Object Storage] | Agora você pode se conectar [!DNL Oracle Object Storage] para [!DNL Experience Platform] usando o [!DNL Flow Service] API ou a interface do usuário. Consulte a [[!DNL Oracle Object Storage] visão geral do conector](../../sources/connectors/cloud-storage/oracle-object-storage.md) para obter mais informações. |

Para obter informações mais gerais sobre fontes, consulte [visão geral das fontes](../../sources/home.md).
