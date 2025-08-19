---
title: Visão geral do Azure Blob Source Connector
description: Saiba como conectar sua conta do Azure Blob à Experience Platform
exl-id: 62adc74f-3570-42c7-9ae6-3ddbc09eccc7
source-git-commit: f659d78eebc1c5e74021f9a41a2a489389a6588e
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 0%

---

# [!DNL Azure Blob Storage] origem

[!DNL Azure Blob Storage] é um serviço de armazenamento de objetos baseado na nuvem fornecido por [!DNL Microsoft Azure]. Ele foi projetado para armazenar grandes quantidades de dados não estruturados, como texto, imagens, vídeos, backups e registros. Você pode usar o [!DNL Azure Blob Storage] para armazenar e gerenciar grandes quantidades de dados não estruturados, como documentos, imagens, vídeos e arquivos de áudio. É ideal para backup e arquivamento de dados, suporte à recuperação de desastres e tratamento de cargas de trabalho de big data para análise.

Use a origem [!DNL Azure Blob Storage] para conectar sua conta e assimilar dados de [!DNL Azure Blob Storage] para a Adobe Experience Platform.

## Pré-requisitos {#prerequisites}

Leia as seções a seguir para concluir a configuração de pré-requisito antes de conectar sua conta do [!DNL Azure Blob Storage] à Experience Platform.

### INCLUIR NA LISTA DE PERMISSÕES endereço IP

Você deve adicionar endereços IP específicos da sua região ao incluo na lista de permissões antes de conectar suas fontes à Experience Platform. Leia o manual sobre [Como Experience Platform endereços IP para conexão com o incluir na lista de permissões](../../ip-address-allow-list.md) para obter mais informações.

>[!IMPORTANT]
>
>A origem [!DNL Azure Blob] não dá suporte à conectividade da mesma região com o Experience Platform. Se a instância do [!DNL Azure] estiver usando a mesma região de rede que o Experience Platform, não será possível estabelecer uma conexão com as origens do Experience Platform. Atualmente, somente a conectividade entre regiões é compatível.

### Restrições de nomenclatura para arquivos e diretórios

Veja a seguir uma lista de restrições que você deve considerar ao nomear seu arquivo ou diretório de armazenamento em nuvem.

