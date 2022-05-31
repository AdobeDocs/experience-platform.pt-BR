---
title: Notas de versão da Adobe Experience Platform
description: As notas de versão mais recentes do Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 1b417935d557f7d58039c508544ed768f6ad1cc4
workflow-type: tm+mt
source-wordcount: '1719'
ht-degree: 6%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 25 de maio de 2022**

<!-- New features in Adobe Experience Platform: -->

<!-- - [Attribute-based access control](#abac) -->
<!-- - [Data hygiene](#hygiene) -->

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Alertas](#alerts)
- [Logs de auditoria](#audit-logs)
- [Painéis](#dashbaords)
- [Coleta de dados](#data-collection)
<!-- - [Data Governance](#data-governance) -->
- [Preparação de dados](#data-prep)
- [Destinos](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Serviço de query](#query-service)
- [Fontes](#sources)

## Alertas {#alerts}

O Experience Platform permite assinar alertas baseados em eventos para várias atividades da plataforma. É possível assinar diferentes regras de alerta por meio do [!UICONTROL Alertas] na interface do usuário da plataforma e pode optar por receber mensagens de alerta na própria interface do usuário ou por meio de notificações por email.

**Recursos atualizados**

| Recurso | Regra de alerta | Descrição |
| --- | --- | --- |
| Nova regra de alerta | A taxa de página ignorada excede o limite | Agora você pode usar o alerta para receber notificações quando o fluxo de dados de origens exceder os limites de identidades. Consulte a visão geral em [regras de alerta](../../observability/alerts/rules.md) para obter a lista atualizada de tipos de alertas. |

{style=&quot;table-layout:auto&quot;}


<!-- ## Attribute-based access control {#abac}

>[!IMPORTANT]
>
>Attribute-based access control is currently available in a limited release for US-based healthcare customers. This capability will be available to all Real-time Customer Data Platform customers once it is fully released.

Attribute-based access control is a capability of Adobe Experience Platform that enables administrators to control access to specific objects and/or capabilities based on attributes. Attributes can be metadata added to an object, such as a label added to a schema field or segment. An administrator defines access policies that include attributes to manage user access permissions.

Through attribute-based access control, administrators of your organization can control users’ access to both sensitive personal data (SPD) and personally identifiable information (PII) across all Platform workflows and resources. Administrators can define user roles that have access only to specific fields and data that correspond to those fields.

| Feature | Description |
| --- | --- |
| Attribute-based access control | Attribute-based access control allows you to label Experience Data Model (XDM) schema fields with labels that define organizational or data usage scopes. In parallel, administrators can use the user and role administration interface to define access policies covering XDM schema fields and better manage the access given to users or groups of users (internal, external, or third-party users). Additionally, attribute-based access control allows administrators to manage access to specific segments. |
| Permissions | Permissions is the area of Experience Cloud where administrators can define user roles and access policies to manage access permissions for features and objects within a product application. Through Permissions, you can create and manage roles, as well as assign the desired resource permissions for these roles. Permissions also allow you to manage the labels, sandboxes, and users associated with a specific role. For more information, see the [Permissions UI guide](../../access-control/abac/ui/browse.md). |

For more information on attribute-based access control, see the [attribute-based access control overview](../../access-control/abac/overview.md). -->

<!-- ## Data hygiene {#hygiene}

Experience Platform provides a suite of data hygiene capabilities that allow you manage your stored data through programmatic deletions of consumer records and datasets. Using either the [!UICONTROL Data Hygiene] workspace in the UI or through calls to the Data Hygiene API, you can manage your data stores to ensure that information is used as expected, is updated when incorrect data needs fixing, and is deleted when organizational policies deem it necessary.

>[!IMPORTANT]
>
>Data hygiene capabilities are currently only available for organizations that have purchased the Adobe Shield for Healthcare add-on offering.

**New features**

| Feature | Description |
| --- | --- |
| Consumer deletion | [Delete consumer records](../../hygiene/ui/delete-consumer.md) from the data lake and Profile store based on primary identity data. |
| Time to live (TTL) for datasets | [Schedule TTLs](../../hygiene/ui/ttl.md) for Platform datasets.  |

For more information on audit logs in Platform, refer to the [data hygiene overview](../../hygiene/home.md). -->

## Logs de auditoria {#audit-logs}

O Experience Platform permite auditar a atividade do usuário para vários serviços e recursos. Os logs de auditoria fornecem informações sobre quem fez o quê e quando.

**Recursos atualizados**

| Recurso | Nome | Descrição |
| --- | --- | --- |
| Recursos adicionados | <ul><li> Política de controle de acesso </li><li> Função </li><li> Logs de auditoria </li><li> Ordem de serviço </li><li> Namespace de identidade </li><li> Gráfico de identidade </li><li> Consulta </li><li> Conjunto de dados </li><li> Fluxo de dados de origem </li></ul> | Os recursos do log de auditoria são registrados automaticamente conforme a atividade ocorre. Se o recurso estiver ativado, não é necessário ativar manualmente a coleta de log. |

{style=&quot;table-layout:auto&quot;}

Para obter mais informações sobre logs de auditoria na Platform, consulte [visão geral dos logs de auditoria](../../landing/governance-privacy-security/audit-logs/overview.md).

## Painéis {#dashboards}

O Adobe Experience Platform fornece vários painéis através dos quais você pode visualizar informações importantes sobre os dados de sua organização, conforme capturados durante os instantâneos diários.

### Painéis de perfis

O painel de perfis exibe um instantâneo dos dados do atributo (registro) que sua organização tem na Loja de perfis no Experience Platform.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Sobreposição de público-alvo por widget de política de mesclagem | Esse widget exibe a cruz visual das definições de segmento e permite otimizar a estratégia de segmentação ao estudar as semelhanças entre as definições de segmento. |
| Perfis contam a tendência de alteração por dispositivo de identidade | Esses widgets ajudam você a gerenciar suas necessidades de ativação de destino demonstrando o padrão de crescimento de perfis filtrados pela identidade necessária. |

{style=&quot;table-layout:auto&quot;}

Para obter mais informações sobre perfis, consulte o [documentação do painel de perfis](../../dashboards/guides/profiles.md).

### Painéis de destinos

O painel de destinos exibe um instantâneo dos destinos que sua organização habilitou no Experience Platform.

| Recurso | Descrição |
| --- | --- |
| Públicos-alvo ativados por widget de destino | Este widget ajuda você a entender rapidamente o valor dos destinos com base no número de públicos-alvo ativados. Também fornece acesso fácil a informações mais detalhadas sobre seus segmentos que foram mapeados para o destino. |

{style=&quot;table-layout:auto&quot;}

Para obter mais informações sobre destinos, consulte o [documentação do painel de destinos](../../dashboards/guides/destinations.md).

### Painéis de segmentos

O painel de segmentos fornece uma interface do usuário através da qual você pode visualizar informações importantes sobre seus segmentos, conforme capturado durante um instantâneo diário.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Widget de sobreposição de público | Esse widget permite otimizar sua estratégia de segmentação ao visualizar as semelhanças nos resultados das definições de segmento. |

{style=&quot;table-layout:auto&quot;}

Para obter mais informações sobre segmentos, consulte o [documentação do painel de segmentos](../../dashboards/guides/segments.md).

## Coleta de dados {#data-collection}

O Experience Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente e enviá-los para a Adobe Experience Platform Edge Network, onde podem ser enriquecidos, transformados e distribuídos para destinos Adobe ou não-Adobe.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Copiar datastreams | [Criar uma cópia de um armazenamento de dados existente](../../edge/datastreams/overview.md#copy) e ajuste sua configuração conforme necessário, evitando a necessidade de começar do zero. |
| Importar regras de mapeamento do conjunto de dados | Ao configurar a Preparação de dados para a Coleta de dados, é possível [importar as regras de mapeamento de um conjunto de dados existente](../../edge/datastreams/data-prep.md#import-mapping) em vez de configurar cada mapeamento de campo manualmente. |
| Suporte ao mapeamento de fluxo de dados para SDK móvel | Agora você pode configurar a Preparação de dados para a coleta de dados em conjuntos de dados destinados ao uso com o SDK do Experience Platform Mobile. |
| Suporte para mapeamento de fluxo de dados para objetos XDM | Mapear objetos XDM além de objetos da camada de dados ao [configuração da Preparação de dados para a Coleta de dados](../../edge/datastreams/data-prep.md#select-data). |
| Integração com fluxos de dados | Use o catálogo de fontes no Platform para acessar seus dados na Rede de borda da plataforma, incluindo Preparação de dados para coleta de dados e suporte aprimorado para avisos de Preparação de dados. Consulte a [Visão geral da fonte de coleta de dados do Adobe](../../sources/connectors/adobe-applications/data-collection.md) para obter mais informações. |

Para obter mais informações sobre a coleta de dados no Platform, consulte o [visão geral da coleta de dados](../../collection/home.md).

<!-- ## Data Governance {#governance}

Adobe Experience Platform Data Governance is a series of strategies and technologies used to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data usage. It plays a key role within [!DNL Experience Platform] at various levels, including cataloging, data lineage, data usage labeling, data access policies, and access control on data for marketing actions.

**New features**

| Feature | Description | 
| ------- | ----------- |
| Consent policy enforcement (limited availability) | If your organization has purchased the Adobe Shield for Healthcare add-on offering, you can now [create consent policies](../../data-governance/policies/user-guide.md#consent-policy) to automatically [enforce customer consents and preferences in segment participation](../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation). |

{style="table-layout:auto"}

See the [Data Governance overview](../../data-governance/home.md) for more information on the service. -->

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] O permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Recursos atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Erros de dados localizados | [!DNL Data Prep] agora localiza todos os erros de transformação para o nível do atributo (anteriormente no nível da linha). Os fluxos de dados agora assimilarão linhas parciais preenchidas com colunas que não têm erros de transformação, em vez de ignorar as linhas completas. |
| Transmitir upserts para [!DNL Profile Service] | Autores de fluxo com [!DNL Data Prep] para enviar atualizações de linha parciais ao Serviço de perfil do usando o [[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md), [[!DNL Azure Event Hubs]](../../sources/connectors/cloud-storage/eventhub.md)ou [[!DNL HTTP API]](../../sources/connectors/streaming/http.md) fonte. Consulte o guia sobre [upserts de transmissão](../../data-prep/upserts.md) para obter mais informações. |

{style=&quot;table-layout:auto&quot;}

<!-- | Attribute-based access control in [!DNL Data Prep] | You will now only be able to map attributes that you have access to. Attributes that you do not have access to can not be used in pass-through mappings and calculated fields. For more information, see [attribute-based access control in [!DNL Data Prep]](../../data-prep/home.md). **Note**: Attribute-based access control is currently available in a limited release for US-based healthcare customers. This capability will be available to all Real-time Customer Data Platform customers once it is fully released. | -->

Para obter mais informações sobre [!DNL Data Prep]consulte o [[!DNL Data Prep] visão geral](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, anúncios direcionados e muitos outros casos de uso.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ----------- | ----------- |
| Exportar as qualificações de perfil mais recentes [após a avaliação diária do segmento](../../destinations/ui/activate-batch-profile-destinations.md#export-full-files) | Agora é possível agendar uma exportação de arquivo completa, uma vez ou diariamente, com as últimas qualificações de perfil, após a conclusão da avaliação diária do segmento. |
| ID de conjunto de dados opcional para [Destinos do Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) | Para permitir a personalização do Adobe Target para usuários que não podem implementar o SDK da Web do Experience Platform, a seleção da ID do datastream agora é opcional ao configurar destinos do Adobe Target. Quando não estiver usando um armazenamento de dados, os segmentos exportados do Experience Platform para o Target oferecerão suporte somente à personalização da próxima sessão, enquanto a segmentação de borda está desativada, juntamente com todos os [casos de uso](../../destinations/ui/configure-personalization-destinations.md) que dependem da segmentação de borda. |

{style=&quot;table-layout:auto&quot;}

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Adobe Experience Platform. Ao seguir os padrões XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de uma maneira mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Novos componentes XDM**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Grupo de campos | [[!UICONTROL Alterar conjunto]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/changeset.schema.json) | Captura alterações em nível de linha de e para conjuntos de dados. Esse grupo de campos pode ser empregado por qualquer classe. |
| Grupo de campos | [[!UICONTROL Chaves de referência]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-reference-keys.schema.json) | Captura chaves de referência para esquemas do ExperienceEvent, permitindo criar relacionamentos com esquemas com base em outras classes. |

{style=&quot;table-layout:auto&quot;}

**Componentes XDM atualizados**

| Tipo de componente | Nome | Atualizar descrição |
| --- | --- | --- |
| Comportamento | [[!UICONTROL Esquema da série cronológica]](https://github.com/surbhi114/xdm/blob/master/components/behaviors/time-series.schema.json) | Atualizado `eventType` para incluir vários novos tipos de evento relacionados à mídia e um caso de uso de entrada de canal da Web para o Adobe Journey Optimizer. |
| Schema global | [[!UICONTROL Destino]](https://github.com/tumulurik/xdm/blob/master/schemas/destinations/destination.schema.json) | Remoção dos valores de enumeração de `xdm:destinationCategory`. |
| Grupo de campos | [[!UICONTROL Status do Registro]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/record-status.schema.json) | Atualização do status do grupo de campos de `experimental` para `stable`. |
| Grupo de campos | (Vários) | Vários grupos de campos B2B foram atualizados para que determinados campos de ID sejam descontinuados em favor de campos do tipo chave que usam a variável [[!UICONTROL Origem B2B]](../../xdm/data-types/b2b-source.md) tipo de dados. Os campos de ID anteriores serão descontinuados em uma atualização futura. Consulte o seguinte [solicitação pull](https://github.com/adobe/xdm/pull/1533/files#diff-720c0bb1d1cbaf622f5656c2a4b62d35830c75f6563794da72a280a6a520fbc1) para obter uma lista completa das alterações nos grupos de campos afetados. |
| Tipo de dados | [[!UICONTROL Detalhes do navegador]](https://github.com/liljenback/xdm/blob/master/components/datatypes/browserdetails.schema.json) | Adição de um novo campo `xdm:userAgentClientHints` que captura informações contextuais sobre o agente do usuário que interage com o navegador. |
| Tipo de dados | [[!UICONTROL Informações da mídia]](https://github.com/lidiaist/xdm/blob/master/components/datatypes/media.schema.json) | Adicionou um `xdm:playhead` para capturar a hora do indicador de reprodução de um conteúdo de mídia. Validação de padrão fixa para `xdm:videoSegment`. |
| Tipo de dados | [[!UICONTROL Classificação]](https://github.com/lidiaist/xdm/blob/master/components/datatypes/external/iptc/rating.schema.json) | `iptc4xmpExt:RatingSourceLink` não é mais um campo obrigatório. |

{style=&quot;table-layout:auto&quot;}

Para obter mais informações sobre o XDM na Platform, consulte o [Visão geral do sistema XDM](../../xdm/home.md).

## Serviço de query {#query-service}

O Serviço de Consulta permite que você use o SQL padrão para consultar dados no Adobe Experience Platform [!DNL data lake]. É possível unir qualquer conjunto de dados da [!DNL data lake] e capture os resultados do query como um novo conjunto de dados para usar nos relatórios, no Data Science Workspace ou para assimilação no Perfil do cliente em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Integração de log de auditoria do Serviço de query | A integração do log de auditoria do Serviço de Consulta fornece registros de ações de usuários relacionadas a consultas para fins de solução de problemas ou adesão a políticas corporativas de gerenciamento de dados e requisitos normativos. Consulte a [documentação de integração de log de auditoria](../../query-service/data-governance/audit-log-guide.md) para obter informações abrangentes |
| ALTERAR construção SQL TABLE | Use o SQL para definir identidades primárias em um conjunto de dados ad hoc. O Serviço de query permite marcar colunas de conjunto de dados como identidades primárias ou secundárias diretamente por meio do SQL usando o `ALTER TABLE` comando. |

{style=&quot;table-layout:auto&quot;}

<!-- For more information on data governance in Query Service, see the [data governance overview](../../query-service/data-governance/overview.md). -->

Para obter mais informações sobre recursos do Serviço de query, consulte o [Visão geral do Serviço de query](../../query-service/home.md)

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

| Recurso | Descrição |
| --- | --- |
| Versão beta de [!DNL Zendesk] source | Use o [!DNL Zendesk] origem para assimilar dados de usuários, agentes e organizações de sua [!DNL Zendesk] instância para [!DNL Profile] enriquecimento. Consulte a [[!DNL Zendesk] visão geral da fonte](../../sources/connectors/customer-success/zendesk.md) para obter mais informações. |
| Disponibilidade geral de B2B [!DNL Microsoft Dynamics] source | Agora você pode usar o [!DNL Microsoft Dynamics] origem para assimilar objetos B2B como contas, oportunidades, campanhas, lista de marketing e membros da lista de marketing. Consulte a [[!DNL Microsoft Dynamics] visão geral da fonte](../../sources/connectors/crm/ms-dynamics.md) para obter mais informações. |
| Suporte para coleta de dados do Adobe | Use o catálogo de fontes para acessar os dados da Coleta de dados da Borda da experiência, incluindo Preparação de dados para coleta de dados e suporte aprimorado a avisos de dados da Preparação de dados. Consulte a [Visão geral da fonte de coleta de dados do Adobe](../../sources/connectors/adobe-applications/data-collection.md) para obter mais informações. |
| Suporte para assimilar arquivos com `ISO-8859-1` codificação | Use o `encoding` parâmetro para assimilar `ISO-8859-1` arquivos codificados com uma fonte de armazenamento em nuvem para a Platform usando o [!DNL Flow Service] API. Consulte o guia sobre [criação de uma conexão de origem de armazenamento em nuvem](../../sources/tutorials/api/collect/cloud-storage.md) para obter mais informações. |

{style=&quot;table-layout:auto&quot;}

<!-- | Attribute-based access control in sources | You can now manage and control access to individual source fields and attributes during ingestion. **Note**: Attribute-based access control is currently available in a limited release for US-based healthcare customers. This capability will be available to all Real-time Customer Data Platform customers once it is fully released.  | -->

Para saber mais sobre fontes, consulte o [visão geral das fontes](../../sources/home.md).
