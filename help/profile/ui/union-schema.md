---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, perfil unificado, perfil unificado, unificado, perfil, rtcp, ativar perfil, Ativar perfil, esquema de união, PERFIL DE UNIÃO, perfil de união
title: Guia da interface do usuário do esquema de união
topic-legacy: guide
type: Documentation
description: Na interface do usuário do Adobe Experience Platform (UI), é possível visualizar facilmente qualquer esquema de união em sua organização e visualizar os campos, identidades, relacionamentos e esquemas de contribuição de uma classe específica. Este guia fornece informações detalhadas sobre como visualizar e explorar schemas de união usando a interface do usuário da plataforma.
exl-id: 52af0d77-e37d-4ed8-9dee-71a50b337b4e
source-git-commit: 681418b4198c2b1303fda937c3ffc60dad21b672
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 3%

---

# [!UICONTROL Schema da União] Guia da interface do usuário

Na interface do usuário do Adobe Experience Platform (UI), é possível visualizar facilmente qualquer esquema de união em sua organização e visualizar os campos, identidades, relacionamentos e esquemas de contribuição de uma classe específica. Este guia fornece informações detalhadas sobre como visualizar e explorar schemas de união usando a interface do usuário da plataforma.

## Introdução

Este guia da interface do usuário requer uma compreensão das várias [!DNL Experience Platform] serviços envolvidos no gerenciamento de dados do Perfil do cliente em tempo real. Antes de ler este guia ou trabalhar na interface do usuário, revise a documentação dos seguintes serviços:

