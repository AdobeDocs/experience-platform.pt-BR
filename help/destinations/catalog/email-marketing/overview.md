---
keywords: email; Email; email; destinos de email
title: Visão geral dos destinos de marketing por email
type: Tutorial
description: Os provedores de serviços de email (ESPs) permitem gerenciar suas atividades de marketing por email, como para enviar campanhas de email promocionais. Saiba quais ESPs são compatíveis como destinos de Experience Platform.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: d6ea94b275ab0ed7c0638200188fe7ada7bacf5c
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 4%

---

# Visão geral dos destinos de marketing por email {#email-marketing-destinations}

## Visão geral {#overview}

Os provedores de serviços de email (ESPs) permitem gerenciar suas atividades de marketing por email, como enviar campanhas de email promocionais. O Adobe Experience Platform integra-se com ESPs permitindo ativar segmentos para destinos de marketing por email.

## Destinos de marketing por email suportados {#supported-destinations}

O Adobe Experience Platform oferece suporte para os seguintes destinos de marketing por email:

* [Adobe Campaign](adobe-campaign.md)
* [Adobe Campaign Managed Cloud Services](adobe-campaign-managed-services.md)
* [(API) Oracle Eloqua](oracle-eloqua-api.md)
* [(API) Marketing Cloud do Salesforce](salesforce-marketing-cloud-exact-target.md)
* [(Arquivos) Oracle Eloqua](oracle-eloqua.md)
* [(Arquivos) Marketing Cloud Salesforce](salesforce-marketing-cloud.md)
* [Oracle Responsys](oracle-responsys.md)
* [SendGrid](sendgrid.md)

## Conectar-se a um novo destino de marketing por email {#connect-destination}

Para enviar segmentos para destinos de marketing por email para suas campanhas, a Platform deve primeiro se conectar ao destino. Consulte a [tutorial de criação de destino](../../ui/connect-destination.md) para obter informações detalhadas sobre como configurar um novo destino.

## Práticas recomendadas ao ativar públicos-alvo para destinos de marketing por email {#best-practices}

### Seleção de identidade {#identity}

O Adobe recomenda selecionar um identificador exclusivo de [schema de união](../../../profile/home.md#profile-fragments-and-union-schemas). Este é o campo do qual suas identidades de usuário são destacadas. Geralmente, esse campo é o endereço de email, mas também pode ser uma ID de programa de fidelidade ou um número de telefone. Consulte a tabela abaixo para obter os identificadores exclusivos mais comuns e seu campo XDM no schema.

| Identificador exclusivo | Campo XDM no esquema unificado |
|----------------- | ---------------------------|
| Endereço de email | `personalEmail.address` |
| Telefone | `mobilePhone.number` |
| ID do programa de fidelidade | `Customer-defined XDM field` |

{style="table-layout:auto"}

### Outros atributos de destino {#other-destination-attributes}

No seletor de campo Schema , escolha outros campos que deseja exportar para o destino do email. Algumas opções recomendadas são:

| Esquema | Campo XDM |
|------ | ---------|
| Primeiro nome | `person.name.firstName` |
| Sobrenome | `person.name.lastName` |
| Telefone | `mobilePhone.number` |
| Cidade do Endereço | `homeAddress.city` |
| Estado do Endereço | `homeAddress.stateProvince` |
| Código postal do endereço | `homeAddress.postalCode` |
| Aniversário | `person.birthDayAndMonth` |
| Segmento de afiliação | `segmentMembership.status` |

{style="table-layout:auto"}

## Ativar segmentos para destinos de marketing por email {#activate}

Alguns destinos de marketing por email no catálogo exportam perfis de maneira contínua por meio de uma integração da API com o destino.

Outros destinos exportam arquivos para um local de armazenamento em nuvem. Após a conclusão da exportação, é necessário importar os dados do local de armazenamento na nuvem para o destino de marketing por email.

Siga os links no [destinos de marketing por email aceitos](#supported-destinations) para saber como ativar segmentos em cada destino de marketing por email.

## Recursos adicionais {#additional-resources}

* [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md)
* [Criar destinos de marketing por email e ativar dados usando a API do Serviço de fluxo](../../api/connect-activate-batch-destinations.md)
