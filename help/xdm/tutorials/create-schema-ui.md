---
keywords: Experience Platform, home, tópicos populares, interface do usuário, XDM, sistema XDM, modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados, Modelo de dados, Editor de esquema, Editor de esquema, esquema, Esquema, esquemas, esquemas, criar
solution: Experience Platform
title: Criar um esquema usando o editor de esquema
topic-legacy: tutorial
type: Tutorial
description: Este tutorial aborda as etapas para a criação de um esquema usando o Editor de esquemas na Experience Platform.
exl-id: 3edeb879-3ce4-4adb-a0bd-8d7ad2ec6102
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '3754'
ht-degree: 0%

---

# Crie um schema usando o [!DNL Schema Editor]

A interface do usuário do Adobe Experience Platform permite criar e gerenciar [!DNL Experience Data Model] Esquemas (XDM) em uma tela visual interativa chamada de [!DNL Schema Editor]. Este tutorial aborda como criar um schema usando o [!DNL Schema Editor].

>[!NOTE]
>
>Para fins de demonstração, as etapas neste tutorial envolvem a criação de um schema de exemplo que descreve membros de um programa de fidelidade do cliente. Embora você possa usar essas etapas para criar um schema diferente para seus próprios propósitos, é recomendável primeiro acompanhar a criação do schema de exemplo para saber mais sobre os recursos da variável [!DNL Schema Editor].

Se preferir compor um schema usando o [!DNL Schema Registry] Em vez disso, comece lendo a API [[!DNL Schema Registry] guia do desenvolvedor](../api/getting-started.md) antes de tentar o tutorial em [criação de um schema usando a API](create-schema-api.md).

## Introdução

Este tutorial requer uma compreensão funcional dos vários aspectos do Adobe Experience Platform envolvidos na criação do schema. Antes de iniciar este tutorial, reveja a documentação dos seguintes conceitos:

* [[!DNL Experience Data Model (XDM)]](../home.md): O quadro normalizado pelo qual [!DNL Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../schema/composition.md): Uma visão geral dos esquemas XDM e seus blocos de construção, incluindo classes, grupos de campos de esquema, tipos de dados e campos individuais.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

## Abra o [!UICONTROL Esquemas] espaço de trabalho {#browse}

O [!UICONTROL Esquemas] na área de trabalho do [!DNL Platform] A interface do usuário do fornece uma visualização do [!DNL Schema Library], permitindo que você visualize o gerenciamento dos esquemas disponíveis para sua organização. A área de trabalho também inclui a variável [!DNL Schema Editor], a tela na qual você pode compor um esquema em todo este tutorial.

Depois de fazer logon em [!DNL Experience Platform], selecione **[!UICONTROL Esquemas]** na navegação à esquerda para abrir o **[!UICONTROL Esquemas]** espaço de trabalho. O **[!UICONTROL Procurar]** exibe uma lista de schemas (uma representação da variável [!DNL Schema Library]) que você pode visualizar e personalizar. A lista inclui o nome, o tipo, a classe e o comportamento (registro ou série de tempo) em que o schema se baseia, bem como a data e a hora em que o schema foi modificado pela última vez.

Consulte o guia sobre [exploração de recursos XDM existentes na interface do usuário](../ui/explore.md) para obter mais informações.

## Criar e nomear um esquema {#create}