- Os nomes dos componentes de diretório e arquivo não podem exceder 255 caracteres.
- Nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
- Os seguintes caracteres de URL reservados devem ter um escape adequado: `! ' ( ) ; @ & = + $ , % # [ ]`
- Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
- Caracteres de caminho de URL inválidos não permitidos. Pontos de código como `\uE000`, embora válidos em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode, como caracteres de controle (0x00 a 0x1F, \u0081 etc.), também não são permitidos. Para regras que regem cadeias de caracteres Unicode em HTTP/1.1, consulte [RFC 2616, Seção 2.2: Regras Básicas](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (.) e dois caracteres de ponto (..).

### Autenticar [!DNL Azure Blob Storage] no Experience Platform {#authentication}

Você pode conectar sua conta do [!DNL Azure Blob Storage] à Experience Platform usando estes tipos de autenticação:

- **Autenticação da chave da conta**: usa a chave de acesso da conta de armazenamento para autenticar e conectar-se à sua conta do [!DNL Azure Blob Storage].
- **Assinatura de acesso compartilhado (SAS)**: usa um URI SAS para fornecer acesso delegado e limitado por tempo aos recursos da sua conta [!DNL Azure Blob Storage].
- **Autenticação baseada na entidade de serviço**: usa uma entidade de serviço do Azure Ative Diretory (AAD) (ID de cliente e segredo) para autenticar com segurança em sua conta de Armazenamento de Blobs do Azure.

>[!BEGINTABS]

>[!TAB Autenticação da chave da conta]

Forneça valores para as credenciais a seguir para conectar sua conta do [!DNL Azure Blob Storage] à Experience Platform usando a autenticação de chave de conta.

| Credencial | Descrição |
| --- | --- |
| `connectionString` | A cadeia de conexão [!DNL Azure Blob Storage] da sua conta de armazenamento. Esta cadeia de caracteres contém as informações necessárias para a autenticação e a conexão com a instância do [!DNL Azure Blob Storage]. Formato de exemplo: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY};EndpointSuffix=core.windows.net` |
| `container` | O nome do container [!DNL Azure Blob Storage] onde seus arquivos de dados são armazenados. Um contêiner organiza um conjunto de blobs, semelhante a um diretório em um sistema de arquivos. |
| `folderPath` | O caminho dentro do container especificado onde seus arquivos estão localizados. Esse é um caminho de subdiretório opcional (pasta virtual) dentro do container. Se deixado em branco, a raiz do contêiner será usada. |
| `connectionSpec.id` | A ID de especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID de especificação da conexão para [!DNL Azure Blob Storage] é `4c10e202-c428-4796-9208-5f1f5732b1cf`. **Observação**: esta credencial é necessária somente ao conectar-se por meio da API [!DNL Flow Service]. |

Para saber mais sobre como usar a autenticação de chave de conta com o [!DNL Azure Blob Storage], leia o [guia de autenticação oficial do Microsoft Azure](https://learn.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage?tabs=data-factory#account-key-authentication).

>[!TAB Assinatura de acesso compartilhado]

Forneça valores para as credenciais a seguir para conectar sua conta do [!DNL Azure Blob Storage] à Experience Platform usando assinatura de acesso compartilhado.

| Credencial | Descrição |
| --- | --- |
| `SasURI` | O URI de assinatura de acesso compartilhado que você pode usar como um tipo de autenticação alternativo para conectar sua conta. O padrão do URI SAS é: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}`. Para obter mais informações, consulte este documento [!DNL Azure] em [URIs de assinatura de acesso compartilhado](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| `container` | O nome do container [!DNL Azure Blob Storage] onde seus arquivos de dados são armazenados. Um contêiner organiza um conjunto de blobs, semelhante a um diretório em um sistema de arquivos. |
| `folderPath` | O caminho dentro do container especificado onde seus arquivos estão localizados. Esse é um caminho de subdiretório opcional (pasta virtual) dentro do container. Se deixado em branco, a raiz do contêiner será usada. |
| `connectionSpec.id` | A ID de especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID de especificação da conexão para [!DNL Azure Blob Storage] é `4c10e202-c428-4796-9208-5f1f5732b1cf`. **Observação**: esta credencial é necessária somente ao conectar-se por meio da API [!DNL Flow Service]. |

Para saber mais sobre como usar a assinatura de acesso compartilhado com o [!DNL Azure Blob Storage], leia o [guia de autenticação oficial do Microsoft Azure](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication).

>[!TAB Autenticação baseada na entidade de serviço]

Forneça valores para as credenciais a seguir para conectar sua conta do [!DNL Azure Blob Storage] à Experience Platform usando a autenticação baseada na entidade de serviço.

| Credencial | Descrição |
| --- | --- |
| `serviceEndpoint` | A URL do ponto de extremidade da sua conta [!DNL Azure Blob Storage]. Normalmente no formato: `https://{ACCOUNT_NAME}.blob.core.windows.net`. |
| `accountKind` | O tipo da sua conta [!DNL Azure Blob Storage]. Valores comuns incluem `StorageV2`, `BlobStorage` ou `Storage`. |
| `servicePrincipalId` | A ID do cliente/aplicativo da entidade de serviço do Azure Ative Diretory (AAD) usada para autenticação. |
| `servicePrincipalKey` | O segredo do cliente ou a senha associada à entidade de serviço do Azure. |
| `tenant` | A ID do locatário do Azure Ative Diretory (AAD) em que a entidade de serviço está registrada. |
| `container` | O nome do contêiner do Armazenamento Azure Blob em que seus arquivos de dados são armazenados. |
| `folderPath` | O caminho dentro do container especificado onde seus arquivos estão localizados. Esse é um caminho de subdiretório opcional (pasta virtual) dentro do container. Se deixado em branco, a raiz do contêiner será usada. |
| `connectionSpec.id` | A ID de especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID de especificação da conexão para o Armazenamento Azure Blob é `4c10e202-c428-4796-9208-5f1f5732b1cf`. **Observação**: esta credencial é necessária somente ao conectar-se por meio da API [!DNL Flow Service]. |

Para saber mais sobre como usar a autenticação baseada na entidade de serviço com o [!DNL Azure Blob Storage], leia o [guia de autenticação oficial do Microsoft Azure](https://learn.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage?tabs=data-factory#service-principal-authentication).

>[!ENDTABS]

## Conectar [!DNL Azure Blob Storage] a [!DNL Experience Platform]

A documentação abaixo fornece informações sobre como conectar o Azure Blob ao Adobe Experience Platform usando APIs ou a interface do usuário:

### Uso de APIs

- [Conectar [!DNL Azure Blob Storage] ao Experience Platform](../../tutorials/api/create/cloud-storage/blob.md)
- [Explore a estrutura de dados e o conteúdo de uma fonte de armazenamento na nuvem usando a API do serviço de fluxo](../../tutorials/api/explore/cloud-storage.md)
- [Criar um fluxo de dados para uma fonte de armazenamento na nuvem usando a API do Serviço de fluxo](../../tutorials/api/collect/cloud-storage.md)

### Uso da interface

- [Conectar [!DNL Azure Blob Storage] ao Experience Platform](../../tutorials/ui/create/cloud-storage/blob.md)
- [Criar um fluxo de dados para uma conexão de armazenamento na nuvem na interface](../../tutorials/ui/dataflow/batch/cloud-storage.md)
