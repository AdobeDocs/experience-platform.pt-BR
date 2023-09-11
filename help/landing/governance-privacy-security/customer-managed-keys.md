---
title: Chaves gerenciadas pelo cliente no Adobe Experience Platform
description: Saiba como configurar suas próprias chaves de criptografia para dados armazenados no Adobe Experience Platform.
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: 2564c0cc817362536f1a8291e1c733d9efbf5a78
workflow-type: tm+mt
source-wordcount: '1855'
ht-degree: 1%

---

# Chaves gerenciadas pelo cliente no Adobe Experience Platform

Os dados armazenados no Adobe Experience Platform são criptografados em repouso usando chaves de nível de sistema. Se você estiver usando um aplicativo criado sobre a Platform, poderá optar por usar suas próprias chaves de criptografia, fornecendo maior controle sobre a segurança dos dados.

>[!NOTE]
>
>Os dados no data lake da Adobe Experience Platform e no Armazenamento de perfis são criptografados usando CMK. Eles são considerados seus principais armazenamentos de dados.

Este documento aborda o processo de ativação do recurso de chaves gerenciadas pelo cliente (CMK) na Platform.

## Pré-requisitos

Para acessar as APIs CMK, você deve atribuir a variável [!UICONTROL Gerenciar Chave Gerenciada Pelo Cliente] permissão e acesso a uma sandbox de produção para uma função nova ou existente associada à credencial da API. Se você quiser fornecer essa credencial de API com acesso apenas a CMK, é recomendável criar uma nova função de Administrador de CMK com as permissões necessárias mencionadas anteriormente.

