---
keywords: Experience Platform;home;popular topics;ui;UI;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema editor;Schema Editor;schema;Schema;schemas;Schemas;create
solution: Experience Platform
title: Criar um esquema usando o Editor de esquemas
topic: tutorial
type: Tutorial
description: Este tutorial aborda as etapas para a criação de um esquema usando o Editor de esquemas na Experience Platform.
translation-type: tm+mt
source-git-commit: e5c5fea783aa4088d225f771905fa8b2098613cf
workflow-type: tm+mt
source-wordcount: '3568'
ht-degree: 0%

---


# Crie um schema usando [!DNL Schema Editor]

A interface do usuário do Adobe Experience Platform permite que você crie e gerencie schemas [!DNL Experience Data Model] (XDM) em uma tela visual interativa chamada [!DNL Schema Editor]. Este tutorial aborda como criar um schema usando [!DNL Schema Editor].

>[!NOTE]
>
>Para fins de demonstração, as etapas neste tutorial envolvem a criação de um schema de exemplo que descreve os membros de um programa de fidelidade do cliente. Embora você possa usar essas etapas para criar um schema diferente para seus próprios fins, recomenda-se que você siga primeiro ao criar o schema de exemplo para aprender os recursos do [!DNL Schema Editor].

Se preferir compor um schema usando a API [!DNL Schema Registry], leia o [[!DNL Schema Registry] guia do desenvolvedor](../api/getting-started.md) antes de tentar o tutorial em [criar um schema usando a API](create-schema-api.md).

## Introdução

Este tutorial requer um entendimento prático dos vários aspectos do Adobe Experience Platform envolvidos na criação de schemas. Antes de iniciar este tutorial, reveja a documentação para obter os seguintes conceitos:

* [[!DNL Experience Data Model (XDM)]](../home.md): A estrutura padronizada pela qual  [!DNL Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../schema/composition.md) do schema: Uma visão geral dos schemas XDM e seus blocos de construção, incluindo classes, misturas, tipos de dados e campos.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

## Abra a área de trabalho [!UICONTROL Schemas] {#browse}

A área de trabalho [!UICONTROL Schemas] na interface do usuário [!DNL Platform] fornece uma visualização da [!DNL Schema Library], permitindo que você visualização o gerenciamento dos schemas disponíveis para sua organização. A área de trabalho também inclui a tela [!DNL Schema Editor], na qual você pode compor um schema em todo este tutorial.

Depois de fazer logon em [!DNL Experience Platform], selecione **[!UICONTROL Schemas]** no painel de navegação esquerdo para abrir o espaço de trabalho **[!UICONTROL Schemas]**. A guia **[!UICONTROL Procurar]** exibe uma lista de schemas (uma representação de [!DNL Schema Library]) que você pode visualização e personalizar. A lista inclui o nome, o tipo, a classe e o comportamento (registro ou série de tempo) em que o schema se baseia, bem como a data e a hora em que o schema foi modificado pela última vez.

Consulte o guia em [exploração dos recursos XDM existentes na interface do usuário](../ui/explore.md) para obter mais informações.

## Criar e nomear um schema {#create}

