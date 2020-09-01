---
keywords: Experience Platform;home;popular topics;Azure Blob;azure blob;Azure blob connector
solution: Experience Platform
title: Criar um conector de origem do Blob do Azure na interface do usuário
topic: overview
description: Este tutorial fornece etapas para a criação de um blob do Azure (a seguir denominado "Blob") usando a interface do usuário da Plataforma.
translation-type: tm+mt
source-git-commit: 0da686743e8bc57d310f7eff6f1bf812a8f31238
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---


# Criar um conector [!DNL Azure Blob] de origem na interface do usuário

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um [!DNL Azure Blob] (a seguir denominado &quot;[!DNL Blob]&quot;) usando a interface do [!DNL Platform] usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   - [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
- [[!DNL Perfil do cliente em tempo real]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma [!DNL Blob] conexão válida, poderá ignorar o restante desse documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Formatos de arquivo não suportados

[!DNL Experience Platform] oferece suporte aos seguintes formatos de arquivo para serem assimilados de armazenamentos externos:

- Valores separados por delimitador (DSV): Atualmente, o suporte para arquivos de dados formatados em DSV está limitado a valores separados por vírgulas. O valor dos cabeçalhos de campo nos arquivos formatados em DSV deve consistir apenas em caracteres alfanuméricos e sublinhados. O suporte para arquivos DSV gerais será fornecido no futuro.
- JSON (JavaScript Object Notation): Os arquivos de dados formatados JSON devem ser compatíveis com XDM.
- Parqueta Apache: Os arquivos de dados formatados do parâmetro devem ser compatíveis com XDM.

### Reunir credenciais obrigatórias

Para acessar seu [!DNL Blob] armazenamento em, [!DNL Platform]você deve fornecer um valor válido para a seguinte credencial:

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | A string de conexão necessária para acessar dados no armazenamento Blob. O padrão da string de [!DNL Blob] conexão é: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

Para obter mais informações sobre como começar, visite [ [!DNL Azure Blob] este documento](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string).

## Conectar sua conta Blob

Depois de reunir as credenciais necessárias, siga as etapas abaixo para vincular sua [!DNL Blob] conta a [!DNL Platform].

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Fontes]** . A tela **[!UICONTROL Catálogo]** exibe várias fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Bancos]** de Dados, selecione **[!UICONTROL Armazenamento]** Blob do Azure. Se esta for a sua primeira vez usando este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo [!DNL Blob]conector.

![catálogo](../../../../images/tutorials/create/blob/catalog.png)

A página **[!UICONTROL Conectar-se ao Armazenamento]** Blob do Azure é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas [!DNL Blob] credenciais. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conexão ser estabelecida.

![connect](../../../../images/tutorials/create/blob/new.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Blob] conta à qual deseja se conectar e, em seguida, selecione **[!UICONTROL Avançar]** para continuar.

![existente](../../../../images/tutorials/create/blob/existing.png)

## Próximos passos e recursos adicionais

Ao seguir este tutorial, você estabeleceu uma conexão com sua [!DNL Blob] conta. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados do seu armazenamento em nuvem para [!DNL Platform]](../../dataflow/batch/cloud-storage.md)dentro.