---
keywords: Azure Blob;destino Blob;s3;destino blob do azure
title: Destino da Conexão Blob do Azure
description: Crie uma conexão de saída ao vivo com seu armazenamento Blob do Azure para exportar periodicamente arquivos de dados delimitados por tabulação ou CSV do Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 2%

---


# [!DNL Azure Blob] conexão

[!DNL Azure Blob] (a seguir denominado &quot;[!DNL Blob]&quot;) é a solução de armazenamento de objeto da Microsoft para a nuvem. Este tutorial fornece etapas para criar um destino [!DNL Blob] usando a interface do usuário [!DNL Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   - [Noções básicas da composição](../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../xdm/tutorials/create-schema-ui.md) do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver um destino Blob válido, poderá ignorar o restante deste documento e prosseguir para o tutorial em [ativação de segmentos para o seu destino](../../ui/activate-destinations.md).

### Formatos de arquivo não suportados

[!DNL Experience Platform] suporta o seguinte formato de arquivo a ser exportado para  [!DNL Blob]:

- Valores separados por delimitador (DSV): Atualmente, o suporte para arquivos de dados formatados em DSV está limitado a valores separados por vírgulas. O suporte para arquivos DSV gerais será fornecido no futuro. Para obter mais informações sobre os arquivos suportados, leia a seção armazenamento de nuvem no tutorial em [ativação de destinos](../../ui/activate-destinations.md#esp-and-cloud-storage)

## Conecte sua conta Blob {#connect-destination}

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Destinos]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Destinos]**. A tela **[!UICONTROL Catalog]** exibe uma variedade de destinos com os quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar o destino específico com o qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Armazenamento de nuvem]**, selecione **[!UICONTROL Armazenamento Blob do Azure]**, seguido por **[!UICONTROL Ativar]**.

![Catálogo](../../assets/catalog/cloud-storage/blob/catalog.png)

A página **[!UICONTROL Conectar-se ao Armazenamento Blob do Azure]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta {#new-account}

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça a string de conexão. A string de conexão necessária para acessar dados no armazenamento Blob. O padrão da cadeia de conexão [!DNL Blob] start com: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.

Opcionalmente, você pode anexar sua chave pública formatada pelo RSA para adicionar criptografia aos arquivos exportados. Observe que essa chave pública **deve** ser gravada como uma string codificada em Base64.

![Nova conta](../../assets/catalog/cloud-storage/blob/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL Blob] com a qual você deseja se conectar e selecione **Próximo** para prosseguir.

![Conta existente](../../assets/catalog/cloud-storage/blob/existing.png)

## Autenticação {#authentication}

A página **Authentication** é exibida. No formulário de entrada exibido, forneça um nome, uma descrição opcional, o caminho da pasta e o container dos arquivos. Quando terminar, selecione **[!UICONTROL Criar destino]**.

![Autenticação](../../assets/catalog/cloud-storage/blob/authentication.png)

## Próximas etapas {#activate-segments}

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta [!DNL Blob]. Agora você pode continuar para o próximo tutorial e [ativar segmentos para o seu destino](../../ui/activate-destinations.md).
