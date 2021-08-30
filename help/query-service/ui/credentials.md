---
keywords: Experience Platform, home, tópicos populares, serviço de consultas, serviço de consultas, consulta, editor de consultas, Editor de consultas, Editor de consultas, Editor de consultas;
solution: Experience Platform
title: Guia da interface do usuário do serviço de query
topic-legacy: guide
description: O Adobe Experience Platform Query Service fornece uma interface de usuário que pode ser usada para gravar e executar consultas, exibir consultas executadas anteriormente e acessar consultas salvas pelos usuários em sua Organização IMS.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: aabe89f236bc68a51f14ee1909687982f4fe5973
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 0%

---


# Guia de credenciais

O Adobe Experience Platform Query Service permite conectar-se com clientes externos. Você pode se conectar a esses clientes externos usando credenciais que estão expirando ou credenciais que não estão expirando.

## Credenciais de expiração

Você pode usar as credenciais que estão expirando para configurar rapidamente uma conexão com um cliente externo.

![](../images/ui/credentials/expiring-credentials.png)

A seção **[!UICONTROL Expirando credenciais]** fornece as seguintes informações:

- **[!UICONTROL Host]**: O nome do host ao qual você se conectará. Para conexão com o Serviço de query, isso incluirá o nome da Organização IMS que você está usando no momento.
- **[!UICONTROL Porta]**: O número da porta do host à qual você se conectará.
- **[!UICONTROL Banco de dados]**: O nome do banco de dados ao qual você se conectará.
- **[!UICONTROL Nome de usuário]**: O nome de usuário que você usará para se conectar ao Serviço de query.
- **[!UICONTROL Senha]**: A senha que você usará para se conectar ao Serviço de query.
- **[!UICONTROL comando]** PSQL: Um comando que inseriu automaticamente todas as informações relevantes para você se conectar ao Serviço de query usando PSQL na linha de comando.
- **[!UICONTROL Expira]**: A data de expiração das credenciais que expiram. As credenciais expiram 24 horas após serem geradas.

## Credenciais que não expiram

Você pode usar credenciais que não estão expirando para configurar uma conexão mais permanente com um cliente externo.

Para criar um conjunto de credenciais que não estão expirando, selecione **[!UICONTROL Gerar credenciais]**.

>[!NOTE]
>
>Antes de criar credenciais que não estejam expirando, você deve ter as permissões **Sandboxes** e **Gerenciar integração do serviço de consulta**. Para saber como atribuir essas permissões, leia a documentação em [Controle de acesso](../../access-control/home.md).

![](../images/ui/credentials/generate-credentials.png)

A modal gerar credenciais é exibida. Para criar credenciais que não estão expirando, será necessário fornecer os seguintes detalhes:

- **[!UICONTROL Nome]**: O nome das credenciais que você está gerando.
- **[!UICONTROL Descrição]**: (Opcional) Uma descrição das credenciais que você está gerando.
- **[!UICONTROL Atribuído a]**: O usuário ao qual as credenciais serão atribuídas. Esse valor deve ser o endereço de email do usuário que está criando as credenciais.
- **[!UICONTROL Senha]**  (Opcional) Uma senha opcional para suas credenciais. Se a senha não for definida, o Adobe gerará automaticamente uma senha para você.

Depois de fornecer todos os detalhes necessários, selecione **[!UICONTROL Generate credentials]** para gerar suas credenciais.

![](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>Depois que o botão **[!UICONTROL Generate credentials]** é selecionado, um arquivo de configuração que contém informações como nome de conta técnica, ID de conta técnica e credencial. Como o Adobe **not** registra a credencial gerada, você **deve** armazenar com segurança o arquivo baixado e manter um registro da credencial.
>
>Além disso, se as credenciais não forem usadas por 90 dias, elas serão removidas.

Depois de salvar suas credenciais geradas, selecione **[!UICONTROL Fechar]**. Agora você pode ver uma lista de todas as suas credenciais que não estão expirando.

![](../images/ui/credentials/list-credentials.png)

Você pode editar ou excluir suas credenciais que não expiram. Para editar uma credencial que não expire, selecione o ícone de lápis (![](../images/ui/credentials/edit-icon.png)). Para excluir uma credencial que não esteja expirando, selecione o ícone excluir (![](../images/ui/credentials/delete-icon.png)).

Ao editar uma credencial que não esteja expirando, um modal é exibido. Você pode fornecer os seguintes detalhes para atualizar:

- **[!UICONTROL Nome]**: O nome das credenciais que você está gerando.
- **[!UICONTROL Descrição]**: (Opcional) Uma descrição das credenciais que você está gerando.
- **[!UICONTROL Atribuído a]**: O usuário ao qual as credenciais serão atribuídas. Esse valor deve ser o endereço de email do usuário que está criando as credenciais.

![](../images/ui/credentials/update-credentials.png)

Depois de fornecer todos os detalhes necessários, selecione **[!UICONTROL Update account]** para concluir a atualização de suas credenciais.

## Usar credenciais para se conectar a clientes externos

Você pode usar as credenciais que estão expirando ou que não estão expirando para se conectar a clientes externos, como o Aqua Data Studio, o Looker ou o Power BI.

Ao se conectar a esses clientes externos, geralmente é necessário incluir as seguintes informações:

- **Servidor/Host**: O nome do servidor/host ao qual você está se conectando. Esse valor assume a forma de `server.adobe.io` e pode ser encontrado em **[!UICONTROL Host]** na seção de credenciais que estão expirando.
- **Porta**: A porta do servidor/host ao qual você está se conectando. Esse valor pode ser encontrado em **[!UICONTROL Port]** na seção de credenciais que estão expirando. Um exemplo de valor para a porta seria `80`.
- **Nome de usuário**: O nome de usuário do usuário que está se conectando ao cliente externo. Isso assume o formato de `ID@AdobeOrg` e pode ser encontrado em **[!UICONTROL Nome de usuário]** na seção de credenciais que estão expirando.
- **Senha**: A senha do usuário que está se conectando ao cliente externo. Se você estiver usando credenciais que estão expirando, isso poderá ser encontrado em **[!UICONTROL Password]** na seção de credenciais que estão expirando. Se você estiver usando credenciais que não estão expirando, esse valor será composto pela ID da conta técnica e pela credencial no formulário: `technicalAccountId:credential`.
- **Banco de dados**: O banco de dados ao qual você está se conectando. Esse valor pode ser encontrado em **[!UICONTROL Database]** na seção de credenciais que estão expirando. Um exemplo de valor para o banco de dados seria `prod:all`.

## Próximas etapas

Agora que você entende como as credenciais que estão expirando e que não estão expirando funcionam, pode usar essas credenciais para se conectar a clientes externos. Para obter mais informações detalhadas sobre clientes externos, leia o [guia Conectar clientes ao Serviço de query](../clients/overview.md).