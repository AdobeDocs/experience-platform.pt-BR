---
keywords: Azure Blob; destino Blob; s3; destino de blob do azure
title: Conexão Blob do Azure
description: Crie uma conexão de saída em tempo real com o armazenamento do Azure Blob para exportar periodicamente arquivos de dados CSV do Adobe Experience Platform.
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: b4810dfef7b0d437744ca14a32bd4f5746e8d002
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 1%

---

# [!DNL Azure Blob] conexão

## Visão geral {#overview}

[!DNL Azure Blob] (a seguir designada [!DNL Blob]) é a solução de armazenamento de objetos da Microsoft para a nuvem. Este tutorial fornece etapas para criar um [!DNL Blob] destino usando o [!DNL Platform] interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial do Editor de esquemas](../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL Blob] no destino, você pode ignorar o restante deste documento e prosseguir para o tutorial em [como ativar segmentos no seu destino](../../ui/activate-batch-profile-destinations.md).

## Formatos de arquivo não suportados {#file-formats}

[!DNL Experience Platform] O suporta o seguinte formato de arquivo a ser exportado para [!DNL Blob]:

* Valores separados por delimitador (DSV): No momento, o suporte para arquivos de dados formatados em DSV está limitado a valores separados por vírgula. O suporte para arquivos DSV gerais será fornecido no futuro.

## Conecte-se ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configuração](../../ui/connect-destination.md) nesse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Cadeia de conexão]**: a string de conexão é necessária para acessar dados no armazenamento do Blob. O [!DNL Blob] o padrão da string de conexão começa com: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * Para obter mais informações sobre como configurar seu [!DNL Blob] string de conexão, consulte [Configurar uma cadeia de conexão para uma conta de armazenamento do Azure](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) na documentação do Microsoft.

* Opcionalmente, é possível anexar sua chave pública formatada em RSA para adicionar criptografia aos arquivos exportados. Sua chave pública deve ser escrita como uma [!DNL Base64] sequência de caracteres codificada.
* **[!UICONTROL Nome]**: insira um nome que ajudará a identificar esse destino.
* **[!UICONTROL Descrição]**: insira uma descrição deste destino.
* **[!UICONTROL Caminho da pasta]**: insira o caminho para a pasta de destino que hospedará os arquivos exportados.
* **[!UICONTROL Contêiner]**: digite o nome do [!DNL Azure Blob Storage] contêiner a ser usado por este destino.

Opcionalmente, é possível anexar sua chave pública formatada em RSA para adicionar criptografia aos arquivos exportados. Sua chave pública deve ser escrita como uma [!DNL Base64] sequência de caracteres codificada.

## Ativar segmentos para este destino {#activate}

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.
