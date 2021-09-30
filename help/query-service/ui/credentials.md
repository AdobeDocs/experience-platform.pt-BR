---
keywords: Experience Platform, home, tópicos populares, serviço de consultas, serviço de consultas, consulta, editor de consultas, Editor de consultas, Editor de consultas, Editor de consultas;
solution: Experience Platform
title: Guia da interface do usuário do serviço de query
topic-legacy: guide
description: O Adobe Experience Platform Query Service fornece uma interface de usuário que pode ser usada para gravar e executar consultas, exibir consultas executadas anteriormente e acessar consultas salvas pelos usuários em sua Organização IMS.
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: 696db8081ab8225d79cd468b7435770d407d3e3d
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 1%

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

### Pré-requisitos

Antes de gerar credenciais que não estão expirando, você deve concluir as seguintes etapas no Adobe Admin Console:

1. Faça logon em [Adobe Admin Console](https://adminconsole.adobe.com/) e selecione a Org relevante na barra de navegação superior.
2. [Selecione um perfil de produto.](../../access-control/ui/browse.md)
3. [Configure as permissões de  **** sandboxes e  **Gerenciar** ](../../access-control/ui/permissions.md) integrações do serviço de consulta para o perfil do produto.
4. [Adicione um novo usuário a um ](../../access-control/ui/users.md) perfil de produto para que ele receba as permissões configuradas.
5. [Adicione o usuário como um ](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html) administrador de perfil de produto para permitir a criação de uma conta para qualquer perfil de produto ativo.
6. [Adicione o usuário como um ](https://helpx.adobe.com/br/enterprise/using/manage-developers.html) desenvolvedor de perfil de produto para criar uma integração.

Para saber mais sobre como atribuir permissões, leia a documentação em [controle de acesso](../../access-control/home.md).

Todas as permissões necessárias agora estão configuradas no Console do desenvolvedor do Adobe para que o usuário use o recurso de credenciais que está expirando.

### Gerar credenciais

Para criar um conjunto de credenciais que não estão expirando, retorne à interface do usuário da plataforma e selecione **[!UICONTROL Queries]** na navegação à esquerda para acessar o espaço de trabalho [!UICONTROL Queries]. Em seguida, selecione a guia **[!UICONTROL Credentials]** seguida de **[!UICONTROL Generate credentials]**.

![](../images/ui/credentials/generate-credentials.png)

Uma caixa de diálogo é exibida e permite gerar credenciais. Para criar credenciais que não estão expirando, você deve fornecer os seguintes detalhes:

- **[!UICONTROL Nome]**: O nome das credenciais que você está gerando.
- **[!UICONTROL Descrição]**: (Opcional) Uma descrição das credenciais que você está gerando.
- **[!UICONTROL Atribuído a]**: O usuário ao qual as credenciais serão atribuídas. Esse valor deve ser o endereço de email do usuário que está criando as credenciais.
- **[!UICONTROL Senha]**  (Opcional) Uma senha opcional para suas credenciais. Se a senha não for definida, o Adobe gerará automaticamente uma senha para você.

Depois de fornecer todos os detalhes necessários, selecione **[!UICONTROL Generate credentials]** para gerar suas credenciais.

![](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>Depois que o botão **[!UICONTROL Generate credentials]** é selecionado, um arquivo JSON de configuração é baixado no computador local. Como o Adobe **not** registra as credenciais geradas, você deve armazenar com segurança o arquivo baixado e manter um registro da credencial.
>
>Além disso, se as credenciais não forem usadas por 90 dias, elas serão expurgadas.

O arquivo JSON de configuração contém informações como nome técnico da conta, ID da conta técnica e credencial. Ele é fornecido no formato a seguir.

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

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

Você pode usar as credenciais que estão expirando ou que não estão expirando para se conectar a clientes externos, como o Aqua Data Studio, o Looker ou o Power BI. O método de entrada dessas credenciais varia dependendo do cliente externo. Consulte a documentação do cliente externo para obter instruções específicas sobre o uso dessas credenciais.

A imagem indica o local de cada parâmetro encontrado na interface do usuário, exceto a senha das credenciais que não expiram. Embora as credenciais que não expiram sejam fornecidas pelos arquivos de configuração JSON, você pode exibir suas credenciais que expiram na guia **Credentials** na interface do usuário.

![](../images/ui/credentials/expiring-credentials.png)

A tabela abaixo descreve os parâmetros normalmente necessários para se conectar a clientes externos.

>[!NOTE]
>
>Ao se conectar a um host usando credenciais que não estão expirando, ainda é necessário usar todos os parâmetros listados na seção [!UICONTROL EXPIRING CREDENTIALS] exceto a senha e o nome de usuário.

| Parâmetro | Descrição |
|---|---|
| Servidor/Host | O nome do servidor/host ao qual você está se conectando. <ul><li>Esse valor é usado para credenciais que expiram e credenciais que não expiram e assume a forma de `server.adobe.io`. O valor é encontrado em **[!UICONTROL Host]** na seção [!UICONTROL EXPIRANDO CREDENCIAIS].</ul></li> |
| Porta | A porta do servidor/host ao qual você está se conectando. <ul><li>Esse valor é usado para credenciais que expiram e credenciais que não expiram e é encontrado em **[!UICONTROL Port]** na seção [!UICONTROL EXPIRING CREDENTIALS]. Um exemplo de valor para a porta seria `80`.</ul></li> |
| Banco de dados | O banco de dados ao qual você está se conectando. <ul><li>Esse valor é usado para credenciais que expiram e credenciais que não expiram e encontrado em **[!UICONTROL Database]** na seção [!UICONTROL EXPIRING CREDENTIALS]. Um exemplo de valor para o banco de dados seria `prod:all`.</ul></li> |
| Nome do usuário | O nome de usuário do usuário que está se conectando ao cliente externo. <ul><li>Se você estiver usando credenciais que estão expirando, isso assumirá a forma de uma sequência de caracteres alfanumérica antes de `@AdobeOrg`. Esse valor é encontrado em **[!UICONTROL Username]**.</li><li>Se você estiver usando credenciais que não estão expirando, essa será uma string de sua escolha, embora **não possa** ser a mesma que o valor `technicalAccountID` encontrado no arquivo JSON de configuração.</li></ul> |
| Senha | A senha do usuário que está se conectando ao cliente externo. <ul><li>Se você estiver usando credenciais que estão expirando, isso poderá ser encontrado em **[!UICONTROL Password]** na seção [!UICONTROL EXPIRING CREDENTIALS].</li><li>Se você estiver usando credenciais que não estão expirando, esse valor será o argumento concatenado de technicalAccountID e a credencial obtida do arquivo JSON de configuração. O valor da senha assume o formulário: `{technicalAccountId}:{credential}`.</li></ul> |

## Próximas etapas

Agora que você entende como as credenciais que estão expirando e que não estão expirando funcionam, pode usar essas credenciais para se conectar a clientes externos. Para obter mais informações detalhadas sobre clientes externos, leia o [guia Conectar clientes ao Serviço de query](../clients/overview.md).
