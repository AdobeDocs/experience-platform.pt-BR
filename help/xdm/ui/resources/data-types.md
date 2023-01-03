---
keywords: Experience Platform, home, tópicos populares, ui, XDM, sistema XDM, modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados, Modelo de dados, Registro de esquema, Registro de esquema, esquema, esquemas, esquemas, esquemas, criar, tipo de dados, tipos de dados;
solution: Experience Platform
title: Criar e editar tipos de dados usando a interface do usuário
topic-legacy: tutorial
type: Tutorial
description: Saiba como criar e editar tipos de dados na interface do usuário do Experience Platform.
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 0%

---

# Criar e editar tipos de dados usando a interface do usuário

No Experience Data Model (XDM), os tipos de dados são campos reutilizáveis que contêm vários subcampos. Embora semelhantes aos grupos de campos de esquema, na medida em que permitem o uso consistente de uma estrutura de vários campos, os tipos de dados são mais flexíveis porque podem ser incluídos em qualquer lugar na estrutura do schema, enquanto os grupos de campos só podem ser adicionados no nível raiz.

O Adobe Experience Platform fornece muitos tipos de dados padrão que podem ser usados para abranger uma grande variedade de casos de uso comuns do gerenciamento de experiências. No entanto, você também pode definir seus próprios tipos de dados personalizados para atender às suas necessidades comerciais exclusivas.

Este tutorial aborda as etapas para criar e editar tipos de dados personalizados na interface do usuário da plataforma.

## Pré-requisitos

Este guia requer uma compreensão funcional do Sistema XDM. Consulte a [Visão geral do XDM](../../home.md) para uma introdução ao papel do XDM no ecossistema do Experience Platform, e [noções básicas da composição do schema](../../schema/composition.md) para saber como os tipos de dados contribuem para esquemas XDM.

Embora não seja necessário para este guia, é recomendável seguir também o tutorial em [composição de um esquema na interface do usuário](../../tutorials/create-schema-ui.md) para se familiarizar com os vários recursos do [!DNL Schema Editor].

## Abra o [!DNL Schema Editor] para um tipo de dados

Na interface do usuário da plataforma, selecione **[!UICONTROL Esquemas]** na navegação à esquerda para abrir o [!UICONTROL Esquemas] espaço de trabalho e selecione o **[!UICONTROL Tipos de dados]** guia . Uma lista de tipos de dados disponíveis é exibida, incluindo aqueles definidos pelo Adobe e aqueles criados por sua organização.

![](../../images/ui/resources/data-types/data-types-tab.png)

Aqui, você tem duas opções:

