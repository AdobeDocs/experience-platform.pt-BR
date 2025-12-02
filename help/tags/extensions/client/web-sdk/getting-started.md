---
title: Introdução à extensão de tag do Web SDK
description: Envie dados do evento para o Adobe Experience Platform Edge Network usando a extensão de tag da Web SDK.
exl-id: 01ddbb19-40bb-4cb5-bfca-b272b88008b3
source-git-commit: 8dd658c46fc92ae6d450213ab79f2766f4211c53
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 3%

---

# Introdução à extensão de tag do Web SDK

Use as **tags** da Adobe Experience Platform (antigo Launch) para enviar dados de eventos do seu site para a Edge Network e soluções downstream da Adobe.

Antes de seguir essas etapas, verifique se você pode acessar os [direitos de propriedade](/help/tags/ui/administration/user-permissions.md) a seguir:

* [!UICONTROL Develop]
* [!UICONTROL Manage extensions]

Além disso, verifique se você tem todas as [permissões](/help/access-control/home.md#permissions) nas seguintes categorias:

* Modelagem de dados
* Identidades

## Criar um esquema do XDM {#schema}

O [Experience Data Model (XDM)](/help/xdm/home.md) é uma especificação de código aberto que fornece estruturas e definições comuns para dados na forma de esquemas. É altamente recomendável configurar um esquema ao enviar dados para a Edge Network.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Schemas]**.
1. Selecione **[!UICONTROL Create schema]**.
1. Selecione **[!UICONTROL Experience Event]** e depois **[!UICONTROL Next]**.
1. Dê um nome desejado ao esquema e selecione **[!UICONTROL Finish]**.
1. (Opcional) É possível adicionar mais campos ou [grupos de campos](/help/xdm/ui/resources/field-groups.md) para quaisquer dados adicionais que você queira coletar.

![Tela do esquema](assets/getting-started/schema-structure.png)

>[!NOTE]
>\
>Depois de salvos, os esquemas só permitem *alterações aditivas*. Consulte [evolução do esquema](/help/xdm/schema/composition.md#evolution) para obter mais informações.

## Criar um fluxo de dados {#datastream}

Uma [Sequência de dados](/help/datastreams/overview.md) é uma configuração que informa à Edge Network como lidar com os dados enviados. Ao configurar um fluxo de dados para enviar dados a um determinado produto, o fluxo de dados transmite automaticamente dados relevantes para cada produto de uma forma que o produto específico entenda.

1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Datastreams]**.
1. Selecione **[!UICONTROL New datastream]**.
1. Dê ao fluxo de dados um nome desejado e selecione o esquema criado recentemente em **[!UICONTROL Mapping schema]**.
1. Selecione **[!UICONTROL Save]**.

![Lista de sequências de dados](assets/getting-started/datastreams.png)

## Criar uma propriedade de tag

Depois de criar um esquema e um fluxo de dados, você pode criar e configurar uma propriedade de tag.

1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecione **[!UICONTROL New property]**.
1. Dê à propriedade da marca um nome e um domínio desejados e selecione **[!UICONTROL Save]**.

## Instalar a extensão de tag

A extensão de tag do Web SDK é instalada em uma determinada propriedade de tag.

1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]** > **[!UICONTROL Extensions]**.
1. Selecione a guia **[!UICONTROL Catalog]**.
1. Use a pesquisa para localizar a extensão **[!UICONTROL Adobe Experience Platform Web SDK]**.
1. Selecione o cartão de extensão e, em seguida, selecione **[!UICONTROL Install]** à direita.

![Instalar o SDK](assets/getting-started/install-sdk.png)

## Configurar a extensão de tag

Ao instalar a extensão de tag do Web SDK, você é levado automaticamente para a página [Configuração](configure/config-overview.md).

1. Na [seção Datastreams](configure/datastreams.md), selecione a sequência de dados desejada para cada ambiente.

