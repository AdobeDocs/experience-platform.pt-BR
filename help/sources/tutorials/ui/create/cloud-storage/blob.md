---
title: Criar uma conexão de origem do Azure Blob na interface do usuário
description: Saiba como criar um conector de origem do Azure Blob usando a interface do usuário da Platform.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 1%

---

# Criar um [!DNL Azure Blob] conexão de origem na interface

Este tutorial fornece etapas para a criação de um [!DNL Azure Blob] (a seguir designado por &quot;[!DNL Blob]&quot;) conexão de origem usando a interface do usuário da Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada para organizar os dados de experiência do cliente no Experience Platform.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL Blob] conexão, você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Formatos de arquivo não compatíveis

O Experience Platform suporta os seguintes formatos de arquivo a serem assimilados de armazenamentos externos:

* Valores separados por delimitadores (DSV): você pode usar qualquer delimitador de coluna única, como tabulação, vírgula, barra vertical, ponto e vírgula ou hash, para coletar arquivos simples em qualquer formato.
* Anotação de objeto JavaScript (JSON): os arquivos de dados formatados em JSON devem ser compatíveis com XDM.
* Apache Parquet: os arquivos de dados formatados com Parquet devem ser compatíveis com XDM.

### Coletar credenciais necessárias

Para acessar seu [!DNL Blob] armazenamento no Experience Platform, você deve fornecer valores válidos para as seguintes credenciais:

>[!BEGINTABS]

>[!TAB Autenticação da cadeia de conexão]

| Credencial | Descrição |
| --- | --- |
| String de conexão | Uma cadeia de caracteres que contém as informações de autorização necessárias para autenticação [!DNL Blob] para Experience Platform. A variável [!DNL Blob] o padrão da cadeia de conexão é: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Para obter mais informações sobre cadeias de conexão, consulte esta [!DNL Blob] documento ativado [configurando cadeias de conexão](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |

>[!TAB Autenticação URI SAS]

| Credencial | Descrição |
| --- | --- |
| URI SAS | O URI de assinatura de acesso compartilhado que você pode usar como um tipo de autenticação alternativo para conectar seu [!DNL Blob] conta. A variável [!DNL Blob] O padrão do URI SAS é: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Para obter mais informações, consulte esta [!DNL Blob] documento ativado [URIs de assinatura de acesso compartilhado](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| Contêiner | O nome do container ao qual você deseja designar acesso. Ao criar uma nova conta com o [!DNL Blob] origem, você pode fornecer um nome de container para especificar o acesso do usuário à subpasta de sua escolha. |
| Caminho da pasta | O caminho para a pasta à qual você deseja fornecer acesso. |

>[!ENDTABS]

Depois de obter as credenciais necessárias, siga as etapas abaixo para conectar seu [!DNL Blob] armazenamento para o Experience Platform

## Conecte seu [!DNL Blob] account

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na barra de navegação esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

No [!UICONTROL armazenamento na nuvem] categoria, selecione **[!UICONTROL Armazenamento Azure Blob]** e selecione **[!UICONTROL Adicionar dados]**.

![O catálogo de origens de Experience Platform com a origem de Armazenamento Azure Blob selecionada.](../../../../images/tutorials/create/blob/catalog.png)

A variável **[!UICONTROL Conectar-se ao Armazenamento Azure Blob]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a variável [!DNL Blob] conta com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próxima]** para continuar.

![existente](../../../../images/tutorials/create/blob/existing.png)

### Nova conta

>[!TIP]
>
>Depois de criado, não é possível alterar o tipo de autenticação de um [!DNL Blob] conexão básica. Para alterar o tipo de autenticação, você deve criar uma nova conexão base.

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome e uma descrição opcional para o novo [!DNL Blob] conta.

![A tela da nova conta para a origem do Armazenamento Azure Blob.](../../../../images/tutorials/create/blob/new.png)

A variável [!DNL Blob] A origem oferece suporte à autenticação de chave de conta e à autenticação de assinatura de acesso compartilhado (SAS). Uma autenticação baseada em chave de conta requer uma cadeia de conexão para verificação, enquanto uma autenticação SAS usa um URI que permite autorização delegada segura de sua conta.

Durante essa etapa, também é possível designar as subpastas às quais sua conta terá acesso definindo o nome do container e o caminho para a subpasta.

>[!BEGINTABS]

>[!TAB String de conexão]

Para autenticar com uma chave de conta, selecione **[!UICONTROL Autenticação da chave da conta]** e forneça sua cadeia de conexão. Durante essa etapa, também é possível designar o nome e o caminho do container para a subpasta à qual você deseja acessar o. Quando terminar, selecione **[!UICONTROL Conectar à origem]**.

![cadeia de conexão](../../../../images/tutorials/create/blob/connectionstring.png)

>[!TAB URI SAS]

Você pode usar SAS para criar credenciais de autenticação com vários graus de acesso, já que uma autenticação baseada em SAS permite definir permissões, datas de início e expiração, bem como provisões para recursos específicos.

Para autenticar com uma assinatura de acesso compartilhado, selecione **[!UICONTROL Autenticação de assinatura de acesso compartilhado]** e forneça seu URI SAS. Durante essa etapa, também é possível designar o nome e o caminho do container para a subpasta à qual você deseja acessar o. Quando terminar, selecione **[!UICONTROL Conectar à origem]**.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

>[!ENDTABS]

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com o seu [!DNL Blob] conta. Agora você pode seguir para o próximo tutorial e [configure um fluxo de dados para trazer dados do armazenamento em nuvem para a Platform](../../dataflow/batch/cloud-storage.md).
