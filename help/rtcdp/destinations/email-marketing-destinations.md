---
title: Destinos de marketing de email
seo-title: Destinos de marketing de email
description: Provedores de serviço de email (ESPs) permitem gerenciar suas atividades de marketing de email, como para enviar campanhas de email promocionais.
seo-description: Provedores de serviço de email (ESPs) permitem gerenciar suas atividades de marketing de email, como para enviar campanhas de email promocionais.
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87

---


# Destinos de marketing de email {#email-marketing-destinations}

Provedores de serviço de email (ESPs) permitem gerenciar suas atividades de marketing de email, como enviar campanhas de email promocionais. A Plataforma de dados do cliente em tempo real da Adobe integra-se aos ESPs, permitindo que você ative segmentos para destinos de marketing por email.

Para enviar segmentos para destinos de marketing de email para suas campanhas, o Adobe Real-time CDP deve primeiro se conectar ao destino.

A conexão com destinos de marketing de email é um processo de três etapas. Cada uma das etapas é descrita mais abaixo nesta página.

No fluxo de destino de conexão, descrito na seção abaixo, conecte-se ao Amazon S3 ou ao SFTP. A CDP em tempo real exporta seus segmentos como `.csv` ou `.txt` arquivos e os entrega para o local desejado. Agende sua importação de dados na plataforma de marketing por email a partir do local do armazenamento ativado no CDP em tempo real. O processo de importação de dados varia para cada parceiro. Consulte os artigos de destinos individuais para obter mais informações.

## Etapa 1 - Conectar ao destino {#connect-destination}

1. Em **[!UICONTROL Connections > Destinations]**, selecione o destino de marketing de email ao qual você deseja se conectar e selecione **[!UICONTROL Connect destination]**.

   ![Conectar ao destino](/help/rtcdp/destinations/assets/connect-destination.png)

2. No assistente do Connect , selecione o local **[!UICONTROL Connection type]** do seu armazenamento. Você pode selecionar entre **Amazon S3**, **SFTP com senha**, **SFTP com chave** SSH. Preencha as informações abaixo, dependendo do tipo de conexão, e selecione **[!UICONTROL Connect]**.

Para conexões **** S3, você deve fornecer a ID da chave de acesso e a chave de acesso secreta.

Para **SFTP com conexões de senha** , você deve fornecer Domínio, Porta, Nome de usuário e Senha.

Para **SFTP com conexões de chave** SSH, você deve fornecer Domínio, Porta, Nome de usuário e Chave SSH.

## Etapa 2 - Selecione os campos de schema a serem usados como atributos de destino nos arquivos exportados {#destination-attributes}

Nesta etapa, você está selecionando quais campos exportar para destinos de marketing de email.

![Atributos de destino](/help/rtcdp/destinations/assets/destination-attributes.png)

### Identidade {#identity}

Recomendamos que você selecione um identificador exclusivo do seu schema [de](../../profile/home.md#profile-fragments-and-union-schemas)união. Este é o campo do qual as identidades de seus usuários são destacadas. Normalmente, esse campo é o endereço de email, mas também pode ser uma ID de programa de fidelidade ou um número de telefone. Consulte a tabela abaixo para obter os identificadores exclusivos mais comuns e seus campos XDM no schema unificado.

| Identificador exclusivo | Campo XDM no Schema Unificado |
---------|----------
| Endereço de email | `personalEmail.address` |
| Telefone | `mobilePhone.number` |
| ID do programa de fidelidade | `Customer-defined XDM field` |

### Outros atributos de destino

No seletor de campo Schema, escolha os outros campos que deseja exportar para o destino do email. Algumas opções recomendadas são:

| Schema | Campo XDM |
---------|----------
| Nome | `person.name.firstName` |
| Sobrenome | `person.name.lastName` |
| Telefone | `mobilePhone.number` |
| Cidade do Endereço | `homeAddress.city` |
| Estado do endereço | `homeAddress.stateProvince` |
| Código postal do endereço | `homeAddress.postalCode` |
| Aniversário | `person.birthDayAndMonth` |

## Etapa 3 - Importar dados do local do armazenamento para o destino

Consulte os artigos de destino de marketing de email individuais para saber como importar dados da localização do armazenamento para destinos:

* [Adobe Campaign](/help/rtcdp/destinations/adobe-campaign-destination.md#import-data-into-campaign)
* [Salesforce Marketing Cloud](/help/rtcdp/destinations/salesforce-marketing-cloud-destination.md#import-data-into-salesforce)
* [Oracle Eloqua](/help/rtcdp/destinations/oracle-eloqua-destination.md#import-data-into-eloqua)
* [Oracle Responsys](/help/rtcdp/destinations/oracle-responsys-destination.md#import-data-into-responsys)

## Ativar segmentos para destinos de marketing de email

Para obter instruções sobre como ativar segmentos para destinos de marketing por email, consulte [Ativar dados para destinos](/help/rtcdp/destinations/activate-destinations.md).