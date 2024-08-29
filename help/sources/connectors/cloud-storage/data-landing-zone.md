---
keywords: Experience Platform;página inicial;tópicos populares
solution: Experience Platform
title: Source da zona de aterrissagem de dados
description: Saiba como conectar a Data Landing Zone ao Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: ecef17ed454c7b1f30543278bba6b0e3b70399da
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

>[!IMPORTANT]
>
>Esta página é específica para o conector de [!DNL Data Landing Zone] *origem* no Experience Platform. Para obter informações sobre como se conectar ao conector de [!DNL Data Landing Zone] *destino*, consulte a [[!DNL Data Landing Zone] página de documentação de destino](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

O [!DNL Data Landing Zone] é uma interface de armazenamento do [!DNL Azure Blob] provisionada pela Adobe Experience Platform, que concede a você acesso a um recurso de armazenamento de arquivos seguro e baseado em nuvem para trazer arquivos para a Platform. Você tem acesso a um contêiner [!DNL Data Landing Zone] por sandbox, e o volume total de dados em todos os contêineres é limitado ao total de dados fornecidos com sua licença de Produtos e Serviços da Plataforma. Todos os clientes do Experience Platform são provisionados com um contêiner [!DNL Data Landing Zone] por sandbox. Você pode ler e gravar arquivos no seu contêiner por meio do [!DNL Azure Storage Explorer] ou da interface de linha de comando.

O [!DNL Data Landing Zone] oferece suporte à autenticação baseada em SAS e seus dados estão protegidos com mecanismos de segurança de armazenamento [!DNL Azure Blob] padrão em repouso e em trânsito. A autenticação baseada em SAS permite que você acesse com segurança o contêiner do [!DNL Data Landing Zone] por meio de uma conexão pública com a Internet. Não há alterações de rede necessárias para você acessar o contêiner [!DNL Data Landing Zone], o que significa que você não precisa definir nenhuma configuração de lista de permissões ou entre regiões para sua rede. O Experience Platform impõe um tempo de expiração estrito de sete dias em todos os arquivos e pastas carregados em um contêiner [!DNL Data Landing Zone]. Todos os arquivos e pastas são excluídos após sete dias.

>[!NOTE]
>
>Para acessar [!DNL Data Landing Zone] de [!DNL Azure Data Factory], você deve criar um serviço vinculado para [!DNL Data Landing Zone] usando as [credenciais SAS](../../tutorials/ui/create/cloud-storage/data-landing-zone.md#retrieve-your-data-landing-zone-credentials) fornecidas pelo Experience Platform. Depois de criar o serviço vinculado, você pode explorar o [!DNL Data Landing Zone] selecionando o caminho do contêiner em vez do caminho raiz padrão.

## Restrições de nomenclatura para arquivos e diretórios

Veja a seguir uma lista de restrições que você deve considerar ao nomear seus arquivos ou diretórios de armazenamento em nuvem.

- Os nomes dos componentes de diretório e arquivo não podem exceder 255 caracteres.
- Nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
- Os seguintes caracteres de URL reservados devem ter um escape adequado: `! ' ( ) ; @ & = + $ , % # [ ]`
- Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
- Caracteres de caminho de URL inválidos não permitidos. Pontos de código como `\uE000`, embora válidos em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode, como caracteres de controle (como `0x00` a `0x1F`, `\u0081` e assim por diante), também não são permitidos. Para regras que regem cadeias de caracteres Unicode em HTTP/1.1, consulte [RFC 2616, Seção 2.2: Regras Básicas](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (.) e dois caracteres de ponto (..).

## Gerenciar o conteúdo da Data Landing Zone{#manage-the-contents-of-your-data-landing-zone}

Você pode usar o [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/features/storage-explorer/) para gerenciar o conteúdo do seu contêiner [!DNL Data Landing Zone].

Na interface do usuário do [!DNL Azure Storage Explorer], selecione o ícone de conexão no menu de navegação esquerdo. A janela **Selecionar Recurso** é exibida, fornecendo opções para conexão. Selecione **[!DNL Blob container]** para se conectar a [!DNL Data Landing Zone].

![selecionar-recurso](../../images/tutorials/create/dlz/select-resource.png)

Em seguida, selecione **SAS (URL de assinatura de acesso compartilhado)** como seu método de conexão e selecione **Avançar**.

![selecionar método-conexão](../../images/tutorials/create/dlz/select-connection-method.png)

Depois de selecionar seu método de conexão, você deve fornecer um **nome para exibição** e a URL SAS do contêiner **[!DNL Blob]** que corresponda ao seu contêiner [!DNL Data Landing Zone].

>[!TIP]
>
>Você pode recuperar suas credenciais do [!DNL Data Landing Zone] do catálogo de fontes na interface do usuário da plataforma.

Forneça a URL SAS do [!DNL Data Landing Zone] e selecione **Avançar**

![inserir-informações-conexão](../../images/tutorials/create/dlz/enter-connection-info.png)

A janela **Resumo** é exibida, fornecendo uma visão geral das configurações, incluindo informações sobre o ponto de extremidade e as permissões do [!DNL Blob]. Quando estiver pronto, selecione **Conectar**.

![resumo](../../images/tutorials/create/dlz/summary.png)

Uma conexão bem-sucedida atualiza a interface do usuário [!DNL Azure Storage Explorer] com o contêiner [!DNL Data Landing Zone].

![dlz-user-container](../../images/tutorials/create/dlz/dlz-user-container.png)

Com o contêiner [!DNL Data Landing Zone] conectado ao [!DNL Azure Storage Explorer], você pode começar a carregar arquivos no contêiner [!DNL Data Landing Zone]. Para carregar, selecione **Carregar** e **Carregar Arquivos**.

![carregar](../../images/tutorials/create/dlz/upload.png)

Depois de selecionar o arquivo que deseja carregar, você deve identificar o tipo [!DNL Blob] com o qual deseja carregá-lo e o diretório de destino desejado. Quando terminar, selecione **Carregar**.

| [!DNL Blob] tipos | Descrição |
| --- | --- |
| Bloquear [!DNL Blob] | Os blocos [!DNL Blobs] estão otimizados para carregar grandes quantidades de dados de maneira eficiente. Bloquear [!DNL Blobs] é a opção padrão para [!DNL Data Landing Zone]. |
| Acrescentar [!DNL Blob] | Os acréscimos [!DNL Blobs] são otimizados para anexar dados ao final do arquivo. |

![arquivos de carregamento](../../images/tutorials/create/dlz/upload-files.png)

## Carregar arquivos no [!DNL Data Landing Zone] usando a interface de linha de comando

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

## Conectar [!DNL Data Landing Zone] a [!DNL Platform]

A documentação abaixo fornece informações sobre como trazer dados do seu contêiner do [!DNL Data Landing Zone] para a Adobe Experience Platform usando APIs ou a interface do usuário.

### Uso de APIs

- [Criar uma conexão de origem  [!DNL Data Landing Zone]  usando a API de Serviço de Fluxo](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Criar um fluxo de dados para uma fonte de armazenamento na nuvem usando a API do Serviço de fluxo](../../tutorials/api/collect/cloud-storage.md)

### Uso da interface

- [Conectar [!DNL Data Landing Zone] à Plataforma usando a interface](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [Criar um fluxo de dados para uma conexão de armazenamento na nuvem na interface](../../tutorials/ui/dataflow/batch/cloud-storage.md)

>[!IMPORTANT]
>
>No momento, não há suporte para links privados ao conectar-se ao Experience Platform usando o [!DNL Data Landing Zone]. Os únicos métodos suportados para acesso são os métodos listados [aqui](#manage-the-contents-of-your-data-landing-zone).

