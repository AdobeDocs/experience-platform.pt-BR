---
keywords: Experience Platform, home, tópicos populares, conector de origem do Marketo, namespaces, esquemas
solution: Experience Platform
title: 'Namespaces do Marketo '
topic: visão geral
description: Este documento fornece uma visão geral de namespaces personalizados necessários ao criar um conector de origem de Marketo Engage.
translation-type: tm+mt
source-git-commit: 2563b413ec35cb4c5f05a54bce6f7271917e51f3
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 6%

---


# (Beta) [!DNL Marketo Engage] namespaces e schemas

>[!IMPORTANT]
>
>A fonte [!DNL Marketo Engage] está atualmente em beta. O recurso e a documentação estão sujeitos a alterações.

Este documento fornece informações sobre a configuração subjacente para os namespaces e esquemas B2B usados com [!DNL Marketo Engage] (a seguir denominado &quot;[!DNL Marketo]&quot;). Este documento também fornece detalhes sobre a configuração do utilitário de automação do Postman necessário para gerar [!DNL Marketo] namespaces e esquemas B2B.

## Pré-requisitos

Antes de gerar seus namespaces e esquemas B2B, primeiro você deve configurar o console do desenvolvedor do Platform e o ambiente [!DNL Postman]. Para obter mais informações, consulte o tutorial em [configurar o console do desenvolvedor e [!DNL Postman]](../../../../landing/postman.md).

Com um console de desenvolvedor da Platform e uma configuração [!DNL Postman], aplique as seguintes variáveis ao seu ambiente [!DNL Marketo]:

| Variável de ambiente | Exemplo de valor | Notas |
| --- | --- | --- |
| `PRIVATE_KEY` | `{PRIVATE_KEY}` |
| `SANDBOX_NAME` | `prod` |
| `TENANT_ID` | `b2bcdpproductiontest` |
| `munchkinId` | `123-ABC-456 ` | Consulte o tutorial em [autenticar sua [!DNL Marketo] instância](./marketo-auth.md) para obter mais informações. |
| `sfdc_org_id` | `00D4W000000FgYJUA0` | Consulte o [[!DNL Salesforce] guia](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) a seguir para obter mais informações sobre como adquirir a ID da organização. |
| `msd_org_id` | `f6438fab-67e8-4814-a6b5-8c8dcdf7a98f` | Consulte o [[!DNL Microsoft Dynamics] guia](https://docs.microsoft.com/en-us/power-platform/admin/determine-org-id-name) a seguir para obter mais informações sobre como adquirir a ID da organização. |
| `has_abm` | `false` | Esse valor é definido como `true` se você estiver inscrito no Marketing baseado em conta. |
| `has_msi` | `false` | Esse valor é definido como `true` se você estiver inscrito em [!DNL Marketo Sales Insight]. |

{style=&quot;table-layout:auto&quot;}

## [!DNL Marketo] namespaces

Os namespaces de identidade são um componente de [[!DNL Identity Service]](../../../../identity-service/home.md) que serve como indicadores do contexto ao qual uma identidade está relacionada.

Uma identidade totalmente qualificada inclui um valor de ID e um namespace. Um novo namespace personalizado é necessário para cada nova instância [!DNL Marketo] e combinação de conjunto de dados. Por exemplo, um conector de origem [!DNL Marketo] que assimila o conjunto de dados `programs` requer seu próprio namespace personalizado e outro conector de origem do Marketo que assimila o mesmo conjunto de dados também exige seu próprio namespace personalizado. Consulte a [visão geral dos namespaces](../../../../identity-service/namespaces.md) para obter mais informações.

O namespace [!DNL Marketo] é usado na identidade primária da entidade.

A tabela a seguir contém informações sobre a configuração subjacente para [!DNL Marketo] namespaces.

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

| Nome de exibição | Símbolo de identidade | Tipo de identidade | Tipo de emissor | Tipo de entidade emissor | [!DNL Salesforce] exemplo de ID da organização da assinatura |
| --- | --- | --- | --- | --- | --- |
| `salesforce_person_{SALESFORCE_ORGANIZATION_ID}` | gerado automaticamente | `CROSS_DEVICE` | [!DNL Salesforce] | `person` | `00DA0000000Hz79` |
| `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | gerado automaticamente | `B2B_ACCOUNT` | [!DNL Salesforce] | `account` | `00DA0000000Hz79` |
| `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | gerado automaticamente | `B2B_OPPORTUNITY` | [!DNL Salesforce] | `opportunity` | `00DA0000000Hz79` |
| `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | gerado automaticamente | `B2B_OPPORTUNITY_PERSON` | [!DNL Salesforce] | `opportunity contact role` | `00DA0000000Hz79` |
| `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` | gerado automaticamente | `B2B_CAMPAIGN` | [!DNL Salesforce] | `campaign` | `00DA0000000Hz79` |
| `salesforce_campaign_member_{SALESFORCE_ORGANIZATION_ID}` | gerado automaticamente | `B2B_CAMPAIGN_MEMBER` | [!DNL Salesforce] | `campaign member` | `00DA0000000Hz79` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Microsoft Dynamics] namespaces

Se você estiver inscrito na integração [!DNL Dynamics], o namespace [!DNL Dynamics] será usado como identidade secundária da entidade.

A tabela a seguir contém informações sobre a configuração subjacente para [!DNL Dynamics] namespaces.

| Nome de exibição | Símbolo de identidade | Tipo de identidade | Tipo de emissor | Tipo de entidade emissor | [!DNL Salesforce] exemplo de ID da organização da assinatura |
| --- | --- | --- | --- | --- | --- |
| `microsoft_person_{DYNAMICS_ID}` | gerado automaticamente | `CROSS_DEVICE` | [!DNL Microsoft] | `person` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_account_{DYNAMICS_ID}` | gerado automaticamente | `B2B_ACCOUNT` | [!DNL Microsoft] | `account` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_{DYNAMICS_ID}` | gerado automaticamente | `B2B_OPPORTUNITY` | [!DNL Microsoft] | `opportunity` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_contact_connection_{DYNAMICS_ID}` | gerado automaticamente | `B2B_OPPORTUNITY_PERSON` | [!DNL Microsoft] | `opportunity relationship` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_{DYNAMICS_ID}` | gerado automaticamente | `B2B_CAMPAIGN` | [!DNL Microsoft] | `campaign` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_member_{DYNAMICS_ID}` | gerado automaticamente | `B2B_CAMPAIGN_MEMBER` | [!DNL Microsoft] | `campaign member` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |

## [!DNL Marketo] esquemas

A Experience Platform utiliza esquemas para descrever a estrutura dos dados de forma consistente e reutilizável. Ao definir os dados de forma consistente em todos os sistemas, fica mais fácil manter o significado e, portanto, obter valor dos dados.

Para que os dados possam ser assimilados na Platform, um schema deve ser composto para descrever a estrutura dos dados e fornecer restrições ao tipo de dados que pode ser contido em cada campo. Os esquemas consistem em uma classe base e zero ou mais mixins.

Para obter mais informações sobre o modelo de composição do schema, incluindo princípios de design e práticas recomendadas, consulte as [noções básicas da composição do schema](../../../../xdm/schema/composition.md).

A tabela a seguir contém informações sobre a configuração subjacente de [!DNL Marketo] schemas.

>[!NOTE]
>
>Role a tela para a esquerda/direita para exibir o conteúdo completo da tabela.

| Nome do esquema | Classe base | Misturas | Identidade primária | Namespace da identidade primária | Identidade secundária | Namespace de identidade secundária | Relação | Notas |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| [!DNL Marketo] Empresa {MUNCHKIN_ID} | Conta Comercial XDM | Detalhes da conta comercial XDM | `accountID` na classe base | `marketo_company_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` na classe base | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` na mesclagem Detalhes da conta comercial XDM</li><li>Tipo: um para um</li><li>Esquema de referência: Empresa Marketo {MUNCHKIN_ID}</li><li>Namespace: `marketo_company_{MUNCHKIN_ID}`</li></ul> |
| [!DNL Marketo] Pessoa {MUNCHKIN_ID} | Perfil individual XDM | <ul><li>Detalhes da Pessoa Comercial XDM</li><li>Componentes de Pessoa Comercial XDM</li></ul> | `personID` na classe base | `marketo_person_{MUNCHKIN_ID}` | <ol><li>`extSourceSystemAudit.externalID` do mixin de Detalhes da Pessoa Comercial XDM</li><li>`workEmail.address` do mixin de Detalhes da Pessoa Comercial XDM</li><li>`identityMap` do mixin do Mapa de identidade</ol></li> | <ol><li>`salesforce_person_{SALESFORCE_ORGANIZATION_ID}`</li><li>Email</li><li>ECID</li></ol> | <ul><li>`personComponents.sourceAccountID` da combinação de Componentes de Pessoa Comercial XDM</li><li>Tipo: Muitos para um</li><li>Esquema de referência: Empresa Marketo {MUNCHKIN_ID}</li><li>Namespace: `marketo_company_{MUNCHKIN_ID}`</li><li>Propriedade de destino: `accountID`</li><li>Nome do relacionamento do schema atual: Conta</li><li>Nome do relacionamento do schema de referência: Pessoas</li></ul> |
| [!DNL Marketo] Oportunidade {MUNCHKIN_ID} | Oportunidade de negócios XDM | Detalhes da oportunidade de negócios XDM | `opportunityID` na classe base | `marketo_opportunity_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` na classe base | `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountID` na classe base</li><li>Tipo: Muitos para um</li><li>Esquema de referência: Empresa Marketo {MUNCHKIN_ID}</li><li>Namespace: `marketo_company_{MUNCHKIN_ID}`</li><li>Propriedade de destino: `accountID`</li><li>Nome do relacionamento do schema atual: Conta</li><li>Nome do relacionamento do schema de referência: Oportunidades</li></ul> |
| [!DNL Marketo] Função de Contato da Oportunidade {MUNCHKIN_ID} | Relação de Pessoa da Oportunidade de Negócios XDM | None | `opportunityPersonID` na classe base | `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` na classe base | `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | Primeira relação<ul><li>`personID` na classe base</li><li>Tipo: Muitos para um</li><li>Esquema de referência: Pessoa do Marketo {MUNCHKIN_ID}</li><li>Namespace: `marketo_person_{MUNCHKIN_ID}`</li><li>Propriedade de destino: `personID`</li><li>Nome do relacionamento do schema atual: Pessoa</li><li>Nome do relacionamento do schema de referência: Oportunidades</li></ul>Segunda relação<ul><li>`opportunityID` na classe base</li><li>Tipo: Muitos para um</li><li>Esquema de referência: Oportunidade de Marketo {MUNCHKIN_ID}</li><li>Namespace: `marketo_opportunity_{MUNCHKIN_ID}`</li><li>Propriedade de destino: `opportunityID`</li><li>Nome do relacionamento do schema atual: Oportunidade</li><li>Nome do relacionamento do schema de referência: Pessoas</li></ul> |
| [!DNL Marketo] Programa {MUNCHKIN_ID} | Campanha comercial XDM | Detalhes da campanha comercial XDM | `campaignID` na classe base | `marketo_program_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` na classe base | `salesforce_campaign_SALESFORCE_ORGANIZATION_ID}` |
| [!DNL Marketo] Membro do Programa {MUNCHKIN_ID} | Membro da Campanha Comercial XDM | Detalhes do Membro da Campanha Empresarial XDM | `campaignMemberID` na classe base | `marketo_program_member_{MUNCHKIN_ID}` | Nenhum | Nenhum | Primeira relação<ul><li>`personID` na classe base</li><li>Tipo: Muitos para um</li><li>Esquema de referência: Pessoa do Marketo {MUNCHKIN_ID}</li><li>Namespace: `marketo_person_{MUNCHKIN_ID}`</li><li>Propriedade de destino: `personID`</li><li>Nome do relacionamento do schema atual: Pessoa</li><li>Nome do relacionamento do schema de referência: Programas</li></ul>Segunda relação<ul><li>`campaignID` na classe base</li><li>Tipo: Muitos para um</li><li>Esquema de referência: Programa Marketo {MUNCHKIN_ID}</li><li>Namespace: `marketo_program_{MUNCHKIN_ID}`</li><li>Propriedade de destino: campaignID</li><li>Nome do relacionamento do schema atual: Programa</li><li>Nome do relacionamento do schema de referência: Pessoas</li></ul> |
| [!DNL Marketo] Lista Estática {MUNCHKIN_ID} | Lista de marketing comercial XDM | Nenhum | `marketingListID` na classe base | `marketo_static_list_{MUNCHKIN_ID}` | Nenhum | Nenhum | Nenhum | A Lista Estática não é sincronizada de [!DNL Salesforce] e, portanto, não tem uma identidade secundária |
| [!DNL Marketo] Membro da Lista Estática {MUNCHKIN_ID} | Membros da Lista de Marketing Comercial XDM | Nenhum | `marketingListMemberID` na classe base | `marketo_static_list_member_{MUNCHKIN_ID}` | Nenhum | Nenhum | Primeira relação<ul><li>`personID` na classe base</li><li>Tipo: Muitos para um</li><li>Esquema de referência: Pessoa do Marketo {MUNCHKIN_ID}</li><li>Namespace: `marketo_person_{MUNCHKIN_ID}`</li><li>Propriedade de destino: `personID`</li><li>Nome do relacionamento do schema atual: Pessoa</li><li>Nome do relacionamento do schema de referência: Listas</li></ul>Segunda relação<ul><li>`marketingListID` na classe base</li><li>Tipo: Muitos para um</li><li>Esquema de referência: Lista Estática do Marketo {MUNCHKIN_ID}</li><li>Namespace: `marketo_static_list_{MUNCHKIN_ID}`</li><li>Propriedade de destino: `marketingListID`</li><li>Nome do relacionamento do schema atual: Lista</li><li>Nome do relacionamento do schema de referência: Pessoas</li></ul> |
| [!DNL Marketo] Conta Nomeada {MUNCHKIN_ID} | Conta Comercial XDM | Detalhes da conta comercial XDM | `accountID` na classe base | `marketo_named_account_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` na classe base | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` na mesclagem Detalhes da conta comercial XDM</li><li>Tipo: um para um</li><li>Esquema de referência: Conta com Nome Marketo {MUNCHKIN_ID}</li><li>Namespace: `marketo_named_account_{MUNCHKIN_ID}` |
| [!DNL Marketo] Atividade {ID MUNCHKIN} | Evento de experiência XDM | <ul><li>Visitar WebPage</li><li>Novo cliente potencial</li><li>Converter lead</li><li>Adicionar à lista</li><li>Remover da lista</li><li>Adicionar à Oportunidade</li><li>Remover da Oportunidade</li><li>Formulário preenchido</li><li>Cliques em links</li><li>Email Entregue</li><li>Email aberto</li><li>Email clicado</li><li>Rejeição de email</li><li>Enviar email com rejeição suave</li><li>Email Inscrito</li><li>Pontuação alterada</li><li>Oportunidade Atualizada</li><li>Status in Campaign Progression Changed (Status da Progressão da Campanha Alterado)</li><li>Identificador de pessoa</li><li>URL da Web do Marketo | `personID` mixin do Identificador de Pessoa | marketo_person_{MUNCHKIN_ID} | Nenhum | Nenhum | Primeira relação<ul><li>`listOperations.listID` campo</li><li>Tipo: um para um</li><li>Esquema de referência: Lista Estática do Marketo {MUNCHKIN_ID}</li><li>Namespace: `marketo_static_list_{MUNCHKIN_ID}`</li></ul>Segunda relação<ul><li>`opportunityEvent.opportunityID` campo</li><li>Tipo: um para um</li><li>Esquema de referência: Oportunidade de Marketo {MUNCHKIN_ID}</li><li>Namespace: `marketo_opportunity_{MUNCHKIN_ID}`</li></ul>Terceiro relacionamento<ul><li>`leadOperation.campaignProgression.campaignID` campo</li><li>Tipo: um para um</li><li>Esquema de referência: Programa Marketo {MUNCHKIN_ID}</li><li>Namespace: `marketo_program_{MUNCHKIN_ID}`</li></ul> |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Todos os esquemas estão habilitados para [!DNL Real-time Customer Profile]

## Próximas etapas

Para saber como conectar seus dados [!DNL Marketo] à Platform, consulte o tutorial em [criar um conector de origem Marketo na interface do usuário](../../../tutorials/ui/create/adobe-applications/marketo.md).