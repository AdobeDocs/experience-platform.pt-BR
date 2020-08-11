---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem de Armazenamento do Google Cloud na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 1%

---


# Criar um conector [!DNL Google Cloud Storage] de origem na interface do usuário

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem [!DNL Google Cloud Storage] (a seguir denominado &quot;GCS&quot;) usando a interface do [!DNL Platform] usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão básica GCS, poderá ignorar o restante deste documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Formatos de arquivo não suportados

[!DNL Experience Platform] oferece suporte aos seguintes formatos de arquivo para serem assimilados de armazenamentos externos:

* Valores separados por delimitador (DSV): Atualmente, o suporte para arquivos de dados formatados em DSV está limitado a valores separados por vírgulas. O valor dos cabeçalhos de campo nos arquivos formatados em DSV deve consistir apenas em caracteres alfanuméricos e sublinhados. O suporte para arquivos DSV gerais será fornecido no futuro.
* JSON (JavaScript Object Notation): Os arquivos de dados formatados JSON devem ser compatíveis com XDM.
* Parqueta Apache: Os arquivos de dados formatados do parâmetro devem ser compatíveis com XDM.

### Reunir credenciais obrigatórias

Para acessar seus dados GCS em [!DNL Platform], é necessário fornecer uma ID **de chave de** acesso GCS e um **segredo** válidos. Você pode saber mais sobre como obter esses valores lendo o guia <a href="https://cloud.google.com/docs/authentication/production" target="_blank">de autenticação</a> servidor a servidor para [!DNL Google Cloud].

## Conectar sua conta GCS

Depois de coletar as credenciais necessárias, siga as etapas abaixo para criar uma nova conta GCS à qual se conectar [!DNL Platform].

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho *[!UICONTROL Fontes]* . A tela *[!UICONTROL Catálogo]* exibe várias fontes nas quais você pode criar uma conta de entrada e cada fonte mostra o número de contas e fluxos de dados existentes associados a elas.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria *[!UICONTROL Bancos]* de dados, selecione Armazenamento **[!UICONTROL da]** Google Cloud seguido por **[!UICONTROL Adicionar dados]** para criar um novo conector GCS.

![catálogo](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

A página *[!UICONTROL Conectar-se ao Armazenamento]* do Google Cloud é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça à conexão um nome, uma descrição opcional e suas credenciais GCS. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conta ser estabelecida.

![connect](../../../../images/tutorials/create/google-cloud-storage/connect.png)

### Conta existente

Para conectar uma conta existente, selecione a conta GCS à qual deseja se conectar e, em seguida, selecione **[!UICONTROL Avançar]** para continuar.

![existente](../../../../images/tutorials/create/google-cloud-storage/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta GCS. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados do seu armazenamento em nuvem para a Plataforma](../../dataflow/batch/cloud-storage.md).