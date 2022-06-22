---
keywords: Experience Platform, home, tópicos populares, conector de origem do Marketo, namespaces, schemas, b2b, B2B
solution: Experience Platform
title: Espaços de nomes e esquemas B2B
topic-legacy: overview
description: Este documento fornece uma visão geral de namespaces personalizados necessários ao criar um conector de origem B2B.
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: 9640124bd8fb8b7d069d433369468f8bdb57871b
workflow-type: tm+mt
source-wordcount: '1700'
ht-degree: 4%

---

# Espaços de nomes e esquemas B2B

Este documento fornece informações sobre a configuração subjacente para os namespaces e esquemas a serem usados com fontes B2B. Este documento também fornece detalhes sobre a configuração do utilitário de automação Postman necessário para gerar namespaces e esquemas B2B.

>[!IMPORTANT]
>
>Você deve ter acesso ao [Real-time Customer Data Platform B2B Edition](../../../../rtcdp/b2b-overview.md) para que os esquemas B2B participem em [Perfil do cliente em tempo real](../../../../profile/home.md).

## Configurar namespaces B2B e utilitário de geração automática de esquema

A primeira etapa no uso do namespace B2B e do utilitário de geração automática de esquema é configurar o console do desenvolvedor do Platform e [!DNL Postman] ambiente.

