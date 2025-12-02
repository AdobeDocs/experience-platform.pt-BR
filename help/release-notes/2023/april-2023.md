---
title: Notas de versão de abril de 2023 da Adobe Experience Platform
description: As notas de versão de abril de 2023 da Adobe Experience Platform.
exl-id: 7b501467-99a7-4aee-ae86-66c851250ecf
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '1983'
ht-degree: 94%

---

# Notas de versão da Adobe Experience Platform

>[!IMPORTANT]
>
>A partir de 15 de maio de 2023, o status `Existing` será descontinuado do mapa de segmentos de associação para remover a redundância no ciclo de vida da associação a um segmento. Após essa alteração, os perfis qualificados em um segmento serão representados como `Realized` e os perfis desqualificados continuarão a ser representados como `Exited`. Para obter mais detalhes sobre esta alteração, leia a [seção Serviço de segmentação](#segmentation).

**Data de lançamento: 26 de abril de 2023**

Atualizações dos recursos já existentes na Adobe Experience Platform:

- [Painéis](#dashboards)
- [Preparação de dados](#data-prep)
- [Coleção de dados](#data-collection)
- [Destinos](#destinations)
- [Experience Data Model](#xdm)
- [Real-Time Customer Data Platform](#rtcdp)
- [Perfil do cliente em tempo real](#profile)
- [Serviço de segmentação](#segmentation)
- [Origens](#sources)

## Painéis {#dashboards}

A Adobe Experience Platform fornece vários painéis para você visualizar insights importantes sobre os dados de sua organização, que são capturados por instantâneos diários.

**Recursos novos ou atualizados** {#dashboards-new-updated-features}

| Recurso | Descrição |
| --- | --- |
| Painéis definidos pelo usuário | Agora você pode **filtrar dados históricos** dos insights de widgets e usar dados recentes ou um período de análise personalizado. Consulte o [Guia de painéis definidos pelo usuário](../../dashboards/standard-dashboards.md#filter-historical-data) para obter mais informações.<br>Agora você também pode **duplicar widgets existentes**. Ao personalizar um widget duplicado e editar seus atributos, você elimina a necessidade de criar um widget novo e exclusivo do zero. Leia o [guia de duplicação de widget](../../dashboards/standard-dashboards.md#duplicate-a-widget) para saber mais. |

{style="table-layout:auto"}

Para obter mais informações sobre painéis, incluindo como conceder permissões de acesso e criar widgets personalizados, comece lendo a [visão geral dos painéis](../../dashboards/home.md).

## Preparação de dados {#data-prep}

A preparação de dados permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Atualizações no período de preenchimento retroativo do Adobe Analytics em sandboxes que não são de produção | O período de preenchimento retroativo do Adobe Analytics em sandboxes que não são de produção foi reduzido para três meses. O preenchimento retroativo para sandboxes de produção continua sendo de 13 meses. Essa alteração se aplica somente a novos fluxos e não afetará os fluxos existentes. Para obter mais informações, leia a [Visão geral do Adobe Analytics](../../sources/connectors/adobe-applications/analytics.md). |
| Nova função de mapeamento para converter strings FPID para ECID | Use a função `fpid_to_ecid` para converter strings FPID em ECID para uso em aplicativos da Experience Platform e Experience Cloud. Para obter mais informações, leia o [Guia de funções de preparação de dados](../../data-prep/functions.md). |

{style="table-layout:auto"}

Para obter mais informações sobre a preparação de dados, leia a [Visão geral de preparação de dados](../../data-prep/home.md).

## Coleção de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados da experiência do cliente e enviá-los à Rede de borda da Adobe Experience Platform, onde eles podem ser enriquecidos, transformados e distribuídos para destinos da Adobe ou de outras empresas.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Ofuscação de endereço IP para sequências de dados | Agora é possível definir opções de ofuscação parcial ou completa de IP no nível da sequência de dados por meio da [interface de configuração de sequência de dados](../../datastreams/configure.md). <br><br>A configuração de ofuscação de IP no nível da sequência de dados tem precedência sobre qualquer ofuscação de IP configurada no Adobe Target e no Audience Manager. <br><br>Os dados enviados para a Adobe Analytics não são afetados pela configuração [!UICONTROL IP Obfuscation] no nível de sequência de dados. Atualmente, o Adobe Analytics recebe endereços IP não ofuscados. Para que o Analytics receba endereços IP ofuscados, você deve configurar a ofuscação de IP separadamente no Adobe Analytics. Esse comportamento será atualizado em versões futuras.<br><br> Para obter mais detalhes sobre a ofuscação de IP e instruções sobre como configurá-la, consulte a [documentação de configuração da sequência de dados](../../datastreams/configure.md#advanced-options). |
| [Substituições de configuração da sequência de dados](../../datastreams/overrides.md) | Agora é possível definir opções de configuração adicionais para sequências de dados, o que pode ser usado para substituir configurações específicas, como conjuntos de dados de eventos, tokens de propriedade do Target, containers de sincronização de ID e conjuntos de relatórios do Analytics. <br><br>Substituir as configurações da sequência de dados é um processo de duas etapas: <ol><li>Primeiro, você deve definir as substituições de configuração da sequência na [página de configuração da sequência de dados](../../datastreams/configure.md).</li><li>Em seguida, você deve enviar as substituições para a rede de borda por meio de um comando do SDK da Web ou usando a [extensão de tag](/help/tags/extensions/client/web-sdk/configure/configuration-overrides.md) do SDK da Web.</li></ol> |
| Segredo JWT do OAuth  | O [Segredo JWT do OAuth](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=pt-br) permite aos clientes usar tokens de serviço da Adobe e do Google para oferecer compatibilidade com interações de servidor para servidor no encaminhamento de eventos. |
| Extensão do [!DNL Pinterest Conversions API] | A extensão de encaminhamento de eventos da [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html?lang=pt-BR) permite aproveitar os dados capturados na rede de borda da Adobe Experience Platform e enviá-los para o [!DNL Pinterest] na forma de eventos do lado do servidor usando a [!DNL Pinterest Conversions API]. |

{style="table-layout:auto"}

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Novos destinos** {#new-destinations}

| Destino | Descrição |
| ----------- | ----------- |
| Conexão do [[!DNL Salesforce Marketing Cloud Account Engagement] &#x200B;](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) | Use o destino Salesforce Marketing Cloud Account Engagement (anteriormente conhecido como Pardot) para capturar, rastrear, pontuar e classificar leads. Use esse destino para casos de uso de B2B que envolvam vários departamentos e tomadores de decisão que exigem ciclos de vendas e decisões mais longos. |

{style="table-layout:auto"}

**Funcionalidade nova ou atualizada** {#destinations-new-updated-functionality}

| Funcionalidade | Descrição |
| ----------- | ----------- |
| Monitoramento de fluxo de dados para destinos do [!DNL Custom Personalization] e [!DNL Adobe Commerce] | <p> Agora você pode ver as métricas de ativação das conexões do [Adobe Commerce](/help/destinations/catalog/personalization/adobe-commerce.md), [Personalização individual](../../destinations/catalog/personalization/custom-personalization.md) e [Personalização individual com atributos](../../destinations/catalog/personalization/custom-personalization.md). </p> <p>![Imagem do Adobe Commerce](/help/destinations/assets/common/adobe-commerce-metrics.png "Métricas do Adobe Commerce"){width="100" zoomable="yes"}</p>  Consulte [Monitorar fluxos de dados no espaço de trabalho de destinos](../../dataflows/ui/monitor-destinations.md#monitor-dataflows-in-the-destinations-workspace) para obter mais detalhes. |
| Novo campo **[!UICONTROL Append segment ID to segment name]** para os destinos [!DNL Google Ad Manager] e [!DNL Google Ad Manager 360] | <p>Agora é possível fazer o nome do segmento no [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) e [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) incluir a ID de segmento da Experience Platform, desta forma: `Segment Name (Segment ID)`.</p><p>![Anexar imagem da ID do segmento](/help/destinations/assets/common/append-segment-id-to-segment-name.png "Novo campo Anexar ID de segmento ao nome do segmento "){width="100" zoomable="yes"}</p> |
| Preenchimentos retroativos de público-alvo programados | <p>Para o destino [[!DNL Google Display & Video 360]](/help/destinations/catalog/advertising/google-dv360.md#specifics), a ativação de preenchimentos retroativos de público-alvo para o destino é agendada para ocorrer de 24 a 48 horas depois que um segmento é mapeado pela primeira vez para uma conexão de destino. Esta atualização é uma resposta à política da Google de aguardar 24 horas até assimilar dados e melhorará as taxas de correspondência entre o Real-Time CDP e o [!DNL Google Display & Video 360].</p> <p>Observe que essa é uma configuração de back-end aplicável somente a esse destino e não está relacionada a nenhuma opção de agendamento configurável pelo cliente na interface.</p> |

{style="table-layout:auto"}

**Correções e aprimoramentos** {#destinations-fixes-and-enhancements}

- Corrigimos um problema nas métricas de relatório **Identidades excluídas** para exportações de destino baseadas em arquivo. Os clientes estavam recebendo todas as IDs exportadas da exportação ativada, conforme esperado. No entanto, a métrica de relatório **Identidades excluídas** na interface exibia incorretamente números altos de identidades excluídas devido à contagem incorreta de identidades que nunca deveriam ser exportadas. (PLAT-149774)
- Corrigimos um problema na etapa de **Agendamento** do fluxo de trabalho de ativação. Para destinos que precisam de uma ID de mapeamento, os clientes não conseguiram adicionar uma para segmentos adicionados a conexões de destino já existentes. (PLAT-148808)

<!--
- We have fixed an issue with the beta SFTP destination where the port number was previously hardcoded to 22. The port is now configurable for this destination. 

-->

Para obter mais informações gerais sobre destinos, consulte a [visão geral de destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados inseridos na Adobe Experience Platform. Ao aderir aos padrões do XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Botão de alternância de nomes de exibição | O Editor de esquemas agora fornece um botão de alternância para alternar entre os nomes de campo originais e os nomes de exibição mais legíveis.<br>![O Editor de esquemas com o botão de alternância de nome de exibição realçado.](../../xdm/images/ui/resources/schemas/display-name-toggle.png "Botão de alternância do nome de exibição do Editor de esquemas"){width="100" zoomable="yes"}<br>Essa flexibilidade permite uma descoberta de campo aprimorada e a edição de seus esquemas. Os nomes de exibição para grupos de campos padrão são gerados pelo sistema, mas também podem ser personalizados por meio da interface, se necessário. Leia a [documentação do botão de alternância do nome de exibição](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=pt-BR#display-name-toggle) para saber mais. |

{style="table-layout:auto"}

**Novos componentes de XDM**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Esquema | [[!UICONTROL Adobe Target Classification Fields]](https://github.com/adobe/xdm/pull/1719/files) | Um novo esquema de XDM para conjuntos de dados de Classificação do Target, contendo um conjunto de campos de metadados para classificar atividades e experiências do Target. |

{style="table-layout:auto"}

**Componentes de XDM atualizados**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Grupo de campos | [[!UICONTROL Adobe Unified Profile Service Account Union Extension]](https://github.com/adobe/xdm/pull/1696/files) | Um grupo de campos de extensão de conta para o Perfil do cliente em tempo real foi adicionado. Ele permite aos usuários a adição de segmentos de associação na união de contas. |
| Esquema | [[!UICONTROL Computed Attributes System Schema]](https://github.com/adobe/xdm/pull/1696/files) | O grupo de campos Atributos calculados usado pelo Perfil do cliente em tempo real foi atualizado para um esquema global de somente leitura do sistema. |
| Grupo de campos | Múltiplo | Adição de vários eventos como campos para [[!UICONTROL Time-series Schema]](https://github.com/adobe/xdm/pull/1718/files). |
| Grupo de campos | Detalhes de fidelidade do perfil | [Corrigido o título](https://github.com/adobe/xdm/pull/1717/files) para `xdm:upgradeDate` de “Nome do programa” para “Data de atualização”. |
| Grupo de campos | Múltiplo | Vários campos de [[!UICONTROL Decision Item]](https://github.com/adobe/xdm/pull/1714/files) foram atualizados para remover a hierarquia aninhada dupla. |

{style="table-layout:auto"}

Para obter mais informações sobre o XDM no Experience Platform, leia a [Visão geral do sistema XDM](../../xdm/home.md).

## Real-Time Customer Data Platform

Integrado à Experience Platform, a Real-time Customer Data Platform ([!DNL Real-Time CDP]) ajuda as empresas a unirem dados conhecidos e desconhecidos para ativar perfis de clientes com decisões inteligentes em toda a jornada do cliente. A [!DNL Real-Time CDP] combina várias fontes de dados corporativos para criar perfis de clientes em tempo real. Os segmentos criados a partir desses perfis podem ser enviados para destinos downstream com o fim de oferecer experiências de cliente personalizadas em todos os canais e dispositivos.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Página inicial da Real-Time CDP aprimorada | A [Página inicial da Real-Time CDP](https://experience.adobe.com) foi aprimorada com uma aparência atualizada e melhor desempenho. A página inicial agora tem reconhecimento de permissões e apresentará dispositivos relevantes para os recursos aos quais você tem acesso. Para obter mais informações, leia a [Visão geral do painel da página inicial da Real-Time CDP](../../rtcdp/home-page-dashboards.md). |
| Pesquisa de autoidentificação | A pesquisa de autoidentificação é um pequeno questionário apresentado na página inicial da interface da Adobe Experience Platform. Use a pesquisa de autoidentificação para criar seu perfil pessoal da Experience Platform e receber diretrizes personalizadas com base em suas seleções. Para obter mais informações, leia a [Visão geral da pesquisa de autoidentificação](../../landing/self-identification.md). |

Para obter mais informações sobre a [!DNL Real-Time CDP], consulte a [[!DNL Real-Time CDP] visão geral](../../rtcdp/overview.md).

## Perfil do cliente em tempo real {#profile}

A Adobe Experience Platform permite gerar experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagem com sua marca. Com o Perfil do cliente em tempo real, é possível ter uma visão integral de cada cliente ao combinar dados de vários canais, incluindo online, offline, CRM e de terceiros. O Perfil permite consolidar os dados do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

**Recursos atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Expiração de dados de perfil pseudônimo | A expiração de dados de perfil pseudônimo agora está disponível para todos. Essa versão removerá continuamente perfis pseudônimos obsoletos de sua instância da Experience Platform, uma vez habilitada. Para saber mais sobre este recurso e Perfis pseudônimos, leia o [Guia de expiração de dados do perfil pseudônimo](../../profile/pseudonymous-profiles.md). |

{style="table-layout:auto"}

## Serviço de segmentação {#segmentation}

O [!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo de pessoas na sua base de clientes que pode ser direcionado por campanhas de marketing. Os segmentos podem ser baseados em dados de registro (como informações demográficas) ou em eventos de série temporal que representam interações de clientes com sua marca.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Mapa de segmentos de associação | Seguindo o anúncio anterior em fevereiro, em 15 de maio de 2023, o status `Existing` será descontinuado do mapa de segmentos de associação para remover a redundância no ciclo de vida da associação a um segmento. Após essa alteração, os perfis qualificados em um segmento serão representados como `Realized`, e os perfis desqualificados continuarão a ser representados como `Exited`.<br/><br/> Essa alteração pode impactar quem se estiver usando os [destinos corporativos](../../destinations/destination-types.md#advanced-enterprise-destinations) (Amazon Kinesis, Hubs de Eventos do Azure, API HTTP) e que tenha processos de downstream automatizados em vigor com base no status `Existing`. Se esse for o seu caso, revise suas integrações downstream. Caso se interesse em identificar perfis recém-qualificados além de um determinado período, considere usar uma combinação dos status `Realized` e `lastQualificationTime` no mapa de associação a segmentos. Para obter mais informações, entre em contato com o representante da Adobe. |

{style="table-layout:auto"}

Para obter mais informações sobre o [!DNL Segmentation Service], consulte a [Visão geral de segmentação](../../segmentation/home.md).

## Origens {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e permite estruturar, rotular e aprimorar esses dados usando os serviços da Experience Platform. É possível assimilar dados de várias origens, como aplicativos da Adobe, do armazenamento na nuvem, um software de terceiros e do seu sistema de CRM.

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de ingestão e gerenciar a taxa de transferência de ingestão de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Suporte à API para filtrar dados em nível de linha para origens do Salesforce CRM. | Use operadores lógicos e de comparação para filtrar dados no nível da linha para origens do Salesforce CRM. Leia o manual sobre [filtragem de dados de uma origem usando a API](../../sources/tutorials/api/filter.md) para obter mais informações. |
| Disponibilidade beta da transmissão do Shopify | A [Origem de Transmissão do Shopify](../../sources/connectors/ecommerce/shopify-streaming.md) agora está disponível na versão beta. Use a origem de Transmissão do Shopify para transmitir os dados da conta de seus parceiros do Shopify para a Experience Platform. |
| Disponibilidade geral da integração do OneTrust | A [Origem de integração do OneTrust](../../sources/connectors/consent-and-preferences/onetrust.md) agora está disponível para todos(as). Use a origem de Integração do OneTrust para trazer dados de consentimento e preferências da sua conta de Integração do OneTrust para a Experience Platform. |

{style="table-layout:auto"}

Para saber mais sobre origens, leia a [visão geral de origens](../../sources/home.md).
