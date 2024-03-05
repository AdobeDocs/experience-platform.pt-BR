---
title: Visão geral do encaminhamento de eventos
description: Saiba mais sobre o encaminhamento de eventos da Adobe Experience Platform, que permite usar a Platform Edge Network para executar tarefas sem alterar a sua implementação de tag.
feature: Event Forwarding
exl-id: 18e76b9c-4fdd-4eff-a515-a681bc78d37b
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '1064'
ht-degree: 8%

---

# Visão geral do encaminhamento de eventos

>[!NOTE]
>
>O encaminhamento de eventos é um recurso pago incluído como parte das ofertas do Adobe Real-time Customer Data Platform Connections, Prime ou Ultimate.

>[!NOTE]
>
>O Adobe Experience Platform Launch foi reformulado como um conjunto de tecnologias de coleção de dados na Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

O encaminhamento de eventos no Adobe Experience Platform permite enviar dados de eventos coletados para um destino para processamento no lado do servidor. O encaminhamento de eventos diminui o peso da página da Web e do aplicativo usando a Rede de borda da Adobe Experience Platform para executar tarefas normalmente realizadas no cliente. Implementadas de maneira semelhante às tags, as regras de encaminhamento de eventos podem transformar e enviar dados para novos destinos, mas em vez de enviar esses dados de um aplicativo cliente como um navegador da Web, eles são enviados de servidores Adobe.

Este documento fornece uma visão geral de alto nível do encaminhamento de eventos na Platform.

![Encaminhamento de eventos no ecossistema de coleta de dados](../../../collection/images/home/event-forwarding.png)

>[!NOTE]
>
>Para obter informações sobre como o encaminhamento de eventos se encaixa no ecossistema de coleta de dados da Platform, consulte o [visão geral da coleção de dados](../../../collection/home.md).

