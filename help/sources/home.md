---
keywords: Experience Platform;início;tópicos populares;conectores de origem;conector de origem;fontes;fontes de dados;fonte de dados;conexão da fonte de dados
solution: Experience Platform
title: Visão geral dos Source Connectors
description: A Adobe Experience Platform permite a assimilação de dados de fontes externas, além de permitir estruturar, rotular e aprimorar os dados recebidos por meio dos serviços da Experience Platform. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: fac942a469f61461b5a14d9be5b9a39d921c6b25
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 11%

---

# Visão geral dos conectores do Source

A Adobe Experience Platform permite a assimilação de dados de fontes externas, além de permitir estruturar, rotular e aprimorar os dados recebidos por meio dos serviços da Experience Platform. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamentos baseados na nuvem, bancos de dados e muitas outras.

O [!DNL Flow Service] é usado para coletar e centralizar dados do cliente de várias fontes diferentes na Experience Platform. O serviço fornece uma interface de usuário e API RESTful que permite configurar conexões de origem com vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar seus sistemas de terceiros, definir tempos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

Com o Experience Platform, você pode centralizar os dados coletados de fontes diferentes e usar os insights obtidos com eles para fazer mais.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

>[!BEGINSHADEBOX]

## Fontes criadas pela Adobe e criadas por parceiros {#adobe-and-partner-built-sources}

Alguns dos conectores no catálogo de fontes do Experience Platform são criados e mantidos pela Adobe, enquanto outros são criados e mantidos por empresas parceiras usando o [SDK de Fontes](/help/sources/sources-sdk/overview.md). Uma observação na parte superior da página de documentação para cada conector criado pelo parceiro chama se uma origem é criada e mantida pelo parceiro. Por exemplo, o [conector Amazon S3](/help/sources/connectors/cloud-storage/s3.md) é criado pela Adobe, enquanto o [conector RainFocus](/help/sources/connectors/analytics/rainfocus.md) é criado e mantido pela equipe RainFocus.

Para conectores criados e mantidos pelo parceiro, isso significa que os problemas com o conector podem precisar ser resolvidos pela equipe do parceiro (método de contato fornecido na observação na página de documentação). No caso de problemas com conectores criados e mantidos pela Adobe, entre em contato com o representante da Adobe ou com o Atendimento ao cliente.

>[!ENDSHADEBOX]

## Catálogo de origens

Leia as seções a seguir para obter uma lista de todas as fontes disponíveis no catálogo de fontes.

### aplicativos Adobe {#adobe-applications}

O Experience Platform permite que os dados sejam assimilados de outros aplicativos da Adobe, incluindo o Adobe Analytics e o Adobe Audience Manager. Leia os seguintes documentos relacionados para obter mais informações:

- [Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
   - [Criar uma conexão de origem do Adobe Audience Manager na interface](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Dados de classificações do Adobe Analytics](connectors/adobe-applications/classifications.md)
   - [Criar uma conexão de fonte de dados do Adobe Analytics Classifications na interface](./tutorials/ui/create/adobe-applications/classifications.md)
- [Dados do conjunto de relatórios do Adobe Analytics](connectors/adobe-applications/analytics.md)
   - [Criar uma conexão de origem do Adobe Analytics na interface](./tutorials/ui/create/adobe-applications/analytics.md)
- [Adobe Campaign Managed Cloud Services](connectors/adobe-applications/campaign.md)
   - [Criar uma conexão de origem do Adobe Campaign Managed Cloud Services na interface](./tutorials/ui/create/adobe-applications/campaign.md)
- [Adobe Commerce](connectors/adobe-applications/commerce.md)
- [Coleta de dados do Adobe](connectors/adobe-applications/data-collection.md)
   - [Criar uma conexão de origem de atributos do cliente na interface](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage]](connectors/adobe-applications/marketo/marketo.md)
   - [Criar uma conexão de origem  [!DNL Marketo Engage]  na interface](./tutorials/ui/create/adobe-applications/marketo.md)
   - [Criar uma conexão de origem e um fluxo de dados  [!DNL Marketo Engage]  para dados de atividade personalizados](./tutorials/ui/create/adobe-applications/marketo-custom-activities.md)

