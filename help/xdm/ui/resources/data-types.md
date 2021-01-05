---
keywords: Experience Platform;home;popular topics;ui;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;schema;Schema;schemas;Schemas;create;data type;data types;
solution: Experience Platform
title: Criar e editar tipos de dados usando a interface do usuário
topic: tutorial
type: Tutorial
description: Saiba como criar e editar tipos de dados na interface do usuário do Experience Platform.
translation-type: tm+mt
source-git-commit: eca896ca068a02da7ec7379e8ced2105bbca9f2d
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 0%

---


# Criar e editar tipos de dados usando a interface do usuário

No Experience Data Model (XDM), os tipos de dados são usados como campos do tipo de referência em classes ou combinações da mesma forma que os campos literais básicos, com a principal diferença de que os tipos de dados podem definir vários subcampos. Embora semelhantes às misturas, na medida em que permitem o uso consistente de uma estrutura de vários campos, os tipos de dados são mais flexíveis porque podem ser incluídos em qualquer lugar na estrutura do schema, enquanto as combinações só podem ser adicionadas no nível raiz.

A Adobe Experience Platform fornece vários tipos de dados padrão que podem ser usados para abranger uma grande variedade de casos de uso comuns do gerenciamento de experiências. No entanto, você também pode definir seus próprios tipos de dados personalizados para atender às suas necessidades comerciais exclusivas.

Este tutorial aborda as etapas para criar e editar tipos de dados personalizados na interface do usuário da plataforma.

## Pré-requisitos

Este guia requer um entendimento prático do sistema XDM. Consulte [Visão geral do XDM](../../home.md) para obter uma introdução à função do XDM dentro do ecossistema do Experience Platform, e as [noções básicas da composição do schema](../../schema/composition.md) para saber como os tipos de dados contribuem para os schemas XDM.

Embora não seja necessário para este guia, é recomendável que você também siga o tutorial sobre [compondo um schema na interface do usuário](../../tutorials/create-schema-ui.md) para se familiarizar com os vários recursos do [!DNL Schema Editor].

## Abra [!DNL Schema Editor] para um tipo de dados

Na interface do usuário da plataforma, selecione **[!UICONTROL Schemas]** no painel de navegação esquerdo para abrir o espaço de trabalho [!UICONTROL Schemas] e selecione a guia **[!UICONTROL Tipos de dados]**. Uma lista de tipos de dados disponíveis é exibida, incluindo aqueles definidos pelo Adobe, bem como aqueles criados pela sua organização.

![](../../images/ui/resources/data-types/data-types-tab.png)

Aqui, você tem duas opções:

- [Criar um novo tipo de dados](#create)
- [Selecione um tipo de dados existente para editar](#edit)

### Criar um novo tipo de dados {#create}

Na guia **[!UICONTROL Tipos de dados]**, selecione **[!UICONTROL Criar tipo de dados]**.

![](../../images/ui/resources/data-types/create.png)

O [!DNL Schema Editor] é exibido, mostrando a estrutura atual do novo tipo de dados na tela. No lado direito do editor, é possível fornecer um nome de exibição e uma descrição opcional para o tipo de dados. Certifique-se de fornecer um nome exclusivo e conciso para o seu tipo de dados, já que é assim que ele será identificado ao adicioná-lo a um schema.

Este tutorial cria um tipo de dados que descreve uma propriedade de restaurante, de modo que o tipo de dados recebe um nome de exibição de &quot;Restaurante&quot;.

![](../../images/ui/resources/data-types/data-type-properties.png)

Daqui, você pode pular para a próxima seção [próxima](#add-fields) para o start adicionando campos ao novo tipo de dados.

### Editar um tipo de dados existente

Somente os tipos de dados personalizados definidos pela sua organização podem ser editados. Para restringir a lista exibida, selecione o ícone de filtro (![Ícone de filtro](../../images/ui/resources/data-types/filter.png)) para revelar os controles de filtragem com base em [!UICONTROL Proprietário]. Selecione **[!UICONTROL Cliente]** para mostrar apenas os tipos de dados personalizados pertencentes à sua organização.

Selecione o tipo de dados que deseja editar na lista para abrir o painel direito, mostrando os detalhes do tipo de dados. Selecione o nome do tipo de dados no painel direito para abrir sua estrutura em [!DNL Schema Editor].

![](../../images/ui/resources/data-types/edit.png)

## Adicionar campos ao tipo de dados {#add-fields}

Para adicionar campos ao tipo de dados pelo start, selecione o ícone **mais (+)** ao lado do campo de nível raiz na tela. Um novo campo é exibido abaixo e o painel direito é atualizado para exibir controles para o novo campo.

![](../../images/ui/resources/data-types/new-field.png)

Use os controles no painel direito para configurar os detalhes do novo campo. Consulte o guia em [definindo campos na interface do usuário](../fields/overview.md#define) para obter etapas específicas sobre como configurar e adicionar o campo ao tipo de dados.

O tipo de dados Restaurant requer um campo de string para representar o nome do restaurante. Dessa forma, o [!UICONTROL Nome do campo] está definido como &quot;nome&quot; e [!UICONTROL Tipo] está definido como &quot;[!UICONTROL Cadeia]&quot;. Selecione **[!UICONTROL Aplicar]** para aplicar as alterações ao campo.

![](../../images/ui/resources/data-types/name-field.png)

Continue adicionando mais campos ao tipo de dados, conforme necessário. O exemplo de tipo de dados do Restaurante agora tem campos adicionais para marca, capacidade de assentos e espaço.

![](../../images/ui/resources/data-types/more-fields.png)

Além dos campos básicos, você também pode aninhar outros tipos de dados dentro do seu tipo de dados personalizado. Por exemplo, o tipo de dados Restaurante requer um campo que represente o endereço físico da propriedade. Nesse cenário, você pode adicionar um novo campo &quot;endereço&quot; ao qual é atribuído o tipo de dados padrão &quot;[!UICONTROL Endereço postal]&quot;.

![](../../images/ui/resources/data-types/address-field.png)

Isso demonstra como os tipos de dados podem ser flexíveis em termos de descrição dos dados: os tipos de dados podem empregar campos que também são tipos de dados, que podem conter outros tipos de dados, e assim por diante. Isso permite abstrair e reutilizar padrões de dados comuns em todos os schemas XDM, facilitando a representação de estruturas de dados complexas.

Depois que terminar de adicionar campos ao tipo de dados, selecione **[!UICONTROL Salvar]** para salvar suas alterações e adicionar o tipo de dados ao [!DNL Schema Library].

## Adicionar o tipo de dados a uma classe ou combinação

Depois de criar um tipo de dados, você pode start usando-o em seus schemas. Como os schemas XDM são compostos de uma classe e zero ou mais combinações, os campos fornecidos por um tipo de dados não podem ser adicionados diretamente a um schema. Em vez disso, eles devem ser incluídos em uma classe ou mistura.

Start seguindo as etapas envolvidas com [adicionar um campo a uma classe](./classes.md#add-fields) ou [adicionar um campo a uma mistura](./mixins.md#add-fields). Ao escolher **[!UICONTROL Type]** para o novo campo, selecione o nome do seu tipo de dados no menu suspenso.

## Converter um objeto de vários campos em um tipo de dados {#convert}

Ao criar um campo do tipo objeto com vários subcampos em [!DNL Schema Editor], você pode converter esse campo em um tipo de dados para que possa usar a mesma estrutura de campo em uma classe ou combinação diferente.

Para converter um campo de tipo de objeto em um tipo de dados, selecione o campo na tela. Antes de converter o campo, verifique se **[!UICONTROL Nome de exibição]** é descritivo dos dados que o objeto conterá, pois isso se tornará o nome do tipo de dados. Quando você estiver pronto para converter o campo, selecione **[!UICONTROL Converter em novo tipo de dados]** no painel direito.

![](../../images/ui/resources/data-types/convert-object.png)

A tela atualiza o tipo de dados do campo de &quot;[!UICONTROL Object]&quot; para o novo tipo de dados. Os subcampos também têm pequenos ícones de bloqueio ao lado deles, indicando que não são mais campos individuais, mas parte de um tipo de dados de vários campos. Agora, essa estrutura pode ser reutilizada em outras classes e misturas selecionando esse tipo de dados na lista suspensa **[!UICONTROL Tipo]** ao definir um novo campo.

![](../../images/ui/resources/data-types/converted.png)

## Próximas etapas

Este guia aborda como criar e editar tipos de dados usando a interface do usuário da plataforma. Para obter mais informações sobre os recursos do espaço de trabalho [!UICONTROL Schemas], consulte a [[!UICONTROL visão geral do espaço de trabalho dos Schemas]](../overview.md).

Para saber como gerenciar tipos de dados usando a API [!DNL Schema Registry], consulte o [guia de ponto de extremidade de tipos de dados](../../api/data-types.md).
