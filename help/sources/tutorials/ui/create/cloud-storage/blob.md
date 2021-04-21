---
keywords: Experience Platform, home, tópicos populares, Azure Blob, blob do azure, conector de blob do Azure
solution: Experience Platform
title: Criar uma conexão de fonte de blob do Azure na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar um conector de origem do Azure Blob usando a interface do usuário da plataforma.
exl-id: 0e54569b-7305-4065-981e-951623717648
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 1%

---

# Criar uma conexão de origem [!DNL Azure Blob] na interface do usuário

Este tutorial fornece etapas para criar um [!DNL Azure Blob] (a seguir chamado &quot;[!DNL Blob]&quot;) usando a interface do usuário da plataforma.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   - [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de esquema: Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão válida [!DNL Blob], poderá ignorar o restante deste documento e prosseguir para o tutorial em [configurar um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Formatos de arquivo não suportados

[!DNL Experience Platform] O suporta os seguintes formatos de arquivo a serem assimilados de armazenamentos externos:

- Valores separados por delimitador (DSV): No momento, o suporte para arquivos de dados formatados em DSV está limitado a valores separados por vírgula. O valor dos cabeçalhos de campo em arquivos formatados em DSV deve consistir apenas em caracteres alfanuméricos e sublinhados. O suporte para arquivos DSV gerais será fornecido no futuro.
- Notação de objeto JavaScript (JSON): Os arquivos de dados formatados JSON devem ser compatíveis com XDM.
- Parqueta Apache: Os arquivos de dados formatados do parâmetro devem ser compatíveis com XDM.

### Obter credenciais necessárias

Para acessar o armazenamento [!DNL Blob] na plataforma, você deve fornecer um valor válido para a seguinte credencial:

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | Uma string que contém as informações de autorização necessárias para autenticar [!DNL Blob] no Experience Platform. O padrão da string de conexão [!DNL Blob] é: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Para obter mais informações sobre cadeias de conexão, consulte este documento [!DNL Blob] em [configurar cadeias de conexão](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | O URI da assinatura de acesso compartilhado que você pode usar como um tipo de autenticação alternativo para conectar sua conta [!DNL Blob]. O padrão de URI SAS [!DNL Blob] é: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Para obter mais informações, consulte este documento [!DNL Blob] em [URIs de assinatura de acesso compartilhado](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |

## Conecte sua conta [!DNL Blob]

Depois de reunir suas credenciais necessárias, siga as etapas abaixo para vincular sua conta [!DNL Blob] à Platform.

Na [Interface do usuário da plataforma](https://platform.adobe.com), selecione **[!UICONTROL Sources]** na barra de navegação esquerda para acessar o espaço de trabalho [!UICONTROL Sources]. A tela [!UICONTROL Catalog] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

Na categoria [!UICONTROL Cloud storage], selecione **[!UICONTROL Azure Blob Storage]** e selecione **[!UICONTROL Add data]**.

![catálogo](../../../../images/tutorials/create/blob/catalog.png)

A página **[!UICONTROL Connect to Azure Blob Storage]** é exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Conta existente

Para usar uma conta existente, selecione a conta [!DNL Blob] com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Next]** para prosseguir.

![existente](../../../../images/tutorials/create/blob/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL New account]** e forneça um nome e uma descrição de opção para sua nova conta [!DNL Blob].

**Autenticar usando uma string de conexão**

O conector [!DNL Blob] fornece tipos de autenticação diferentes para acesso. Em [!UICONTROL Account authentication] selecione **[!UICONTROL ConnectionString]** para usar credenciais baseadas em sequências de conexão.

![string de conexão](../../../../images/tutorials/create/blob/connectionstring.png)

**Autenticar usando um URI de assinatura de acesso compartilhado**

Um URI de assinatura de acesso compartilhado (SAS) permite autorização delegada segura para sua conta [!DNL Blob]. Você pode usar a SAS para criar credenciais de autenticação com diferentes graus de acesso, já que uma autenticação baseada em SAS permite definir permissões, datas de início e expiração, bem como provisões para recursos específicos.

Selecione **[!UICONTROL SasURIAuthentication]** e forneça seu URI SAS [!DNL Blob]. Selecione **[!UICONTROL Connect to source]** para continuar.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta [!DNL Blob]. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados do armazenamento de nuvem para a Platform](../../dataflow/batch/cloud-storage.md).
