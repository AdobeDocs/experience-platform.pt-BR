---
keywords: Experience Platform;página inicial;tópicos populares
solution: Experience Platform
title: Origem da zona de aterrissagem de dados
description: Saiba como conectar a Data Landing Zone ao Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: c2cc734d4a5c86fecbd0dabdfe63c896f0fe0f54
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

>[!IMPORTANT]
>
>Esta página é específica do [!DNL Data Landing Zone] *origem* conector no Experience Platform. Para obter informações sobre como se conectar ao [!DNL Data Landing Zone] *destino* conector, consulte a [[!DNL Data Landing Zone] página da documentação de destino](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] é um [!DNL Azure Blob] interface de armazenamento de dados provisionada pela Adobe Experience Platform, permitindo que você acesse um recurso de armazenamento de arquivos seguro e baseado em nuvem para trazer arquivos para a plataforma. Você tem acesso a um [!DNL Data Landing Zone] por sandbox, e o volume total de dados em todos os containers é limitado ao total de dados fornecido com sua licença de Produtos e Serviços da Platform. Todos os clientes da Platform e seus serviços de aplicativos, como [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services], e [!DNL Adobe Real-Time Customer Data Platform] são provisionados com um [!DNL Data Landing Zone] contêiner por sandbox. Você pode ler e gravar arquivos no seu contêiner por meio de [!DNL Azure Storage Explorer] ou na interface de linha de comando.

[!DNL Data Landing Zone] oferece suporte à autenticação baseada em SAS e seus dados estão protegidos com o padrão [!DNL Azure Blob] mecanismos de segurança de armazenamento em repouso e em trânsito. A autenticação baseada em SAS permite que você acesse com segurança seus [!DNL Data Landing Zone] contêiner por meio de uma conexão pública com a internet. Não são necessárias alterações na rede para que você acesse seu [!DNL Data Landing Zone] contêiner, o que significa que você não precisa definir nenhuma configuração de lista de permissões ou entre regiões para sua rede. O Platform impõe um tempo de expiração de sete dias rigoroso em todos os arquivos carregados em um [!DNL Data Landing Zone] recipiente. Todos os arquivos são excluídos após sete dias.

## Restrições de nomenclatura para arquivos e diretórios

Veja a seguir uma lista de restrições que você deve considerar ao nomear seus arquivos ou diretórios de armazenamento em nuvem.