Para começar a compor um schema, selecione **[!UICONTROL Criar schema]** no canto superior direito da área de trabalho **[!UICONTROL Schemas]**. Um menu suspenso é exibido, dando a você a opção de escolher entre as classes principais [!UICONTROL Perfil individual XDM] e [!UICONTROL ExperienceEvent]. Se essas classes não se adequarem aos seus propósitos, você também poderá selecionar **[!UICONTROL Procurar]** para escolher entre outras classes disponíveis ou [criar uma nova classe](#create-new-class).

Para os fins deste tutorial, selecione **[!UICONTROL Perfil individual XDM]**.

![](../images/tutorials/create-schema/create_schema_button.png)

O [!DNL Schema Editor] é exibido. Esta é a tela sobre a qual você irá compor seu schema. Como você escolheu uma classe XDM padrão para basear o schema, um schema sem título é criado automaticamente na seção **[!UICONTROL Estrutura]** da tela quando você chega ao editor, juntamente com os campos padrão incluídos em todos os schemas com base nessa classe. A classe atribuída ao schema também está listada em **[!UICONTROL Class]** na seção **[!UICONTROL Composition]**.

![](../images/tutorials/create-schema/schema_editor.png)

>[!NOTE]
>
>Você pode [alterar a classe de um schema](#change-class) a qualquer momento durante o processo de composição inicial antes que o schema seja salvo, mas isso deve ser feito com extrema cautela. Misturas são compatíveis somente com certas classes, e, portanto, alterar a classe redefinirá a tela de desenho e quaisquer campos adicionados.

Use os campos no lado direito do editor para fornecer um nome de exibição e uma descrição opcional para o schema. Depois que um nome é inserido, a tela é atualizada para refletir o novo nome do schema.

![](../images/tutorials/create-schema/name_schema.png)

Há várias considerações importantes a serem feitas ao decidir um nome para o seu schema:

* Os nomes de schemas devem ser curtos e descritivos para que o schema possa ser facilmente encontrado posteriormente.
* Os nomes dos schemas devem ser exclusivos, o que significa que também devem ser específicos o suficiente para que não sejam reutilizados no futuro. Por exemplo, se sua organização tivesse programas de fidelidade separados para diferentes marcas, seria aconselhável nomear seu schema como &quot;Membros de fidelidade da Marca A&quot; para facilitar a distinção entre outros schemas relacionados à fidelidade que você possa definir posteriormente.
* Você também pode usar a descrição do schema para fornecer quaisquer informações contextuais adicionais relacionadas ao schema.

Este tutorial compõe um schema para assimilar dados relacionados aos membros de um programa de fidelidade e, portanto, o schema é denominado &quot;Membros de fidelidade&quot;.

## Adicionar uma mistura {#mixin}

Agora você pode começar a adicionar campos ao seu schema adicionando mixins. Uma combinação é um grupo de um ou mais campos que são frequentemente usados em conjunto para descrever um conceito específico. Este tutorial usa mixins para descrever os membros do programa de fidelidade e capturar informações-chave como nome, aniversário, número de telefone, endereço e muito mais.

Para adicionar uma mistura, selecione **[!UICONTROL Adicionar]** na subseção **[!UICONTROL Misturas]**.

![](../images/tutorials/create-schema/add_mixin_button.png)

Uma nova caixa de diálogo é exibida, exibindo uma lista de combinações disponíveis. Cada mixin é destinada somente para uso com uma classe específica, portanto, a caixa de diálogo somente lista as combinações compatíveis com a classe selecionada (neste caso, a classe [!DNL XDM Individual Profile]). Se você estiver usando uma classe XDM padrão, a lista de combinações será classificada de forma inteligente com base na popularidade de uso.

![](../images/tutorials/create-schema/mixin-popularity.png)

Selecionar uma mistura na lista faz com que ela apareça no painel direito. Se desejar, você pode selecionar várias combinações, adicionando cada uma à lista no painel direito antes de confirmar. Além disso, um ícone é exibido no lado direito do mixin atualmente selecionado, permitindo que você pré-visualização a estrutura dos campos fornecidos.

![](../images/tutorials/create-schema/preview-mixin-button.png)

Ao visualizar uma mistura, uma descrição detalhada do schema da mistura é fornecida no painel direito. Também é possível navegar pelos campos do mixin na tela fornecida. À medida que você seleciona campos diferentes, o painel direito é atualizado para mostrar detalhes sobre o campo em questão. Selecione **[!UICONTROL Voltar]** quando terminar a visualização para voltar à caixa de diálogo de seleção de combinação.

![](../images/tutorials/create-schema/preview-mixin.png)

Para este tutorial, selecione a combinação **[!UICONTROL Detalhes Demográficos]** e **[!UICONTROL Adicionar mistura]**.

![](../images/tutorials/create-schema/add_mixin_person_details.png)

A tela do schema é exibida novamente. A seção **[!UICONTROL Mixins]** agora lista &quot;[!UICONTROL Detalhes Demográficos]&quot; e a seção **[!UICONTROL Estrutura]** inclui os campos contribuídos pelo mixin. Você pode selecionar o nome da mistura na seção **[!UICONTROL Mixins]** para realçar os campos específicos fornecidos na tela.

![](../images/tutorials/create-schema/person_details_structure.png)

Esse mixin contribui com vários campos sob o nome de nível superior `person` com o tipo de dados &quot;[!UICONTROL Pessoa]&quot;. Este grupo de campos descreve informações sobre um indivíduo, incluindo nome, data de nascimento e sexo.

>[!NOTE]
>
>Lembre-se de que os campos podem usar tipos escalares (como string, integer, array ou data), bem como qualquer tipo de dados (um grupo de campos que representa um conceito comum) definido em [!DNL Schema Registry].

Observe que o campo `name` tem um tipo de dados &quot;[!UICONTROL Nome da pessoa]&quot;, o que significa que também descreve um conceito comum e contém subcampos relacionados ao nome, como nome, sobrenome, título de cortesia e sufixo.

Selecione os diferentes campos na tela para revelar quaisquer campos adicionais que contribuem para a estrutura do schema.

## Adicionar outra mistura {#mixin-2}

Agora você pode repetir as mesmas etapas para adicionar outra mixin. Quando você visualização a caixa de diálogo **[!UICONTROL Adicionar mixin]** desta vez, observe que a combinação &quot;[!UICONTROL Detalhes Demográficos]&quot; está esmaecida e a caixa de seleção ao lado dela não pode ser selecionada. Isso evita que você duplique acidentalmente misturas que já foram incluídas no schema atual.

Para este tutorial, selecione a combinação &quot;[!DNL Personal Contact Details]&quot; na caixa de diálogo e, em seguida, selecione **[!UICONTROL Adicionar mistura]** para adicioná-la ao schema.

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

Depois de adicionada, a tela de desenho reaparece. &quot;[!UICONTROL Detalhes do Contato Pessoal]&quot; agora está listado em **[!UICONTROL Mixins]** na seção **[!UICONTROL Composição]**, e os campos para endereço residencial, telefone celular e muito mais foram adicionados em **[!UICONTROL Estrutura]**.

Semelhante ao campo `name`, os campos que você acabou de adicionar representam os conceitos de vários campos. Por exemplo, `homeAddress` tem um tipo de dados de &quot;[!UICONTROL Endereço postal]&quot; e `mobilePhone` tem um tipo de dados de &quot;[!UICONTROL Número de telefone]&quot;. Você pode selecionar cada um desses campos para expandi-los e ver os campos adicionais incluídos no tipo de dados.

![](../images/tutorials/create-schema/personal_details_structure.png)

## Definir uma nova mistura {#define-mixin}

O schema &quot;[!UICONTROL Membros de Fidelidade]&quot; destina-se a capturar dados relacionados aos membros de um programa de fidelidade, pelo que exigirá alguns campos específicos relacionados à fidelidade. Não há combinações padrão disponíveis que contenham os campos necessários, portanto, será necessário definir uma nova mistura.

Desta vez, ao abrir a caixa de diálogo **[!UICONTROL Adicionar mistura]**, selecione **[!UICONTROL Criar nova mistura]**. Você será solicitado a fornecer um nome de exibição e uma descrição para a sua combinação.

![](../images/tutorials/create-schema/mixin_create_new.png)

Assim como com os nomes de classe, o nome da mistura deve ser curto e simples, descrevendo o que a mistura contribuirá para o schema. Eles também são únicos, portanto, você não poderá reutilizar o nome e deve, portanto, garantir que seja suficientemente específico.

Para este tutorial, nomeie a nova combinação como &quot;Detalhes da fidelidade&quot;.

Selecione **[!UICONTROL Adicionar mixin]** para voltar para [!DNL Schema Editor]. &quot;[!UICONTROL Detalhes da Fidelidade]&quot; agora deve aparecer em **[!UICONTROL Mixins]** no lado esquerdo da tela, mas ainda não há campos associados a ela e, portanto, nenhum novo campo aparece em **[!UICONTROL Estrutura]**.

## Adicionar campos ao mixin {#mixin-fields}

Agora que você criou a combinação &quot;Detalhes da Fidelidade&quot;, é hora de definir os campos que a combinação contribuirá para o schema.

Para começar, selecione o nome da mistura na seção **[!UICONTROL Mixins]**. Assim que você fizer isso, as propriedades do mixin aparecerão no lado direito do editor e um ícone **mais (+)** aparecerá ao lado do nome do schema em **[!UICONTROL Estrutura]**.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

Selecione o ícone **mais (+)** ao lado de &quot;[!DNL Loyalty Members]&quot; para criar um novo nó na estrutura. Esse nó (chamado `_tenantId` neste exemplo) representa a ID de locatário da Organização IMS, precedida de um sublinhado. A presença da ID do locatário indica que os campos que você está adicionando estão contidos na namespace de sua organização.

Em outras palavras, os campos que você está adicionando são exclusivos à sua organização e serão salvos em [!DNL Schema Registry] em uma área específica acessível apenas à sua organização. Os campos que você definir devem ser sempre adicionados à namespace do locatário para evitar colisões com nomes de outras classes padrão, combinações, tipos de dados e campos.

Dentro desse nó com namespaces há um &quot;[!UICONTROL Novo campo]&quot;. Este é o início da combinação &quot;[!UICONTROL Detalhes da Fidelidade]&quot;.

![](../images/tutorials/create-schema/new_field_loyalty.png)

Usando os controles no lado direito do editor, crie um campo `loyalty` com o tipo &quot;[!UICONTROL Object]&quot; que será usado para manter seus campos relacionados à fidelidade. Quando terminar, selecione **[!UICONTROL Aplicar]**.

![](../images/tutorials/create-schema/loyalty_object.png)

As alterações são aplicadas e o objeto `loyalty` recém-criado é exibido. Selecione o ícone **mais (+)** ao lado do objeto para adicionar campos adicionais relacionados à fidelidade. Uma seção &quot;[!UICONTROL Novo campo]&quot; é exibida e a seção **[!UICONTROL Propriedades de campo]** é visível no lado direito da tela.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

Cada campo requer as seguintes informações:

* **[!UICONTROL Nome] do campo:** o nome do campo, escrito em caso de camelo. Exemplo: leyaltyLevel
* **[!UICONTROL Nome] para exibição:** o nome do campo, escrito em caso de título. Exemplo: Nível de Fidelidade
* **[!UICONTROL Tipo]:** O tipo de dados do campo. Isso inclui tipos escalares básicos e quaisquer tipos de dados definidos em [!DNL Schema Registry]. Exemplos: [!UICONTROL Cadeia], [!UICONTROL Número inteiro], [!UICONTROL Booliano], [!UICONTROL Pessoa], [!UICONTROL Endereço], [!UICONTROL Número de telefone], etc.
* **[!UICONTROL Descrição]:** uma descrição opcional do campo deve ser incluída, escrita em caso de sentença, com um máximo de 200 caracteres.

O primeiro campo para o objeto `Loyalty` será uma string chamada `loyaltyId`. Ao definir o tipo do novo campo como &quot;[!UICONTROL String]&quot;, a seção **[!UICONTROL Propriedades do campo]** é preenchida com várias opções para aplicar restrições, incluindo valor padrão, formato e comprimento máximo.

![](../images/tutorials/create-schema/string_constraints.png)

Diferentes opções de restrição estão disponíveis dependendo do tipo de dados selecionado. Como `loyaltyId` será um endereço de email, selecione &quot;[!UICONTROL email]&quot; no menu suspenso **[!UICONTROL Formato]**. Selecione **[!UICONTROL Aplicar]** para aplicar as alterações.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## Adicionar mais campos ao mixin {#mixin-fields-2}

Agora que você adicionou o campo `loyaltyId`, é possível adicionar campos adicionais para capturar informações relacionadas à fidelidade, como:

* Pontos (número inteiro)
* Membro desde (data)

Para adicionar cada campo ao schema, selecione o ícone **mais (+)** ao lado do objeto `loyalty` e preencha as informações necessárias.

Quando concluído, o objeto de Fidelidade conterá campos para ID de fidelidade, pontos e membro-a-partir.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## Adicionar um campo enum à mistura {#enum}

Ao definir campos em [!DNL Schema Editor], há algumas opções adicionais que podem ser aplicadas a tipos de campos básicos para fornecer restrições adicionais aos dados que o campo pode conter. Os casos de uso para essas restrições são explicados na tabela a seguir:

| Restrição | Descrição |
| --- | --- |
| [!UICONTROL Obrigatório] | Indica que o campo é obrigatório para a ingestão de dados. Todos os dados carregados em um conjunto de dados com base nesse schema que não contém esse campo falharão após a ingestão. |
| [!UICONTROL Matriz] | Indica que o campo contém uma matriz de valores, cada um com o tipo de dados especificado. Por exemplo, usar essa restrição em um campo com um tipo de dados &quot;[!UICONTROL String]&quot; especifica que o campo conterá uma matriz de sequências de caracteres. |
| [!UICONTROL Enum] | Indica que esse campo deve conter um dos valores de uma lista enumerada de valores possíveis. |
| [!UICONTROL Identidade] | Indica que este campo é um campo de identidade. Mais informações sobre campos de identidade são fornecidas [posteriormente neste tutorial](#identity-field). |
| [!UICONTROL Relação] | Embora as relações de schema possam ser inferidas com o uso do schema de união e [!DNL Real-time Customer Profile], isso se aplica somente aos schemas que compartilham a mesma classe. A restrição [!UICONTROL Relationship] indica que este campo faz referência à identidade primária de um schema com base numa classe diferente, o que implica uma relação entre os dois schemas. Consulte o tutorial em [definindo uma relação](./relationship-ui.md) para obter mais informações. |

>[!NOTE]
>
>Todos os campos obrigatórios, de identidade ou de relacionamento são mostrados no painel esquerdo, permitindo que você localize esses campos facilmente, independentemente da complexidade do schema.
>
>![](../images/tutorials/create-schema/left-rail-special.png)

Para este tutorial, o objeto [!DNL "loyalty"] no schema requer um novo campo enum que descreve o &quot;nível de fidelidade&quot; de um cliente, onde o valor pode ser apenas uma das quatro opções possíveis. Para adicionar esse campo ao schema, selecione o ícone **mais (+)** ao lado do objeto `loyalty` e preencha os campos obrigatórios para **[!UICONTROL Nome do campo]** e **[!UICONTROL Nome de exibição]**. Para **[!UICONTROL Type]**, selecione &quot;[!UICONTROL String]&quot;.

![](../images/tutorials/create-schema/loyalty-level-type.png)

Caixas de seleção adicionais aparecem para o campo depois que seu tipo é selecionado, incluindo caixas de seleção para **[!UICONTROL Array]**, **[!UICONTROL Enum]** e **[!UICONTROL Identity]**.

Marque a caixa de seleção **[!UICONTROL Enum]** para abrir a seção **[!UICONTROL Enum values]** abaixo. Aqui você pode inserir **[!UICONTROL Value]** (em camelCase) e **[!UICONTROL Label]** (um nome opcional e amigável para o leitor no Título Case) para cada nível de fidelidade aceitável.

Depois de concluir todas as propriedades do campo, selecione **[!UICONTROL Aplicar]** para adicionar o campo &quot;[!DNL loyaltyLevel]&quot; ao objeto `loyalty`.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

## Converter um objeto de vários campos em um tipo de dados {#datatype}

O objeto `loyalty` agora contém vários campos específicos de fidelidade e representa uma estrutura de dados comum que pode ser útil em outros schemas. O [!DNL Schema Editor] permite que você aplique objetos de vários campos reutilizáveis rapidamente, convertendo a estrutura desses objetos em tipos de dados.

Os tipos de dados permitem o uso consistente de estruturas de vários campos e proporcionam mais flexibilidade do que uma combinação, pois podem ser usados em qualquer lugar dentro de um schema. Isso é feito configurando o valor **[!UICONTROL Type]** do campo para o valor de qualquer tipo de dados definido em [!DNL Schema Registry].

Para converter o objeto `loyalty` em um tipo de dados, selecione o campo `loyalty` em **[!UICONTROL Estrutura]**, em seguida, selecione **[!UICONTROL Converter em novo tipo de dados]** no lado direito do editor em **[!UICONTROL Propriedades de campos]**. Uma janela verde é exibida, confirmando que o objeto foi convertido com êxito.

![](../images/tutorials/create-schema/convert-data-type.png)

Agora, quando você olha em **[!UICONTROL Structure]**, você pode ver que o campo `loyalty` tem um tipo de dados de &quot;[!DNL Loyalty]&quot; e que os campos têm pequenos ícones de bloqueio ao seu lado, indicando que não são mais campos individuais, mas sim parte de um tipo de dados de vários campos.

![](../images/tutorials/create-schema/loyalty_data_type.png)

Em um schema futuro, agora é possível atribuir um campo como um tipo &quot;[!DNL Loyalty]&quot; e ele incluirá automaticamente campos para ID, nível de fidelidade, membro desde e pontos.

>[!NOTE]
>
>Você também pode criar e editar tipos de dados personalizados independentemente de schemas de edição. Consulte o guia em [criar e editar tipos de dados](../ui/resources/data-types.md) para obter mais informações.

## Pesquisar e filtrar campos de schema

Seu schema agora contém várias combinações além dos campos fornecidos por sua classe base. Ao trabalhar com schemas maiores, você pode marcar as caixas de seleção ao lado dos nomes de mixagem no painel esquerdo para filtrar os campos exibidos somente para os campos fornecidos pelas combinações que você está interessado.

![](../images/tutorials/create-schema/filter-by-mixin.png)

Se você estiver procurando um campo específico no seu schema, também poderá usar a barra de pesquisa para filtrar os campos exibidos pelo nome, independentemente da combinação em que eles são fornecidos.

![](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>A função de pesquisa leva em conta qualquer filtros de combinação selecionado ao exibir campos correspondentes. Se um query de pesquisa não estiver exibindo os resultados que você espera, talvez seja necessário verificar no duplo se você não está filtrando nenhuma mistura relevante.

## Definir um campo de schema como um campo de identidade {#identity-field}

A estrutura de dados padrão que os schemas fornecem pode ser aproveitada para identificar dados pertencentes ao mesmo indivíduo em várias fontes, permitindo vários casos de uso downstream, como segmentação, relatórios, análise de ciência de dados e muito mais. Para unir dados com base em identidades individuais, os campos principais devem ser marcados como campos [!UICONTROL Identity] nos schemas aplicáveis.

[!DNL Experience Platform] facilita a identificação de um campo de identidade através do uso de uma caixa de seleção  **** Identificador no  [!DNL Schema Editor]. No entanto, você deve determinar qual campo é o melhor candidato a usar como uma identidade, com base na natureza de seus dados.

Por exemplo, pode haver milhares de membros do programa de fidelidade pertencentes ao mesmo &quot;nível de fidelidade&quot;, mas cada membro do programa de fidelidade tem um `loyaltyId` exclusivo (que, neste caso, é o endereço de email de cada membro). O fato de `loyaltyId` ser um identificador exclusivo para cada membro faz dele um bom candidato para um campo de identidade, ao passo que `loyaltyLevel` não é.

>[!IMPORTANT]
>
>As etapas descritas abaixo abordam como adicionar um descritor de identidade a um campo de schema existente. Como alternativa à definição de campos de identidade na estrutura do próprio schema, também é possível usar um campo `identityMap` para conter informações de identidade.
>
>Se você planeja usar `identityMap`, lembre-se de que isso substituirá qualquer identidade primária adicionada ao schema diretamente. Consulte a seção `identityMap` no [básico do guia de composição do schema](../schema/composition.md#identityMap) para obter mais informações.

Na seção **[!UICONTROL Estrutura]** do editor, selecione o campo `loyaltyId` e a caixa de seleção **[!UICONTROL Identity]** será exibida em **[!UICONTROL Propriedades de campo]**. Marque a caixa e a opção para definir isso como **[!UICONTROL Identidade primária]** é exibida. Selecione essa caixa também.

>[!NOTE]
>
>Cada schema pode conter apenas um campo de identidade principal. Depois que um campo de schema for definido como a identidade primária, você receberá uma mensagem de erro se tentar definir outro campo de identidade no schema como principal.

Em seguida, você deve fornecer uma **[!UICONTROL namespace de identidade]** da lista de namespaces predefinidas na lista suspensa. Como `loyaltyId` é o endereço de email do cliente, selecione &quot;[!UICONTROL Email]&quot; na lista suspensa. Selecione **[!UICONTROL Aplicar]** para confirmar as atualizações do campo `loyaltyId`.

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>Para obter uma lista de namespaces padrão e suas definições, consulte a [[!DNL Identity Service] documentação](../../identity-service/troubleshooting-guide.md#standard-namespaces).

Depois de aplicar a alteração, o ícone de `loyaltyId` mostra um símbolo de impressão digital, indicando que agora é um campo de identidade.

![](../images/tutorials/create-schema/identity-applied.png)

Agora, todos os dados ingeridos no campo `loyaltyId` serão usados para ajudar a identificar esse indivíduo e unir uma única visualização do cliente. Para saber mais sobre como trabalhar com identidades em [!DNL Experience Platform], consulte a documentação [[!DNL Identity Service]](../../identity-service/home.md).

## Ative o schema para uso em [!DNL Real-time Customer Profile] {#profile}

[[!DNL Real-time Customer Profile]](../../profile/home.md) aproveita os dados de identidade  [!DNL Experience Platform] para fornecer uma visualização holística de cada cliente individual. O serviço cria perfis robustos, 360°, de atributos do cliente, bem como contas com carimbos de data e hora de cada interação que os clientes tiveram em qualquer sistema integrado com [!DNL Experience Platform].

Para que um schema seja habilitado para uso com [!DNL Real-time Customer Profile], ele deve ter uma identidade primária definida. Você receberá uma mensagem de erro se tentar ativar um schema sem primeiro definir uma identidade primária.

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

Para ativar o schema &quot;Membros de Fidelidade&quot; para uso em [!DNL Profile], comece selecionando &quot;[!DNL Loyalty Members]&quot; na seção **[!UICONTROL Estrutura]** do editor.

No lado direito do editor, são mostradas informações sobre o schema, incluindo seu nome de exibição, descrição e tipo. Além dessas informações, há um botão de alternância **[!UICONTROL Perfil]**.

![](../images/tutorials/create-schema/profile-toggle.png)

Selecione **[!UICONTROL Perfil]** e um provedor será exibido, solicitando que você confirme que deseja ativar o schema para [!DNL Profile].

<img src="../images/tutorials/create-schema/enable-profile.png" width="700" /><br>

>[!WARNING]
>
>Depois que um schema é ativado para [!DNL Real-time Customer Profile] e salvo, ele não pode ser desativado.

Selecione **[!UICONTROL Habilitar]** para confirmar sua escolha. Você pode selecionar a alternância **[!UICONTROL Perfil]** novamente para desativar o schema, se desejar, mas depois que o schema for salvo enquanto [!DNL Profile] estiver ativado, ele não poderá mais ser desativado.

## Próximos passos e recursos adicionais

Agora que você terminou de compor o schema, você pode ver o schema completo na tela. Selecione **[!UICONTROL Salvar]** e o schema será salvo em [!DNL Schema Library], tornando-o acessível pelo [!DNL Schema Registry].

Seu novo schema agora pode ser usado para assimilar dados em [!DNL Platform]. Lembre-se de que, uma vez que o schema tenha sido usado para ingerir dados, somente alterações aditivas poderão ser feitas. Consulte as [noções básicas da composição do schema](../schema/composition.md) para obter mais informações sobre o controle de versão do schema.

Agora você pode seguir o tutorial em [definindo uma relação de schema na interface do usuário](./relationship-ui.md) para adicionar um novo campo de relação ao schema &quot;Membros de Fidelidade&quot;.

O schema &quot;Membros de fidelidade&quot; também está disponível para exibição e gerenciamento usando a API [!DNL Schema Registry]. Para começar a trabalhar com a API, leia o [[!DNL Schema Registry API] guia do desenvolvedor](../api/getting-started.md).

### Recursos de vídeo

>[!WARNING]
>
>A interface do usuário [!DNL Platform] mostrada nos vídeos a seguir está desatualizada. Consulte a documentação acima para obter as capturas de tela e a funcionalidade mais recentes da interface do usuário.

O vídeo a seguir mostra como criar um schema simples na interface do usuário [!DNL Platform].

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

O vídeo a seguir destina-se a reforçar sua compreensão sobre como trabalhar com mixins e classes.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## Apêndice

As seções a seguir fornecem informações adicionais sobre o uso do [!DNL Schema Editor].

### Criar uma nova classe {#create-new-class}

[!DNL Experience Platform] fornece a flexibilidade para definir um schema com base em uma classe exclusiva de sua organização. Para saber como criar uma nova classe, consulte o guia em [criar e editar classes na interface do usuário](../ui/resources/classes.md#create).

### Alterar a classe de um schema {#change-class}

É possível alterar a classe de um schema em qualquer ponto durante o processo de composição inicial antes que o schema seja salvo.

>[!WARNING]
>
>A reatribuição da classe para um schema deve ser feita com extrema cautela. Misturas são compatíveis somente com certas classes, e, portanto, alterar a classe redefinirá a tela de desenho e quaisquer campos adicionados.

Para saber como alterar a classe de um schema, consulte o guia sobre [como gerenciar schemas na interface do usuário](../ui/resources/schemas.md).