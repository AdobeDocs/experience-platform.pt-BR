---
title: Notas de versão da Adobe Experience Platform de fevereiro de 2021
description: As notas de versão de fevereiro de 2021 do Adobe Experience Platform.
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

Novos recursos na Adobe Experience Platform:

- [(Beta) Painéis de Controle](#dashboards)

Atualizações dos recursos existentes na Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## (Beta) Painéis de Controle {#dashboards}

O Adobe Experience Platform fornece vários painéis por meio dos quais você pode visualizar informações importantes sobre os dados de sua organização, conforme capturados durante instantâneos diários.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Perfis, segmentos, destinos e painéis de uso de licença (Beta) | **Observação: a funcionalidade Painel está atualmente na versão beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.**<br/><br/> Os painéis fornecem relatórios prontos para uso sobre os dados de sua organização e são criados diretamente no fluxo de trabalho do profissional de marketing na Platform. Esses painéis estão disponíveis sem a necessidade de suporte de TI adicional ou o tempo e esforço que seriam necessários para exportar e processar dados com projeto e implementação adicionais de data warehouse. |

## [!DNL Data Science Workspace] {#dsw}

O Data Science Workspace usa aprendizado de máquina e inteligência artificial para criar insights a partir de seus dados. Integrado à Adobe Experience Platform, o Data Science Workspace ajuda a fazer previsões usando seu conteúdo e ativos de dados nas soluções da Adobe.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Notebook JupyterLab EDA | O notebook Python para análise exploratória de dados (EDA) agora está disponível em Jupyterlab. Esse notebook foi projetado para ajudá-lo a descobrir padrões de dados, verificar a integridade dos dados e resumir os dados relevantes para modelos preditivos. Veja o tutorial sobre [exploração de dados baseados na web para modelos preditivos](../../data-science-workspace/jupyterlab/eda-notebook.md) para obter mais informações. |

Para obter informações mais gerais sobre o Data Science Workspace, consulte o [Visão geral do Espaço de trabalho de ciência de dados](../../data-science-workspace/home.md).

## [!DNL Dataflows] {#dataflows}

No Adobe Experience Platform, os dados são assimilados de uma grande variedade de fontes, analisados no Experience Platform e ativados para uma grande variedade de destinos. O Platform facilita o processo de rastreamento desse fluxo de dados potencialmente não linear, fornecendo transparência aos fluxos de dados.

Os fluxos de dados são uma representação de trabalhos de dados que movem os dados pela Plataforma. Esses fluxos de dados são configurados em diferentes serviços, ajudando a mover dados dos conectores de origem para os conjuntos de dados de destino, onde são utilizados pelo [!DNL Identity Service] e [!DNL Real-Time Customer Profile] antes de ser ativada para [!DNL Destinations].

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Novo painel de monitoramento | Agora você pode usar o painel de monitoramento para transparência entre serviços e insights acionáveis para assimilações de dados de origem. O novo painel de monitoramento fornece uma visualização abrangente dos dados processados do [!DNL Data Lake] para [!DNL Identity Service] e para [!DNL Profile], enquanto também permite monitorar as taxas de assimilação, os sucessos e as falhas. Veja o tutorial sobre [monitoramento de fluxos de dados de origem na interface do](../../dataflows/ui/monitor-sources.md) para obter mais informações. |

Para obter informações mais gerais sobre fluxos de dados, consulte o [visão geral dos fluxos de dados](../../dataflows/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, publicidade direcionada e muitos outros casos de uso.

**Novos destinos**

| Destino | Descrição |
| ----------- | ----------- |
| [[!DNL LinkedIn Matched Audiences]](../../destinations/catalog/social/linkedin.md) | A variável [!DNL LinkedIn Matched Audiences] A conexão do permite ativar públicos-alvo na [!DNL LinkedIn] plataforma social. |

Para obter informações mais gerais sobre destinos, consulte o [visão geral dos destinos](../../destinations/home.md).

## [!DNL Experience Data Model (XDM) System] {#xdm}

A normalização e a interoperabilidade são conceitos fundamentais [!DNL Experience Platform]. [!DNL Experience Data Model] O (XDM), orientado pelo Adobe, é um esforço para padronizar os dados de experiência do cliente e definir esquemas para o gerenciamento da experiência do cliente.

O XDM é uma especificação documentada publicamente projetada para melhorar o potencial das experiências digitais. Ele fornece estruturas e definições comuns para que qualquer aplicativo se comunique com os serviços na Adobe Experience Platform. Seguindo os padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum, fornecendo insights de maneira mais rápida e integrada. Você pode obter insights valiosos das ações do cliente, definir públicos do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Interface de pesquisa atualizada | Os recursos de pesquisa aprimorados agora estão disponíveis no [!UICONTROL Procurar] na guia [!UICONTROL Esquemas] espaço de trabalho e a caixa de diálogo de seleção do grupo de campos de esquema na [!DNL Schema Editor].<br><br>Ao pesquisar por um termo anteriormente, os resultados incluiriam apenas recursos XDM cujo nome correspondesse à consulta de pesquisa. Agora, além dos recursos cujo nome corresponde à consulta, os recursos que contêm atributos individuais que correspondem ao termo também serão incluídos. Isso permite pesquisar recursos XDM com base nos atributos que eles contêm, em vez de pelo nome do recurso.<br><br>Consulte os documentos em [exploração de recursos XDM](../../xdm/ui/explore.md) e [gerenciamento de esquemas](../../xdm/ui/resources/schemas.md) na interface para obter mais informações. |

Para obter informações mais gerais sobre o XDM, consulte o [Visão geral do sistema XDM](../../xdm/home.md).

## [!DNL Identity Service] {#identity}

Para fornecer experiências digitais relevantes, é necessário ter uma compreensão completa do cliente. Isso se torna mais difícil quando os dados do cliente são fragmentados em sistemas diferentes, fazendo com que cada cliente individual pareça ter várias &quot;identidades&quot;.

Adobe Experience Platform [!DNL Identity Service] O ajuda você a obter uma melhor visualização do cliente e do comportamento dele, unindo identidades em dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e impactantes em tempo real.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Visualizador de gráficos de identidade | O visualizador de gráficos de identidade permite validar e visualizar identidades que são compiladas na interface do usuário, permitindo uma depuração e transparência aprimoradas. Consulte a [documento do visualizador de gráficos de identidade](../../identity-service/ui/identity-graph-viewer.md) para obter mais informações. |

Para obter informações mais gerais sobre [!DNL Identity Service], consulte o [Visão geral do serviço de identidade](../../identity-service/home.md).

## Perfil do cliente em tempo real {#profile}

O Adobe Experience Platform permite gerar experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde e quando eles interagem com sua marca. Com o Perfil do cliente em tempo real, você pode ter uma visualização integral de cada cliente individual, combinando dados de vários canais, inclusive dados online, offline, de CRM e de terceiros. [!DNL Profile] O permite consolidar os dados do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Atributos computados (Alfa) | ***Observação: no momento, essa funcionalidade está em alfa e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.*** <br/><br/>Os atributos computados são funções usadas para agregar dados no nível do evento em atributos no nível do perfil. Você pode usar as agregações na segmentação, ativação e personalização. Alguns exemplos dessas funções incluem count, sum, average, min, max, true/false. Atualmente, os atributos computados estão disponíveis somente por meio da API. Para obter mais informações, consulte [visão geral dos atributos computados](../../profile/computed-attributes/overview.md). |

Para obter mais informações sobre o Perfil do cliente em tempo real, incluindo tutoriais e práticas recomendadas para trabalhar com a [!DNL Profile] dados, comece lendo o [Visão geral do Perfil do cliente em tempo real](../../profile/home.md).

## [!DNL Sources] {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir tempos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Novas fontes**

| Recurso | Descrição |
| --- | --- |
| [!DNL Google PubSub] | Agora você pode se conectar [!DNL Google PubSub] para [!DNL Experience Platform] usando o [!DNL Flow Service] API ou a interface do usuário. Consulte a [[!DNL Google PubSub] visão geral do conector](../../sources/connectors/cloud-storage/google-pubsub.md) para obter mais informações. |
| [!DNL Oracle Object Storage] | Agora você pode se conectar [!DNL Oracle Object Storage] para [!DNL Experience Platform] usando o [!DNL Flow Service] API ou a interface do usuário. Consulte a [[!DNL Oracle Object Storage] visão geral do conector](../../sources/connectors/cloud-storage/oracle-object-storage.md) para obter mais informações. |

Para obter informações mais gerais sobre fontes, consulte [visão geral das origens](../../sources/home.md).
