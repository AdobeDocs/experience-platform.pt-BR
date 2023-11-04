---
keywords: Experience Platform;página inicial;tópicos populares;serviço de consulta;serviço de consulta;consulta;editor de consultas;Editor de consultas;editor de consultas;
solution: Experience Platform
title: Guia de credenciais do Serviço de consulta
description: O Serviço de consulta da Adobe Experience Platform fornece uma interface que pode ser usada para gravar e executar consultas, exibir consultas executadas anteriormente e acessar consultas salvas por usuários em sua organização.
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: 74e3dc2fa5fc84b5ce4b09e2adb0093ecb94bd82
workflow-type: tm+mt
source-wordcount: '1517'
ht-degree: 3%

---

# Guia de credenciais

O Adobe Experience Platform Query Service permite conectar-se com clientes externos. Você pode se conectar a esses clientes externos usando credenciais com ou sem expiração.

>[!NOTE]
>
>O painel de credenciais não está disponível automaticamente para todos os usuários. Entre em contato com a equipe de conta do Adobe para solicitar o [!UICONTROL Credenciais] para ser incluída no espaço de trabalho do Serviço de consulta, se necessário. Se solicitado, essa alteração abrange toda a organização e é realizada pela equipe de engenharia do Adobe. Não é uma configuração controlada por usuários.

## Credenciais expiradas {#expiring-credentials}

>[!CONTEXTUALHELP]
>id="platform_queryservice_credentials_expiringcredentials"
>title="Modo SSL do cliente"
>abstract="O SSL deve ser habilitado nos clientes conectados ao Query Service. Verifique se o modo SSL está definido como “obrigatório”."

Você pode usar credenciais com expiração para configurar rapidamente uma conexão com um cliente externo.

![A guia Credenciais do painel de consultas com a seção Credenciais que expiram destacada.](../images/ui/credentials/expiring-credentials.png)

A variável **[!UICONTROL Credenciais que expiram]** fornece as seguintes informações:

- **[!UICONTROL Host]**: O nome do host ao qual conectar o cliente. Ele incorpora o nome da sua organização, como visto na faixa superior da interface do usuário da Platform.
- **[!UICONTROL Porta]**: o número da porta do host ao qual se conectar.
- **[!UICONTROL Banco de dados]**: O nome do banco de dados ao qual conectar um cliente.
- **[!UICONTROL Nome de usuário]**: o nome de usuário usado para se conectar ao Serviço de consulta.
- **[!UICONTROL Senha]**: a senha usada para se conectar ao Serviço de consulta. As senhas na interface do usuário receberam hash por questões de segurança. Selecione o ícone de cópia (![O ícone de cópia.](../images/ui/credentials/copy-icon.png)) para copiar suas credenciais completas e sem hash para a área de transferência.
- **[!UICONTROL comando PSQL]**: um comando que inseriu automaticamente todas as informações relevantes para você se conectar ao Serviço de consulta usando PSQL na linha de comando.
- **[!UICONTROL Expira]**: a data e a hora de expiração das credenciais que estão expirando. A duração padrão da validade do token é de 24 horas, mas pode ser alterada nas configurações avançadas do Admin Console.