- [Criar um novo tipo de dados](#create)
- [Selecionar um tipo de dados existente para editar](#edit)

### Criar um novo tipo de dados {#create}

No **[!UICONTROL Tipos de dados]** guia , selecione **[!UICONTROL Criar tipo de dados]**.

![](../../images/ui/resources/data-types/create.png)

O [!DNL Schema Editor] for exibida, mostrando a estrutura atual do novo tipo de dados na tela. No lado direito do editor, é possível fornecer um nome de exibição e uma descrição opcional para o tipo de dados. Certifique-se de fornecer um nome exclusivo e conciso para o tipo de dados, pois é assim que ele será identificado ao adicioná-lo a um schema.

Este tutorial cria um tipo de dados que descreve uma propriedade de restaurante, de modo que o tipo de dados recebe um nome de exibição de &quot;Restaurante&quot;.

![](../../images/ui/resources/data-types/data-type-properties.png)

A partir daqui, você pode pular para o [próxima seção](#add-fields) para começar a adicionar campos ao novo tipo de dados.

### Editar um tipo de dados existente

>[!NOTE]
>
>Depois que um tipo de dados existente é usado em um schema que foi ativado para uso no Perfil do cliente em tempo real, somente alterações não destrutivas podem ser feitas nesse tipo de dados a partir de então. Consulte a [regras de evolução do schema](../../schema/composition.md#evolution) para obter mais informações.

Somente os tipos de dados personalizados definidos pela sua organização podem ser editados. Para restringir a lista exibida, selecione o ícone de filtro (![Ícone de filtro](../../images/ui/resources/data-types/filter.png)) para revelar controles para filtragem com base em [!UICONTROL Proprietário]. Selecionar **[!UICONTROL Cliente]** para mostrar apenas os tipos de dados personalizados de propriedade de sua organização.

Selecione o tipo de dados que deseja editar na lista para abrir o painel direito, mostrando os detalhes do tipo de dados. Selecione o nome do tipo de dados no painel direito para abrir sua estrutura no [!DNL Schema Editor].

![](../../images/ui/resources/data-types/edit.png)

## Adicionar campos ao tipo de dados {#add-fields}

Para começar a adicionar campos ao tipo de dados, selecione o **mais (+)** ícone ao lado do campo de nível raiz na tela de desenho. Um novo campo é exibido abaixo e o painel direito é atualizado para exibir controles para o novo campo.

![](../../images/ui/resources/data-types/new-field.png)

Use os controles no painel direito para configurar os detalhes do novo campo. Consulte o guia sobre [definição de campos na interface do usuário](../fields/overview.md#define) para obter etapas específicas sobre como configurar e adicionar o campo ao tipo de dados.

O tipo de dados Restaurant requer um campo de string para representar o nome do restaurante. Como tal, a variável [!UICONTROL Nome do campo] é definido como &quot;name&quot; e a variável [!UICONTROL Tipo] está definida como &quot;[!UICONTROL String]&quot;. Selecionar **[!UICONTROL Aplicar]** para aplicar as alterações no campo .

![](../../images/ui/resources/data-types/name-field.png)

Continue adicionando mais campos ao tipo de dados, conforme necessário. O exemplo de tipo de dados Restaurant agora tem campos adicionais para marca, capacidade de assentos e espaço do chão.

![](../../images/ui/resources/data-types/more-fields.png)

Além dos campos básicos, também é possível aninhar outros tipos de dados dentro do tipo de dados personalizado. Por exemplo, o tipo de dados Restaurante requer um campo que representa o endereço físico da propriedade. Nesse cenário, é possível adicionar um novo campo &quot;endereço&quot; ao qual é atribuído o tipo de dados padrão &quot;[!UICONTROL Endereço postal]&quot;.

![](../../images/ui/resources/data-types/address-field.png)

Isso demonstra como os tipos de dados podem ser flexíveis em termos de descrição dos dados: os tipos de dados podem empregar campos que também são tipos de dados, que podem conter outros tipos de dados, e assim por diante. Isso permite abstrair e reutilizar padrões de dados comuns em seus esquemas XDM, facilitando a representação de estruturas de dados complexas.

Depois de concluir a adição de campos ao tipo de dados, selecione **[!UICONTROL Salvar]** para salvar as alterações e adicionar o tipo de dados à [!DNL Schema Library].

## Adicionar o tipo de dados a uma classe ou grupo de campos

Depois de criar um tipo de dados, você pode começar a usá-lo em seus esquemas. Como os esquemas XDM são compostos de uma classe e zero ou mais grupos de campos, os campos fornecidos por um tipo de dados não podem ser adicionados a um schema diretamente. Em vez disso, eles devem ser incluídos em uma classe ou em um grupo de campos.

Comece seguindo as etapas envolvidas com [adição de um campo a uma classe](./classes.md#add-fields) ou [adição de um campo a um grupo de campos](./field-groups.md#add-fields). Ao escolher a variável **[!UICONTROL Tipo]** para o novo campo, selecione o nome do tipo de dados no menu suspenso.

## Converter um objeto de vários campos em um tipo de dados {#convert}

Ao criar um campo do tipo objeto com vários subcampos na variável [!DNL Schema Editor], é possível converter esse campo em um tipo de dados para usar a mesma estrutura de campo em uma classe ou grupo de campos diferente.

Para converter um campo do tipo objeto em um tipo de dados, selecione o campo na tela. Antes de converter o campo, verifique se **[!UICONTROL Nome de exibição]** é descritiva dos dados que o objeto conterá, pois se tornará o nome do tipo de dados. Quando estiver pronto para converter o campo, selecione **[!UICONTROL Converter em novo tipo de dados]** no painel direito.

![](../../images/ui/resources/data-types/convert-object.png)

A tela atualiza o tipo de dados do campo de &quot;[!UICONTROL Objeto]&quot; para o novo tipo de dados. Os subcampos também têm pequenos ícones de bloqueio ao lado, indicando que não são mais campos individuais, mas parte de um tipo de dados de vários campos. Essa estrutura agora pode ser reutilizada em outras classes e grupos de campos ao selecionar esse tipo de dados na variável **[!UICONTROL Tipo]** lista suspensa ao definir um novo campo.

![](../../images/ui/resources/data-types/converted.png)

## Próximas etapas

Este guia cobriu como criar e editar tipos de dados usando a interface do usuário da plataforma. Para obter mais informações sobre os recursos da [!UICONTROL Esquemas] espaço de trabalho, consulte o [[!UICONTROL Esquemas] visão geral do espaço de trabalho](../overview.md).

Para saber como gerenciar tipos de dados usando o [!DNL Schema Registry] API, consulte o [guia do endpoint de tipos de dados](../../api/data-types.md).
