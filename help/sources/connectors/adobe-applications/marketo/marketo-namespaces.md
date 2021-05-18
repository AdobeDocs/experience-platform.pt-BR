---
keywords: Experience Platform, home, tópicos populares, conector de origem do Marketo, namespaces, esquemas
solution: Experience Platform
title: Namespaces do Marketo
topic-legacy: overview
description: Este documento fornece uma visão geral de namespaces personalizados necessários ao criar um conector de origem de Marketo Engage.
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: af728fb508c514db3d5871114f9a406c1ed428f2
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 5%

---

# (Beta) [!DNL Marketo Engage] namespaces e schemas

>[!IMPORTANT]
>
>A fonte [!DNL Marketo Engage] está atualmente em beta. O recurso e a documentação estão sujeitos a alterações.

Este documento fornece informações sobre a configuração subjacente para os namespaces e esquemas B2B usados com [!DNL Marketo Engage] (a seguir denominado &quot;[!DNL Marketo]&quot;). Este documento também fornece detalhes sobre a configuração do utilitário de automação do Postman necessário para gerar [!DNL Marketo] namespaces e esquemas B2B.

## Configure o namespace [!DNL Marketo] e o utilitário de geração automática de esquema

A primeira etapa no uso do namespace [!DNL Marketo] e do utilitário de geração automática de esquema é configurar o console do desenvolvedor de plataforma e o ambiente [!DNL Postman].

