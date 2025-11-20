---
keywords: Experience Platform;perfil;perfil de cliente em tempo real;perfil unificado;Perfil unificado;unificado;Perfil;rtcp;habilitar perfil;Habilitar perfil;esquema de união;PERFIL DE UNIÃO;perfil de união
title: Guia da interface do usuário do esquema de união
type: Documentation
description: Na interface (UI) do Adobe Experience Platform, é possível visualizar facilmente qualquer esquema de união na organização e visualizar os campos, identidades, relacionamentos e esquemas de contribuição de uma classe específica. Este guia fornece informações detalhadas sobre como visualizar e explorar esquemas de união usando a interface do Experience Platform.
exl-id: 52af0d77-e37d-4ed8-9dee-71a50b337b4e
source-git-commit: b7f5f08d5b3632a2d80c39559a5fb5116d9567f8
workflow-type: tm+mt
source-wordcount: '1190'
ht-degree: 0%

---

# [!UICONTROL Union schema] Guia da interface

Na interface (UI) do Adobe Experience Platform, é possível visualizar facilmente qualquer esquema de união na organização e visualizar os campos, identidades, relacionamentos e esquemas de contribuição de uma classe específica. Este guia fornece informações detalhadas sobre como visualizar e explorar esquemas de união usando a interface do Experience Platform.

## Introdução {#getting-started}

Este guia de interface do usuário requer uma compreensão dos vários serviços do [!DNL Experience Platform] envolvidos no gerenciamento de dados do Perfil do Cliente em Tempo Real. Antes de ler este guia ou trabalhar na interface do usuário, consulte a documentação dos seguintes serviços:

