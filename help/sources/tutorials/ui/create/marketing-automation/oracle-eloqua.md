---
title: Criar uma conexão de origem do Oracle Eloqua usando a interface do usuário do Experience Platform
description: Saiba como conectar o Adobe Experience Platform ao Oracle Eloqua usando a interface do usuário do Experience Platform.
exl-id: c4431d85-5948-4122-9a99-dbacdde5a09f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 2%

---

# Criar uma conexão de origem [!DNL Oracle Eloqua] usando a interface do Experience Platform

>[!WARNING]
>
>A origem [!DNL Oracle Eloqua] será substituída no final de junho de 2025.

Este tutorial fornece etapas para criar uma conexão de origem [!DNL Oracle Eloqua] usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

Se você já tiver uma conta autenticada do [!DNL Oracle Eloqua] no Experience Platform, ignore o restante deste documento e prossiga para o tutorial em [criação de um fluxo de dados para trazer dados de automação de marketing para o Experience Platform](../../dataflow/marketing-automation.md).

### Coletar credenciais necessárias

Para conectar [!DNL Oracle Eloqua] ao Experience Platform, você deve fornecer valores para as seguintes propriedades de autenticação:

| Credencial | Descrição |
| --- | --- |
| Endpoint | O ponto de extremidade do servidor [!DNL Oracle Eloqua]. [!DNL Oracle Eloqua] dá suporte a vários data centers. Para encontrar seu ponto de extremidade, faça logon na [[!DNL Oracle Eloqua] interface](https://login.eloqua.com) com suas credenciais e copie a parte da URL de base da URL de redirecionamento. O formato do padrão de URL é `xxx.xx.eloqua.com` e deve ser inserido sem `http` ou `https`. |
| Nome de usuário | O nome de usuário do servidor [!DNL Oracle Eloqua]. O nome de usuário deve ser formatado como `siteName + \\ + username`, onde `siteName` é o nome da empresa que você usou para fazer logon em [!DNL Oracle Eloqua] e `username` é seu nome de usuário. Por exemplo, seu nome de usuário de logon pode ser: `Eloqua\Andy`. **Observação**: você deve usar uma única barra invertida (`\`) ao usar a interface do usuário, pois a interface do usuário do Experience Platform adiciona automaticamente uma barra invertida adicional (`\`) ao inserir um nome de usuário. |
| Senha | A senha correspondente ao seu nome de usuário [!DNL Oracle Eloqua]. |

Para obter mais informações sobre credenciais de autenticação para [!DNL Oracle Eloqua], consulte o [[!DNL Oracle Eloqua] guia sobre autenticação](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular sua conta do [!DNL Oracle Eloqua] à Experience Platform.

## Conectar sua conta do [!DNL Oracle Eloqua]

Na interface do Experience Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria [!UICONTROL Automação de marketing], selecione **[!UICONTROL Oracle Eloqua]** e **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/oracle-eloqua/catalog.png)

A página **[!UICONTROL Conectar conta do Oracle Eloqua]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a conta [!DNL Oracle Eloqua] com a qual deseja criar um novo fluxo de dados e clique em **[!UICONTROL Avançar]** para continuar.

![existente](../../../../images/tutorials/create/oracle-eloqua/existing.png)

### Nova conta

Se você estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e os valores apropriados para suas credenciais do [!DNL Oracle Eloqua]. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![novo](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Próximas etapas

Seguindo este tutorial, você autenticou e criou uma conexão de origem entre sua conta do [!DNL Oracle Eloqua] e a Experience Platform. Agora você pode seguir para o próximo tutorial e [criar um fluxo de dados para trazer os dados de automação de marketing para o Experience Platform](../../dataflow/marketing-automation.md).
