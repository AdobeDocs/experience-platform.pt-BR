---
keywords: Experience Platform;home;popular topics;SFTP;sftp;Secure File Transfer Protocol;secure file transfer protocol
solution: Experience Platform
title: Criar um conector SFTP usando a API de Serviço de Fluxo
topic: overview
type: Tutorial
description: Este tutorial usa a API de Serviço de Fluxo para guiá-lo pelas etapas para conectar o Experience Platform a um servidor SFTP (Secure File Transfer Protocol).
translation-type: tm+mt
source-git-commit: c88b9400144f511ef456fd5fdc968a5a6b7a3dc0
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 1%

---


# Crie um conector SFTP usando a API [!DNL Flow Service]

>[!NOTE]
>
>O conector SFTP está em beta. Os recursos e a documentação estão sujeitos a alterações. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores marcados com beta.

Este tutorial usa a API [!DNL Flow Service] para guiá-lo pelas etapas para conectar o Experience Platform a um servidor SFTP (Secure File Transfer Protocol).

## Introdução

Este guia exige uma compreensão prática dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, ao mesmo tempo em que lhe fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Caixas de proteção](../../../../../sandboxes/home.md): O Experience Platform fornece caixas de proteção virtuais que particionam uma única instância da Plataforma em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

>[!IMPORTANT]
>
>É recomendável evitar novas linhas ou retornos de carro ao assimilar objetos JSON com uma conexão de origem SFTP. Para contornar a limitação, use um único objeto JSON por linha e use várias linhas para arquivos subsequentes.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a um servidor SFTP usando a API [!DNL Flow Service].

### Reunir credenciais obrigatórias

Para que [!DNL Flow Service] se conecte ao SFTP, é necessário fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O nome ou endereço IP associado ao servidor SFTP. |
| `username` | O nome de usuário com acesso ao seu servidor SFTP. |
| `password` | A senha do servidor SFTP. |
| `privateKeyContent` | O conteúdo de chave privada SSH codificado em Base64. O formato SSH private key OpenSSH (RSA/DSA). |
| `passPhrase` | A senha ou senha para descriptografar a chave privada se o arquivo de chave ou o conteúdo de chave estiver protegido por uma senha. Se PrivateKeyContent for protegido por senha, esse parâmetro deverá ser usado com a senha de PrivateKeyContent como valor. |

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção em [como ler chamadas de API de exemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas do Experience Platform.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para APIs de plataforma, você deve primeiro concluir o [tutorial de autenticação](../../../../../tutorials/authentication.md). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API de Experience Platform, como mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo os pertencentes a [!DNL Flow Service], são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* `Content-Type: application/json`

## Criar uma conexão

Uma conexão especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão é necessária, pois pode ser usada para criar vários fluxos de dados para trazer dados diferentes.

### Criar uma conexão SFTP usando autenticação básica

Para criar uma conexão SFTP usando autenticação básica, faça uma solicitação POST para a API [!DNL Flow Service], fornecendo valores para as `host`, `userName` e `password` da sua conexão.

**Formato da API**

```http
POST /connections
```

**Solicitação**

Para criar uma conexão SFTP, sua ID exclusiva de especificação de conexão deve ser fornecida como parte da solicitação de POST. A ID de especificação de conexão para SFTP é `b7bf2577-4520-42c9-bae9-cad01560f7bc`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.host` | O nome do host do servidor SFTP. |
| `auth.params.username` | O nome de usuário associado ao servidor SFTP. |
| `auth.params.password` | A senha associada ao servidor SFTP. |
| `connectionSpec.id` | A ID da especificação da conexão do servidor SFTP: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão recém-criada. Essa ID é necessária para explorar o servidor SFTP no próximo tutorial.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

### Criar uma conexão SFTP usando autenticação de chave pública SSH

Para criar uma conexão SFTP usando a autenticação de chave pública SSH, faça uma solicitação de POST à API [!DNL Flow Service], fornecendo valores para as `host`, `userName`, `privateKeyContent` e `passPhrase` da sua conexão.

**Formato da API**

```http
POST /connections
```

**Solicitação**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.host` | O nome do host do servidor SFTP. |
| `auth.params.username` | O nome de usuário associado ao servidor SFTP. |
| `auth.params.privateKeyContent` | O conteúdo da chave privada SSH codificado em base64. O formato SSH private key OpenSSH (RSA/DSA). |
| `auth.params.passPhrase` | A senha ou senha para descriptografar a chave privada se o arquivo de chave ou o conteúdo de chave estiver protegido por uma senha. Se PrivateKeyContent for protegido por senha, esse parâmetro deverá ser usado com a senha de PrivateKeyContent como valor. |
| `connectionSpec.id` | A ID da especificação da conexão do servidor SFTP: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão recém-criada. Essa ID é necessária para explorar o servidor SFTP no próximo tutorial.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão SFTP usando a API [!DNL Flow Service] e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID de conexão para [explorar armazenamentos em nuvem usando a API do Serviço de Fluxo](../../explore/cloud-storage.md) ou [assimilar dados de parquet usando a API do Serviço de Fluxo](../../cloud-storage-parquet.md).