- Os nomes dos componentes de diretório e arquivo não podem exceder 255 caracteres.
- Nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
- Os seguintes caracteres de URL reservados devem ter escape adequado: `! ' ( ) ; @ & = + $ , % # [ ]`
- Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
- Caracteres de caminho de URL inválidos não permitidos. Pontos de código como `\uE000`, embora sejam válidos em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode, como caracteres de controle (como `0x00` para `0x1F`, `\u0081`e assim por diante), também não são permitidos. Para obter as regras que regem strings Unicode em HTTP/1.1, consulte [RFC 2616, Seção 2.2: regras básicas](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (.) e dois caracteres de ponto (..).

## Gerenciar o conteúdo da Data Landing Zone{#manage-the-contents-of-your-data-landing-zone}

Você pode usar [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/features/storage-explorer/) para gerenciar o conteúdo do [!DNL Data Landing Zone] recipiente.

No [!DNL Azure Storage Explorer] Selecione o ícone de conexão no menu de navegação esquerdo. A variável **Selecionar recurso** é exibida, fornecendo opções para conexão. Selecionar **[!DNL Blob container]** para se conectar a [!DNL Data Landing Zone].

![select-resource](../../images/tutorials/create/dlz/select-resource.png)

Em seguida, selecione **URL de assinatura de acesso compartilhado (SAS)** como seu método de conexão e, em seguida, selecione **Próxima**.

![select-connection-method](../../images/tutorials/create/dlz/select-connection-method.png)

Depois de selecionar o método de conexão, você deve fornecer um **nome de exibição** e a variável **[!DNL Blob]URL SAS do contêiner** que corresponde ao seu [!DNL Data Landing Zone] recipiente.

>[!TIP]
>
>Você pode recuperar seus [!DNL Data Landing Zone] credenciais do catálogo de origens na interface do usuário da Platform.

Forneça o seu [!DNL Data Landing Zone] SAS URL e selecione **Próxima**

![enter-connection-info](../../images/tutorials/create/dlz/enter-connection-info.png)

A variável **Resumo** é exibida, fornecendo uma visão geral de suas configurações, incluindo informações sobre [!DNL Blob] endpoint e permissões. Quando estiver pronto, selecione **Conectar**.

![resumo](../../images/tutorials/create/dlz/summary.png)

Uma conexão bem-sucedida atualiza seu [!DNL Azure Storage Explorer] Interface com o seu [!DNL Data Landing Zone] recipiente.

![dlz-user-container](../../images/tutorials/create/dlz/dlz-user-container.png)

Com o seu [!DNL Data Landing Zone] contêiner conectado a [!DNL Azure Storage Explorer], agora é possível iniciar o upload de arquivos para o [!DNL Data Landing Zone] recipiente. Para fazer upload, selecione **Carregar** e selecione **Fazer upload de arquivos**.

![upload](../../images/tutorials/create/dlz/upload.png)

Depois de selecionar o arquivo que deseja fazer upload, você deve identificar o [!DNL Blob] digite como você deseja carregá-lo e o diretório de destino desejado. Quando terminar, selecione **Carregar**.

| [!DNL Blob] tipos | Descrição |
| --- | --- |
| Bloquear [!DNL Blob] | Bloquear [!DNL Blobs] são otimizadas para carregar grandes quantidades de dados de maneira eficiente. Bloquear [!DNL Blobs] são a opção padrão para [!DNL Data Landing Zone]. |
| Anexar [!DNL Blob] | Anexar [!DNL Blobs] são otimizados para anexar dados ao final do arquivo. |

![upload de arquivos](../../images/tutorials/create/dlz/upload-files.png)

## Fazer upload de arquivos para o [!DNL Data Landing Zone] usando a interface de linha de comando

Você também pode usar a interface de linha de comando do dispositivo e acessar os arquivos de upload no [!DNL Data Landing Zone].

### Carregar um arquivo usando o Bash

O exemplo a seguir usa Bash e cURL para fazer upload de um arquivo para um [!DNL Data Landing Zone] com o [!DNL Azure Blob Storage] API REST:

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

O exemplo a seguir usa [!DNL Microsoft's] Python v12 SDK para carregar um arquivo em um [!DNL Data Landing Zone]:

>[!TIP]
>
>Enquanto o exemplo abaixo usa o URI SAS completo para se conectar a um [!DNL Azure Blob] contêiner, é possível usar outros métodos e operações para autenticação. Veja isto [[!DNL Microsoft] documento no Python v12 SDK](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-python) para obter mais informações.

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

O exemplo a seguir usa [!DNL Microsoft's] [!DNL AzCopy] utilitário para carregar um arquivo em um [!DNL Data Landing Zone]:

>[!TIP]
>
>Embora o exemplo abaixo esteja usando a variável `copy` você pode usar outros comandos e opções para fazer upload de um arquivo no seu [!DNL Data Landing Zone], utilizando [!DNL AzCopy]. Veja isto [[!DNL Microsoft AzCopy] documento](https://docs.microsoft.com/en-us/azure/storage/common/storage-ref-azcopy?toc=/azure/storage/blobs/toc.json) para obter mais informações.

```bat
set sasUri=<FULL SAS URI, PROPERLY ESCAPED>
set srcFilePath=<PATH TO LOCAL FILE(S); WORKS WITH WILDCARD PATTERNS>

azcopy copy "%srcFilePath%" "%sasUri%" --overwrite=true --recursive=true
```

## Conectar [!DNL Data Landing Zone] para [!DNL Platform]

A documentação abaixo fornece informações sobre como trazer dados de seu [!DNL Data Landing Zone] contêiner ao Adobe Experience Platform usando APIs ou a interface do usuário.

### Uso de APIs

- [Criar um [!DNL Data Landing Zone] conexão de origem usando a API do Serviço de fluxo](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Criar um fluxo de dados para uma fonte de armazenamento na nuvem usando a API do Serviço de fluxo](../../tutorials/api/collect/cloud-storage.md)

### Uso da interface

- [Conectar [!DNL Data Landing Zone] para a Platform usando a interface](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [Criar um fluxo de dados para uma conexão de armazenamento na nuvem na interface](../../tutorials/ui/dataflow/batch/cloud-storage.md)

>[!IMPORTANT]
>
>No momento, os links privados não são compatíveis ao conectar-se ao Experience Platform usando o [!DNL Data Landing Zone]. Os únicos métodos compatíveis de acesso são os métodos listados [aqui](#manage-the-contents-of-your-data-landing-zone).