- É possível baixar o namespace e o ambiente do utilitário de geração automática de esquema dessa [Repositório GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Para obter informações sobre como usar APIs de plataforma, incluindo detalhes sobre como coletar valores para cabeçalhos necessários e ler chamadas de API de exemplo, consulte o guia em [introdução às APIs do Platform](../../../../landing/api-guide.md).
- Para obter informações sobre como gerar suas credenciais para APIs da plataforma, consulte o tutorial em [autenticação e acesso às APIs do Experience Platform](../../../../landing/api-authentication.md).
- Para obter informações sobre como configurar [!DNL Postman] para APIs da plataforma, consulte o tutorial em [configurar o console do desenvolvedor e [!DNL Postman]](../../../../landing/postman.md).

Com um console de desenvolvedor do Platform e [!DNL Postman] , agora é possível começar a aplicar os valores de ambiente apropriados ao [!DNL Postman] ambiente.

A tabela a seguir contém valores de exemplo e informações adicionais sobre como preencher [!DNL Postman] ambiente:

| Variable | Descrição | Exemplo |
| --- | --- | --- |
| `CLIENT_SECRET` | Um identificador exclusivo usado para gerar o `{ACCESS_TOKEN}`. Veja o tutorial em [autenticação e acesso às APIs do Experience Platform](../../../../landing/api-authentication.md) para obter informações sobre como recuperar seu `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | O JSON Web Token (JWT) é uma credencial de autenticação usada para gerar seu {ACCESS_TOKEN}. Veja o tutorial em [autenticação e acesso às APIs do Experience Platform](../../../../landing/api-authentication.md) para obter informações sobre como gerar seu `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | Um identificador exclusivo usado para autenticar chamadas para APIs do Experience Platform. Veja o tutorial em [autenticação e acesso às APIs do Experience Platform](../../../../landing/api-authentication.md) para obter informações sobre como recuperar seu `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | O token de autorização necessário para concluir chamadas para APIs do Experience Platform. Veja o tutorial em [autenticação e acesso às APIs do Experience Platform](../../../../landing/api-authentication.md) para obter informações sobre como recuperar seu `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | No que diz respeito à [!DNL Marketo], esse valor é fixo e sempre está definido como: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | O `global` O container contém todas as classes, grupos de campos do esquema, tipos de dados e esquemas fornecidos pelo Adobe e parceiro de Experience Platform. No que diz respeito à [!DNL Marketo], esse valor é fixo e sempre está definido como `global`. | `global` |
| `PRIVATE_KEY` | Uma credencial usada para autenticar seu [!DNL Postman] para APIs do Experience Platform. Consulte o tutorial sobre como configurar o console do desenvolvedor e [configurar o console do desenvolvedor e [!DNL Postman]](../../../../landing/postman.md) para obter instruções sobre como recuperar o {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Uma credencial usada para integrar ao Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | O Sistema Identity Management (IMS) fornece a estrutura para autenticação dos serviços da Adobe. No que diz respeito à [!DNL Marketo], esse valor é fixo e sempre está definido como: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Uma entidade corporativa que pode ser proprietária ou licenciar produtos e serviços e permitir o acesso a seus membros. Veja o tutorial em [configurar o console do desenvolvedor e [!DNL Postman]](../../../../landing/postman.md) para obter instruções sobre como recuperar seu `{ORG_ID}` informações. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | O nome da partição da sandbox virtual que você está usando. | `prod` |
| `TENANT_ID` | Uma ID usada para garantir que os recursos criados sejam namespacados corretamente e estejam contidos na organização IMS. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | O endpoint de URL para o qual você está fazendo chamadas de API. Esse valor é fixo e sempre está definido como: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |

{style=&quot;table-layout:auto&quot;}

### Execução dos scripts

Com seu [!DNL Postman] coleção e ambiente configuradas, agora é possível executar o script pelo [!DNL Postman] interface.

No [!DNL Postman] selecione a pasta raiz do utilitário autogerador e selecione **[!DNL Run]** no cabeçalho superior.

![pasta raiz](../images/marketo/root-folder.png)

O [!DNL Runner] é exibida. A partir daqui, verifique se todas as caixas de seleção estão selecionadas e, em seguida, selecione **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![gerador de rodagem](../images/marketo/run-generator.png)

Uma solicitação bem-sucedida cria os namespaces e schemas necessários para o B2B.

## Namespaces B2B

Os namespaces de identidade são um componente do [[!DNL Identity Service]](../../../../identity-service/home.md) que servem para distinguir o contexto ou o tipo de uma identidade. Uma identidade totalmente qualificada inclui um valor de ID e um namespace. Consulte a [visão geral do namespaces](../../../../identity-service/namespaces.md) para obter mais informações.

Os namespaces B2B são usados na identidade primária da entidade.

A tabela a seguir contém informações sobre a configuração subjacente para namespaces B2B.

>[!NOTE]
>
>Role a tela para a esquerda/direita para exibir o conteúdo completo da tabela.

| Nome de exibição | Símbolo de identidade | Tipo de identidade |
| --- | --- | --- |
| Pessoa B2B | `b2b_person` | `CROSS_DEVICE` |
| Conta B2B | `b2b_account` | `B2B_ACCOUNT` |
| Oportunidade B2B | `b2b_opportunity` | `B2B_OPPORTUNITY` |
| Relação de Pessoa da Oportunidade B2B | `b2b_opportunity_person_relation` | `B2B_OPPORTUNITY_PERSON` |
| Campanha B2B | `b2b_campaign` | `B2B_CAMPAIGN` |
| Membro da Campanha B2B | `b2b_campaign_member` | `B2B_CAMPAIGN_MEMBER` |
| Lista de marketing B2B | `b2b_marketing_list` | `B2B_MARKETING_LIST` |
| Membro da Lista de Marketing B2B | `b2b_marketing_list_member` | `B2B_MARKETING_LIST_MEMBER` |
| Relação de Pessoa da Conta B2B | `b2b_account_person_relation` | `B2B_ACCOUNT_PERSON` |

{style=&quot;table-layout:auto&quot;}

## Esquemas B2B

A Experience Platform utiliza esquemas para descrever a estrutura dos dados de forma consistente e reutilizável. Ao definir os dados de forma consistente em todos os sistemas, fica mais fácil manter o significado e, portanto, obter valor dos dados.

Para que os dados possam ser assimilados na Platform, um schema deve ser composto para descrever a estrutura dos dados e fornecer restrições ao tipo de dados que pode ser contido em cada campo. Os esquemas consistem em uma classe base e zero ou mais grupos de campos de esquema.

Para obter mais informações sobre o modelo de composição de schema, incluindo princípios de design e práticas recomendadas, consulte o [noções básicas da composição do schema](../../../../xdm/schema/composition.md).

A tabela a seguir contém informações sobre a configuração subjacente dos esquemas B2B.

>[!NOTE]
>
>Role a tela para a esquerda/direita para exibir o conteúdo completo da tabela.

| Nome do esquema | Classe base | Grupos de campos | [!DNL Profile] no Esquema | Identidade primária | Namespace da identidade primária | Identidade secundária | Namespace de identidade secundária | Relação | Notas |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Conta B2B | [Conta Comercial XDM](../../../../xdm/classes/b2b/business-account.md) | Detalhes da conta comercial XDM | Ativado | `accountKey.sourceKey` na classe base | Conta B2B | `extSourceSystemAudit.externalKey.sourceKey` na classe base | Conta B2B | <ul><li>`accountParentKey.sourceKey` no grupo de campos Detalhes da conta comercial XDM</li><li>Propriedade de destino: `/accountKey/sourceKey`</li><li>Tipo: um para um</li><li>Esquema de referência: Conta B2B</li><li>Namespace: Conta B2B</li></ul> |
| Pessoa B2B | [Perfil individual XDM](../../../../xdm/classes/individual-profile.md) | <ul><li>Detalhes da Pessoa Comercial XDM</li><li>Componentes de Pessoa Comercial XDM</li><li>IdentityMap</li><li>Detalhes de consentimento e preferência</li></ul> | Ativado | `b2b.personKey.sourceKey` no Grupo de campos Detalhes da pessoa comercial do XDM | Pessoa B2B | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` do grupo de campos Detalhes da Pessoa Comercial XDM</li><li>`workEmail.address` do grupo de campos Detalhes da Pessoa Comercial XDM</ol></li> | <ol><li>Pessoa B2B</li><li>Email</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` do grupo de campos Componentes da Pessoa Comercial XDM</li><li>Tipo: Muitos para um</li><li>Esquema de referência: Conta B2B</li><li>Namespace: Conta B2B</li><li>Propriedade de destino: accountKey.sourceKey</li><li>Nome do relacionamento do schema atual: Conta</li><li>Nome do relacionamento do schema de referência: Pessoas</li></ul> |
| Oportunidade B2B | [Oportunidade de negócios XDM](../../../../xdm/classes/b2b/business-opportunity.md) | Detalhes da oportunidade de negócios XDM | Ativado | `opportunityKey.sourceKey` na classe base | Oportunidade B2B | `extSourceSystemAudit.externalKey.sourceKey` na classe base | Oportunidade B2B | <ul><li>`accountKey.sourceKey` na classe base</li><li>Tipo: Muitos para um</li><li>Esquema de referência: Conta B2B</li><li>Namespace: Conta B2B</li><li>Propriedade de destino: `accountKey.sourceKey`</li><li>Nome do relacionamento do schema atual: Conta</li><li>Nome do relacionamento do schema de referência: Oportunidades</li></ul> |
| Relação de Pessoa da Oportunidade B2B | [Relação de Pessoa da Oportunidade de Negócios XDM](../../../../xdm/classes/b2b/business-opportunity-person-relation.md) | None | Ativado | `opportunityPersonKey.sourceKey` na classe base | Relação de Pessoa da Oportunidade B2B | `extSourceSystemAudit.externalKey.sourceKey` na classe base | Relação de Pessoa da Oportunidade B2B | **Primeira relação**<ul><li>`personKey.sourceKey` na classe base</li><li>Tipo: Muitos para um</li><li>Esquema de referência: Pessoa B2B</li><li>Namespace: Pessoa B2B</li><li>Propriedade de destino: b2b.personKey.sourceKey</li><li>Nome do relacionamento do schema atual: Pessoa</li><li>Nome do relacionamento do schema de referência: Oportunidades</li></ul>**Segunda relação**<ul><li>`opportunityKey.sourceKey` na classe base</li><li>Tipo: Muitos para um</li><li>Esquema de referência: Oportunidade B2B </li><li>Namespace: Oportunidade B2B </li><li>Propriedade de destino: `opportunityKey.sourceKey`</li><li>Nome do relacionamento do schema atual: Oportunidade</li><li>Nome do relacionamento do schema de referência: Pessoas</li></ul> |
| Campanha B2B | [Campanha comercial XDM](../../../../xdm/classes/b2b/business-campaign.md) | Detalhes da campanha comercial XDM | Ativado | `campaignKey.sourceKey` na classe base | Campanha B2B | `extSourceSystemAudit.externalKey.sourceKey` na classe base | Campanha B2B |
| Membro da Campanha B2B | [Membros da Campanha Comercial XDM](../../../../xdm/classes/b2b/business-campaign-members.md) | Detalhes do Membro da Campanha Empresarial XDM | Ativado | `ccampaignMemberKey.sourceKey` na classe base | Membro da Campanha B2B | `extSourceSystemAudit.externalKey.sourceKey` na classe base | Membro da Campanha B2B | **Primeira relação**<ul><li>`personKey.sourceKey` na classe base</li><li>Tipo: Muitos para um</li><li>Esquema de referência: Pessoa B2B</li><li>Namespace: Pessoa B2B</li><li>Propriedade de destino: `b2b.personKey.sourceKey`</li><li>Nome do relacionamento do schema atual: Pessoa</li><li>Nome do relacionamento do schema de referência: Campanhas</li></ul>**Segunda relação**<ul><li>`campaignKey.sourceKey` na classe base</li><li>Tipo: Muitos para um</li><li>Esquema de referência: Campanha B2B</li><li>Namespace: Campanha B2B</li><li>Propriedade de destino: `campaignKey.sourceKey`</li><li>Nome do relacionamento do schema atual: Campanha</li><li>Nome do relacionamento do schema de referência: Pessoas</li></ul> |
| Lista de marketing B2B | [Lista de marketing comercial XDM](../../../../xdm/classes/b2b/business-marketing-list.md) | Nenhum | Ativado | `marketingListKey.sourceKey` na classe base | Lista de marketing B2B | Nenhum | Nenhum | Nenhum | A Lista Estática não é sincronizada a partir de [!DNL Salesforce] e, portanto, não tem uma identidade secundária. |
| Membro da Lista de Marketing B2B | [Membros da Lista de Marketing Comercial XDM](../../../../xdm/classes/b2b/business-marketing-list-members.md) | Nenhum | Ativado | `marketingListMemberKey.sourceKey` na classe base | Membro da Lista de Marketing B2B | Nenhum | Nenhum | **Primeira relação**<ul><li>`PersonKey.sourceKey` na classe base</li><li>Tipo: Muitos para um</li><li>Esquema de referência: Pessoa B2B</li><li>Namespace: Pessoa B2B</li><li>Propriedade de destino: `b2b.personKey.sourceKey`</li><li>Nome do relacionamento do schema atual: Pessoa</li><li>Nome do relacionamento do schema de referência: Listas de marketing</li></ul>**Segunda relação**<ul><li>`marketingListKey.sourceKey` na classe base</li><li>Tipo: Muitos para um</li><li>Esquema de referência: Lista de marketing B2B</li><li>Namespace: Lista de marketing B2B</li><li>Propriedade de destino: `marketingListKey.sourceKey`</li><li>Nome do relacionamento do schema atual: Lista de marketing</li><li>Nome do relacionamento do schema de referência: Pessoas</li></ul> | O membro da lista estática não é sincronizado do [!DNL Salesforce] e, portanto, não tem uma identidade secundária. |
| Atividade B2B | [ExperiênciaEvento XDM](../../../../xdm/classes/experienceevent.md) | <ul><li>Visitar WebPage</li><li>Novo cliente potencial</li><li>Converter lead</li><li>Adicionar à lista</li><li>Remover da lista</li><li>Adicionar à Oportunidade</li><li>Remover da Oportunidade</li><li>Formulário preenchido</li><li>Cliques em links</li><li>Email Entregue</li><li>Email aberto</li><li>Email clicado</li><li>Rejeição de email</li><li>Enviar email com rejeição suave</li><li>Email Inscrito</li><li>Pontuação alterada</li><li>Oportunidade Atualizada</li><li>Status in Campaign Progression Changed (Status da Progressão da Campanha Alterado)</li><li>Identificador de pessoa</li><li>URL da Web do Marketo</li><li>Momento interessante</li><li>Chame o Webhook</li><li>Alterar a cadência da campanha</li><li>Estágio da Receita Alterado</li><li>Mesclar leads</li><li>Email enviado</li></ul> | Ativado | `personKey.sourceKey` do grupo de campos Identificador de Pessoa | Pessoa B2B | Nenhum | Nenhum | **Primeira relação**<ul><li>`listOperations.listKey.sourceKey` campo</li><li>Tipo: um para um</li><li>Esquema de referência: Lista de marketing B2B</li><li>Namespace: Lista de marketing B2B</li></ul>**Segunda relação**<ul><li>`opportunityEvent.opportunityKey.sourceKey` campo</li><li>Tipo: um para um</li><li>Esquema de referência: Oportunidade B2B</li><li>Namespace: Oportunidade B2B</li></ul>**Terceiro relacionamento**<ul><li>`leadOperation.campaignProgression.campaignKey.sourceKey` campo</li><li>Tipo: um para um</li><li>Esquema de referência: Campanha B2B</li><li>Namespace: Campanha B2B</li></ul> | `ExperienceEvent` é diferente das entidades. A identidade do evento de experiência é a pessoa que fez a atividade. |
| Relação de Pessoa da Conta B2B | [Relação de Pessoa da Conta Comercial XDM](../../../../xdm/classes/b2b/business-account-person-relation.md) | Mapa de identidade | Ativado | `accountPersonKey.sourceKey` na classe base | Relação de Pessoa da Conta B2B | Nenhum | Nenhum | **Primeira relação**<ul><li>`personKey.sourceKey` na classe base</li><li>Tipo: Muitos para um</li><li>Esquema de referência: Pessoa B2B</li><li>Namespace: Pessoa B2B</li><li>Propriedade de destino: `b2b.personKey.SourceKey`</li><li>Nome do relacionamento do schema atual: Pessoas</li><li>Nome do relacionamento do schema de referência: Conta</li></ul>**Segunda relação**<ul><li>`accountKey.sourceKey` na classe base</li><li>Tipo: Muitos para um</li><li>Esquema de referência: Conta B2B</li><li>Namespace: Conta B2B</li><li>Propriedade de destino: `accountKey.sourceKey`</li><li>Nome do relacionamento do schema atual: Conta</li><li>Nome do relacionamento do schema de referência: Pessoas</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Próximas etapas

Para saber como conectar seu [!DNL Marketo] dados para a Platform, consulte o tutorial em [criar um conector de origem do Marketo na interface do usuário](../../../tutorials/ui/create/adobe-applications/marketo.md).
