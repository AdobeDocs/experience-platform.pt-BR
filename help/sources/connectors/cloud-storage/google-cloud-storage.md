---
keywords: Experience Platform;página inicial;tópicos populares;Google Cloud Storage;google cloud storage
solution: Experience Platform
title: Visão geral do Google Cloud Storage Source Connector
description: Saiba como conectar o Google Cloud Storage ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: f7ebd213-f914-4c49-aebd-1df4514ffec0
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# Conector do Google Cloud Storage

>[!IMPORTANT]
>
>Agora você pode usar a origem [!DNL Google Cloud Storage] ao executar o Adobe Experience Platform no Amazon Web Services (AWS). O Experience Platform em execução no AWS está disponível atualmente para um número limitado de clientes. Para saber mais sobre a infraestrutura do Experience Platform compatível, consulte a [visão geral da nuvem múltipla do Experience Platform](../../../landing/multi-cloud.md).

O Adobe Experience Platform fornece conectividade nativa para provedores de nuvem, como o AWS, o [!DNL Google Cloud Platform] e o [!DNL Azure], permitindo que você traga seus dados desses sistemas.

As fontes de armazenamento na nuvem podem trazer seus próprios dados para a Experience Platform sem a necessidade de baixar, formatar ou carregar. Os dados assimilados podem ser formatados como JSON ou Parquet compatível com o Experience Data Model (XDM) ou em um formato delimitado. Cada etapa do processo é integrada ao fluxo de trabalho de origens. O Experience Platform permite trazer dados de [!DNL Google Cloud Storage] por meio de lotes.

## INCLUO NA LISTA DE PERMISSÕES de endereços IP

Você deve adicionar endereços IP específicos da região ao incluo na lista de permissões antes de conectar suas fontes à Experience Platform. Para obter mais informações, leia o guia sobre [como ler os endereços IP de incluir na lista de permissões para se conectar ao Experience Platform](../../ip-address-allow-list.md) para obter mais informações.

## Pré-requisito de configuração para conectar sua conta do [!DNL Google Cloud Storage]

Para se conectar ao Experience Platform, primeiro você deve habilitar a interoperabilidade para sua conta [!DNL Google Cloud Storage]. Para acessar a configuração de interoperabilidade, abra o [!DNL Google Cloud Platform] e selecione **[!UICONTROL Settings]** na opção **[!UICONTROL Cloud Storage]** no painel de navegação.

<!-- ![](../../images/tutorials/create/google-cloud-storage/nav.png) -->

A página **[!UICONTROL Settings]** é exibida. Aqui, você pode ver informações sobre sua ID de projeto do [!DNL Google] e detalhes sobre sua conta do [!DNL Google Cloud Storage]. Para acessar as configurações de interoperabilidade, selecione **[!UICONTROL Interoperability]** no cabeçalho superior.

<!-- ![](../../images/tutorials/create/google-cloud-storage/project-access.png) -->

A página **[!UICONTROL Interoperability]** contém informações sobre autenticação, chaves de acesso e o projeto padrão associado à sua conta de serviço. Para gerar uma nova ID de chave de acesso e uma chave de acesso secreta para sua conta de serviço, selecione **[!UICONTROL Create a Key for a Service Account]**.

<!-- ![](../../images/tutorials/create/google-cloud-storage/interoperability.png) -->

Você pode usar a ID da chave de acesso recém-gerada e a chave de acesso secreta para conectar sua conta do [!DNL Google Cloud Storage] à Experience Platform.

Para obter mais informações, leia o manual sobre [criação e gerenciamento de chaves de conta de serviço](https://cloud.google.com/iam/docs/creating-managing-service-account-keys) na documentação [!DNL Google Cloud].

## Restrições de nomenclatura para arquivos e diretórios

Veja a seguir uma lista de restrições que você deve considerar ao nomear seu arquivo ou diretório de armazenamento em nuvem.

- Os nomes dos componentes de diretório e arquivo não podem exceder 255 caracteres.
- Nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
- Os seguintes caracteres de URL reservados devem ter um escape adequado: `! ' ( ) ; @ & = + $ , % # [ ]`
- Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
- Caracteres de caminho de URL inválidos não permitidos. Pontos de código como `\uE000`, embora válidos em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode, como caracteres de controle (0x00 a 0x1F, \u0081 etc.), também não são permitidos. Para regras que regem cadeias de caracteres Unicode em HTTP/1.1, consulte [RFC 2616, Seção 2.2: Regras Básicas](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (.) e dois caracteres de ponto (..).

## Conectar [!DNL Google Cloud Storage] ao Experience Platform

A documentação abaixo fornece informações sobre como conectar o [!DNL Google Cloud Storage] ao Experience Platform usando APIs ou a interface do usuário:

### Uso de APIs

- [Criar uma conexão básica do Google Cloud Storage usando a API do Serviço de fluxo](../../tutorials/api/create/cloud-storage/google.md)
- [Explore a estrutura de dados e o conteúdo de uma fonte de armazenamento na nuvem usando a API do serviço de fluxo](../../tutorials/api/explore/cloud-storage.md)
- [Criar um fluxo de dados para uma fonte de armazenamento na nuvem usando a API do Serviço de fluxo](../../tutorials/api/collect/cloud-storage.md)

### Uso da interface

- [Criar uma conexão de origem do Google Cloud Storage na interface](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Criar um fluxo de dados para uma conexão de armazenamento na nuvem na interface](../../tutorials/ui/dataflow/batch/cloud-storage.md)
