---
keywords: Experience Platform;início;tópicos populares;ui;XDM;sistema XDM;modelo de dados de experiência;modelo de dados de experiência;modelo de dados de experiência;modelo de dados;modelo de dados;modelo de dados;registro de esquemas;esquema;Esquema;esquemas;criar;tipo de dados;tipos de dados;
solution: Experience Platform
title: Criar e editar tipos de dados usando a interface
type: Tutorial
description: Saiba como criar e editar tipos de dados na interface do usuário do Experience Platform.
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
source-git-commit: c04e5a49f2a4e90345ca20ecd0547d02b5004fcf
workflow-type: tm+mt
source-wordcount: '1384'
ht-degree: 6%

---

# Criar e editar tipos de dados usando a interface {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_datatype_filter"
>title="Filtro de tipo de dados padrão ou personalizado"
>abstract="A lista de tipos de dados disponíveis é pré-filtrada com base em como foram criados. Selecione o botão de opção para escolher entre as opções Padrão e Personalizado. A opção Padrão mostra entidades criadas pela Adobe e a opção Personalizado exibe entidades criadas na sua organização. Consulte a documentação para saber mais sobre criação e edição de tipos de dados."

No Experience Data Model (XDM), os tipos de dados são campos reutilizáveis que contêm vários subcampos. Embora semelhantes aos grupos de campos de esquema, no sentido de que permitem o uso consistente de uma estrutura de vários campos, os tipos de dados são mais flexíveis, pois podem ser incluídos em qualquer lugar na estrutura do esquema, enquanto os grupos de campos só podem ser adicionados no nível raiz.

O Adobe Experience Platform fornece vários tipos de dados padrão que podem ser usados para abranger uma grande variedade de casos de uso comuns do gerenciamento de experiência. No entanto, você também pode definir seus próprios tipos de dados personalizados para atender às suas necessidades comerciais exclusivas.

>[!NOTE]
>
>Se um campo for definido como um tipo de dados específico, você não poderá criar o mesmo campo com um tipo de dados diferente em outro esquema. Essa restrição se aplica ao locatário da organização.

Este tutorial aborda as etapas para a criação e edição de tipos de dados personalizados na interface do usuário da Platform.

## Pré-requisitos {#prerequisites}

Este guia requer uma compreensão funcional do Sistema XDM. Consulte a [Visão geral do XDM](../../home.md) para obter uma introdução ao papel do XDM no ecossistema de Experience Platform, e a [noções básicas da composição do esquema](../../schema/composition.md) para saber como os tipos de dados contribuem para esquemas XDM.

Embora não seja necessário para este guia, é recomendável seguir o tutorial em [composição de um esquema na interface](../../tutorials/create-schema-ui.md) para se familiarizar com os vários recursos do [!DNL Schema Editor].

## Abra o [!DNL Schema Editor] para um tipo de dados {#data-type}

Na interface do usuário da Platform, selecione **[!UICONTROL Esquemas]** na navegação à esquerda, para abrir a [!UICONTROL Esquemas] e selecione o **[!UICONTROL Tipos de dados]** guia. Uma lista de tipos de dados disponíveis é exibida. A lista de tipos de dados é automaticamente filtrada com base em como foram criados. A configuração padrão exibe os tipos de dados definidos pelo Adobe. Também é possível filtrar a lista para mostrar os criados por sua organização.

![A variável [!UICONTROL Esquemas] espaço de trabalho com [!UICONTROL Esquemas] no painel de navegação esquerdo e [!UICONTROL Tipos de dados] destacado.](../../images/ui/resources/data-types/data-types-tab.png)

Aqui, você tem as seguintes opções:

