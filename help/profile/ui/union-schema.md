---
keywords: Experience Platform;perfil;perfil do cliente em tempo real;perfil unificado;Perfil unificado; unificado;Perfil;rtcp;ativar perfil;Ativar perfil;União; do cliente; unificado; unificado;;rtcp;ativar ;Ativar ;schema de UNIÃO PERFIL de ;união perfil de
title: Guia da interface do Schema da união
topic: guide
type: Documentation
description: Na interface do usuário do Adobe Experience Platform (UI), você pode visualização facilmente qualquer schema de união dentro da organização e pré-visualização os campos, identidades, relacionamentos e schemas de contribuição para uma classe específica. Este guia fornece informações detalhadas sobre como visualização e explorar schemas de união usando a interface do usuário da plataforma.
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 0%

---


# [!UICONTROL Guia ] da interface do usuário do esquema de união

Na interface do usuário do Adobe Experience Platform (UI), você pode visualização facilmente qualquer schema de união dentro da organização e pré-visualização os campos, identidades, relacionamentos e schemas de contribuição para uma classe específica. Este guia fornece informações detalhadas sobre como visualização e explorar schemas de união usando a interface do usuário da plataforma.

## Introdução

Este guia de interface do usuário requer uma compreensão dos vários [!DNL Experience Platform] serviços envolvidos no gerenciamento de dados de Perfil do cliente em tempo real. Antes de ler este guia ou trabalhar na interface do usuário, consulte a documentação dos seguintes serviços:

* [[!DNL Real-time Customer Profile]](../home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
* [[!DNL Identity Service]](../../identity-service/home.md): Habilita  [!DNL Real-time Customer Profile] ao fazer a ponte entre identidades de diferentes fontes de dados à medida que são assimiladas  [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Platform] organiza os dados de experiência do cliente.

## Noções básicas sobre schemas uniões

O Perfil do cliente em tempo real permite que você crie perfis robustos e centralizados que contêm atributos do cliente e eventos com carimbos de data e hora para cada interação do cliente em sistemas integrados à Adobe Experience Platform. O formato e a estrutura desses dados são fornecidos pelos schemas do Modelo de Dados de Experiência (XDM), com cada schema baseado em uma classe XDM e contendo campos compatíveis com essa classe.

Schemas podem ser criados para vários casos de uso, fazendo referência à mesma classe, mas contendo campos específicos para seu uso. Quando um schema é ativado para Perfil, ele se torna parte de um schema de união. Em outras palavras, schemas de união são compostos de vários schemas que compartilham a mesma classe e foram habilitados para Perfis. O schema de união permite que você veja uma combinação de todos os campos contidos em schemas que compartilham a mesma classe. O Perfil do cliente em tempo real usa o schema da união para criar uma visualização holística de cada cliente.

Trabalhar com schemas uniões requer uma compreensão profunda dos schemas XDM. Para obter mais informações, comece lendo as [noções básicas da composição do schema](../../xdm/schema/composition.md).

## Schemas da união visualização

Para navegar até schemas de união na interface do usuário da plataforma, selecione **[!UICONTROL Perfis]** no painel de navegação esquerdo e selecione a guia **[!UICONTROL Schema]**. A guia [!UICONTROL Schema de União] é aberta para exibir o schema de união da classe selecionada no momento.

![](../images/union-schema/union-schema-landing.png)

## Selecionar uma classe

Para exibir o schema de união de uma classe XDM específica, selecione a classe na lista suspensa **[!UICONTROL Class]**. Devido ao fato de nem todas as classes terem schemas uniões, somente as classes com schemas uniões (ou seja, classes com schemas que foram ativados para Perfis) estão disponíveis na lista suspensa.

Depois que uma classe é selecionada, o schema exibido é atualizado para refletir o schema de união da classe selecionada. Por exemplo, você pode selecionar **[!UICONTROL Perfil individual XDM]** para visualização do schema de união dessa classe.

![](../images/union-schema/union-schema-class.png)

## Explore schemas de união

Você pode explorar o schema da união rolando para cima e para baixo para visualização da estrutura completa do schema e selecionando um colchete de ângulo direito (`>`) para expandir os campos aninhados.

![](../images/union-schema/union-schema-explore.png)

Selecione qualquer campo para visualização de seus detalhes, incluindo nome de exibição, tipo de dados, descrição, caminho, data de criação e data da última modificação. Você também pode visualização uma lista de schemas contribuintes que contêm o campo selecionado.

![](../images/union-schema/union-schema-explore-field.png)

Selecionar o nome de um schema contribuinte revela os nomes dos conjuntos de dados relacionados a esse schema que estão assimilando dados no campo selecionado. Cada nome do conjunto de dados aparece como um link. Selecionar um nome de conjunto de dados abre a guia atividade para esse conjunto de dados em uma nova janela.

Para obter mais informações sobre conjuntos de dados, incluindo exibição da atividade do conjunto de dados e visualização dos dados do conjunto de dados na interface do usuário, visite o [guia da interface do usuário dos conjuntos de dados](../../catalog/datasets/user-guide.md).

![](../images/union-schema/union-schema-field-datasets.png)

## Schemas contribuintes de visualizações

Você também pode visualização quais schemas específicos estão contribuindo para o schema da união selecionando **[!UICONTROL Todos os schemas contribuintes]** para expandir a lista dos schemas. Dependendo da classe selecionada e do número de schemas criados pela sua organização na Plataforma, pode ser uma lista curta contendo um único schema ou uma lista longa contendo vários schemas.

![](../images/union-schema/union-schema-contributing-schemas.png)

Selecionar o nome de um schema específico destaca os campos dentro do schema da união que fazem parte do schema selecionado. Depois que um schema é selecionado, a schema da união é exibida esmaecida com barras pretas, indicando os campos que fazem parte do schema que contribui.

![](../images/union-schema/union-schema-select-schema.png)

## Identidades da visualização

Por meio da interface, é possível visualização de uma lista de identidades incluídas no schema de união selecionando **[!UICONTROL Identidades]** para expandir a lista.

![](../images/union-schema/union-schema-identities.png)

Selecionar uma identidade individual na lista faz com que o schema exibido seja atualizado automaticamente conforme necessário para exibir o campo de identidade. Isso pode incluir a expansão de vários campos se o campo de identidade estiver aninhado.

O campo de identidade é realçado no schema da união e os detalhes da identidade são exibidos no lado direito da tela. Os detalhes incluem uma lista de schemas contribuintes que contêm o campo de identidade e você pode fazer drill-down para localizar links para os conjuntos de dados relacionados a esse schema que estão assimilando dados no campo de identidade selecionado.

![](../images/union-schema/union-schema-select-identity.png)

## Relações de visualização

A interface do usuário do schema de união também permite que você veja relações que foram definidas para schemas com base na classe do schema selecionada. A definição de uma relação é uma forma de conectar dois schemas pertencentes a classes diferentes para obter insights mais complexos sobre os dados do cliente.

Se relações tiverem sido estabelecidas para a classe selecionada, selecionar **[!UICONTROL Relações]** exibirá uma lista de campos usados para criar relações. Nem todos os schemas usam ou precisam de relacionamentos definidos, portanto, é comum que a seção de relacionamentos não contenha campos.

Para saber mais sobre relações de schema, incluindo como defini-las usando a interface do usuário, visite [este documento sobre relações de schema](../../xdm/tutorials/relationship-ui.md).

![](../images/union-schema/union-schema-relationships.png)

Selecionar um campo de relação na lista faz com que o schema exibido seja atualizado conforme necessário para exibir o campo de relacionamento realçado. Isso pode incluir a expansão de vários campos se o campo de relacionamento estiver aninhado.

![](../images/union-schema/union-schema-select-relationship.png)

## Próximas etapas

Ao ler este guia, agora você sabe como visualização e navegar em schemas de união usando a interface do usuário [!DNL Experience Platform]. Para obter mais informações sobre os schemas, incluindo como eles são usados em toda a Plataforma, comece lendo a [visão geral do Sistema XDM](../../xdm/home.md).
