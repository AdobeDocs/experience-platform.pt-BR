---
title: Definir e configurar chaves gerenciadas pelo cliente usando a API
description: Saiba como configurar seu aplicativo CMK com seu locatário do Azure e enviar sua ID de chave de criptografia para a Adobe Experience Platform.
exl-id: c9a1888e-421f-4bb4-b4c7-968fb1d61746
source-git-commit: 4f08e8fcc8d53b981af60226f1397a1d1ac4d8dc
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 1%

---

# Definir e configurar chaves gerenciadas pelo cliente usando a API

Este documento aborda o processo de ativação do recurso de chaves gerenciadas pelo cliente (CMK) no Adobe Experience Platform usando a API. Para obter instruções sobre como concluir esse processo usando a interface do usuário, consulte o [documento de configuração do CMK da interface do usuário](./ui-set-up.md).

## Pré-requisitos

Para exibir e visitar a seção [!UICONTROL Criptografia] no Adobe Experience Platform, você deve ter criado uma função e atribuído a permissão [!UICONTROL Gerenciar chave gerenciada pelo cliente] a essa função. Qualquer usuário com a permissão [!UICONTROL Gerenciar Chave gerenciada pelo cliente] pode habilitar o CMK para sua organização.

Para obter mais informações sobre atribuição de funções e permissões no Experience Platform, consulte a [documentação sobre configuração de permissões](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

Para habilitar o CMK, o [[!DNL Azure] Cofre da Chave deve ser configurado](./azure-key-vault-config.md) com as seguintes configurações:

* [Habilitar proteção para limpeza](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Habilitar exclusão reversível](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Configurar acesso usando [!DNL Azure] controle de acesso baseado em função](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [Configurar um  [!DNL Azure] Cofre de Chaves](./azure-key-vault-config.md)

## Configurar o aplicativo CMK {#register-app}

Após configurar o cofre de chaves, a próxima etapa é se registrar para o aplicativo CMK que será vinculado ao locatário [!DNL Azure].

### Introdução

Para registrar o aplicativo CMK, é necessário fazer chamadas para APIs da plataforma. Para obter detalhes sobre como coletar os cabeçalhos de autenticação necessários para fazer essas chamadas, consulte o [guia de autenticação da API da plataforma](../../api-authentication.md).

Embora o guia de autenticação forneça instruções sobre como gerar seu próprio valor exclusivo para o cabeçalho de solicitação `x-api-key` necessário, todas as operações de API neste guia usam o valor estático `acp_provisioning`. No entanto, você ainda deve fornecer seus próprios valores para `{ACCESS_TOKEN}` e `{ORG_ID}`.

Em todas as chamadas de API mostradas neste guia, `platform.adobe.io` é usado como o caminho raiz, que assume como padrão a região VA7. Se sua organização usar uma região diferente, `platform` deverá ser seguido por um traço e o código de região atribuído a sua organização: `nld2` para NLD2 ou `aus5` para AUS5 (por exemplo: `platform-aus5.adobe.io`). Caso não saiba a região da organização, entre em contato com o administrador do sistema.

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

Uma resposta bem-sucedida retorna uma propriedade `applicationRedirectUrl`, contendo a URL de autenticação.

```json
{
    "id": "byok",
    "name": "acpebae9422Caepcmkmultitenantapp",
    "applicationUri": "https://adobe.com/acpebae9422Caepcmkmultitenantapp",
    "applicationId": "e463a445-c6ac-4ca2-b36a-b5146fcf6a52",
    "applicationRedirectUrl": "https://login.microsoftonline.com/common/oauth2/authorize?response_type=code&client_id=e463a445-c6ac-4ca2-b36a-b5146fcf6a52&redirect_uri=https://adobe.com/acpebae9422Caepcmkmultitenantapp&scope=user.read"
}
```

Copie e cole o endereço `applicationRedirectUrl` em um navegador para abrir uma caixa de diálogo de autenticação. Selecione **[!DNL Accept]** para adicionar a entidade de serviço do aplicativo CMK ao locatário [!DNL Azure].

![Uma caixa de diálogo de solicitação de permissão do Microsoft com [!UICONTROL Aceitar] realçada.](../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

### Atribuir o aplicativo CMK a uma função {#assign-to-role}

Após concluir o processo de autenticação, volte para o Cofre da Chave do [!DNL Azure] e selecione **[!DNL Access control]** na navegação à esquerda. Aqui, selecione **[!DNL Add]** seguido por **[!DNL Add role assignment]**.

![O painel do Microsoft Azure com [!DNL Add] e [!DNL Add role assignment] realçados.](../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

A próxima tela solicita que você escolha uma função para esta atribuição. Selecione **[!DNL Key Vault Crypto Service Encryption User]** antes de selecionar **[!DNL Next]** para continuar.

>[!NOTE]
>
>Se você tiver a camada [!DNL Managed-HSM Key Vault], deverá selecionar a função de usuário **[!DNL Managed HSM Crypto Service Encryption User]**.

![O painel do Microsoft Azure com o [!DNL Key Vault Crypto Service Encryption User] realçado.](../../images/governance-privacy-security/customer-managed-keys/select-role.png)

Na próxima tela, escolha **[!DNL Select members]** para abrir uma caixa de diálogo no painel direito. Use a barra de pesquisa para localizar a entidade de serviço para a aplicação CMK e selecione-a na lista. Quando terminar, selecione **[!DNL Save]**.

>[!NOTE]
>
>Se você não conseguir encontrar seu aplicativo na lista, seu principal de serviço não foi aceito no locatário. Para garantir que você tenha os privilégios corretos, fale com o administrador ou representante do [!DNL Azure].

## Habilitar a configuração da chave de criptografia no Experience Platform {#send-to-adobe}

Depois de instalar o aplicativo CMK em [!DNL Azure], você pode enviar o identificador de chave de criptografia para o Adobe. Selecione **[!DNL Keys]** na navegação à esquerda, seguido pelo nome da chave que você deseja enviar.

![O painel do Microsoft Azure com o objeto [!DNL Keys] e o nome da chave realçados.](../../images/governance-privacy-security/customer-managed-keys/select-key.png)

Selecione a versão mais recente da chave e sua página de detalhes será exibida. Aqui, você pode configurar opcionalmente as operações permitidas para a chave.

>[!IMPORTANT]
>
>As operações mínimas necessárias a serem permitidas para a chave são as permissões **[!DNL Wrap Key]** e **[!DNL Unwrap Key]**. Você pode incluir [!DNL Encrypt], [!DNL Decrypt], [!DNL Sign] e [!DNL Verify] conforme desejar.

O campo **[!UICONTROL Identificador de Chave]** exibe o identificador de URI para a chave. Copie este valor de URI para usar na próxima etapa.

![Os detalhes da Chave do painel do Microsoft Azure com as seções [!DNL Permitted operations] e copiar URL da chave destacadas.](../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

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
| `name` | Um nome para a configuração. Lembre-se desse valor, pois ele é necessário para verificar o status da configuração em uma [etapa posterior](#check-status). O valor diferencia maiúsculas e minúsculas. |
| `type` | O tipo de configuração. Deve ser definido como `BYOK_CONFIG`. |
| `imsOrgId` | Sua ID da organização. Essa ID deve ter o mesmo valor fornecido sob o cabeçalho `x-gw-ims-org-id`. |
| `configData` | Essa propriedade contém os seguintes detalhes sobre a configuração:<ul><li>`providerType`: Deve ser definido como `AZURE_KEYVAULT`.</li><li>`keyVaultKeyIdentifier`: O URI do cofre de chaves que você copiou [anteriormente](#send-to-adobe).</li></ul> |

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

Você deve anexar o `name` da configuração que deseja verificar ao caminho (`config1` no exemplo abaixo) e incluir um parâmetro de consulta `configType` definido como `BYOK_CONFIG`.

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

O atributo `status` pode ter um de quatro valores com os seguintes significados:

1. `RUNNING`: valida se a Platform pode acessar o cofre de chaves e chaves.
1. `UPDATE_EXISTING_RESOURCES`: o sistema está adicionando o cofre de chaves e o nome da chave aos armazenamentos de dados em todas as sandboxes da sua organização.
1. `COMPLETED`: o cofre de chaves e o nome da chave foram adicionados com êxito aos armazenamentos de dados.
1. `FAILED`: ocorreu um problema, relacionado principalmente à chave, cofre de chaves ou configuração de aplicativo multilocatário.

## Próximas etapas

Ao concluir as etapas acima, você ativou o CMK com êxito para sua organização. Os dados assimilados nos armazenamentos de dados principais agora serão criptografados e descriptografados usando a(s) chave(s) no Cofre da Chave do [!DNL Azure]. Para saber mais sobre a criptografia de dados no Adobe Experience Platform, consulte a [documentação sobre criptografia](../encryption.md).