### Fontes empresariais avançadas {#advanced-enterprise-sources}

As fontes a seguir estão disponíveis somente para clientes do [Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).

| Fonte | Categoria | Tipo de assimilação | Nuvem |
| --- | --- | --- | --- |
| [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md) | Armazenamento na nuvem | Transmissão | Azure, AWS |
| [[!DNL Amazon Redshift]](connectors/databases/redshift.md) | Banco de dados | Lote | Azure, AWS |
| [[!DNL Azure Databricks]](connectors/databases/databricks.md) | Banco de dados | Lote | Azure |
| [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md) | Armazenamento na nuvem | Transmissão | Azure, AWS |
| [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md) | Banco de dados | Lote | Azure |
| [[!DNL Google BigQuery]](connectors/databases/bigquery.md) | Banco de dados | Lote | Azure, AWS |
| [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md) | Armazenamento na nuvem | Transmissão | Azure |
| [[!DNL Snowflake]](connectors/databases/snowflake-streaming.md) | Banco de dados | Transmissão | Azure, AWS |
| [[!DNL Snowflake]](connectors/databases/snowflake.md) | Banco de dados | Lote | Azure, AWS |

{style="table-layout:auto"}

### Advertising {#advertising}

Você pode usar as seguintes fontes para assimilar dados de publicidade na Experience Platform.

| Fonte | Tipo de assimilação | Nuvem |
| --- | --- | --- |
| [Anúncios do Google](connectors/advertising/ads.md) | Lote | Azure |

{style="table-layout:auto"}

### Analytics {#analytics}

Você pode usar as seguintes fontes para assimilar dados de análise na Experience Platform.

| Fonte | Tipo de assimilação | Nuvem |
| --- | --- | --- |
| [[!DNL Mixpanel]](connectors/analytics/mixpanel.md) | Lote | Azure |
| [[!DNL Pendo]](connectors/analytics/pendo-webhook.md) | Transmissão | Azure |
| [[!DNL RainFocus]](connectors/analytics/rainfocus.md) | Transmissão | Azure |

{style="table-layout:auto"}

### Armazenamento na nuvem {#cloud-storage}

As fontes de armazenamento na nuvem podem trazer seus próprios dados para a Experience Platform sem a necessidade de baixar, formatar ou carregar. Os dados assimilados podem ser formatados como XDM JSON, XDM Parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho Origens usando a interface do usuário. Consulte os seguintes documentos relacionados para obter mais informações:

Você pode usar as seguintes fontes para assimilar dados de armazenamento na nuvem na Experience Platform.

| Fonte | Tipo de assimilação | Nuvem |
| --- | --- | --- |
| [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md) | Lote | Azure |
| [[!DNL Azure Blob Storage]](connectors/cloud-storage/blob.md) | Lote | Azure |
| [[!DNL Amazon S3]](connectors/cloud-storage/s3.md) | Lote | Azure, AWS |
| [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md) | Lote | Azure |
| [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md) | Lote | Azure |
| [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md) | Lote | Azure, AWS |
| [[!DNL FTP]](connectors/cloud-storage/ftp.md) | Lote | Azure |
| [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md) | Lote | Azure |
| [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md) | Lote | Azure |
| [[!DNL SFTP]](connectors/cloud-storage/sftp.md) | Lote | Azure |

{style="table-layout:auto"}

### Consentimento e preferências {#consent}

Você pode usar as seguintes fontes para assimilar dados de consentimento e preferências da Experience Platform.

| Fonte | Tipo de assimilação | Nuvem |
| --- | --- | --- |
| [[!DNL Didomi]](../sources/connectors/consent-and-preferences/didomi.md) | Transmissão | Azure |
| [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md) | Lote | Azure |

{style="table-layout:auto"}

### Gerenciamento de Relacionamento com o Cliente (CRM) {#customer-relationship-management}

Os sistemas de CRM fornecem dados que podem ajudar a criar relacionamentos com o cliente, o que, por sua vez, cria fidelidade e impulsiona a retenção do cliente. A Experience Platform oferece suporte para assimilação de dados do CRM de [!DNL Microsoft Dynamics 365] e [!DNL Salesforce]. Consulte os seguintes documentos relacionados para obter mais informações:

Você pode usar as seguintes fontes para assimilar dados do CRM para o Experience Platform.

| Fonte | Tipo de assimilação | Nuvem |
| --- | --- | --- |
| [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md) | Lote | Azure |
| [[!DNL Salesforce]](connectors/crm/salesforce.md) | Lote | Azure, AWS |
| [[!DNL SugarCRM]](connectors/crm/sugarcrm.md) | Lote | Azure |
| [[!DNL Veeva CRM]](connectors/crm/veeva.md) | Lote | Azure |

{style="table-layout:auto"}

### Sucesso do cliente {#customer-success}

Você pode usar as seguintes fontes para assimilar dados de sucesso do cliente na Experience Platform.

| Fonte | Tipo de assimilação | Nuvem |
| --- | --- | --- |
| [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md) | Lote | Azure |
| [[!DNL ServiceNow]](connectors/customer-success/servicenow.md) | Lote | Azure |
| [[!DNL Zendesk]](connectors/customer-success/zendesk.md) | Lote | Azure |

{style="table-layout:auto"}

### Banco de dados {#database}

O Experience Platform oferece suporte para assimilação de dados de um banco de dados de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

Você pode usar as seguintes fontes para assimilar dados do banco de dados para o Experience Platform.

| Fonte | Tipo de assimilação | Nuvem |
| --- | --- | --- |
| [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md) | Lote | Azure |
| [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md) | Lote | Azure |
| [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md) | Lote | Azure |
| [[!DNL Azure Table Storage]](connectors/databases/ats.md) | Lote | Azure |
| [[!DNL GreenPlum]](connectors/databases/greenplum.md) | Lote | Azure |
| [[!DNL HP Vertica]](connectors/databases/hp-vertica.md) | Lote | Azure |
| [[!DNL IBM DB2]](connectors/databases/ibm-db2.md) | Lote | Azure |
| [[!DNL MariaDB]](connectors/databases/mariadb.md) | Lote | Azure |
| [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md) | Lote | Azure |
| [[!DNL MySQL]](connectors/databases/mysql.md) | Lote | Azure, AWS |
| [[!DNL Oracle]](connectors/databases/oracle.md) | Lote | Azure, AWS |
| [[!DNL PostgreSQL]](connectors/databases/postgres.md) | Lote | Azure, AWS |
| [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md) | Lote | Azure |

{style="table-layout:auto"}

### Parceiros de dados e identidade {#data-partner}

Você pode usar as seguintes fontes para assimilar dados e identificar dados de parceiros na Experience Platform.

| Fonte | Tipo de assimilação | Nuvem |
| --- | --- | --- |
| [[!DNL Acxiom Data Ingestion]](connectors/data-partners/acxiom-data-ingestion.md) | Lote | Azure |
| [[!DNL Acxiom Prospecting Data Import]](connectors/data-partners/acxiom-prospecting-data-import.md) | Lote | Azure |
| [[!DNL Algolia User Profiles]](connectors/data-partners/algolia-user-profiles.md) | Lote | Azure |
| [[!DNL Bombora Intent]](connectors/data-partners/bombora.md) | Lote | Azure |
| [[!DNL Demandbase Intent]](connectors/data-partners/demandbase.md) | Lote | Azure |
| [[!DNL Merkury Enterprise Identity Resolution]](connectors/data-partners/merkury.md) | Lote | Azure |

{style="table-layout:auto"}

### comércio eletrônico {#ecommerce}

Você pode usar as seguintes fontes para assimilar dados de comércio eletrônico na Experience Platform.

| Fonte | Tipo de assimilação | Nuvem |
| --- | --- | --- |
| [[!DNL SAP Commerce]](connectors/ecommerce/sap-commerce.md) | Lote | Azure |
| [[!DNL Shopify]](connectors/ecommerce/shopify.md) | Lote | Azure |
| [[!DNL Shopify]](connectors/ecommerce/shopify-streaming.md) | Transmissão | Azure |

{style="table-layout:auto"}

### Sistema local {#local-system}

