---
title: Extensões
description: Saiba como as extensões de tag funcionam no Adobe Experience Platform.
source-git-commit: 5b8ef30b1d0e6d682c94453117677c806eba1e02
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 77%

---

# Extensões

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Uma extensão é um conjunto de código empacotado que estende as funcionalidades fornecidas por tags ou pelo encaminhamento de eventos.

A adição de uma extensão inclui novos elementos de dados e novas opções para a criação de regras.

As extensões determinam os elementos que estão disponíveis ao construir propriedades, regras e elementos de dados. Elas fornecem:

* Eventos, condições e exceções
* Elementos de dados
* Código do lado do cliente

Use os links na parte superior da lista de extensões para exibir as extensões instaladas, o catálogo de extensões ou as atualizações.

Selecione uma extensão e depois selecione [!UICONTROL Configurar] para ver e alterar as configurações da extensão. Consulte [Adicionar uma nova extensão](#add-a-new-extension) para obter informações sobre opções de extensão.

>[!IMPORTANT]
>
>As alterações não entrarão em vigor até serem [publicadas](../../publishing/overview.md).

Por padrão, o Adobe fornece extensões que oferecem suporte a integrações comuns. As extensões podem ser modificadas com configurações personalizadas. Configurações são fornecidas por meio das extensões. Para criar uma configuração, selecione o cartão de extensão e, em seguida, selecione **[!UICONTROL Adicionar nova configuração]**.

Para obter uma introdução ao vídeo, consulte [Extensões](../../../quick-start/videos.md).

## Catálogo de extensões

Use o catálogo de extensões para procurar, configurar e implantar tecnologia de marketing e publicidade projetada e mantida por fornecedores de software independentes, bem como extensões para soluções de Adobe.

A página Extensões fornece três exibições:

* instalados

   Mostra todas as extensões instaladas.

* Catálogo
* Mostra todas as extensões disponíveis.
* Atualizações

   Mostra as atualizações de extensões instaladas.

Selecione **[!UICONTROL Extensões]** para ver todas as extensões instaladas. Você também pode usar o catálogo para ver uma lista de todas as extensões disponíveis e quais extensões têm atualizações disponíveis.

Consulte [Referência de extensões](../../../extensions/web/overview.md) para obter detalhes sobre as extensões de propriedade do Adobe.

## Adicione uma nova extensão {#add-a-new-extension}

As tags são altamente extensíveis. Extensões adicionam funcionalidades importantes às tags. Um uso comum das extensões é criar integrações com outros aplicativos.

1. Na página de visão geral de uma propriedade, abra a guia **[!UICONTROL Extensões]**.
1. Selecione uma extensão.

   ![]()../../../images/extensions.png)

   * Se a extensão existir, selecione-a no catálogo de extensões.
   * Passe o mouse sobre uma extensão na lista para configurá-la ou desativá-la.
   * Adicione outras extensões no catálogo, se elas não estiverem na lista.

   A extensão principal é o ponto de partida para a nova extensão. A extensão padrão fornece:

   * Evento padrão
   * Condições e exceções padrão
   * Código padrão do lado do cliente

   Esses padrões são a base para as regras personalizadas que você criará para produzir sua extensão.

Ao criar ou editar elementos, você pode salvar e construir sua [biblioteca ativa](../../publishing/libraries.md#active-library). Isso salva imediatamente sua alteração na biblioteca e executa uma build. O status da build será exibido. Você também pode criar uma nova biblioteca no menu suspenso Biblioteca ativa.

## Configurar uma extensão

Passe o mouse sobre uma extensão instalada e selecione **[!UICONTROL Configurar]**.

>[!NOTE]
>
>Algumas extensões não exigem configuração e não oferecem opções de configuração.

Cada extensão configurável tem opções exclusivas. Consulte [Referência de extensões](../../../extensions/web/overview.md) para obter informações sobre as opções disponíveis para cada extensão do Adobe.
