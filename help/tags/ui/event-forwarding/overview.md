---
title: Visão geral do encaminhamento de eventos
description: Saiba mais sobre o encaminhamento de eventos da Adobe Experience Platform, que permite usar a Platform Edge Network para executar tarefas sem alterar a sua implementação de tag.
feature: Event Forwarding
exl-id: 18e76b9c-4fdd-4eff-a515-a681bc78d37b
source-git-commit: b445e25ebda39e1604b926dc40d8ed52ad2e9b54
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 9%

---

# Visão geral do encaminhamento de eventos

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

O encaminhamento de eventos no Adobe Experience Platform permite enviar dados de eventos coletados para um destino para processamento no servidor. O encaminhamento de eventos diminui o peso da página da Web e do aplicativo usando a Rede de Borda da Adobe Experience Platform para executar tarefas normalmente realizadas no cliente. Implementado de maneira semelhante às tags, as regras de encaminhamento do evento podem transformar e enviar dados para novos destinos, mas em vez de enviar esses dados de um aplicativo cliente, como um navegador da Web, é enviado dos servidores Adobe.

Este documento fornece uma visão geral de alto nível do encaminhamento de eventos no Platform.

![Encaminhamento de eventos no ecossistema de coleta de dados](../../../collection/images/home/event-forwarding.png)

>[!NOTE]
>
>Para obter informações sobre como o encaminhamento de eventos se encaixa no ecossistema de coleta de dados no Platform, consulte o [visão geral da coleta de dados](../../../collection/home.md).

