---
title: Visão geral da extensão de demonstração da Adobe Experience Platform
description: Saiba mais sobre a extensão de demonstração da Adobe Experience Platform no Adobe Experience Platform.
source-git-commit: 1d3415146335d3011963c969d5b6aeea1f1a51d0
workflow-type: tm+mt
source-wordcount: '1068'
ht-degree: 85%

---

# Extensão demo do Adobe Experience Platform

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

>[!NOTE]
>
>Essa extensão será substituída pelo [SDK da Web da Adobe Experience Platform](../sdk/overview.md).

Os recursos desta extensão estão sendo transmitidos para uma nova extensão. Veja uma rápida comparação dos recursos atuais.

| Extensão de demonstração da Platform | SDK da Web da Platform |
| ------------------ | ----------- |
| Suporte para IDs personalizadas do cliente | Suporte para IDs personalizadas do cliente |
| Interface do usuário de mapeamento do lado do cliente para XDM | Criar NA ECID (não é necessário para visitor.js) |
| Capacidade de criar uma conexão de streaming | Suporte para aceitação |
|  | Suporte XDM como um elemento de dados |
|  | Suporte para domínio próprio |
|  | Ferramentas de depuração integradas |
|  | Coletar automaticamente o contexto do navegador |
|  | Fonte totalmente aberta |


## Configurar a extensão da Adobe Experience Platform

Esta seção fornece uma referência para as opções disponíveis ao configurar a extensão da Adobe Experience Platform.

Se a extensão da Adobe Experience Platform ainda não tiver sido instalada, abra a propriedade e selecione **[!UICONTROL Extensões > Catálogo]**, passe o mouse sobre a extensão da Adobe Experience Platform e selecione **[!UICONTROL Instalar]**.

Para configurar a extensão, abra a guia [!UICONTROL Extensões], passe o mouse sobre a extensão e selecione **[!UICONTROL Configurar]**.

![](../../../images/adobe-experience-platform-extension-configuration.png)

### Conexão de transmissão

Escolher uma conexão de transmissão é a primeira etapa para iniciar a transmissão de dados para a Adobe Experience Platform. Você pode selecionar uma opção na caixa de combinação com as conexões de transmissão. A conexão de transmissão é um campo obrigatório. Caso ainda não tenha uma conexão de streaming, você poderá criar uma selecionando o botão **[!UICONTROL Criar uma conexão de streaming]**.

Se você selecionar **[!UICONTROL Criar uma conexão de streaming]**, uma janela modal será exibida.

![](../../../images/adobe-experienc-platform-create-streaming-connection.png)

A modal contém campos com valores pré-preenchidos que podem ser alterados para atender às suas necessidades. Se você planeja criar mais de uma conexão de transmissão, deve estar ciente de que o campo **[!UICONTROL Data Source]** precisa ser exclusivo. Tentar criar outra conexão de streaming usando uma **[!UICONTROL Fonte de dados]** já em uso em outra conexão causará uma falha.

Depois de ter selecionado um endpoint de transmissão, você será o URL e a fonte do endpoint de transmissão.

![](../../../images/adobe-experience-platform-streaming-endpoint-selected.png)

## Tipos de ação da extensão da Adobe Experience Platform

Esta seção descreve os tipos de ação disponíveis na extensão da Adobe Experience Platform.

### Enviar sinal {#send-beacon}

Esse é o tipo de ação que você usará para enviar dados para a Adobe Experience Platform.

![](../../../images/adobe-experience-platform-send-beacon-dataset.png)

Primeiro, selecione o conjunto de dados em que os dados serão armazenados. Geralmente, os conjuntos de dados representam uma tabela que armazena os dados enviados pela conexão de transmissão. É necessário criar os conjuntos de dados dentro da Adobe Experience Platform antes de usar este tipo de ação.

![](../../../images/adobe-experience-platform-send-beacon-dataset-selected1.png)

Depois de selecionar o conjunto de dados em que os dados serão armazenados, você verá detalhes sobre o esquema vinculado ao conjunto de dados selecionado.

### Mapeamento do esquema

Depois de selecionar o conjunto de dados, você pode definir o mapeamento do esquema.

![](../../../images/adobe-experience-platform-send-beacon-schema-mapping.png)

