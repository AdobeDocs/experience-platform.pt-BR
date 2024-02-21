---
title: Namespaces e esquemas B2B
description: Este documento fornece uma visão geral dos namespaces personalizados necessários ao criar um conector de origem B2B.
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: 5e8bb04ca18159eab98b2f7f0bba8cb1488a1f26
workflow-type: tm+mt
source-wordcount: '1620'
ht-degree: 4%

---

# Namespaces e esquemas B2B

>[!NOTE]
>
>Você pode usar modelos na interface do usuário do Adobe Experience Platform para agilizar a criação de ativos para dados B2B e B2C. Para obter mais informações, leia o guia em [uso de modelos na interface do usuário da Platform](../../../tutorials/ui/templates.md).

Este documento fornece informações sobre a configuração subjacente para os namespaces e esquemas a serem usados com origens B2B. Este documento também fornece detalhes sobre a configuração do utilitário de automação do Postman necessário para gerar namespaces B2B e esquemas.

>[!IMPORTANT]
>
>Você deve ter acesso a [Adobe Real-time Customer Data Platform B2B Edition](../../../../rtcdp/b2b-overview.md) para que os esquemas B2B participem em [Perfil do cliente em tempo real](../../../../profile/home.md).

## Configurar namespaces B2B e o utilitário de geração automática de esquema

A primeira etapa no uso do namespace B2B e do utilitário de geração automática de esquema é configurar o console do desenvolvedor da Platform e [!DNL Postman] ambiente.