* [[!DNL Real-time Customer Profile]](../home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
* [[!DNL Identity Service]](../../identity-service/home.md): Habilitar [!DNL Real-time Customer Profile] por conectar identidades a partir de fontes de dados diferentes, à medida que são assimiladas [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): O quadro normalizado pelo qual [!DNL Platform] organiza os dados de experiência do cliente.

## Noções básicas sobre schemas de união

O Perfil do cliente em tempo real permite criar perfis robustos e centralizados contendo atributos do cliente e eventos com carimbos de data e hora para cada interação do cliente em sistemas integrados com o Adobe Experience Platform. O formato e a estrutura desses dados são fornecidos pelos esquemas do Experience Data Model (XDM), com cada schema sendo baseado em uma classe XDM e contendo campos compatíveis com essa classe.

Os esquemas podem ser criados para vários casos de uso, fazendo referência à mesma classe, mas contendo campos específicos para seu uso. Quando um schema é ativado para Perfil, ele se torna parte de um schema de união. Em outras palavras, os esquemas de união são compostos de vários esquemas que compartilham a mesma classe e foram habilitados para o Perfil. O esquema de união permite ver uma combinação de todos os campos contidos em esquemas que compartilham a mesma classe. O Perfil do cliente em tempo real usa o esquema de união para criar uma visualização holística de cada cliente individual.

Trabalhar com schemas de união requer uma compreensão profunda dos esquemas XDM. Para obter mais informações, comece lendo o [noções básicas da composição do schema](../../xdm/schema/composition.md).

## Exibir esquemas de união

Para navegar até esquemas de união na interface do usuário da plataforma, selecione **[!UICONTROL Perfis]** no menu de navegação esquerdo, selecione o **[!UICONTROL Esquema de união]** guia . O [!UICONTROL Esquema de união] é aberta para exibir o schema de união para a classe selecionada no momento.

![A página Esquema de união é exibida, com a guia Perfil e Esquema de união realçada.](../images/union-schema/landing.png)

## Selecionar uma classe

Para exibir o esquema de união para uma classe XDM específica, selecione a classe no **[!UICONTROL Classe]** lista suspensa. Devido ao fato de nem todas as classes terem esquemas de união, somente as classes com esquemas de união (ou seja, classes com esquemas que foram habilitados para Perfil) estão disponíveis na lista suspensa.

Depois que uma classe é selecionada, o schema exibido é atualizado para refletir o schema de união para a classe selecionada. Por exemplo, você pode selecionar **[!UICONTROL Perfil individual XDM]** para exibir o schema de união para essa classe.

![Uma lista suspensa contendo as classes do schema de união é realçada.](../images/union-schema/class.png)

## Explorar schemas de união

Você pode explorar o schema de união rolando para cima e para baixo para exibir a estrutura completa do schema e selecionando um colchete de ângulo direito (`>`) para expandir campos aninhados.

![Um conjunto de campos aninhados no schema de união é expandido.](../images/union-schema/explore.png)

Selecione qualquer campo para exibir seus detalhes, incluindo nome de exibição, tipo de dados, descrição, caminho, data criada e data da última modificação. Também é possível exibir uma lista de schemas de contribuição contendo o campo selecionado.

![Um campo de esquema de união é realçado. Os detalhes sobre o campo destacado são exibidos na barra lateral direita.](../images/union-schema/explore-field.png)

Selecionar o nome de um schema de contribuição revela os nomes dos conjuntos de dados relacionados a esse schema que estão assimilando dados no campo selecionado. Cada nome do conjunto de dados é exibido como um link. Selecionar um nome de conjunto de dados abre a guia atividade para esse conjunto de dados em uma nova janela.

Para obter mais informações sobre conjuntos de dados, incluindo a visualização da atividade do conjunto de dados e a visualização dos dados do conjunto de dados na interface do usuário, visite o [guia da interface do usuário de conjuntos de dados](../../catalog/datasets/user-guide.md).

![A lista de conjuntos de dados relacionados ao esquema é realçada.](../images/union-schema/datasets.png)

## Exibir esquemas de contribuição

Também é possível visualizar quais schemas específicos estão contribuindo para o schema da união selecionando **[!UICONTROL Todos os esquemas de contribuição]** para expandir a lista de schemas. Dependendo da classe selecionada e do número de schemas que sua organização criou no Platform, pode ser uma lista curta contendo um único schema ou uma lista longa contendo muitos schemas.

![A lista de schemas que contribuem para o schema de união é realçada.](../images/union-schema/contributing-schemas.png)

Selecionar o nome de um schema específico destaca os campos dentro do schema de união que fazem parte do schema selecionado. Depois que um schema é selecionado, o schema de união aparece esmaecido com barras pretas, indicando os campos que fazem parte do schema de contribuição.

![O schema de contribuição selecionado é realçado. Os campos que fazem parte do esquema de contribuição permanecem em preto, enquanto os campos que não fazem parte do esquema de contribuição ficam esmaecidos.](../images/union-schema/select-schema.png)

## Exibir identidades

Na interface do usuário, é possível visualizar uma lista de identidades incluídas no esquema da união selecionando **[!UICONTROL Identidades]** para expandir a lista.

![As identidades que pertencem ao schema da união são destacadas.](../images/union-schema/identities.png)

Selecionar uma identidade individual na lista faz com que o schema exibido seja atualizado automaticamente conforme necessário para exibir o campo de identidade. Isso pode incluir a expansão de vários campos se o campo de identidade estiver aninhado.

O campo de identidade é realçado no schema da união e os detalhes da identidade são exibidos no lado direito da tela. Os detalhes incluem uma lista de esquemas de contribuição que contêm o campo de identidade e você pode fazer drill-down para localizar links para os conjuntos de dados relacionados a esse esquema que estão assimilando dados no campo de identidade selecionado.

![A identidade selecionada é realçada. Os detalhes sobre a identidade selecionada são exibidos na barra lateral direita.](../images/union-schema/select-identity.png)

## Exibir relacionamentos

A interface do usuário do schema de união também permite que você veja os relacionamentos que foram definidos para esquemas com base na classe de schema selecionada. Definir um relacionamento é uma maneira de conectar dois schemas pertencentes a classes diferentes para obter insights mais complexos sobre os dados do cliente.

Se os relacionamentos tiverem sido estabelecidos para a classe selecionada, selecionando **[!UICONTROL Relações]** exibe uma lista de campos usados para criar relações. Nem todos os schemas usam ou precisam de relacionamentos definidos, portanto, é comum que a seção de relacionamentos não contenha nenhum campo.

Para saber mais sobre relações de esquema, incluindo como defini-los usando a interface do usuário, visite [este documento sobre relações de esquema](../../xdm/tutorials/relationship-ui.md).

![As relações que pertencem ao schema da união são destacadas.](../images/union-schema/relationships.png)

Selecionar um campo de relacionamento na lista faz com que o schema exibido seja atualizado conforme necessário para exibir o campo de relacionamento destacado. Isso pode incluir a expansão de vários campos se o campo de relacionamento estiver aninhado.

![A relação selecionada é realçada. O campo correspondente da relação também é realçado.](../images/union-schema/select-relationship.png)

## Próximas etapas

Ao ler este guia, agora você sabe como visualizar e navegar pelos esquemas de união usando o [!DNL Experience Platform] IU. Para obter mais informações sobre schemas, incluindo como eles são usados em toda a plataforma, comece lendo o [Visão geral do sistema XDM](../../xdm/home.md).