Encaminhamento de eventos combinado com o Adobe Experience Platform [SDK da Web](/help/web-sdk/home.md) e [SDK móvel](https://experienceleague.adobe.com/docs/platform-learn/data-collection/mobile-sdk/overview.html) oferece os seguintes benefícios:

**Desempenho**:

* Fazer uma única chamada de uma página que contém uma carga de dados que é federada no lado do servidor para reduzir o tráfego de rede do lado do cliente e fornecer uma experiência mais rápida aos clientes.
* Diminuir o tempo de carregamento das páginas da Web para melhorar o desempenho do site.
* Diminua o número de tecnologias necessárias do lado do cliente para fornecer sua experiência e enviar dados para muitos destinos.

**Governança de dados**:

* Aumentar a transparência e o controle sobre quais dados são enviados e para onde, em todas as propriedades.

## Diferenças entre o encaminhamento de eventos e as tags {#differences-from-tags}

Em termos de configuração, o encaminhamento de eventos usa muitos dos mesmos conceitos que as tags, como [regras](../managing-resources/rules.md), [elementos de dados](../managing-resources/data-elements.md), e [extensões](../managing-resources/extensions/overview.md). A principal diferença entre os dois pode ser resumida da seguinte forma:

* Tags **coleta** dados do evento de um site ou aplicativo móvel nativo e os envia para a Platform Edge Network.
* Encaminhamento de eventos **envia** dados de evento de entrada da Platform Edge Network para um endpoint que representa um destino final ou um endpoint que fornece dados com os quais você deseja enriquecer a carga original.

Embora as tags coletem dados do evento diretamente do seu site ou aplicativo móvel nativo usando os SDKs da Web e móvel da Platform, o encaminhamento de eventos exige que os dados do evento já sejam enviados pela Rede de borda da Platform para encaminhá-los aos destinos. Em outras palavras, você deve implementar o SDK da Web ou móvel da Platform na sua propriedade digital (por meio de tags ou usando código bruto) para usar o encaminhamento de eventos.

### Propriedades {#properties}

O encaminhamento de eventos mantém seu próprio armazenamento de propriedades separadas das tags, que podem ser visualizadas na interface do usuário do Experience Platform ou na interface da Coleção de dados ao selecionar **[!UICONTROL Encaminhamento de evento]** no painel de navegação esquerdo.

![Propriedades de encaminhamento de eventos na interface da Coleção de dados](../../images/ui/event-forwarding/overview/properties.png)

Lista de propriedades de todo o encaminhamento de eventos **[!UICONTROL Edge]** como sua plataforma. Eles não fazem distinção entre Web ou dispositivos móveis porque processam apenas dados recebidos da Platform Edge Network, que pode receber dados do evento de plataformas da Web e móveis.

### Extensões {#extensions}

O encaminhamento de eventos tem seu próprio catálogo de extensões compatíveis, como o [Núcleo](../../extensions/server/core/overview.md) extensão e [Adobe Cloud Connector](../../extensions/server/cloud-connector/overview.md) extensão. É possível visualizar as extensões disponíveis para as propriedades do encaminhamento de eventos na interface do usuário selecionando **[!UICONTROL Extensões]** na navegação à esquerda, seguido por **[!UICONTROL Catálogo]**.

![Extensões de encaminhamento de eventos na interface da Coleção de dados](../../images/ui/event-forwarding/overview/extensions.png)

### Elementos de dados {#data-elements}

Os tipos de elementos de dados disponíveis no encaminhamento de eventos estão limitados ao catálogo de [extensões](#extensions) que os fornecem.

Embora os elementos de dados em si sejam criados e configurados da mesma forma no encaminhamento de eventos que para tags, há algumas diferenças de sintaxe importantes quando se trata de como eles fazem referência a dados da Rede de borda da Platform.

#### Fazendo referência a dados da Platform Edge Network {#data-element-path}

Para referenciar dados da Platform Edge Network, você deve criar um elemento de dados que forneça um caminho válido para esses dados. Ao criar o elemento de dados na interface do usuário, selecione **[!UICONTROL Núcleo]** para a extensão e **[!UICONTROL Caminho]** para o tipo.

A variável **[!UICONTROL Caminho]** O valor do elemento de dados deve seguir o padrão `arc.event.{ELEMENT}` (por exemplo: `arc.event.xdm.web.webPageDetails.URL`). Esse caminho deve ser especificado corretamente para que os dados sejam enviados.

![Exemplo de um elemento de dados de tipo de caminho para encaminhamento de eventos](../../images/ui/event-forwarding/overview/data-reference.png)

### Regras {#rules}

A criação de regras nas propriedades do encaminhamento de eventos funciona de maneira semelhante às tags, com a principal diferença sendo que não é possível selecionar eventos como componentes de regra. Em vez disso, uma regra de encaminhamento de eventos processa todos os eventos que recebe da [sequência de dados](../../../datastreams/overview.md) e encaminhará esses eventos para destinos se determinadas condições forem atendidas.

Além disso, há um tempo limite de 30 segundos que se aplica a um único evento, pois ele é processado em todas as regras (e, portanto, todas as ações) em uma propriedade de encaminhamento de eventos. Isso significa que todas as regras e ações para um único evento devem ser concluídas nesse período.

![Regras de encaminhamento de eventos na interface da Coleção de dados](../../images/ui/event-forwarding/overview/rules.png)

#### Tokenização do elemento de dados {#tokenization}

Nas regras de tags, os elementos de dados são tokenizados com um `%` no início e no fim do nome do elemento de dados (por exemplo: `%viewportHeight%`). Nas regras de encaminhamento de eventos, os elementos de dados são tokenizados com `{{` no início e `}}` no final do nome do elemento de dados (por exemplo: `{{viewportHeight}}`).

![Exemplo de um elemento de dados de tipo de caminho para encaminhamento de eventos](../../images/ui/event-forwarding/overview/tokenization.png)

#### Sequência de ações de regras {#action-sequencing}

A variável [!UICONTROL Ações] de uma regra de encaminhamento de eventos é sempre executada sequencialmente. Por exemplo, se uma regra tiver duas ações, a segunda ação não iniciará a execução até que a ação anterior seja concluída (e nos casos em que uma resposta é esperada de um endpoint, esse endpoint respondeu). Certifique-se de que a ordem das ações esteja correta ao salvar uma regra. Essa sequência de execução não pode ser executada de forma assíncrona como com as regras de tag.

## Segredos {#secrets}

O encaminhamento de eventos permite criar, gerenciar e armazenar segredos que podem ser usados para autenticação nos servidores para os quais você está enviando dados. Consulte o guia sobre [segredos](./secrets.md) sobre os diferentes tipos de tipos de segredos disponíveis e como eles são implementados na interface do usuário do.

## Próximas etapas

Este documento forneceu uma introdução de alto nível ao encaminhamento de eventos. Para obter mais informações sobre como configurar esse recurso para sua organização, consulte [guia de introdução](./getting-started.md).
