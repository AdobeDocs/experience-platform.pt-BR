---
title: Destinos de marketing de email
seo-title: Destinos de marketing de email
description: Os provedores de serviços de e-mail (ESPs) permitem gerenciar suas atividades de marketing de e-mail, como para enviar campanhas promocionais por e-mail.
seo-description: Os provedores de serviços de e-mail (ESPs) permitem gerenciar suas atividades de marketing de e-mail, como para enviar campanhas promocionais por e-mail.
translation-type: tm+mt
source-git-commit: 463212a8fabb9dd5962b4d3f523a6f2d88bb1d9d

---


# Destinos de marketing de email {#email-marketing-destinations}

Os provedores de serviços de email (ESPs) permitem gerenciar suas atividades de marketing de email, como o envio de campanhas promocionais por email. A Plataforma de dados do cliente em tempo real da Adobe integra-se aos ESPs, permitindo que você ative segmentos para destinos de marketing por email.

Para enviar segmentos para destinos de marketing de email de suas campanhas, o Adobe Real-time CDP deve primeiro se conectar ao destino.

A conexão com destinos de marketing de email é um processo de três etapas. Cada uma das etapas é descrita mais abaixo nesta página.

No fluxo de destino de conexão, descrito na seção abaixo, conecte-se ao Amazon S3 ou ao SFTP. A CDP em tempo real exporta seus segmentos como `.csv` ou `.txt` arquivos e os entrega para o local desejado. Agende sua importação de dados na plataforma de marketing por email a partir do local de armazenamento habilitado na CDP em tempo real. O processo de importação de dados varia para cada parceiro. Consulte os artigos de destinos individuais para obter mais informações.

## Etapa 1 - Conectar ao destino {#connect-destination}

1. Em **[!UICONTROL Connections > Destinations]**, selecione o destino de marketing de email ao qual você deseja se conectar e selecione **[!UICONTROL Connect destination]**.

   ![Conectar ao destino](/help/rtcdp/destinations/assets/connect-destination.png)

2. No assistente do Connect, selecione o local de armazenamento **[!UICONTROL Connection type]** para o qual você deseja acessar. Você pode selecionar entre **Amazon S3**, **SFTP com senha**, **SFTP com chave** SSH. Preencha as informações abaixo, dependendo do tipo de conexão, e selecione **[!UICONTROL Connect]**.

Para conexões **** S3, você deve fornecer a ID da chave de acesso e a chave de acesso secreta.

Para **SFTP com conexões de senha** , você deve fornecer Domínio, Porta, Nome de usuário e Senha.

Para **SFTP com conexões de chave** SSH, você deve fornecer Domínio, Porta, Nome de usuário e Chave SSH.

## Etapa 2 - Selecione os campos de esquema a serem usados como atributos de destino nos arquivos exportados {#destination-attributes}

Nesta etapa, você está selecionando quais campos exportar para destinos de marketing de email.

![Atributos de destino](/help/rtcdp/destinations/assets/destination-attributes.png)

### Identidade {#identity}

Recomendamos que você selecione um identificador exclusivo do seu esquema [de](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)união. Este é o campo do qual as identidades de seus usuários são destacadas. Normalmente, esse campo é o endereço de email, mas também pode ser uma ID de programa de fidelidade ou um número de telefone. Consulte a tabela abaixo para obter os identificadores exclusivos mais comuns e seus campos XDM no esquema unificado.

| Identificador exclusivo | Campo XDM no Esquema Unificado |
---------|----------
| Email Address | `personalEmail.address` |
| Telefone | `mobilePhone.number` |
| ID do programa de fidelidade | `Customer-defined XDM field` |

### Outros atributos de destino

No seletor de campo Esquema, escolha os outros campos que deseja exportar para o destino do email. Algumas opções recomendadas são:

| Esquema | Campo XDM |
---------|----------
| Nome | `person.name.firstName` |
| Sobrenome | `person.name.lastName` |
| Telefone | `mobilePhone.number` |
| Cidade do Endereço | `homeAddress.city` |
| Estado do endereço | `homeAddress.stateProvince` |
| Código postal do endereço | `homeAddress.postalCode` |
| Aniversário | `person.birthDayAndMonth` |

## Etapa 3 - Importe dados do local de armazenamento para o destino

Consulte os artigos de destino de marketing de email individuais para saber como importar dados do seu local de armazenamento para destinos:

* [Adobe Campaign](/help/rtcdp/destinations/adobe-campaign-destination.md#import-data-into-campaign)
* [Salesforce Marketing Cloud](/help/rtcdp/destinations/salesforce-marketing-cloud-destination.md#import-data-into-salesforce)
* [Oracle Eloqua](/help/rtcdp/destinations/oracle-eloqua-destination.md#import-data-into-eloqua)
* [Oracle Responsys](/help/rtcdp/destinations/oracle-responsys-destination.md#import-data-into-responsys)

## Ativar segmentos para destinos de marketing de email

Para obter instruções sobre como ativar segmentos para destinos de marketing por email, consulte [Ativar dados para destinos](/help/rtcdp/destinations/activate-destinations.md).