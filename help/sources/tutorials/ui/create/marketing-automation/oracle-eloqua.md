---
title: Criar uma conexão de origem do Oracle Eloqua usando a interface do usuário da plataforma
description: Saiba como conectar o Adobe Experience Platform ao Oracle Eloqua usando a interface do usuário da plataforma.
exl-id: c4431d85-5948-4122-9a99-dbacdde5a09f
source-git-commit: e8f54f06ad3431227e140219a9960e8e04f83ccc
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 1%

---

# Criar um [!DNL Oracle Eloqua] conexão de origem usando a interface do usuário da Platform

Este tutorial fornece etapas para a criação de um [!DNL Oracle Eloqua] conexão de origem usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes da Platform:

* [Origens](../../../../home.md): a Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da Platform.
* [Sandboxes](../../../../../sandboxes/home.md): a Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

Se você já tiver um [!DNL Oracle Eloqua] conta na Platform, ignore o restante deste documento e prossiga para o tutorial em [criação de um fluxo de dados para trazer dados de automação de marketing para a Platform](../../dataflow/marketing-automation.md).

### Coletar credenciais necessárias

Para se conectar [!DNL Oracle Eloqua] Para o Platform, você deve fornecer valores para as seguintes propriedades de autenticação:

| Credencial | Descrição |
| --- | --- |
| Endpoint | O terminal do seu [!DNL Oracle Eloqua] servidor. [!DNL Oracle Eloqua] O suporta vários data centers. Para encontrar seu terminal, faça logon na [[!DNL Oracle Eloqua] interface](https://login.eloqua.com) com suas credenciais e, em seguida, copie a parte do URL básico do URL de redirecionamento. O formato para o padrão do URL é `xxx.xx.eloqua.com` e devem ser inseridas sem `http` ou `https`. |
| Nome de usuário | O nome de usuário do seu [!DNL Oracle Eloqua] servidor. O nome de usuário deve ser formatado como `siteName + \\ + username`, onde `siteName` é o nome da empresa na qual você fez logon [!DNL Oracle Eloqua] e `username` é seu nome de usuário. Por exemplo, seu nome de usuário de logon pode ser: `Eloqua\Andy`. **Nota**: você deve usar uma única barra invertida (`\`) ao usar a interface do usuário do, pois a interface do usuário do Experience Platform adiciona automaticamente uma barra invertida adicional (`\`) ao inserir um nome de usuário. |
| Senha | A senha correspondente ao seu [!DNL Oracle Eloqua] usuário. |

Para obter mais informações sobre credenciais de autenticação para [!DNL Oracle Eloqua], consulte o [[!DNL Oracle Eloqua] guia sobre autenticação](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular [!DNL Oracle Eloqua] para a Platform.

## Conecte seu [!DNL Oracle Eloqua] account

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No [!UICONTROL Automação de marketing] categoria, selecione **[!UICONTROL Oracle Eloqua]** e selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/oracle-eloqua/catalog.png)

A variável **[!UICONTROL Conectar a conta do Oracle Eloqua]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a variável [!DNL Oracle Eloqua] conta com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próxima]** para continuar.

![existente](../../../../images/tutorials/create/oracle-eloqua/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e os valores apropriados para o [!DNL Oracle Eloqua] credenciais. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para estabelecer a nova conexão.

![novo](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Próximas etapas

Ao seguir este tutorial, você autenticou e criou uma conexão de origem entre [!DNL Oracle Eloqua] conta e plataforma. Agora você pode seguir para o próximo tutorial e [criar um fluxo de dados para trazer dados de automação de marketing para a Platform](../../dataflow/marketing-automation.md).
