---
keywords: Experience Platform;home;popular tópicos;blob do Azure;blob do Azure;conector blob do Azure
solution: Experience Platform
title: Criar um conector de origem do Blob do Azure na interface do usuário
topic: overview
type: Tutorial
description: Este tutorial fornece etapas para a criação de um blob do Azure (a seguir denominado "Blob") usando a interface do usuário da Plataforma.
translation-type: tm+mt
source-git-commit: e22e57e20b985b50e1d29e944fb8f04addc91703
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 1%

---


# Crie um conector de origem [!DNL Azure Blob] na interface do usuário

Este tutorial fornece etapas para criar um [!DNL Azure Blob] (a seguir denominado &quot;[!DNL Blob]&quot;) usando a interface do usuário da plataforma.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   - [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão válida [!DNL Blob], poderá ignorar o restante desse documento e prosseguir para o tutorial em [configurar um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Formatos de arquivo não suportados

[!DNL Experience Platform] oferece suporte aos seguintes formatos de arquivo para serem assimilados de armazenamentos externos:

- Valores separados por delimitador (DSV): Atualmente, o suporte para arquivos de dados formatados em DSV está limitado a valores separados por vírgulas. O valor dos cabeçalhos de campo nos arquivos formatados em DSV deve consistir apenas em caracteres alfanuméricos e sublinhados. O suporte para arquivos DSV gerais será fornecido no futuro.
- JSON (JavaScript Object Notation): Os arquivos de dados formatados JSON devem ser compatíveis com XDM.
- Parqueta Apache: Os arquivos de dados formatados do parâmetro devem ser compatíveis com XDM.

### Reunir credenciais obrigatórias

Para acessar o armazenamento [!DNL Blob] na plataforma, é necessário fornecer um valor válido para a seguinte credencial:

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | Uma string que contém as informações de autorização necessárias para autenticar [!DNL Blob] no Experience Platform. O padrão da cadeia de conexão [!DNL Blob] é: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Para obter mais informações sobre strings de conexão, consulte este documento [!DNL Blob] em [configurar strings de conexão](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | O URI de assinatura de acesso compartilhado que você pode usar como um tipo de autenticação alternativo para conectar sua conta [!DNL Blob]. O padrão de URI SAS [!DNL Blob] é: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Para obter mais informações, consulte este documento [!DNL Blob] em [URIs de assinatura de acesso compartilhado](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |

## Conectar sua conta [!DNL Blob]

Depois de reunir as credenciais necessárias, siga as etapas abaixo para vincular sua conta [!DNL Blob] à Plataforma.

Na [Interface do usuário da plataforma](https://platform.adobe.com), selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catalog] exibe várias fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

Na categoria [!UICONTROL armazenamento Cloud], selecione **[!UICONTROL Armazenamento Blob do Azure]** e selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/blob/catalog.png)

A página **[!UICONTROL Conectar-se ao Armazenamento Blob do Azure]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a conta [!DNL Blob] com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próximo]** para continuar.

![existente](../../../../images/tutorials/create/blob/existing.png)

### Nova conta

Se você estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome e uma descrição de opção para sua nova conta [!DNL Blob].

**Autenticar usando uma string de conexão**

O conector [!DNL Blob] fornece tipos de autenticação diferentes para acesso. Em [!UICONTROL Autenticação de conta] selecione **[!UICONTROL ConnectionString]** para utilizar credenciais baseadas em cadeia de ligação.

![cadeia de conexão](../../../../images/tutorials/create/blob/connectionstring.png)

**Autenticar usando um URI de assinatura de acesso compartilhado**

Um URI de assinatura de acesso compartilhado (SAS) permite autorização delegada segura para sua conta [!DNL Blob]. Você pode usar o SAS para criar credenciais de autenticação com graus variáveis de acesso, já que uma autenticação baseada em SAS permite definir permissões, datas de start e expiração, bem como provisões para recursos específicos.

Selecione **[!UICONTROL SasURIAuthentication]** e forneça seu URI SAS [!DNL Blob]. Selecione **[!UICONTROL Ligar à origem]** para prosseguir.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta [!DNL Blob]. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados do seu armazenamento em nuvem para a Plataforma](../../dataflow/batch/cloud-storage.md).