- Você pode baixar a coleção de utilitários de geração automática de namespace e esquema e o ambiente a partir deste [Repositório do GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Para obter informações sobre como usar APIs da plataforma, incluindo detalhes sobre como coletar valores para cabeçalhos necessários e ler chamadas de API de amostra, consulte o manual em [introdução às APIs da Platform](../../../../landing/api-guide.md).
- Para obter informações sobre como gerar suas credenciais para APIs da Platform, consulte o tutorial em [autenticação e acesso às APIs do Experience Platform](../../../../landing/api-authentication.md).
- Para obter informações sobre como configurar [!DNL Postman] para APIs da Platform, consulte o tutorial em [configuração do console do desenvolvedor e [!DNL Postman]](../../../../landing/postman.md).

Com um console de desenvolvedor da Platform e [!DNL Postman] configurada, agora é possível começar a aplicar os valores de ambiente apropriados às suas [!DNL Postman] ambiente.

A tabela a seguir contém valores de exemplo, bem como informações adicionais sobre como preencher o [!DNL Postman] ambiente:

| Variable | Descrição | Exemplo |
| --- | --- | --- |
| `CLIENT_SECRET` | Um identificador exclusivo usado para gerar sua `{ACCESS_TOKEN}`. Veja o tutorial sobre [autenticação e acesso às APIs do Experience Platform](../../../../landing/api-authentication.md) para obter informações sobre como recuperar o `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | O JSON Web Token (JWT) é uma credencial de autenticação usada para gerar seu {ACCESS_TOKEN}. Veja o tutorial sobre [autenticação e acesso às APIs do Experience Platform](../../../../landing/api-authentication.md) para obter informações sobre como gerar seus `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | Um identificador exclusivo usado para autenticar chamadas para APIs Experience Platform. Veja o tutorial sobre [autenticação e acesso às APIs do Experience Platform](../../../../landing/api-authentication.md) para obter informações sobre como recuperar o `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | O token de autorização necessário para completar chamadas para APIs de Experience Platform. Veja o tutorial sobre [autenticação e acesso às APIs do Experience Platform](../../../../landing/api-authentication.md) para obter informações sobre como recuperar o `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | No que diz respeito a [!DNL Marketo], esse valor é fixo e sempre é definido como: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | A variável `global` o container contém todas as classes padrão fornecidas por Adobe e parceiros de Experience Platform, grupos de campos de esquema, tipos de dados e esquemas. No que diz respeito a [!DNL Marketo], esse valor é fixo e sempre é definido como `global`. | `global` |
| `PRIVATE_KEY` | Uma credencial usada para autenticar seu [!DNL Postman] para APIs Experience Platform. Consulte o tutorial sobre a configuração do console do desenvolvedor e [configuração do console do desenvolvedor e [!DNL Postman]](../../../../landing/postman.md) para obter instruções sobre como recuperar o {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Uma credencial usada para integrar ao Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | O Sistema Identity Management (IMS) fornece a estrutura para autenticação de serviços da Adobe. No que diz respeito a [!DNL Marketo], esse valor é fixo e sempre é definido como: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Uma entidade corporativa que pode ser proprietária ou licenciar produtos e serviços e permitir acesso a seus membros. Veja o tutorial sobre [configuração do console do desenvolvedor e [!DNL Postman]](../../../../landing/postman.md) para obter instruções sobre como recuperar o `{ORG_ID}` informações. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | O nome da partição de sandbox virtual que você está usando. | `prod` |
| `TENANT_ID` | Uma ID usada para garantir que os recursos criados tenham o namespace adequado e estejam contidos na organização. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | O endpoint de URL para o qual você está fazendo chamadas de API. Esse valor é fixo e sempre é definido como: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |

{style="table-layout:auto"}

### Execução dos scripts

Com o seu [!DNL Postman] coleção e ambiente configurados, agora é possível executar o script por meio da variável [!DNL Postman] interface.

No [!DNL Postman] , selecione a pasta raiz do utilitário gerador automático e selecione **[!DNL Run]** no cabeçalho superior.

![pasta-raiz](../images/marketo/root-folder.png)

A variável [!DNL Runner] é exibida. Aqui, verifique se todas as caixas de seleção estão marcadas e selecione **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![run-generator](../images/marketo/run-generator.png)

Uma solicitação bem-sucedida cria os namespaces e esquemas necessários para o B2B.

## Namespaces B2B

Os namespaces de identidade são um componente de [[!DNL Identity Service]](../../../../identity-service/home.md) que servem para distinguir o contexto de uma identidade. Uma identidade totalmente qualificada inclui um valor de identidade e um namespace. Leia o [visão geral dos namespaces](../../../../identity-service/features/namespaces.md) para obter mais informações.

Os namespaces B2B são usados na identidade principal da entidade.

A tabela a seguir contém informações sobre a configuração subjacente para namespaces B2B.

>[!NOTE]
>
>Role a tela para a esquerda/direita para visualizar o conteúdo completo da tabela.

| Nome de exibição | Símbolo de identidade | Tipo de identidade |
| --- | --- | --- |
| Pessoa B2B | `b2b_person` | `CROSS_DEVICE` |
| Conta B2B | `b2b_account` | `B2B_ACCOUNT` |
| Oportunidade B2B | `b2b_opportunity` | `B2B_OPPORTUNITY` |
| Relação pessoal da oportunidade B2B | `b2b_opportunity_person_relation` | `B2B_OPPORTUNITY_PERSON` |
| Campanha B2B | `b2b_campaign` | `B2B_CAMPAIGN` |
| Membro da campanha B2B | `b2b_campaign_member` | `B2B_CAMPAIGN_MEMBER` |
| Lista de marketing B2B | `b2b_marketing_list` | `B2B_MARKETING_LIST` |
| Membro da lista de marketing B2B | `b2b_marketing_list_member` | `B2B_MARKETING_LIST_MEMBER` |
| Relação pessoal da conta B2B | `b2b_account_person_relation` | `B2B_ACCOUNT_PERSON` |

{style="table-layout:auto"}

## Esquemas B2B

A Experience Platform utiliza esquemas para descrever a estrutura dos dados de forma consistente e reutilizável. Ao definir os dados de forma consistente em todos os sistemas, fica mais fácil manter o significado e, portanto, obter valor dos dados.

Antes que os dados possam ser assimilados na Platform, um esquema deve ser composto para descrever a estrutura dos dados e fornecer restrições ao tipo de dados que podem estar contidos em cada campo. Os esquemas consistem em uma classe base e zero ou mais grupos de campos de esquema.

Para obter mais informações sobre o modelo de composição do schema, incluindo princípios de design e práticas recomendadas, consulte o [noções básicas da composição do esquema](../../../../xdm/schema/composition.md).

A tabela a seguir contém informações sobre a configuração subjacente de esquemas B2B.

>[!NOTE]
>
>Role a tela para a esquerda/direita para visualizar o conteúdo completo da tabela.

| Nome do esquema | Classe base | Grupos de campos | [!DNL Profile] no esquema | Identidade principal | Namespace de identidade primário | Identidade secundária | Namespace de identidade secundário | Relação | Notas |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Conta B2B | [Conta de negócios XDM](../../../../xdm/classes/b2b/business-account.md) | Detalhes da conta de negócios XDM | Ativado | `accountKey.sourceKey` na classe base | Conta B2B | `extSourceSystemAudit.externalKey.sourceKey` na classe base | Conta B2B | <ul><li>`accountParentKey.sourceKey` no grupo de campos Detalhes da conta de negócios XDM</li><li>Propriedade de destino: `/accountKey/sourceKey`</li><li>Tipo: um para um</li><li>Esquema de referência: Conta B2B</li><li>Namespace: conta B2B</li></ul> |
| Pessoa B2B | [Perfil individual XDM](../../../../xdm/classes/individual-profile.md) | <ul><li>Detalhes de pessoa de negócios XDM</li><li>Componentes de pessoa de negócios XDM</li><li>IdentityMap</li><li>Detalhes sobre consentimento e preferência</li></ul> | Ativado | `b2b.personKey.sourceKey` no Grupo de campos Detalhes da pessoa de negócios XDM | Pessoa B2B | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` do grupo de campos Detalhes da pessoa de negócios XDM</li><li>`workEmail.address` do grupo de campos Detalhes da pessoa de negócios XDM</ol></li> | <ol><li>Pessoa B2B</li><li>Email</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` do grupo de campos Componentes de pessoa de negócios XDM</li><li>Tipo: De muitos para um</li><li>Esquema de referência: conta B2B</li><li>Namespace: conta B2B</li><li>Propriedade de destino: accountKey.sourceKey</li><li>Nome do relacionamento do esquema atual: Conta</li><li>Nome do relacionamento do esquema de referência: Pessoas</li></ul> |
| Oportunidade B2B | [Oportunidade de negócios XDM](../../../../xdm/classes/b2b/business-opportunity.md) | Detalhes de oportunidades de negócios XDM | Ativado | `opportunityKey.sourceKey` na classe base | Oportunidade B2B | `extSourceSystemAudit.externalKey.sourceKey` na classe base | Oportunidade B2B | <ul><li>`accountKey.sourceKey` na classe base</li><li>Tipo: De muitos para um</li><li>Esquema de referência: conta B2B</li><li>Namespace: conta B2B</li><li>Propriedade de destino: `accountKey.sourceKey`</li><li>Nome do relacionamento do esquema atual: Conta</li><li>Nome do relacionamento do esquema de referência: Oportunidades</li></ul> |
| Relação pessoal da oportunidade B2B | [Relação pessoal de oportunidade de negócios XDM](../../../../xdm/classes/b2b/business-opportunity-person-relation.md) | None | Ativado | `opportunityPersonKey.sourceKey` na classe base | Relação pessoal da oportunidade B2B | `extSourceSystemAudit.externalKey.sourceKey` na classe base | Relação pessoal da oportunidade B2B | **Primeiro relacionamento**<ul><li>`personKey.sourceKey` na classe base</li><li>Tipo: De muitos para um</li><li>Esquema de referência: pessoa B2B</li><li>Namespace: pessoa B2B</li><li>Propriedade de destino: b2b.personKey.sourceKey</li><li>Nome do relacionamento do esquema atual: Pessoa</li><li>Nome do relacionamento do esquema de referência: Oportunidades</li></ul>**Segundo relacionamento**<ul><li>`opportunityKey.sourceKey` na classe base</li><li>Tipo: De muitos para um</li><li>Esquema de referência: Oportunidade B2B </li><li>Namespace: oportunidade B2B </li><li>Propriedade de destino: `opportunityKey.sourceKey`</li><li>Nome do relacionamento do esquema atual: Oportunidade</li><li>Nome do relacionamento do esquema de referência: Pessoas</li></ul> |
| Campanha B2B | [Campanha de negócios XDM](../../../../xdm/classes/b2b/business-campaign.md) | Detalhes da campanha de negócios XDM | Ativado | `campaignKey.sourceKey` na classe base | Campanha B2B | `extSourceSystemAudit.externalKey.sourceKey` na classe base | Campanha B2B |
| Membro da campanha B2B | [Membros da campanha de negócios XDM](../../../../xdm/classes/b2b/business-campaign-members.md) | Detalhes do membro da campanha de negócios XDM | Ativado | `ccampaignMemberKey.sourceKey` na classe base | Membro da campanha B2B | `extSourceSystemAudit.externalKey.sourceKey` na classe base | Membro da campanha B2B | **Primeiro relacionamento**<ul><li>`personKey.sourceKey` na classe base</li><li>Tipo: De muitos para um</li><li>Esquema de referência: pessoa B2B</li><li>Namespace: pessoa B2B</li><li>Propriedade de destino: `b2b.personKey.sourceKey`</li><li>Nome do relacionamento do esquema atual: Pessoa</li><li>Nome do relacionamento do esquema de referência: Campanhas</li></ul>**Segundo relacionamento**<ul><li>`campaignKey.sourceKey` na classe base</li><li>Tipo: De muitos para um</li><li>Esquema de referência: campanha B2B</li><li>Namespace: campanha B2B</li><li>Propriedade de destino: `campaignKey.sourceKey`</li><li>Nome do relacionamento do esquema atual: Campanha</li><li>Nome do relacionamento do esquema de referência: Pessoas</li></ul> |
| Lista de marketing B2B | [Lista de marketing de negócios XDM](../../../../xdm/classes/b2b/business-marketing-list.md) | None | Ativado | `marketingListKey.sourceKey` na classe base | Lista de marketing B2B | None | None | None | A lista estática não é sincronizada a partir de [!DNL Salesforce] e, portanto, não tem uma identidade secundária. |
| Membro da lista de marketing B2B | [Membros da lista de marketing de negócios XDM](../../../../xdm/classes/b2b/business-marketing-list-members.md) | None | Ativado | `marketingListMemberKey.sourceKey` na classe base | Membro da lista de marketing B2B | None | None | **Primeiro relacionamento**<ul><li>`PersonKey.sourceKey` na classe base</li><li>Tipo: De muitos para um</li><li>Esquema de referência: pessoa B2B</li><li>Namespace: pessoa B2B</li><li>Propriedade de destino: `b2b.personKey.sourceKey`</li><li>Nome do relacionamento do esquema atual: Pessoa</li><li>Nome do relacionamento do esquema de referência: Listas de marketing</li></ul>**Segundo relacionamento**<ul><li>`marketingListKey.sourceKey` na classe base</li><li>Tipo: De muitos para um</li><li>Esquema de referência: Lista de marketing B2B</li><li>Namespace: lista de marketing B2B</li><li>Propriedade de destino: `marketingListKey.sourceKey`</li><li>Nome do relacionamento do esquema atual: Lista de marketing</li><li>Nome do relacionamento do esquema de referência: Pessoas</li></ul> | O membro da lista estática não é sincronizado a partir de [!DNL Salesforce] e, portanto, não tem uma identidade secundária. |
| Atividade B2B | [XDM ExperienceEvent](../../../../xdm/classes/experienceevent.md) | <ul><li>Visitar página da Web</li><li>Novo lead</li><li>Converter lead</li><li>Adicionar à lista</li><li>Remover da lista</li><li>Adicionar à oportunidade</li><li>Remover da oportunidade</li><li>Formulário preenchido</li><li>Cliques de link</li><li>Email entregue</li><li>Email aberto</li><li>Email clicado</li><li>Email rejeitado</li><li>Email rejeitado temporariamente</li><li>Email cancelado</li><li>Pontuação alterada</li><li>Oportunidade atualizada</li><li>Status na progressão da campanha alterado</li><li>Identificador de pessoa</li><li>URL da Web do Marketo</li><li>Momento interessante</li><li>Chamar Webhook</li><li>Alterar cadência da campanha</li><li>Estágio da receita alterado</li><li>Mesclar leads</li><li>Email enviado</li><li>Alterar fluxo da campanha</li><li>Adicionar à campanha</li></ul> | Ativado | `personKey.sourceKey` do grupo de campos Identificador de pessoa | Pessoa B2B | None | None | **Primeiro relacionamento**<ul><li>`listOperations.listKey.sourceKey` campo</li><li>Tipo: um para um</li><li>Esquema de referência: Lista de marketing B2B</li><li>Namespace: lista de marketing B2B</li></ul>**Segundo relacionamento**<ul><li>`opportunityEvent.opportunityKey.sourceKey` campo</li><li>Tipo: um para um</li><li>Esquema de referência: Oportunidade B2B</li><li>Namespace: oportunidade B2B</li></ul>**Terceiro relacionamento**<ul><li>`leadOperation.campaignProgression.campaignKey.sourceKey` campo</li><li>Tipo: um para um</li><li>Esquema de referência: campanha B2B</li><li>Namespace: campanha B2B</li></ul> | `ExperienceEvent` é diferente de entidades. A identidade do evento de experiência é a pessoa que realizou a atividade. |
| Relação pessoal da conta B2B | [Relação pessoal da conta de negócios XDM](../../../../xdm/classes/b2b/business-account-person-relation.md) | Mapa de identidade | Ativado | `accountPersonKey.sourceKey` na classe base | Relação pessoal da conta B2B | None | None | **Primeiro relacionamento**<ul><li>`personKey.sourceKey` na classe base</li><li>Tipo: De muitos para um</li><li>Esquema de referência: pessoa B2B</li><li>Namespace: pessoa B2B</li><li>Propriedade de destino: `b2b.personKey.SourceKey`</li><li>Nome do relacionamento do esquema atual: People</li><li>Nome do relacionamento do esquema de referência: Conta</li></ul>**Segundo relacionamento**<ul><li>`accountKey.sourceKey` na classe base</li><li>Tipo: De muitos para um</li><li>Esquema de referência: conta B2B</li><li>Namespace: conta B2B</li><li>Propriedade de destino: `accountKey.sourceKey`</li><li>Nome do relacionamento do esquema atual: Conta</li><li>Nome do relacionamento do esquema de referência: Pessoas</li></ul> |

{style="table-layout:auto"}

## Próximas etapas

Para saber como conectar seu [!DNL Marketo] para a Platform, consulte o tutorial em [criação de um conector de origem do Marketo na interface](../../../tutorials/ui/create/adobe-applications/marketo.md).