Encaminhamento de eventos combinado à Adobe Experience Platform [Web SDK](../../../edge/home.md) e [SDK móvel](https://aep-sdks.gitbook.io/docs/) oferece os seguintes benefícios:

**Desempenho**:

* Faça uma única chamada em uma página que contenha uma carga de dados que se federe no lado do servidor para reduzir o tráfego de rede do lado do cliente e fornecer uma experiência mais rápida para os clientes.
* Diminua o tempo que leva para páginas da Web serem carregadas para melhorar o desempenho do site.
* Diminua o número de tecnologias necessárias do lado do cliente para fornecer sua experiência e enviar dados para vários destinos.

**Governança de dados**:

* Aumente a transparência e o controle sobre quais dados são enviados em todas as propriedades.

## Diferenças entre o encaminhamento de eventos e as tags {#differences-from-tags}

Em termos de configuração, o encaminhamento de eventos usa muitos dos mesmos conceitos que as tags, como [regras](../managing-resources/rules.md), [elementos de dados](../managing-resources/data-elements.md)e [extensões](../managing-resources/extensions/overview.md). A principal diferença entre as duas pode ser resumida da seguinte forma:

* Tags **coleções** dados de evento de um site ou aplicativo móvel nativo e os envia para a Rede de borda da plataforma.
* Encaminhamento de evento **envios** dados de evento de entrada da Rede de borda da plataforma para um terminal que representa um destino final ou um terminal que fornece dados com os quais você deseja enriquecer a carga original.

Enquanto as tags coletam dados de evento diretamente do seu site ou aplicativo móvel nativo usando SDKs da Web da plataforma e móveis, o encaminhamento de eventos requer que os dados de eventos já sejam enviados pela Rede de borda da plataforma para encaminhá-los para destinos. Em outras palavras, você deve implementar o SDK móvel ou da Web da plataforma em sua propriedade digital (por meio de tags ou usando código bruto) para usar o encaminhamento do evento.

### Propriedades {#properties}

O encaminhamento de eventos mantém seu próprio armazenamento de propriedades separado das tags, que podem ser exibidas na interface do usuário da coleta de dados ao selecionar **[!UICONTROL Encaminhamento de evento]** no painel de navegação esquerdo.

![Propriedades de encaminhamento de eventos na interface do usuário da coleção de dados](../../images/ui/event-forwarding/overview/properties.png)

Toda a lista de propriedades de encaminhamento de eventos **[!UICONTROL Edge]** como sua plataforma. Eles não fazem distinção entre Web ou dispositivos móveis porque processam apenas dados recebidos da Rede de Borda da Plataforma, que pode receber dados de evento das plataformas da Web e móvel.

### Extensões {#extensions}

O encaminhamento de eventos tem seu próprio catálogo de extensões compatíveis, como o [Núcleo](../../extensions/web/core/event-forwarding.md) extensão e [Conector da nuvem do Adobe](../../extensions/web/cloud-connector/overview.md) extensão. Você pode exibir as extensões disponíveis para as propriedades de encaminhamento de eventos na interface do usuário selecionando **[!UICONTROL Extensões]** no painel de navegação esquerdo, seguido de **[!UICONTROL Catálogo]**.

![Extensões de encaminhamento de eventos na interface do usuário da coleção de dados](../../images/ui/event-forwarding/overview/extensions.png)

### Elementos de dados {#data-elements}

Os tipos de elementos de dados que estão disponíveis no encaminhamento de eventos são limitados ao catálogo de [extensões](#extensions) que os fornecem.

Embora os elementos de dados em si sejam criados e configurados da mesma maneira no encaminhamento do evento que são para as tags, há algumas diferenças importantes na sintaxe quando se trata de como eles fazem referência aos dados da Rede de borda da plataforma.

#### Referência de dados da rede de borda da plataforma {#data-element-path}

Para fazer referência aos dados da Rede de Borda da Plataforma, você deve criar um elemento de dados que forneça um caminho válido para esses dados. Ao criar o elemento de dados na interface do usuário, selecione **[!UICONTROL Núcleo]** para a extensão e **[!UICONTROL Caminho]** para o tipo .

O **[!UICONTROL Caminho]** o valor do elemento de dados deve seguir o padrão `arc.event.{ELEMENT}` (por exemplo: `arc.event.xdm.web.webPageDetails.URL`). Esse caminho deve ser especificado corretamente para que os dados sejam enviados.

![Exemplo de um elemento de dados do tipo de caminho para o encaminhamento de eventos](../../images/ui/event-forwarding/overview/data-reference.png)

### Regras {#rules}

A criação de regras no encaminhamento de eventos das propriedades funciona de maneira semelhante às tags, sendo que não é possível selecionar eventos como componentes da regra. Em vez disso, uma regra de encaminhamento de eventos processa todos os eventos que recebe da variável [datastream](../../../edge/datastreams/overview.md) e encaminhar esses eventos para destinos, se determinadas condições forem satisfeitas.

![Regras de encaminhamento de eventos na interface do usuário da coleção de dados](../../images/ui/event-forwarding/overview/rules.png)

#### Tokenização do elemento de dados {#tokenization}

Nas regras de tags, os elementos de dados são tokenizados com um `%` no início e no fim do nome do elemento de dados (por exemplo: `%viewportHeight%`). Nas regras de encaminhamento de eventos, os elementos de dados são tokenizados com `{{` no início e `}}` no final do nome do elemento de dados (por exemplo: `{{viewportHeight}}`).

![Exemplo de um elemento de dados do tipo de caminho para o encaminhamento de eventos](../../images/ui/event-forwarding/overview/tokenization.png)

#### Sequência de ações de regras {#action-sequencing}

O [!UICONTROL Ações] A seção de uma regra de encaminhamento de evento é sempre executada sequencialmente. Certifique-se de que a ordem das ações esteja correta ao salvar uma regra. Essa sequência de execução não pode ser executada de forma assíncrona como pode com tags .

## Segredos {#secrets}

O encaminhamento de eventos permite criar, gerenciar e armazenar segredos que podem ser usados para autenticar nos servidores para os quais você está enviando dados. Consulte o guia sobre [segredos](./secrets.md) sobre os diferentes tipos de segredo disponíveis e como eles são implementados na interface do usuário do .

## Próximas etapas

Este documento forneceu uma introdução de alto nível ao encaminhamento de eventos. Para obter mais informações sobre como configurar esse recurso para sua organização, consulte o [guia de introdução](./getting-started.md).
