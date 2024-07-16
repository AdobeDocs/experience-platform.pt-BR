---
title: Criar uma conexão básica SFTP usando a API do serviço de fluxo
description: Saiba como conectar o Adobe Experience Platform a um servidor SFTP usando a API do serviço de fluxo.
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: f6d1cc811378f2f37968bf0a42b428249e52efd8
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 2%

---

# Criar uma conexão básica SFTP usando a API [!DNL Flow Service]

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Este tutorial guiará você pelas etapas para criar uma conexão base para o [!DNL SFTP] (Protocolo de Transferência Segura de Arquivo) usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

>[!IMPORTANT]
>
>É recomendável evitar novas linhas ou retornos de carro ao assimilar objetos JSON com uma conexão de origem [!DNL SFTP]. Para contornar a limitação, use um único objeto JSON por linha e use várias linhas para os arquivos subsequentes.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a um servidor [!DNL SFTP] usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL SFTP], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O nome ou endereço IP associado ao servidor [!DNL SFTP]. |
| `port` | A porta do servidor SFTP à qual você está se conectando. Se não for fornecido, o valor padrão será `22`. |
| `username` | O nome de usuário com acesso ao servidor [!DNL SFTP]. |
| `password` | A senha do servidor [!DNL SFTP]. |
| `privateKeyContent` | O conteúdo da chave privada SSH codificada na Base64. O tipo de chave OpenSSH deve ser classificado como RSA ou DSA. |
| `passPhrase` | A senha para descriptografar a chave privada se o arquivo de chave ou o conteúdo da chave estiver protegido por uma senha. Se o `privateKeyContent` estiver protegido por senha, esse parâmetro precisará ser usado com a senha do conteúdo da chave privada como valor. |
| `maxConcurrentConnections` | Esse parâmetro permite especificar um limite máximo para o número de conexões simultâneas que a Platform criará ao se conectar ao servidor SFTP. Você deve definir esse valor como menor que o limite definido pelo SFTP. **Observação**: quando esta configuração é habilitada para uma conta SFTP existente, ela afeta apenas os fluxos de dados futuros, não os existentes. |
| `folderPath` | O caminho para a pasta à qual você deseja fornecer acesso. [!DNL SFTP] origem, você pode fornecer o caminho da pasta para especificar o acesso do usuário à subpasta de sua escolha. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL SFTP] é: `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual sobre [introdução às APIs da Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica

>[!TIP]
>
>Depois de criada, você não pode alterar o tipo de autenticação de uma conexão de base [!DNL SFTP]. Para alterar o tipo de autenticação, você deve criar uma nova conexão base.

Uma conexão base retém informações entre sua origem e a Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e sua ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

A origem [!DNL SFTP] dá suporte à autenticação básica e à autenticação via chave pública SSH. Durante essa etapa, também é possível designar o caminho para a subpasta à qual você deseja fornecer acesso.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` enquanto fornece suas credenciais de autenticação [!DNL SFTP] como parte dos parâmetros de solicitação.

>[!IMPORTANT]
>
>O conector [!DNL SFTP] dá suporte a uma chave OpenSSH do tipo RSA ou DSA. Verifique se o conteúdo do arquivo de chave começa com `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` e termina com `"-----END [RSA/DSA] PRIVATE KEY-----"`. Se o arquivo de chave privada for um arquivo no formato PPK, use a ferramenta PuTTY para converter do formato PPK para o formato OpenSSH.

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
| `connectionSpec.id` | A ID da especificação de conexão do servidor SFTP: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

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
| `auth.params.host` | O nome do host do servidor [!DNL SFTP]. |
| `auth.params.port` | A porta do servidor SFTP. O padrão desse valor inteiro é 22. |
| `auth.params.username` | O nome de usuário associado ao seu servidor [!DNL SFTP]. |
| `auth.params.privateKeyContent` | O conteúdo da chave privada SSH codificada na Base64. O tipo de chave OpenSSH deve ser classificado como RSA ou DSA. |
| `auth.params.passPhrase` | A senha para descriptografar a chave privada se o arquivo de chave ou o conteúdo da chave estiver protegido por uma senha. Se PrivateKeyContent estiver protegida por senha, esse parâmetro precisará ser usado com a senha de PrivateKeyContent como valor. |
| `auth.params.maxConcurrentConnections` | O número máximo de conexões simultâneas especificadas ao conectar a Platform ao SFTP. Quando ativado, esse valor deve ser definido como pelo menos 1. |
| `auth.params.folderPath` | O caminho para a pasta à qual você deseja fornecer acesso. |
| `connectionSpec.id` | A ID da especificação de conexão do servidor [!DNL SFTP]: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

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

Seguindo este tutorial, você criou uma conexão [!DNL SFTP] usando a API [!DNL Flow Service] e obteve o valor da ID exclusiva da conexão. Você pode usar esta ID de conexão para [explorar armazenamentos em nuvem usando a API de Serviço de Fluxo](../../explore/cloud-storage.md).
