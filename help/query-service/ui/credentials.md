---
keywords: Experience Platform, home, tópicos populares, serviço de consultas, serviço de consultas, consulta, editor de consultas, Editor de consultas, Editor de consultas, Editor de consultas;
solution: Experience Platform
title: Guia de credenciais do serviço de query
description: O Adobe Experience Platform Query Service fornece uma interface de usuário que pode ser usada para gravar e executar consultas, exibir consultas executadas anteriormente e acessar consultas salvas pelos usuários em sua organização.
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 3%

---

# Guia de credenciais

O Adobe Experience Platform Query Service permite conectar-se com clientes externos. Você pode se conectar a esses clientes externos usando credenciais que estão expirando ou credenciais que não estão expirando.

## Credenciais de expiração {#expiring-credentials}

>[!CONTEXTUALHELP]
>id="platform_queryservice_credentials_expiringcredentials"
>title="Modo SSL do cliente"
>abstract="O SSL deve ser habilitado nos clientes conectados ao Query Service. Verifique se o modo SSL está definido como “obrigatório”."

Você pode usar as credenciais que estão expirando para configurar rapidamente uma conexão com um cliente externo.

![A guia Query dashboard Credentials com a seção Expiring credentials realçada.](../images/ui/credentials/expiring-credentials.png)

O **[!UICONTROL Credenciais de expiração]** fornece as seguintes informações:

- **[!UICONTROL Host]**: O nome do host ao qual conectar seu cliente. Isso incorpora o nome da sua organização, conforme visto na faixa superior da interface do usuário da plataforma.
- **[!UICONTROL Port]**: O número da porta do host à qual se conectar.
- **[!UICONTROL Banco de dados]**: O nome do banco de dados ao qual conectar um cliente.
- **[!UICONTROL Nome do usuário]**: O nome de usuário usado para se conectar ao Serviço de query.
- **[!UICONTROL Senha]**: A senha usada para se conectar ao Serviço de Consulta. As senhas na interface do usuário foram transformadas em hash para fins de segurança. Selecione o ícone de cópia (![O ícone de cópia.](../images/ui/credentials/copy-icon.png)) para copiar suas credenciais completas e sem hash para a área de transferência.
- **[!UICONTROL comando PSQL]**: Um comando que inseriu automaticamente todas as informações relevantes para você se conectar ao Serviço de query usando PSQL na linha de comando.
- **[!UICONTROL Expira]**: A data e a hora de expiração das credenciais. A duração padrão da validade do token é de 24 horas, mas pode ser alterada nas configurações avançadas do Admin Console.

