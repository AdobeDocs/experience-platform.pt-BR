---
keywords: Experience Platform;início;tópicos populares;conectores de origem;conector de origem;fontes;fontes de dados;fonte de dados;conexão da fonte de dados
solution: Experience Platform
title: Visão geral dos Source Connectors
description: O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da Experience Platform. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1557'
ht-degree: 2%

---

# Visão geral dos conectores do Source

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da Experience Platform. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamentos baseados na nuvem, bancos de dados e muitas outras.

O [!DNL Flow Service] é usado para coletar e centralizar dados do cliente de várias fontes diferentes na Experience Platform. O serviço fornece uma interface de usuário e API RESTful que permite configurar conexões de origem com vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar seus sistemas de terceiros, definir tempos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

Com o Experience Platform, você pode centralizar os dados coletados de fontes diferentes e usar os insights obtidos com eles para fazer mais.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## Fontes empresariais avançadas {#advanced-enterprise-sources}

As fontes a seguir estão disponíveis somente para clientes do [Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).

- [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md) [!BADGE Streaming]{type=Positive}
- [[!DNL Amazon Redshift]](connectors/databases/redshift.md) [!BADGE Lote]{type=Informative}
- [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md) [!BADGE Streaming]{type=Positive}
- [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md) [!BADGE Lote]{type=Informative}
- [[!DNL Google BigQuery]](connectors/databases/bigquery.md) [!BADGE Lote]{type=Informative}
- [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md) [!BADGE Streaming]{type=Positive}
- [[!DNL Snowflake]](connectors/databases/snowflake-streaming.md) [!BADGE Streaming]{type=Positive}
- [[!DNL Snowflake]](connectors/databases/snowflake.md) [!BADGE Lote]{type=Informative}

## Fontes criadas pela Adobe e criadas por parceiros {#adobe-and-partner-built-sources}

Alguns dos conectores no catálogo de fontes do Experience Platform são criados e mantidos pela Adobe, enquanto outros são criados e mantidos por empresas parceiras usando o [SDK de Fontes](/help/sources/sources-sdk/overview.md). Uma observação na parte superior da página de documentação para cada conector criado pelo parceiro chama se uma origem é criada e mantida pelo parceiro. Por exemplo, o [conector Amazon S3](/help/sources/connectors/cloud-storage/s3.md) é criado pela Adobe, enquanto o [conector RainFocus](/help/sources/connectors/analytics/rainfocus.md) é criado e mantido pela equipe RainFocus.

Para conectores criados e mantidos pelo parceiro, isso significa que os problemas com o conector podem precisar ser resolvidos pela equipe do parceiro (método de contato fornecido na observação na página de documentação). No caso de problemas com conectores criados e mantidos pela Adobe, entre em contato com o representante da Adobe ou com o Atendimento ao cliente.

## Categorias de origens

As origens no Experience Platform são agrupadas nas seguintes categorias:

### aplicativos Adobe {#adobe-applications}

O Experience Platform permite que os dados sejam assimilados de outros aplicativos da Adobe, incluindo o Adobe Analytics e o Adobe Audience Manager. Consulte os seguintes documentos relacionados para obter mais informações:

- [Visão geral da origem do Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
   - [Criar uma conexão de origem do Adobe Audience Manager na interface](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Visão geral da fonte de dados do Adobe Analytics Classifications](connectors/adobe-applications/classifications.md)
   - [Criar uma conexão de fonte de dados do Adobe Analytics Classifications na interface](./tutorials/ui/create/adobe-applications/classifications.md)
- [Visão geral da fonte de dados do conjunto de relatórios do Adobe Analytics](connectors/adobe-applications/analytics.md)
   - [Criar uma conexão de origem do Adobe Analytics na interface](./tutorials/ui/create/adobe-applications/analytics.md)
- [Visão geral da origem do Adobe Campaign Managed Cloud Services](connectors/adobe-applications/campaign.md)
   - [Criar uma conexão de origem do Adobe Campaign Managed Cloud Services na interface](./tutorials/ui/create/adobe-applications/campaign.md)
- [Visão geral da origem do Adobe Commerce](connectors/adobe-applications/commerce.md)
- [Visão geral da fonte de coleta de dados do Adobe](connectors/adobe-applications/data-collection.md)
   - [Criar uma conexão de origem de atributos do cliente na interface](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [Visão geral da origem de [!DNL Marketo Engage]](connectors/adobe-applications/marketo/marketo.md)
   - [Criar uma conexão de origem  [!DNL Marketo Engage]  na interface](./tutorials/ui/create/adobe-applications/marketo.md)
   - [Criar uma conexão de origem e um fluxo de dados  [!DNL Marketo Engage]  para dados de atividade personalizados](./tutorials/ui/create/adobe-applications/marketo-custom-activities.md)

### Advertising {#advertising}

O Experience Platform fornece suporte para assimilação de dados de um sistema de publicidade de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [Anúncios do Google](connectors/advertising/ads.md) [!BADGE Lote]{type=Informative}

### Analytics {#analytics}

O Experience Platform oferece suporte para assimilação de dados de uma plataforma de análise de terceiros. Leia os seguintes documentos relacionados para obter mais informações:

- [[!DNL Mixpanel]](connectors/analytics/mixpanel.md) [!BADGE Lote]{type=Informative}
- [[!DNL Pendo]](connectors/analytics/pendo-webhook.md) [!BADGE Streaming]{type=Positive}
- [[!DNL RainFocus]](connectors/analytics/rainfocus.md) [!BADGE Streaming]{type=Positive}

### Armazenamento na nuvem {#cloud-storage}

As fontes de armazenamento na nuvem podem trazer seus próprios dados para a Experience Platform sem a necessidade de baixar, formatar ou carregar. Os dados assimilados podem ser formatados como XDM JSON, XDM Parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho Origens usando a interface do usuário. Consulte os seguintes documentos relacionados para obter mais informações:

- [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md) [!BADGE Lote]{type=Informative}
- [[!DNL Azure Blob]](connectors/cloud-storage/blob.md) [!BADGE Lote]{type=Informative}
- [[!DNL Amazon S3]](connectors/cloud-storage/s3.md) [!BADGE Lote]{type=Informative}
- [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md) [!BADGE Lote]{type=Informative}
- [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md) [!BADGE Lote]{type=Informative}
- [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md) [!BADGE Lote]{type=Informative}
- [[!DNL FTP]](connectors/cloud-storage/ftp.md) [!BADGE Lote]{type=Informative}
- [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md) [!BADGE Lote]{type=Informative}
- [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md) [!BADGE Lote]{type=Informative}
- [[!DNL SFTP]](connectors/cloud-storage/sftp.md) [!BADGE Lote]{type=Informative}

### Consentimento e preferências {#consent}

O Experience Platform oferece suporte para assimilação de dados de uma plataforma de gerenciamento de preferências e consentimento de terceiros. Consulte os seguintes documentos relacionados para obter mais informações:

- [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md) [!BADGE Lote]{type=Informative}

### Gerenciamento de Relacionamento com o Cliente (CRM) {#customer-relationship-management}

Os sistemas de CRM fornecem dados que podem ajudar a criar relacionamentos com o cliente, o que, por sua vez, cria fidelidade e impulsiona a retenção do cliente. A Experience Platform oferece suporte para assimilação de dados do CRM de [!DNL Microsoft Dynamics 365] e [!DNL Salesforce]. Consulte os seguintes documentos relacionados para obter mais informações:

- [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md) [!BADGE Lote]{type=Informative}
- [[!DNL Salesforce]](connectors/crm/salesforce.md) [!BADGE Lote]{type=Informative}
- [[!DNL SugarCRM]](connectors/crm/sugarcrm.md) [!BADGE Lote]{type=Informative}
- [[!DNL Veeva CRM]](connectors/crm/veeva.md) [!BADGE Lote]{type=Informative}
- [[!DNL Zoho CRM]](connectors/crm/zoho.md) [!BADGE Lote]{type=Informative}

### Sucesso do cliente {#customer-success}

A Experience Platform oferece suporte para assimilação de dados de um aplicativo de sucesso de clientes de terceiros. Consulte os seguintes documentos relacionados para obter mais informações:

- [[!DNL Oracle Service Cloud]](connectors/customer-success/oracle-service-cloud.md) [!BADGE Lote]{type=Informative}
- [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md) [!BADGE Lote]{type=Informative}
- [[!DNL ServiceNow]](connectors/customer-success/servicenow.md) [!BADGE Lote]{type=Informative}
- [[!DNL Zendesk]](connectors/customer-success/zendesk.md) [!BADGE Lote]{type=Informative}

### Banco de dados {#database}

O Experience Platform oferece suporte para assimilação de dados de um banco de dados de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md) [!BADGE Lote]{type=Informative}
- [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md) [!BADGE Lote]{type=Informative}
- [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md) [!BADGE Lote]{type=Informative}
- [[!DNL Azure Table Storage]](connectors/databases/ats.md) [!BADGE Lote]{type=Informative}
- [[!DNL Couchbase]](connectors/databases/couchbase.md) [!BADGE Lote]{type=Informative}
- [[!DNL GreenPlum]](connectors/databases/greenplum.md) [!BADGE Lote]{type=Informative}
- [[!DNL HP Vertica]](connectors/databases/hp-vertica.md) [!BADGE Lote]{type=Informative}
- [[!DNL IBM DB2]](connectors/databases/ibm-db2.md) [!BADGE Lote]{type=Informative}
- [[!DNL MariaDB]](connectors/databases/mariadb.md) [!BADGE Lote]{type=Informative}
- [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md) [!BADGE Lote]{type=Informative}
- [[!DNL MySQL]](connectors/databases/mysql.md) [!BADGE Lote]{type=Informative}
- [[!DNL Oracle]](connectors/databases/oracle.md) [!BADGE Lote]{type=Informative}
- [[!DNL Phoenix]](connectors/databases/phoenix.md) [!BADGE Lote]{type=Informative}
- [[!DNL PostgreSQL]](connectors/databases/postgres.md) [!BADGE Lote]{type=Informative}
- [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md) [!BADGE Lote]{type=Informative}

### Parceiros de dados e identidade {#data-partner}

O Experience Platform oferece suporte para assimilação de dados de um parceiro de dados e identidade. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [[!DNL Acxiom Data Ingestion]](connectors/data-partners/acxiom-data-ingestion.md) [!BADGE Lote]{type=Informative}
- [[!DNL Acxiom Prospecting Data Import]](connectors/data-partners/acxiom-prospecting-data-import.md) [!BADGE Lote]{type=Informative}
- [[!DNL Bombora Intent]](connectors/data-partners/bombora.md) [!BADGE Lote]{type=Informative}
- [[!DNL Demandbase Intent]](connectors/data-partners/demandbase.md) [!BADGE Lote]{type=Informative}
- [[!DNL Merkury Enterprise Identity Resolution]](connectors/data-partners/merkury.md) [!BADGE Lote]{type=Informative}

### comércio eletrônico {#ecommerce}

O Experience Platform oferece suporte para assimilação de dados de um sistema de comércio eletrônico de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [[!DNL SAP Commerce]](connectors/ecommerce/sap-commerce.md) [!BADGE Lote]{type=Informative}
- [[!DNL Shopify]](connectors/ecommerce/shopify.md) [!BADGE Lote]{type=Informative}
- [[!DNL Shopify]](connectors/ecommerce/shopify-streaming.md) [!BADGE Streaming]{type=Positive}

### Sistema local {#local-system}

O Experience Platform oferece suporte para assimilação de dados do sistema local. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [Upload de arquivo local](connectors/local-system/local-file-upload.md)

### Automação de marketing {#marketing-automation}

O Experience Platform oferece suporte para assimilação de dados de um sistema de automação de marketing de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [[!DNL Braze]](connectors/marketing-automation/braze.md) [!BADGE Streaming]{type=Positive}
- [[!DNL Chatlio]](connectors/marketing-automation/chatlio-webhook.md) [!BADGE Streaming]{type=Positive}
- [[!DNL Customer.io]](connectors/marketing-automation/customerio-webhook.md) [!BADGE Streaming]{type=Positive}
- [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md) [!BADGE Lote]{type=Informative}
- [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md) [!BADGE Lote]{type=Informative}
- [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md) [!BADGE Lote]{type=Informative}
- [[!DNL Oracle NetSuite]](connectors/marketing-automation/oracle-netsuite.md) [!BADGE Lote]{type=Informative}
- [[!DNL PathFactory]](connectors/marketing-automation/pathfactory.md) [!BADGE Lote]{type=Informative}
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md) [!BADGE Lote]{type=Informative}
<!-- 
- [[!DNL Oracle Responsys]](connectors/marketing-automation/oracle-responsys.md)
-->

