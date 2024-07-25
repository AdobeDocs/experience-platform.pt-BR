---
title: Definir e configurar chaves gerenciadas pelo cliente usando a interface do usuário da plataforma
description: Saiba como configurar seu aplicativo CMK com seu locatário do Azure e enviar sua ID de chave de criptografia para a Adobe Experience Platform.
exl-id: 5f38997a-66f3-4f9d-9c2f-fb70266ec0a6
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1090'
ht-degree: 0%

---

# Definir e configurar chaves gerenciadas pelo cliente usando a interface do usuário da plataforma

Este documento aborda o processo de ativação do recurso de chaves gerenciadas pelo cliente (CMK) na Platform usando a interface do usuário. Para obter instruções sobre como concluir esse processo usando a API, consulte o [documento de configuração do CMK da API](./api-set-up.md).

## Pré-requisitos

Para exibir e visitar a seção [!UICONTROL Criptografia] no Adobe Experience Platform, você deve ter criado uma função e atribuído a permissão [!UICONTROL Gerenciar chave gerenciada pelo cliente] a essa função. Qualquer usuário com a permissão [!UICONTROL Gerenciar Chave gerenciada pelo cliente] pode habilitar o CMK para sua organização.

Para obter mais informações sobre atribuição de funções e permissões no Experience Platform, consulte a [documentação sobre configuração de permissões](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

Para habilitar o CMK, o [[!DNL Azure] Cofre da Chave deve ser configurado](./azure-key-vault-config.md) com as seguintes configurações:

* [Habilitar proteção para limpeza](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Habilitar exclusão reversível](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Configurar acesso usando [!DNL Azure] controle de acesso baseado em função](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [Configurar um  [!DNL Azure] Cofre de Chaves](./azure-key-vault-config.md)

## Configurar o aplicativo CMK {#register-app}

Após configurar o cofre de chaves, a próxima etapa é registrar o aplicativo CMK que será vinculado ao locatário [!DNL Azure].

### Introdução

Para exibir o painel [!UICONTROL Configurações de criptografia], selecione **[!UICONTROL Criptografia]** no cabeçalho [!UICONTROL Administração] da barra lateral de navegação esquerda.

![O painel de configuração de Criptografia com Criptografia e o cartão Chaves Gerenciadas pelo Cliente foram realçados.](../../images/governance-privacy-security/customer-managed-keys/encryption-configraion.png)

Selecione **[!UICONTROL Configurar]** para abrir a exibição [!UICONTROL Chaves gerenciadas pelo cliente]. Este espaço de trabalho contém todos os valores necessários para concluir as etapas descritas abaixo e executar a integração com seu Cofre de Chaves do Azure.

### Copiar URL de autenticação {#copy-authentication-url}

Para iniciar o processo de registro, copie a URL de autenticação de aplicativo da sua organização da exibição [!UICONTROL Configuração de chaves gerenciadas pelo cliente] e cole-a no ambiente [!DNL Azure] **[!DNL Key Vault Crypto Service Encryption User]**. Detalhes sobre como [atribuir uma função](#assign-to-role) são fornecidos na próxima seção.

Selecione o ícone de cópia (![O ícone de cópia.](/help/images/icons/copy.png)) pela [!UICONTROL URL de autenticação do aplicativo].

![A exibição da [!UICONTROL Configuração de Chaves Gerenciadas pelo Cliente] com a seção de URL de autenticação de Aplicativo realçada.](../../images/governance-privacy-security/customer-managed-keys/application-authentication-url.png)

Copie e cole a [!UICONTROL URL de autenticação do aplicativo] em um navegador para abrir uma caixa de diálogo de autenticação. Selecione **[!DNL Accept]** para adicionar a entidade de serviço do aplicativo CMK ao locatário [!DNL Azure]. A confirmação da autenticação o redireciona para a página de aterrissagem do Experience Cloud.

![Uma caixa de diálogo de solicitação de permissão do Microsoft com [!UICONTROL Aceitar] realçada.](../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

>[!IMPORTANT]
>
>Se você tiver várias assinaturas [!DNL Microsoft Azure], poderá conectar sua instância do Platform ao cofre de chaves incorreto. Nessa situação, você deve trocar a seção `common` do nome da URL de autenticação do aplicativo pela ID do diretório CMK.<br>Copie a ID do diretório CMK da página Configurações do Portal, Diretórios e Assinaturas do aplicativo [!DNL Microsoft Azure]<br>![A página [!DNL Microsoft Azure] configurações do Portal do aplicativo, Diretórios e Assinaturas com a ID do Diretório realçada.](../../images/governance-privacy-security/customer-managed-keys/directory-id.png)<br>Em seguida, cole-o na barra de endereços do navegador.<br>![Uma página do navegador Google com a seção &#39;comum&#39; da URL de autenticação de Aplicativo realçada.](../../images/governance-privacy-security/customer-managed-keys/common-url-section.png)

### Atribuir o aplicativo CMK a uma função {#assign-to-role}

Após concluir o processo de autenticação, volte para o Cofre da Chave do [!DNL Azure] e selecione **[!DNL Access control]** na navegação à esquerda. Aqui, selecione **[!DNL Add]** seguido por **[!DNL Add role assignment]**.

![O painel [!DNL Microsoft Azure] com [!DNL Add] e [!DNL Add role assignment] realçados.](../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

A próxima tela solicita que você escolha uma função para esta atribuição. Selecione **[!DNL Key Vault Crypto Service Encryption User]** antes de selecionar **[!DNL Next]** para continuar.

>[!NOTE]
>
>Se você tiver a camada [!DNL Managed-HSM Key Vault], deverá selecionar a função de usuário **[!DNL Managed HSM Crypto Service Encryption User]**.

![O painel [!DNL Microsoft Azure] com o [!DNL Key Vault Crypto Service Encryption User] realçado.](../../images/governance-privacy-security/customer-managed-keys/select-role.png)

Na próxima tela, escolha **[!DNL Select members]** para abrir uma caixa de diálogo no painel direito. Use a barra de pesquisa para localizar a entidade de serviço para a aplicação CMK e selecione-a na lista. Quando terminar, selecione **[!DNL Save]**.

>[!NOTE]
>
>Se você não conseguir encontrar seu aplicativo na lista, seu principal de serviço não foi aceito no locatário. Para garantir que você tenha os privilégios corretos, fale com o administrador ou representante do [!DNL Azure].

Você pode verificar o aplicativo comparando a exibição [!UICONTROL ID do Aplicativo] fornecida na [!UICONTROL configuração de Chaves Gerenciadas pelo Cliente] com a [!DNL Application ID] fornecida na visão geral do aplicativo [!DNL Microsoft Azure].

![A exibição da [!UICONTROL Configuração de Chaves Gerenciadas pelo Cliente] com a [!UICONTROL ID do Aplicativo] realçada.](../../images/governance-privacy-security/customer-managed-keys/application-id.png)

Todos os detalhes necessários para verificar as ferramentas do Azure estão incluídos na interface do usuário da plataforma. Esse nível de granularidade é fornecido quando muitos usuários desejam usar outras ferramentas do Azure para aprimorar sua capacidade de monitorar e registrar esses aplicativos no acesso ao cofre de chaves. Entender esses identificadores é essencial para essa finalidade e para ajudar os serviços da Adobe a acessar a chave.

## Habilitar a configuração da chave de criptografia no Experience Platform {#send-to-adobe}

Depois de instalar o aplicativo CMK em [!DNL Azure], você pode enviar o identificador de chave de criptografia para o Adobe. Selecione **[!DNL Keys]** na navegação à esquerda, seguido pelo nome da chave que você deseja enviar.

![O painel do Microsoft Azure com o objeto [!DNL Keys] e o nome da chave realçados.](../../images/governance-privacy-security/customer-managed-keys/select-key.png)

Selecione a versão mais recente da chave e sua página de detalhes será exibida. Aqui, você pode configurar opcionalmente as operações permitidas para a chave.

>[!IMPORTANT]
>
>As operações mínimas necessárias a serem permitidas para a chave são as permissões **[!DNL Wrap Key]** e **[!DNL Unwrap Key]**. Você pode incluir [!DNL Encrypt], [!DNL Decrypt], [!DNL Sign] e [!DNL Verify] conforme desejar.

O campo **[!UICONTROL Identificador de Chave]** exibe o identificador de URI para a chave. Copie este valor de URI para usar na próxima etapa.

![Os detalhes da Chave do painel do Microsoft Azure com as seções [!DNL Permitted operations] e copiar URL da chave destacadas.](../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

Depois de obter o [!DNL Key vault URI], retorne à exibição [!UICONTROL Configuração de chaves gerenciadas pelo cliente] e insira um **[!UICONTROL nome de configuração]** descritivo. Em seguida, adicione a [!DNL Key Identifier] retirada da página de detalhes da Chave do Azure ao **[!UICONTROL Identificador da chave do cofre de chaves]** e selecione **[!UICONTROL Salvar]**.

![A exibição da [!UICONTROL Configuração de chaves gerenciadas pelo cliente] com as seções [!UICONTROL Nome da configuração] e [!UICONTROL Identificador de chave do cofre de chaves] destacadas.](../../images/governance-privacy-security/customer-managed-keys/configuration-name.png)

Você retornou ao [!UICONTROL painel de configurações de criptografia]. O status da configuração [!UICONTROL Chaves gerenciadas pelo cliente] é exibido como [!UICONTROL Processando].

![O painel [!UICONTROL Configurações de criptografia] com [!UICONTROL Processamento] realçado no cartão [!UICONTROL Chaves gerenciadas pelo cliente].](../../images/governance-privacy-security/customer-managed-keys/processing.png)

## Verificar o status da configuração {#check-status}

Permita um tempo significativo para o processamento. Para verificar o status da configuração, retorne à exibição [!UICONTROL Chaves gerenciadas pelo cliente] e role para baixo até o [!UICONTROL Status da configuração]. A barra de progresso avançou para a etapa um de três e explica que o sistema está validando se a Platform tem acesso à chave e ao cofre de chaves.

Há quatro status possíveis da configuração do CMK. Elas são as seguintes:

* Etapa 1: valida se a Platform tem a capacidade de acessar o cofre de chaves e chaves.
* Etapa 2: o cofre de chaves e o nome da chave estão sendo adicionados a todos os armazenamentos de dados em sua organização.
* Etapa 3: O cofre de chaves e o nome da chave foram adicionados com êxito aos armazenamentos de dados.
* `FAILED`: ocorreu um problema, relacionado principalmente à chave, cofre de chaves ou configuração de aplicativo multilocatário.

## Próximas etapas

Ao concluir as etapas acima, você ativou o CMK com êxito para sua organização. Os dados assimilados nos armazenamentos de dados principais agora serão criptografados e descriptografados usando a(s) chave(s) no Cofre da Chave do [!DNL Azure].
