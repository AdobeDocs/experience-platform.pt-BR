---
title: Visão geral do Conector de origem do Salesforce
description: Saiba como conectar o Salesforce ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: 5d28db34edd377269e8710b1741098a08616ae5f
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 0%

---

# [!DNL Salesforce]

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform fornece suporte para assimilação de dados de um sistema CRM de terceiros. O suporte para provedores de CRM inclui [!DNL Salesforce].

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a [LISTA DE PERMISSÕES de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Mapeamento de campo de [!DNL Salesforce] ao XDM

Para estabelecer uma conexão de origem entre [!DNL Salesforce] e Platform, a [!DNL Salesforce] os campos de dados de origem devem ser mapeados para os campos XDM de destino apropriados antes de serem assimilados na Platform.

Consulte o seguinte para obter informações detalhadas sobre as regras de mapeamento de campo entre [!DNL Salesforce] conjuntos de dados e plataforma:

- [Contatos](../adobe-applications/mapping/salesforce.md#contact)
- [Clientes potenciais](../adobe-applications/mapping/salesforce.md#lead)
- [Contas](../adobe-applications/mapping/salesforce.md#account)
- [Oportunidades](../adobe-applications/mapping/salesforce.md#opportunity)
- [Funções do contato da oportunidade](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [Campanhas](../adobe-applications/mapping/salesforce.md#campaign)
- [Membros da campanha](../adobe-applications/mapping/salesforce.md#campaign-member)
- [Relação de contato da conta](../adobe-applications/mapping/salesforce.md#account-contact-relation)

## Configurar o [!DNL Salesforce] utilitário de geração automática de namespace e esquema

Para usar o [!DNL Salesforce] origem como parte de [!DNL B2B-CDP], você deve primeiro configurar um [!DNL Postman] utilitário para gerar automaticamente o [!DNL Salesforce] namespaces e esquemas. A documentação a seguir fornece informações adicionais sobre a configuração do [!DNL Postman] utilitário:

- Você pode baixar a coleção de utilitários de geração automática de namespace e esquema e o ambiente a partir deste [Repositório do GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Para obter informações sobre como usar APIs da plataforma, incluindo detalhes sobre como coletar valores para cabeçalhos necessários e ler chamadas de API de amostra, consulte o manual em [introdução às APIs da Platform](../../../landing/api-guide.md).
- Para obter informações sobre como gerar suas credenciais para APIs da Platform, consulte o tutorial em [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md).
- Para obter informações sobre como configurar [!DNL Postman] para APIs da Platform, consulte o tutorial em [configuração do console do desenvolvedor e [!DNL Postman]](../../../landing/postman.md).

Com um console de desenvolvedor da Platform e [!DNL Postman] configurada, agora é possível começar a aplicar os valores de ambiente apropriados às suas [!DNL Postman] ambiente.

A tabela a seguir contém valores de exemplo, bem como informações adicionais sobre como preencher o [!DNL Postman] ambiente:

| Variable | Descrição | Exemplo |
| --- | --- | --- |
| `CLIENT_SECRET` | Um identificador exclusivo usado para gerar sua `{ACCESS_TOKEN}`. Veja o tutorial sobre [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md) para obter informações sobre como recuperar o `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | O JSON Web Token (JWT) é uma credencial de autenticação usada para gerar seu {ACCESS_TOKEN}. Veja o tutorial sobre [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md) para obter informações sobre como gerar seus `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | Um identificador exclusivo usado para autenticar chamadas para APIs Experience Platform. Veja o tutorial sobre [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md) para obter informações sobre como recuperar o `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | O token de autorização necessário para completar chamadas para APIs de Experience Platform. Veja o tutorial sobre [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md) para obter informações sobre como recuperar o `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | No que diz respeito a [!DNL Marketo], esse valor é fixo e sempre é definido como: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | A variável `global` o container contém todas as classes padrão fornecidas por Adobe e parceiros de Experience Platform, grupos de campos de esquema, tipos de dados e esquemas. No que diz respeito a [!DNL Marketo], esse valor é fixo e sempre é definido como `global`. | `global` |
| `PRIVATE_KEY` | Uma credencial usada para autenticar seu [!DNL Postman] para APIs Experience Platform. Consulte o tutorial sobre a configuração do console do desenvolvedor e [configuração do console do desenvolvedor e [!DNL Postman]](../../../landing/postman.md) para obter instruções sobre como recuperar o {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Uma credencial usada para integrar ao Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | O Sistema Identity Management (IMS) fornece a estrutura para autenticação de serviços da Adobe. No que diz respeito a [!DNL Marketo], esse valor é fixo e sempre é definido como: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Uma entidade corporativa que pode ser proprietária ou licenciar produtos e serviços e permitir acesso a seus membros. Veja o tutorial sobre [configuração do console do desenvolvedor e [!DNL Postman]](../../../landing/postman.md) para obter instruções sobre como recuperar o `{ORG_ID}` informações. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | O nome da partição de sandbox virtual que você está usando. | `prod` |
| `TENANT_ID` | Uma ID usada para garantir que os recursos criados tenham o namespace adequado e estejam contidos na organização. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | O endpoint de URL para o qual você está fazendo chamadas de API. Esse valor é fixo e sempre é definido como: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | O identificador exclusivo do [!DNL Marketo] conta. Veja o tutorial sobre [autenticando seu [!DNL Marketo] instância](../adobe-applications/marketo/marketo-auth.md) para obter informações sobre como recuperar o `munchkinId`. | `123-ABC-456` |
| `sfdc_org_id` | A ID da organização do [!DNL Salesforce] conta. Consulte o seguinte [[!DNL Salesforce] guia](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) para obter mais informações sobre como adquirir o [!DNL Salesforce] ID da organização. | `00D4W000000FgYJUA0` |
| `has_abm` | Um valor booliano que indica se você está inscrito no [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | Um valor booliano que indica se você está inscrito no [!DNL Marketo Sales Insight]. | `false` |

{style="table-layout:auto"}

### Execução dos scripts

Com o seu [!DNL Postman] coleção e ambiente configurados, agora é possível executar o script por meio da variável [!DNL Postman] interface.

No [!DNL Postman] , selecione a pasta raiz do utilitário gerador automático e selecione **[!DNL Run]** no cabeçalho superior.

![pasta-raiz](../../images/tutorials/create/salesforce/root-folder.png)

A variável [!DNL Runner] é exibida. Aqui, verifique se todas as caixas de seleção estão marcadas e selecione **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![run-generator](../../images/tutorials/create/salesforce/run-generator.png)

Uma solicitação bem-sucedida cria os namespaces B2B e esquemas de acordo com as especificações beta.

## Conectar [!DNL Salesforce] para a Platform usando APIs

A documentação abaixo fornece informações sobre como se conectar [!DNL Salesforce] para a Platform usando APIs ou a interface do usuário:

- [Criar uma conexão básica do Salesforce usando a API do Serviço de fluxo](../../tutorials/api/create/crm/salesforce.md)
- [Explorar tabelas de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/tabular.md)
- [Criar um fluxo de dados para uma origem de CRM usando a API do Serviço de Fluxo](../../tutorials/api/collect/crm.md)

## Conectar [!DNL Salesforce] para a Platform usando a interface

- [Criar uma conexão de origem do Salesforce na interface](../../tutorials/ui/create/crm/salesforce.md)
- [Criar um fluxo de dados para uma conexão de CRM na interface](../../tutorials/ui/dataflow/crm.md)
