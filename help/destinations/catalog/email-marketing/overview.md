---
keywords: email;Email;e-mail;destinos de e-mail;email;Email;e-mail;email destinations
title: Visão geral dos destinos de marketing por email
type: Tutorial
description: Os Provedores de serviços de email (ESPs) permitem gerenciar atividades de marketing por email, como o envio de campanhas de email promocionais.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: ccbc633bfce8f4f66577b50064c28cfc26cb6dca
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 4%

---

# Visão geral dos destinos de marketing por email {#email-marketing-destinations}

## Visão geral {#overview}

Os Provedores de serviços de email (ESPs) permitem gerenciar atividades de marketing por email, como o envio de campanhas de email promocionais. O Adobe Experience Platform integra-se aos ESPs permitindo ativar segmentos para destinos de marketing por email.

A Platform exporta seus segmentos como `.csv` e entrega-os no local de sua preferência. Agendar sua importação de dados na plataforma de marketing por email a partir do local de armazenamento habilitado em [!DNL Platform]. O processo para importar dados varia para cada parceiro. Leia os artigos de destinos individuais para obter mais informações.

## Destinos de marketing por email compatíveis {#supported-destinations}

O Adobe Experience Platform é compatível com os seguintes destinos de marketing por email:

* [Adobe Campaign](adobe-campaign.md)
* [Oracle Eloqua](oracle-eloqua.md)
* [Oracle Responsys](oracle-responsys.md)
* [Marketing Cloud do Salesforce](salesforce-marketing-cloud.md)
* [SendGrid](sendgrid.md)

## Conectar-se a um novo destino de marketing por email {#connect-destination}

Para enviar segmentos para destinos de marketing por email para suas campanhas, a Platform deve primeiro se conectar ao destino. Consulte a [tutorial de criação do destino](../../ui/connect-destination.md) para obter informações detalhadas sobre como configurar um novo destino.

## Práticas recomendadas ao ativar públicos para destinos de marketing por email {#best-practices}

### Seleção de identidade {#identity}

O Adobe recomenda que você selecione um identificador exclusivo de sua [esquema de união](../../../profile/home.md#profile-fragments-and-union-schemas). Este é o campo do qual suas identidades de usuário são destacadas. Normalmente, esse campo é o endereço de email, mas também pode ser uma ID de programa de fidelidade ou um número de telefone. Consulte a tabela abaixo para obter os identificadores exclusivos mais comuns e seu campo XDM no esquema.

| Identificador exclusivo | Campo XDM no esquema unificado |
|----------------- | ---------------------------|
| Endereço de email | `personalEmail.address` |
| Telefone | `mobilePhone.number` |
| ID do programa de fidelidade | `Customer-defined XDM field` |

### Outros atributos de destino

No seletor de campo Esquema, escolha quais outros campos você deseja exportar para o destino de email. Algumas opções recomendadas são:

| Esquema | Campo XDM |
|------ | ---------|
| Primeiro nome | `person.name.firstName` |
| Sobrenome | `person.name.lastName` |
| Telefone | `mobilePhone.number` |
| Cidade do Endereço | `homeAddress.city` |
| Estado do endereço | `homeAddress.stateProvince` |
| CEP do endereço | `homeAddress.postalCode` |
| Aniversário | `person.birthDayAndMonth` |
| Segmento de afiliação | `segmentMembership.status` |

## Importar dados do local de armazenamento para o destino {#import-data-into-destination}

Leia os artigos individuais de destino de marketing por email para saber como importar dados do local de armazenamento para destinos:

* [Adobe Campaign](adobe-campaign.md)
* [Oracle Eloqua](oracle-eloqua.md)
* [Oracle Responsys](oracle-responsys.md)
* [Marketing Cloud do Salesforce](salesforce-marketing-cloud.md)

## Ativar segmentos para destinos de marketing por email {#activate}

Para obter instruções sobre como ativar segmentos para destinos de marketing por email, consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md).

## Recursos adicionais

* [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md)
* [Criar destinos de marketing por email e ativar dados usando a API do Serviço de fluxo](../../api/connect-activate-batch-destinations.md)