>[!TIP]
>
>Para alterar a vida útil da sessão para sua conexão de credenciais com o Serviço de consulta expirando, navegue até a [Admin Console](https://adminconsole.adobe.com/) e selecione as seguintes opções na tela: **Configurações** > **Privacidade e segurança** > **Configurações de autenticação** > **Configurações avançadas** > **Duração máxima da sessão**.
>
>![A guia Admin Console settings com Privacy and Security, Authentication settings e Max session life está realçada.](../images/ui/credentials/max-session-life.png)
>
>Consulte a documentação de ajuda do Adobe para obter mais informações sobre o [Configurações avançadas](https://helpx.adobe.com/enterprise/using/authentication-settings.html#advanced-settings) oferecido pelo Admin Console.

## Credenciais sem expiração {#non-expiring-credentials}

Você pode usar credenciais sem expiração para configurar uma conexão mais permanente com um cliente externo.

>[!NOTE]
>
>As credenciais sem expiração têm as seguintes limitações:<br><ul><li>Os usuários devem fazer logon com seu nome de usuário e senha compostos por `{technicalAccountId}:{credential}`. Mais informações podem ser encontradas no [Gerar credenciais](#generate-credentials) seção.</li><li>Após a criação de credenciais que estão expirando, uma nova função com um conjunto de permissões básicas é criada e permite que os usuários visualizem esquemas e conjuntos de dados. A permissão &quot;gerenciar consultas&quot; também é atribuída a essa função para uso com o Serviço de consulta.</li><li>Os clientes de terceiros podem ter um desempenho diferente do esperado ao listar objetos de consulta. Por exemplo, alguns clientes de terceiros, como [!DNL DB Visualizer] não exibirá o nome da visualização no painel esquerdo. No entanto, o nome da exibição pode ser acessado se for chamado em uma consulta SELECT. Da mesma forma, [!DNL PowerUI] não pode listar as exibições temporárias criadas por meio do SQL a serem selecionadas para criação do painel.</li></ul>

### Pré-requisitos

Antes de gerar credenciais sem expiração, você deve concluir as seguintes etapas no Adobe Admin Console:

1. Efetue logon no [Adobe Admin Console](https://adminconsole.adobe.com/) e selecione a Organização relevante na barra de navegação superior.
2. [Selecione um perfil de produto.](../../access-control/ui/browse.md)
3. [Configure os dois **Sandboxes** e **Gerenciar Integração do Serviço de Consulta** permissões](../../access-control/ui/permissions.md) para o perfil do produto.
4. [Adicionar um novo usuário a um perfil de produto](../../access-control/ui/users.md) para que tenham suas permissões configuradas.
5. [Adicionar o usuário como administrador de perfil de produto](https://helpx.adobe.com/br/enterprise/using/manage-product-profiles.html) para permitir a criação de uma conta para qualquer perfil de produto ativo.
6. [Adicionar o usuário como desenvolvedor de perfil de produto](https://helpx.adobe.com/br/enterprise/using/manage-developers.html) para criar uma integração.

Para saber mais sobre como atribuir permissões, leia a documentação em [controle de acesso](../../access-control/home.md).

Todas as permissões necessárias agora estão configuradas no Console do Adobe Developer para que o usuário use o recurso de credenciais que estão expirando.

### Gerar credenciais {#generate-credentials}

Para criar um conjunto de credenciais sem expiração, retorne à interface do usuário da Platform e selecione **[!UICONTROL Consultas]** na navegação à esquerda, para acessar a [!UICONTROL Consultas] espaço de trabalho. Em seguida, selecione o **[!UICONTROL Credenciais]** guia seguida por **[!UICONTROL Gerar credenciais]**.

![O painel Queries com a guia Credenciais e Generate credentials será destacado.](../images/ui/credentials/generate-credentials.png)

Uma caixa de diálogo é exibida com a permissão para gerar credenciais. Para criar credenciais sem expiração, você deve fornecer os seguintes detalhes:

- **[!UICONTROL Nome]**: O nome das credenciais que você está gerando.
- **[!UICONTROL Descrição]**: (opcional) uma descrição das credenciais geradas.
- **[!UICONTROL Atribuído a]**: o usuário ao qual as credenciais serão atribuídas. Esse valor deve ser o endereço de email do usuário que está criando as credenciais.
- **[!UICONTROL Senha]** (Opcional) Uma senha opcional para suas credenciais. Se a senha não for definida, o Adobe gerará automaticamente uma senha para você.

Depois de fornecer todos os detalhes necessários, selecione **[!UICONTROL Gerar credenciais]** para gerar suas credenciais.

![A caixa de diálogo Gerar credenciais é realçada.](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>Quando **[!UICONTROL Gerar credenciais]** for selecionada, um arquivo JSON de configuração será baixado na máquina local. Como o Adobe faz **não** Para registrar as credenciais geradas, você deve armazenar com segurança o arquivo baixado e manter um registro da credencial.
>
>Além disso, se as credenciais não forem usadas por 90 dias, elas serão eliminadas.

O arquivo JSON de configuração contém informações como nome da conta técnica, ID da conta técnica e credencial. Ela é fornecida no formato a seguir.

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

Depois de salvar as credenciais geradas, selecione **[!UICONTROL Fechar]**. Agora você pode ver uma lista de todas as suas credenciais sem expiração.

![A guia Credenciais do painel Consultas com a seção Credenciais sem expiração destacada.](../images/ui/credentials/list-credentials.png)

Você pode editar ou excluir suas credenciais sem expiração. Para editar uma credencial sem expiração, selecione o ícone de lápis (![Um lápis.](../images/ui/credentials/edit-icon.png)). Para excluir uma credencial sem expiração, selecione o ícone excluir (![Um ícone de lixeira.](../images/ui/credentials/delete-icon.png)).

Ao editar uma credencial sem expiração, um modal é exibido. Você pode fornecer os seguintes detalhes para atualizar:

- **[!UICONTROL Nome]**: O nome das credenciais que você está gerando.
- **[!UICONTROL Descrição]**: (opcional) uma descrição das credenciais geradas.
- **[!UICONTROL Atribuído a]**: o usuário ao qual as credenciais serão atribuídas. Esse valor deve ser o endereço de email do usuário que está criando as credenciais.

![A janela para Atualizar a conta.](../images/ui/credentials/update-credentials.png)

Depois de fornecer todos os detalhes necessários, selecione **[!UICONTROL Atualizar conta]** para concluir a atualização das suas credenciais.

## Usar credenciais para se conectar a clientes externos {#use-credential-to-connect}

Você pode usar as credenciais com ou sem expiração para se conectar com clientes externos, como Aqua Data Studio, Looker ou Power BI. O método de entrada dessas credenciais varia de acordo com o cliente externo. Consulte a documentação do cliente externo para obter instruções específicas sobre o uso dessas credenciais.

A imagem indica o local de cada parâmetro encontrado na interface, exceto a senha das credenciais sem expiração. Embora as credenciais sem expiração sejam fornecidas pelos arquivos de configuração JSON, você pode visualizar as credenciais que estão expirando no **Credenciais** na interface do usuário.

![A guia Credenciais do espaço de trabalho de Consultas com a seção Credenciais de Expiração destacada.](../images/ui/credentials/expiring-credentials.png)

A tabela abaixo descreve os parâmetros normalmente necessários para se conectar a clientes externos.

>[!NOTE]
>
>Ao conectar-se a um host usando credenciais sem expiração, ainda é necessário usar todos os parâmetros listados no [!UICONTROL CREDENCIAIS QUE EXPIRAM] exceto a senha e o nome de usuário.
>O formato para inserir seu nome de usuário e senha usa valores separados por dois pontos, como visto neste exemplo `username:{your_username}` e `password:{password_string}`.

| Parâmetro | Descrição | Exemplo |
|---|---|---|
| **Servidor/Host** | O nome do servidor/host ao qual você está se conectando. <ul><li>Esse valor é usado para credenciais que estão ou não expirando e assume a forma de `server.adobe.io`. O valor é encontrado em **[!UICONTROL Host]** no [!UICONTROL CREDENCIAIS QUE EXPIRAM] seção.</ul></li> | `acme.platform.adobe.io` |
| **Porta** | A porta do servidor/host ao qual você está se conectando. <ul><li>Esse valor é usado para credenciais que estão ou não expirando e é encontrado em **[!UICONTROL Porta]** no [!UICONTROL CREDENCIAIS QUE EXPIRAM] seção.</ul></li> | `80` |
| **Banco de dados** | O banco de dados ao qual você está se conectando. <ul><li>Esse valor é usado para credenciais que estão ou não expirando e é encontrado em **[!UICONTROL Banco de dados]** no [!UICONTROL CREDENCIAIS QUE EXPIRAM] seção. </ul></li> | `prod:all` |
| **Nome de usuário** | O nome de usuário do usuário que está se conectando ao cliente externo. <ul><li>Esse valor é usado para credenciais com e sem expiração. Assume a forma de uma sequência alfanumérica antes de `@AdobeOrg`. Esse valor é encontrado em **[!UICONTROL Nome de usuário]**.</li></ul> | `ECBB80245ECFC73E8A095EC9@AdobeOrg` |
| **Senha** | A senha do usuário que está se conectando ao cliente externo. <ul><li>Se você estiver usando credenciais com expiração, isso poderá ser encontrado em **[!UICONTROL Senha]** no prazo de [!UICONTROL CREDENCIAIS QUE EXPIRAM] seção.</li><li>Se você estiver usando credenciais sem expiração, esse valor serão os argumentos concatenados de technicalAccountID e a credencial retirada do arquivo JSON de configuração. O valor da senha tem o formato: `{technicalAccountId}:{credential}`.</li></ul> | <ul><li>Uma senha de credencial que expira tem mais de mil caracteres alfanuméricos. Nenhum exemplo será dado.</li><li>Uma senha de credencial sem expiração é a seguinte:<br>`4F2611B8613DK3670V495N55:3d182fa9e0b54f33a7881305c06203ee`</li></ul> |

{style="table-layout:auto"}

## Próximas etapas

Agora que você entende como as credenciais com e sem expiração funcionam, é possível usá-las para se conectar a clientes externos. Para obter mais informações detalhadas sobre clientes externos, leia o [guia conectar clientes ao Serviço de consulta](../clients/overview.md).