Para obter mais informações sobre atribuição de funções e permissões no Experience Platform, consulte o [configurar documentação de permissões](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

Para habilitar o CMK, seu [!DNL Azure] O Cofre da Chave deve ser configurado com as seguintes configurações:

* [Habilitar proteção contra limpeza](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Habilitar exclusão reversível](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Configure o acesso usando [!DNL Azure] controle de acesso baseado em função](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

## Resumo do processo

A CMK está incluída nas ofertas Healthcare Shield e Privacy and Security Shield da Adobe. Depois que sua organização comprar uma licença para uma dessas ofertas, você poderá iniciar um processo único para configurar o recurso.

>[!WARNING]
>
>Após configurar o CMK, não é possível reverter para chaves gerenciadas pelo sistema. Você é responsável por gerenciar com segurança suas chaves e fornecer acesso ao Cofre da chave, Chave e aplicativo CMK no [!DNL Azure] para evitar a perda de acesso aos seus dados.

O processo é o seguinte:

1. [Configurar um [!DNL Azure] Cofre da Chave](#create-key-vault) com base nas políticas de sua organização, em seguida [gerar uma chave de criptografia](#generate-a-key) que será compartilhado com o Adobe.
1. Use chamadas de API para [configurar o aplicativo CMK](#register-app) com o seu [!DNL Azure] inquilino.
1. Use chamadas de API para [enviar a ID da chave de criptografia para o Adobe](#send-to-adobe) e inicie o processo de ativação do recurso.
1. [Verificar o status da configuração](#check-status) para verificar se o CMK foi ativado.

Quando o processo de configuração estiver concluído, todos os dados integrados na Platform em todas as sandboxes serão criptografados usando o [!DNL Azure] configuração de chave. Para usar CMK, você aproveitará [!DNL Microsoft Azure] funcionalidade que pode fazer parte do seu [programa de visualização pública](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/).

## Configurar um [!DNL Azure] Cofre da Chave {#create-key-vault}

O CMK suporta apenas chaves de um [!DNL Microsoft Azure] Cofre da Chave. Para começar, você deve trabalhar com o [!DNL Azure] para criar uma nova conta corporativa ou usar uma conta corporativa existente, siga as etapas abaixo para criar o Cofre da Chave.

>[!IMPORTANT]
>
>Somente os níveis de serviço Premium e Standard para [!DNL Azure] O Cofre de Chaves é compatível. [!DNL Azure Managed HSM], [!DNL Azure Dedicated HSM] e [!DNL Azure Payments HSM] não são compatíveis. Consulte a [[!DNL Azure] documentação](https://learn.microsoft.com/en-us/azure/security/fundamentals/key-management#azure-key-management-services) para obter mais informações sobre os principais serviços de gerenciamento oferecidos.

>[!NOTE]
>
>A documentação abaixo cobre apenas as etapas básicas para criar o cofre de chaves. Fora dessa orientação, você deve configurar o cofre de chaves de acordo com as políticas da organização.

Faça logon no [!DNL Azure] portal e use a barra de pesquisa para localizar **[!DNL Key vaults]** na lista de serviços.

![Pesquisar e selecionar cofres de chaves](../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

A variável **[!DNL Key vaults]** será exibida após selecionar o serviço. Aqui, selecione **[!DNL Create]**.

![Criar cofre de chaves](../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

Usando o formulário fornecido, preencha os detalhes básicos do cofre de chaves, incluindo um nome e um grupo de recursos atribuído.

>[!WARNING]
>
>Embora a maioria das opções possa ser deixada como seus valores padrão, **certifique-se de ativar as opções de exclusão reversível e de proteção de limpeza**. Se você não ativar esses recursos, poderá correr o risco de perder o acesso aos dados se o cofre de chaves for excluído.
>
>![Habilitar proteção contra limpeza](../images/governance-privacy-security/customer-managed-keys/basic-config.png)

A partir daqui, continue percorrendo o fluxo de trabalho de criação do cofre de chaves e configure as diferentes opções de acordo com as políticas da organização.

Uma vez que você chegar ao **[!DNL Review + create]** etapa, você pode revisar os detalhes do cofre de chaves enquanto ele passa pela validação. Depois que a validação for aprovada, selecione **[!DNL Create]** para concluir o processo.

![Configuração básica para o cofre de chaves](../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

### Configurar opções de rede

Se o cofre de chaves estiver configurado para restringir o acesso público a determinadas redes virtuais ou desabilitar totalmente o acesso público, conceda à Microsoft uma exceção de firewall.

Selecionar **[!DNL Networking]** no painel de navegação esquerdo. Em **[!DNL Firewalls and virtual networks]**, marque a caixa de seleção **[!DNL Allow trusted Microsoft services to bypass this firewall]** e selecione **[!DNL Apply]**.

![Configuração básica para o cofre de chaves](../images/governance-privacy-security/customer-managed-keys/networking.png)

### Gerar uma chave {#generate-a-key}

Depois de criar um cofre de chaves, você pode gerar uma nova chave. Navegue até a **[!DNL Keys]** e selecione **[!DNL Generate/Import]**.

![Gerar uma chave](../images/governance-privacy-security/customer-managed-keys/view-keys.png)

Use o formulário fornecido para fornecer um nome para a chave e selecione **RSA** para o tipo de chave. No mínimo, a variável **[!DNL RSA key size]** deve ser pelo menos **3072** bits conforme exigido pelo [!DNL Cosmos DB]. [!DNL Azure Data Lake Storage] também é compatível com o RSA 3027.

>[!NOTE]
>
>Lembre-se do nome fornecido para a chave, pois ele será usado na etapa posterior quando [envio da chave para o Adobe](#send-to-adobe).

Use os controles restantes para configurar a chave que deseja gerar ou importar conforme desejado. Quando terminar, selecione **[!DNL Create]**.

![Configurar chave](../images/governance-privacy-security/customer-managed-keys/configure-key.png)

A chave configurada é exibida na lista de chaves do Vault.

![Chave adicionada](../images/governance-privacy-security/customer-managed-keys/key-added.png)

## Configurar o aplicativo CMK {#register-app}

Depois de configurar o cofre de chaves, a próxima etapa é se registrar para o aplicativo CMK que será vinculado ao seu [!DNL Azure] inquilino.

### Introdução

Para registrar o aplicativo CMK, é necessário fazer chamadas para APIs da plataforma. Para obter detalhes sobre como coletar os cabeçalhos de autenticação necessários para fazer essas chamadas, consulte a [Guia de autenticação da API da plataforma](../../landing/api-authentication.md).

Embora o guia de autenticação forneça instruções sobre como gerar seu próprio valor exclusivo para o `x-api-key` cabeçalho da solicitação, todas as operações da API neste guia usam o valor estático `acp_provisioning` em vez disso. Você ainda deve fornecer seus próprios valores para `{ACCESS_TOKEN}` e `{ORG_ID}`No entanto.

Em todas as chamadas de API mostradas neste guia, `platform.adobe.io` é usado como o caminho raiz, que assume como padrão a região VA7. Se sua organização usar uma região diferente, `platform` deve ser seguido por um traço e o código de região atribuído à organização: `nld2` para NLD2 ou `aus5` para AUS5 (por exemplo: `platform-aus5.adobe.io`). Se você não souber a região de sua organização, entre em contato com o administrador do sistema.

### Buscar um URL de autenticação

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

![Aceitar solicitação de permissão](../images/governance-privacy-security/customer-managed-keys/app-permission.png)

### Atribuir o aplicativo CMK a uma função {#assign-to-role}

Após concluir o processo de autenticação, navegue de volta para a [!DNL Azure] Cofre da Chave e selecione **[!DNL Access control]** no painel de navegação esquerdo. Aqui, selecione **[!DNL Add]** seguido por **[!DNL Add role assignment]**.

![Adicionar atribuição de função](../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

A próxima tela solicita que você escolha uma função para esta atribuição. Selecionar **[!DNL Key Vault Crypto Service Encryption User]** antes de selecionar **[!DNL Next]** para continuar.

![Selecionar função](../images/governance-privacy-security/customer-managed-keys/select-role.png)

Na próxima tela, escolha **[!DNL Select members]** para abrir um diálogo no painel direito. Use a barra de pesquisa para localizar a entidade de serviço para a aplicação CMK e selecione-a na lista. Quando terminar, selecione **[!DNL Save]**.

>[!NOTE]
>
>Se você não conseguir encontrar seu aplicativo na lista, seu principal de serviço não foi aceito no locatário. Trabalhe com o seu [!DNL Azure] administrador ou representante para garantir que você tenha os privilégios corretos.

## Habilitar a configuração da chave de criptografia no Experience Platform {#send-to-adobe}

Após instalar o aplicativo CMK no [!DNL Azure], você pode enviar o identificador da chave de criptografia para o Adobe. Selecionar **[!DNL Keys]** na navegação à esquerda, seguido pelo nome da chave que você deseja enviar.

![Selecionar chave](../images/governance-privacy-security/customer-managed-keys/select-key.png)

Selecione a versão mais recente da chave e sua página de detalhes será exibida. Aqui você pode configurar opcionalmente as operações permitidas para a chave. No mínimo, a chave deve receber a permissão **[!DNL Wrap Key]** e **[!DNL Unwrap Key]** permissões.

A variável **[!UICONTROL Identificador de chave]** exibe o identificador URI da chave. Copie este valor de URI para usar na próxima etapa.

![Copiar URL da chave](../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

Depois de obter o URI do cofre de chaves, você pode enviá-lo usando uma solicitação POST para o endpoint de configuração do CMK.

>[!NOTE]
>
>Somente o cofre de chaves e o nome da chave são armazenados com o Adobe, não com a versão da chave.

**Solicitação**

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
| `name` | Um nome para a configuração. Lembre-se desse valor, pois ele será necessário para verificar o status da configuração em um [etapa posterior](#check-status). O valor diferencia maiúsculas e minúsculas. |
| `type` | O tipo de configuração. Deve ser definido como `BYOK_CONFIG`. |
| `imsOrgId` | Sua ID de organização. Deve ser o mesmo valor fornecido na variável `x-gw-ims-org-id` cabeçalho. |
| `configData` | Contém os seguintes detalhes sobre a configuração:<ul><li>`providerType`: Deve ser definido como `AZURE_KEYVAULT`.</li><li>`keyVaultKeyIdentifier`: o URI do cofre de chaves que você copiou [anterior](#send-to-adobe).</li></ul> |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do trabalho de configuração.

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
    "imsOrgId": "{IMS_ORG}",
    "status": "NEW"
  },
  "status": "CREATED"
}
```

O processo deve ser concluído em alguns minutos.

## Verificar o status da configuração {#check-status}

Para verificar o status da solicitação de configuração, faça uma solicitação GET.

**Solicitação**

Você deve anexar o `name` da configuração que você deseja verificar para o caminho (`config1` no exemplo abaixo) e inclua um `configType` parâmetro de consulta definido como `BYOK_CONFIG`.

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/customer/config/config1?configType=BYOK_CONFIG \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status do processo.

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
  "imsOrgId": "{IMS_ORG}",
  "subscriptionId": "cf978863-7325-47b1-8fd9-554b9fdb6c36",
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "rowType": "BYOK_KEY"
}
```

A variável `status` O atributo pode ter um dos quatro valores com os seguintes significados:

1. `RUNNING`: valida se o Platform tem a capacidade de acessar o cofre de chaves e chaves.
1. `UPDATE_EXISTING_RESOURCES`: o sistema está adicionando o cofre de chaves e o nome da chave aos armazenamentos de dados em todas as sandboxes da organização.
1. `COMPLETED`: o cofre de chaves e o nome da chave foram adicionados aos armazenamentos de dados.
1. `FAILED`: ocorreu um problema, relacionado principalmente à chave, cofre de chaves ou configuração de aplicativo de vários locatários.

## Revogar acesso {#revoke-access}

Se quiser revogar o acesso do Platform aos seus dados, você poderá remover a função de usuário associada à aplicação do cofre de chaves no [!DNL Azure].

>[!WARNING]
>
>Desabilitar o cofre de chaves, a Chave ou o aplicativo CMK pode resultar em uma mudança radical. Quando o cofre de chaves, a chave ou o aplicativo CMK estiverem desativados e os dados não estiverem mais acessíveis na Platform, nenhuma operação downstream relacionada a esses dados será mais possível. Certifique-se de entender os impactos de downstream da revogação do acesso da Platform à sua chave antes de fazer alterações na configuração.

Após remover o acesso à chave ou desabilitar/excluir a chave do [!DNL Azure] cofre de chaves, pode levar de alguns minutos a 24 horas para que essa configuração se propague para os armazenamentos de dados principais. Os fluxos de trabalho da plataforma também incluem armazenamentos de dados em cache e transitórios, necessários para o desempenho e a funcionalidade principal do aplicativo. A propagação da revogação de CMK por meio desses armazenamentos em cache e transitórios pode levar até sete dias, conforme determinado por seus workflows de processamento de dados. Por exemplo, isso significa que o painel Perfil manteria e exibiria dados de seu armazenamento de dados em cache e levaria sete dias para expirar os dados mantidos nos armazenamentos de dados em cache como parte do ciclo de atualização. O mesmo atraso se aplica para que os dados fiquem disponíveis novamente ao reativar o acesso ao aplicativo.

>[!NOTE]
>
>Há duas exceções específicas de caso de uso para a expiração do conjunto de dados de sete dias em dados não primários (em cache/transitórios). Consulte a respectiva documentação para obter mais informações sobre esses recursos.<ul><li>[Encurtador de URL do Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=pt-BR#message-preset-sms)</li><li>[Projeções de borda](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## Próximas etapas

Ao concluir as etapas acima, você ativou o CMK com êxito para sua organização. Os dados assimilados nos armazenamentos de dados principais agora serão criptografados e descriptografados usando as chaves na [!DNL Azure] Cofre da Chave.

