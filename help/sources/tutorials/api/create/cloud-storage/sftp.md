---
title: Criar uma conexão básica SFTP usando a API do serviço de fluxo
description: Saiba como conectar o Adobe Experience Platform a um servidor SFTP usando a API do serviço de fluxo.
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: f6d1cc811378f2f37968bf0a42b428249e52efd8
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 3%

---

# Crie uma conexão básica SFTP usando o [!DNL Flow Service] API

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Este tutorial guiará você pelas etapas para criar uma conexão básica para [!DNL SFTP] (Protocolo de transferência segura de arquivo) usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Origens](../../../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

>[!IMPORTANT]
>
>É recomendável evitar novas linhas ou retornos de carro ao assimilar objetos JSON com um [!DNL SFTP] conexão de origem. Para contornar a limitação, use um único objeto JSON por linha e use várias linhas para os arquivos subsequentes.

As seções a seguir fornecem as informações adicionais que você precisará saber para se conectar com êxito a um [!DNL SFTP] servidor usando o [!DNL Flow Service] API.

### Coletar credenciais necessárias

A fim de [!DNL Flow Service] para se conectar a [!DNL SFTP], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O nome ou endereço IP associado à [!DNL SFTP] servidor. |
| `port` | A porta do servidor SFTP à qual você está se conectando. Se não fornecido, o valor padrão será `22`. |
| `username` | O nome de usuário com acesso ao seu [!DNL SFTP] servidor. |
| `password` | A senha do [!DNL SFTP] servidor. |
| `privateKeyContent` | O conteúdo da chave privada SSH codificada na Base64. O tipo de chave OpenSSH deve ser classificado como RSA ou DSA. |
| `passPhrase` | A senha para descriptografar a chave privada se o arquivo de chave ou o conteúdo da chave estiver protegido por uma senha. Se a variável `privateKeyContent` estiver protegido por senha, esse parâmetro precisará ser usado com a senha do conteúdo da chave privada como valor. |
| `maxConcurrentConnections` | Esse parâmetro permite especificar um limite máximo para o número de conexões simultâneas que a Platform criará ao se conectar ao servidor SFTP. Você deve definir esse valor como menor que o limite definido pelo SFTP. **Nota**: quando essa configuração estiver ativada para uma conta SFTP existente, ela afetará somente os fluxos de dados futuros, não os existentes. |
| `folderPath` | O caminho para a pasta à qual você deseja fornecer acesso. [!DNL SFTP] fonte, você pode fornecer o caminho da pasta para especificar o acesso do usuário à subpasta de sua escolha. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL SFTP] é: `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual em [introdução às APIs da Platform](../../../../../landing/api-guide.md).

## Crie uma conexão básica

>[!TIP]
>
>Depois de criado, não é possível alterar o tipo de autenticação de um [!DNL SFTP] conexão básica. Para alterar o tipo de autenticação, você deve criar uma nova conexão base.

Uma conexão base retém informações entre sua origem e a Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e sua ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

A variável [!DNL SFTP] A fonte oferece suporte à autenticação básica e à autenticação por meio da chave pública SSH. Durante essa etapa, também é possível designar o caminho para a subpasta à qual você deseja fornecer acesso.

Para criar um ID de conexão base, faça uma solicitação POST ao `/connections` ao fornecer sua [!DNL SFTP] credenciais de autenticação como parte dos parâmetros de solicitação.

>[!IMPORTANT]
>
>A variável [!DNL SFTP] O conector é compatível com uma chave OpenSSH do tipo RSA ou DSA. Verifique se o conteúdo do arquivo principal começa com `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` e termina com `"-----END [RSA/DSA] PRIVATE KEY-----"`. Se o arquivo de chave privada for um arquivo no formato PPK, use a ferramenta PuTTY para converter do formato PPK para o formato OpenSSH.

**Formato da API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Autenticação básica]

+++Solicitação

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d  '{
      "name": "SFTP connector with password",
      "description": "SFTP connector password",
      "auth": {
          "specName": "Basic Authentication for sftp",
          "params": {
              "host": "{HOST}",
              "port": 22,
              "userName": "{USERNAME}",
              "password": "{PASSWORD}",
              "maxConcurrentConnections": 5,
              "folderPath": "acme/business/customers/holidaySales"
          }
      },
      "connectionSpec": {
          "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
          "version": "1.0"
      }
  }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.host` | O nome do host do servidor SFTP. |
| `auth.params.port` | A porta do servidor SFTP. O padrão desse valor inteiro é 22. |
| `auth.params.username` | O nome de usuário associado ao servidor SFTP. |
| `auth.params.password` | A senha associada ao servidor SFTP. |
| `auth.params.maxConcurrentConnections` | O número máximo de conexões simultâneas especificadas ao conectar a Platform ao SFTP. Quando ativado, esse valor deve ser definido como pelo menos 1. |
| `auth.params.folderPath` | O caminho para a pasta à qual você deseja fornecer acesso. |
| `connectionSpec.id` | A ID da especificação da conexão do servidor SFTP: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

+++

+++Resposta

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão recém-criada. Essa ID é necessária para explorar o servidor SFTP no próximo tutorial.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

+++

>[!TAB Autenticação de chave pública SSH]

+++Solicitação

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SFTP connector with SSH authentication",
      "description": "SFTP connector with SSH authentication",
      "auth": {
          "specName": "SSH PublicKey Authentication for sftp",
          "params": {
              "host": "{HOST}",
              "port": 22,
              "userName": "{USERNAME}",
              "privateKeyContent": "{PRIVATE_KEY_CONTENT}",
              "passPhrase": "{PASSPHRASE}",
              "maxConcurrentConnections": 5,
              "folderPath": "acme/business/customers/holidaySales"
          }
      },
      "connectionSpec": {
          "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
          "version": "1.0"
      }
  }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.host` | O nome do host de seu [!DNL SFTP] servidor. |
| `auth.params.port` | A porta do servidor SFTP. O padrão desse valor inteiro é 22. |
| `auth.params.username` | O nome de usuário associado à [!DNL SFTP] servidor. |
| `auth.params.privateKeyContent` | O conteúdo da chave privada SSH codificada na Base64. O tipo de chave OpenSSH deve ser classificado como RSA ou DSA. |
| `auth.params.passPhrase` | A senha para descriptografar a chave privada se o arquivo de chave ou o conteúdo da chave estiver protegido por uma senha. Se PrivateKeyContent estiver protegida por senha, esse parâmetro precisará ser usado com a senha de PrivateKeyContent como valor. |
| `auth.params.maxConcurrentConnections` | O número máximo de conexões simultâneas especificadas ao conectar a Platform ao SFTP. Quando ativado, esse valor deve ser definido como pelo menos 1. |
| `auth.params.folderPath` | O caminho para a pasta à qual você deseja fornecer acesso. |
| `connectionSpec.id` | A variável [!DNL SFTP] ID da especificação de conexão do servidor: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

+++

+++Resposta

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão recém-criada. Essa ID é necessária para explorar o servidor SFTP no próximo tutorial.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

+++

>[!ENDTABS]

## Próximas etapas

Ao seguir este tutorial, você criou um [!DNL SFTP] conexão usando o [!DNL Flow Service] e obtiveram o valor de identificador exclusivo da conexão. Você pode usar essa ID de conexão para [explorar armazenamentos em nuvem usando a API do Serviço de fluxo](../../explore/cloud-storage.md).