- Você pode baixar o namespace e o ambiente do utilitário de geração automática de esquema deste [repositório GitHub](https://git.corp.adobe.com/marketo-engineering/namespace_schema_utility).
- Para obter informações sobre como usar APIs de plataforma, incluindo detalhes sobre como coletar valores para cabeçalhos necessários e ler chamadas de API de amostra, consulte o guia sobre como [começar a usar APIs de plataforma](../../../../landing/api-guide.md).
- Para obter informações sobre como gerar suas credenciais para APIs da plataforma, consulte o tutorial em [autenticação e acesso a APIs do Experience Platform](../../../../landing/api-authentication.md).
- Para obter informações sobre como configurar [!DNL Postman] para APIs da plataforma, consulte o tutorial em [configurar o console do desenvolvedor e [!DNL Postman]](../../../../landing/postman.md).

Com um console do desenvolvedor da Platform e [!DNL Postman] configuradas, agora é possível começar a aplicar os valores de ambiente apropriados ao seu ambiente [!DNL Postman].

A tabela a seguir contém valores de exemplo e informações adicionais sobre como preencher o ambiente [!DNL Postman]:

| Variable | Descrição | Exemplo |
| --- | --- | --- |
| `CLIENT_SECRET` | Um identificador exclusivo usado para gerar `{ACCESS_TOKEN}`. Consulte o tutorial em [autenticar e acessar APIs do Experience Platform](../../../../landing/api-authentication.md) para obter informações sobre como recuperar seu `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | O JSON Web Token (JWT) é uma credencial de autenticação usada para gerar seu {ACCESS_TOKEN}. Consulte o tutorial em [autenticar e acessar APIs do Experience Platform](../../../../landing/api-authentication.md) para obter informações sobre como gerar seu `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | Um identificador exclusivo usado para autenticar chamadas para APIs do Experience Platform. Consulte o tutorial em [autenticar e acessar APIs do Experience Platform](../../../../landing/api-authentication.md) para obter informações sobre como recuperar seu `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | O token de autorização necessário para concluir chamadas para APIs do Experience Platform. Consulte o tutorial em [autenticar e acessar APIs do Experience Platform](../../../../landing/api-authentication.md) para obter informações sobre como recuperar seu `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | No que diz respeito a [!DNL Marketo], esse valor é fixo e sempre está definido como: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | O contêiner `global` contém todas as classes, grupos de campos de esquema, tipos de dados e esquemas fornecidos pelo Adobe e parceiro de Experience Platform. Em relação a [!DNL Marketo], esse valor é fixo e sempre está definido como `global`. | `global` |
| `PRIVATE_KEY` | Uma credencial usada para autenticar sua instância [!DNL Postman] para APIs do Experience Platform. Consulte o tutorial sobre como configurar o console do desenvolvedor e [configurar o console do desenvolvedor e [!DNL Postman]](../../../../landing/postman.md) para obter instruções sobre como recuperar seu {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Uma credencial usada para integrar ao Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | O Sistema Identity Management (IMS) fornece a estrutura para autenticação dos serviços de Adobe. No que diz respeito a [!DNL Marketo], esse valor é fixo e sempre está definido como: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Uma entidade corporativa que pode ser proprietária ou licenciar produtos e serviços e permitir o acesso a seus membros. Consulte o tutorial em [configurar o console do desenvolvedor e [!DNL Postman]](../../../../landing/postman.md) para obter instruções sobre como recuperar suas informações `{IMS_ORG}`. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | O nome da partição da sandbox virtual que você está usando. | `prod` |
| `TENANT_ID` | Uma ID usada para garantir que os recursos criados sejam namespacados corretamente e estejam contidos na organização IMS. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | O endpoint de URL para o qual você está fazendo chamadas de API. Esse valor é fixo e sempre está definido como: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | A ID exclusiva para sua conta [!DNL Marketo]. Consulte o tutorial em [autenticar sua [!DNL Marketo] instância](./marketo-auth.md) para obter informações sobre como recuperar seu `munchkinId`. | `123-ABC-456` |
| `sfdc_org_id` | A ID da organização da sua conta [!DNL Salesforce]. Consulte o [[!DNL Salesforce] guia](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) a seguir para obter mais informações sobre como adquirir a ID da organização [!DNL Salesforce]. | `00D4W000000FgYJUA0` |
| `msd_org_id` | A ID da organização da sua conta [!DNL Dynamics]. Consulte o [[!DNL Microsoft Dynamics] guia](https://docs.microsoft.com/en-us/power-platform/admin/determine-org-id-name) a seguir para obter mais informações sobre como adquirir a ID da organização [!DNL Dynamics]. | `f6438fab-67e8-4814-a6b5-8c8dcdf7a98f` |
| `has_abm` | Um valor booleano que indica se você está inscrito em [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | Um valor booleano que indica se você está inscrito em [!DNL Marketo Sales Insight]. | `false` |

{style=&quot;table-layout:auto&quot;}

### Execução dos scripts

Com sua coleção [!DNL Postman] e o ambiente configurados, agora é possível executar o script por meio da interface [!DNL Postman].

Na interface [!DNL Postman], selecione a pasta raiz do utilitário de gerador automático e selecione **[!DNL Run]** no cabeçalho superior.

![pasta raiz](../images/marketo/root-folder.png)

A interface [!DNL Runner] é exibida. A partir daqui, verifique se todas as caixas de seleção estão selecionadas e selecione **[!DNL Run Adobe I/O Access Token Generation + Automate Namespace creation]**.

![gerador de rodagem](../images/marketo/run-generator.png)

Uma solicitação bem-sucedida cria namespaces e schemas B2B de acordo com as especificações beta.

## [!DNL Marketo] namespaces

Os namespaces de identidade são um componente de [[!DNL Identity Service]](../../../../identity-service/home.md) que serve como indicadores do contexto ao qual uma identidade está relacionada.

Uma identidade totalmente qualificada inclui um valor de ID e um namespace. Um novo namespace personalizado é necessário para cada nova instância [!DNL Marketo] e combinação de conjunto de dados. Por exemplo, um conector de origem [!DNL Marketo] que assimila o conjunto de dados `programs` requer seu próprio namespace personalizado e outro conector de origem do Marketo que assimila o mesmo conjunto de dados também exige seu próprio namespace personalizado. Consulte a [visão geral dos namespaces](../../../../identity-service/namespaces.md) para obter mais informações.

O namespace [!DNL Marketo] é usado na identidade primária da entidade.

A tabela a seguir contém informações sobre a configuração subjacente para [!DNL Marketo] namespaces.

>[!NOTE]
>
>Role a tela para a esquerda/direita para exibir o conteúdo completo da tabela.

| Nome de exibição | Símbolo de identidade | Tipo de identidade | Tipo de emissor | Tipo de entidade emissor | Exemplo da ID do Munchkin |
| --- | --- | --- | --- | --- | --- |
| `marketo_person_{MUNCHKIN_ID}` | gerado automaticamente | `CROSS_DEVICE` | [!DNL Marketo] | `person` | `123-ABC-789` |
| `marketo_company_{MUNCHKIN_ID}` | gerado automaticamente | `B2B_ACCOUNT` | [!DNL Marketo] | `company` | `123-ABC-789` |
| `marketo_opportunity_{MUNCHKIN_ID}` | gerado automaticamente | `B2B_OPPORTUNITY` | [!DNL Marketo] | `opportunity` | `123-ABC-789` |
| `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | gerado automaticamente | `B2B_OPPORTUNITY_PERSON` | [!DNL Marketo] | `opportunity contact role` | `123-ABC-789` |
| `marketo_program_{MUNCHKIN_ID}` | gerado automaticamente | `B2B_CAMPAIGN` | [!DNL Marketo] | `program` | `123-ABC-789` |
| `marketo_program_member_{MUNCHKIN_ID}` | gerado automaticamente | `B2B_CAMPAIGN_MEMBER` | [!DNL Marketo] | `program member` | `123-ABC-789` |
| `marketo_static_list_{MUNCHKIN_ID}` | gerado automaticamente | `B2B_MARKETING_LIST` | [!DNL Marketo] | `static list` | `123-ABC-789` |
| `marketo_static_list_member_{MUNCHKIN_ID}` | gerado automaticamente | `B2B_MARKETING_LIST_MEMBER` | [!DNL Marketo] | `static list member` | `123-ABC-789` |
| `marketo_named_account_{MUNCHKIN_ID}` | gerado automaticamente | `B2B_ACCOUNT` | [!DNL Marketo] | `named account` | `123-ABC-789` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Salesforce] namespaces

Se você estiver inscrito na integração [!DNL Salesforce], o namespace [!DNL Salesforce] será usado na identidade secundária da entidade.

A tabela a seguir contém informações sobre a configuração subjacente para [!DNL Salesforce] namespaces.

>[!NOTE]
>
>Role a tela para a esquerda/direita para exibir o conteúdo completo da tabela.

| Nome de exibição | Símbolo de identidade | Tipo de identidade | Tipo de emissor | Tipo de entidade emissor | [!DNL Salesforce] exemplo de ID da organização da assinatura |
| --- | --- | --- | --- | --- | --- |
| `salesforce_lead_{SALESFORCE_ORGANIZATION_ID}` | gerado automaticamente | `CROSS_DEVICE` | [!DNL Salesforce] | `lead` | `00DA0000000Hz79` |
| `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | gerado automaticamente | `B2B_ACCOUNT` | [!DNL Salesforce] | `account` | `00DA0000000Hz79` |
| `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | gerado automaticamente | `B2B_OPPORTUNITY` | [!DNL Salesforce] | `opportunity` | `00DA0000000Hz79` |
| `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | gerado automaticamente | `B2B_OPPORTUNITY_PERSON` | [!DNL Salesforce] | `opportunity contact role` | `00DA0000000Hz79` |
| `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` | gerado automaticamente | `B2B_CAMPAIGN` | [!DNL Salesforce] | `campaign` | `00DA0000000Hz79` |
| `salesforce_campaign_member_{SALESFORCE_ORGANIZATION_ID}` | gerado automaticamente | `B2B_CAMPAIGN_MEMBER` | [!DNL Salesforce] | `campaign member` | `00DA0000000Hz79` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Microsoft Dynamics] namespaces

Se você estiver inscrito na integração [!DNL Dynamics], o namespace [!DNL Dynamics] será usado como identidade secundária da entidade.

A tabela a seguir contém informações sobre a configuração subjacente para [!DNL Dynamics] namespaces.

>[!NOTE]
>
>Role a tela para a esquerda/direita para exibir o conteúdo completo da tabela.

| Nome de exibição | Símbolo de identidade | Tipo de identidade | Tipo de emissor | Tipo de entidade emissor | [!DNL Dynamics] exemplo de ID da organização da assinatura |
| --- | --- | --- | --- | --- | --- |
| `microsoft_person_{DYNAMICS_ID}` | gerado automaticamente | `CROSS_DEVICE` | [!DNL Microsoft] | `person` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_account_{DYNAMICS_ID}` | gerado automaticamente | `B2B_ACCOUNT` | [!DNL Microsoft] | `account` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_{DYNAMICS_ID}` | gerado automaticamente | `B2B_OPPORTUNITY` | [!DNL Microsoft] | `opportunity` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_contact_connection_{DYNAMICS_ID}` | gerado automaticamente | `B2B_OPPORTUNITY_PERSON` | [!DNL Microsoft] | `opportunity relationship` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_{DYNAMICS_ID}` | gerado automaticamente | `B2B_CAMPAIGN` | [!DNL Microsoft] | `campaign` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_member_{DYNAMICS_ID}` | gerado automaticamente | `B2B_CAMPAIGN_MEMBER` | [!DNL Microsoft] | `campaign member` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |

{style=&quot;table-layout:auto&quot;}

## [!DNL Marketo] esquemas

A Experience Platform utiliza esquemas para descrever a estrutura dos dados de forma consistente e reutilizável. Ao definir os dados de forma consistente em todos os sistemas, fica mais fácil manter o significado e, portanto, obter valor dos dados.

Para que os dados possam ser assimilados na Platform, um schema deve ser composto para descrever a estrutura dos dados e fornecer restrições ao tipo de dados que pode ser contido em cada campo. Os esquemas consistem em uma classe base e zero ou mais grupos de campos de esquema.

Para obter mais informações sobre o modelo de composição do schema, incluindo princípios de design e práticas recomendadas, consulte as [noções básicas da composição do schema](../../../../xdm/schema/composition.md).

A tabela a seguir contém informações sobre a configuração subjacente de [!DNL Marketo] schemas.

>[!NOTE]
>
>Role a tela para a esquerda/direita para exibir o conteúdo completo da tabela.

| Nome do esquema | Classe base | Grupos de campos | [!DNL Profile] no Esquema | Identidade primária | Namespace da identidade primária | Identidade secundária | Namespace de identidade secundária | Relação | Notas |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `[!DNL Marketo] Company {MUNCHKIN_ID}` | Conta Comercial XDM | Detalhes da conta comercial XDM | Ativado | `accountID` na classe base | `marketo_company_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` na classe base | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` no grupo de campos Detalhes da conta comercial XDM</li><li>Tipo: um para um</li><li>Esquema de referência: `[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>Namespace: `marketo_company_{MUNCHKIN_ID}`</li></ul> |
| `[!DNL Marketo] Person {MUNCHKIN_ID}` | Perfil individual XDM | <ul><li>Detalhes da Pessoa Comercial XDM</li><li>Componentes de Pessoa Comercial XDM</li><li>IdentityMap</li></ul> | Ativado | `personID` na classe base | `marketo_person_{MUNCHKIN_ID}` | <ol><li>`extSourceSystemAudit.externalID` do grupo de campos Detalhes da Pessoa Comercial XDM</li><li>`workEmail.address` do grupo de campos Detalhes da Pessoa Comercial XDM</li><li>`identityMap` do grupo de campos do Mapa de identidade</ol></li> | <ol><li>`salesforce_lead_{SALESFORCE_ORGANIZATION_ID}`</li><li>Email</li><li>ECID</li></ol> | <ul><li>`personComponents.sourceAccountID` do grupo de campos Componentes da Pessoa Comercial XDM</li><li>Tipo: Muitos para um</li><li>Esquema de referência: `[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>Namespace: `marketo_company_{MUNCHKIN_ID}`</li><li>Propriedade de destino: `accountID`</li><li>Nome do relacionamento do schema atual: Conta</li><li>Nome do relacionamento do schema de referência: Pessoas</li></ul> |
| `[!DNL Marketo] Opportunity {MUNCHKIN_ID}` | Oportunidade de negócios XDM | Detalhes da oportunidade de negócios XDM | Ativado | `opportunityID` na classe base | `marketo_opportunity_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` na classe base | `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountID` na classe base</li><li>Tipo: Muitos para um</li><li>Esquema de referência: `[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>Namespace: `marketo_company_{MUNCHKIN_ID}`</li><li>Propriedade de destino: `accountID`</li><li>Nome do relacionamento do schema atual: Conta</li><li>Nome do relacionamento do schema de referência: Oportunidades</li></ul> |
| `[!DNL Marketo] Opportunity Contact Role {MUNCHKIN_ID}` | Relação de Pessoa da Oportunidade de Negócios XDM | None | Ativado | `opportunityPersonID` na classe base | `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` na classe base | `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | Primeira relação<ul><li>`personID` na classe base</li><li>Tipo: Muitos para um</li><li>Esquema de referência: `[!DNL Marketo] Person {MUNCHKIN_ID}`</li><li>Namespace: `marketo_person_{MUNCHKIN_ID}`</li><li>Propriedade de destino: `personID`</li><li>Nome do relacionamento do schema atual: Pessoa</li><li>Nome do relacionamento do schema de referência: Oportunidades</li></ul>Segunda relação<ul><li>`opportunityID` na classe base</li><li>Tipo: Muitos para um</li><li>Esquema de referência: `[!DNL Marketo] Opportunity {MUNCHKIN_ID}`</li><li>Namespace: `marketo_opportunity_{MUNCHKIN_ID}`</li><li>Propriedade de destino: `opportunityID`</li><li>Nome do relacionamento do schema atual: Oportunidade</li><li>Nome do relacionamento do schema de referência: Pessoas</li></ul> |
| `[!DNL Marketo] Program {MUNCHKIN_ID}` | Campanha comercial XDM | Detalhes da campanha comercial XDM | Ativado | `campaignID` na classe base | `marketo_program_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` na classe base | `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` |
| `[!DNL Marketo] Program Member {MUNCHKIN_ID}` | Membro da Campanha Comercial XDM | Detalhes do Membro da Campanha Empresarial XDM | Ativado | `campaignMemberID` na classe base | `marketo_program_member_{MUNCHKIN_ID}` | Nenhum | Nenhum | Primeira relação<ul><li>`personID` na classe base</li><li>Tipo: Muitos para um</li><li>Esquema de referência: Pessoa do Marketo {MUNCHKIN_ID}</li><li>Namespace: `marketo_person_{MUNCHKIN_ID}`</li><li>Propriedade de destino: `personID`</li><li>Nome do relacionamento do schema atual: Pessoa</li><li>Nome do relacionamento do schema de referência: Programas</li></ul>Segunda relação<ul><li>`campaignID` na classe base</li><li>Tipo: Muitos para um</li><li>Esquema de referência: `[!DNL Marketo] Program {MUNCHKIN_ID}`</li><li>Namespace: `marketo_program_{MUNCHKIN_ID}`</li><li>Propriedade de destino: `campaignID`</li><li>Nome do relacionamento do schema atual: Programa</li><li>Nome do relacionamento do schema de referência: Pessoas</li></ul> |
| `[!DNL Marketo] Static List {MUNCHKIN_ID}` | Lista de marketing comercial XDM | Nenhum | Ativado | `marketingListID` na classe base | `marketo_static_list_{MUNCHKIN_ID}` | Nenhum | Nenhum | Nenhum | A Lista estática não é sincronizada de [!DNL Salesforce] e, portanto, não tem uma identidade secundária. |
| `[!DNL Marketo] Static List Member {MUNCHKIN_ID}` | Membros da Lista de Marketing Comercial XDM | Nenhum | Ativado | `marketingListMemberID` na classe base | `marketo_static_list_member_{MUNCHKIN_ID}` | Nenhum | Nenhum | Primeira relação<ul><li>`personID` na classe base</li><li>Tipo: Muitos para um</li><li>Esquema de referência: `[!DNL Marketo] Person {MUNCHKIN_ID}`</li><li>Namespace: `marketo_person_{MUNCHKIN_ID}`</li><li>Propriedade de destino: `personID`</li><li>Nome do relacionamento do schema atual: Pessoa</li><li>Nome do relacionamento do schema de referência: Listas</li></ul>Segunda relação<ul><li>`marketingListID` na classe base</li><li>Tipo: Muitos para um</li><li>Esquema de referência: `[!DNL Marketo] Static List {MUNCHKIN_ID}`</li><li>Namespace: `marketo_static_list_{MUNCHKIN_ID}`</li><li>Propriedade de destino: `marketingListID`</li><li>Nome do relacionamento do schema atual: Lista</li><li>Nome do relacionamento do schema de referência: Pessoas</li></ul> | O membro da lista estática não é sincronizado de [!DNL Salesforce] e, portanto, não tem uma identidade secundária. |
| `[!DNL Marketo] Named Account {MUNCHKIN_ID}` | Conta Comercial XDM | Detalhes da conta comercial XDM | Ativado | `accountID` na classe base | `marketo_named_account_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` na classe base | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` no grupo de campos Detalhes da conta comercial XDM</li><li>Tipo: um para um</li><li>Esquema de referência: `[!DNL Marketo] Named Account {MUNCHKIN_ID}`</li><li>Namespace: `marketo_named_account_{MUNCHKIN_ID}` |
| [!DNL Marketo] Atividade `{MUNCHKIN ID}` | ExperiênciaEvento XDM | <ul><li>Visitar WebPage</li><li>Novo cliente potencial</li><li>Converter lead</li><li>Adicionar à lista</li><li>Remover da lista</li><li>Adicionar à Oportunidade</li><li>Remover da Oportunidade</li><li>Formulário preenchido</li><li>Cliques em links</li><li>Email Entregue</li><li>Email aberto</li><li>Email clicado</li><li>Rejeição de email</li><li>Enviar email com rejeição suave</li><li>Email Inscrito</li><li>Pontuação alterada</li><li>Oportunidade Atualizada</li><li>Status in Campaign Progression Changed (Status da Progressão da Campanha Alterado)</li><li>Identificador de pessoa</li><li>URL da Web do Marketo | Ativado | `personID` do grupo de campos Identificador de Pessoa | `marketo_person_{MUNCHKIN_ID}` | Nenhum | Nenhum | Primeira relação<ul><li>`listOperations.listID` campo</li><li>Tipo: um para um</li><li>Esquema de referência: `[!DNL Marketo] Static List {MUNCHKIN_ID}`</li><li>Namespace: `marketo_static_list_{MUNCHKIN_ID}`</li></ul>Segunda relação<ul><li>`opportunityEvent.opportunityID` campo</li><li>Tipo: um para um</li><li>Esquema de referência: `[!DNL Marketo] Opportunity {MUNCHKIN_ID}`</li><li>Namespace: `marketo_opportunity_{MUNCHKIN_ID}`</li></ul>Terceiro relacionamento<ul><li>`leadOperation.campaignProgression.campaignID` campo</li><li>Tipo: um para um</li><li>Esquema de referência: `[!DNL Marketo] Program {MUNCHKIN_ID}`</li><li>Namespace: `marketo_program_{MUNCHKIN_ID}`</li></ul> | A identidade primária do schema `[!DNL Marketo] Activity {MUNCHKIN_ID}` é `personID`, que é a mesma identidade primária do schema `[!DNL Marketo] Person {MUNCHKIN_ID}`. |

{style=&quot;table-layout:auto&quot;}

## Próximas etapas

Para saber como conectar seus dados [!DNL Marketo] à Platform, consulte o tutorial em [criar um conector de origem Marketo na interface do usuário](../../../tutorials/ui/create/adobe-applications/marketo.md).
