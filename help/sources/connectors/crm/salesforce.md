---
title: Visão geral do Conector Source do Salesforce
description: Saiba como conectar o Salesforce ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: 5d28db34edd377269e8710b1741098a08616ae5f
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---

# [!DNL Salesforce]

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform fornece suporte para assimilação de dados de um sistema CRM de terceiros. O suporte para provedores de CRM inclui [!DNL Salesforce].

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a página [lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Mapeamento de campo de [!DNL Salesforce] para XDM

Para estabelecer uma conexão de origem entre [!DNL Salesforce] e a Platform, os campos de dados de origem [!DNL Salesforce] devem ser mapeados para seus campos XDM de destino apropriados antes de serem assimilados na Platform.

Consulte o seguinte para obter informações detalhadas sobre as regras de mapeamento de campos entre [!DNL Salesforce] conjuntos de dados e a Plataforma:

- [Contatos](../adobe-applications/mapping/salesforce.md#contact)
- [Clientes potenciais](../adobe-applications/mapping/salesforce.md#lead)
- [Contas](../adobe-applications/mapping/salesforce.md#account)
- [Oportunidades](../adobe-applications/mapping/salesforce.md#opportunity)
- [Funções do contato da oportunidade](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [Campanhas](../adobe-applications/mapping/salesforce.md#campaign)
- [Membros da campanha](../adobe-applications/mapping/salesforce.md#campaign-member)
- [Relação de contato da conta](../adobe-applications/mapping/salesforce.md#account-contact-relation)

## Configurar o namespace [!DNL Salesforce] e o utilitário de geração automática de esquema

Para usar a origem [!DNL Salesforce] como parte de [!DNL B2B-CDP], primeiro você deve configurar um utilitário [!DNL Postman] para gerar automaticamente seus namespaces e esquemas [!DNL Salesforce]. A documentação a seguir fornece informações adicionais sobre a configuração do utilitário [!DNL Postman]:

- Você pode baixar a coleção de utilitários de geração automática de namespace e esquema e o ambiente deste [repositório do GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Para obter informações sobre como usar APIs da plataforma, incluindo detalhes sobre como coletar valores para cabeçalhos necessários e ler chamadas de API de exemplo, consulte o manual em [introdução às APIs da plataforma](../../../landing/api-guide.md).
- Para obter informações sobre como gerar suas credenciais para APIs da plataforma, consulte o tutorial sobre [autenticação e acesso a APIs do Experience Platform](../../../landing/api-authentication.md).
- Para obter informações sobre como configurar o [!DNL Postman] para APIs da Platform, consulte o tutorial em [configuração do console do desenvolvedor e [!DNL Postman]](../../../landing/postman.md).

Com um console de desenvolvedor da Platform e o [!DNL Postman] configurado, agora é possível começar a aplicar os valores de ambiente apropriados ao seu ambiente [!DNL Postman].

A tabela a seguir contém valores de exemplo, bem como informações adicionais sobre como preencher o ambiente [!DNL Postman]:

| Variable | Descrição | Exemplo |
| --- | --- | --- |
| `CLIENT_SECRET` | Um identificador exclusivo usado para gerar o `{ACCESS_TOKEN}`. Consulte o tutorial sobre [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md) para obter informações sobre como recuperar o `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | O JSON Web Token (JWT) é uma credencial de autenticação usada para gerar seu {ACCESS_TOKEN}. Consulte o tutorial sobre [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md) para obter informações sobre como gerar seu `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | Um identificador exclusivo usado para autenticar chamadas para APIs Experience Platform. Consulte o tutorial sobre [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md) para obter informações sobre como recuperar o `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | O token de autorização necessário para completar chamadas para APIs de Experience Platform. Consulte o tutorial sobre [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md) para obter informações sobre como recuperar o `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Com relação a [!DNL Marketo], esse valor é fixo e sempre é definido como: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | O contêiner `global` contém todas as classes, grupos de campos de esquema, tipos de dados e esquemas fornecidos por parceiros de Adobe e Experience Platform padrão. Com relação a [!DNL Marketo], esse valor é fixo e sempre é definido como `global`. | `global` |
| `PRIVATE_KEY` | Uma credencial usada para autenticar sua instância do [!DNL Postman] para APIs Experience Platform. Consulte o tutorial sobre configuração do console do desenvolvedor e [configuração do console do desenvolvedor e  [!DNL Postman]](../../../landing/postman.md) para obter instruções sobre como recuperar o {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Uma credencial usada para integrar ao Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | O Sistema Identity Management (IMS) fornece a estrutura para autenticação de serviços da Adobe. Com relação a [!DNL Marketo], esse valor é fixo e sempre é definido como: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Uma entidade corporativa que pode ser proprietária ou licenciar produtos e serviços e permitir acesso a seus membros. Consulte o tutorial em [configuração do console do desenvolvedor e [!DNL Postman]](../../../landing/postman.md) para obter instruções sobre como recuperar as informações de `{ORG_ID}`. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | O nome da partição de sandbox virtual que você está usando. | `prod` |
| `TENANT_ID` | Uma ID usada para garantir que os recursos criados tenham o namespace adequado e estejam contidos na organização. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | O endpoint de URL para o qual você está fazendo chamadas de API. Este valor é fixo e está sempre definido como: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | O identificador exclusivo da sua conta [!DNL Marketo]. Consulte o tutorial em [autenticando sua [!DNL Marketo] instância](../adobe-applications/marketo/marketo-auth.md) para obter informações sobre como recuperar sua `munchkinId`. | `123-ABC-456` |
| `sfdc_org_id` | A ID da organização da sua conta [!DNL Salesforce]. Consulte o [[!DNL Salesforce] guia](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) a seguir para obter mais informações sobre como adquirir a ID da organização do [!DNL Salesforce]. | `00D4W000000FgYJUA0` |
| `has_abm` | Um valor booleano que indica se você assinou o [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | Um valor booleano que indica se você assinou [!DNL Marketo Sales Insight]. | `false` |

{style="table-layout:auto"}

### Execução dos scripts

Com a coleção e o ambiente [!DNL Postman] configurados, agora é possível executar o script por meio da interface [!DNL Postman].

Na interface [!DNL Postman], selecione a pasta raiz do utilitário gerador automático e, em seguida, selecione **[!DNL Run]** no cabeçalho superior.

![pasta-raiz](../../images/tutorials/create/salesforce/root-folder.png)

A interface [!DNL Runner] é exibida. Aqui, verifique se todas as caixas de seleção estão marcadas e selecione **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![run-generator](../../images/tutorials/create/salesforce/run-generator.png)

Uma solicitação bem-sucedida cria os namespaces B2B e esquemas de acordo com as especificações beta.

## Conectar [!DNL Salesforce] à plataforma usando APIs

A documentação abaixo fornece informações sobre como conectar o [!DNL Salesforce] à Plataforma usando APIs ou a interface do usuário:

- [Criar uma conexão básica do Salesforce usando a API do Serviço de fluxo](../../tutorials/api/create/crm/salesforce.md)
- [Explorar tabelas de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/tabular.md)
- [Criar um fluxo de dados para uma origem de CRM usando a API do Serviço de Fluxo](../../tutorials/api/collect/crm.md)

## Conectar [!DNL Salesforce] à Plataforma usando a interface

- [Criar uma conexão de origem do Salesforce na interface](../../tutorials/ui/create/crm/salesforce.md)
- [Criar um fluxo de dados para uma conexão de CRM na interface](../../tutorials/ui/dataflow/crm.md)