### Pagamentos {#payments}

O Experience Platform oferece suporte para assimilação de dados de um sistema de pagamentos de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [[!DNL PayPal]](connectors/payments/paypal.md) [!BADGE Lote]{type=Informative}
- [[!DNL Square]](connectors/payments/square.md) [!BADGE Lote]{type=Informative}
- [[!DNL Stripe]](connectors/payments/stripe.md) [!BADGE Lote]{type=Informative}

### Transmissão {#streaming}

O Experience Platform oferece suporte para assimilação de dados de fontes de transmissão. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [[!DNL HTTP API]](connectors/streaming/http.md) [!BADGE Streaming]{type=Positive}

### Protocolos {#protocols}

O Experience Platform oferece suporte para assimilação de dados de um sistema de protocolos de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [[!DNL Generic OData]](connectors/protocols/odata.md) [!BADGE Lote]{type=Informative}
- [[!DNL Generic REST API]](connectors/protocols/generic-rest.md) [!BADGE Lote]{type=Informative}

## Controle de acesso para fontes na assimilação de dados

As permissões para fontes na assimilação de dados podem ser gerenciadas no Adobe Admin Console. Você pode acessar permissões por meio da guia **[!UICONTROL Permissões]** em um perfil de produto específico. No painel **[!UICONTROL Editar Permissões]**, você pode acessar as permissões relacionadas às origens por meio da entrada de menu **[!UICONTROL assimilação de dados]**. A permissão **[!UICONTROL Exibir Fontes]** concede acesso somente leitura às fontes disponíveis na guia **[!UICONTROL Catálogo]** e às fontes autenticadas na guia **[!UICONTROL Procurar]**, enquanto a permissão **[!UICONTROL Gerenciar Fontes]** concede acesso total às fontes de leitura, criação, edição e desabilitação.

