---
keywords: Experience Platform;página inicial;tópicos populares;conectores de origem;conector de origem;fontes;fontes de dados;fonte de dados;conexão da fonte de dados
solution: Experience Platform
title: Visão geral dos conectores de origem
description: O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: 632cff3ee4ca82d391e9a1df0cb38d903e8a5428
workflow-type: tm+mt
source-wordcount: '1526'
ht-degree: 1%

---

# Visão geral dos conectores de origem

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamentos baseados na nuvem, bancos de dados e muitas outras.

[!DNL Flow Service] O é usado para coletar e centralizar dados do cliente de várias fontes diferentes na Platform. O serviço fornece uma interface de usuário e API RESTful que permite configurar conexões de origem com vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar seus sistemas de terceiros, definir tempos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

Com o Experience Platform, é possível centralizar os dados coletados de fontes diferentes e usar os insights obtidos com eles para fazer mais.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## origens desenvolvidas por Adobe e parceiros {#adobe-and-partner-built-sources}

Alguns dos conectores no catálogo de fontes de Experience Platform são criados e mantidos pelo Adobe, enquanto outros são criados e mantidos por empresas parceiras usando [SDK de origens](/help/sources/sources-sdk/overview.md). Uma observação na parte superior da página de documentação para cada conector criado pelo parceiro chama se uma origem é criada e mantida pelo parceiro. Por exemplo, a variável [Conector Amazon S3](/help/sources/connectors/cloud-storage/s3.md) é criada pelo Adobe, enquanto a variável [Conector RainFocus](/help/sources/connectors/analytics/rainfocus.md) O é criado e mantido pela equipe do RainFocus.

Para conectores criados e mantidos pelo parceiro, isso significa que os problemas com o conector podem precisar ser resolvidos pela equipe do parceiro (método de contato fornecido na observação na página de documentação). No caso de problemas com conectores criados e mantidos pelo Adobe, entre em contato com o representante da Adobe ou com o Atendimento ao cliente.

## Tipos de origens

As origens em Experience Platform são agrupadas nas seguintes categorias:

### aplicativos Adobe {#adobe-applications}

O Experience Platform permite que os dados sejam assimilados de outros aplicativos Adobe, incluindo Adobe Analytics e Adobe Audience Manager. Consulte os seguintes documentos relacionados para obter mais informações:

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
- [[!DNL Marketo Engage] visão geral da origem](connectors/adobe-applications/marketo/marketo.md)
   - [Criar um [!DNL Marketo Engage] conexão de origem na interface](./tutorials/ui/create/adobe-applications/marketo.md)
   - [Criar um [!DNL Marketo Engage] conexão de origem e fluxo de dados para dados de atividade personalizados](./tutorials/ui/create/adobe-applications/marketo-custom-activities.md)

### Advertising {#advertising}

O Experience Platform fornece suporte para assimilação de dados de um sistema de publicidade de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [Anúncios do Google](connectors/advertising/ads.md) [!BADGE Lote]{type=Informative}

### Analytics {#analytics}

O Experience Platform fornece suporte para assimilação de dados de uma plataforma de análise de terceiros. Consulte os seguintes documentos relacionados para obter mais informações:

- [[!DNL Mixpanel]](connectors/analytics/mixpanel.md) [!BADGE Lote]{type=Informative}
- [[!DNL Pendo]](connectors/analytics/pendo-webhook.md) [!BADGE Streaming]{type=Positive}
- [[!DNL RainFocus]](connectors/analytics/rainfocus.md) [!BADGE Streaming]{type=Positive}

### Armazenamento na nuvem {#cloud-storage}

As fontes de armazenamento na nuvem podem trazer seus próprios dados para a Platform sem a necessidade de baixar, formatar ou carregar. Os dados assimilados podem ser formatados como XDM JSON, XDM Parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho Origens usando a interface do usuário. Consulte os seguintes documentos relacionados para obter mais informações:

- [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md) [!BADGE Lote]{type=Informative}
- [[!DNL Azure Blob]](connectors/cloud-storage/blob.md) [!BADGE Lote]{type=Informative}
- [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md) [!BADGE Streaming]{type=Positive}
- [[!DNL Amazon S3]](connectors/cloud-storage/s3.md) [!BADGE Lote]{type=Informative}
- [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md) [!BADGE Lote]{type=Informative}
- [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md) [!BADGE Streaming]{type=Positive}
- [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md) [!BADGE Lote]{type=Informative}
- [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md) [!BADGE Lote]{type=Informative}
- [[!DNL FTP]](connectors/cloud-storage/ftp.md) [!BADGE Lote]{type=Informative}
- [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md) [!BADGE Lote]{type=Informative}
- [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md) [!BADGE Streaming]{type=Positive}
- [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md) [!BADGE Lote]{type=Informative}
- [[!DNL SFTP]](connectors/cloud-storage/sftp.md) [!BADGE Lote]{type=Informative}

### Consentimento e preferências {#consent}

O Experience Platform oferece suporte para assimilação de dados de uma plataforma de gerenciamento de preferências e consentimento de terceiros. Consulte os seguintes documentos relacionados para obter mais informações:

- [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md) [!BADGE Lote]{type=Informative}

### Gerenciamento de Relacionamento com o Cliente (CRM) {#customer-relationship-management}

Os sistemas de CRM fornecem dados que podem ajudar a criar relacionamentos com o cliente, o que, por sua vez, cria fidelidade e impulsiona a retenção do cliente. O Experience Platform oferece suporte para assimilação de dados de CRM do [!DNL Microsoft Dynamics 365] e [!DNL Salesforce]. Consulte os seguintes documentos relacionados para obter mais informações:

- [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md) [!BADGE Lote]{type=Informative}
- [[!DNL Salesforce]](connectors/crm/salesforce.md) [!BADGE Lote]{type=Informative}
- [[!DNL SugarCRM]](connectors/crm/sugarcrm.md) [!BADGE Lote]{type=Informative}
- [[!DNL Veeva CRM]](connectors/crm/veeva.md) [!BADGE Lote]{type=Informative}
- [[!DNL Zoho CRM]](connectors/crm/zoho.md) [!BADGE Lote]{type=Informative}

### Sucesso do cliente {#customer-success}

O Experience Platform fornece suporte para assimilação de dados de um aplicativo de sucesso de clientes de terceiros. Consulte os seguintes documentos relacionados para obter mais informações:

- [[!DNL Oracle Service Cloud]](connectors/customer-success/oracle-service-cloud.md) [!BADGE Lote]{type=Informative}
- [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md) [!BADGE Lote]{type=Informative}
- [[!DNL ServiceNow]](connectors/customer-success/servicenow.md) [!BADGE Lote]{type=Informative}
- [[!DNL Zendesk]](connectors/customer-success/zendesk.md) [!BADGE Lote]{type=Informative}

### Banco de dados {#database}

O Experience Platform fornece suporte para assimilação de dados de um banco de dados de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [[!DNL Amazon Redshift]](connectors/databases/redshift.md) [!BADGE Lote]{type=Informative}
- [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md) [!BADGE Lote]{type=Informative}
- [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md) [!BADGE Lote]{type=Informative}
- [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md) [!BADGE Lote]{type=Informative}
- [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md) [!BADGE Lote]{type=Informative}
- [[!DNL Azure Table Storage]](connectors/databases/ats.md) [!BADGE Lote]{type=Informative}
- [[!DNL Couchbase]](connectors/databases/couchbase.md) [!BADGE Lote]{type=Informative}
- [[!DNL Google BigQuery]](connectors/databases/bigquery.md) [!BADGE Lote]{type=Informative}
- [[!DNL GreenPlum]](connectors/databases/greenplum.md) [!BADGE Lote]{type=Informative}
- [[!DNL HP Vertica]](connectors/databases/hp-vertica.md) [!BADGE Lote]{type=Informative}
- [[!DNL IBM DB2]](connectors/databases/ibm-db2.md) [!BADGE Lote]{type=Informative}
- [[!DNL MariaDB]](connectors/databases/mariadb.md) [!BADGE Lote]{type=Informative}
- [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md) [!BADGE Lote]{type=Informative}
- [[!DNL MySQL]](connectors/databases/mysql.md) [!BADGE Lote]{type=Informative}
- [[!DNL Oracle]](connectors/databases/oracle.md) [!BADGE Lote]{type=Informative}
- [[!DNL Phoenix]](connectors/databases/phoenix.md) [!BADGE Lote]{type=Informative}
- [[!DNL PostgreSQL]](connectors/databases/postgres.md) [!BADGE Lote]{type=Informative}
- [[!DNL Snowflake]](connectors/databases/snowflake-streaming.md) [!BADGE Streaming]{type=Positive}
- [[!DNL Snowflake]](connectors/databases/snowflake.md) [!BADGE Lote]{type=Informative}
- [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md) [!BADGE Lote]{type=Informative}

