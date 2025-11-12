---
title: Source da zona de aterrissagem de dados
description: Saiba como conectar a Data Landing Zone ao Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '1361'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

>[!IMPORTANT]
>
>Esta página é específica para o conector de [!DNL Data Landing Zone] *origem* na Experience Platform. Para obter informações sobre como se conectar ao conector de [!DNL Data Landing Zone] *destino*, consulte a [[!DNL Data Landing Zone] página de documentação de destino](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

O [!DNL Data Landing Zone] é uma interface de armazenamento do [!DNL Azure Blob] provisionada pela Adobe Experience Platform, que concede a você acesso a um recurso de armazenamento de arquivos seguro e baseado em nuvem para trazer arquivos para a Experience Platform. Você tem acesso a um [!DNL Data Landing Zone] contêiner por sandbox, e o volume total de dados em todos os contêineres é limitado ao total de dados fornecidos com sua licença de Produtos e Serviços da Experience Platform. Todos os clientes do Experience Platform são provisionados com um contêiner de [!DNL Data Landing Zone] por sandbox. Você pode ler e gravar arquivos no seu contêiner por meio do [!DNL Azure Storage Explorer] ou da interface de linha de comando.

O [!DNL Data Landing Zone] oferece suporte à autenticação baseada em SAS e seus dados estão protegidos com mecanismos de segurança de armazenamento [!DNL Azure Blob] padrão em repouso e em trânsito. A autenticação baseada em SAS permite que você acesse com segurança o contêiner do [!DNL Data Landing Zone] por meio de uma conexão pública com a Internet. Não há alterações de rede necessárias para que você acesse o contêiner [!DNL Data Landing Zone], o que significa que você não precisa definir nenhum incluo na lista de permissões ou configurações entre regiões para sua rede. O Experience Platform impõe um tempo de expiração rigoroso de sete dias em todos os arquivos e pastas carregados em um contêiner [!DNL Data Landing Zone]. Todos os arquivos e pastas são excluídos após sete dias.

## Configure sua origem [!DNL Data Landing Zone] para o Experience Platform no Azure {#azure}

Siga as etapas abaixo para saber como configurar sua conta do [!DNL Data Landing Zone] para o Experience Platform no Azure.

>[!NOTE]
>
>Para acessar [!DNL Data Landing Zone] a partir de [!DNL Azure Data Factory], você deve criar um serviço vinculado para [!DNL Data Landing Zone] usando as [credenciais SAS](../../tutorials/ui/create/cloud-storage/data-landing-zone.md#retrieve-your-data-landing-zone-credentials) fornecidas pela Experience Platform. Depois de criar o serviço vinculado, você pode explorar o [!DNL Data Landing Zone] selecionando o caminho do contêiner em vez do caminho raiz padrão.

### Restrições de nomenclatura para arquivos e diretórios

Veja a seguir uma lista de restrições que você deve considerar ao nomear seus arquivos ou diretórios de armazenamento em nuvem.

- Os nomes dos componentes de diretório e arquivo não podem exceder 255 caracteres.
- Nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
- Os seguintes caracteres de URL reservados devem ter um escape adequado: `! ' ( ) ; @ & = + $ , % # [ ]`
- Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
- Caracteres de caminho de URL inválidos não permitidos. Pontos de código como `\uE000`, embora válidos em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode, como caracteres de controle (como `0x00` a `0x1F`, `\u0081` e assim por diante), também não são permitidos. Para regras que regem cadeias de caracteres Unicode em HTTP/1.1, consulte [RFC 2616, Seção 2.2: Regras Básicas](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (.) e dois caracteres de ponto (..).

### Gerenciar o conteúdo da Data Landing Zone{#manage-the-contents-of-your-data-landing-zone}

Você pode usar o [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/features/storage-explorer/) para gerenciar o conteúdo do seu contêiner [!DNL Data Landing Zone].

Na interface do usuário do [!DNL Azure Storage Explorer], selecione o ícone de conexão no menu de navegação esquerdo. A janela **Selecionar Recurso** é exibida, fornecendo opções para conexão. Selecione **[!DNL Blob container]** para se conectar a [!DNL Data Landing Zone].

![O espaço de trabalho de recursos selecionado no Azure Explorer.](../../images/tutorials/create/dlz/select-resource.png)

Em seguida, selecione **SAS (URL de assinatura de acesso compartilhado)** como seu método de conexão e selecione **Avançar**.

![O método de conexão selecionado no Azure Explorer, com assinatura de acesso compartilhado selecionada.](../../images/tutorials/create/dlz/select-connection-method.png)

Depois de selecionar seu método de conexão, você deve fornecer um **nome para exibição** e a URL SAS do contêiner **[!DNL Blob]** que corresponda ao seu contêiner [!DNL Data Landing Zone].

>[!TIP]
>
>Você pode recuperar suas credenciais do [!DNL Data Landing Zone] no catálogo de origens na interface do usuário do Experience Platform.

Forneça a URL SAS do [!DNL Data Landing Zone] e selecione **Avançar**

![O espaço de trabalho para inserir informações de conexão no Azure Explorer, onde o nome para exibição e a URL SAS são inseridos.](../../images/tutorials/create/dlz/enter-connection-info.png)

A janela **Resumo** é exibida, fornecendo uma visão geral das configurações, incluindo informações sobre o ponto de extremidade e as permissões do [!DNL Blob]. Quando estiver pronto, selecione **Conectar**.

![O espaço de trabalho de resumo do Azure Explorer que recapitula as configurações de sua conexão de recurso.](../../images/tutorials/create/dlz/summary.png)

Uma conexão bem-sucedida atualiza a interface do usuário [!DNL Azure Storage Explorer] com o contêiner [!DNL Data Landing Zone].

![O espaço de trabalho de navegação da zona de aterrissagem de dados no Azure Explorer.](../../images/tutorials/create/dlz/dlz-user-container.png)

Com o contêiner [!DNL Data Landing Zone] conectado ao [!DNL Azure Storage Explorer], você pode começar a carregar arquivos no contêiner [!DNL Data Landing Zone]. Para carregar, selecione **Carregar** e **Carregar Arquivos**.

![O espaço de trabalho de carregamento de arquivos do Azure Explorer.](../../images/tutorials/create/dlz/upload.png)

Depois de selecionar o arquivo que deseja carregar, você deve identificar o tipo [!DNL Blob] com o qual deseja carregá-lo e o diretório de destino desejado. Quando terminar, selecione **Carregar**.

| [!DNL Blob] tipos | Descrição |
| --- | --- |
| Bloquear [!DNL Blob] | Os blocos [!DNL Blobs] estão otimizados para carregar grandes quantidades de dados de maneira eficiente. Bloquear [!DNL Blobs] é a opção padrão para [!DNL Data Landing Zone]. |
| Acrescentar [!DNL Blob] | Os acréscimos [!DNL Blobs] são otimizados para anexar dados ao final do arquivo. |

![A janela de carregamento de arquivos do Azure Explorer onde os arquivos selecionados, o tipo de Blob e a categoria de destino são exibidos.](../../images/tutorials/create/dlz/upload-files.png)

### Carregar arquivos no [!DNL Data Landing Zone] usando a interface de linha de comando

Você também pode usar a interface de linha de comando do seu dispositivo e acessar arquivos de carregamento no [!DNL Data Landing Zone].

### Carregar um arquivo usando o Bash

O exemplo a seguir usa Bash e cURL para carregar um arquivo para um [!DNL Data Landing Zone] com a API REST [!DNL Azure Blob Storage]:

```shell
# Set Azure Blob-related settings
DATE_NOW=$(date -Ru | sed 's/\+0000/GMT/')
AZ_VERSION="2018-03-28"
AZ_BLOB_URL="<URL TO BLOB ACCOUNT>"
AZ_BLOB_CONTAINER="<BLOB CONTAINER NAME>"
AZ_BLOB_TARGET="${AZ_BLOB_URL}/${AZ_BLOB_CONTAINER}"
AZ_SAS_TOKEN="<SAS TOKEN, STARTING WITH ? AND ENDING WITH %3D>"

# Path to the file we wish to upload
FILE_PATH="</PATH/TO/FILE>"
FILE_NAME=$(basename "$FILE_PATH")

# Execute HTTP PUT to upload file (remove '-v' flag to suppress verbose output)
curl -v -X PUT \
   -H "Content-Type: application/octet-stream" \
   -H "x-ms-date: ${DATE_NOW}" \
   -H "x-ms-version: ${AZ_VERSION}" \
   -H "x-ms-blob-type: BlockBlob" \
   --data-binary "@${FILE_PATH}" "${AZ_BLOB_TARGET}/${FILE_NAME}${AZ_SAS_TOKEN}"
```

### Carregar um arquivo usando o Python

O exemplo a seguir usa o SDK do Python v12 [!DNL Microsoft's] para carregar um arquivo em um [!DNL Data Landing Zone]:

>[!TIP]
>
>Embora o exemplo abaixo use o URI SAS completo para se conectar a um contêiner [!DNL Azure Blob], você pode usar outros métodos e operações para autenticar. Consulte este [[!DNL Microsoft] documento no Python v12 SDK](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-python) para obter mais informações.

```py
import os
from azure.storage.blob import ContainerClient

try:
    # Set Azure Blob-related settings
    sasUri = "<SAS URI>"
    srcFilePath = "<FULL PATH TO FILE>" 
    srcFileName = os.path.basename(srcFilePath)

    # Connect to container using SAS URI
    containerClient = ContainerClient.from_container_url(sasUri)

    # Upload file to Data Landing Zone with overwrite enabled
    with open(srcFilePath, "rb") as fileToUpload:
        containerClient.upload_blob(srcFileName, fileToUpload, overwrite=True)

except Exception as ex:
    print("Exception: " + ex.strerror)
```

### Carregar um arquivo usando [!DNL AzCopy]

O exemplo a seguir usa o utilitário [!DNL Microsoft's] [!DNL AzCopy] para carregar um arquivo para um [!DNL Data Landing Zone]:

>[!TIP]
>
>Enquanto o exemplo abaixo está usando o comando `copy`, você pode usar outros comandos e opções para carregar um arquivo no [!DNL Data Landing Zone], usando [!DNL AzCopy]. Consulte este [[!DNL Microsoft AzCopy] documento](https://docs.microsoft.com/en-us/azure/storage/common/storage-ref-azcopy?toc=/azure/storage/blobs/toc.json) para obter mais informações.

```bat
set sasUri=<FULL SAS URI, PROPERLY ESCAPED>
set srcFilePath=<PATH TO LOCAL FILE(S); WORKS WITH WILDCARD PATTERNS>

azcopy copy "%srcFilePath%" "%sasUri%" --overwrite=true --recursive=true
```

## Configure sua origem do [!DNL Data Landing Zone] para o Experience Platform no Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Esta seção se aplica às implementações do Experience Platform em execução no Amazon Web Services (AWS). O Experience Platform em execução no AWS está disponível atualmente para um número limitado de clientes. Para saber mais sobre a infraestrutura do Experience Platform compatível, consulte a [visão geral da nuvem múltipla do Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud).

Siga as etapas abaixo para saber como configurar sua conta do [!DNL Data Landing Zone] para o Experience Platform no Amazon Web Services (AWS).

### INCLUO NA LISTA DE PERMISSÕES de endereços IP para conexão no AWS

Você deve adicionar endereços IP específicos da região ao incluo na lista de permissões antes de conectar suas fontes à Experience Platform no AWS. Para obter mais informações, leia o manual sobre [sobre como ler os endereços IP de incluir na lista de permissões para se conectar ao Experience Platform no AWS](../../ip-address-allow-list.md) para obter mais informações.

### Configurar a CLI do AWS e executar operações

- Leia o guia sobre [instalação ou atualização para a versão mais recente da CLI do AWS](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).

### Configurar o AWS CLI com credenciais temporárias

Use o comando `configure` do AWS para configurar sua CLI com chaves de acesso e um token de sessão.

```shell
aws configure
```

Quando solicitado, insira os seguintes valores:

- ID da chave de acesso do AWS: `{YOUR_ACCESS_KEY_ID}`
- Chave de acesso secreta do AWS: `{YOUR_SECRET_ACCESS_KEY}`
- Nome da região padrão: `{YOUR_REGION}` (por exemplo, `us-west-2`)
- Formato de saída padrão: `json`

Em seguida, defina o token da sessão:

```shell
aws configure set aws_session_token your-session-token
```

### Trabalhar com arquivos em [!DNL Amazon S3]

>[!BEGINTABS]

>[!TAB Carregar um arquivo no Amazon S3]

Modelo:

```shell
aws s3 cp local-file-path s3://bucketName/dlzFolder/remote-file-Name
```

Exemplo:

```shell
aws s3 cp example.txt s3://bucketName/dlzFolder/example.txt
```


>[!TAB Baixar um arquivo do Amazon S3]

Modelo:

```shell
aws s3 cp s3://bucketName/dlzFolder/remote-file local-file-path
```

Exemplo:

```shell
aws s3 cp s3://bucketName/dlzFolder/example.txt example.txt
```

>[!ENDTABS]

### Use suas credenciais do [!DNL Data Landing Zone] para fazer logon no Console do AWS

#### Extrair suas credenciais

Primeiro, você deve obter o seguinte:

- `awsAccessKeyId`
- `awsSecretAccessKey`
- `awsSessionToken`

#### Gerar um token de entrada

Em seguida, use as credenciais extraídas para criar uma sessão e gerar um token de logon usando o endpoint do AWS Federation:

```py
import json
import requests
 
# Example DLZ response with credentials
response_json = '''{
    "credentials": {
        "awsAccessKeyId": "your-access-key",
        "awsSecretAccessKey": "your-secret-key",
        "awsSessionToken": "your-session-token"
    }
}'''
 
# Parse credentials
response_data = json.loads(response_json)
aws_access_key_id = response_data['credentials']['awsAccessKeyId']
aws_secret_access_key = response_data['credentials']['awsSecretAccessKey']
aws_session_token = response_data['credentials']['awsSessionToken']
 
# Create session dictionary
session = {
    'sessionId': aws_access_key_id,
    'sessionKey': aws_secret_access_key,
    'sessionToken': aws_session_token
}
 
# Generate the sign-in token
signin_token_url = "https://signin.aws.amazon.com/federation"
signin_token_payload = {
    "Action": "getSigninToken",
    "Session": json.dumps(session)
}
signin_token_response = requests.post(signin_token_url, data=signin_token_payload)
signin_token = signin_token_response.json()['SigninToken']
```

#### Construir o URL de logon do console do AWS

Depois de usar o token de entrada, você poderá criar a URL que o registra no Console do AWS e aponta diretamente para o bucket [!DNL Amazon S3] desejado.

```py
from urllib.parse import quote
 
# Define the S3 bucket and folder path you want to access
bucket_name = "your-bucket-name"
bucket_path = "your-bucket-folder"
 
# Construct the destination URL
destination_url = f"https://s3.console.aws.amazon.com/s3/buckets/{bucket_name}?prefix={bucket_path}/&tab=objects"
 
# Create the final sign-in URL
signin_url = f"https://signin.aws.amazon.com/federation?Action=login&Issuer=YourAppName&Destination={quote(destination_url)}&SigninToken={signin_token}"
 
print(f"Sign-in URL: {signin_url}")
```

#### Acessar o console do AWS

Finalmente, navegue até a URL gerada para fazer logon diretamente no Console do AWS com suas credenciais do [!DNL Data Landing Zone], que fornece acesso a uma pasta específica em um bucket do [!DNL Amazon S3]. O URL de entrada o levará diretamente para essa pasta, garantindo que você veja e gerencie apenas os dados permitidos.

## Conectar [!DNL Data Landing Zone] ao Experience Platform

>[!IMPORTANT]
>
>- Para se conectar à origem, você precisa das permissões de controle de acesso **[!UICONTROL View Sources]** e **[!UICONTROL Manage Sources]**. Para obter mais informações, leia a [visão geral do controle de acesso](../../../access-control/home.md) ou contate o administrador do produto para obter as permissões necessárias.
>
>- No momento, não há suporte para links privados ao se conectar ao Experience Platform usando o [!DNL Data Landing Zone]. Os únicos métodos suportados para acesso são os métodos listados [aqui](#manage-the-contents-of-your-data-landing-zone).

A documentação abaixo fornece informações sobre como trazer dados do seu contêiner do [!DNL Data Landing Zone] para a Adobe Experience Platform usando APIs ou a interface do usuário.

### Uso de APIs

- [Criar uma conexão de origem  [!DNL Data Landing Zone]  usando a API de Serviço de Fluxo](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Criar um fluxo de dados para uma fonte de armazenamento na nuvem usando a API do Serviço de fluxo](../../tutorials/api/collect/cloud-storage.md)

### Uso da interface

- [Conectar [!DNL Data Landing Zone] ao Experience Platform usando a interface](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [Criar um fluxo de dados para uma conexão de armazenamento na nuvem na interface](../../tutorials/ui/dataflow/batch/cloud-storage.md)

