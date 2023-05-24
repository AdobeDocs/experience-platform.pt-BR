---
title: Notas de versão da Adobe Experience Platform de março de 2023
description: As notas de versão de março de 2023 do Adobe Experience Platform.
exl-id: 3f4d764a-77cd-4e4a-ae11-e97a23006a53
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '2206'
ht-degree: 4%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 29 de março de 2023**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Painéis](#dashboards)
- [Coleta de dados](#data-collection)
- [Preparação de dados](#data-prep)
- [Destinos](#destinations)
- [Experience Data Model](#xdm)
- [Serviço de query](#query-service)
- [Real-Time Customer Data Platform B2B Edition](#b2b)
- [Serviço de segmentação](#segmentation)
- [Fontes](#sources)

## Painéis {#dashboards}

O Adobe Experience Platform fornece vários painéis por meio dos quais você pode visualizar insights importantes sobre os dados de sua organização, conforme capturados durante instantâneos diários.

**Recursos novos ou atualizados** {#dashboards-new-updated-features}

| Recurso | Descrição |
| --- | --- |
| Painéis definidos pelo usuário | Agora você pode **valores de atributo de exemplo** antes de adicionar um atributo a um widget no widget de painéis definido pelo usuário. Alguns exemplos de valores dessa coluna de atributo estão disponíveis para atributos individuais ao criar um widget.<br>Agora você pode **trocar os eixos X e Y** no widget com o botão trocar eixo. Isso economiza tempo e fornece uma experiência mais ergonômica ao adicionar atributos aos seus widgets. Isso evita a necessidade de localizar os dois atributos novamente no painel Atributos.<br> Agora você pode **alterar o local e o título da legenda** em seus widgets. Depois que uma legenda estiver presente em um widget, você pode realocá-la em qualquer lugar ao redor do gráfico e renomear o título da legenda, como é possível com rótulos de eixo e o título do widget. |

{style="table-layout:auto"}

Para obter mais informações sobre painéis, incluindo como conceder permissões de acesso e criar widgets personalizados, comece lendo o [visão geral dos painéis](../../dashboards/home.md).

## Coleta de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente do lado do cliente e enviá-los à Rede de borda da Adobe Experience Platform, onde eles podem ser enriquecidos, transformados e distribuídos para destinos Adobe ou não Adobe.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Novo fluxo de trabalho de início rápido para a API de meta conversões (Beta) | Acesse os novos workflows de início rápido em &quot;Introdução&quot; na tela inicial da Coleção de dados! A variável [fluxo de trabalho de início rápido para a API de meta conversões](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) O permite que os clientes coletem e encaminhem rapidamente os dados do evento, do lado do servidor para o Meta, para conversões de anúncios em apenas algumas etapas simples. |
| Novo fluxo de trabalho de início rápido para o SDK móvel (Beta) | Acesse os novos workflows de início rápido em &quot;Introdução&quot; na tela inicial da Coleção de dados! A variável [fluxo de trabalho de início rápido para o SDK móvel](https://developer.adobe.com/client-sdks/documentation/) O permite implementar rapidamente o SDK móvel e validar eventos móveis básicos em apenas algumas etapas simples. |
| [!DNL Braze] extensão de encaminhamento de eventos | A variável [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) A extensão de encaminhamento de eventos permite aproveitar os dados capturados na Rede de borda da Adobe Experience Platform e enviá-los para o [!DNL Braze] na forma de eventos do lado do servidor usando o [!DNL Braze] APIs de rastreamento de usuários. |
| [!DNL Epsilon] extensão de encaminhamento de eventos | A variável [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/overview.html) A extensão do permite aproveitar o encaminhamento de eventos para capturar informações de eventos na Adobe Experience Platform Edge Network e enviá-las para o [!DNL Epsilon] usando o [!DNL Epsilon] API de evento. |
| [!DNL Mixpanel] extensão de encaminhamento de eventos | A variável [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) Essa extensão permite que os clientes aproveitem o encaminhamento de eventos para capturar informações de eventos na Adobe Experience Platform Edge Network e enviá-las para o Mixpanel usando a API Rastrear eventos. |

{style="table-layout:auto"}

## Preparação de dados {#data-prep}

O Preparo de dados permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Disponibilidade geral da filtragem para dados do Adobe Analytics | Agora você pode usar as funcionalidades de Preparo de dados para aplicar regras e condições a fim de filtrar os dados do Analytics antes de assimilá-los no Perfil do cliente em tempo real. Para obter mais informações, leia o guia em [filtragem de dados do Analytics para assimilação de perfis](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile). |
| Novas funções para codificar e decodificar sequências de caracteres de URL | <ul><li>A variável `get_url_encoded` A função pega uma URL como entrada e substitui ou codifica caracteres especiais por caracteres ASCII.</li><li>A variável `get_url_decoded` A função pega uma URL como entrada e decodifica caracteres ASCII em caracteres especiais.</li></ul> Para obter mais informações, leia a [Guia de funções do Preparo de dados](../../data-prep/functions.md). Para obter uma lista abrangente de caracteres reservados e seus caracteres codificados correspondentes, leia o guia em [caracteres especiais](../../data-prep/functions.md#special-characters). |

Para obter mais informações sobre o Preparo de dados, leia o [Visão geral do Preparo de dados](../../data-prep/home.md).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, publicidade direcionada e muitos outros casos de uso.

**Novos destinos** {#new-destinations}

| Destino | Descrição |
| ----------- | ----------- |
| [[!DNL Adobe Commerce] conexão GA](../../destinations/catalog/personalization/adobe-commerce.md) | A variável [!DNL Adobe Commerce] o conector de destino (agora disponível no geral) permite selecionar um ou mais públicos-alvo da Real-Time CDP para ativar no [!DNL Adobe Commerce] para fornecer uma experiência personalizada dinâmica aos seus compradores. |
| [[!DNL Snap Inc] conexão GA](../../destinations/catalog/advertising/snap-inc.md) | A variável [!DNL Snap Inc] o conector de destino (agora disponível no geral) permite que os profissionais de marketing importem segmentos de usuários criados no Experience Platform para o [!DNL Snapchat Ads] e usá-los para direcionar seus anúncios. |
| [(API) Conexão Oracle Eloqua](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | Use a conexão baseada em API para [!DNL Oracle Eloqua] planejar e executar campanhas enquanto fornece uma experiência personalizada do cliente para seus clientes potenciais em [!DNL Oracle Eloqua]. |
| [(Beta) [!DNL Amazon Ads] conexão](../../destinations/catalog/advertising/amazon-ads.md) | A variável [!DNL Amazon Ads] integração com o Adobe Experience Platform fornece integração pronta para uso para [!DNL Amazon Ads] produtos, incluindo o [!DNL Amazon DSP (ADSP)]. Usar o [!DNL Amazon Ads] no Adobe Experience Platform, os usuários podem definir públicos-alvo do anunciante para direcionamento e ativação no [!DNL Amazon DSP]. |
| [[!DNL Marketo Measure Ultimate] conexão](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] (anteriormente Bizible) fornece aos profissionais de marketing informações sobre quais esforços de marketing são os mais eficientes na geração de receita e na maximização do retorno sobre o investimento para sua empresa. O destino permite que os dados B2B (B2B) fluam do Adobe Experience Platform para [!DNL Marketo Measure]. O cartão só está disponível para [!DNL Marketo Measure Ultimate] clientes. |
| [Conexão com o TikTok](../../destinations/catalog/social/tiktok.md) | Crie públicos-alvo personalizados no TikTok com seus dados para direcionar com suas campanhas de publicidade. |
| [Conexão do Zendesk](../../destinations/catalog/crm/zendesk.md) | Usar este destino para criar e atualizar identidades dentro de um segmento como contatos dentro [!DNL Zendesk]. |

{style="table-layout:auto"}

**Funcionalidade nova ou atualizada** {#destinations-new-updated-functionality}

| Funcionalidade | Descrição |
| ----------- | ----------- |
| Nova permissão de controle de acesso para destinos: [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | A nova permissão oferece aos usuários a capacidade de ativar segmentos para destinos existentes, sem exibir a variável [etapa de mapeamento](../../destinations/ui/activate-batch-profile-destinations.md#mapping). Os usuários podem adicionar e remover segmentos em workflows de ativação, mas não podem adicionar ou remover atributos ou identidades mapeadas. |

{style="table-layout:auto"}

**Correções e aprimoramentos** {#destinations-fixes-and-enhancements}

Estamos lançando uma correção de erros para a criptografia PGP/GPG em destinos baseados em arquivos para a CDP em tempo real. Com essa alteração, os destinos baseados em arquivo que estão usando a criptografia gerarão um nome de arquivo com uma extensão diferente da anterior.

- Extensão atual ao usar criptografia: `filename.csv`
- Extensão futura ao usar criptografia: `filename.csv.gpg`

Para obter informações mais gerais sobre destinos, consulte o [visão geral dos destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Adobe Experience Platform. Seguindo os padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos das ações do cliente, definir públicos do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| CSV para recomendação de esquema | Agora você pode fazer upload de arquivos locais para criar esquemas gerados pelo aprendizado de máquina que eliminam a necessidade de criar manualmente um esquema. No [!UICONTROL Origens] , faça upload de um arquivo CSV de amostra e os algoritmos de aprendizado de máquina do Adobe sugerirão um esquema com base nos campos de destino. Consulte a [documentação da](../../ingestion/tutorials/map-csv/recommendations.md) para obter mais informações.&quot; |

{style="table-layout:auto"}

**Novos componentes XDM**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Classe | [[!UICONTROL Item de oferta]](https://github.com/adobe/xdm/pull/1678/files) | Classe que representa uma Oferta. |
| Classe | [[!UICONTROL Item de decisão]](https://github.com/adobe/xdm/pull/1678/files) | Um item que pode ser sujeito a decisão. A saída de um processo de decisão é um ou mais itens de decisão. |
| Classe | [[!UICONTROL Tempo limite do servidor de sessão de mídia]](https://github.com/adobe/xdm/pull/1676/files) | Isso indica o tempo, em segundos, decorrido entre a última interação conhecida do usuário e o momento em que a sessão foi encerrada. |
| Grupo de campos | [[!UICONTROL Atributos computados do perfil XDM]](https://github.com/adobe/xdm/pull/1686/files) | Isso adiciona atributos computados dos serviços internos da Adobe aos dados de entrada do cliente. Isso não deve ser usado pelos clientes para assimilar dados. |
| Tipo de dados | [[!UICONTROL Item de reembolso]](https://github.com/adobe/xdm/pull/1685/files) | Indica se um reembolso está associado a um pedido e define o tipo de reembolso, o valor e a moeda associada. |
| Tipo de dados | [[!UICONTROL Dados da categoria]](https://github.com/adobe/xdm/pull/1677/files) | Esse novo tipo de dados representa a categoria de um produto. |
| Esquema | [[!UICONTROL Campos de classificação do Adobe Target]](https://github.com/adobe/xdm/pull/1682/files) | Um novo esquema XDM foi criado para conjuntos de dados de Classificação de destino. Ele contém um conjunto de campos de metadados que classificam as atividades e experiências do Target. |

{style="table-layout:auto"}

**Componentes XDM atualizados**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Grupo de campos | [[!UICONTROL Detalhes do componente de conteúdo]](https://github.com/adobe/xdm/pull/1674/files) | `uri-reference` foi removido de [!UICONTROL Detalhes do componente de conteúdo] |
| Grupo de campos | [[!UICONTROL Tags de entidade do AJO]](https://github.com/adobe/xdm/pull/1672/files) | Adição das tags de entidade do AJO a [!UICONTROL Campos de entidade do AJO], que correspondem a uma Jornada ou Campanha |
| Grupo de campos | (Múltiplos) | Adição de vários campos para [[!UICONTROL Campos Comuns de Evento de Etapa do Journey Orchestration]](https://github.com/adobe/xdm/pull/1671/files) |
| Grupo de campos | (Múltiplos) | [Adição de vários tipos de evento XDM para [!UICONTROL Relatórios de mídia]](https://github.com/adobe/xdm/pull/1670/files). |
| Grupo de campos | [!UICONTROL Evento de alteração do Workfront] | A variável `Full Record` e `Accessor Employee Ids` grupos de campos foram adicionados. |
| Tipo de dados | [[!UICONTROL Item da lista de produtos]](https://github.com/adobe/xdm/pull/1685/files) | A variável [!UICONTROL Valor do reembolso] foi adicionado para indicar o valor reembolsado para o item, se houver. |
| Tipo de dados | [[!UICONTROL Pedido ]](https://github.com/adobe/xdm/pull/1685/files) | [!UICONTROL Lista de Reembolsos] foi adicionado à lista de reembolsos para este pedido. |
| Tipo de dados | [[!UICONTROL Item da lista de produtos ]](https://github.com/adobe/xdm/pull/1677/files) | Categorias de produto foram adicionadas à lista de dados de categoria deste produto. |
| Tipo de dados | [!UICONTROL Informações de detalhes da sessão] | Adição de `pev3` campo de string que [indica o tipo de fluxo de mídia usado para relatórios](https://github.com/adobe/xdm/pull/1676/files). Também foi adicionado o `pccr` indica se um redirecionamento ocorreu. |
| Tipo de dados | [!UICONTROL Lista de Requisições] | Fornece a [propriedades da lista de requisições](https://github.com/adobe/xdm/pull/1675/files). Eles incluem nome, ID e descrição. |
| Tipo de dados | [!UICONTROL Commerce] | A variável [O tipo de dados de comércio foi atualizado](https://github.com/adobe/xdm/pull/1675/files) para incluir `requisitionListOpens`, `requisitionListAdds`, `requisitionListRemovals`, e `requisitionList`. |

{style="table-layout:auto"}

Para obter mais informações sobre o XDM na Platform, leia o [Visão geral do sistema XDM](../../xdm/home.md).

## Serviço de query {#query-service}

O Serviço de consulta permite usar o SQL padrão para consultar dados no Adobe Experience Platform [!DNL Data Lake]. Você pode unir qualquer conjunto de dados do data lake e capturar os resultados da consulta como um novo conjunto de dados para usar em relatórios, no Data Science Workspace ou para assimilação no Perfil do cliente em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Controle de acesso baseado em atributos no armazenamento acelerado | Use o Controle de acesso baseado em atributos com o Data Distiller para definir o controle de acesso em todos os conjuntos de dados no armazenamento acelerado. Isso controla o acesso aos modelos de dados personalizados criados pelos usuários e armazenados em um armazenamento acelerado para alimentar painéis personalizados. |

{style="table-layout:auto"}

Para obter mais informações sobre os Serviços de consulta, consulte [Visão geral do Serviço de consulta](../../query-service/home.md).

## Real-Time Customer Data Platform B2B Edition {#b2b}

Criado no Real-time Customer Data Platform (Real-Time CDP), o Real-Time CDP B2B Edition foi desenvolvido especificamente para profissionais de marketing que operam em um modelo de serviço business-to-business. Ele reúne dados de várias fontes e os combina em uma única visualização de pessoas e perfis de conta. Esses dados unificados permitem que os profissionais de marketing direcionem públicos específicos com precisão e envolvam esses públicos em todos os canais disponíveis.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Correção de erros | Para fornecer uma representação mais precisa dos perfis em seu sistema, o sistema não inclui mais perfis internos na contagem total de perfis ou na métrica de público-alvo endereçável do Real-time Customer Data Platform B2B Edition. A partir de hoje, você poderá observar uma queda única na métrica de contagem total de perfis/público-alvo endereçável. Nenhum de seus dados foi apagado, isso é apenas uma alteração na contagem. Entre em contato com o executivo da sua Adobe para esclarecer dúvidas que você possa ter |

{style="table-layout:auto"}

Para saber mais sobre o Real-Time CDP B2B Edition, leia o [Visão geral da Real-Time CDP B2B Edition](../../rtcdp/overview.md).

## Serviço de segmentação {#segmentation}

[!DNL Segmentation Service] O define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo comercializável de pessoas na sua base de clientes. Os segmentos podem ser baseados em dados de registro (como informações demográficas) ou eventos de séries temporais que representam interações do cliente com sua marca.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Métricas de perfil | Para fornecer uma representação mais precisa das métricas de perfil, as métricas de detalhamento de associação e churn estão sendo combinadas e agora são calculadas em um período de 24 horas. Mais informações disponíveis na [Guia da interface de segmentação](../../segmentation/ui/overview.md#browse) |

{style="table-layout:auto"}

Para obter mais informações sobre [!DNL Segmentation Service], consulte o [Visão geral da segmentação](../../segmentation/home.md).

## Fontes {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e permite estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir tempos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Disponibilidade beta de [!DNL Chatlio] | A variável [!DNL Chatlio] a fonte agora está disponível na versão beta. Use o [!DNL Chatlio] origem para transmitir seu [!DNL Chatlio] dados de eventos para o Experience Platform. Para obter mais informações, leia a [[!DNL Chatlio] visão geral](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| Disponibilidade beta de [!DNL Customer.io] | A variável [!DNL Customer.io] a fonte agora está disponível na versão beta. Use o [!DNL Customer.io] fonte para transmitir os dados dos eventos do cliente para o Experience Platform. Para obter mais informações, leia a [[!DNL Customer.io] visão geral](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| Disponibilidade beta de [!DNL Pendo] | A variável [!DNL Pendo] a fonte agora está disponível na versão beta. Use o [!DNL Pendo] fonte para transmitir os dados de análise do produto para o Experience Platform. Para obter mais informações, leia a [[!DNL Pendo] visão geral](../../sources/connectors/analytics/pendo-webhook.md). |
| Suporte para fluxos de dados de rascunho | Agora você pode usar a API do Serviço de fluxo para definir seus fluxos de dados para um estado de rascunho. Os fluxos de dados rascunhados podem ser atualizados e publicados posteriormente com novas informações. Para obter mais informações, leia o guia em [definição dos fluxos de dados de origens como rascunhos](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

Para saber mais sobre fontes, leia o [visão geral das origens](../../sources/home.md).
