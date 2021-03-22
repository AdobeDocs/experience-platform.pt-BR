---
keywords: email; Email; email; destinos de email
title: Visão geral dos destinos de marketing por email
type: Tutorial
description: Os provedores de serviços de email (ESPs) permitem gerenciar suas atividades de marketing por email, como para enviar campanhas de email promocionais.
translation-type: tm+mt
source-git-commit: 7d579d85d427c45f39d000288ed883c7ffd003bf
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 1%

---


# Visão geral dos destinos de marketing de email {#email-marketing-destinations}

Os provedores de serviços de email (ESPs) permitem gerenciar suas atividades de marketing por email, como enviar campanhas de email promocionais. O Adobe Experience Platform integra-se com ESPs permitindo ativar segmentos para destinos de marketing por email.

Para enviar segmentos para destinos de marketing por email para suas campanhas, a Platform deve primeiro se conectar ao destino.

A conexão com destinos de marketing por email é um processo de três etapas. Cada uma das etapas é descrita abaixo nesta página.

No fluxo de destino de conexão, descrito na seção abaixo, conecte-se ao Amazon S3 ou SFTP. A Platform exporta seus segmentos como arquivos `.csv` ou `.txt` e os entrega ao local desejado. Programe sua importação de dados na sua plataforma de marketing por email a partir do local de armazenamento habilitado na Platform. O processo para importar dados varia de acordo com cada parceiro. Consulte os artigos de destinos individuais para obter mais informações.

## Configurar destino {#connect-destination}

Em **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selecione o destino de marketing por email ao qual deseja se conectar e selecione **[!UICONTROL Configure]**.

![Ligar ao destino](../../assets/catalog/email-marketing/overview/connect-email-marketing.png)

Na etapa **[!UICONTROL Authentication]**, se você tiver configurado anteriormente uma conexão com seu destino de marketing por email, selecione **[!UICONTROL Existing Account]** e selecione sua conexão existente. Ou você pode selecionar **[!UICONTROL New Account]** para configurar uma nova conexão com seu destino de marketing por email. No seletor **[!UICONTROL Connection type]**, é possível selecionar entre Amazon S3, SFTP com senha ou SFTP com chave SSH. Preencha as informações abaixo, dependendo do tipo de conexão, e selecione **[!UICONTROL Connect]**.

- Para **S3 connections**, você deve fornecer sua ID de chave de acesso Amazon e sua chave de acesso secreta.
- Para **SFTP com conexões Password**, você deve fornecer Domínio, Porta, Nome de usuário e Senha para o servidor SFTP.
- Para conexões **SFTP com chave SSH**, você deve fornecer domínio, porta, nome de usuário e chave SSH para o servidor SFTP.

Como opção, você pode anexar sua chave pública formatada em RSA para adicionar criptografia aos arquivos exportados na seção **[!UICONTROL Key]**. Observe que essa chave pública **must** deve ser gravada como uma string codificada em Base64.

Na etapa **[!UICONTROL Setup]** , digite um nome e uma descrição para o novo destino, bem como o formato de arquivo para os arquivos exportados.

Se você selecionou Amazon S3 como opção de armazenamento na etapa anterior, insira o nome do bucket e o caminho da pasta no destino de armazenamento na nuvem onde os arquivos serão entregues. Para a opção de armazenamento SFTP, insira o caminho da pasta onde os arquivos serão entregues.

Além disso, nesta etapa, é possível selecionar qualquer ação de marketing que deve se aplicar a esse destino. As ações de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar ações de marketing definidas pelo Adobe ou criar sua própria ação de marketing. Para obter mais informações sobre ações de marketing, consulte a [Visão geral das políticas de uso de dados](../../../data-governance/policies/overview.md).

![Etapa de configuração de email](../../assets/catalog/email-marketing/overview/email-setup-step.png)

## Selecione quais membros de segmento incluir nas exportações de destino {#select-segments}

Na página **[!UICONTROL Select Segments]** , selecione quais segmentos enviar para o destino. Encontre mais informações sobre os campos nas seções abaixo.

![Selecionar segmentos](../../assets/common/email-select-segments.png)

## Configurar nomes de arquivo

Para obter informações sobre o agendamento do segmento e as opções de edição de nome de arquivo, consulte a etapa [Configurar](../../ui/activate-destinations.md#configure) no tutorial ativar destinos.

## Selecionar atributos - Selecione quais campos do esquema usar como atributos de destino em seus arquivos exportados {#destination-attributes}

Nesta etapa, você está selecionando quais campos serão exportados para destinos de marketing por email, bem como marcando quais campos são obrigatórios.

![Atributos de destino](../../assets/catalog/email-marketing/overview/recommended-attributes.png)

Para obter mais informações sobre essa etapa, consulte a etapa [Selecionar atributos](../../ui/activate-destinations.md#select-attributes) no tutorial ativar destinos.

## Identidade {#identity}

Recomendamos que você selecione um identificador exclusivo no [union schema](../../../profile/home.md#profile-fragments-and-union-schemas). Este é o campo do qual as identidades dos usuários são destacadas. Geralmente, esse campo é o endereço de email, mas também pode ser uma ID de programa de fidelidade ou um número de telefone. Consulte a tabela abaixo para obter os identificadores exclusivos mais comuns e seu campo XDM no esquema.

| Identificador exclusivo | Campo XDM no esquema unificado |
----------------- | ---------------------------
| Endereço de email | `personalEmail.address` |
| Telefone | `mobilePhone.number` |
| ID do programa de fidelidade | `Customer-defined XDM field` |

## Outros atributos de destino

No seletor de campo Schema , escolha outros campos que deseja exportar para o destino do email. Algumas opções recomendadas são:

| Esquema | Campo XDM |
------ | ---------
| Nome | `person.name.firstName` |
| Sobrenome | `person.name.lastName` |
| Telefone | `mobilePhone.number` |
| Cidade do Endereço | `homeAddress.city` |
| Estado do Endereço | `homeAddress.stateProvince` |
| Código postal do endereço | `homeAddress.postalCode` |
| Aniversário | `person.birthDayAndMonth` |
| Associação de segmento | `segmentMembership.status` |

## Importe dados do seu local de armazenamento para o destino

Consulte os artigos de destino de marketing por email individuais para saber como importar dados do seu local de armazenamento para destinos:

- [Adobe Campaign](./adobe-campaign.md#import-data-into-campaign)
- [Oracle Eloqua](./oracle-eloqua.md#import-data-into-eloqua)
- [Oracle Responsys](./oracle-responsys.md#import-data-into-responsys)
- [Marketing Cloud Salesforce](./salesforce-marketing-cloud.md#import-data-into-salesforce)

## Ativar segmentos para destinos de marketing por email

Para obter instruções sobre como ativar segmentos para destinos de marketing por email, consulte [Ativar dados para destinos](../../ui/activate-destinations.md).

## Recursos adicionais

- [Ativar dados para destinos](../../ui/activate-destinations.md)
- [Criar destinos de marketing por email e ativar dados usando a API do Serviço de fluxo](../../api/email-marketing.md)