### Parceiro de dados {#data-partner}

O Experience Platform fornece suporte para assimilação de dados de um banco de dados de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [[!DNL Merkury Enterprise Identity Resolution]](connectors/data-partners/merkury.md) [!BADGE Lote]{type=Informative}

### eCommerce {#ecommerce}

O Experience Platform fornece suporte para assimilação de dados de um sistema de comércio eletrônico de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [[!DNL SAP Commerce]](connectors/ecommerce/sap-commerce.md) [!BADGE Lote]{type=Informative}
- [[!DNL Shopify]](connectors/ecommerce/shopify.md) [!BADGE Lote]{type=Informative}
- [[!DNL Shopify]](connectors/ecommerce/shopify-streaming.md) [!BADGE Streaming]{type=Positive}

### Sistema local {#local-system}

O Experience Platform fornece suporte para assimilação de dados do sistema local. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [Upload de arquivo local](connectors/local-system/local-file-upload.md)

### Automação de marketing {#marketing-automation}

O Experience Platform fornece suporte para assimilação de dados de um sistema de automação de marketing de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [[!DNL Braze]](tutorials/ui/create/marketing-automation/braze.md) [!BADGE Streaming]{type=Positive}
- [[!DNL Chatlio]](connectors/marketing-automation/chatlio-webhook.md) [!BADGE Streaming]{type=Positive}
- [[!DNL Customer.io]](connectors/marketing-automation/customerio-webhook.md) [!BADGE Streaming]{type=Positive}
- [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md) [!BADGE Lote]{type=Informative}
- [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md) [!BADGE Lote]{type=Informative}
- [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md) [!BADGE Lote]{type=Informative}
- [[!DNL Oracle NetSuite]](connectors/marketing-automation/oracle-netsuite.md) [!BADGE Lote]{type=Informative}
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md) [!BADGE Lote]{type=Informative}
<!-- 
- [[!DNL Oracle Responsys]](connectors/marketing-automation/oracle-responsys.md)
-->

### Pagamentos {#payments}

O Experience Platform oferece suporte para assimilação de dados de um sistema de pagamentos de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [[!DNL PayPal]](connectors/payments/paypal.md) [!BADGE Lote]{type=Informative}
- [[!DNL Square]](connectors/payments/square.md) [!BADGE Lote]{type=Informative}

### Streaming {#streaming}

O Experience Platform fornece suporte para assimilação de dados de fontes de transmissão. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [[!DNL HTTP API]](connectors/streaming/http.md) [!BADGE Streaming]{type=Positive}

### Protocolos {#protocols}

O Experience Platform fornece suporte para assimilação de dados de um sistema de protocolos de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [[!DNL Generic OData]](connectors/protocols/odata.md) [!BADGE Lote]{type=Informative}
- [[!DNL Generic REST API]](connectors/protocols/generic-rest.md) [!BADGE Lote]{type=Informative}

## Controle de acesso para fontes na assimilação de dados

As permissões para fontes na assimilação de dados podem ser gerenciadas no Adobe Admin Console. Você pode acessar permissões por meio da variável **[!UICONTROL Permissões]** em um perfil de produto específico. No **[!UICONTROL Editar permissões]** painel, você pode acessar as permissões relacionadas às fontes por meio da **[!UICONTROL assimilação de dados]** entrada de menu. A variável **[!UICONTROL Exibir fontes]** concede acesso somente leitura às fontes disponíveis na **[!UICONTROL Catálogo]** e fontes autenticadas na **[!UICONTROL Procurar]** , enquanto a guia **[!UICONTROL Gerenciar fontes]** A permissão concede acesso total para ler, criar, editar e desativar fontes.

A tabela a seguir descreve como a interface do usuário se comporta com base em diferentes combinações dessas permissões:

