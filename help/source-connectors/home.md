---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visão geral dos Conectores de origem da plataforma Adobe Experience
topic: overview
translation-type: tm+mt
source-git-commit: 291d669cc0f5b009b23dc2771688ee54b53d08db

---


# Visão geral dos conectores de origem

A plataforma Adobe Experience permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamentos baseados em nuvem, bancos de dados e muitas outras.

A plataforma Experience fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem com vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar sistemas de terceiros, definir horários para execuções de ingestão e gerenciar o throughput de ingestão de dados.

Com a plataforma Experience, você pode centralizar os dados coletados de fontes diferentes e usar os insights obtidos com ela para fazer mais.

## Tipos de fontes

As fontes na plataforma Experience são agrupadas nas seguintes categorias:

### Aplicativos da Adobe

A plataforma Experience permite que os dados sejam assimilados de outros aplicativos da Adobe, incluindo o Adobe Analytics, o Adobe Audiência Manager e o Experience Platform Launch. Consulte os seguintes documentos relacionados para obter mais informações:

- [Visão geral do conector do Adobe Audiência Manager](./ui/adobe-applications/audience-manager.md)
- [Criar um conector de origem do Adobe Audiência Manager na interface do usuário](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/adobe-applications/aam-ui-tutorial.md)
- [Visão geral do conector de dados do Adobe Analytics](./ui/adobe-applications/analytics.md)
- [Criar um conector de origem do Adobe Analytics na interface do usuário](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/adobe-applications/adobe-analytics-ui-tutorial.md)

### Armazenamento em nuvem

As fontes de armazenamentos na nuvem podem trazer seus próprios dados para a Plataforma sem a necessidade de baixar, formatar ou fazer upload. Cada etapa do processo é integrada ao fluxo de trabalho Fontes usando a interface do usuário. O suporte para provedores de armazenamentos em nuvem inclui Amazon S3, Azure Blob, servidores FTP e servidores SFTP. Consulte os seguintes documentos relacionados para obter mais informações:

- [Criar um conector de origem do Azure Blob ou Amazon S3 na interface do usuário](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/amazon-s3-ui-tutorial.md)
- [Criar um conector de origem Gen2 do Armazenamento Azure Data Lake na interface do usuário](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/adls-gen2-ui-tutorial.md)
- [Criar um conector de origem FTP ou SFTP na interface do usuário](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/ftp-sftp-ui-tutorial.md)
- [Criar um conector de origem de Armazenamento do Google Cloud na interface do usuário](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/google-cloud-storage-ui-tutorial.md)

### Gerenciamento de Relacionamento com o Cliente (CRM)

Os sistemas CRM fornecem dados que podem ajudar a construir relações com os clientes, o que, por sua vez, cria fidelidade e impulsiona a retenção dos clientes. A plataforma Experience oferece suporte para a assimilação de dados CRM do Microsoft Dynamics 365 e Salesforce. Consulte os seguintes documentos relacionados para obter mais informações:

- [Criar um conector de origem do Microsoft Dynamics 365 ou Salesforce na interface do usuário](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/crm/dynamics-salesforce-ui-tutorial.md)
- [Criar um conector de origem PayPal na interface do usuário](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/crm/paypal-tutorial.md)

### Sucesso do cliente (CS)

A plataforma Experience oferece suporte para a assimilação de dados de um aplicativo de terceiros com sucesso. Consulte os seguintes documentos relacionados para obter mais informações:

- [Criar um conector de origem da Salesforce Service Cloud na interface do usuário](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/customer-success/salesforce-service-cloud-tutorial.md)
- [Criar um conector de origem ServiceNow na interface do usuário](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/customer-success/servicenow-ui-tutorial.md)

### Banco de dados

A plataforma Experience oferece suporte para a assimilação de dados de um banco de dados de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [Criar um conector de origem do Redshift AWS na interface do usuário](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/amazon-redshift-ui-tutorial.md)
- [Criar um conector de origem do Azure Synapse Analytics na interface do usuário](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/azure-synapse-analytics-ui-tutorial.md)
- [Criar um conector de origem do Google BigQuery na interface do usuário](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/google-big-query-ui-tutorial.md)
- [Criar um conector de origem MariaDB na interface do usuário](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-api-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/api/database-nosql/mariadb-api-tutorial.md)
- [Criar um conector de origem do Microsoft SQL Server na interface do usuário](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/sql-server-ui-tutorial.md)
- [Criar um conector de origem MySQL na interface do usuário](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/mysql-ui-tutorial.md)
- [Criar um conector de origem PostgreSQL na interface do usuário](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/postgresql-tutorial.md)

### Automação de marketing

A plataforma Experience oferece suporte para a assimilação de dados de um sistema de automação de marketing de terceiros. Consulte os seguintes documentos relacionados para obter mais informações sobre conectores de origem específicos:

- [Criar um conector de origem HubSpot na interface do usuário](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/marketing-automation/hubspot-tutorial.md)

## Tutoriais de API

Você pode criar conectores de origem usando a API de Serviço de Fluxo. Para obter mais informações, consulte o documento [tutorial da API de](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-api-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/api/sources-api-tutorial.md)fontes.

## Controle de acesso para fontes na ingestão de dados

As permissões para fontes na ingestão de dados podem ser gerenciadas no Adobe Admin Console. Você pode acessar permissões por meio da guia *Permissões* em um perfil de produto específico. No painel **Editar permissões** , é possível acessar as permissões pertencentes às fontes por meio da entrada do menu de ingestão *de* dados. A permissão Fontes **de** Visualização concede acesso somente leitura a fontes disponíveis na guia *Catálogo* e a fontes autenticadas na guia *Procurar* , enquanto a permissão **Gerenciar fontes** concede acesso total a fontes de leitura, criação, edição e desativação.

A tabela a seguir descreve como a interface se comporta com base em diferentes combinações dessas permissões:

| Nível de permissão | Descrição |
| ---- | ----|
| **Fontes** de Visualização ativadas | Conceda acesso somente leitura às fontes em cada tipo de fonte na guia *Catálogo* , bem como nas guias *Procurar*, *Contas* e *DataFlow* . |
| **Gerenciar fontes** em | Além das funções incluídas nas Fontes **de** Visualização, concede acesso à opção Fonte *do* Connect no *Catálogo* e à opção *Selecionar dados* na *Navegação*. **Gerenciar fontes** também permite ativar ou desativar *DataFlows* e editar seus agendamentos. |
| **Fontes** de Visualização desativadas e **gerenciamento de fontes** desativadas | Revogar todo o acesso às fontes. |

Para obter mais informações sobre as permissões disponíveis concedidas por meio do Admin Console, incluindo essas quatro fontes, consulte a visão geral [do](../access-control/home.md)controle de acesso.
