---
keywords: Experience Platform, home, tópicos populares, fontes, conectores, conectores de origem, sdk de fontes, sdk, SDK
solution: Experience Platform
title: Criar uma conexão de origem de campanhas MailChimp usando a interface do usuário da plataforma
topic-legacy: tutorial
description: Saiba como conectar o Adobe Experience Platform às campanhas do MailChimp usando a interface do usuário da plataforma.
source-git-commit: a67f9589346a117eb6f51dc9f908680d661e5d5b
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 1%

---


# Crie um [!DNL MailChimp Campaigns] conexão de origem usando a interface do usuário da plataforma

Este tutorial fornece etapas para criar um [!DNL Mailchimp] conector de origem para assimilação [!DNL Mailchimp Campaigns] dados para o Adobe Experience Platform usando a interface do usuário do .

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): A Platform permite que os dados sejam assimilados de várias fontes, além de fornecer a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): A Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Obter credenciais necessárias

Para trazer a [!DNL Mailchimp Campaigns] dados para a Platform, primeiro você deve fornecer as credenciais de autenticação apropriadas que correspondam a [!DNL Mailchimp] conta.

O [!DNL Mailchimp Campaigns] A fonte suporta o Código de atualização OAuth 2 e a autenticação básica, consulte as tabelas abaixo para obter mais informações sobre esses tipos de autenticação.

### Código de atualização do OAuth 2

| Credenciais | Descrição |
| --- | --- |
| Host | O URL raiz usado para se conectar à API MailChimp. O formato do URL raiz é `https://{DC}.api.mailchimp.com`, onde `{DC}` representa o data center que corresponde à sua conta. |
| URL do teste de autorização | O URL do teste de autorização é usado para validar credenciais ao conectar [!DNL Mailchimp] para Platform. Se isso não for fornecido, as credenciais serão verificadas automaticamente durante a etapa de criação da conexão de origem. |
| Token de acesso | O token de acesso correspondente usado para autenticar sua fonte. Isso é necessário para a autenticação baseada em OAuth. |

Para obter mais informações sobre como usar o OAuth 2 para autenticar seu [!DNL Mailchimp] para a Platform, consulte esta [[!DNL Mailchimp] documento sobre o uso do OAuth 2](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/).

### Autenticação básica

| Credenciais | Descrição |
| --- | --- |
| Host | O URL raiz usado para se conectar à API MailChimp. O formato do URL raiz é `https://{DC}.api.mailchimp.com`, onde `{DC}` representa o data center que corresponde à sua conta. |
| Nome do usuário | O nome de usuário que corresponde à sua conta MailChimp. Isso é necessário para a autenticação básica. |
| Senha | A senha que corresponde à sua conta MailChimp. Isso é necessário para a autenticação básica. |

## Conecte seu [!DNL Mailchimp Campaigns] conta para a Platform

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em [!UICONTROL Automação de marketing] categoria , selecione **[!UICONTROL Campanha Mailchimp]** e selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/mailchimp-campaigns/catalog.png)

O **[!UICONTROL Conta de Campanhas do Connect Mailchimp]** será exibida. Nesta página, você pode selecionar se está acessando uma conta existente ou optando por criar uma nova conta.

### Conta existente

Para usar uma conta existente, selecione a [!DNL Mailchimp Campaigns] conta com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próximo]** para continuar.

![existente](../../../../images/tutorials/create/mailchimp-campaigns/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome e uma descrição para o [!DNL Mailchimp Campaigns] detalhes da conexão de origem.

![novo](../../../../images/tutorials/create/mailchimp-campaigns/new.png)

#### Autenticar usando OAuth 2

Para usar o OAuth 2, selecione [!UICONTROL Código de atualização do OAuth 2], forneça valores para seu host, URL do teste de autorização e token de acesso e selecione **[!UICONTROL Conectar-se à origem]**. Aguarde alguns instantes para que suas credenciais sejam validadas e selecione **[!UICONTROL Próximo]** para continuar.

![oauth](../../../../images/tutorials/create/mailchimp-campaigns/oauth.png)

#### Autenticar usando autenticação básica

Para usar a autenticação básica, selecione [!UICONTROL Autenticação básica], forneça valores para seu host, nome de usuário e senha e selecione **[!UICONTROL Conectar-se à origem]**. Aguarde alguns instantes para que suas credenciais sejam validadas e selecione **[!UICONTROL Próximo]** para continuar.

![básico](../../../../images/tutorials/create/mailchimp-campaigns/basic.png)

### Selecionar [!DNL Mailchimp Campaigns] dados

Depois que a fonte for autenticada, você deverá fornecer a variável `campaignId` que corresponde ao seu [!DNL Mailchimp Campaigns] conta.

No [!UICONTROL Selecionar dados] insira sua `campaignId` e depois selecione **[!UICONTROL Explorar]**.

![explore](../../../../images/tutorials/create/mailchimp-campaigns/explore.png)

A página é atualizada em uma árvore de esquema interativa que permite explorar e inspecionar a hierarquia de seus dados. Selecionar **[!UICONTROL Próximo]** para continuar.

![select-data](../../../../images/tutorials/create/mailchimp-campaigns/select-data.png)

## Próximas etapas

Com seu [!DNL Mailchimp] conta autenticada e seu [!DNL Mailchimp Campaigns] dados selecionados, agora é possível começar a criar um fluxo de dados para trazer seus dados para a plataforma. Para obter etapas detalhadas sobre como criar um fluxo de dados, consulte a documentação em [criação de um fluxo de dados para trazer dados de automação de marketing para a Platform](../../dataflow/marketing-automation.md).