Você pode usar as seguintes fontes para assimilar dados do sistema local para o Experience Platform.

| Fonte | Tipo de assimilação | Nuvem |
| --- | --- | --- |
| [Carregamento de arquivo local](connectors/local-system/local-file-upload.md) | Lote | Azure |

{style="table-layout:auto"}

### Fidelidade {#loyalty}

Você pode usar as seguintes fontes para assimilar dados do programa de fidelidade da Experience Platform.

| Fonte | Tipo de assimilação | Nuvem |
| --- | --- | --- |
| [[!DNL Capillary Streaming Events]](connectors/loyalty/capillary.md) | Transmissão | Azure |

{style="table-layout:auto"}

### Automação de marketing {#marketing-automation}

Você pode usar as seguintes fontes para assimilar dados de automação de marketing para o Experience Platform.

| Fonte | Tipo de assimilação | Nuvem |
| --- | --- | --- |
| [[!DNL Braze]](connectors/marketing-automation/braze.md) | Transmissão | Azure |
| [[!DNL Chatlio]](connectors/marketing-automation/chatlio-webhook.md) | Transmissão | Azure |
| [[!DNL Customer.io]](connectors/marketing-automation/customerio-webhook.md) | Transmissão | Azure |
| [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md) | Lote | Azure |
| [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md) | Lote | Azure |
| [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md) | Lote | Azure |
| [[!DNL Oracle NetSuite]](connectors/marketing-automation/oracle-netsuite.md) | Lote | Azure |
| [[!DNL PathFactory]](connectors/marketing-automation/pathfactory.md) | Lote | Azure |
| [[!DNL Relay Connector]](tutorials/ui/create/marketing-automation/relay-connector.md) | Transmissão | Azure |
| [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md) | Lote | Azure, AWS |

{style="table-layout:auto"}

### Pagamentos {#payments}

Você pode usar as seguintes fontes para assimilar dados de pagamentos para o Experience Platform.

| Fonte | Tipo de assimilação | Nuvem |
| --- | --- | --- |
| [[!DNL Square]](connectors/payments/square.md) | Lote | Azure |
| [[!DNL Stripe]](connectors/payments/stripe.md) | Lote | Azure |

{style="table-layout:auto"}

### Transmissão {#streaming}

Você pode usar as seguintes fontes para transmitir dados para o Experience Platform.

| Fonte | Tipo de assimilação | Suporte na nuvem |
| --- | --- | --- |
| [[!DNL HTTP API]](connectors/streaming/http.md) | Transmissão | Azure, AWS |

{style="table-layout:auto"}

### Protocolos {#protocols}

Você pode usar as seguintes fontes para assimilar dados de protocolo na Experience Platform.

| Fonte | Tipo de assimilação | Suporte na nuvem |
| --- | --- | --- |
| [[!DNL Generic OData]](connectors/protocols/odata.md) | Lote | Azure |
| [[!DNL Generic REST API]](connectors/protocols/generic-rest.md) | Lote | Azure |

{style="table-layout:auto"}

## Controle de acesso para fontes na assimilação de dados

As permissões para fontes na assimilação de dados podem ser gerenciadas no Adobe Admin Console. Você pode acessar permissões por meio da guia **[!UICONTROL Permissions]** em um perfil de produto específico. No painel **[!UICONTROL Edit Permissions]**, você pode acessar as permissões relacionadas às origens por meio da entrada de menu **[!UICONTROL data ingestion]**. A permissão **[!UICONTROL View Sources]** concede acesso somente leitura às fontes disponíveis na guia **[!UICONTROL Catalog]** e às fontes autenticadas na guia **[!UICONTROL Browse]**, enquanto a permissão **[!UICONTROL Manage Sources]** concede acesso total às fontes de leitura, criação, edição e desabilitação.

A tabela a seguir descreve como a interface do usuário se comporta com base em diferentes combinações dessas permissões:

| Nível de permissão | Descrição |
| ---- | ----|
| **[!UICONTROL View Sources]** Em | Conceda acesso somente leitura às origens em cada tipo de origem na guia Catálogo, bem como nas guias Procurar, Contas e Fluxo de dados. |
| **[!UICONTROL Manage Sources]** Em | Além das funções incluídas em **[!UICONTROL View Sources]**, concede acesso às opções **[!UICONTROL Connect Source]** em **[!UICONTROL Catalog]** e **[!UICONTROL Select Data]** em **[!UICONTROL Browse]**. **[!UICONTROL Manage Sources]** também permite habilitar ou desabilitar **[!UICONTROL DataFlows]** e editar seus cronogramas. |
| **[!UICONTROL View Sources]** Desativado e **[!UICONTROL Manage Sources]** Desativado | Revogar todo o acesso a origens. |

Para obter mais informações sobre as permissões disponíveis concedidas por meio das Permissões do Adobe, leia a [visão geral do controle de acesso](../access-control/home.md).

### Controle de acesso baseado em atributos

O controle de acesso baseado em atributos no Adobe Experience Platform permite que os administradores controlem o acesso a objetos e/ou recursos específicos com base em atributos.

Com o controle de acesso baseado em atributos, é possível aplicar configurações de mapeamento a campos aos quais você tem permissões. Além disso, não é possível assimilar dados em um conjunto de dados se você não tiver acesso a todos os campos no conjunto de dados.

#### Suporte para controle de acesso baseado em atributos nas origens

>[!TIP]
>
>O controle de acesso baseado em atributos funciona da seguinte maneira: **funções** são criadas para categorizar os tipos de usuários que interagem com sua instância do Experience Platform. **Rótulos** são aplicados a **funções** para designar o acesso a essa função específica. **Rótulos** também são aplicados a recursos como campos de esquema e segmentos. Para que um usuário tenha acesso a determinados campos e segmentos de esquema, ele deve ser adicionado a *uma função com o mesmo rótulo atribuído ao recurso consultado*. Para obter mais informações, leia o [manual completo sobre controle de acesso baseado em atributos](../access-control/abac/end-to-end-guide.md).

- Aplique rótulos a campos de esquema para definir o acesso a campos de esquema específicos na organização. Uma vez estabelecido o acesso a campos de esquema específicos, os usuários só poderão criar mapeamentos para os campos aos quais têm acesso.
- Os usuários sem as funções apropriadas não poderão criar ou atualizar fluxos de dados com mapeamentos que envolvam campos de esquema inacessíveis. Além disso, os usuários não autorizados não podem atualizar, excluir, ativar ou desativar fluxos de dados existentes com campos de esquema inacessíveis.
- Além disso, um fluxo de dados deve ter exatamente a mesma ID e versão do esquema em seu mapeamento, conjunto de dados de destino e conexão de destino. Isso se aplica aos esquemas XDM padrão e aos esquemas relacionais.

>[!NOTE]
>
>Os esquemas relacionais têm requisitos adicionais, incluindo campos de chave primária e identificador de versão. Para obter mais informações, consulte a [visão geral do esquema relacional](../xdm/schema/relational.md).

Para obter mais informações sobre o controle de acesso baseado em atributos, leia a [visão geral do controle de acesso baseado em atributos](../access-control/abac/overview.md).

## Termos e condições {#terms-and-conditions}

Ao usar qualquer uma das Fontes rotuladas como beta (&quot;Beta&quot;), você reconhece que a Beta é fornecida ***&quot;no estado em que se encontra&quot; sem garantias de qualquer tipo***.

A Adobe não tem nenhuma obrigação de manter, corrigir, atualizar, alterar, modificar ou oferecer suporte à Beta. Você é aconselhado a usar materiais informativos e não se basear, de forma alguma, no funcionamento ou no desempenho corretos desses Beta e/ou dos materiais que os acompanham. O Beta é considerado Informações confidenciais da Adobe.

Qualquer &quot;Feedback&quot; (informação sobre o Beta incluindo, mas não se limitando a, problemas ou defeitos encontrados durante o uso do Beta, sugestões, melhorias e recomendações) fornecido por Você ao Adobe é atribuído ao Adobe, incluindo todos os direitos, cargos e interesses no e no Feedback.

Envie Feedback Aberto ou crie um Tíquete de Suporte para compartilhar suas sugestões ou relatar um erro, buscar um aprimoramento de recurso.
