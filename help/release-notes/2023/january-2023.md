---
title: Notas de versão da Adobe Experience Platform em janeiro de 2023
description: As notas de versão de janeiro de 2023 para o Adobe Experience Platform.
source-git-commit: 3fd3e96d5db6b1e63df338efe383d209690eb1f6
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 6%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 25 de janeiro de 2023**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Coleta de dados](#data-collection)
- [Experience Data Model (XDM)](#xdm)
- [Fontes](#sources)

## Coleta de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente e enviá-los para a Adobe Experience Platform Edge Network, onde podem ser enriquecidos, transformados e distribuídos para destinos Adobe ou não-Adobe.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Nova tela inicial | A página inicial da interface do usuário da coleta de dados foi atualizada para incluir informações úteis sobre integração e links para simplificar a produtividade. Isso inclui:<ol><li>Documentação e fluxos de trabalho recomendados para começar</li><li>Propriedades, regras e elementos de dados recentes</li><li>Extensões populares</li><li>Novas atualizações de extensão com um recurso de instalação rápida</li></ol> |
| Enviar dados para [!DNL Google Ads] uso do encaminhamento de eventos | Agora você pode usar o [[!DNL Google Ads Enhanced Conversions] Extensão da API](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) para encaminhamento de eventos, combinado com [Segredo do Google Oauth 2](../../tags/ui/event-forwarding/secrets.md#google-oauth2), para enviar dados do lado do servidor para o [!DNL Google Ads] em tempo real. |

{style=&quot;table-layout:auto&quot;}

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Adobe Experience Platform. Ao seguir os padrões XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de uma maneira mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Desativar valores sugeridos para campos de cadeia de caracteres | Agora você pode [desativar valores sugeridos individuais para campos de cadeia de caracteres](../../xdm/ui/fields/enum.md) no [!UICONTROL Esquemas] espaço de trabalho, incluindo aqueles de componentes padrão. Esse recurso está disponível somente para campos com valores sugeridos e não é compatível com restrições de enumeração. |

**Novos componentes XDM**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Classe | [[!UICONTROL Conversão]](https://github.com/adobe/xdm/blob/master/components/classes/conversion.schema.json) | Uma classe para rastrear dados de conversão como conversões de moeda. |
| Grupo de campos | [[!UICONTROL Detalhes da Taxa de Conversão de Moeda]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/conversion/currency-conversion-details.schema.json) | Um grupo de campos para a variável [!UICONTROL Conversão] , capturando detalhes adicionais relacionados à conversão de moeda. |
| Grupo de campos | [[!UICONTROL Mapa de resultados de avaliação de políticas de consentimento com metadados]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResultsv2.schema.jsonn) | Captura detalhes para o resultado da avaliação de várias políticas de consentimento, incluindo informações de metadados sobre entradas e saídas da política de consentimento. |

**Componentes XDM atualizados**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Tipo de dados | [[!UICONTROL Informações de detalhes de publicidade]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | O `ID` foi renomeado para `name`e as `name` campo agora `friendlyName`. |
| Tipo de dados | [[!UICONTROL Detalhes da proposta de decisão]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-detail.schema.json) | Adicionado um `selectionStrategy` campo que captura os detalhes de uma estratégia de seleção. |
| Grupo de campos | [[!UICONTROL Evento de experiência - Interações de proposta]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/experienceevent-proposition-interaction.schema.json) | O grupo de campos agora é compatível com o [!UICONTROL Evento de etapa de Jornada] classe . |
| Tipo de dados | [[!UICONTROL Informações de detalhes do erro]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | O `ID` foi renomeado para `name`. |
| Tipo de dados | [[!UICONTROL Informações da mídia]](https://github.com/adobe/xdm/blob/master/components/datatypes/media.schema.json) | Reversão de uma alteração no padrão para a propriedade de segmento de vídeo. |
| Tipo de dados | [[!UICONTROL Informações de detalhes de dados de Qoe]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Remoção do `droppedFrameCount` campo. |
| Tipo de dados | [[!UICONTROL Informações de detalhes da sessão]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Renomeada a função `isAuthorized` campo para `authorized`e atualizou seu `type` para uma string quando era anteriormente uma booleana. |
| Tipo de dados | [[!UICONTROL Envio]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Adição de vários novos campos: `shipDate`, `trackingNumber`e `trackingURL`. |
| Grupo de campos | [[!UICONTROL Campos de entidade AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-mixins.schema.json) | Adição de vários novos campos: `journeyNodeID`, `journeyNodeName`e `journeyModeType`. |
| Grupo de campos | [[!UICONTROL Evento de experiência do consumidor]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/experienceevent-consumer.schema.json) | O grupo de campos agora também é compatível com o [!UICONTROL Métricas de resumo] classe . |
| Grupo de campos | [[!UICONTROL Acionadores do produto]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | O `productTriggers` agora está aninhado em um `weather` objeto. |
| Grupo de campos | [[!UICONTROL Acionadores relativos]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | O `relativeTriggers` agora está aninhado em um `weather` objeto. |
| Grupo de campos | [[!UICONTROL Acionadores graves]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | O `severeTriggers` agora está aninhado em um `weather` objeto. |
| Grupo de campos | [[!UICONTROL Acionadores do tempo]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | O `weatherTriggers` agora está aninhado em um `weather` objeto. |
| Grupo de campos | [[!UICONTROL Contas Comerciais Relacionadas ao XDM]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account/related-accounts.schema.json) | O grupo de campos agora está estável. |

{style=&quot;table-layout:auto&quot;}

Para obter mais informações sobre o XDM na Platform, consulte o [Visão geral do sistema XDM](../../xdm/home.md).

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e permite estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

| Recurso | Descrição |
| --- | --- |
| Permitir acesso do usuário às subpastas de fontes de armazenamento na nuvem | Agora é possível definir o acesso a uma subpasta específica da fonte de armazenamento na nuvem ao criar uma nova conta. Depois de criados, os usuários só poderão acessar dados da subpasta permitida. Esse recurso está disponível nas seguintes fontes de armazenamento em nuvem: [Armazenamento Azure Blob](../../sources/connectors/cloud-storage/blob.md), [Armazenamento em nuvem Google](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md)e [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Disponibilidade beta de [!DNL SugarCRM] | [!DNL SugarCRM] Agora, as fontes estão disponíveis em beta. Use o [!DNL SugarCRM Accounts & Contacts] e [!DNL SugarCRM Events] fontes para trazer dados de [!DNL SugarCRM] para o Experience Platform. Para obter mais informações, leia a [[!DNL SugarCRM] visão geral](../../sources/connectors/crm/sugarcrm.md). |
