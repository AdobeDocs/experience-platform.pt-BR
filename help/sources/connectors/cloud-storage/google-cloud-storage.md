---
keywords: Experience Platform, home, tópicos populares, Armazenamento no Google Cloud, armazenamento na nuvem do google
solution: Experience Platform
title: Visão geral do Conector de origem de armazenamento do Google Cloud
topic-legacy: overview
description: Saiba como conectar o Armazenamento do Google Cloud à Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: f7ebd213-f914-4c49-aebd-1df4514ffec0
source-git-commit: 1f9948d6e419ee5d6a021a589378f7aa990b7291
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# Conector de armazenamento do Google Cloud

O Adobe Experience Platform fornece conectividade nativa para provedores de nuvem como AWS, [!DNL Google Cloud Platform] e [!DNL Azure], permitindo que você traga seus dados desses sistemas.

As fontes de armazenamento em nuvem podem trazer seus próprios dados para a plataforma sem precisar baixar, formatar ou fazer upload. Os dados assimilados podem ser formatados como JSON ou Parquet compatível com o Experience Data Model (XDM) ou em um formato delimitado. Cada etapa do processo é integrada ao fluxo de trabalho de fontes. A plataforma permite trazer dados de [!DNL Google Cloud Storage] por meio de lotes.

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à lista de permissões pode causar erros ou não desempenho ao usar fontes. Consulte a página [lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Configuração de pré-requisito para conectar sua conta [!DNL Google Cloud Storage]

Para se conectar à Platform, você deve primeiro habilitar a interoperabilidade para sua conta [!DNL Google Cloud Storage]. Para acessar a configuração de interoperabilidade, abra [!DNL Google Cloud Platform] e selecione **[!UICONTROL Configurações]** na opção **[!UICONTROL Armazenamento na nuvem]** no painel de navegação.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

A página **[!UICONTROL Settings]** é exibida. Aqui, você pode ver informações sobre sua ID do projeto [!DNL Google] e detalhes sobre sua conta [!DNL Google Cloud Storage]. Para acessar as configurações de interoperabilidade, selecione **[!UICONTROL Interoperability]** no cabeçalho superior.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

A página **[!UICONTROL Interoperability]** contém informações sobre autenticação, chaves de acesso e o projeto padrão associado à sua conta de serviço. Para gerar uma nova ID de chave de acesso e uma chave de acesso secreta para sua conta de serviço, selecione **[!UICONTROL Create a Key for a Service Account]**.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

Você pode usar a ID da chave de acesso recém-gerada e a chave de acesso secreta para conectar a conta [!DNL Google Cloud Storage] à Platform.

## Restrições de nomenclatura para arquivos e diretórios

Esta é uma lista de restrições que devem ser consideradas ao nomear seu arquivo ou diretório de armazenamento em nuvem.

- Os nomes de componentes de diretório e arquivo não podem exceder 255 caracteres.
- Os nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
- Os seguintes caracteres de URL reservados devem ser evitados corretamente: `! ' ( ) ; @ & = + $ , % # [ ]`
- Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
- Caracteres de caminho de URL inválidos não permitidos. Pontos de código como `\uE000`, enquanto válidos em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode, como caracteres de controle (0x00 a 0x1F, \u0081, etc.), também não são permitidos. Para regras que regem cadeias de caracteres Unicode no HTTP/1.1, consulte [RFC 2616, Seção 2.2: Regras básicas](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (...) e dois caracteres de ponto (.).

## Conectar [!DNL Google Cloud Storage] à plataforma

A documentação abaixo fornece informações sobre como se conectar [!DNL Google Cloud Storage] à Plataforma usando APIs ou a interface do usuário:

### Uso de APIs

- [Criar uma conexão básica do Armazenamento no Google Cloud usando a API do Serviço de fluxo](../../tutorials/api/create/cloud-storage/google.md)
- [Explore a estrutura de dados e o conteúdo de uma fonte de armazenamento em nuvem usando a API do Serviço de Fluxo](../../tutorials/api/explore/cloud-storage.md)
- [Criar um fluxo de dados para uma fonte de armazenamento em nuvem usando a API do Serviço de Fluxo](../../tutorials/api/collect/cloud-storage.md)

### Uso da interface do usuário

- [Criar uma conexão de origem do Armazenamento do Google Cloud na interface do usuário](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Criar um fluxo de dados para uma conexão de armazenamento em nuvem na interface do usuário do](../../tutorials/ui/dataflow/batch/cloud-storage.md)