* [[!DNL Real-Time Customer Profile]](../home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
* [[!DNL Identity Service]](../../identity-service/home.md): Habilita [!DNL Real-Time Customer Profile] unindo identidades de fontes de dados diferentes conforme elas são assimiladas em [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): a estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.

## Noções básicas união schemas {#understanding-union-schemas}

>[!CONTEXTUALHELP]
>id="rtcdp_collaboration_union_schema"
>title="Schemas de união"
>abstract=""

<!-- The above contextual help is used in the Collaboration UI for a read more link. -->

O Perfil do cliente em tempo real permite criar perfis robustos e centralizados contendo atributos do cliente e eventos com carimbos de data e hora a cada interação com o cliente em todos os sistemas integrados a Adobe Experience Platform. O formato e a estrutura desses dados são fornecidos pelos esquemas do Experience Data Model (XDM), com cada schema sendo baseados em uma classe XDM e contendo campos compatíveis com essa classe.

Esquemas podem ser criados para vários casos de uso, fazendo referência à mesma classe, mas contendo campos específicos para seu uso. Quando um esquema é ativado para Perfil, ele se torna parte de um esquema de união. Em outras palavras, os esquemas de união são compostos de vários esquemas que compartilham a mesma classe e foram ativados para Perfil. O esquema de união permite ver uma combinação de todos os campos contidos em esquemas que compartilham a mesma classe. O Perfil do cliente em tempo real usa o esquema de união para criar uma visualização integral de cada cliente individual.

Trabalhar com esquemas de união requer uma compreensão profunda dos esquemas XDM. Para obter mais informações, comece lendo as [noções básicas da composição de esquema](../../xdm/schema/composition.md).

## Exibir esquemas de união {#view-union-schemas}

Para navegar para união schemas na interface de Experience Platform, selecione **[!UICONTROL Profiles]** na navegação esquerda e selecione o **[!UICONTROL Union Schema]** guia. A guia [!UICONTROL Union Schema] é aberta para exibir o esquema de união para a classe selecionada no momento.

![A página Esquema de União é exibida, com as guias Perfil e Esquema de União realçadas.](../images/union-schema/landing.png)

## Selecionar uma classe {#select-a-class}

Para exibir o esquema de união para uma classe XDM específica, selecione a classe na lista suspensa **[!UICONTROL Class]**. Devido ao fato de que nem todas as classes têm esquemas de união, somente as classes com esquemas de união (ou seja, classes com esquemas que foram ativados para Perfil) estão disponíveis na lista suspensa.

Depois que uma classe é selecionada, o esquema exibido é atualizado para refletir o esquema de união para a classe selecionada. Por exemplo, você pode selecionar **[!UICONTROL XDM Individual Profile]** para visualizar o esquema de união para essa classe.

![Uma lista suspensa contendo as classes do esquema de união está realçada.](../images/union-schema/class.png)

## Explorar esquemas de união {#explore-union-schemas}

Você pode explorar o esquema de união rolando para cima e para baixo para visualizar a estrutura completa do esquema e selecionando um colchete angular direito (`>`) para expandir campos aninhados.

![Um conjunto de campos aninhados no esquema de união foi expandido.](../images/union-schema/explore.png)

Selecione qualquer campo para exibir seus detalhes, incluindo nome de exibição, tipo de dados, descrição, caminho, data de criação e data da última modificação. Você também pode exibir uma lista de esquemas contribuintes contendo o campo selecionado.

![Um campo de união schema é destacado. Os detalhes sobre o campo destacado são exibidos na barra lateral direita.](../images/union-schema/explore-field.png)

Selecionar o nome de um schema contribuinte revela os nomes dos conjuntos de dados relacionados a esse schema que estão assimilando dados no campo selecionado. Cada nome conjunto de dados aparece como uma link. Selecionar um conjunto de dados nome abre a guia de atividade para esse conjunto de dados em uma nova janela.

Para obter mais informações sobre conjuntos de dados, incluindo a visualização conjunto de dados atividade e a visualização de dados do conjunto de dados no interface, visita o guia[ de interface de ](../../catalog/datasets/user-guide.md)conjuntos de dados.

![As lista de conjuntos de dados relacionados ao schema são destacadas.](../images/union-schema/datasets.png)

## Exibir esquemas de contribuição {#view-contributing-schemas}

Você também pode ver quais esquemas específicos estão contribuindo para o esquema de união selecionando **[!UICONTROL All contributing schemas]** para expandir a lista de esquemas. Dependendo da classe selecionada e do número de esquemas criados por sua organização no Experience Platform, pode ser uma lista curta que contém um único esquema ou uma lista longa que contém muitos esquemas.

![A lista de esquemas que contribuem para o esquema de união está realçada.](../images/union-schema/contributing-schemas.png)

Selecionar o nome de uma schema específica realça os campos no união schema que fazem parte do schema que você selecionou. Depois que um schema é selecionado, a união schema aparece acinzentado com barras pretas indicando os campos que fazem parte da schema contribuinte.

![O esquema de contribuição selecionado está realçado. Os campos que fazem parte do esquema de contribuição permanecem em preto, enquanto os campos que não fazem parte do esquema de contribuição estão esmaecidos.](../images/union-schema/select-schema.png)

## Exibir identidades {#view-identities}

Por meio da interface do usuário, é possível exibir uma lista de identidades incluídas no esquema de união selecionando **[!UICONTROL Identities]** para expandir a lista.

![As identidades que pertencem ao esquema de união estão realçadas.](../images/union-schema/identities.png)

Selecionar uma identidade individual na lista faz com que o esquema exibido seja atualizado automaticamente, conforme necessário, para exibir o campo de identidade. Isso pode incluir a expansão de vários campos se o campo de identidade estiver aninhado.

O campo de identidade é destacado dentro da união schema e os detalhes da identidade são exibidos no lado direito da tela. Os detalhes incluem uma lista de esquemas contribuintes contendo o campo de identidade e você pode detalhar encontrar links para os conjuntos de dados relacionados a esse schema que estão assimilando dados no campo de identidade selecionado.

![A identidade selecionada é realçada. Os detalhes sobre a identidade selecionada são exibidos na barra lateral direita.](../images/union-schema/select-identity.png)

## Exibir relações {#view-relationships}

O união schema interface permite ver relacionamentos que foram definidos para esquemas com base na classe schema selecionada. A definição de um relacionamento é uma forma de conectar dois schemas pertencentes a classes diferentes no solicitar para obter insights mais complexos sobre os dados dos clientes.

Se as relações tiverem sido estabelecidas para a classe selecionada, selecionar **[!UICONTROL Relationships]** exibirá uma lista de campos usados para criar relações. Nem todos os esquemas usam ou precisam de relacionamentos definidos, portanto, é comum que a seção relacionamentos não contenha campos.

Para saber mais sobre relações de esquema, incluindo como defini-las usando a interface, visite [este documento sobre relações de esquema](../../xdm/tutorials/relationship-ui.md).

![As relações que pertencem ao esquema de união estão realçadas.](../images/union-schema/relationships.png)

Selecionar um campo de relacionamento na lista faz com que o esquema exibido seja atualizado conforme necessário para exibir o campo de relacionamento destacado. Isso pode incluir a expansão de vários campos se o campo de relacionamento estiver aninhado.

![A relação selecionada está realçada. O campo correspondente da relação também é destacado.](../images/union-schema/select-relationship.png)

## Próximas etapas

Ao ler este guia, agora você sabe como visualizar e navegar pelos esquemas de união usando a interface do usuário do [!DNL Experience Platform]. Para obter mais informações sobre esquemas, incluindo como eles são usados em toda a Experience Platform, comece lendo a [visão geral do Sistema XDM](../../xdm/home.md).
