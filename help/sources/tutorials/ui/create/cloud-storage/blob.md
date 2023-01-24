---
title: Criar uma conexão de fonte de blob do Azure na interface do usuário
description: Saiba como criar um conector de origem do Azure Blob usando a interface do usuário da plataforma.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: 922e9a26f1791056b251ead2ce2702dfbf732193
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 1%

---

# Crie um [!DNL Azure Blob] conexão de origem na interface do usuário

Este tutorial fornece etapas para criar um [!DNL Azure Blob] (a seguir designado por &quot;[!DNL Blob]&quot;) conexão de origem usando a interface do usuário da plataforma.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada para organizar os dados de experiência do cliente no Experience Platform.
   * [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL Blob] , você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Formatos de arquivo não compatíveis

O Experience Platform oferece suporte aos seguintes formatos de arquivo para serem assimilados de armazenamentos externos:

* Valores separados por delimitador (DSV): Você pode usar qualquer delimitador de coluna único, como uma guia, vírgula, barra vertical, ponto e vírgula ou hash para coletar arquivos simples em qualquer formato.
* Notação de objeto JavaScript (JSON): Os arquivos de dados formatados JSON devem ser compatíveis com XDM.
* Parqueta Apache: Os arquivos de dados formatados do parâmetro devem ser compatíveis com XDM.

### Obter credenciais necessárias

Para acessar o [!DNL Blob] no Platform, você deve fornecer um valor válido para a seguinte credencial:

| Credencial | Descrição |
| ---------- | ----------- |
| Cadeia de conexão | Uma string que contém as informações de autorização necessárias para autenticar [!DNL Blob] para Experience Platform. O [!DNL Blob] o padrão da string de conexão é: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Para obter mais informações sobre strings de conexão, consulte esta seção [!DNL Blob] documento em [configuração das cadeias de conexão](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| URI SAS | O URI da assinatura de acesso compartilhado que você pode usar como um tipo de autenticação alternativo para conectar seu [!DNL Blob] conta. O [!DNL Blob] O padrão de URI SAS é: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Para obter mais informações, consulte [!DNL Blob] documento em [URIs de assinatura de acesso compartilhado](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| Contêiner | O nome do contêiner ao qual você deseja designar acesso. Ao criar uma nova conta com o [!DNL Blob] na origem, você pode fornecer um nome de contêiner para especificar o acesso do usuário à subpasta de sua escolha. |
| Caminho da pasta | O caminho para a pasta à qual você deseja fornecer acesso. |

Depois de reunir suas credenciais necessárias, siga as etapas abaixo para vincular seus [!DNL Blob] para a Platform.

## Conecte seu [!DNL Blob] account

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

Em [!UICONTROL armazenamento na nuvem] categoria , selecione **[!UICONTROL Armazenamento Azure Blob]** e selecione **[!UICONTROL Adicionar dados]**.

![O catálogo de origens de Experience Platform com a origem de Armazenamento Azure Blob selecionada.](../../../../images/tutorials/create/blob/catalog.png)

O **[!UICONTROL Conectar-se ao Armazenamento Azure Blob]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Conta existente

Para usar uma conta existente, selecione a [!DNL Blob] conta com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próximo]** para continuar.

![existente](../../../../images/tutorials/create/blob/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome e uma descrição opcional para o novo [!DNL Blob] conta.

![A nova tela de conta para a origem do Armazenamento Azure Blob.](../../../../images/tutorials/create/blob/new.png)

O [!DNL Blob] A origem suporta autenticação de chave de conta e autenticação de assinatura de acesso compartilhado (SAS). Uma autenticação baseada em chave de conta requer uma string de conexão para verificação, enquanto uma autenticação SAS usa um URI que permite a autorização delegada segura de sua conta.

Durante essa etapa, também é possível designar as subpastas às quais sua conta terá acesso, definindo o nome do contêiner e o caminho para a subpasta.

>[!BEGINTABS]

>[!TAB String de conexão]

Para autenticar com uma chave de conta, selecione **[!UICONTROL Autenticação da chave da conta]** e forneça sua string de conexão. Durante essa etapa, também é possível designar o nome e o caminho do contêiner para a subpasta à qual deseja acessar. Quando terminar, selecione **[!UICONTROL Conectar-se à origem]**.

![string de conexão](../../../../images/tutorials/create/blob/connectionstring.png)

>[!TAB URI SAS]

Você pode usar a SAS para criar credenciais de autenticação com diferentes graus de acesso, já que uma autenticação baseada em SAS permite definir permissões, datas de início e expiração, bem como provisões para recursos específicos.

Para autenticar com uma assinatura de acesso compartilhado, selecione **[!UICONTROL Autenticação de assinatura de acesso compartilhado]** e forneça seu URI SAS. Durante essa etapa, também é possível designar o nome e o caminho do contêiner para a subpasta à qual deseja acessar. Quando terminar, selecione **[!UICONTROL Conectar-se à origem]**.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

>[!ENDTABS]

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com seu [!DNL Blob] conta. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados do armazenamento em nuvem para a Platform](../../dataflow/batch/cloud-storage.md).
