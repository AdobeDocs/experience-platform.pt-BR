---
keywords: email;Email;e-mail;destinos de e-mail;email;Email;e-mail;email destinations
title: Visão geral dos destinos de marketing por email
type: Tutorial
description: Os Provedores de serviços de email (ESPs) permitem gerenciar atividades de marketing por email, como o envio de campanhas de email promocionais. Saiba quais ESPs são compatíveis como destinos do Experience Platform.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 5%

---

# Visão geral dos destinos de marketing por email {#email-marketing-destinations}

## Visão geral {#overview}

Os Provedores de serviços de email (ESPs) permitem gerenciar atividades de marketing por email, como o envio de campanhas de email promocionais. O Adobe Experience Platform integra-se aos ESPs permitindo ativar públicos-alvo para destinos de marketing por email.

## Destinos de marketing por email compatíveis {#supported-destinations}

O Adobe Experience Platform é compatível com os seguintes destinos de marketing por email:

* [Adobe Campaign](adobe-campaign.md)
* [Adobe Campaign Managed Cloud Services](adobe-campaign-managed-services.md)
* [Categorias de interesse do Mailchimp](mailchimp-interest-categories.md)
* [Tags do Mailchimp](mailchimp-tags.md)
* [(API) Oracle Eloqua](oracle-eloqua-api.md)
* [(API) [!DNL Salesforce Marketing Cloud]](salesforce-marketing-cloud-exact-target.md)
* [(Arquivos) Oracle Eloqua](oracle-eloqua.md)
* [(Arquivos) [!DNL Salesforce Marketing Cloud]](salesforce-marketing-cloud.md)
* [[!DNL Salesforce Marketing Cloud Account Engagement]](salesforce-marketing-cloud-account-engagement.md)
* [Oracle Responsys](oracle-responsys.md)
* [SendGrid](sendgrid.md)

## Conectar-se a um novo destino de marketing por email {#connect-destination}

Para enviar públicos-alvo para destinos de marketing por email de suas campanhas, o Experience Platform deve primeiro se conectar ao destino. Consulte o [tutorial de criação de destino](../../ui/connect-destination.md) para obter informações detalhadas sobre a configuração de um novo destino.

## Práticas recomendadas ao ativar públicos para destinos de marketing por email {#best-practices}

### Seleção de identidade {#identity}

A Adobe recomenda selecionar um identificador exclusivo do seu [esquema de união](../../../profile/home.md#profile-fragments-and-union-schemas). Este é o campo do qual suas identidades de usuário são destacadas. Normalmente, esse campo é o endereço de email, mas também pode ser uma ID de programa de fidelidade ou um número de telefone. Consulte a tabela abaixo para obter os identificadores exclusivos mais comuns e seu campo XDM no esquema.

| Identificador exclusivo | Campo XDM no esquema unificado |
|----------------- | ---------------------------|
| Endereço de e-mail | `personalEmail.address` |
| Telefone | `mobilePhone.number` |
| ID do programa de fidelidade | `Customer-defined XDM field` |

{style="table-layout:auto"}

### Outros atributos de destino {#other-destination-attributes}

No seletor de campo Esquema, escolha quais outros campos você deseja exportar para o destino de email. Algumas opções recomendadas são:

| Esquema | Campo XDM |
|------ | ---------|
| Nome | `person.name.firstName` |
| Sobrenome | `person.name.lastName` |
| Telefone | `mobilePhone.number` |
| Cidade do Endereço | `homeAddress.city` |
| Estado do endereço | `homeAddress.stateProvince` |
| CEP do endereço | `homeAddress.postalCode` |
| Aniversário | `person.birthDayAndMonth` |
| Associação de segmento | `segmentMembership.status` |

{style="table-layout:auto"}

## Ativar públicos para destinos de marketing por email {#activate}

Alguns destinos de marketing por email no catálogo exportam perfis de maneira contínua por meio de uma integração de API com o destino.

Outros destinos exportam arquivos para um local de armazenamento na nuvem. Após concluir a exportação, é necessário importar os dados do local de armazenamento na nuvem para o destino de marketing por email.

Siga os links na seção [destinos de marketing por email compatíveis](#supported-destinations) para saber como ativar públicos para cada destino de marketing por email.

## Recursos adicionais {#additional-resources}

* [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md)
* [Criar destinos de marketing por email e ativar dados usando a API do Serviço de fluxo](../../api/connect-activate-batch-destinations.md)