Para começar a compor um schema, selecione **[!UICONTROL Criar esquema]** no canto superior direito do **[!UICONTROL Esquemas]** espaço de trabalho. Um menu suspenso é exibido, dando a você a opção de escolher entre as classes principais [!UICONTROL Perfil individual XDM] e [!UICONTROL ExperiênciaEvento XDM]. Se essas classes não atenderem aos seus propósitos, você também poderá selecionar **[!UICONTROL Procurar]** escolher entre outras classes disponíveis ou [criar uma nova classe](#create-new-class).

Para fins deste tutorial, selecione **[!UICONTROL Perfil individual XDM]**.

![](../images/tutorials/create-schema/create_schema_button.png)

Como você escolheu uma classe XDM padrão para basear o esquema, a variável **[!UICONTROL Adicionar grupo de campos]** for exibida, permitindo que você comece imediatamente a adicionar campos ao esquema. Por enquanto, selecione **[!UICONTROL Cancelar]** para sair da caixa de diálogo.

![](../images/tutorials/create-schema/cancel-field-group.png)

O [!DNL Schema Editor] é exibido. Essa é a tela sobre a qual você irá compor o esquema. Um schema sem título é criado automaticamente no **[!UICONTROL Estrutura]** da tela ao chegar ao editor, juntamente com os campos padrão incluídos em todos os schemas com base nessa classe. A classe atribuída para o schema também é listada em **[!UICONTROL Classe]** em **[!UICONTROL Composição]** seção.

![](../images/tutorials/create-schema/schema_editor.png)

>[!NOTE]
>
>Você pode [alterar a classe de um schema](#change-class) em qualquer ponto durante o processo de composição inicial antes que o schema seja salvo, mas isso deve ser feito com extremo cuidado. Os grupos de campos são compatíveis apenas com determinadas classes e, portanto, alterar a classe redefinirá a tela e quaisquer campos adicionados.

Use os campos no lado direito do editor para fornecer um nome de exibição e uma descrição opcional para o esquema. Depois que um nome é inserido, a tela é atualizada para refletir o novo nome do schema.

![](../images/tutorials/create-schema/name_schema.png)

Há várias considerações importantes a serem feitas ao decidir um nome para o esquema:

* Os nomes de esquema devem ser curtos e descritivos para que o esquema possa ser facilmente encontrado posteriormente.
* Os nomes de esquema devem ser exclusivos, o que significa que também devem ser específicos o suficiente para que não sejam reutilizados no futuro. Por exemplo, se sua organização tivesse programas de fidelidade separados para diferentes marcas, seria recomendável nomear seu esquema como &quot;Membros da Fidelidade da Marca A&quot; para facilitar a distinção entre outros esquemas relacionados à fidelidade que você poderá definir posteriormente.
* Você também pode usar a descrição do schema para fornecer quaisquer informações contextuais adicionais relacionadas ao schema.

Este tutorial compõe um schema para assimilar dados relacionados aos membros de um programa de fidelidade e, portanto, o schema é chamado de &quot;Membros de fidelidade&quot;.

## Adicionar um grupo de campos {#field-group}

Agora é possível começar a adicionar campos ao esquema adicionando grupos de campos. Um grupo de campos é um grupo de um ou mais campos que são frequentemente usados em conjunto para descrever um conceito específico. Este tutorial usa grupos de campos para descrever os membros do programa de fidelidade e capturar informações-chave como nome, aniversário, número de telefone, endereço e muito mais.

Para adicionar um grupo de campos, selecione **[!UICONTROL Adicionar]** no **[!UICONTROL Grupos de campos]** subseção.

![](../images/tutorials/create-schema/add-field-group-button.png)

Uma nova caixa de diálogo é exibida, exibindo uma lista de grupos de campos disponíveis. Cada grupo de campos deve ser usado somente com uma classe específica, portanto, a caixa de diálogo lista somente grupos de campos compatíveis com a classe selecionada (nesse caso, a variável [!DNL XDM Individual Profile] classe ). Se você estiver usando uma classe XDM padrão, a lista de grupos de campo será classificada de forma inteligente com base na popularidade do uso.

![](../images/tutorials/create-schema/field-group-popularity.png)

Selecionar um grupo de campos na lista faz com que ele apareça no painel direito. É possível selecionar vários grupos de campos, se desejar, adicionando cada um à lista no painel direito antes de confirmar. Além disso, um ícone é exibido no lado direito do grupo de campos atualmente selecionado, permitindo que você visualize a estrutura dos campos fornecidos.

![](../images/tutorials/create-schema/preview-field-group-button.png)

Ao visualizar um grupo de campos, uma descrição detalhada do esquema do grupo de campos é fornecida no painel direito. Também é possível navegar pelos campos do grupo de campos na tela fornecida. À medida que você seleciona campos diferentes, o painel direito é atualizado para mostrar detalhes sobre o campo em questão. Selecionar **[!UICONTROL Voltar]** quando você terminar de visualizar para retornar à caixa de diálogo de seleção do grupo de campos.

![](../images/tutorials/create-schema/preview-field-group.png)

Para este tutorial, selecione o **[!UICONTROL Detalhes demográficos]** grupo de campos e selecione **[!UICONTROL Adicionar grupo de campos]**.

![](../images/tutorials/create-schema/demographic-details.png)

A tela do esquema é exibida novamente. O **[!UICONTROL Grupos de campos]** seção agora lista &quot;[!UICONTROL Detalhes demográficos]&quot; e o **[!UICONTROL Estrutura]** inclui os campos contribuídos pelo grupo de campos. Você pode selecionar o nome do grupo de campos sob a variável **[!UICONTROL Grupos de campos]** para realçar os campos específicos fornecidos na tela.

![](../images/tutorials/create-schema/demographic-details-structure.png)

Esse grupo de campos contribui com vários campos sob o nome de nível superior `person` com o tipo de dados &quot;[!UICONTROL Pessoa]&quot;. Este grupo de campos descreve informações sobre um indivíduo, incluindo nome, data de nascimento e gênero.

>[!NOTE]
>
>Lembre-se de que os campos podem usar tipos escalares (como string, integer, array ou data), bem como qualquer tipo de dados (um grupo de campos que representa um conceito comum) definido na variável [!DNL Schema Registry].

Observe que a variável `name` tem um tipo de dados de &quot;[!UICONTROL Nome da pessoa]&quot;, o que significa que também descreve um conceito comum e contém subcampos relacionados ao nome, como nome, sobrenome, título de cortesia e sufixo.

Selecione os diferentes campos na tela para revelar quaisquer campos adicionais que contribuem para a estrutura do schema.

## Adicionar outro grupo de campos {#field-group-2}

Agora é possível repetir as mesmas etapas para adicionar outro grupo de campos. Ao exibir a variável **[!UICONTROL Adicionar grupo de campos]** dessa vez, observe que &quot;[!UICONTROL Detalhes demográficos]&quot; o grupo de campos foi esmaecido e a caixa de seleção ao lado dele não pode ser selecionada. Isso evita a duplicação acidental de grupos de campos que já foram incluídos no esquema atual.

Neste tutorial, selecione o &quot;[!DNL Personal Contact Details]&quot; grupo de campos na caixa de diálogo e selecione **[!UICONTROL Adicionar grupo de campos]** para adicioná-lo ao schema.

![](../images/tutorials/create-schema/personal-contact-details.png)

Depois de adicionada, a tela reaparece. &quot;[!UICONTROL Detalhes de contato pessoal]&quot; agora está listado em **[!UICONTROL Grupos de campos]** no **[!UICONTROL Composição]** seção e campos para endereço residencial, telefone celular e muito mais foram adicionados em **[!UICONTROL Estrutura]**.

Semelhante ao `name` , os campos que você acabou de adicionar representam os conceitos de vários campos. Por exemplo, `homeAddress` tem um tipo de dados de &quot;[!UICONTROL Endereço postal]&quot; e `mobilePhone` tem um tipo de dados de &quot;[!UICONTROL Número de telefone]&quot;. Você pode selecionar cada um desses campos para expandi-los e ver os campos adicionais incluídos no tipo de dados.

![](../images/tutorials/create-schema/personal-contact-details-structure.png)

## Definir um grupo de campos personalizado {#define-field-group}

O &quot;[!UICONTROL Membros de Fidelidade]&quot; O schema destina-se a capturar dados relacionados aos membros de um programa de fidelidade, de modo que exigirá alguns campos específicos relacionados a fidelidade.

Existe um padrão [!UICONTROL Detalhes da Fidelidade] grupo de campos que pode ser adicionado ao schema para capturar campos comuns relacionados a um programa de fidelidade. Embora seja altamente recomendável usar grupos de campos padrão para representar conceitos capturados por seus esquemas, a estrutura do grupo de campos de fidelidade padrão pode não ser capaz de capturar todos os dados relevantes para seu programa de fidelidade específico. Nesse cenário, você pode optar por definir um novo grupo de campos personalizados para capturar esses campos.

Abra o **[!UICONTROL Adicionar grupo Campo]** novamente, mas desta vez selecione **[!UICONTROL Criar novo grupo de campos]** perto do topo. Em seguida, é necessário fornecer um nome de exibição e uma descrição para o grupo de campos.

![](../images/tutorials/create-schema/create-new-field-group.png)

Assim como com os nomes de classe, o nome do grupo de campos deve ser curto e simples, descrevendo o que o grupo de campos contribuirá para o schema. Eles também são exclusivos, portanto, você não poderá reutilizar o nome e deve garantir que seja específico o suficiente.

Para este tutorial, nomeie o novo grupo de campos &quot;Detalhes de fidelidade&quot;.

Selecionar **[!UICONTROL Adicionar grupo de campos]** para retornar ao [!DNL Schema Editor]. &quot;[!UICONTROL Detalhes da Fidelidade]&quot; agora deve aparecer em **[!UICONTROL Grupos de campos]** no lado esquerdo da tela, mas ainda não há campos associados a ela e, portanto, nenhum novo campo é exibido em **[!UICONTROL Estrutura]**.

## Adicionar campos ao grupo de campos {#field-group-fields}

Depois de criar o grupo de campos &quot;Detalhes de fidelidade&quot;, é hora de definir os campos que o grupo de campos contribuirá para o esquema.

Para começar, selecione o nome do grupo de campos na **[!UICONTROL Grupos de campos]** seção. Depois disso, as propriedades do grupo de campos serão exibidas no lado direito do editor e uma **mais (+)** ícone aparece ao lado do nome do schema em **[!UICONTROL Estrutura]**.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

Selecione o **mais (+)** ícone ao lado de &quot;[!DNL Loyalty Members]&quot; para criar um novo nó na estrutura. Este nó (chamado `_tenantId` neste exemplo) representa a ID do locatário da organização IMS, precedida por um sublinhado. A presença da ID do locatário indica que os campos que você está adicionando estão contidos no namespace da sua organização.

Em outras palavras, os campos que você está adicionando são exclusivos de sua organização e serão salvos na variável [!DNL Schema Registry] em uma área específica acessível somente à sua organização. Os campos definidos devem sempre ser adicionados ao namespace do locatário para evitar colisões com nomes de outras classes padrão, grupos de campos, tipos de dados e campos.

Dentro desse nó namespaces há um &quot;[!UICONTROL Novo campo]&quot;. Este é o início do &quot;[!UICONTROL Detalhes da Fidelidade]&quot; grupo de campos.

![](../images/tutorials/create-schema/new_field_loyalty.png)

Usando os controles no lado direito do editor, comece criando um `loyalty` campo com tipo &quot;[!UICONTROL Objeto]&quot; que será usado para manter seus campos relacionados à fidelidade. Quando terminar, selecione **[!UICONTROL Aplicar]**.

![](../images/tutorials/create-schema/loyalty_object.png)

As alterações são aplicadas e as `loyalty` é exibido. Selecione o **mais (+)** ícone ao lado do objeto para adicionar campos relacionados à fidelidade. Um &quot;[!UICONTROL Novo campo]&quot; é exibido e o **[!UICONTROL Propriedades do campo]** é visível no lado direito da tela.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

Cada campo requer as seguintes informações:

* **[!UICONTROL Nome do campo]:** O nome do campo, escrito em camel case. Exemplo: loyaltyLevel
* **[!UICONTROL Nome de exibição]:** O nome do campo, escrito no caso de título. Exemplo: Nível de Fidelidade
* **[!UICONTROL Tipo]:** O tipo de dados do campo. Isso inclui tipos escalares básicos e quaisquer tipos de dados definidos na variável [!DNL Schema Registry]. Exemplos: [!UICONTROL String], [!UICONTROL Número inteiro], [!UICONTROL Booleano], [!UICONTROL Pessoa], [!UICONTROL Endereço], [!UICONTROL Número de telefone], etc.
* **[!UICONTROL Descrição]:** Uma descrição opcional do campo deve ser incluída, escrita em caso de frase, com no máximo 200 caracteres.

O primeiro campo para a variável `Loyalty` será uma string chamada `loyaltyId`. Ao definir o tipo do novo campo como &quot;[!UICONTROL String]&quot;, o **[!UICONTROL Propriedades do campo]** torna-se preenchida com várias opções para aplicar restrições, incluindo valor padrão, formato e comprimento máximo.

![](../images/tutorials/create-schema/string_constraints.png)

Diferentes opções de restrição estão disponíveis dependendo do tipo de dados selecionado. Since `loyaltyId` será um endereço de email, selecione &quot;[!UICONTROL email]&quot; do **[!UICONTROL Formato]** menu suspenso. Selecionar **[!UICONTROL Aplicar]** para aplicar as alterações.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## Adicionar mais campos ao grupo de campos {#field-group-fields-2}

Agora que você adicionou o `loyaltyId` , é possível adicionar campos adicionais para capturar informações relacionadas à fidelidade, como:

* Pontos (número inteiro)
* Membro desde (data)

Para adicionar cada campo ao schema, selecione o **mais (+)** ícone ao lado do `loyalty` e preencha as informações necessárias.

Quando concluído, o objeto de Fidelidade conterá campos para ID de fidelidade, pontos e desde-o-membro.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## Adicionar um campo enum ao grupo de campos {#enum}

Ao definir campos na variável [!DNL Schema Editor], há algumas opções adicionais que podem ser aplicadas aos tipos básicos de campos para fornecer restrições adicionais sobre os dados que o campo pode conter. Os casos de uso dessas restrições são explicados na tabela a seguir:

| Restrição | Descrição |
| --- | --- |
| [!UICONTROL Obrigatório] | Indica que o campo é obrigatório para a assimilação de dados. Qualquer dado carregado em um conjunto de dados com base nesse esquema que não contenha esse campo falhará ao ser assimilado. |
| [!UICONTROL Matriz] | Indica que o campo contém uma matriz de valores, cada um com o tipo de dados especificado. Por exemplo, o uso dessa restrição em um campo com um tipo de dados &quot;[!UICONTROL String]&quot; especifica que o campo conterá uma matriz de sequências de caracteres. |
| [!UICONTROL Enum] | Indica que este campo deve conter um dos valores de uma lista enumerada de valores possíveis. |
| [!UICONTROL Identidade] | Indica que este campo é um campo de identidade. Mais informações sobre campos de identidade são fornecidas [mais tarde neste tutorial](#identity-field). |
| [!UICONTROL Relação] | Embora os relacionamentos de schema possam ser inferidos por meio do uso do schema de união e [!DNL Real-Time Customer Profile], isso se aplica somente a esquemas que compartilham a mesma classe. O [!UICONTROL Relação] constraint indica que esse campo faz referência à identidade primária de um schema com base em uma classe diferente, implicando uma relação entre os dois schemas. Veja o tutorial em [definição de uma relação](./relationship-ui.md) para obter mais informações. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Todos os campos obrigatórios, de identidade ou de relacionamento são mostrados no painel esquerdo, permitindo localizar esses campos facilmente, independentemente da complexidade do esquema.
>
>![](../images/tutorials/create-schema/left-rail-special.png)

Para este tutorial, a variável [!DNL "loyalty"] no esquema requer um novo campo enum que descreve o &quot;nível de fidelidade&quot; de um cliente, onde o valor pode ser apenas uma das quatro opções possíveis. Para adicionar esse campo ao schema, selecione o **mais (+)** ícone ao lado do `loyalty` e preencha os campos obrigatórios para **[!UICONTROL Nome do campo]** e **[!UICONTROL Nome de exibição]**. Para **[!UICONTROL Tipo]**, selecione &quot;[!UICONTROL String]&quot;.

![](../images/tutorials/create-schema/loyalty-level-type.png)

Caixas de seleção adicionais aparecem para o campo depois que seu tipo é selecionado, incluindo caixas de seleção para **[!UICONTROL Matriz]**, **[!UICONTROL Enum]** e **[!UICONTROL Identidade]**.

Selecione o **[!UICONTROL Enum]** caixa de seleção para abrir o **[!UICONTROL Valores Enum]** abaixo. Aqui você pode inserir o **[!UICONTROL Valor]** (em camelCase) e **[!UICONTROL Rótulo]** (um nome opcional e amigável para leitores no caso de título) para cada nível de fidelidade aceitável.

Após concluir todas as propriedades do campo, selecione **[!UICONTROL Aplicar]** para adicionar o &quot;[!DNL loyaltyLevel]&quot; para o campo `loyalty` objeto.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

## Converter um objeto de vários campos em um tipo de dados {#datatype}

O `loyalty` agora contém vários campos específicos de fidelidade e representa uma estrutura de dados comum que pode ser útil em outros schemas. O [!DNL Schema Editor] O permite aplicar prontamente objetos de vários campos reutilizáveis, convertendo a estrutura desses objetos em tipos de dados.

Os tipos de dados permitem o uso consistente de estruturas de vários campos e fornecem mais flexibilidade do que um grupo de campos, pois podem ser usados em qualquer lugar dentro de um esquema. Isso é feito definindo as **[!UICONTROL Tipo]** para o de qualquer tipo de dados definido na variável [!DNL Schema Registry].

Para converter o `loyalty` para um tipo de dados, selecione a variável `loyalty` campo sob **[!UICONTROL Estrutura]**, em seguida selecione **[!UICONTROL Converter em novo tipo de dados]** no lado direito do editor, abaixo **[!UICONTROL Propriedades do campo]**. Uma tampa verde é exibida, confirmando que o objeto foi convertido com êxito.

![](../images/tutorials/create-schema/convert-data-type.png)

Agora, quando você olha para baixo **[!UICONTROL Estrutura]**, você pode ver que a variável `loyalty` tem um tipo de dados de &quot;[!DNL Loyalty]&quot; e os campos têm pequenos ícones de bloqueio ao seu lado, indicando que não são mais campos individuais, mas parte de um tipo de dados de vários campos.

![](../images/tutorials/create-schema/loyalty_data_type.png)

Em um schema futuro, agora é possível atribuir um campo como um &quot;[!DNL Loyalty]&quot; e incluiria automaticamente campos para ID, nível de fidelidade, membro desde e pontos.

>[!NOTE]
>
>Você também pode criar e editar tipos de dados personalizados independentemente dos esquemas de edição. Consulte o guia sobre [criação e edição de tipos de dados](../ui/resources/data-types.md) para obter mais informações.

## Pesquisar e filtrar campos de esquema

O esquema agora contém vários grupos de campos além dos campos fornecidos pela classe base. Ao trabalhar com esquemas maiores, você pode marcar as caixas de seleção ao lado dos nomes dos grupos de campos no painel à esquerda para filtrar os campos exibidos somente para aqueles fornecidos pelos grupos de campos em que está interessado.

![](../images/tutorials/create-schema/filter-by-field-group.png)

Se você estiver procurando um campo específico no esquema, também poderá usar a barra de pesquisa para filtrar os campos exibidos por nome, independentemente do grupo de campos em que foram fornecidos.

![](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>A função de pesquisa considera todos os filtros de grupo de campos selecionados ao exibir campos correspondentes. Se uma consulta de pesquisa não estiver exibindo os resultados esperados, talvez seja necessário verificar novamente se você não está filtrando nenhum grupo de campo relevante.

## Definir um campo de esquema como um campo de identidade {#identity-field}

A estrutura de dados padrão fornecida pelos esquemas pode ser aproveitada para identificar dados pertencentes ao mesmo indivíduo em várias fontes, permitindo vários casos de uso downstream, como segmentação, relatórios, análise da ciência de dados e muito mais. Para compilar dados com base em identidades individuais, os campos principais devem ser marcados como [!UICONTROL Identidade] campos dentro de schemas aplicáveis.

[!DNL Experience Platform] facilita a identificação de um campo de identidade por meio do uso de um **[!UICONTROL Identidade]** na caixa de seleção [!DNL Schema Editor]. No entanto, você deve determinar qual campo é o melhor candidato a usar como identidade, com base na natureza de seus dados.

Por exemplo, pode haver milhares de membros do programa de fidelidade pertencentes ao mesmo &quot;nível de fidelidade&quot;, mas cada membro do programa de fidelidade tem um único `loyaltyId` (que, neste caso, é o endereço de email de cada membro). O fato de que `loyaltyId` é um identificador único para cada membro e o torna um bom candidato para um campo de identidade, enquanto `loyaltyLevel` não é.

>[!IMPORTANT]
>
>As etapas descritas abaixo abordam como adicionar um descritor de identidade a um campo de esquema existente. Como alternativa à definição de campos de identidade dentro da estrutura do próprio schema, também é possível usar um `identityMap` para conter informações de identidade.
>
>Se você planeja usar `identityMap`, lembre-se de que isso substituirá qualquer identidade primária adicionada ao schema diretamente. Consulte a seção sobre `identityMap` no [noções básicas do guia de composição do schema](../schema/composition.md#identityMap) para obter mais informações.

No **[!UICONTROL Estrutura]** do editor, selecione o `loyaltyId` e o **[!UICONTROL Identidade]** a caixa de seleção aparece em **[!UICONTROL Propriedades do campo]**. Marque a caixa e a opção para definir isso como a **[!UICONTROL Identidade primária]** é exibido. Selecione essa caixa também.

>[!NOTE]
>
>Cada schema pode conter apenas um campo de identidade primário. Depois que um campo de esquema tiver sido definido como a identidade primária, você receberá uma mensagem de erro se, posteriormente, tentar definir outro campo de identidade no esquema como primário.

Em seguida, você deve fornecer um **[!UICONTROL Namespace de identidade]** na lista de namespaces predefinidos na lista suspensa. Since `loyaltyId` é o endereço de email do cliente, selecione &quot;[!UICONTROL Email]&quot; na lista suspensa. Selecionar **[!UICONTROL Aplicar]** para confirmar as atualizações no `loyaltyId` campo.

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>Para obter uma lista de namespaces padrão e suas definições, consulte o [[!DNL Identity Service] documentação](../../identity-service/troubleshooting-guide.md#standard-namespaces).

Depois de aplicar a alteração, o ícone para `loyaltyId` mostra um símbolo de impressão digital, indicando que agora é um campo de identidade.

![](../images/tutorials/create-schema/identity-applied.png)

Agora todos os dados assimilados no `loyaltyId` será usado para ajudar a identificar esse indivíduo e unir uma única visualização desse cliente. Para saber mais sobre como trabalhar com identidades no [!DNL Experience Platform], reveja o [[!DNL Identity Service]](../../identity-service/home.md) documentação.

## Ative o esquema para usar em [!DNL Real-Time Customer Profile] {#profile}

[[!DNL Real-Time Customer Profile]](../../profile/home.md) usa dados de identidade em [!DNL Experience Platform] para fornecer uma visão holística de cada cliente individual. O serviço cria perfis robustos e de 360° dos atributos do cliente, bem como contas com carimbos de data e hora de cada interação que os clientes tiveram em qualquer sistema integrado com o [!DNL Experience Platform].

Para que um schema seja ativado para uso com o [!DNL Real-Time Customer Profile], deve ter uma identidade primária definida. Você receberá uma mensagem de erro ao tentar ativar um esquema sem primeiro definir uma identidade primária.

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

Para ativar o schema &quot;Membros de Fidelidade&quot; para uso em [!DNL Profile]comece selecionando &quot;[!DNL Loyalty Members]&quot; na **[!UICONTROL Estrutura]** do editor.

No lado direito do editor, são mostradas informações sobre o schema, incluindo o nome de exibição, a descrição e o tipo. Além dessas informações, há um **[!UICONTROL Perfil]** botão de alternância.

![](../images/tutorials/create-schema/profile-toggle.png)

Selecionar **[!UICONTROL Perfil]** e uma instância será exibida, solicitando que você confirme que deseja habilitar o schema de [!DNL Profile].

<img src="../images/tutorials/create-schema/enable-profile.png" width="700" /><br>

>[!WARNING]
>
>Depois que um schema é ativado para [!DNL Real-Time Customer Profile] e salvo, não poderá ser desativado.

Selecionar **[!UICONTROL Habilitar]** para confirmar sua escolha. Você pode selecionar a variável **[!UICONTROL Perfil]** alterne novamente para desativar o schema, se desejar, mas uma vez que o schema tenha sido salvo enquanto [!DNL Profile] estiver ativado, não poderá mais ser desativado.

## Próximas etapas e recursos adicionais

Agora que você terminou de compor o schema, é possível ver o schema completo na tela. Selecionar **[!UICONTROL Salvar]** e o esquema será salvo no [!DNL Schema Library], tornando-a acessível ao [!DNL Schema Registry].

O novo schema agora pode ser usado para assimilar dados no [!DNL Platform]. Lembre-se de que, uma vez que o schema tenha sido usado para assimilar dados, somente alterações aditivas poderão ser feitas. Consulte a [noções básicas da composição do schema](../schema/composition.md) para obter mais informações sobre o controle de versão do schema.

Agora você pode seguir o tutorial em [definição de uma relação de schema na interface do usuário](./relationship-ui.md) para adicionar um novo campo de relacionamento ao schema &quot;Membros de fidelidade&quot;.

O schema &quot;Membros de Fidelidade&quot; também está disponível para exibição e gerenciamento usando o [!DNL Schema Registry] API. Para começar a trabalhar com a API, comece lendo o [[!DNL Schema Registry API] guia do desenvolvedor](../api/getting-started.md).

### Recursos de vídeo

>[!WARNING]
>
>O [!DNL Platform] A interface do usuário exibida nos vídeos a seguir está desatualizada. Consulte a documentação acima para obter as capturas de tela e a funcionalidade mais recentes da interface do usuário.

O vídeo a seguir mostra como criar um schema simples no [!DNL Platform] IU.

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

O vídeo a seguir destina-se a reforçar sua compreensão sobre como trabalhar com grupos e classes de campo.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## Apêndice

As seções a seguir fornecem informações adicionais sobre o uso da variável [!DNL Schema Editor].

### Criar uma nova classe {#create-new-class}

[!DNL Experience Platform] O oferece a flexibilidade para definir um schema com base em uma classe exclusiva para sua organização. Para saber como criar uma nova classe, consulte o guia em [criação e edição de classes na interface do usuário](../ui/resources/classes.md#create).

### Alterar a classe de um schema {#change-class}

Você pode alterar a classe de um schema em qualquer ponto durante o processo de composição inicial antes que o schema tenha sido salvo.

>[!WARNING]
>
>A reatribuição da classe para um schema deve ser feita com extremo cuidado. Os grupos de campos são compatíveis apenas com determinadas classes e, portanto, alterar a classe redefinirá a tela e quaisquer campos adicionados.

Para saber como alterar a classe de um schema, consulte o guia em [gerenciamento de schemas na interface do usuário](../ui/resources/schemas.md).
