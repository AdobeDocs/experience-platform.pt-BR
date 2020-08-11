---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem Gen2 do Armazenamento Azure Data Lake na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 1%

---


# Criar um conector [!DNL Azure Data Lake Storage Gen2] de origem na interface do usuário

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para autenticação de um conector de origem [!DNL Azure Data Lake Storage Gen2] (a seguir denominado &quot;ADLS Gen2&quot;) usando a interface do [!DNL Platform] usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
- [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão básica ADLS Gen2, poderá ignorar o restante desse documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Reunir credenciais obrigatórias

Para autenticar seu conector de origem ADLS Gen2, é necessário fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `url` | O endpoint para ADLS Gen2. |
| `servicePrincipalId` | A ID do cliente do aplicativo. |
| `servicePrincipalKey` | A chave do aplicativo. |
| `tenant` | As informações do locatário que contêm seu aplicativo. |

Para obter mais informações sobre esses valores, consulte [este documento](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage)ADLS Gen2.

## Conectar sua conta ADLS Gen2

Depois de reunir as credenciais necessárias, siga as etapas abaixo para criar uma nova conexão básica de entrada para vincular sua conta ADLS Gen2 a [!DNL Platform].

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho *[!UICONTROL Fontes]* . A guia *[!UICONTROL Catálogo]* exibe diversas fontes para as quais é possível usar para criar conexões de base de entrada. Cada fonte mostra o número de conexões base existentes associadas a elas.

Na categoria *[!UICONTROL do Armazenamento]* Cloud, selecione **[!UICONTROL Azure Data Lake Gen2]** para exibir uma barra de informações no lado direito da tela. A barra de informações fornece uma breve descrição para a fonte selecionada, bem como opções para se conectar com a visualização de origem em sua documentação. Para criar uma nova conexão básica de entrada, clique em **[!UICONTROL Adicionar dados]**.

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

A caixa de diálogo *[!UICONTROL Conectar-se ao Azure Data Lake Gen2]* é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais ADLS Gen2. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conexão básica ser estabelecida.

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### Conta existente

Para conectar uma conta existente, selecione a conta ADLS Gen2 com a qual você deseja se conectar e selecione **[!UICONTROL Avançar]** para continuar.

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão básica com sua conta ADLS Gen2. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados do seu armazenamento em nuvem para a Plataforma](../../dataflow/batch/cloud-storage.md).