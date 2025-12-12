---
title: Bibliotecas
description: Saiba mais sobre o conceito de bibliotecas de tags e como elas funcionam na Adobe Experience Platform.
exl-id: 4d6f86e6-5684-4635-aaf1-87ba10cd7d94
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 97%

---

# Bibliotecas

Uma biblioteca é um conjunto de instruções sobre como as extensões, os elementos de dados e as regras interagem entre si após a implantação. Ao criar uma biblioteca, especifique as alterações que você deseja fazer na biblioteca. No momento da criação, essas alterações são combinadas com tudo o que foi enviado, aprovado ou publicado nas bibliotecas anteriores.

As bibliotecas contêm a adição ou remoção de:

* Regras
* Elementos
* Configuração de extensão

As bibliotecas devem ser atribuídas a um ambiente antes de serem compiladas em uma criação. As bibliotecas são aprovadas ou rejeitadas como um todo. Não é possível aprovar ou rejeitar itens individuais em uma biblioteca. Uma biblioteca passa por vários ambientes durante o fluxo de trabalho de publicação.

## Criar uma biblioteca {#create-a-library}

Para criar uma biblioteca, conclua as etapas a seguir.

1. Abra a guia [!UICONTROL Publishing].

   A página [!UICONTROL Publishing] lista as bibliotecas de Desenvolvimento e fornece os meios para enviá-las para aprovação, movê-las para o armazenamento temporário ou publicá-las para produção.

1. Selecione **[!UICONTROL Add New Library]**.

   ![](../../images/library-create.jpg)

1. Dê um nome para a biblioteca.
1. Atribua a biblioteca a um ambiente de Desenvolvimento.
1. Adicione uma alteração à biblioteca.
Para adicionar um item, selecione **[!UICONTROL Add a Change]** e escolha os itens que deseja adicionar. Qualquer item editado ou excluído está disponível para ser adicionado à biblioteca escolhida.

   ![](../../images/library-add-change.jpg)

   Você pode adicionar o seguinte à biblioteca:

   * Regras
   * Elementos de dados
   * Configurações de extensão

1. Para adicionar recursos que foram alterados, selecione **[!UICONTROL Add All Changed Resources]**.
1. Selecione **[!UICONTROL Save]** ou **[!UICONTROL Save and Build for Development]**.

   A implantação compila uma criação e a implanta no ambiente atribuído.

Após criar uma biblioteca, use o menu suspenso dessa biblioteca para selecionar uma das seguintes opções:

* **Editar**: essa opção permite alterar a configuração da biblioteca.

* **Criar para desenvolvimento**: essa opção compila um build e o implanta no ambiente atribuído.

* **Enviar para aprovação**: essa opção disponibiliza a biblioteca para que um Aprovador a mova para a próxima etapa do processo de publicação.

* **Excluir**: essa opção remove a biblioteca selecionada no momento do processo de publicação.

![](../../images/library-menu.png)

## Adicionar a uma biblioteca {#add-to-a-library}

Para adicionar a uma biblioteca, conclua as etapas a seguir.

1. Instale as [extensões](../managing-resources/extensions/overview.md) que deseja adicionar.
1. Crie os [elementos de dados](../managing-resources/data-elements.md) e as regras que deseja adicionar.
1. Abra a guia **[!UICONTROL Publishing]**.
1. Selecione a [biblioteca](libraries.md) que deseja alterar e, em seguida, selecione **[!UICONTROL Edit]**.
1. Use as regras, os elementos de dados e os botões de extensões para selecionar os itens que deseja adicionar à biblioteca.
1. Salve as alterações.

As alterações na biblioteca são mostradas no log de alterações do Conteúdo da biblioteca.

>[!NOTE]
>
>Os elementos de dados podem depender das extensões. As regras podem depender dos elementos de dados e das extensões. Se você não incluir todos os componentes necessários na biblioteca, ocorrerá uma falha no momento da criação e será preciso adicionar os componentes necessários antes de concluir uma criação com sucesso. Uma versão futura verificará as dependências ao fazer alterações em uma biblioteca.

## Remover de uma biblioteca

Para remover um item de uma biblioteca, você deve desativá-lo e publicar o estado desativado.

1. Desabilite as extensões que deseja remover, juntamente com os elementos de dados e as regras que dependem dessas extensões.
1. Desabilite os elementos de dados e as regras que deseja remover.
1. Abra a guia **[!UICONTROL Publishing]**.
1. Selecione a biblioteca que deseja alterar.
1. Use as regras, os elementos de dados e os botões de extensões para selecionar os itens desabilitados que deseja remover da biblioteca.
1. Salve as alterações.

## Gerenciar alterações na biblioteca

Para editar as opções da biblioteca, conclua as etapas a seguir.

1. Escolha uma biblioteca e selecione **[!UICONTROL Edit]** para exibir as alterações nela. Todas as alterações são mostradas na lista [!UICONTROL Library Contents].

   ![](../../images/library-contents.jpg)

1. Selecione uma alteração para exibir e selecionar uma revisão.

   ![](../../images/library-contents-revision.jpg)

1. Selecione se deseja mostrar **todos** os itens ou os itens **alterados**.
1. Selecione a revisão e, em seguida, **[!UICONTROL Select Revision]**.
1. Selecione **[!UICONTROL Add a Change]** ou **[!UICONTROL Add All Changed Resources]**.

## Biblioteca ativa {#active-library}

As bibliotecas encapsulam um conjunto de alterações que você gostaria de fazer no código implantado. A Biblioteca ativa facilita isso, permitindo que você repita rapidamente as alterações e veja o impacto.

Extensões, regras e elementos de dados agora podem ser salvos diretamente na biblioteca em que você está trabalhando. Se necessário, também é possível criar uma nova build ou até mesmo uma nova biblioteca na lista suspensa [!UICONTROL Active Library].

A lista a seguir fornece mais informações sobre o gerenciamento de uma biblioteca ativa.

1. [Crie uma nova biblioteca](libraries.md#create-a-library).
1. Vá para [Regras](../managing-resources/rules.md), [Elementos de dados](../managing-resources/data-elements.md) ou [Extensões](../managing-resources/extensions/overview.md).
1. Selecione a Biblioteca ativa.
1. Faça as alterações, então salve e crie a biblioteca.
1. Teste as alterações e repita essas etapas conforme necessário.
