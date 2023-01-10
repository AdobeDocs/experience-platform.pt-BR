---
keywords: Experience Platform, home, tópicos populares, Azure Blob, blob do azure, conector de blob do Azure
solution: Experience Platform
title: Criar uma conexão de fonte de blob do Azure na interface do usuário
type: Tutorial
description: Saiba como criar um conector de origem do Azure Blob usando a interface do usuário da plataforma.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 1%

---

# Crie um [!DNL Azure Blob] conexão de origem na interface do usuário

Este tutorial fornece etapas para criar um [!DNL Azure Blob] (a seguir designado por &quot;[!DNL Blob]&quot;) usando a interface do usuário da plataforma.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   - [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL Blob] , você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Formatos de arquivo não compatíveis

[!DNL Experience Platform] O suporta os seguintes formatos de arquivo a serem assimilados de armazenamentos externos:

- Valores separados por delimitador (DSV): No momento, o suporte para arquivos de dados formatados em DSV está limitado a valores separados por vírgula. O valor dos cabeçalhos de campo em arquivos formatados em DSV deve consistir apenas em caracteres alfanuméricos e sublinhados. O suporte para arquivos DSV gerais será fornecido no futuro.
- Notação de objeto JavaScript (JSON): Os arquivos de dados formatados JSON devem ser compatíveis com XDM.
- Parqueta Apache: Os arquivos de dados formatados do parâmetro devem ser compatíveis com XDM.

### Obter credenciais necessárias

Para acessar o [!DNL Blob] no Platform, você deve fornecer um valor válido para a seguinte credencial:

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | Uma string que contém as informações de autorização necessárias para autenticar [!DNL Blob] para Experience Platform. O [!DNL Blob] o padrão da string de conexão é: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Para obter mais informações sobre strings de conexão, consulte esta seção [!DNL Blob] documento em [configuração das cadeias de conexão](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | O URI da assinatura de acesso compartilhado que você pode usar como um tipo de autenticação alternativo para conectar seu [!DNL Blob] conta. O [!DNL Blob] O padrão de URI SAS é: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Para obter mais informações, consulte [!DNL Blob] documento em [URIs de assinatura de acesso compartilhado](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |

## Conecte seu [!DNL Blob] account

Depois de reunir suas credenciais necessárias, siga as etapas abaixo para vincular seus [!DNL Blob] para a Platform.

No [Interface do usuário da plataforma](https://platform.adobe.com), selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

Em [!UICONTROL armazenamento na nuvem] categoria , selecione **[!UICONTROL Armazenamento Azure Blob]** e selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/blob/catalog.png)

O **[!UICONTROL Conectar-se ao Armazenamento Azure Blob]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Conta existente

Para usar uma conta existente, selecione a [!DNL Blob] conta com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próximo]** para continuar.

![existente](../../../../images/tutorials/create/blob/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome e uma descrição de opção para o novo [!DNL Blob] conta.

**Autenticar usando uma string de conexão**

O [!DNL Blob] O conector fornece tipos de autenticação diferentes para acesso. Em [!UICONTROL Autenticação da conta] select **[!UICONTROL ConnectionString]** para usar credenciais baseadas em string de conexão.

![string de conexão](../../../../images/tutorials/create/blob/connectionstring.png)

**Autenticar usando um URI de assinatura de acesso compartilhado**

Um URI de assinatura de acesso compartilhado (SAS) permite autorização delegada segura para seu [!DNL Blob] conta. Você pode usar a SAS para criar credenciais de autenticação com diferentes graus de acesso, já que uma autenticação baseada em SAS permite definir permissões, datas de início e expiração, bem como provisões para recursos específicos.

Selecionar **[!UICONTROL SasURIAuthentication]** e, em seguida, forneça seu [!DNL Blob] URI SAS. Selecionar **[!UICONTROL Conectar-se à origem]** para continuar.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com seu [!DNL Blob] conta. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados do armazenamento em nuvem para a Platform](../../dataflow/batch/cloud-storage.md).