>[!TIP]
>
>Para alterar a vida da sessão para sua conexão de credenciais que expiram com o Serviço de query, navegue até o [Admin Console](https://adminconsole.adobe.com/) e selecione as seguintes opções na tela: **Configurações** > **Privacidade e segurança** > **Configurações de autenticação** > **Configurações avançadas** > **Duração máxima da sessão**.
>
>![A guia Admin Console settings com Privacy and Security, Authentication settings e Max session life foi realçada.](../images/ui/credentials/max-session-life.png)
>
>Consulte a documentação de Ajuda do Adobe para obter mais informações sobre [Configurações avançadas](https://helpx.adobe.com/enterprise/using/authentication-settings.html#advanced-settings) oferecido pelo Admin Console.

## Credenciais que não expiram {#non-expiring-credentials}

Você pode usar credenciais que não estão expirando para configurar uma conexão mais permanente com um cliente externo.

### Pré-requisitos

Antes de gerar credenciais que não estão expirando, você deve concluir as seguintes etapas no Adobe Admin Console:

1. Faça logon [Adobe Admin Console](https://adminconsole.adobe.com/) e selecione a Org relevante na barra de navegação superior.
2. [Selecione um perfil de produto.](../../access-control/ui/browse.md)
3. [Configure ambas as **Sandboxes** e **Gerenciar integração do serviço de consulta** permissões](../../access-control/ui/permissions.md) para o perfil do produto.
4. [Adicionar um novo usuário a um perfil de produto](../../access-control/ui/users.md) assim, as permissões configuradas são concedidas a eles.
5. [Adicionar o usuário como administrador do perfil de produto](https://helpx.adobe.com/br/enterprise/using/manage-product-profiles.html) para permitir a criação de uma conta para qualquer perfil de produto ativo.
6. [Adicionar o usuário como desenvolvedor de perfil de produto](https://helpx.adobe.com/br/enterprise/using/manage-developers.html) para criar uma integração.

Para saber mais sobre como atribuir permissões, leia a documentação em [controle de acesso](../../access-control/home.md).

Todas as permissões necessárias agora estão configuradas no Adobe Developer Console para que o usuário use o recurso de credenciais que está expirando.

### Gerar credenciais

Para criar um conjunto de credenciais que não estão expirando, retorne à interface do usuário da plataforma e selecione **[!UICONTROL Queries]** na navegação à esquerda para acessar o [!UICONTROL Queries] espaço de trabalho. Em seguida, selecione o **[!UICONTROL Credenciais]** guia seguida por **[!UICONTROL Gerar credenciais]**.

![O painel Consultas com a guia Credenciais e Gerar credenciais são realçados.](../images/ui/credentials/generate-credentials.png)

Uma caixa de diálogo é exibida e permite gerar credenciais. Para criar credenciais que não estão expirando, você deve fornecer os seguintes detalhes:

- **[!UICONTROL Nome]**: O nome das credenciais que você está gerando.
- **[!UICONTROL Descrição]**: (Opcional) Uma descrição das credenciais que você está gerando.
- **[!UICONTROL Atribuído a]**: O usuário ao qual as credenciais serão atribuídas. Esse valor deve ser o endereço de email do usuário que está criando as credenciais.
- **[!UICONTROL Senha]** (Opcional) Uma senha opcional para suas credenciais. Se a senha não for definida, o Adobe gerará automaticamente uma senha para você.

Depois de fornecer todos os detalhes necessários, selecione **[!UICONTROL Gerar credenciais]** para gerar suas credenciais.

![A caixa de diálogo Gerar credenciais é realçada.](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>When **[!UICONTROL Gerar credenciais]** for selecionado, um arquivo JSON de configuração será baixado no computador local. Como o Adobe faz **not** registre as credenciais geradas, armazene com segurança o arquivo baixado e mantenha um registro da credencial.
>
>Além disso, se as credenciais não forem usadas por 90 dias, elas serão expurgadas.

O arquivo JSON de configuração contém informações como nome técnico da conta, ID da conta técnica e credencial. Ele é fornecido no formato a seguir.

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

Depois de salvar suas credenciais geradas, selecione **[!UICONTROL Fechar]**. Agora você pode ver uma lista de todas as suas credenciais que não estão expirando.

![A guia Query dashboard Credentials com a seção Non-expiring Credentials realçada.](../images/ui/credentials/list-credentials.png)

Você pode editar ou excluir suas credenciais que não expiram. Para editar uma credencial que não esteja expirando, selecione o ícone de lápis (![Um ícone de lápis.](../images/ui/credentials/edit-icon.png)). Para excluir uma credencial que não esteja expirando, selecione o ícone excluir (![Um ícone de lixeira.](../images/ui/credentials/delete-icon.png)).

Ao editar uma credencial que não esteja expirando, um modal é exibido. Você pode fornecer os seguintes detalhes para atualizar:

- **[!UICONTROL Nome]**: O nome das credenciais que você está gerando.
- **[!UICONTROL Descrição]**: (Opcional) Uma descrição das credenciais que você está gerando.
- **[!UICONTROL Atribuído a]**: O usuário ao qual as credenciais serão atribuídas. Esse valor deve ser o endereço de email do usuário que está criando as credenciais.

![A caixa de diálogo Atualizar conta .](../images/ui/credentials/update-credentials.png)

Depois de fornecer todos os detalhes necessários, selecione **[!UICONTROL Atualizar conta]** para concluir a atualização de suas credenciais.

## Usar credenciais para se conectar a clientes externos {#use-credential-to-connect}

Você pode usar as credenciais que estão expirando ou que não estão expirando para se conectar a clientes externos, como o Aqua Data Studio, o Looker ou o Power BI. O método de entrada dessas credenciais varia dependendo do cliente externo. Consulte a documentação do cliente externo para obter instruções específicas sobre o uso dessas credenciais.

A imagem indica o local de cada parâmetro encontrado na interface do usuário, exceto a senha das credenciais que não expiram. Embora as credenciais que não expiram sejam fornecidas pelos arquivos de configuração JSON, você pode visualizar suas credenciais que expiram no **Credenciais** na interface do usuário.

![A guia Query workspace Credentials com a seção Expiring credentials realçada.](../images/ui/credentials/expiring-credentials.png)

A tabela abaixo descreve os parâmetros normalmente necessários para se conectar a clientes externos.

>[!NOTE]
>
>Ao se conectar a um host usando credenciais que não estão expirando, ainda é necessário usar todos os parâmetros listados na variável [!UICONTROL CREDENCIAIS DE EXPIRAÇÃO] exceto por senha e nome de usuário.
>O formato para inserir seu nome de usuário e senha usa valores separados por dois pontos, como é visto neste exemplo `username:{your_username}` e `password:{password_string}`.

| Parâmetro | Descrição | Exemplo |
|---|---|---|
| **Servidor/Host** | O nome do servidor/host ao qual você está se conectando. <ul><li>Esse valor é usado para credenciais que expiram e credenciais que não expiram e assume a forma de `server.adobe.io`. O valor é encontrado em **[!UICONTROL Host]** no [!UICONTROL CREDENCIAIS DE EXPIRAÇÃO] seção.</ul></li> | `acme.platform.adobe.io` |
| **Porta** | A porta do servidor/host ao qual você está se conectando. <ul><li>Esse valor é usado para credenciais que expiram e credenciais que não expiram e é encontrado em **[!UICONTROL Port]** no [!UICONTROL CREDENCIAIS DE EXPIRAÇÃO] seção.</ul></li> | `80` |
| **Banco de dados** | O banco de dados ao qual você está se conectando. <ul><li>Esse valor é usado para credenciais que estão expirando e credenciais que não estão expirando e foi encontrado em **[!UICONTROL Banco de dados]** no [!UICONTROL CREDENCIAIS DE EXPIRAÇÃO] seção. </ul></li> | `prod:all` |
| **Nome de usuário** | O nome de usuário do usuário que está se conectando ao cliente externo. <ul><li>Esse valor é usado para credenciais que estão expirando e credenciais que não estão expirando. Ele assume o formato de uma sequência alfanumérica antes de `@AdobeOrg`. Esse valor é encontrado em **[!UICONTROL Nome do usuário]**.</li></ul> | `ECBB80245ECFC73E8A095EC9@AdobeOrg` |
| **Senha** | A senha do usuário que está se conectando ao cliente externo. <ul><li>Se você estiver usando credenciais que estão expirando, isso poderá ser encontrado em **[!UICONTROL Senha]** no [!UICONTROL CREDENCIAIS DE EXPIRAÇÃO] seção.</li><li>Se você estiver usando credenciais que não estão expirando, esse valor será o argumento concatenado de technicalAccountID e a credencial obtida do arquivo JSON de configuração. O valor da senha assume o formulário: `{technicalAccountId}:{credential}`.</li></ul> | <ul><li>Uma senha de credencial que expira é superior a mil caracteres alfanuméricos. Nenhum exemplo será dado.</li><li>Uma senha de credencial que não expira é a seguinte:<br>`4F2611B8613DK3670V495N55:3d182fa9e0b54f33a7881305c06203ee`</li></ul> |

{style="table-layout:auto"}

## Próximas etapas

Agora que você entende como as credenciais que estão expirando e que não estão expirando funcionam, pode usar essas credenciais para se conectar a clientes externos. Para obter mais informações detalhadas sobre clientes externos, leia o [conectar clientes ao guia Serviço de query](../clients/overview.md).