O campo de valor de origem aceita um valor ou um elemento de dados. É possível adicionar um elemento de dados selecionando o botão de elemento de dados ao lado do campo de valor de origem.

O campo Esquema de destino contém o caminho de um campo XDM definido no esquema do conjunto de dados. Para campos definidos mais profundamente na hierarquia de esquema, você pode usar o ponto como separador entre as partes do caminho (por exemplo, timeSeriesEvents.eventType).

### Seletor de campo de esquema

A extensão oferece também a possibilidade de selecionar um campo Esquema de destino usando um seletor visual. Se você selecionar o botão ao lado da entrada do campo de esquema de destino, será exibido um modal em que você verá a árvore do esquema do conjunto de dados. Você pode escolher um campo e, em seguida, clicar no botão **Selecionar**, e a entrada do campo Esquema de destino será atualizada com o caminho XDM correto.

![](../../../images/adobe-experience-platform-send-beacon-schema-field-selector.png)

### Campos de identidade dentro da Adobe Experience Platform

Esquemas de registro de dados e esquemas de dados de séries de tempo podem conter um ou mais campos de identidade. Campos de identidade se juntam para formar uma única representação de identidade de uma indivíduo e incluem informações como um identificador CRM, o Experience Cloud ID (ECID), um cookie do navegador, o AdvertisingId ou outras IDs em diferentes domínios.

Os campos de identidade podem ser definidos de duas formas dentro do esquema:

1. Os esquemas Gravar e Série de tempo contêm um campo especial chamado `xdm:identityMap` que pode conter um mapa de identidades.
1. Os campos principais podem ser marcados como campos de &quot;identidade&quot; dentro do esquema.

### Campos de identidade dentro da extensão da Adobe Experience Platform

Para cada campo de esquema definido como um campo de identidade, uma linha será adicionada à seção de mapeamento do esquema. Cada linha adicionada conterá o campo Esquema de destino já preenchido com o caminho do esquema XDM correspondente. Você pode reconhecer se um campo de esquema também é um campo de identidade caso veja um ícone de perfil próximo ao campo.

![](../../../images/adobe-experience-platform-send-beacon-identity-field.png)

Os campos de identidade primários são sempre obrigatórios, portanto, não é possível excluir as linhas que os contêm da seção de mapeamento de esquema.

Um campo de esquema definido como um campo de identidade não primário será automaticamente adicionado à seção de mapeamento de esquema, mas a entrada do valor de origem poderá permanecer vazia. Esse campo pode ser excluído. O campo será descartado se a entrada do valor de origem correspondente estiver vazia.

![](../../../images/adobe-experience-platform-send-beacon-identity-field-warning.png)

Você verá um ícone de aviso próximo de cada campo de identidade não primário que não contenha um valor.

Uma seção de identidades estará visível se o esquema contiver um campo `xdm:identityMap`. Você pode usar esta seção se preferir enviar dados relacionados às identidades usando o `xdm:identityMap`.

![](../../../images/adobe-experience-platform-send-beacon-identity-section.png)

A seção Mapeamento de identidades pode conter várias linhas. Cada linha pode definir um determinado tipo de identidade. Você pode definir os seguintes atributos para uma identidade: tipo, estado autenticado, principal e valor.

Se você tiver várias identidades dentro da seção Mapeamento de identidade, apenas uma identidade pode ser marcada como primária.

Se um esquema tiver um campo `xdm:identityMap` e, ao mesmo tempo, outro campo for marcado como um campo de identidade primário, a coluna primária dentro da seção Mapeamento de identidade não estará visível.

![](../../../images/adobe-experience-platform-send-beacon-identity-section-not-primary.png)

### Campos obrigatórios

Alguns esquemas terão campos obrigatórios de nível superior. Os mais comuns são `timestamp` e `_id`. Sem definir esses campos, o sinal falhará. Você pode defini-los dentro da seção Mapeamento de esquema.

Se a seção Mapeamento de esquema não contiver `timestamp` ou `_id`, mas o esquema de conjunto de dados exigi-los, a extensão da Adobe Experience Platform enviará um sinal contendo valores gerados automaticamente para que o sinal não falhe. Os valores gerados automaticamente serão adicionados aos dados do sinal somente se você não tiver definido esses campos dentro da seção Mapeamento de esquema.
