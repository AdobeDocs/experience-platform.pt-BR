---
keywords: Experience Platform, home, tópicos populares, esquema de crm, crm, CRM, salesforce, Salesforce
solution: Experience Platform
title: Visão geral do conector de origem do Salesforce
topic-legacy: overview
description: Saiba como conectar o Salesforce ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: bd3d3a83c030baaecccba2b1793b49ad8a6caa08
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# [!DNL Salesforce] conector

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform oferece suporte para assimilar dados de um sistema de CRM de terceiros. O suporte para provedores de CRM inclui [!DNL Salesforce].

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à lista de permissões pode causar erros ou não desempenho ao usar fontes. Consulte a [LISTA DE PERMISSÕES de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Mapeamento de campo de [!DNL Salesforce] para XDM

Para estabelecer uma conexão de origem entre [!DNL Salesforce] e a Platform, [!DNL Salesforce] Os campos de dados de origem devem ser mapeados para os campos XDM de destino apropriados antes de serem assimilados na Platform.

Consulte o seguinte para obter informações detalhadas sobre as regras de mapeamento de campo entre [!DNL Salesforce] conjuntos de dados e plataforma:

- [Contatos](../adobe-applications/mapping/salesforce.md#contact)
- [Clientes potenciais](../adobe-applications/mapping/salesforce.md#lead)
- [Contas](../adobe-applications/mapping/salesforce.md#account)
- [Oportunidades](../adobe-applications/mapping/salesforce.md#opportunity)
- [Funções de contato da oportunidade](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [Campanhas](../adobe-applications/mapping/salesforce.md#campaign)
- [Membros da campanha](../adobe-applications/mapping/salesforce.md#campaign-member)

## Configure o [!DNL Salesforce] utilitário de geração automática de namespace e schema

Para usar o [!DNL Salesforce] como parte de [!DNL B2B-CDP], primeiro você deve configurar um [!DNL Postman] para gerar automaticamente seu [!DNL Salesforce] namespaces e schemas. A documentação a seguir fornece informações adicionais sobre a configuração do [!DNL Postman] utilitário:

- É possível baixar o namespace e o ambiente do utilitário de geração automática de esquema dessa [Repositório GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Para obter informações sobre como usar APIs de plataforma, incluindo detalhes sobre como coletar valores para cabeçalhos necessários e ler chamadas de API de exemplo, consulte o guia em [introdução às APIs do Platform](../../../landing/api-guide.md).
- Para obter informações sobre como gerar suas credenciais para APIs da plataforma, consulte o tutorial em [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md).
- Para obter informações sobre como configurar [!DNL Postman] para APIs da plataforma, consulte o tutorial em [configurar o console do desenvolvedor e [!DNL Postman]](../../../landing/postman.md).

Com um console de desenvolvedor do Platform e [!DNL Postman] , agora é possível começar a aplicar os valores de ambiente apropriados ao [!DNL Postman] ambiente.

A tabela a seguir contém valores de exemplo e informações adicionais sobre como preencher [!DNL Postman] ambiente:

| Variable | Descrição | Exemplo |
| --- | --- | --- |
| `CLIENT_SECRET` | Um identificador exclusivo usado para gerar o `{ACCESS_TOKEN}`. Veja o tutorial em [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md) para obter informações sobre como recuperar seu `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | O JSON Web Token (JWT) é uma credencial de autenticação usada para gerar seu {ACCESS_TOKEN}. Veja o tutorial em [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md) para obter informações sobre como gerar seu `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | Um identificador exclusivo usado para autenticar chamadas para APIs do Experience Platform. Veja o tutorial em [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md) para obter informações sobre como recuperar seu `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | O token de autorização necessário para concluir chamadas para APIs do Experience Platform. Veja o tutorial em [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md) para obter informações sobre como recuperar seu `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | No que diz respeito à [!DNL Marketo], esse valor é fixo e sempre está definido como: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | O `global` O container contém todas as classes, grupos de campos do esquema, tipos de dados e esquemas fornecidos pelo Adobe e parceiro de Experience Platform. No que diz respeito à [!DNL Marketo], esse valor é fixo e sempre está definido como `global`. | `global` |
| `PRIVATE_KEY` | Uma credencial usada para autenticar seu [!DNL Postman] para APIs do Experience Platform. Consulte o tutorial sobre como configurar o console do desenvolvedor e [configurar o console do desenvolvedor e [!DNL Postman]](../../../landing/postman.md) para obter instruções sobre como recuperar o {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Uma credencial usada para integrar ao Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | O Sistema Identity Management (IMS) fornece a estrutura para autenticação dos serviços da Adobe. No que diz respeito à [!DNL Marketo], esse valor é fixo e sempre está definido como: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Uma entidade corporativa que pode ser proprietária ou licenciar produtos e serviços e permitir o acesso a seus membros. Veja o tutorial em [configurar o console do desenvolvedor e [!DNL Postman]](../../../landing/postman.md) para obter instruções sobre como recuperar seu `{IMS_ORG}` informações. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | O nome da partição da sandbox virtual que você está usando. | `prod` |
| `TENANT_ID` | Uma ID usada para garantir que os recursos criados sejam namespacados corretamente e estejam contidos na organização IMS. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | O endpoint de URL para o qual você está fazendo chamadas de API. Esse valor é fixo e sempre está definido como: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | A ID exclusiva para sua [!DNL Marketo] conta. Veja o tutorial em [autenticação de [!DNL Marketo] instância](../adobe-applications/marketo/marketo-auth.md) para obter informações sobre como recuperar seu `munchkinId`. | `123-ABC-456` |
| `sfdc_org_id` | A ID da organização da [!DNL Salesforce] conta. Veja o seguinte [[!DNL Salesforce] guia](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) para obter mais informações sobre como adquirir [!DNL Salesforce] ID da organização. | `00D4W000000FgYJUA0` |
| `has_abm` | Um valor booleano que indica se você está inscrito [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | Um valor booleano que indica se você está inscrito como [!DNL Marketo Sales Insight]. | `false` |

{style=&quot;table-layout:auto&quot;}

### Execução dos scripts

Com seu [!DNL Postman] coleção e ambiente configuradas, agora é possível executar o script pelo [!DNL Postman] interface.

No [!DNL Postman] selecione a pasta raiz do utilitário autogerador e selecione **[!DNL Run]** no cabeçalho superior.

![pasta raiz](../../images/tutorials/create/salesforce/root-folder.png)

O [!DNL Runner] é exibida. A partir daqui, verifique se todas as caixas de seleção estão selecionadas e, em seguida, selecione **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![gerador de rodagem](../../images/tutorials/create/salesforce/run-generator.png)

Uma solicitação bem-sucedida cria namespaces e schemas B2B de acordo com as especificações beta.

## Connect [!DNL Salesforce] para Plataforma usando APIs

A documentação abaixo fornece informações sobre como se conectar [!DNL Salesforce] para Plataforma usando APIs ou a interface do usuário:

- [Criar uma conexão base do Salesforce usando a API do Serviço de Fluxo](../../tutorials/api/create/crm/salesforce.md)
- [Explore a estrutura de dados e o conteúdo de uma fonte de CRM usando a API do Serviço de Fluxo](../../tutorials/api/explore/crm.md)
- [Crie um fluxo de dados para uma fonte CRM usando a API do Serviço de Fluxo](../../tutorials/api/collect/crm.md)

## Connect [!DNL Salesforce] para Plataforma usando a interface do usuário

- [Criar uma conexão de origem do Salesforce na interface do usuário](../../tutorials/ui/create/crm/salesforce.md)
- [Criar um fluxo de dados para uma conexão CRM na interface do usuário](../../tutorials/ui/dataflow/crm.md)
