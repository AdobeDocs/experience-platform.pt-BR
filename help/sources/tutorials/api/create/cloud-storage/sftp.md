---
keywords: Experience Platform, home, tópicos populares, SFTP, sftp, protocolo de transferência segura de arquivo, protocolo de transferência segura de arquivo
solution: Experience Platform
title: Criar uma conexão base SFTP usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform a um servidor SFTP (Secure File Transfer Protocol) usando a API do Serviço de Fluxo.
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 2%

---

# Crie uma conexão base SFTP usando o [!DNL Flow Service] API

Uma conexão base representa a conexão autenticada entre uma fonte e o Adobe Experience Platform.

Este tutorial o orienta pelas etapas para criar uma conexão básica para [!DNL SFTP] (Protocolo de transferência segura de arquivo) usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

>[!IMPORTANT]
>
>Recomenda-se evitar quebras de linha ou retornos de carro ao assimilar objetos JSON com um [!DNL SFTP] conexão de origem. Para contornar a limitação, use um único objeto JSON por linha e use várias linhas para os arquivos subsequentes.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a um [!DNL SFTP] usando o [!DNL Flow Service] API.

### Obter credenciais necessárias

Para [!DNL Flow Service] para se conectar a [!DNL SFTP], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O nome ou endereço IP associado à [!DNL SFTP] servidor. |
| `port` | A porta do servidor SFTP à qual você está se conectando. Se não for fornecido, o valor assumirá como padrão `22`. |
| `username` | O nome de usuário com acesso ao [!DNL SFTP] servidor. |
| `password` | A senha de seu [!DNL SFTP] servidor. |
| `privateKeyContent` | O conteúdo da chave privada SSH codificada em Base64. O tipo de chave OpenSSH deve ser classificado como RSA ou DSA. |
| `passPhrase` | A senha ou senha para descriptografar a chave privada se o arquivo da chave ou o conteúdo da chave estiver protegido por uma senha. Se a variável `privateKeyContent` estiver protegido por senha, esse parâmetro precisará ser usado com a senha do conteúdo da chave privada como valor. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem. A ID de especificação de conexão para [!DNL SFTP] é: `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../../../landing/api-guide.md).

## Criar uma conexão base

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST para a variável `/connections` endpoint enquanto fornece seu [!DNL SFTP] credenciais de autenticação como parte dos parâmetros da solicitação.

### Crie um [!DNL SFTP] conexão básica usando autenticação básica

Para criar um [!DNL SFTP] conexão básica usando autenticação básica, faça uma solicitação de POST para [!DNL Flow Service] API enquanto fornece valores para o `host`, `userName`e `password`.

**Formato da API**

```http
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL SFTP] usando autenticação básica:

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
                "userName": "{USERNAME}",
                "password": "{PASSWORD}"
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
| `auth.params.host` | O nome do host do seu servidor SFTP. |
| `auth.params.username` | O nome de usuário associado ao servidor SFTP. |
| `auth.params.password` | A senha associada ao servidor SFTP. |
| `connectionSpec.id` | A ID de especificação da conexão do servidor SFTP: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão recém-criada. Essa ID é necessária para explorar seu servidor SFTP no próximo tutorial.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

### Crie um [!DNL SFTP] conexão básica usando autenticação de chave pública SSH

Para criar um [!DNL SFTP] conexão básica usando autenticação de chave pública SSH, faça uma solicitação POST para [!DNL Flow Service] API enquanto fornece valores para o `host`, `userName`, `privateKeyContent`e `passPhrase`.

>[!IMPORTANT]
>
>O [!DNL SFTP] O conector é compatível com uma chave OpenSSH tipo RSA ou DSA. Certifique-se de que o conteúdo do arquivo principal comece com `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` e termina com `"-----END [RSA/DSA] PRIVATE KEY-----"`. Se o arquivo de chave privada for um arquivo no formato PPK, use a ferramenta PuTTY para converter do formato PPK para OpenSSH.

**Formato da API**

```http
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL SFTP] usando a autenticação de chave pública SSH:

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
                "userName": "{USERNAME}",
                "privateKeyContent": "{PRIVATE_KEY_CONTENT}",
                "passPhrase": "{PASSPHRASE}"
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
| `auth.params.host` | O nome de host do seu [!DNL SFTP] servidor. |
| `auth.params.username` | O nome de usuário associado à [!DNL SFTP] servidor. |
| `auth.params.privateKeyContent` | O conteúdo da chave privada SSH codificada em Base64. O tipo de chave OpenSSH deve ser classificado como RSA ou DSA. |
| `auth.params.passPhrase` | A senha ou senha para descriptografar a chave privada se o arquivo da chave ou o conteúdo da chave estiver protegido por uma senha. Se PrivateKeyContent estiver protegido por senha, esse parâmetro precisará ser usado com a senha de PrivateKeyContent como valor. |
| `connectionSpec.id` | O [!DNL SFTP] ID de especificação de conexão do servidor: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão recém-criada. Essa ID é necessária para explorar [!DNL SFTP] no próximo tutorial.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou um [!DNL SFTP] conexão usando o [!DNL Flow Service] e obtiveram o valor de ID exclusivo da conexão. Você pode usar essa ID de conexão para [explorar armazenamentos em nuvem usando a API do Serviço de fluxo](../../explore/cloud-storage.md).
