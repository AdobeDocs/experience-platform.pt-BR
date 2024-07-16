---
title: Criar uma conexão do Azure Blob Source na interface
description: Saiba como criar um conector de origem do Azure Blob usando a interface do usuário da Platform.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 2%

---

# Criar uma conexão de origem [!DNL Azure Blob] na interface

Este tutorial fornece etapas para a criação de uma conexão de origem [!DNL Azure Blob] (a seguir denominada &quot;[!DNL Blob]&quot;) usando a interface do usuário da Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada para organizar os dados de experiência do cliente no Experience Platform.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão [!DNL Blob] válida, ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Formatos de arquivo não suportados

O Experience Platform suporta os seguintes formatos de arquivo a serem assimilados de armazenamentos externos:

* Valores separados por delimitadores (DSV): você pode usar qualquer delimitador de coluna única, como tabulação, vírgula, barra vertical, ponto e vírgula ou hash, para coletar arquivos simples em qualquer formato.
* Notação de objeto do JavaScript (JSON): os arquivos de dados formatados em JSON devem ser compatíveis com XDM.
* Apache Parquet: os arquivos de dados formatados com Parquet devem ser compatíveis com XDM.

### Coletar credenciais necessárias

Para acessar o armazenamento do [!DNL Blob] no Experience Platform, você deve fornecer valores válidos para as seguintes credenciais:

>[!BEGINTABS]

>[!TAB Autenticação da cadeia de conexão]

| Credencial | Descrição |
| --- | --- |
| String de conexão | Uma cadeia de caracteres que contém as informações de autorização necessárias para autenticar [!DNL Blob] em Experience Platform. O padrão da cadeia de conexão [!DNL Blob] é: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Para obter mais informações sobre cadeias de conexão, consulte este documento [!DNL Blob] em [configurando cadeias de conexão](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |

>[!TAB Autenticação do URI SAS]

| Credencial | Descrição |
| --- | --- |
| URI SAS | O URI de assinatura de acesso compartilhado que você pode usar como um tipo de autenticação alternativo para conectar sua conta do [!DNL Blob]. O padrão do URI SAS [!DNL Blob] é: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Para obter mais informações, consulte este [!DNL Blob] documento em [URIs de assinatura de acesso compartilhado](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| Contêiner | O nome do container ao qual você deseja designar acesso. Ao criar uma nova conta com a origem [!DNL Blob], você pode fornecer um nome de contêiner para especificar o acesso do usuário à subpasta de sua escolha. |
| Caminho da pasta | O caminho para a pasta à qual você deseja fornecer acesso. |

>[!ENDTABS]

Depois de obter as credenciais necessárias, você poderá seguir as etapas abaixo para conectar o armazenamento do [!DNL Blob] ao Experience Platform

## Conectar sua conta do [!DNL Blob]

Na interface da Platform, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

Na categoria [!UICONTROL Armazenamento na nuvem], selecione **[!UICONTROL Armazenamento do Azure Blob]** e **[!UICONTROL Adicionar dados]**.

![O catálogo de origens de Experience Platform com a origem de Armazenamento de Blob do Azure selecionada.](../../../../images/tutorials/create/blob/catalog.png)

A página **[!UICONTROL Conectar-se ao Armazenamento Azure Blob]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a conta [!DNL Blob] com a qual deseja criar um novo fluxo de dados e clique em **[!UICONTROL Avançar]** para continuar.

![existente](../../../../images/tutorials/create/blob/existing.png)

### Nova conta

>[!TIP]
>
>Depois de criada, você não pode alterar o tipo de autenticação de uma conexão de base [!DNL Blob]. Para alterar o tipo de autenticação, você deve criar uma nova conexão base.

Se você estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome e uma descrição opcional para sua nova conta [!DNL Blob].

![A tela da nova conta para a fonte do Armazenamento Azure Blob.](../../../../images/tutorials/create/blob/new.png)

A origem [!DNL Blob] dá suporte à autenticação de chave de conta e à autenticação de assinatura de acesso compartilhado (SAS). Uma autenticação baseada em chave de conta requer uma cadeia de conexão para verificação, enquanto uma autenticação SAS usa um URI que permite autorização delegada segura de sua conta.

Durante essa etapa, também é possível designar as subpastas às quais sua conta terá acesso definindo o nome do container e o caminho para a subpasta.

>[!BEGINTABS]

>[!TAB Cadeia de Conexão]

Para autenticar com uma chave de conta, selecione **[!UICONTROL Autenticação da chave de conta]** e forneça sua cadeia de conexão. Durante essa etapa, também é possível designar o nome e o caminho do container para a subpasta à qual você deseja acessar o. Quando terminar, selecione **[!UICONTROL Conectar à origem]**.

![cadeia de conexão](../../../../images/tutorials/create/blob/connectionstring.png)

>[!TAB URI SAS]

Você pode usar SAS para criar credenciais de autenticação com vários graus de acesso, já que uma autenticação baseada em SAS permite definir permissões, datas de início e expiração, bem como provisões para recursos específicos.

Para autenticar com uma assinatura de acesso compartilhado, selecione **[!UICONTROL Autenticação de assinatura de acesso compartilhado]** e forneça seu URI SAS. Durante essa etapa, também é possível designar o nome e o caminho do container para a subpasta à qual você deseja acessar o. Quando terminar, selecione **[!UICONTROL Conectar à origem]**.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

>[!ENDTABS]

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua conta do [!DNL Blob]. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados do seu armazenamento em nuvem para a Platform](../../dataflow/batch/cloud-storage.md).