A tabela a seguir descreve como a interface do usuário se comporta com base em diferentes combinações dessas permissões:

| Nível de permissão | Descrição |
| ---- | ----|
| **[!UICONTROL Exibir Fontes]** Em | Conceda acesso somente leitura às origens em cada tipo de origem na guia Catálogo, bem como nas guias Procurar, Contas e Fluxo de dados. |
| **[!UICONTROL Gerenciar Fontes]** Em | Além das funções incluídas em **[!UICONTROL Exibir Fontes]**, concede acesso à opção **[!UICONTROL Conectar Source]** do **[!UICONTROL Catálogo]** e à opção **[!UICONTROL Selecionar Dados]** do **[!UICONTROL Procurar]**. **[!UICONTROL Gerenciar Fontes]** também permite habilitar ou desabilitar **[!UICONTROL DataFlows]** e editar suas agendas. |
| **[!UICONTROL Exibir Fontes]** Desativada e **[!UICONTROL Gerenciar Fontes]** Desativada | Revogar todo o acesso a origens. |

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
- Além disso, um fluxo de dados deve ter exatamente a mesma ID e versão do esquema em seu mapeamento, conjunto de dados de destino e conexão de destino.

Para obter mais informações sobre o controle de acesso baseado em atributos, leia a [visão geral do controle de acesso baseado em atributos](../access-control/abac/overview.md).

## Termos e condições {#terms-and-conditions}

Ao usar qualquer uma das Fontes rotuladas como beta (&quot;Beta&quot;), você reconhece que a Beta é fornecida ***&quot;no estado em que se encontra&quot; sem garantias de qualquer tipo***.

A Adobe não tem nenhuma obrigação de manter, corrigir, atualizar, alterar, modificar ou oferecer suporte à Beta. Você é aconselhado a usar materiais informativos e não se basear, de forma alguma, no funcionamento ou no desempenho corretos desses Beta e/ou dos materiais que os acompanham. O Beta é considerado Informações confidenciais da Adobe.

Qualquer &quot;Feedback&quot; (informação sobre o Beta incluindo, mas não se limitando a, problemas ou defeitos encontrados durante o uso do Beta, sugestões, melhorias e recomendações) fornecido por Você ao Adobe é atribuído ao Adobe, incluindo todos os direitos, cargos e interesses no e no Feedback.

Envie Feedback Aberto ou crie um Tíquete de Suporte para compartilhar suas sugestões ou relatar um erro, buscar um aprimoramento de recurso.
