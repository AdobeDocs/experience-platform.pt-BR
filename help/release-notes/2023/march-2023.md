---
title: Notas de versão da Adobe Experience Platform de março de 2023
description: As notas de versão de março de 2023 para o Adobe Experience Platform.
source-git-commit: 1aeaf832f6cb2acf65c25199693b06669682883b
workflow-type: tm+mt
source-wordcount: '2398'
ht-degree: 4%

---

# Notas de versão da Adobe Experience Platform

>[!IMPORTANT]
>
>A partir de 5 de abril de 2023, a variável `Existing` será descontinuado do mapa de associação de segmentos para remover a redundância no ciclo de vida de associação de segmentos. Após essa alteração, os perfis qualificados em um segmento serão representados como `Realized` e os perfis desqualificados continuarão sendo representados como `Exited`. Para obter mais detalhes sobre esta alteração, leia o [Seção Serviço de segmentação](#segmentation).

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

O Adobe Experience Platform fornece vários painéis através dos quais você pode visualizar informações importantes sobre os dados de sua organização, como capturados durante os instantâneos diários.

**Recursos novos ou atualizados** {#dashboards-new-updated-features}

| Recurso | Descrição |
| --- | --- |
| Painéis definidos pelo usuário | Agora você pode **valores do atributo de amostra** antes de adicionar um atributo a um widget no compositor de widget de painéis definido pelo usuário. Alguns valores de exemplo dessa coluna de atributo estão disponíveis para atributos individuais ao criar um widget.<br>Agora você pode **trocar o eixo X e Y** no widget com o botão de eixo de troca. Isso economiza tempo e fornece uma experiência mais ergonômica ao adicionar atributos aos widgets. Isso salva a necessidade de localizar ambos os atributos novamente no painel de atributos.<br> Agora você pode **alterar a localização e o título da legenda** em seus widgets. Depois que uma legenda estiver presente em um widget, você poderá reposicionar a legenda em qualquer lugar do gráfico e também renomear o título da legenda, como pode fazer com rótulos de eixo e o título do widget. |

{style="table-layout:auto"}

Para obter mais informações sobre painéis, incluindo como conceder permissões de acesso e criar widgets personalizados, comece lendo o [visão geral dos painéis](../../dashboards/home.md).

## Coleta de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente e enviá-los para a Adobe Experience Platform Edge Network, onde podem ser enriquecidos, transformados e distribuídos para destinos Adobe ou não-Adobe.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Novo fluxo de trabalho de início rápido para a API Meta conversões (Beta) | Acesse novos fluxos de trabalho de início rápido em &quot;Introdução&quot; na tela inicial da Coleta de dados! O [fluxo de trabalho de início rápido para a API de Meta conversões](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) permite que os clientes coletem e encaminhem rapidamente os dados do evento, do lado do servidor para o Meta para conversões de anúncios em apenas algumas etapas simples. |
| Novo fluxo de trabalho de início rápido para o SDK móvel (Beta) | Acesse novos fluxos de trabalho de início rápido em &quot;Introdução&quot; na tela inicial da Coleta de dados! O [fluxo de trabalho de início rápido para o Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) O permite implementar rapidamente o SDK móvel e validar eventos móveis básicos em apenas algumas etapas simples. |
| [!DNL Braze] extensão de encaminhamento de eventos | O [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) a extensão de encaminhamento de eventos permite aproveitar os dados capturados na Rede de borda do Adobe Experience Platform e enviá-los para [!DNL Braze] na forma de eventos do lado do servidor usando o [!DNL Braze] APIs de rastreamento de usuário. |
| [!DNL Epsilon] extensão de encaminhamento de eventos | O [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/overview.html) A extensão permite aproveitar o encaminhamento do evento para capturar informações do evento na Rede de borda do Adobe Experience Platform e enviá-las para [!DNL Epsilon] usando o [!DNL Epsilon] API de evento. |
| [!DNL Mixpanel] extensão de encaminhamento de eventos | O [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) A extensão permite que os clientes aproveitem o encaminhamento do evento para capturar informações do evento na Rede de borda do Adobe Experience Platform e enviá-las para o Mixpanel usando a API de rastreamento de eventos. |

{style="table-layout:auto"}

## Preparação de dados {#data-prep}

A Preparação de dados permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Disponibilidade geral de filtragem para dados do Adobe Analytics | Agora é possível usar as funcionalidades de Preparação de dados para aplicar regras e condições para filtrar os dados do Analytics antes de assimilá-los no Perfil do cliente em tempo real. Para obter mais informações, leia o guia sobre [filtrar dados do Analytics para assimilação de perfil](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile). |
| Novas funções para codificação e decodificação de strings de URL | <ul><li>O `get_url_encoded` assume um URL como entrada e substitui ou codifica caracteres especiais com caracteres ASCII.</li><li>O `get_url_decoded` assume um URL como entrada e decodifica caracteres ASCII em caracteres especiais.</li></ul> Para obter mais informações, leia a [Guia de funções de Preparação de dados](../../data-prep/functions.md). Para obter uma lista abrangente de caracteres reservados e seus caracteres codificados correspondentes, leia o guia em [caracteres especiais](../../data-prep/functions.md#special-characters). |

Para obter mais informações sobre Preparação de dados, leia a [Visão geral da preparação de dados](../../data-prep/home.md).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, anúncios direcionados e muitos outros casos de uso.

**Novos destinos** {#new-destinations}

| Destino | Descrição |
| ----------- | ----------- |
| [[!DNL Adobe Commerce] conexão GA](../../destinations/catalog/personalization/adobe-commerce.md) | O [!DNL Adobe Commerce] o conector de destino (agora disponível geralmente) permite selecionar um ou mais públicos-alvo do Real-Time CDP para ativar em seu [!DNL Adobe Commerce] conta para fornecer uma experiência personalizada dinâmica para seus compradores. |
| [[!DNL Snap Inc] conexão GA](../../destinations/catalog/advertising/snap-inc.md) | O [!DNL Snap Inc] o conector de destino (agora disponível no geral) permite que os profissionais de marketing importem segmentos de usuários criados no Experience Platform para [!DNL Snapchat Ads] e use-as para direcionar seus anúncios. |
| [Conexão Eloqua do Oracle (API)](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | Use a conexão baseada em API para [!DNL Oracle Eloqua] para planejar e executar campanhas, fornecendo uma experiência personalizada do cliente para seus prospetos em [!DNL Oracle Eloqua]. |
| [(Beta) [!DNL Amazon Ads] conexão](../../destinations/catalog/advertising/amazon-ads.md) | O [!DNL Amazon Ads] a integração com o Adobe Experience Platform fornece integração completa para [!DNL Amazon Ads] , incluindo a [!DNL Amazon DSP (ADSP)]. Usar o [!DNL Amazon Ads] no Adobe Experience Platform, os usuários podem definir públicos do anunciante para direcionamento e ativação no [!DNL Amazon DSP]. |
| [[!DNL Marketo Measure Ultimate] conexão](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] (anteriormente Bizible) fornece aos profissionais de marketing informações sobre quais esforços de marketing são os mais eficazes na geração de receita e na maximização do retorno sobre o investimento de sua empresa. O destino habilita os fluxos de dados B2B (B2B) de negócios para o Adobe Experience Platform [!DNL Marketo Measure]. O cartão só está disponível para [!DNL Marketo Measure Ultimate] clientes. |
| [Conexão TikTok](../../destinations/catalog/social/tiktok.md) | Crie públicos personalizados no TikTok com seus dados para segmentação com suas campanhas de publicidade. |
| [Conexão com o Zendesk](../../destinations/catalog/crm/zendesk.md) | Usar este destino para criar e atualizar identidades em um segmento como contatos dentro de [!DNL Zendesk]. |

{style="table-layout:auto"}

**Funcionalidade nova ou atualizada** {#destinations-new-updated-functionality}

| Funcionalidade | Descrição |
| ----------- | ----------- |
| Nova permissão de controle de acesso para destinos: [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | A nova permissão oferece aos usuários a capacidade de ativar segmentos para destinos existentes, sem exibir a variável [etapa de mapeamento](../../destinations/ui/activate-batch-profile-destinations.md#mapping). Os usuários podem adicionar e remover segmentos em workflows de ativação, mas não podem adicionar ou remover atributos ou identidades mapeadas. |

{style="table-layout:auto"}

**Correções e aprimoramentos** {#destinations-fixes-and-enhancements}

Estamos lançando uma correção de erro para criptografia PGP/GPG em destinos com base em arquivo para CDP em tempo real. Com essa alteração, os destinos existentes baseados em arquivos que atualmente usam criptografia gerarão um nome de arquivo com uma extensão diferente de antes.

- Extensão atual ao usar criptografia: `filename.csv`
- Extensão futura ao usar criptografia: `filename.csv.gpg`

Para obter informações mais gerais sobre destinos, consulte [visão geral dos destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Adobe Experience Platform. Ao seguir os padrões XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de uma maneira mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| CSV para recomendação de esquema | Agora é possível fazer upload de seus arquivos locais para criar esquemas gerados pelo aprendizado de máquina que eliminam a necessidade de criar manualmente um schema. No [!UICONTROL Fontes] espaço de trabalho, carregar um arquivo CSV de amostra e algoritmos de aprendizado de máquina do Adobe sugerirão um esquema para você com base nos campos de destino. Consulte a [documentação da](../../ingestion/tutorials/map-csv/recommendations.md) para obter mais informações.&quot; |

{style="table-layout:auto"}

**Novos componentes XDM**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Classe | [[!UICONTROL Item da oferta]](https://github.com/adobe/xdm/pull/1678/files) | Classe que representa uma Oferta. |
| Classe | [[!UICONTROL Item de decisão]](https://github.com/adobe/xdm/pull/1678/files) | Um item que pode ser sujeito a decisão. O resultado de um processo de decisão é um ou mais elementos de decisão. |
| Classe | [[!UICONTROL Tempo limite do servidor da sessão de mídia]](https://github.com/adobe/xdm/pull/1676/files) | Isso indica o tempo, em segundos, decorrido entre a última interação conhecida do usuário e o momento em que a sessão foi encerrada. |
| Grupo de campos | [[!UICONTROL Atributos calculados do perfil XDM]](https://github.com/adobe/xdm/pull/1686/files) | Isso adiciona atributos calculados dos serviços internos da Adobe aos dados de entrada do cliente. Isso não deve ser usado pelos clientes para assimilar dados. |
| Tipo de dados | [[!UICONTROL Item de reembolso]](https://github.com/adobe/xdm/pull/1685/files) | Indica se um reembolso está associado a um pedido e define o tipo de reembolso, o valor e a moeda associada. |
| Tipo de dados | [[!UICONTROL Dados da categoria]](https://github.com/adobe/xdm/pull/1677/files) | Este novo tipo de dados representa a categoria de um produto. |
| Esquema | [[!UICONTROL Campos de classificação Adobe Target]](https://github.com/adobe/xdm/pull/1682/files) | Um novo esquema XDM foi criado para os conjuntos de dados de Classificação do Target. Ele contém um conjunto de campos de metadados que classificam atividades e experiências do Target. |

{style="table-layout:auto"}

**Componentes XDM atualizados**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Grupo de campos | [[!UICONTROL Detalhes do componente de conteúdo]](https://github.com/adobe/xdm/pull/1674/files) | `uri-reference` foi removido de [!UICONTROL Detalhes do componente de conteúdo] |
| Grupo de campos | [[!UICONTROL Tags de entidade AJO]](https://github.com/adobe/xdm/pull/1672/files) | Adição de tags de entidade AJO ao [!UICONTROL Campos de entidade AJO], que correspondem a uma Jornada ou campanha |
| Grupo de campos | (Várias) | Foram adicionados vários campos para [[!UICONTROL Campos comuns do evento Journey Orchestration Step]](https://github.com/adobe/xdm/pull/1671/files) |
| Grupo de campos | (Várias) | [Adição de vários tipos de evento XDM para [!UICONTROL Relatórios de mídia]](https://github.com/adobe/xdm/pull/1670/files). |
| Grupo de campos | [!UICONTROL Evento Workfront Change] | O `Full Record` e `Accessor Employee Ids` grupos de campos foram adicionados. |
| Tipo de dados | [[!UICONTROL Item da lista de produtos]](https://github.com/adobe/xdm/pull/1685/files) | O [!UICONTROL Montante do reembolso] foi adicionado para indicar o montante reembolsado do item, se houver. |
| Tipo de dados | [[!UICONTROL Pedido ]](https://github.com/adobe/xdm/pull/1685/files) | [!UICONTROL Lista de reembolsos] foi adicionado à lista de reembolsos para este pedido. |
| Tipo de dados | [[!UICONTROL Item da Lista de Produtos ]](https://github.com/adobe/xdm/pull/1677/files) | As categorias de produto foram adicionadas à lista dos dados de categoria deste produto. |
| Tipo de dados | [!UICONTROL Informações de detalhes da sessão] | Adicionado o `pev3` campo de string que [indica o tipo de fluxo de mídia usado para relatórios](https://github.com/adobe/xdm/pull/1676/files). Também foi adicionado o `pccr` indica se ocorreu um redirecionamento. |
| Tipo de dados | [!UICONTROL Lista de Requisições] | Fornece o [propriedades da lista de requisições](https://github.com/adobe/xdm/pull/1675/files). Eles incluem nome, ID e descrição. |
| Tipo de dados | [!UICONTROL Commerce] | O [O tipo de dados de comércio foi atualizado](https://github.com/adobe/xdm/pull/1675/files) para incluir `requisitionListOpens`, `requisitionListAdds`, `requisitionListRemovals`e `requisitionList`. |

{style="table-layout:auto"}

Para obter mais informações sobre o XDM na Platform, leia o [Visão geral do sistema XDM](../../xdm/home.md).

## Serviço de query {#query-service}

O Serviço de Consulta permite que você use o SQL padrão para consultar dados no Adobe Experience Platform [!DNL Data Lake]. É possível unir qualquer conjunto de dados de data lake e capturar os resultados da consulta como um novo conjunto de dados para uso em relatórios, na Data Science Workspace ou para assimilação no Perfil do cliente em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Controle de acesso baseado em atributos no armazenamento acelerado | Use o Controle de acesso com base em atributos com o Data Distiller para definir o controle de acesso em todos os conjuntos de dados no armazenamento acelerado. Isso controla o acesso aos modelos de dados personalizados criados pelos usuários e armazenados em uma loja acelerada para potencializar painéis personalizados. |

{style="table-layout:auto"}

Para obter mais informações sobre Serviços de query, consulte [Visão geral do Serviço de query](../../query-service/home.md).

## Real-Time Customer Data Platform B2B Edition {#b2b}

Baseado no Real-time Customer Data Platform (Real-Time CDP), o Real-Time CDP B2B Edition foi desenvolvido para profissionais de marketing que operam em um modelo de serviço de empresa para empresa. Ele reúne dados de várias fontes e os combina em uma única visualização de pessoas e perfis de conta. Esses dados unificados permitem que os profissionais de marketing direcionem com precisão públicos-alvo específicos e os envolvam em todos os canais disponíveis.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Bugfix | Para fornecer uma representação mais precisa dos perfis em seu sistema, o sistema não inclui mais perfis internos na contagem total de perfis ou na métrica de público-alvo endereçável para o Real-time Customer Data Platform B2B Edition. A partir de hoje, você pode ver uma queda única na métrica de contagem de perfis/público-alvo endereçável total. Nenhum de seus dados foi apagado, isso é simplesmente uma alteração na contagem. Entre em contato com o executivo do Adobe se tiver dúvidas |

{style="table-layout:auto"}

Para saber mais sobre o Real-Time CDP B2B Edition, leia a [Visão geral do Real-Time CDP B2B Edition](../../rtcdp/overview.md).

## Serviço de segmentação {#segmentation}

[!DNL Segmentation Service] O define um subconjunto específico de perfis ao descrever os critérios que distinguem um grupo comercializável de pessoas dentro da base do cliente. Os segmentos podem se basear em dados de registro (como informações demográficas) ou em eventos de séries cronológicas que representem as interações do cliente com sua marca.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Métricas de perfil | Para fornecer uma representação mais precisa das métricas de perfil, o detalhamento da associação e as métricas de rotatividade estão sendo combinados e agora são calculadas por um período de 24 horas. Mais informações estão disponíveis na [Guia da interface do usuário de segmentação](../../segmentation/ui/overview.md#browse) |
| Mapa de associação de segmento | Como seguimento ao anúncio anterior em fevereiro, em 5 de abril de 2023, o `Existing` será descontinuado do mapa de associação de segmentos para remover a redundância no ciclo de vida de associação de segmentos. Após essa alteração, os perfis qualificados em um segmento serão representados como `Realized` e os perfis desqualificados continuarão sendo representados como `Exited`.<br/><br/>  Essa alteração pode afetar você se, você estiver usando [destinos corporativos](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Hubs de eventos do Azure, API HTTP) e pode ter processos downstream automatizados em vigor com base no `Existing` status. Revise suas integrações downstream, se for o caso. Se estiver interessado em identificar perfis recém-qualificados além de um determinado tempo, considere usar uma combinação do `Realized` e o `lastQualificationTime` no mapa de associação de segmentos. Para obter mais informações, entre em contato com o representante do Adobe. |

{style="table-layout:auto"}

Para obter mais informações sobre [!DNL Segmentation Service]consulte o [Visão geral da segmentação](../../segmentation/home.md).

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e permite estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Disponibilidade beta de [!DNL Chatlio] | O [!DNL Chatlio] A fonte agora está disponível em beta. Use o [!DNL Chatlio] origem para transmitir [!DNL Chatlio] dados de eventos para o Experience Platform. Para obter mais informações, leia a [[!DNL Chatlio] visão geral](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| Disponibilidade beta de [!DNL Customer.io] | O [!DNL Customer.io] A fonte agora está disponível em beta. Use o [!DNL Customer.io] fonte para transmitir os dados de eventos do cliente para o Experience Platform. Para obter mais informações, leia a [[!DNL Customer.io] visão geral](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| Disponibilidade beta de [!DNL Pendo] | O [!DNL Pendo] A fonte agora está disponível em beta. Use o [!DNL Pendo] fonte para transmitir os dados de análise do produto para o Experience Platform. Para obter mais informações, leia a [[!DNL Pendo] visão geral](../../sources/connectors/analytics/pendo-webhook.md). |
| Suporte para fluxos de dados de rascunho | Agora é possível usar a API do Serviço de fluxo para definir os fluxos de dados para um estado de rascunho. Fluxos de dados preparados podem ser atualizados e publicados posteriormente com novas informações. Para obter mais informações, leia o guia sobre [definição dos fluxos de dados de origens como rascunhos](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

Para saber mais sobre fontes, leia a [visão geral das fontes](../../sources/home.md).
