---
title: Definir e configurar chaves gerenciadas pelo cliente usando a interface do usuário da plataforma
description: Saiba como configurar seu aplicativo CMK com seu locatário do Azure e enviar sua ID de chave de criptografia para a Adobe Experience Platform.
source-git-commit: a0df05cde19e97d4abdad7abd19eafea8efe1096
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 0%

---

# Definir e configurar chaves gerenciadas pelo cliente usando a interface do usuário da plataforma

Este documento aborda o processo de ativação do recurso de chaves gerenciadas pelo cliente (CMK) na Platform usando a interface do usuário. Para obter instruções sobre como concluir esse processo usando a API, consulte o [Documento de configuração da API CMK](./api-set-up.md).

## Pré-requisitos

Para visualizar e visitar o [!UICONTROL Criptografia] no Adobe Experience Platform, você deve ter criado uma função e atribuído a [!UICONTROL Gerenciar Chave Gerenciada Pelo Cliente] permissão para essa função. Qualquer usuário que tenha o [!UICONTROL Gerenciar Chave Gerenciada Pelo Cliente] permissão pode habilitar o CMK para sua organização.

Para obter mais informações sobre atribuição de funções e permissões no Experience Platform, consulte o [configurar documentação de permissões](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

Para ativar o CMK, seu [[!DNL Azure] O Cofre de Chaves deve ser configurado](./azure-key-vault-config.md) com as seguintes configurações:

* [Habilitar proteção contra limpeza](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Habilitar exclusão reversível](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Configure o acesso usando [!DNL Azure] controle de acesso baseado em função](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [Configurar um [!DNL Azure] Cofre da Chave](./azure-key-vault-config.md)

## Configurar o aplicativo CMK {#register-app}

Depois de configurar o cofre de chaves, a próxima etapa é registrar o aplicativo CMK que será vinculado ao seu [!DNL Azure] inquilino.

### Introdução

Para exibir as [!UICONTROL Configurações de criptografia] painel, selecione **[!UICONTROL Criptografia]** no [!UICONTROL Administração] cabeçalho da barra lateral de navegação à esquerda.

![O painel de configuração Criptografia com Criptografia e o cartão Chaves gerenciadas pelo cliente destacados.](../../images/governance-privacy-security/customer-managed-keys/encryption-configraion.png)

Selecionar **[!UICONTROL Configurar]** para abrir o [!UICONTROL Configuração de chaves gerenciadas pelo cliente] exibição. Este espaço de trabalho contém todos os valores necessários para concluir as etapas descritas abaixo e executar a integração com seu Cofre de Chaves do Azure.

### Copiar URL de autenticação {#copy-authentication-url}

Para iniciar o processo de registro, copie do site [!UICONTROL Configuração de chaves gerenciadas pelo cliente] visualize e cole no seu [!DNL Azure] ambiente **[!DNL Key Vault Crypto Service Encryption User]**. Detalhes sobre como [atribuir uma função](#assign-to-role) são apresentados na próxima seção.

Selecione o ícone de cópia (![O ícone de cópia.](../../images/governance-privacy-security/customer-managed-keys/copy-icon.png)) pela [!UICONTROL URL de autenticação do aplicativo].

![A variável [!UICONTROL Configuração de chaves gerenciadas pelo cliente] visualização com a seção Application authentication url realçada.](../../images/governance-privacy-security/customer-managed-keys/application-authentication-url.png)

Copie e cole o [!UICONTROL URL de autenticação do aplicativo] em um navegador para abrir uma caixa de diálogo de autenticação. Selecionar **[!DNL Accept]** para adicionar a entidade de serviço do aplicativo CMK ao seu [!DNL Azure] inquilino. A confirmação da autenticação o redireciona para a página de aterrissagem do Experience Cloud.

![Uma caixa de diálogo de solicitação de permissão do Microsoft com [!UICONTROL Aceitar] destacado.](../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

>[!IMPORTANT]
>
>Se você tiver vários [!DNL Microsoft Azure] assinaturas, você poderá conectar sua instância do Platform ao cofre de chaves errado. Nessa situação, você deve trocar a variável `common` seção do nome do URL de autenticação de aplicativo para a ID do diretório CMK.<br>Copie a ID do diretório CMK da página Configurações do portal, Diretórios e assinaturas do [!DNL Microsoft Azure] aplicativo<br>![A variável [!DNL Microsoft Azure] Configurações do Portal da aplicação, diretórios e páginas de assinaturas com a ID do diretório realçada.](../../images/governance-privacy-security/customer-managed-keys/directory-id.png)<br>Em seguida, cole-o na barra de endereços do navegador.<br>![Uma página do navegador Google com a seção &quot;comum&quot; do URL de autenticação do aplicativo destacada.](../../images/governance-privacy-security/customer-managed-keys/common-url-section.png)

### Atribuir o aplicativo CMK a uma função {#assign-to-role}

Após concluir o processo de autenticação, navegue de volta para a [!DNL Azure] Cofre da Chave e selecione **[!DNL Access control]** no painel de navegação esquerdo. Aqui, selecione **[!DNL Add]** seguido por **[!DNL Add role assignment]**.

![A variável [!DNL Microsoft Azure] painel com [!DNL Add] e [!DNL Add role assignment] destacado.](../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

A próxima tela solicita que você escolha uma função para esta atribuição. Selecionar **[!DNL Key Vault Crypto Service Encryption User]** antes de selecionar **[!DNL Next]** para continuar.

![A variável [!DNL Microsoft Azure] painel com o [!DNL Key Vault Crypto Service Encryption User] destacado.](../../images/governance-privacy-security/customer-managed-keys/select-role.png)

Na próxima tela, escolha **[!DNL Select members]** para abrir um diálogo no painel direito. Use a barra de pesquisa para localizar a entidade de serviço para a aplicação CMK e selecione-a na lista. Quando terminar, selecione **[!DNL Save]**.

>[!NOTE]
>
>Se você não conseguir encontrar seu aplicativo na lista, seu principal de serviço não foi aceito no locatário. Para garantir que você tenha os privilégios corretos, trabalhe com o seu [!DNL Azure] administrador ou representante.

Você pode verificar o aplicativo comparando o [!UICONTROL ID do aplicativo] fornecido no [!UICONTROL Configuração de chaves gerenciadas pelo cliente] exibir com o [!DNL Application ID] fornecido no [!DNL Microsoft Azure] visão geral do aplicativo.

![A variável [!UICONTROL Configuração de chaves gerenciadas pelo cliente] exibir com o [!UICONTROL ID do aplicativo] destacado.](../../images/governance-privacy-security/customer-managed-keys/application-id.png)

Todos os detalhes necessários para verificar as ferramentas do Azure estão incluídos na interface do usuário da plataforma. Esse nível de granularidade é fornecido quando muitos usuários desejam usar outras ferramentas do Azure para aprimorar sua capacidade de monitorar e registrar esses aplicativos no acesso ao cofre de chaves. Entender esses identificadores é essencial para essa finalidade e para ajudar os serviços da Adobe a acessar a chave.

## Habilitar a configuração da chave de criptografia no Experience Platform {#send-to-adobe}

Após instalar o aplicativo CMK no [!DNL Azure], você pode enviar o identificador da chave de criptografia para o Adobe. Selecionar **[!DNL Keys]** na navegação à esquerda, seguido pelo nome da chave que você deseja enviar.

![O painel do Microsoft Azure com o [!DNL Keys] e o nome da chave destacado.](../../images/governance-privacy-security/customer-managed-keys/select-key.png)

Selecione a versão mais recente da chave e sua página de detalhes será exibida. Aqui, você pode configurar opcionalmente as operações permitidas para a chave.

>[!IMPORTANT]
>
>As operações mínimas necessárias a serem permitidas para a chave são **[!DNL Wrap Key]** e **[!DNL Unwrap Key]** permissões. É possível incluir [!DNL Encrypt], [!DNL Decrypt], [!DNL Sign], e [!DNL Verify] Se você quiser.

A variável **[!UICONTROL Identificador de chave]** exibe o identificador URI da chave. Copie este valor de URI para usar na próxima etapa.

![Os detalhes da Chave do painel do Microsoft Azure com a [!DNL Permitted operations] e as seções de copiar URL principal realçadas.](../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

Depois de obter o [!DNL Key vault URI], retorne à guia [!UICONTROL Configuração de chaves gerenciadas pelo cliente] exibir e inserir um descritivo **[!UICONTROL Nome da configuração]**. Em seguida, adicione o [!DNL Key Identifier] retirada da página Detalhes da chave do Azure para a **[!UICONTROL Identificador de chave do cofre de chaves]** e selecione **[!UICONTROL Salvar]**.

![A variável [!UICONTROL Configuração de chaves gerenciadas pelo cliente] exibir com o [!UICONTROL Nome da configuração] e a variável [!UICONTROL Identificador de chave do cofre de chaves] seções destacadas.](../../images/governance-privacy-security/customer-managed-keys/configuration-name.png)

Você retornará à janela [!UICONTROL Painel de configurações de criptografia]. O status do [!UICONTROL Chaves gerenciadas pelo cliente] A configuração do é exibida como [!UICONTROL Processando].

![A variável [!UICONTROL Configurações de criptografia] painel com [!UICONTROL Processando] destacado na [!UICONTROL Chaves gerenciadas pelo cliente] cartão.](../../images/governance-privacy-security/customer-managed-keys/processing.png)

## Verificar o status da configuração {#check-status}

Permita um tempo significativo para o processamento. Para verificar o status da configuração, volte para a guia [!UICONTROL Configuração de chaves gerenciadas pelo cliente] exibir e rolar para baixo até o [!UICONTROL Status da configuração]. A barra de progresso avançou para a etapa um de três e explica que o sistema está validando se a Platform tem acesso à chave e ao cofre de chaves.

Há quatro status possíveis da configuração do CMK. Elas são as seguintes:

* Etapa 1: valida se a Platform tem a capacidade de acessar o cofre de chaves e chaves.
* Etapa 2: o cofre de chaves e o nome da chave estão sendo adicionados a todos os armazenamentos de dados em sua organização.
* Etapa 3: O cofre de chaves e o nome da chave foram adicionados com êxito aos armazenamentos de dados.
* `FAILED`: ocorreu um problema, relacionado principalmente à chave, cofre de chaves ou configuração de aplicativo de vários locatários.

## Próximas etapas

Ao concluir as etapas acima, você ativou o CMK com êxito para sua organização. Os dados assimilados nos armazenamentos de dados principais agora serão criptografados e descriptografados usando as chaves na [!DNL Azure] Cofre da Chave.
