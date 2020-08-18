---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem de Armazenamento do Google Cloud na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: ec2d0a33e0ae92a3153b7bdcad29734e487a0439
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 1%

---


# Criar um conector [!DNL Google Cloud Storage] de origem na interface do usuário

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem [!DNL Google Cloud Storage] (a seguir denominado &quot;GCS&quot;) usando a interface do [!DNL Platform] usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [[!DNL Perfil do cliente em tempo real]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão GCS válida, poderá ignorar o restante deste documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Formatos de arquivo não suportados

[!DNL Experience Platform] oferece suporte aos seguintes formatos de arquivo para serem assimilados de armazenamentos externos:

* Valores separados por delimitador (DSV): Atualmente, o suporte para arquivos de dados formatados em DSV está limitado a valores separados por vírgulas. O valor dos cabeçalhos de campo nos arquivos formatados em DSV deve consistir apenas em caracteres alfanuméricos e sublinhados. O suporte para arquivos DSV gerais será fornecido no futuro.
* JSON (JavaScript Object Notation): Os arquivos de dados formatados JSON devem ser compatíveis com XDM.
* Parqueta Apache: Os arquivos de dados formatados do parâmetro devem ser compatíveis com XDM.

### Reunir credenciais obrigatórias

Para acessar seus dados GCS em [!DNL Platform], forneça os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| ID da chave de acesso | A ID da chave de acesso da [!DNL Google Cloud Storage] conta. |
| Chave de acesso secreta | O segredo do cliente da [!DNL Google Cloud Storage] conta. |

Para obter mais informações sobre a introdução, consulte o guia [de autenticação](https://cloud.google.com/docs/authentication/production) servidor a servidor para [!DNL Google Cloud Storage].

## Conectar sua [!DNL Google Cloud Storage] conta

Depois de reunir as credenciais necessárias, siga as etapas abaixo para vincular sua conta GCS à [!DNL Platform].

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Fontes]** . A tela **[!UICONTROL Catálogo]** exibe várias fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Bancos]** de dados, selecione Armazenamento **[!UICONTROL da]** Google Cloud. Se esta for a sua primeira vez usando este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector GCS.

![catálogo](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

A página **[!UICONTROL Conectar-se ao Armazenamento]** do Google Cloud é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais GCS. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conexão ser estabelecida.

![connect](../../../../images/tutorials/create/google-cloud-storage/connect.png)

### Conta existente

Para conectar uma conta existente, selecione a conta GCS à qual deseja se conectar e, em seguida, selecione **[!UICONTROL Avançar]** para continuar.

![existente](../../../../images/tutorials/create/google-cloud-storage/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta GCS. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados do seu armazenamento em nuvem para [!DNL Platform]](../../dataflow/batch/cloud-storage.md)dentro.