| Nível de permissão | Descrição |
| ---- | ----|
| **[!UICONTROL Exibir fontes]** Ligado | Conceda acesso somente leitura às origens em cada tipo de origem na guia Catálogo, bem como nas guias Procurar, Contas e Fluxo de dados. |
| **[!UICONTROL Gerenciar fontes]** Ligado | Além das funções incluídas em **[!UICONTROL Exibir fontes]**, concede acesso a **[!UICONTROL Origem da conexão]** opção em **[!UICONTROL Catálogo]** e para **[!UICONTROL Selecionar dados]** opção em **[!UICONTROL Procurar]**. **[!UICONTROL Gerenciar fontes]** também permite ativar ou desativar o **[!UICONTROL FluxosDados]** e editar suas programações. |
| **[!UICONTROL Exibir fontes]** Desativado e **[!UICONTROL Gerenciar fontes]** Desligado | Revogar todo o acesso a origens. |

Para obter mais informações sobre as permissões disponíveis concedidas por meio das Permissões do Adobe, leia o [visão geral do controle de acesso](../access-control/home.md).

### Controle de acesso baseado em atributos

O controle de acesso baseado em atributos no Adobe Experience Platform permite que os administradores controlem o acesso a objetos e/ou recursos específicos com base em atributos.

Com o controle de acesso baseado em atributos, é possível aplicar configurações de mapeamento a campos aos quais você tem permissões. Além disso, não é possível assimilar dados em um conjunto de dados se você não tiver acesso a todos os campos no conjunto de dados.

#### Suporte para controle de acesso baseado em atributos nas origens

>[!TIP]
>
>O controle de acesso baseado em atributos funciona da seguinte maneira: **funções** são criados para categorizar os tipos de usuários que interagem com sua instância da Platform. **Rótulos** são aplicados a **funções** para designar o acesso a essa determinada função. **Rótulos** também são aplicados a recursos como campos de esquema e segmentos. Para que um usuário tenha acesso a determinados campos e segmentos de esquema, ele deve ser adicionado a *uma função com o mesmo rótulo que é atribuída ao recurso consultado*. Para obter mais informações, leia a [guia completo do controle de acesso baseado em atributos](../access-control/abac/end-to-end-guide.md).

- Aplique rótulos a campos de esquema para definir o acesso a campos de esquema específicos na organização. Uma vez estabelecido o acesso a campos de esquema específicos, os usuários só poderão criar mapeamentos para os campos aos quais têm acesso.
- Os usuários sem as funções apropriadas não poderão criar ou atualizar fluxos de dados com mapeamentos que envolvam campos de esquema inacessíveis. Além disso, os usuários não autorizados não podem atualizar, excluir, ativar ou desativar fluxos de dados existentes com campos de esquema inacessíveis.
- Além disso, um fluxo de dados deve ter exatamente a mesma ID e versão do esquema em seu mapeamento, conjunto de dados de destino e conexão de destino.

Para obter mais informações sobre o controle de acesso baseado em atributos, leia a [visão geral do controle de acesso baseado em atributos](../access-control/abac/overview.md).

## Termos e condições {#terms-and-conditions}

Ao usar qualquer uma das Fontes rotuladas como beta (&quot;Beta&quot;), você reconhece que a versão Beta é fornecida ***&quot;no estado em que se encontra&quot; sem qualquer tipo de garantia***.

O Adobe não terá nenhuma obrigação de manter, corrigir, atualizar, alterar, modificar ou oferecer suporte ao Beta. Você é aconselhado a usar o Informativo e não depender de forma alguma do correto funcionamento ou desempenho de tais Beta e/ou materiais de acompanhamento. O Beta é considerado Informação confidencial do Adobe.

Qualquer &quot;Feedback&quot; (informação sobre o Beta incluindo, mas não se limitando a, problemas ou defeitos que você encontrar ao usar o Beta, sugestões, melhorias e recomendações) fornecido por Você ao Adobe é atribuído ao Adobe, incluindo todos os direitos, títulos e interesses no e para tal Feedback.

Envie Feedback Aberto ou crie um Tíquete de Suporte para compartilhar suas sugestões ou relatar um erro, buscar um aprimoramento de recurso.
