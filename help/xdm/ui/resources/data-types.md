---
keywords: Experience Platform;início;tópicos populares;ui;XDM;sistema XDM;modelo de dados de experiência;modelo de dados de experiência;modelo de dados de experiência;modelo de dados;modelo de dados;modelo de dados;registro de esquemas;esquema;Esquema;esquemas;criar;tipo de dados;tipos de dados;
solution: Experience Platform
title: Criar e editar tipos de dados usando a interface
type: Tutorial
description: Saiba como criar e editar tipos de dados na interface do usuário do Experience Platform.
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '1156'
ht-degree: 0%

---

# Criar e editar tipos de dados usando a interface

No Experience Data Model (XDM), os tipos de dados são campos reutilizáveis que contêm vários subcampos. Embora semelhantes aos grupos de campos de esquema, no sentido de que permitem o uso consistente de uma estrutura de vários campos, os tipos de dados são mais flexíveis, pois podem ser incluídos em qualquer lugar na estrutura do esquema, enquanto os grupos de campos só podem ser adicionados no nível raiz.

O Adobe Experience Platform fornece vários tipos de dados padrão que podem ser usados para abranger uma grande variedade de casos de uso comuns do gerenciamento de experiência. No entanto, você também pode definir seus próprios tipos de dados personalizados para atender às suas necessidades comerciais exclusivas.

Este tutorial aborda as etapas para a criação e edição de tipos de dados personalizados na interface do usuário da Platform.

## Pré-requisitos

Este guia requer uma compreensão funcional do Sistema XDM. Consulte a [Visão geral do XDM](../../home.md) para obter uma introdução ao papel do XDM no ecossistema de Experience Platform, e a [noções básicas da composição do esquema](../../schema/composition.md) para saber como os tipos de dados contribuem para esquemas XDM.

Embora não seja necessário para este guia, é recomendável seguir o tutorial em [composição de um esquema na interface](../../tutorials/create-schema-ui.md) para se familiarizar com os vários recursos do [!DNL Schema Editor].

## Abra o [!DNL Schema Editor] para um tipo de dados

Na interface do usuário da Platform, selecione **[!UICONTROL Esquemas]** na navegação à esquerda, para abrir a [!UICONTROL Esquemas] e selecione o **[!UICONTROL Tipos de dados]** guia. Uma lista de tipos de dados disponíveis é exibida, incluindo aqueles definidos pelo Adobe e aqueles criados por sua organização.

![](../../images/ui/resources/data-types/data-types-tab.png)

Aqui, você tem duas opções:

- [Criar um novo tipo de dados](#create)
- [Selecionar um tipo de dados existente para editar](#edit)

### Criar um novo tipo de dados {#create}

No **[!UICONTROL Tipos de dados]** selecione **[!UICONTROL Criar tipo de dados]**.

![](../../images/ui/resources/data-types/create.png)

A variável [!DNL Schema Editor] é exibida, mostrando a estrutura atual do novo tipo de dados na tela. No lado direito do editor, é possível fornecer um nome de exibição e uma descrição opcional para o tipo de dados. Certifique-se de fornecer um nome exclusivo e conciso para o tipo de dados, pois é assim que ele será identificado ao adicioná-lo a um esquema.

Este tutorial cria um tipo de dados que descreve uma propriedade de restaurante, portanto, o tipo de dados recebe o nome de exibição &quot;Restaurante&quot;.

![](../../images/ui/resources/data-types/data-type-properties.png)

A partir daqui, você pode pular para a [próxima seção](#add-fields) para começar a adicionar campos ao novo tipo de dados.

### Editar um tipo de dados existente

>[!NOTE]
>
>Depois que um tipo de dados existente for usado em um esquema que foi ativado para uso no Perfil do cliente em tempo real, somente alterações não destrutivas poderão ser feitas nesse tipo de dados. Consulte a [regras de evolução do schema](../../schema/composition.md#evolution) para obter mais informações.

Somente tipos de dados personalizados definidos por sua organização podem ser editados. Para restringir a lista exibida, selecione o ícone de filtro (![Ícone de filtro](../../images/ui/resources/data-types/filter.png)) para revelar controles para filtragem com base em [!UICONTROL Proprietário]. Selecionar **[!UICONTROL Cliente]** para mostrar somente os tipos de dados personalizados de propriedade de sua organização.

Selecione o tipo de dados que deseja editar na lista para abrir o painel direito, mostrando os detalhes do tipo de dados. Selecione o nome do tipo de dados no painel direito para abrir sua estrutura no [!DNL Schema Editor].

![](../../images/ui/resources/data-types/edit.png)

## Adicionar campos ao tipo de dados {#add-fields}

Para começar a adicionar campos ao tipo de dados, selecione o **mais (+)** ícone ao lado do campo de nível raiz na tela. Um novo campo é exibido abaixo, e o painel direito é atualizado para exibir controles do novo campo.

![](../../images/ui/resources/data-types/new-field.png)

Use os controles no painel direito para configurar os detalhes do novo campo. Consulte o guia sobre [definição de campos na interface](../fields/overview.md#define) para obter etapas específicas sobre como configurar e adicionar o campo ao tipo de dados.

O tipo de dados Restaurant requer um campo de sequência para representar o nome do restaurante. Como tal, a Comissão [!UICONTROL Nome do campo] é definido como &quot;name&quot; e a variável [!UICONTROL Tipo] está definido como &quot;[!UICONTROL String]&quot;. Selecionar **[!UICONTROL Aplicar]** para aplicar as alterações ao campo.

![](../../images/ui/resources/data-types/name-field.png)

Continue adicionando mais campos ao tipo de dados, conforme necessário. O tipo de dados Exemplo de restaurante agora tem campos adicionais para marca, capacidade de assento e espaço.

![](../../images/ui/resources/data-types/more-fields.png)

Além dos campos básicos, você também pode aninhar tipos de dados adicionais com seu tipo de dados personalizado. Por exemplo, o tipo de dados Restaurant requer um campo que representa o endereço físico da propriedade. Nesse cenário, é possível adicionar um novo campo &quot;address&quot;, que recebe o tipo de dados padrão &quot;[!UICONTROL Endereço postal]&quot;.

![](../../images/ui/resources/data-types/address-field.png)

Isso demonstra como tipos de dados podem ser flexíveis em termos de descrição de seus dados: os tipos de dados podem empregar campos que também são tipos de dados, que podem conter outros tipos de dados e assim por diante. Isso permite abstrair e reutilizar padrões de dados comuns em todos os esquemas XDM, facilitando a representação de estruturas de dados complexas.

Quando terminar de adicionar campos ao tipo de dados, selecione **[!UICONTROL Salvar]** para salvar suas alterações e adicionar o tipo de dados à [!DNL Schema Library].

## Adicionar o tipo de dados a um esquema

Depois de criar um tipo de dados, você pode começar a usá-lo em seus schemas. Como os esquemas XDM são compostos de uma classe e zero ou mais grupos de campos, os campos fornecidos por um tipo de dados não podem ser adicionados diretamente a um esquema. Em vez disso, eles devem ser incluídos em uma classe ou em um grupo de campos.

Comece seguindo as etapas envolvidas com [adicionar um campo a uma classe](./classes.md#add-fields) ou [adicionar um campo a um grupo de campos](./field-groups.md#add-fields). Como alternativa, você pode iniciar [adição de um campo diretamente a um esquema](./schemas.md#add-individual-fields) e escolha a classe pai ou o grupo de campos a partir daí. Ao escolher a variável **[!UICONTROL Tipo]** para o novo campo, selecione o nome do seu tipo de dados no menu suspenso.

## Converter um objeto de vários campos em um tipo de dados {#convert}

Ao criar um campo do tipo objeto com vários subcampos no [!DNL Schema Editor], é possível converter esse campo em um tipo de dados para que você possa usar a mesma estrutura de campo em uma classe ou grupo de campos diferente.

Para converter um campo do tipo objeto em um tipo de dados, selecione o campo na tela. Antes de converter o campo, verifique se **[!UICONTROL Nome de exibição]** é descritiva dos dados que o objeto conterá, pois esse se tornará o nome do tipo de dados. Quando estiver pronto para converter o campo, selecione **[!UICONTROL Converter em novo tipo de dados]** no painel direito.

![](../../images/ui/resources/data-types/convert-object.png)

A tela atualiza o tipo de dados do campo de &quot;[!UICONTROL Objeto]&quot; para o novo tipo de dados. Essa estrutura agora pode ser reutilizada em outras classes e grupos de campos selecionando esse tipo de dados na **[!UICONTROL Tipo]** ao definir um novo campo.

![](../../images/ui/resources/data-types/converted.png)

## Próximas etapas

Este guia abordou como criar e editar tipos de dados usando a interface do usuário da plataforma. Para obter mais informações sobre os recursos do [!UICONTROL Esquemas] espaço de trabalho, consulte a [[!UICONTROL Esquemas] visão geral do espaço de trabalho](../overview.md).

Para saber como gerenciar tipos de dados usando o [!DNL Schema Registry] , consulte a [guia de endpoint de tipos de dados](../../api/data-types.md).
