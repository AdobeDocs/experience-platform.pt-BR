---
keywords: Experience Platform;home;popular topics;Armazenamento da Google Cloud;armazenamento da nuvem do google
solution: Experience Platform
title: Visão geral do conector de origem do Armazenamento do Google Cloud
topic: overview
description: Saiba como conectar o Armazenamento do Google Cloud à Adobe Experience Platform usando APIs ou a interface do usuário.
translation-type: tm+mt
source-git-commit: a489ab248793a063295578943ad600d8eacab6a2
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 0%

---


# Conector de Armazenamento do Google Cloud

A Adobe Experience Platform fornece conectividade nativa para provedores de nuvem como AWS, [!DNL Google Cloud Platform] e [!DNL Azure], permitindo que você extraia seus dados desses sistemas.

As fontes de armazenamentos na nuvem podem trazer seus próprios dados para [!DNL Platform] sem a necessidade de baixar, formatar ou fazer upload. Os dados ingeridos podem ser formatados como XDM JSON, XDM Parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho de Fontes. [!DNL Platform] permite trazer dados de  [!DNL Google Cloud Storage] lotes.

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à sua lista de permissões pode resultar em erros ou em não desempenho ao usar fontes. Consulte a página [lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Configuração de pré-requisito para conectar sua conta [!DNL Google Cloud Storage]

Para se conectar a [!DNL Platform], é necessário primeiro habilitar a interoperabilidade para sua conta [!DNL Google Cloud Storage]. Para acessar a configuração de interoperabilidade, abra [!DNL Google Cloud Platform] e selecione **[!UICONTROL Configurações]** na opção **[!UICONTROL Armazenamento]** no painel de navegação.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

A página **[!UICONTROL Settings]** é exibida. Aqui, você pode ver informações sobre sua [!DNL Google] ID do projeto e detalhes sobre sua conta [!DNL Google Cloud Storage]. Para acessar as configurações de interoperabilidade, selecione **[!UICONTROL Interoperabilidade]** no cabeçalho superior.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

A página **[!UICONTROL Interoperabilidade]** contém informações sobre autenticação, chaves de acesso e o projeto padrão associado à sua conta de usuário. Se você ainda não tiver estabelecido um projeto padrão para acesso interoperável, poderá configurar um projeto na seção **[!UICONTROL Projeto padrão para acesso interoperável]**. Se um projeto padrão já tiver sido estabelecido, a seção mostrará uma confirmação de que um projeto foi definido como padrão.

Para gerar uma nova ID de chave de acesso e uma chave de acesso secreta para sua conta de usuário, selecione **[!UICONTROL Criar uma chave]**.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

Você pode usar a ID da chave de acesso recém-gerada e a chave de acesso secreta para conectar sua conta [!DNL Google Cloud Storage] a [!DNL Platform].

## Restrições de nomenclatura para arquivos e diretórios

A seguir, há uma lista de restrições que você deve levar em conta ao nomear seu arquivo ou diretório de armazenamento na nuvem.

- Nomes de diretório e de componente de arquivo não podem exceder 255 caracteres.
- Os nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
- Os seguintes caracteres de URL reservados devem ser escapados corretamente: `! * ' ( ) ; : @ & = + $ , / ? % # [ ]`
- Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
- Caracteres de caminho de URL ilegais não permitidos. Pontos de código como `\uE000`, embora válidos em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode, como caracteres de controle (0x00 a 0x1F, \u0081 etc.), também não são permitidos. Para obter as regras que regem strings Unicode em HTTP/1.1, consulte [RFC 2616, Seção 2.2: Regras básicas](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (..) e dois caracteres de ponto (.).

## Conectar [!DNL Google Cloud Storage] a [!DNL Platform]

A documentação abaixo fornece informações sobre como conectar [!DNL Google Cloud Storage] a [!DNL Platform] usando APIs ou a interface do usuário:

### Uso de APIs

- [Criar uma conexão de origem de Armazenamento do Google Cloud usando a API de Serviço de Fluxo](../../tutorials/api/create/cloud-storage/google.md)
- [Explore um sistema de armazenamento em nuvem usando a API de Serviço de Fluxo](../../tutorials/api/explore/cloud-storage.md)
- [Coletar dados de armazenamento na nuvem usando a API de Serviço de Fluxo](../../tutorials/api/collect/cloud-storage.md)

### Uso da interface

- [Criar uma conexão de origem de Armazenamento do Google Cloud na interface do usuário](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Configurar um fluxo de dados para uma conexão de armazenamento em nuvem na interface do usuário](../../tutorials/ui/dataflow/batch/cloud-storage.md)