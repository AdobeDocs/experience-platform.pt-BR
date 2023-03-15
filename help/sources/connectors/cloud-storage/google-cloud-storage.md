---
keywords: Experience Platform;página inicial;tópicos populares;Google Cloud Storage;google cloud storage
solution: Experience Platform
title: Visão geral do Conector de origem do Google Cloud Storage
description: Saiba como conectar o Google Cloud Storage ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: f7ebd213-f914-4c49-aebd-1df4514ffec0
source-git-commit: ae22e423119bf378a068349d481f0717a75171bb
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# Conector do Google Cloud Storage

O Adobe Experience Platform fornece conectividade nativa para provedores de nuvem, como o AWS, [!DNL Google Cloud Platform], e [!DNL Azure], permitindo que você traga seus dados desses sistemas.

As fontes de armazenamento na nuvem podem trazer seus próprios dados para a Platform sem a necessidade de baixar, formatar ou carregar. Os dados assimilados podem ser formatados como JSON ou Parquet compatível com o Experience Data Model (XDM) ou em um formato delimitado. Cada etapa do processo é integrada ao fluxo de trabalho de origens. A Platform permite trazer dados de [!DNL Google Cloud Storage] em lotes.

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a [LISTA DE PERMISSÕES de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Pré-requisito de configuração para a conexão com o [!DNL Google Cloud Storage] account

Para se conectar à Platform, você deve primeiro habilitar a interoperabilidade para o seu [!DNL Google Cloud Storage] conta. Para acessar a configuração de interoperabilidade, abra [!DNL Google Cloud Platform] e selecione **[!UICONTROL Configurações]** do **[!UICONTROL Armazenamento na nuvem]** no painel de navegação.

<!-- ![](../../images/tutorials/create/google-cloud-storage/nav.png) -->

A variável **[!UICONTROL Configurações]** é exibida. Aqui, você pode ver informações sobre o seu [!DNL Google] ID do projeto e detalhes sobre o [!DNL Google Cloud Storage] conta. Para acessar as configurações de interoperabilidade, selecione **[!UICONTROL Interoperabilidade]** no cabeçalho superior.

<!-- ![](../../images/tutorials/create/google-cloud-storage/project-access.png) -->

A variável **[!UICONTROL Interoperabilidade]** Esta página contém informações sobre autenticação, chaves de acesso e o projeto padrão associado à sua conta de serviço. Para gerar uma nova ID de chave de acesso e uma chave de acesso secreta para sua conta de serviço, selecione **[!UICONTROL Criar uma Chave para uma Conta de Serviço]**.

<!-- ![](../../images/tutorials/create/google-cloud-storage/interoperability.png) -->

Você pode usar a ID da chave de acesso recém-gerada e a chave de acesso secreta para conectar [!DNL Google Cloud Storage] para a Platform.

Para obter mais informações, leia o guia em [criando e gerenciando chaves de conta de serviço](https://cloud.google.com/iam/docs/creating-managing-service-account-keys) do [!DNL Google Cloud] documentação.

## Restrições de nomenclatura para arquivos e diretórios

Veja a seguir uma lista de restrições que você deve considerar ao nomear seu arquivo ou diretório de armazenamento em nuvem.

- Os nomes dos componentes de diretório e arquivo não podem exceder 255 caracteres.
- Nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
- Os seguintes caracteres de URL reservados devem ter escape adequado: `! ' ( ) ; @ & = + $ , % # [ ]`
- Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
- Caracteres de caminho de URL inválidos não permitidos. Pontos de código como `\uE000`, embora sejam válidos em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode, como caracteres de controle (0x00 a 0x1F, \u0081 etc.), também não são permitidos. Para obter as regras que regem strings Unicode em HTTP/1.1, consulte [RFC 2616, Seção 2.2: regras básicas](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (.) e dois caracteres de ponto (..).

## Conectar [!DNL Google Cloud Storage] para a Platform

A documentação abaixo fornece informações sobre como se conectar [!DNL Google Cloud Storage] para a Platform usando APIs ou a interface do usuário:

### Uso de APIs

- [Criar uma conexão básica do Google Cloud Storage usando a API do Serviço de fluxo](../../tutorials/api/create/cloud-storage/google.md)
- [Explore a estrutura de dados e o conteúdo de uma fonte de armazenamento na nuvem usando a API do serviço de fluxo](../../tutorials/api/explore/cloud-storage.md)
- [Criar um fluxo de dados para uma fonte de armazenamento na nuvem usando a API do Serviço de fluxo](../../tutorials/api/collect/cloud-storage.md)

### Uso da interface

- [Criar uma conexão de origem do Google Cloud Storage na interface](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Criar um fluxo de dados para uma conexão de armazenamento na nuvem na interface](../../tutorials/ui/dataflow/batch/cloud-storage.md)