- [Criar um novo tipo de dados](#create)
- [Filtrar tipos de dados](#filter)
- [Selecionar um tipo de dados existente para editar](#edit)

### Criar um novo tipo de dados {#create}

No **[!UICONTROL Tipos de dados]** selecione **[!UICONTROL Criar tipo de dados]**.

![A variável [!UICONTROL Esquemas] espaço de trabalho [!UICONTROL Tipos de dados] guia com [!UICONTROL Criar tipo de dados] destacado.](../../images/ui/resources/data-types/create.png)

A variável [!DNL Schema Editor] é exibida, mostrando a estrutura atual do novo tipo de dados na tela. No lado direito do editor, é possível fornecer um nome de exibição e uma descrição opcional para o tipo de dados. Certifique-se de fornecer um nome exclusivo e conciso para o tipo de dados, pois é assim que ele será identificado ao adicioná-lo a um esquema.

Este tutorial cria um tipo de dados que descreve uma propriedade de restaurante, portanto, o tipo de dados recebe o nome de exibição &quot;Restaurante&quot;.

![](../../images/ui/resources/data-types/data-type-properties.png)

A partir daqui, você pode pular para a [próxima seção](#add-fields) para começar a adicionar campos ao novo tipo de dados.

### Filtrar tipos de dados {#filter}

A lista de tipos de dados disponíveis é pré-filtrada com base em como foram criados. Selecione o botão de opção para escolher entre as opções [!UICONTROL Padrão] e [!UICONTROL Personalizado] opções. A variável [!UICONTROL Padrão] mostra entidades criadas por Adobe e a variável [!UICONTROL Personalizado] exibe entidades criadas na organização.

![A variável [!UICONTROL Tipos de dados] guia do [!UICONTROL Esquemas] espaço de trabalho com [!UICONTROL Padrão] e [!UICONTROL Personalizado] destacado.](../../images/ui/resources/data-types/standard-and-custom-data-types.png)

### Editar um tipo de dados existente {#edit}

>[!NOTE]
>
>Depois que um tipo de dados existente for usado em um esquema que foi ativado para uso no Perfil do cliente em tempo real, somente alterações não destrutivas poderão ser feitas nesse tipo de dados. Consulte a [regras de evolução do schema](../../schema/composition.md#evolution) para obter mais informações.

Somente tipos de dados personalizados definidos por sua organização podem ser editados. Selecionar **[!UICONTROL Personalizado]** para mostrar somente os tipos de dados personalizados de propriedade de sua organização.

Selecione o tipo de dados que deseja editar na lista para abrir o painel direito, mostrando os detalhes do tipo de dados. No painel de detalhes, também é possível baixar um arquivo de amostra, copiar a estrutura JSON ou adicionar o tipo de dados a um pacote.

Selecione o nome do tipo de dados no painel direito para abrir sua estrutura no [!DNL Schema Editor].

![A variável [!UICONTROL Tipos de dados] guia do [!UICONTROL Esquemas] espaço de trabalho, com um tipo de dados, [!UICONTROL Personalizado] e o tipo de dados [!UICONTROL Nome] destacado.](../../images/ui/resources/data-types/edit.png)

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

## Adicionar o tipo de dados a um esquema {#add-data-type}

Depois de criar um tipo de dados, você pode começar a usá-lo em seus schemas. Como os esquemas XDM são compostos de uma classe e zero ou mais grupos de campos, os campos fornecidos por um tipo de dados não podem ser adicionados diretamente a um esquema. Em vez disso, eles devem ser incluídos em uma classe ou em um grupo de campos.

Comece seguindo as etapas envolvidas com [adicionar um campo a uma classe](./classes.md#add-fields) ou [adicionar um campo a um grupo de campos](./field-groups.md#add-fields). Como alternativa, você pode iniciar [adição de um campo diretamente a um esquema](./schemas.md#add-individual-fields) e escolha a classe pai ou o grupo de campos a partir daí. Ao escolher a variável **[!UICONTROL Tipo]** para o novo campo, selecione o nome do seu tipo de dados no menu suspenso.

## Converter um objeto de vários campos em um tipo de dados {#convert}

Ao criar um campo do tipo objeto com vários subcampos no [!DNL Schema Editor], é possível converter esse campo em um tipo de dados para usar a mesma estrutura de campo em uma classe ou grupo de campos diferente.

Para converter um campo do tipo objeto em um tipo de dados, selecione o campo na tela. Antes de converter o campo, verifique se **[!UICONTROL Nome de exibição]** é descritiva dos dados que o objeto conterá, pois esse se tornará o nome do tipo de dados. Quando estiver pronto para converter o campo, selecione **[!UICONTROL Converter em novo tipo de dados]** no painel direito.

![](../../images/ui/resources/data-types/convert-object.png)

A tela atualiza o tipo de dados do campo de &quot;[!UICONTROL Objeto]&quot; para o novo tipo de dados. Essa estrutura agora pode ser reutilizada em outras classes e grupos de campos selecionando esse tipo de dados na **[!UICONTROL Tipo]** ao definir um novo campo.

![](../../images/ui/resources/data-types/converted.png)

## Próximas etapas {#next-steps}

Este guia abordou como criar e editar tipos de dados usando a interface do usuário da plataforma. Para obter mais informações sobre os recursos do [!UICONTROL Esquemas] espaço de trabalho, consulte a [[!UICONTROL Esquemas] visão geral do espaço de trabalho](../overview.md).

Para saber como gerenciar tipos de dados usando o [!DNL Schema Registry] , consulte a [guia de endpoint de tipos de dados](../../api/data-types.md).
