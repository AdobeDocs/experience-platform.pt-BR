---
title: Destinos de marketing de email
seo-title: Destinos de marketing de email
description: Provedores de serviço de email (ESPs) permitem gerenciar suas atividades de marketing de email, como para enviar campanhas de email promocionais.
seo-description: Provedores de serviço de email (ESPs) permitem gerenciar suas atividades de marketing de email, como para enviar campanhas de email promocionais.
translation-type: tm+mt
source-git-commit: 570c627672439a5ee0f4215b7bf7915ec3dd2bb3
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 1%

---


# Destinos de marketing de email {#email-marketing-destinations}

Provedores de serviço de email (ESPs) permitem gerenciar suas atividades de marketing de email, como enviar campanhas de email promocionais. Dados do cliente em tempo real do Adobe A Platform integra-se aos ESPs, permitindo ativar segmentos para destinos de marketing por email.

Para enviar segmentos para destinos de marketing de email para suas campanhas, a CDP em tempo real do Adobe deve primeiro se conectar ao destino.

A conexão com destinos de marketing de email é um processo de três etapas. Cada uma das etapas é descrita mais abaixo nesta página.

No fluxo de destino de conexão, descrito na seção abaixo, conecte-se ao Amazon S3 ou SFTP. A CDP em tempo real exporta seus segmentos como `.csv` ou `.txt` arquivos e os entrega para o local desejado. Agende sua importação de dados na plataforma de marketing por email a partir do local do armazenamento ativado no CDP em tempo real. O processo de importação de dados varia para cada parceiro. Consulte os artigos de destinos individuais para obter mais informações.

## Etapa 1 - Conectar ao destino {#connect-destination}

1. Em **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]**, selecione o destino de marketing de email ao qual você deseja se conectar e selecione o destino **[!UICONTROL do]** Connect.

   ![Conectar ao destino](/help/rtcdp/destinations/assets/connect-email-marketing.png)

2. Na etapa **[!UICONTROL Autenticação]** , se você já tiver configurado uma conexão com o destino de marketing por email, selecione Conta **** existente e selecione a conexão existente. Ou você pode selecionar **[!UICONTROL Nova conta]** para configurar uma nova conexão com seu destino de marketing de email. No seletor de tipo **** Conexão, você pode selecionar entre **Amazon S3**, **SFTP com senha**, **SFTP com chave** SSH. Preencha as informações abaixo, dependendo do tipo de conexão, e selecione **[!UICONTROL Connect (Conectar]**).

   Para conexões **** S3, você deve fornecer a ID da chave de acesso Amazon e a chave de acesso secreta.

   Para **SFTP com conexões de senha** , você deve fornecer Domínio, Porta, Nome de usuário e Senha para seu servidor SFTP.

   Para **SFTP com conexões de chave** SSH, você deve fornecer Domínio, Porta, Nome de usuário e Chave SSH para seu servidor SFTP.

3. Na etapa **[!UICONTROL Configuração]** , digite um **[!UICONTROL Nome]** e uma **[!UICONTROL Descrição]** para o novo destino, bem como o formato **** Arquivo para os arquivos exportados. <br>
Se você selecionou Amazon S3 como opção de armazenamento na etapa anterior, insira o nome **[!UICONTROL do]** compartimento e o caminho **[!UICONTROL da]** pasta no destino do armazenamento na nuvem onde os arquivos serão entregues. Para a opção armazenamento SFTP, insira o caminho **[!UICONTROL da]** pasta onde os arquivos serão entregues. <br>
Também nesta etapa, você pode selecionar qualquer caso **[!UICONTROL de uso de]** Marketing que deve ser aplicado a este destino. Os casos de uso de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar de casos de uso de marketing definidos pelo Adobe ou criar seu próprio caso de uso de marketing. Para obter mais informações sobre casos de uso de marketing, consulte a página [Data Governance em CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) em tempo real. Para obter informações sobre casos individuais de uso de marketing definidos pelo Adobe, consulte a visão geral [das políticas de uso de](/help/data-governance/policies/overview.md#core-actions)dados. <br>
   ![Etapa de configuração de email](/help/rtcdp/destinations/assets/email-setup-step.png)

## Etapa 2 - Selecione os membros do segmento a serem incluídos nas exportações de destino {#select-segments}

Na página **[!UICONTROL Selecionar segmentos]** , selecione quais segmentos serão enviados para o destino. Encontre mais informações sobre os campos nas seções abaixo.

![Selecionar segmentos](/help/rtcdp/destinations/assets/email-select-segments.png)

## Etapa 3 - Selecione os campos de schema a serem usados como atributos de destino nos arquivos exportados {#destination-attributes}

Nesta etapa, você está selecionando quais campos exportar para destinos de marketing de email.

![Atributos de destino](/help/rtcdp/destinations/assets/destination-attributes.png)

### Identidade {#identity}

Recomendamos que você selecione um identificador exclusivo do seu schema [de](../../profile/home.md#profile-fragments-and-union-schemas)união. Este é o campo do qual as identidades de seus usuários são destacadas. Normalmente, esse campo é o endereço de email, mas também pode ser uma ID de programa de fidelidade ou um número de telefone. Consulte a tabela abaixo para obter os identificadores exclusivos mais comuns e seus campos XDM no schema da união.

| Identificador exclusivo | Campo XDM no Schema Unificado |
---------|----------
| Endereço de email | `personalEmail.address` |
| Telefone | `mobilePhone.number` |
| ID do programa de fidelidade | `Customer-defined XDM field` |

### Outros atributos de destino

No seletor de campo Schema, escolha os outros campos que deseja exportar para o destino do email. Algumas opções recomendadas são:

| Esquema | Campo XDM |
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
* [Marketing Cloud do Salesforce](/help/rtcdp/destinations/salesforce-marketing-cloud-destination.md#import-data-into-salesforce)
* [Oracle Eloqua](/help/rtcdp/destinations/oracle-eloqua-destination.md#import-data-into-eloqua)
* [Oracle Responsys](/help/rtcdp/destinations/oracle-responsys-destination.md#import-data-into-responsys)

## Ativar segmentos para destinos de marketing de email

Para obter instruções sobre como ativar segmentos para destinos de marketing por email, consulte [Ativar dados para destinos](/help/rtcdp/destinations/activate-destinations.md).