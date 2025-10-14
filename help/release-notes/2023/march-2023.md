---
title: Notas da versão de março de 2023 da Adobe Experience Platform
description: As notas da versão de março de 2023 da Adobe Experience Platform.
exl-id: 3f4d764a-77cd-4e4a-ae11-e97a23006a53
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2081'
ht-degree: 97%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 29 de março de 2023**

Atualizações dos recursos já existentes na Adobe Experience Platform:

- [Painéis](#dashboards)
- [Coleção de dados](#data-collection)
- [Preparação de dados](#data-prep)
- [Destinos](#destinations)
- [Experience Data Model](#xdm)
- [Query Service](#query-service)
- [Real-Time Customer Data Platform B2B Edition](#b2b)
- [Serviço de segmentação](#segmentation)
- [Origens](#sources)

## Painéis {#dashboards}

A Adobe Experience Platform fornece vários painéis para você visualizar insights importantes sobre os dados de sua organização, que são capturados por instantâneos diários.

**Recursos novos ou atualizados** {#dashboards-new-updated-features}

| Recurso | Descrição |
| --- | --- |
| Painéis definidos pelo usuário | Agora você pode **testar valores de atributo** antes de adicionar um atributo a um widget no criador de widgets dos painéis definidos pelo usuário. Alguns exemplos de valores dessa coluna de atributo estão disponíveis para atributos individuais ao criar um widget.<br>Agora você pode **trocar os eixos X e Y** no widget com o botão de trocar eixo. Assim você economiza tempo e tem uma experiência mais ergonômica ao adicionar atributos aos seus widgets. Isso evita a necessidade de localizar os atributos novamente no painel de atributos.<br> Agora você pode **alterar o local e o título da legenda** em seus widgets. Depois que uma legenda estiver presente em um widget, você pode realocá-la para qualquer lugar do gráfico e renomear o título, da mesma maneira que os rótulos de eixo e o título do widget. |

{style="table-layout:auto"}

Para obter mais informações sobre painéis, incluindo como conceder permissões de acesso e criar widgets personalizados, comece lendo a [visão geral dos painéis](../../dashboards/home.md).

## Coleção de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados da experiência do cliente e enviá-los à Rede de borda da Adobe Experience Platform, onde eles podem ser enriquecidos, transformados e distribuídos para destinos da Adobe ou de outras empresas.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Novo fluxo de trabalho de início rápido para a API de conversões da Meta (Beta) | Acesse os novos fluxos de trabalho de início rápido na seção de “Introdução” da página inicial da Coleção de dados. O [fluxo de trabalho de início rápido da API de conversões da Meta](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=pt-br#quick-start) permite coletar e encaminhar dados de evento do lado do servidor para a Meta com rapidez, a fim de realizar conversões de anúncios em apenas algumas etapas simples. |
| Novo fluxo de trabalho de início rápido para o SDK móvel (Beta) | Acesse os novos fluxos de trabalho de início rápido na seção de “Introdução” da página inicial da Coleção de dados. O [fluxo de trabalho de início rápido do SDK móvel](https://developer.adobe.com/client-sdks/documentation/) permite implementar o SDK móvel com rapidez e validar eventos móveis básicos em apenas algumas etapas simples. |
| Extensão de encaminhamento de eventos da [!DNL Braze] | A extensão de encaminhamento de eventos [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=pt-BR) permite aproveitar os dados capturados na rede de borda da Adobe Experience Platform e enviá-los para a [!DNL Braze] na forma de eventos do lado do servidor usando as APIs de rastreamento de usuário da [!DNL Braze]. |
| Extensão de encaminhamento de eventos da [!DNL Epsilon] | A extensão [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/overview.html?lang=pt-BR) permite aproveitar o encaminhamento de eventos para capturar informações na rede de borda da Adobe Experience Platform e enviá-las para a [!DNL Epsilon] usando a API de eventos da [!DNL Epsilon]. |
| Extensão de encaminhamento de eventos da [!DNL Mixpanel] | A extensão [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=pt-BR) permite aproveitar o encaminhamento de eventos para capturar informações na rede de borda da Adobe Experience Platform e enviá-las para a Mixpanel usando a API de rastreamento de eventos. |

{style="table-layout:auto"}

## Preparação de dados {#data-prep}

A preparação de dados permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Disponibilidade geral da filtragem para dados do Adobe Analytics | Agora você pode usar as funcionalidades de preparação de dados e aplicar regras e condições para filtrar os dados do Analytics antes de assimilá-los no perfil do cliente em tempo real. Para obter mais informações, leia o guia sobre [filtragem de dados do Analytics para assimilação de perfis](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile). |
| Novas funções para codificar e decodificar strings de URL | <ul><li>A função `get_url_encoded` usa uma URL como entrada e substitui ou codifica caracteres especiais por caracteres ASCII.</li><li>A função `get_url_decoded` usa uma URL como entrada e decodifica caracteres ASCII em caracteres especiais.</li></ul> Para obter mais informações, leia o [Guia de funções da preparação de dados](../../data-prep/functions.md). Para obter uma lista abrangente de caracteres reservados e seus caracteres codificados correspondentes, leia o guia sobre [caracteres especiais](../../data-prep/functions.md#special-characters). |

Para obter mais informações sobre a preparação de dados, leia a [Visão geral da preparação de dados](../../data-prep/home.md).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Novos destinos** {#new-destinations}

| Destino | Descrição |
| ----------- | ----------- |
| Disponibilidade geral de conexão do [[!DNL Adobe Commerce] &#x200B;](../../destinations/catalog/personalization/adobe-commerce.md) | O conector de destinos do [!DNL Adobe Commerce] (agora disponível para o público) permite selecionar um ou mais públicos-alvo da Real-Time CDP para ativar na conta do [!DNL Adobe Commerce] e fornecer uma experiência personalizada e dinâmica aos compradores. |
| Disponibilidade geral de conexão da [[!DNL Snap Inc] &#x200B;](../../destinations/catalog/advertising/snap-inc.md) | O conector de destinos da [!DNL Snap Inc] (agora disponível para o público) permite que profissionais de marketing importem segmentos de usuários criados na Experience Platform para o [!DNL Snapchat Ads] e usem esses segmentos para direcionar anúncios. |
| [(API) Conexão com o Oracle Eloqua](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | Use a conexão baseada em API com o [!DNL Oracle Eloqua] para planejar e executar campanhas enquanto fornece uma experiência personalizada para seus clientes potenciais no [!DNL Oracle Eloqua]. |
| [(Beta) Conexão com o  [!DNL Amazon Ads] &#x200B;](../../destinations/catalog/advertising/amazon-ads.md) | A integração do [!DNL Amazon Ads] com a Adobe Experience Platform fornece uma integração pronta para uso com produtos do [!DNL Amazon Ads], incluindo o [!DNL Amazon DSP (ADSP)]. Usando o destino do [!DNL Amazon Ads] na Adobe Experience Platform, é possível definir os públicos-alvo do anunciante para direcionamento e ativação no [!DNL Amazon DSP]. |
| Conexão com o [[!DNL Marketo Measure Ultimate] &#x200B;](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | O [!DNL Marketo Measure] (antigo Bizible) fornece a profissionais de marketing as informações sobre quais esforços de marketing são mais eficientes na geração de receita e na maximização do retorno do investimento para a empresa. O destino permite o fluxo dos dados B2B da Adobe Experience Platform para o [!DNL Marketo Measure]. O cartão só está disponível para clientes do [!DNL Marketo Measure Ultimate]. |
| [Conexão com o TikTok](../../destinations/catalog/social/tiktok.md) | Crie públicos-alvo personalizados no TikTok com seus dados para direcionar suas campanhas de publicidade. |
| [Conexão com o Zendesk](../../destinations/catalog/crm/zendesk.md) | Use este destino para criar e atualizar identidades em um segmento na forma de contatos do [!DNL Zendesk]. |

{style="table-layout:auto"}

**Funcionalidades novas ou atualizadas** {#destinations-new-updated-functionality}

| Funcionalidade | Descrição |
| ----------- | ----------- |
| Nova permissão de controle de acesso para destinos: [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | A nova permissão oferece a capacidade de ativar segmentos para destinos existentes, sem exibir a [etapa de mapeamento](../../destinations/ui/activate-batch-profile-destinations.md#mapping). Usuários podem adicionar e remover segmentos em fluxos de trabalho de ativação, mas não podem adicionar ou remover identidades ou atributos mapeados. |

{style="table-layout:auto"}

**Correções e aprimoramentos** {#destinations-fixes-and-enhancements}

Estamos lançando uma correção de erros para a criptografia PGP/GPG em destinos baseados em arquivos para o Real-Time CDP. Com essa alteração, os destinos baseados em arquivo que estão usando a criptografia gerarão um nome de arquivo com uma extensão diferente da anterior.

- Extensão atual ao usar a criptografia: `filename.csv`
- Extensão futura ao usar a criptografia: `filename.csv.gpg`

Para obter informações mais gerais sobre destinos, consulte a [visão geral de destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados inseridos na Adobe Experience Platform. Ao aderir aos padrões do XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Recomendações de esquema com base em um CSV | Agora você pode fazer upload de arquivos locais para criar esquemas gerados por aprendizado de máquina que eliminam a necessidade de criar um esquema manualmente. No espaço de trabalho [!UICONTROL Origens], faça upload de um arquivo CSV de amostra e os algoritmos de aprendizado de máquina da Adobe sugerirão um esquema com base nos campos de destino. Consulte a [documentação](../../ingestion/tutorials/map-csv/recommendations.md) para obter mais informações.&quot; |

{style="table-layout:auto"}

**Novos componentes do XDM**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Classe | [[!UICONTROL Item de oferta]](https://github.com/adobe/xdm/pull/1678/files) | Classe que representa uma oferta. |
| Classe | [[!UICONTROL Item de decisão]](https://github.com/adobe/xdm/pull/1678/files) | Um item que pode ser sujeito a uma decisão. O resultado de um processo de decisão é um ou mais itens de decisão. |
| Classe | [[!UICONTROL Tempo limite do servidor de sessão de mídia]](https://github.com/adobe/xdm/pull/1676/files) | Isso indica o tempo, em segundos, decorrido entre a última interação conhecida do usuário e o momento em que a sessão foi encerrada. |
| Grupo de campos | [[!UICONTROL Atributos calculados do perfil de XDM]](https://github.com/adobe/xdm/pull/1686/files) | Isso adiciona atributos calculados dos serviços internos da Adobe aos dados de entrada de clientes. Isso não deve ser usado por clientes para assimilar dados. |
| Tipo de dados | [[!UICONTROL Item de reembolso]](https://github.com/adobe/xdm/pull/1685/files) | Indica se um reembolso está associado a um pedido e define o tipo de reembolso, o valor e a moeda associada. |
| Tipo de dados | [[!UICONTROL Dados da categoria]](https://github.com/adobe/xdm/pull/1677/files) | Esse novo tipo de dados representa a categoria de um produto. |
| Esquema | [[!UICONTROL Campos de classificação do Adobe Target]](https://github.com/adobe/xdm/pull/1682/files) | Um novo esquema de XDM foi criado para conjuntos de dados de classificação do Target. Ele contém um conjunto de campos de metadados que classificam as atividades e experiências do Target. |

{style="table-layout:auto"}

**Componentes de XDM atualizados**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Grupo de campos | [[!UICONTROL Detalhes do componente de conteúdo]](https://github.com/adobe/xdm/pull/1674/files) | `uri-reference` foi removido dos [!UICONTROL Detalhes do componente de conteúdo] |
| Grupo de campos | [[!UICONTROL Tags de entidade do AJO]](https://github.com/adobe/xdm/pull/1672/files) | Adição das tags de entidade do AJO aos [!UICONTROL campos de entidade do AJO], que correspondem a uma jornada ou campanha |
| Grupo de campos | (Vários) | Adição de vários campos aos [[!UICONTROL Campos comuns de evento de etapa do Journey Orchestration]](https://github.com/adobe/xdm/pull/1671/files) |
| Grupo de campos | (Vários) | [Adição de vários tipos de evento XDM aos [!UICONTROL relatórios de mídia]](https://github.com/adobe/xdm/pull/1670/files). |
| Grupo de campos | [!UICONTROL Evento de alteração do Workfront] | Os grupos de campos `Full Record` e `Accessor Employee Ids` foram adicionados. |
| Tipo de dados | [[!UICONTROL Item da lista de produtos]](https://github.com/adobe/xdm/pull/1685/files) | O [!UICONTROL Valor do reembolso] foi adicionado para indicar o valor reembolsado do item, se houver. |
| Tipo de dados | [[!UICONTROL Pedido &#x200B;]](https://github.com/adobe/xdm/pull/1685/files) | A [!UICONTROL Lista de reembolsos] foi adicionada à lista deste pedido. |
| Tipo de dados | [[!UICONTROL Item da lista de produtos &#x200B;]](https://github.com/adobe/xdm/pull/1677/files) | Categorias de produto foram adicionadas à lista de dados de categoria deste produto. |
| Tipo de dados | [!UICONTROL Informações de detalhes da sessão] | Adição do campo de string `pev3` que [indica o tipo de fluxo de mídia usado para criar relatórios](https://github.com/adobe/xdm/pull/1676/files). Também foi adicionada a propriedade `pccr`, que indica se ocorreu um redirecionamento. |
| Tipo de dados | [!UICONTROL Lista de requisições] | Fornece as [propriedades da lista de requisições](https://github.com/adobe/xdm/pull/1675/files). Estas incluem: nome, ID e descrição. |
| Tipo de dados | [!UICONTROL Comércio] | O [tipo de dados do Comércio foi atualizado](https://github.com/adobe/xdm/pull/1675/files) para incluir `requisitionListOpens`, `requisitionListAdds`, `requisitionListRemovals` e `requisitionList`. |

{style="table-layout:auto"}

Para obter mais informações sobre o XDM no Experience Platform, leia a [Visão geral do sistema XDM](../../xdm/home.md).

## Query Service {#query-service}

O Query Service permite usar SQL padrão para consultar dados no [!DNL Data Lake] da Adobe Experience Platform. É possível unir qualquer conjunto de dados do data lake e capturar os resultados de consultas como um novo conjunto de dados para usar em relatórios, no espaço de trabalho de ciência de dados ou para assimilação no perfil do cliente em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Controle de acesso baseado em atributos no armazenamento acelerado | Use o controle de acesso baseado em atributos com o Data Distiller para definir o controle de acesso em todos os conjuntos de dados no armazenamento acelerado. Isso controla o acesso aos modelos de dados personalizados criados por usuários e armazenados em um armazenamento acelerado para alimentar painéis personalizados. |

{style="table-layout:auto"}

Para obter mais informações sobre o Query Service, acesse a [Visão geral do Query Service](../../query-service/home.md).

## Real-Time Customer Data Platform B2B Edition {#b2b}

Criada com base na Real-time Customer Data Platform (Real-Time CDP), a Real-Time CDP B2B Edition foi desenvolvida especificamente para profissionais de marketing que operam em um modelo de serviço B2B. A plataforma reúne dados de várias origens e os combina numa única exibição de perfis de pessoas e contas. Esses dados unificados permitem que profissionais de marketing direcionem públicos-alvo específicos com precisão e gerem engajamento em todos os canais disponíveis.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Correção de erros | Para fornecer uma representação mais precisa dos perfis em seu sistema, o sistema já não inclui perfis internos na contagem total de perfis ou na métrica de público-alvo endereçável da Real-time Customer Data Platform B2B Edition. A partir de hoje, você poderá observar uma queda única na contagem total de perfis/métrica de público-alvo endereçável. Nenhum de seus dados foi apagado, isso é apenas uma alteração na contagem. Para esclarecer quaisquer dúvidas, entre em contato com o executivo da sua conta da Adobe. |

{style="table-layout:auto"}

Para saber mais sobre a Real-Time CDP B2B Edition, leia a [Visão geral da Real-Time CDP B2B Edition](../../rtcdp/overview.md).

## Serviço de segmentação {#segmentation}

O [!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo de pessoas na sua base de clientes que pode ser direcionado por campanhas de marketing. Os segmentos podem ser baseados em dados de registro (como informações demográficas) ou em eventos de séries temporais que representam interações de clientes com sua marca.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Métricas de perfil | Para fornecer uma representação mais precisa das métricas de perfil, as métricas de detalhamento de associação e churn estão sendo combinadas e agora são calculadas em um período de 24 horas. Mais informações disponíveis no [guia da Interface de segmentação](../../segmentation/ui/overview.md#browse) |

{style="table-layout:auto"}

Para obter mais informações sobre o [!DNL Segmentation Service], consulte a [Visão geral de segmentação](../../segmentation/home.md).

## Origens {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e permite estruturar, rotular e aprimorar esses dados usando os serviços da Experience Platform. É possível assimilar dados de várias origens, como aplicativos da Adobe, do armazenamento na nuvem, um software de terceiros e do seu sistema de CRM.

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Disponibilidade beta do [!DNL Chatlio] | A origem do [!DNL Chatlio] está disponível na versão beta. Use a origem do [!DNL Chatlio] para transmitir dados de eventos do [!DNL Chatlio] para a Experience Platform. Para obter mais informações, leia a visão geral[&#128279;](../../sources/connectors/marketing-automation/chatlio-webhook.md) do [!DNL Chatlio] . |
| Disponibilidade beta do [!DNL Customer.io] | A origem do [!DNL Customer.io] agora está disponível na versão beta. Use a origem do [!DNL Customer.io] para transmitir dados de evento de clientes para a Experience Platform. Para obter mais informações, leia a visão geral[&#128279;](../../sources/connectors/marketing-automation/customerio-webhook.md) do [!DNL Customer.io] . |
| Disponibilidade beta do [!DNL Pendo] | A origem do [!DNL Pendo] agora está disponível na versão beta. Use a origem do [!DNL Pendo] para transmitir os dados de análise do produto para a Experience Platform. Para obter mais informações, leia a visão geral[&#128279;](../../sources/connectors/analytics/pendo-webhook.md) do [!DNL Pendo] . |
| Suporte para fluxos de dados de rascunho | Agora você pode usar a API do serviço de fluxo para atribuir um estado de rascunho aos fluxos de dados. Os fluxos de dados em rascunho podem ser atualizados e publicados posteriormente com novas informações. Para obter mais informações, leia o guia [Definir os fluxos de dados de origem como rascunhos](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

Para saber mais sobre origens, leia a [visão geral de origens](../../sources/home.md).