Todas as outras configurações são preenchidas para você ou opcionais. Defina quaisquer definições de configuração desejadas e selecione **[!UICONTROL Save]**.

## Criar um elemento de dados variável

A Adobe recomenda usar elementos de dados [Variável](data-element-types.md#variable) para armazenar a carga que você deseja enviar para o Adobe. Os objetos XDM também são elementos de dados disponíveis, mas são mais antigos e limitados nos casos de uso aplicáveis.

1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Selecione **[!UICONTROL Data elements]** > **[!UICONTROL Create new data element]**.
1. Forneça ao elemento de dados as seguintes propriedades à esquerda:
   * **[!UICONTROL Name]**: Qualquer nome desejado
   * **[!UICONTROL Extension]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Data element type]**: [!UICONTROL Variable]
1. Defina as seguintes propriedades à direita:
   **Tipo de variável**: XDM
   **[!UICONTROL Sandbox]**: a sandbox na qual você criou seu esquema
   **[!UICONTROL Schema]**: o esquema desejado
1. Selecione **[!UICONTROL Save]**.

## Criar uma regra

As regras determinam quando você deseja acionar algo ou definir variáveis. A criação de uma regra que é executada sempre que a biblioteca é carregada permite preencher facilmente variáveis que você deseja que contenham um valor em cada página.

1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Selecione **[!UICONTROL Rules]** > **[!UICONTROL Add rule]**.
1. Dê um nome desejado à regra.
1. Selecione o ícone &#39;`+`&#39; ao lado de **[!UICONTROL Events]**.
1. Atribua ao evento as seguintes configurações:
   * **[!UICONTROL Extension]**: [!UICONTROL Core]
   * **[!UICONTROL Event type]**: [!UICONTROL Library loaded (page top)]
1. Selecione **[!UICONTROL Keep changes]**.

As etapas acima estabelecem a parte de critérios da regra, que é acionada quando a biblioteca é carregada. As etapas a seguir estabelecem as medidas a serem tomadas quando esses critérios forem atendidos.

1. Selecione o ícone &#39;`+`&#39; ao lado de **[!UICONTROL Actions]**.
1. Atribua à ação as seguintes configurações à esquerda:
   * **[!UICONTROL Extension]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Action type]**: [!UICONTROL Send event]
1. Defina os seguintes campos à direita:
   * **[!UICONTROL XDM]**: o elemento de dados da variável XDM
1. Selecione **[!UICONTROL Keep changes]**.

![Configuração de ação](assets/getting-started/action-config.png)

## Publicação

A propriedade da tag contém todos os componentes necessários para enviar dados para a Edge Network.

1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Publishing flow]**.
1. Selecione **[!UICONTROL Add library]**.
1. Dê um nome desejado à biblioteca. Considere esse nome semelhante a um nome de confirmação ao trabalhar no software de controle de versão.
1. Defina o menu suspenso de ambiente como **[!UICONTROL Development]**.
1. Selecione **[!UICONTROL Add all changed resources]**.
1. Selecione **[!UICONTROL Save & build to Development]**.

Suas alterações agora são implantadas no ambiente de desenvolvimento.

1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Environments]**.
1. Selecione o ícone de instalação ao lado do ambiente de desenvolvimento
1. Instale o código incorporado em uma página da Web de teste no site.

Depois de validar que a tag funciona no ambiente de desenvolvimento, você poderá usar a interface do [!UICONTROL Publishing flow] para publicar a biblioteca no ambiente de preparo e, em seguida, no ambiente de produção.

1. Adicione a extensão e a regra a uma **Biblioteca**, crie-a em um **Ambiente** e instale o código de inserção no site.
2. Validar com **Adobe Experience Platform Debugger**.

Agora você tem uma configuração de lean que captura eventos e os envia para a Edge Network. Agora, você pode aumentar ainda mais a implementação adicionando campos ao esquema, produtos a um fluxo de dados ou elementos de dados à propriedade de tag.
