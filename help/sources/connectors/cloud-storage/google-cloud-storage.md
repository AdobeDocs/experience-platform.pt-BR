---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conector de Armazenamento do Google Cloud
topic: overview
translation-type: tm+mt
source-git-commit: 0ed2ed3b08f262100746f255a78c248a1748eb5e
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# Conector de Armazenamento do Google Cloud

A plataforma Adobe Experience fornece conectividade nativa para provedores de nuvem como AWS, plataforma Google Cloud e Azure, permitindo que você traga seus dados desses sistemas.

As fontes de armazenamentos na nuvem podem trazer seus próprios dados para a Plataforma sem a necessidade de baixar, formatar ou fazer upload. Os dados ingeridos podem ser formatados como XDM JSON, XDM parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho de Fontes. A plataforma permite trazer dados do Armazenamento do Google Cloud por lotes.

## Configuração de pré-requisito para conectar sua conta de Armazenamento do Google Cloud

Para se conectar à plataforma, é necessário primeiro habilitar a interoperabilidade para sua conta de Armazenamento da Google Cloud. Para acessar a configuração de interoperabilidade, abra a Plataforma do Google Cloud e selecione **[!UICONTROL Configurações]** na opção **[!UICONTROL Armazenamento]** no painel de navegação.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

A página **[!UICONTROL Configurações]** é exibida. Aqui, você pode ver informações sobre sua ID de projeto do Google e detalhes sobre sua conta de Armazenamento do Google Cloud. Para acessar as configurações de interoperabilidade, selecione **[!UICONTROL Interoperabilidade]** no cabeçalho superior.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

A página **[!UICONTROL Interoperabilidade]** contém informações sobre autenticação, chaves de acesso e o projeto padrão associado à sua conta de usuário. Se você ainda não tiver estabelecido um projeto padrão para acesso interoperável, poderá configurar um projeto a partir do projeto *[!UICONTROL Padrão para a seção de acesso]* interoperável. Se um projeto padrão já tiver sido estabelecido, a seção mostrará uma confirmação de que um projeto foi definido como padrão.

Para gerar uma nova ID de chave de acesso e uma chave de acesso secreta para sua conta de usuário, selecione **[!UICONTROL Criar uma chave]**.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

Você pode usar a ID da chave de acesso recém-gerada e a chave de acesso secreta para conectar sua conta do Armazenamento do Google Cloud à Plataforma.

A documentação abaixo fornece informações sobre como conectar o Armazenamento do Google Cloud à plataforma usando APIs ou a interface do usuário:

## Conectar o Armazenamento do Google Cloud à plataforma

A documentação abaixo fornece informações sobre como conectar o Armazenamento do Google Cloud à plataforma usando APIs ou a interface do usuário:

### Uso de APIs

- [Criar um conector de Armazenamento do Google Cloud usando a API de Serviço de Fluxo](../../tutorials/api/create/cloud-storage/google.md)
- [Explore um sistema de armazenamento em nuvem usando a API de Serviço de Fluxo](../../tutorials/api/explore/cloud-storage.md)
- [Coletar dados de armazenamento na nuvem usando a API de Serviço de Fluxo](../../tutorials/api/collect/cloud-storage.md)

### Uso da interface

- [Criar um conector de origem de Armazenamento do Google Cloud na interface do usuário](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Configurar um fluxo de dados para um conector de armazenamento em nuvem na interface do usuário](../../tutorials/ui/dataflow/batch/cloud-storage.md)