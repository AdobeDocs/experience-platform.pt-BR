---
title: Definir e configurar chaves gerenciadas pelo cliente usando a API
description: Saiba como configurar seu aplicativo CMK com seu locatário do Azure e enviar sua ID de chave de criptografia para a Adobe Experience Platform.
exl-id: c9a1888e-421f-4bb4-b4c7-968fb1d61746
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 2%

---

# Definir e configurar chaves gerenciadas pelo cliente usando a API

Este documento aborda o processo de ativação do recurso de chaves gerenciadas pelo cliente (CMK) no Adobe Experience Platform usando a API. Para obter instruções sobre como concluir esse processo usando a interface do usuário, consulte [Documento de configuração do CMK da interface](./ui-set-up.md).

## Pré-requisitos

Para visualizar e visitar o [!UICONTROL Criptografia] no Adobe Experience Platform, você deve ter criado uma função e atribuído a [!UICONTROL Gerenciar Chave Gerenciada Pelo Cliente] permissão para essa função. Qualquer usuário que tenha o [!UICONTROL Gerenciar Chave Gerenciada Pelo Cliente] permissão pode habilitar o CMK para sua organização.

Para obter mais informações sobre atribuição de funções e permissões no Experience Platform, consulte o [configurar documentação de permissões](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html?lang=pt-BR).

Para ativar o CMK, seu [[!DNL Azure] O Cofre de Chaves deve ser configurado](./azure-key-vault-config.md) com as seguintes configurações:

* [Habilitar proteção contra limpeza](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Habilitar exclusão reversível](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Configure o acesso usando [!DNL Azure] controle de acesso baseado em função](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [Configurar um [!DNL Azure] Cofre da Chave](./azure-key-vault-config.md)

## Configurar o aplicativo CMK {#register-app}

Depois de configurar o cofre de chaves, a próxima etapa é se registrar para o aplicativo CMK que será vinculado ao seu [!DNL Azure] inquilino.

### Introdução

Para registrar o aplicativo CMK, é necessário fazer chamadas para APIs da plataforma. Para obter detalhes sobre como coletar os cabeçalhos de autenticação necessários para fazer essas chamadas, consulte a [Guia de autenticação da API da plataforma](../../api-authentication.md).

Embora o guia de autenticação forneça instruções sobre como gerar seu próprio valor exclusivo para o `x-api-key` cabeçalho da solicitação, todas as operações da API neste guia usam o valor estático `acp_provisioning` em vez disso. Você ainda deve fornecer seus próprios valores para `{ACCESS_TOKEN}` e `{ORG_ID}`No entanto.

Em todas as chamadas de API mostradas neste guia, `platform.adobe.io` é usado como o caminho raiz, que assume como padrão a região VA7. Se sua organização usar uma região diferente, `platform` deve ser seguido por um traço e o código de região atribuído à organização: `nld2` para NLD2 ou `aus5` para AUS5 (por exemplo: `platform-aus5.adobe.io`). Caso não saiba a região da organização, entre em contato com o administrador do sistema.

### Buscar um URL de autenticação {#fetch-authentication-url}

Para iniciar o processo de registro, faça uma solicitação GET ao endpoint de registro do aplicativo para buscar o URL de autenticação necessário para sua organização.

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/byok/app-registration \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma `applicationRedirectUrl` propriedade, contendo o URL de autenticação.

```json
{
    "id": "byok",
    "name": "acpebae9422Caepcmkmultitenantapp",
    "applicationUri": "https://adobe.com/acpebae9422Caepcmkmultitenantapp",
    "applicationId": "e463a445-c6ac-4ca2-b36a-b5146fcf6a52",
    "applicationRedirectUrl": "https://login.microsoftonline.com/common/oauth2/authorize?response_type=code&client_id=e463a445-c6ac-4ca2-b36a-b5146fcf6a52&redirect_uri=https://adobe.com/acpebae9422Caepcmkmultitenantapp&scope=user.read"
}
```

Copie e cole o `applicationRedirectUrl` em um navegador para abrir uma caixa de diálogo de autenticação. Selecionar **[!DNL Accept]** para adicionar a entidade de serviço do aplicativo CMK ao seu [!DNL Azure] inquilino.

![Uma caixa de diálogo de solicitação de permissão do Microsoft com [!UICONTROL Aceitar] destacado.](../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

### Atribuir o aplicativo CMK a uma função {#assign-to-role}

Após concluir o processo de autenticação, navegue de volta para a [!DNL Azure] Cofre da Chave e selecione **[!DNL Access control]** no painel de navegação esquerdo. Aqui, selecione **[!DNL Add]** seguido por **[!DNL Add role assignment]**.

![O painel do Microsoft Azure com [!DNL Add] e [!DNL Add role assignment] destacado.](../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

A próxima tela solicita que você escolha uma função para esta atribuição. Selecionar **[!DNL Key Vault Crypto Service Encryption User]** antes de selecionar **[!DNL Next]** para continuar.

![O painel do Microsoft Azure com o [!DNL Key Vault Crypto Service Encryption User] destacado.](../../images/governance-privacy-security/customer-managed-keys/select-role.png)

Na próxima tela, escolha **[!DNL Select members]** para abrir um diálogo no painel direito. Use a barra de pesquisa para localizar a entidade de serviço para a aplicação CMK e selecione-a na lista. Quando terminar, selecione **[!DNL Save]**.

>[!NOTE]
>
>Se você não conseguir encontrar seu aplicativo na lista, seu principal de serviço não foi aceito no locatário. Para garantir que você tenha os privilégios corretos, trabalhe com o seu [!DNL Azure] administrador ou representante.

## Habilitar a configuração da chave de criptografia no Experience Platform {#send-to-adobe}

Após instalar o aplicativo CMK no [!DNL Azure], você pode enviar o identificador da chave de criptografia para o Adobe. Selecionar **[!DNL Keys]** na navegação à esquerda, seguido pelo nome da chave que você deseja enviar.

![O painel do Microsoft Azure com o [!DNL Keys] e o nome da chave destacado.](../../images/governance-privacy-security/customer-managed-keys/select-key.png)

Selecione a versão mais recente da chave e sua página de detalhes será exibida. Aqui, você pode configurar opcionalmente as operações permitidas para a chave.

>[!IMPORTANT]
>
>As operações mínimas necessárias a serem permitidas para a chave são **[!DNL Wrap Key]** e **[!DNL Unwrap Key]** permissões. É possível incluir [!DNL Encrypt], [!DNL Decrypt], [!DNL Sign], e [!DNL Verify] Se você quiser.

A variável **[!UICONTROL Identificador de chave]** exibe o identificador URI da chave. Copie este valor de URI para usar na próxima etapa.

![Os detalhes da Chave do painel do Microsoft Azure com a [!DNL Permitted operations] e as seções de copiar URL principal realçadas.](../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

Depois de obter o URI do cofre de chaves, você pode enviá-lo usando uma solicitação POST para o endpoint de configuração do CMK.

>[!NOTE]
>
>Somente o cofre de chaves e o nome da chave são armazenados com o Adobe, não com a versão da chave.

**Solicitação**

+++ Um exemplo de solicitação para enviar o URI do cofre de chaves para o ponto de extremidade de configuração do CMK.

```shell
curl -X POST \
  https://platform.adobe.io/data/infrastructure/manager/customer/config \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
        "name": "Config1",
        "type": "BYOK_CONFIG",
        "imsOrgId": "{ORG_ID}",
        "configData": {
          "providerType": "AZURE_KEYVAULT",
          "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4"
        }
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | Um nome para a configuração. Lembre-se desse valor, pois ele é necessário para verificar o status da configuração em um [etapa posterior](#check-status). O valor diferencia maiúsculas e minúsculas. |
| `type` | O tipo de configuração. Deve ser definido como `BYOK_CONFIG`. |
| `imsOrgId` | Sua ID de organização. Essa ID deve ter o mesmo valor fornecido em `x-gw-ims-org-id` cabeçalho. |
| `configData` | Essa propriedade contém os seguintes detalhes sobre a configuração:<ul><li>`providerType`: Deve ser definido como `AZURE_KEYVAULT`.</li><li>`keyVaultKeyIdentifier`: o URI do cofre de chaves que você copiou [anterior](#send-to-adobe).</li></ul> |

+++

**Resposta**

+++ A resposta bem-sucedida retorna os detalhes do trabalho de configuração.

```json
{
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "config": {
    "configData": {
      "keyVaultUri": "https://adobecmkexample.vault.azure.net",
      "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4",
      "keyVersion": "7c1d50lo28234cc895534c00d7eb4eb4",
      "keyName": "Config1",
      "providerType": "AZURE_KEYVAULT"
    },
    "name": "acpcf978863Aaepcmkmultitenantapp",
    "type": "BYOK_CONFIG",
    "imsOrgId": "{ORG_ID}",
    "status": "NEW"
  },
  "status": "CREATED"
}
```

+++

O processo deve ser concluído em alguns minutos.

## Verificar o status da configuração {#check-status}

Para verificar o status da solicitação de configuração, faça uma solicitação GET.

**Solicitação**

Você deve anexar o `name` da configuração que você deseja verificar para o caminho (`config1` no exemplo abaixo) e inclua um `configType` parâmetro de consulta definido como `BYOK_CONFIG`.

+++ Um exemplo de solicitação para verificar o status da solicitação de configuração.

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/customer/config/config1?configType=BYOK_CONFIG \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

+++

**Resposta**

+++ A resposta bem-sucedida retorna o status do processo.

```json
{
  "name": "acpcf978863Aaepcmkmultitenantapp",
  "type": "BYOK_CONFIG",
  "status": "COMPLETED",
  "configData": {
    "keyVaultUri": "https://adobecmkexample.vault.azure.net",
    "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4",
    "keyVersion": "7c1d50lo28234cc895534c00d7eb4eb4",
    "keyName": "Config1",
    "providerType": "AZURE_KEYVAULT"
  },
  "imsOrgId": "{ORG_ID}",
  "subscriptionId": "cf978863-7325-47b1-8fd9-554b9fdb6c36",
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "rowType": "BYOK_KEY"
}
```

+++

A variável `status` O atributo pode ter um dos quatro valores com os seguintes significados:

1. `RUNNING`: valida se a Platform pode acessar o cofre de chaves e chaves.
1. `UPDATE_EXISTING_RESOURCES`: o sistema está adicionando o cofre de chaves e o nome da chave aos armazenamentos de dados em todas as sandboxes da organização.
1. `COMPLETED`: o cofre de chaves e o nome da chave foram adicionados com êxito aos armazenamentos de dados.
1. `FAILED`: ocorreu um problema, relacionado principalmente à chave, cofre de chaves ou configuração de aplicativo de vários locatários.

## Próximas etapas

Ao concluir as etapas acima, você ativou o CMK com êxito para sua organização. Os dados assimilados nos armazenamentos de dados principais agora serão criptografados e descriptografados usando as chaves na [!DNL Azure] Cofre da Chave. Para saber mais sobre a criptografia de dados na Adobe Experience Platform, consulte a [documentação de criptografia](../encryption.md).
