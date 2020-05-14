---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem do Armazenamento de Arquivo do Azure na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: b8ebe57482fdd10ccd8bdcf1a86009a373ea579e
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---


# Criar um conector de origem do Armazenamento de Arquivo do Azure na interface do usuário

>[!NOTE]
>O Armazenamento de Tabela do Azure está em beta. Os recursos e a documentação estão sujeitos a alterações.

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para autenticação de um conector de origem do Armazenamento de Arquivo do Azure usando a interface do usuário da Plataforma.

## Introdução

Este tutorial requer uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

- [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual a plataforma Experience organiza os dados da experiência do cliente.
   - [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
- [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão com o Armazenamento File, poderá ignorar o restante desse documento e prosseguir para o tutorial sobre como [configurar um dataflow](../../dataflow/batch/cloud-storage.md).

### Reunir credenciais obrigatórias

Para autenticar seu conector de origem do Armazenamento de Arquivo do Azure, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O ponto de extremidade da instância do Armazenamento de Arquivo do Azure que você está acessando. |
| `userId` | O usuário com acesso suficiente ao ponto de extremidade do Armazenamento do Arquivo do Azure. |
| `password` | A chave de acesso do Armazenamento de Arquivo do Azure. |

Para obter mais informações sobre a introdução, consulte [este documento](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows)de Armazenamento de Arquivo do Azure.

## Ligar a sua conta do Armazenamento de Ficheiros do Azure

Depois de reunir as credenciais necessárias, siga as etapas abaixo para criar uma nova conta do Armazenamento de Arquivo do Azure para se conectar à Plataforma.

Faça logon na [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho *[!UICONTROL Fontes]* . A tela *[!UICONTROL Catálogo]* exibe várias fontes nas quais você pode criar uma conta de entrada e cada fonte mostra o número de contas e fluxos de dados existentes associados a elas.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria *[!UICONTROL Bancos]* de Dados, selecione Armazenamento **[!UICONTROL Arquivo do]** Azure clique **no ícone + (+)** para criar um novo conector de Armazenamento de Arquivo do Azure.

![catálogo](../../../../images/tutorials/create/azure-file-storage/catalog.png)

A página *[!UICONTROL Conectar-se ao Armazenamento]* de Arquivo do Azure é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça à conexão um nome, uma descrição opcional e suas credenciais de Armazenamento de arquivo. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conta ser estabelecida.

![connect](../../../../images/tutorials/create/azure-file-storage/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta do Armazenamento de Arquivo do Azure com a qual você deseja se conectar e, em seguida, selecione **[!UICONTROL Próximo]** para prosseguir.

![existente](../../../../images/tutorials/create/azure-file-storage/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta do Armazenamento de Arquivo do Azure. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados do seu armazenamento em nuvem para a Plataforma](../../dataflow/batch/cloud-storage.md).