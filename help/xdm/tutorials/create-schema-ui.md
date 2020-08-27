---
keywords: Experience Platform;home;popular topics;schema;Schema;create schema;enum;XDM individual profile;primary identity;primary idenity;enum datatype;schema design
solution: Experience Platform
title: Criar um esquema usando o Editor de esquemas.
topic: tutorials
description: Este tutorial aborda as etapas para a criação de um schema usando o Editor de Schemas no Experience Platform.
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '3528'
ht-degree: 0%

---


# Crie um schema usando a variável [!DNL Schema Editor]

A interface do usuário do Adobe Experience Platform permite criar e gerenciar schemas [!DNL Experience Data Model] (XDM) em uma tela visual interativa chamada de [!DNL Schema Editor]. Este tutorial aborda como criar um schema usando o [!DNL Schema Editor].

>[!NOTE]
>
>Para fins de demonstração, as etapas neste tutorial envolvem a criação de um schema de exemplo que descreve os membros de um programa de fidelidade do cliente. Embora você possa usar essas etapas para criar um schema diferente para os seus propósitos, recomenda-se que você siga as etapas para criar o schema de exemplo e aprender os recursos do [!DNL Schema Editor].

Se você preferir compor um schema usando a [!DNL Schema Registry] API, leia o guia [[!DNL Schema Registry] do](../api/getting-started.md) desenvolvedor antes de tentar o tutorial sobre como [criar um schema usando a API](create-schema-api.md).

## Introdução

Este tutorial requer um entendimento prático dos vários aspectos do Adobe Experience Platform envolvidos na criação de schemas. Antes de iniciar este tutorial, reveja a documentação para obter os seguintes conceitos:

* [[!DNL Experience Data Model (XDM)]](../home.md): A estrutura padronizada pela qual [!DNL Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../schema/composition.md)do schema: Uma visão geral dos schemas XDM e seus blocos de construção, incluindo classes, misturas, tipos de dados e campos.
* [[!DNL Perfil do cliente em tempo real]](../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

## Procurar schemas existentes na área de trabalho de [!UICONTROL Schemas] {#browse}

A área de trabalho de [!UICONTROL Schemas] na [!DNL Platform] interface do usuário fornece uma visualização do [!DNL Schema Library], permitindo que você visualização gerenciar os schemas disponíveis para sua organização. A área de trabalho também inclui a tela [!DNL Schema Editor], na qual você pode compor um schema em todo este tutorial.

Depois de fazer logon [!DNL Experience Platform], selecione **[!UICONTROL Schemas]** na navegação à esquerda para abrir a área de trabalho de **[!UICONTROL Schemas]** . A guia **[!UICONTROL Procurar]** exibe uma lista de schemas (uma representação do [!DNL Schema Library]) que você pode visualização e personalizar. A lista inclui o nome, o tipo, a classe e o comportamento (registro ou série de tempo) em que o schema se baseia, bem como a data e a hora em que o schema foi modificado pela última vez.

Selecione o ícone de filtro ao lado da barra de pesquisa para usar os recursos de filtragem para todos os recursos no registro, incluindo classes, mixins e tipos de dados. Você também pode filtrar com base em se os recursos são de propriedade do Adobe ou de sua organização e se foram habilitados para uso em [!DNL Real-time Customer Profile].

![](../images/tutorials/create-schema/schemas_filter.png)

## Criar e nomear um schema {#create}

Para começar a compor um schema, selecione **[!UICONTROL Criar Schema]** no canto superior direito da área de trabalho dos **[!UICONTROL Schemas]** . Um menu suspenso é exibido, dando a você a opção de escolher entre as classes principais Perfil [!UICONTROL XDM Individual e] XDM ExperienceEvent , ou de navegar por outras classes disponíveis. Para os fins deste tutorial, selecione Perfil **[!UICONTROL individual]** XDM.

![](../images/tutorials/create-schema/create_schema_button.png)

O [!DNL Schema Editor] é exibido. Esta é a tela sobre a qual você irá compor seu schema. Quando você chega ao editor, um schema sem título é criado automaticamente na seção **[!UICONTROL Estrutura]** da tela, juntamente com os campos padrão incluídos em todos os schemas com base na classe [!UICONTROL XDM Individual Perfil] . A classe atribuída ao schema está listada em **[!UICONTROL Classe]** na seção **[!UICONTROL Composição]** .

![](../images/tutorials/create-schema/schema_editor.png)

>[!NOTE]
>
>Você pode [alterar a classe de um schema](#change-class) em qualquer ponto durante o processo de composição inicial antes que o schema seja salvo, mas isso deve ser feito com extrema cautela. Misturas são compatíveis somente com certas classes, e, portanto, alterar a classe redefinirá a tela de desenho e quaisquer campos adicionados.

Use os campos no lado direito do editor para fornecer um nome de exibição e uma descrição opcional para o schema. Depois que um nome é inserido, a tela é atualizada para refletir o novo nome do schema.

![](../images/tutorials/create-schema/name_schema.png)

Há várias considerações importantes a serem feitas ao decidir um nome para o seu schema:

* Os nomes de schemas devem ser curtos e descritivos para que o schema possa ser facilmente encontrado posteriormente.
* Os nomes dos schemas devem ser exclusivos, o que significa que também devem ser específicos o suficiente para que não sejam reutilizados no futuro. Por exemplo, se sua organização tivesse programas de fidelidade separados para diferentes marcas, seria aconselhável nomear seu schema como &quot;Membros de fidelidade da Marca A&quot; para facilitar a distinção entre outros schemas relacionados à fidelidade que você possa definir posteriormente.
* Você também pode usar a descrição do schema para fornecer quaisquer informações contextuais adicionais relacionadas ao schema.

Este tutorial compõe um schema para assimilar dados relacionados aos membros de um programa de fidelidade e, portanto, o schema é denominado &quot;Membros de fidelidade&quot;.

## Adicionar uma mistura {#mixin}

Agora você pode começar a adicionar campos ao seu schema adicionando mixins. Uma combinação é um grupo de um ou mais campos que são frequentemente usados em conjunto para descrever um conceito específico. Este tutorial usa mixins para descrever os membros do programa de fidelidade e capturar informações-chave como nome, aniversário, número de telefone, endereço e muito mais.

Para adicionar uma mistura, selecione **[!UICONTROL Adicionar]** na subseção **[!UICONTROL Misturas]** .

![](../images/tutorials/create-schema/add_mixin_button.png)

Uma nova caixa de diálogo é exibida, exibindo uma lista de combinações disponíveis. Cada mistura é destinada somente para uso com uma classe específica, portanto, a caixa de diálogo somente lista combinações compatíveis com a classe selecionada (neste caso, a [!DNL XDM Individual Profile] classe).

Selecionar uma mistura na lista faz com que ela apareça no painel direito. Além disso, um ícone é exibido no lado direito do mixin selecionado, permitindo que você pré-visualização a estrutura dos campos fornecidos. Selecione a combinação Detalhes **[!UICONTROL da pessoa do]** Perfil e selecione **[!UICONTROL Adicionar mistura]**.

![](../images/tutorials/create-schema/add_mixin_person_details.png)

A tela do schema é exibida novamente. A seção **[!UICONTROL Misturas]** agora lista &quot;Detalhes[!UICONTROL da pessoa do]Perfil&quot; e a seção **[!UICONTROL Estrutura]** inclui os campos contribuídos pelo mixin. Você pode selecionar o nome da mistura na seção **[!UICONTROL Misturas]** para realçar os campos específicos que ela fornece dentro da tela.

![](../images/tutorials/create-schema/person_details_structure.png)

Esse mixin contribui com vários campos sob o nome de nível superior &quot;[!UICONTROL pessoa]&quot; com o tipo de dados &quot;[!UICONTROL Pessoa]&quot;. Este grupo de campos descreve informações sobre um indivíduo, incluindo nome, data de nascimento e sexo.

>[!NOTE]
>
>Lembre-se de que os campos podem usar tipos escalares (como string, integer, array ou data), bem como qualquer tipo de dados (um grupo de campos que representa um conceito comum) definido dentro do [!DNL Schema Registry].

Observe que o campo &quot;[!UICONTROL name]&quot; tem um tipo de dados de &quot;[!UICONTROL Full name]&quot;, o que significa que também descreve um conceito comum e contém subcampos relacionados ao nome, como nome, sobrenome, título de cortesia e sufixo.

Selecione os diferentes campos na tela para ver quaisquer campos adicionais que contribuem para a estrutura do schema.

## Adicionar outra mistura {#mixin-2}

Agora você pode repetir as mesmas etapas para adicionar outra mixin. Ao visualização da caixa de diálogo **[!UICONTROL Adicionar mistura]** desta vez, observe que a combinação &quot;Detalhes[!UICONTROL da pessoa do]Perfil&quot; está esmaecida e o botão de opção ao lado dela não pode ser selecionado. Isso evita que você duplique acidentalmente misturas que já foram incluídas no schema atual.

Agora é possível adicionar &quot;[!DNL Profile Personal Details" mixin] a partir da caixa de diálogo.

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

Depois de adicionada, a tela de desenho reaparece. &quot;Detalhes[!UICONTROL pessoais do]Perfil&quot; agora está listado em **[!UICONTROL Mixins]** na seção **[!UICONTROL Composição]** , e campos para endereço residencial, telefone celular e muito mais foram adicionados em **[!UICONTROL Estrutura]**.

Semelhante ao campo &quot;[!UICONTROL name]&quot;, os campos que você acabou de adicionar representam os conceitos de vários campos. Por exemplo, &quot;[!UICONTROL homeAddress]&quot; tem um tipo de dados de &quot;[!UICONTROL Address]&quot; e &quot;[!UICONTROL mobilePhone]&quot; tem um tipo de dados de &quot;Número[!UICONTROL de]telefone&quot;. Você pode selecionar cada um desses campos para expandi-los e ver os campos adicionais incluídos no tipo de dados.

![](../images/tutorials/create-schema/personal_details_structure.png)

## Definir uma nova mistura {#define-mixin}

O schema &quot;Membros[!UICONTROL de]fidelidade&quot; destina-se a capturar dados relacionados aos membros de um programa de fidelidade, para que sejam necessários alguns campos específicos relacionados à fidelidade. Não há combinações padrão disponíveis que contenham os campos necessários, portanto, será necessário definir uma nova mistura.

Desta vez, ao abrir a caixa de diálogo *[!UICONTROL Adicionar mistura]* , selecione **[!UICONTROL Criar nova mistura]**. Você será solicitado a fornecer um Nome **[!UICONTROL de]** exibição e uma **[!UICONTROL Descrição]** para sua combinação.

![](../images/tutorials/create-schema/mixin_create_new.png)

Assim como com os nomes de classe, o nome da mistura deve ser curto e simples, descrevendo o que a mistura contribuirá para o schema. Eles também são únicos, portanto, você não poderá reutilizar o nome e deve, portanto, garantir que seja suficientemente específico.

Para este tutorial, nomeie a nova combinação como &quot;Detalhes[!UICONTROL da]Fidelidade&quot;.

Selecione **[!UICONTROL Adicionar mistura]** para retornar ao [!DNL Schema Editor]. &quot;Detalhes[!UICONTROL da]fidelidade&quot; agora deve aparecer em **[!UICONTROL Mixins]** no lado esquerdo da tela, mas não há campos associados a ela ainda e, portanto, nenhum campo novo aparece em **[!UICONTROL Estrutura]**.

## Adicionar campos ao mixin {#mixin-fields}

Agora que você criou a combinação &quot;Detalhes[!UICONTROL da]Fidelidade&quot;, é hora de definir os campos que a combinação contribuirá para o schema.

Para começar, selecione o nome da mistura na seção **[!UICONTROL Misturas]** . Depois disso, as propriedades do mixin são exibidas no lado direito do editor e um botão **[!UICONTROL Adicionar campo]** é exibido ao lado do nome do schema em **[!UICONTROL Estrutura]**.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

Selecione **[!UICONTROL Adicionar campo]** ao lado de &quot;[!DNL Loyalty Members]&quot; para criar um novo nó na estrutura. Esse nó (chamado &quot;_locatárioId&quot; neste exemplo) representa a ID de locatário da organização IMS, precedida de um sublinhado. A presença da ID do locatário indica que os campos que você está adicionando estão contidos na namespace de sua organização.

Em outras palavras, os campos que você está adicionando são exclusivos à sua organização e serão salvos no [!DNL Schema Registry] em uma área específica acessível apenas à sua organização. Os campos que você definir devem ser sempre adicionados à namespace do locatário para evitar colisões com nomes de outras classes padrão, combinações, tipos de dados e campos.

Dentro desse nó com namespaces há um &quot;[!UICONTROL Novo campo]&quot;. Este é o início da mistura &quot;Detalhes[!UICONTROL da]Fidelidade&quot;.

![](../images/tutorials/create-schema/new_field_loyalty.png)

Usando os controles no lado direito do editor, start criando um campo &quot;[!DNL loyalty]&quot; com o tipo &quot;[!UICONTROL Objeto]&quot; que será usado para manter seus campos relacionados à fidelidade. Quando terminar, selecione **[!UICONTROL Aplicar]**.

![](../images/tutorials/create-schema/loyalty_object.png)

As alterações são aplicadas e o objeto &quot;[!DNL loyalty]&quot; recém-criado é exibido. Selecione **[!UICONTROL Adicionar campo]** ao lado do objeto para adicionar campos relacionados à fidelidade. Um &quot;[!UICONTROL Novo campo]&quot; é exibido e a seção Propriedades **[!UICONTROL do]** campo está visível no lado direito da tela.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

Cada campo requer as seguintes informações:

* **[!UICONTROL Nome]do campo:** O nome do campo, escrito em caso de camelo. Exemplo: leyaltyLevel
* **[!UICONTROL Nome]de exibição:** O nome do campo, escrito em caso de título. Exemplo: Nível de Fidelidade
* **[!UICONTROL Tipo]:** O tipo de dados do campo. Isso inclui tipos escalares básicos e quaisquer tipos de dados definidos no [!DNL Schema Registry]. Exemplos: [!UICONTROL string], [!UICONTROL integer], [!UICONTROL booleano], [!UICONTROL Pessoa], [!UICONTROL Endereço], Número de telefone, etc.
* **[!UICONTROL Descrição]:** Uma descrição opcional do campo deve ser incluída, escrita em caso de sentença, com um máximo de 200 caracteres.

O primeiro campo do [!DNL Loyalty] objeto será uma string chamada &quot;[!DNL loyaltyId]&quot;. Ao definir o tipo do novo campo como &quot;[!UICONTROL String]&quot;, a seção Propriedades **[!UICONTROL do]** campo é preenchida com várias opções para aplicar restrições, incluindo Valor **** padrão, **[!UICONTROL Formato]** e Comprimento **** máximo.

![](../images/tutorials/create-schema/string_constraints.png)

Diferentes opções de restrição estão disponíveis dependendo do tipo de dados selecionado. Como &quot;[!DNL loyaltyId]&quot; será um endereço de email, selecione &quot;[!UICONTROL email]&quot; no menu suspenso **[!UICONTROL Formato]** . Selecione **[!UICONTROL Aplicar]** para aplicar suas alterações.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## Adicionar mais campos ao mixin {#mixin-fields-2}

Agora que você adicionou o campo &quot;[!DNL loyaltyId]&quot;, é possível adicionar campos adicionais para capturar informações relacionadas à fidelidade, como:

* Pontos (número inteiro)
* Membro desde (data)

Cada campo é adicionado selecionando **[!UICONTROL Adicionar campo]** no objeto de fidelidade e preenchendo as informações necessárias.

Quando concluído, o objeto de Fidelidade conterá campos para ID de fidelidade, pontos e membro-a-partir.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## Adicionar um campo de enumeração ao mixin {#enum}

Ao definir campos no campo, [!DNL Schema Editor]há algumas opções adicionais que podem ser aplicadas a tipos de campos básicos para fornecer restrições adicionais aos dados que o campo pode conter. Os casos de uso para essas restrições são explicados na tabela a seguir:

| Restrição | Descrição |
| --- | --- |
| [!UICONTROL Obrigatório] | Indica que o campo é obrigatório para a ingestão de dados. Todos os dados carregados em um conjunto de dados com base nesse schema que não contém esse campo falharão após a ingestão. |
| [!UICONTROL Matriz] | Indica que o campo contém uma matriz de valores, cada um com o tipo de dados especificado. Por exemplo, usar essa restrição em um campo com um tipo de dados de &quot;[!UICONTROL String]&quot; especifica que o campo conterá uma matriz de strings. |
| [!UICONTROL Enum] | Indica que esse campo deve conter um dos valores de uma lista enumerada de valores possíveis. |
| [!UICONTROL Identidade] | Indica que este campo é um campo de identidade. Mais informações sobre campos de identidade são fornecidas [posteriormente neste tutorial](#identity-field). |
| [!UICONTROL Relação] | Embora as relações com os schemas possam ser inferidas com o uso do schema da união e [!DNL Real-time Customer Profile], isso se aplica somente aos schemas que compartilham a mesma classe. A restrição [!UICONTROL Relacionamento] indica que esse campo faz referência à identidade primária de um schema com base em uma classe diferente, o que implica uma relação entre os dois schemas. Consulte o tutorial sobre como [definir um relacionamento](./relationship-ui.md) para obter mais informações. |

Para este tutorial, o [!DNL "loyalty"] objeto no schema requer um novo campo enum que descreva o &quot;nível de fidelidade&quot; de um cliente, onde o valor pode ser apenas uma das quatro opções possíveis. Para adicionar esse campo ao schema, selecione **[!UICONTROL Adicionar campo]** ao lado do objeto &quot;[!DNL loyalty]&quot; e preencha os campos obrigatórios para nome **** de campo e nome **[!UICONTROL de]** exibição. Para **[!UICONTROL Tipo]**, selecione &quot;[!UICONTROL String]&quot;.

![](../images/tutorials/create-schema/loyalty-level-type.png)

Caixas de seleção adicionais aparecem para o campo depois que seu tipo é selecionado, incluindo caixas de seleção para **[!UICONTROL Matriz]**, **[!UICONTROL enumeração]** e **[!UICONTROL Identidade]**.

Marque a caixa de seleção **[!UICONTROL Enum]** para abrir a seção Valores **** Enum abaixo. Aqui, você pode inserir o **[!UICONTROL Valor]** (em camelCase) e o **[!UICONTROL Rótulo]** (um nome opcional e amigável para o leitor no Título Case) para cada nível de fidelidade aceitável.

Depois de concluir todas as propriedades do campo, selecione **[!UICONTROL Aplicar]** para adicionar o campo &quot;[!DNL loyaltyLevel]&quot; ao objeto &quot;[!DNL loyalty]&quot;.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

## Converter um objeto de vários campos em um tipo de dados {#datatype}

O objeto &quot;[!DNL loyalty]&quot; agora contém vários campos específicos de fidelidade e representa uma estrutura de dados comum que pode ser útil em outros schemas. O [!DNL Schema Editor] permite aplicar prontamente objetos de vários campos reutilizáveis, convertendo a estrutura desses objetos em tipos de dados.

Os tipos de dados permitem o uso consistente de estruturas de vários campos e proporcionam mais flexibilidade do que uma combinação, pois podem ser usados em qualquer lugar dentro de um schema. Isso é feito configurando o valor **[!UICONTROL Tipo]** do campo para o valor de qualquer tipo de dados definido no [!DNL Schema Registry].

Para converter o objeto &quot;[!DNL loyalty]&quot; em um tipo de dados, selecione o campo &quot;[!DNL loyalty]&quot; em **[!UICONTROL Estrutura]** e, em seguida, selecione **[!UICONTROL Converter em novo tipo]** de dados no lado direito do editor em Propriedades **[!UICONTROL de]** campo. Uma janela verde é exibida, confirmando que o objeto foi convertido com êxito.

![](../images/tutorials/create-schema/convert-data-type.png)

Agora, quando você olha em **[!UICONTROL Estrutura]**, você pode ver que o campo &quot;[!DNL loyalty]&quot; tem um tipo de dados &quot;[!DNL Loyalty]&quot; e os campos têm pequenos ícones de bloqueio ao seu lado, indicando que não são mais campos individuais, mas sim parte de um tipo de dados de vários campos.

![](../images/tutorials/create-schema/loyalty_data_type.png)

Em um schema futuro, agora é possível atribuir um campo ao **[!UICONTROL Tipo]** de &quot;[!DNL Loyalty]&quot; e ele incluirá automaticamente campos para ID, nível de fidelidade, membro desde e pontos.

## Definir um campo de schema como um campo de identidade {#identity-field}

A estrutura de dados padrão que os schemas fornecem pode ser aproveitada para identificar dados pertencentes ao mesmo indivíduo em várias fontes, permitindo vários casos de uso downstream, como segmentação, relatórios, análise de ciência de dados e muito mais. Para unir dados com base em identidades individuais, os campos principais devem ser marcados como campos de &quot;[!UICONTROL Identidade]&quot; nos schemas aplicáveis.

[!DNL Experience Platform] facilita a identificação de um campo de identidade através do uso de uma caixa de seleção **[!UICONTROL Identidade]** no [!DNL Schema Editor]. No entanto, você deve determinar qual campo é o melhor candidato a usar como uma identidade, com base na natureza de seus dados.

Por exemplo, pode haver milhares de membros do programa de fidelidade pertencentes ao mesmo &quot;nível de fidelidade&quot;, mas cada membro do programa de fidelidade tem um &quot;[!DNL loyaltyId]&quot; exclusivo (que, neste caso, é o endereço de email do membro individual). O fato de que &quot;[!DNL loyaltyId]&quot; é um identificador exclusivo para cada membro faz dele um bom candidato para um campo de identidade, ao passo que &quot;nível de fidelidade&quot; não é.

>[!IMPORTANT]
>
>As etapas descritas abaixo abordam como adicionar um descritor de identidade a um campo de schema existente. Como alternativa à definição de campos de identidade na estrutura do próprio schema, também é possível usar um `identityMap` campo para conter informações de identidade.
>
>Se você planeja usar `identityMap`, lembre-se de que isso substituirá qualquer identidade primária adicionada ao schema diretamente. Consulte a seção sobre `identityMap` as [noções básicas do guia](../schema/composition.md#identityMap) de composição do schema para obter mais informações.

Na seção **[!UICONTROL Estrutura]** do editor, selecione o campo &quot;[!DNL loyaltyId]&quot; e a caixa de seleção **[!UICONTROL Identidade]** aparecerá em Propriedades **** de campo. Marque a caixa e a opção para definir isso como a Identidade **** principal será exibida. Selecione essa caixa também.

Em seguida, você deve fornecer uma Namespace **[!UICONTROL de]** identidade da lista de namespaces predefinidas na lista suspensa. Como &quot;[!DNL loyaltyId]&quot; é o endereço de email do cliente, selecione &quot;[!UICONTROL Email]&quot; na lista suspensa. Selecione **[!UICONTROL Aplicar]** para confirmar as atualizações do campo &quot;[!DNL loyaltyId]&quot;.

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>Para obter uma lista de namespaces padrão e suas definições, consulte a documentação [do Serviço de](../../identity-service/troubleshooting-guide.md#standard-namespaces)identidade.

Agora, todos os dados ingeridos no campo &quot;[!DNL loyaltyId]&quot; serão usados para ajudar a identificar esse indivíduo e unir uma única visualização do cliente.

>[!NOTE]
>
>Depois que um campo de schema for definido como a identidade primária, você receberá uma mensagem de erro se tentar definir outro campo no schema como principal. Cada schema pode conter apenas um campo de identidade principal.

Para saber mais sobre como trabalhar com identidades no, consulte a documentação do [!DNL Experience Platform][!DNL Identity Service] [](../../identity-service/home.md) .

## Ative o schema para uso em [!DNL Real-time Customer Profile] {#profile}

[O [!DNL Real-time Customer Perfil]](../../profile/home.md) aproveita os dados de identidade [!DNL Experience Platform] para fornecer uma visualização holística de cada cliente individual. O serviço cria perfis robustos, 360°, de atributos do cliente, bem como contas com carimbos de data e hora de cada interação que os clientes tiveram em qualquer sistema integrado com [!DNL Experience Platform].

Para que um schema seja habilitado para uso com [!DNL Real-time Customer Profile], ele deve ter uma identidade primária definida. Você receberá uma mensagem de erro se tentar ativar um schema sem primeiro definir uma identidade primária.

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

Para ativar o schema &quot;Membros de Fidelidade&quot; para uso em [!DNL Profile], comece selecionando &quot;[!DNL Loyalty Members]&quot; na seção **[!UICONTROL Estrutura]** do editor.

No lado direito do editor, são mostradas informações sobre o schema, incluindo seu nome de exibição, descrição e tipo. Além dessas informações, há um botão de alternância de **[!UICONTROL Perfil]** .

![](../images/tutorials/create-schema/profile-toggle.png)

Selecione **[!UICONTROL Perfil]** e um  será exibido, solicitando que você confirme que deseja ativar o schema para [!DNL Profile].

![](../images/tutorials/create-schema/enable-profile.png)

>[!WARNING]
>
>Depois que um schema é ativado para [!DNL Real-time Customer Profile] e salvo, ele não pode ser desativado.

Selecione **[!UICONTROL Ativar]** para confirmar sua escolha. Se desejar, você pode selecionar a alternância do **[!UICONTROL Perfil]** para desativar o schema, mas depois que o schema for salvo enquanto [!DNL Profile] estiver ativado, ele não poderá mais ser desativado.

## Próximos passos e recursos adicionais

Agora que você terminou de compor um schema &quot;Membros da Fidelidade&quot;, você pode ver o schema completo na tela. Selecione **[!UICONTROL Salvar]** e o schema será salvo no [!DNL Schema Library], tornando-o acessível pelo [!DNL Schema Registry].

Seu novo schema agora pode ser usado para assimilar dados em [!DNL Platform]. Lembre-se de que, uma vez que o schema tenha sido usado para ingerir dados, somente alterações aditivas poderão ser feitas. Consulte as [noções básicas da composição](../schema/composition.md) do schema para obter mais informações sobre o controle de versão do schema.

Agora você pode seguir o tutorial sobre como [definir uma relação de schema na interface do usuário](./relationship-ui.md) para adicionar um novo campo de relação ao schema &quot;Membros da fidelidade&quot;.

O schema &quot;Membros da fidelidade&quot; também está disponível para exibição e gerenciamento usando a [!DNL Schema Registry] API. Para começar a trabalhar com a API, leia o guia [[!DNL Schema Registry API] do](../api/getting-started.md)desenvolvedor para obter mais informações.

### Recursos de vídeo

>[!WARNING]
>
>A [!DNL Platform] interface do usuário exibida nos vídeos a seguir está desatualizada. Consulte a documentação acima para obter as capturas de tela e a funcionalidade mais recentes da interface do usuário.

O vídeo a seguir mostra como criar um schema simples na [!DNL Platform] interface do usuário.

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

O vídeo a seguir destina-se a reforçar sua compreensão sobre como trabalhar com mixins e classes.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## Apêndice

As seções a seguir fornecem informações adicionais sobre o uso do [!DNL Schema Editor].

### Create a new class {#create-new-class}

[!DNL Experience Platform] fornece a flexibilidade para definir um schema com base em uma classe exclusiva de sua organização.

Na área de trabalho **[!UICONTROL Schemas]** , selecione **[!UICONTROL Criar schema]** e, em seguida, selecione **[!UICONTROL Procurar]** na lista suspensa.

![](../images/tutorials/create-schema/browse-classes.png)

Uma caixa de diálogo é exibida permitindo que você selecione uma lista de classes disponíveis. Na parte superior da caixa de diálogo, selecione **[!UICONTROL Criar nova classe]**. Em seguida, você pode atribuir a sua nova classe um Nome **[!UICONTROL de]** exibição (um nome curto, descritivo, exclusivo e fácil de usar para a classe), uma **[!UICONTROL Descrição]** e um **[!UICONTROL Comportamento]** (&quot;[!UICONTROL Registro]&quot; ou &quot;Sériecronológica&quot;) para os dados que o schema definirá.

![](../images/tutorials/create-schema/create_new_class.png)

>[!IMPORTANT]
>
>Ao criar um schema que implemente uma classe definida pela sua organização, lembre-se de que as combinações estão disponíveis para uso somente com classes compatíveis. Como a classe definida é nova, não há combinações compatíveis listadas na caixa de diálogo *Adicionar mistura* . Em vez disso, será necessário selecionar **[!UICONTROL Criar nova mistura]** e definir uma mistura para uso com essa classe. Na próxima vez que você redigir um schema que implementa a nova classe, a combinação definida será listada e estará disponível para uso.

### Alterar a classe de um schema {#change-class}

É possível alterar a classe de um schema em qualquer ponto durante o processo de composição inicial antes que o schema seja salvo.

>[!WARNING]
>
>A reatribuição da classe para um schema deve ser feita com extrema cautela. Misturas são compatíveis somente com certas classes, e, portanto, alterar a classe redefinirá a tela de desenho e quaisquer campos adicionados.

Para reatribuir uma classe, selecione **[!UICONTROL Atribuir]** no lado esquerdo da tela.

![](../images/tutorials/create-schema/assign_class_button.png)

Uma caixa de diálogo é exibida mostrando uma lista de todas as classes disponíveis, incluindo qualquer classe definida por sua organização (o proprietário sendo &quot;[!UICONTROL Cliente]&quot;), bem como as classes padrão definidas pelo Adobe.

Selecione uma classe na lista para exibir sua descrição no lado direito da caixa de diálogo. Você também pode selecionar Estrutura **[!UICONTROL de classe de]** Pré-visualização para ver os campos e metadados associados à classe. Selecione **[!UICONTROL Atribuir classe]** para continuar.

![](../images/tutorials/create-schema/assign_class.png)

Uma nova caixa de diálogo é aberta solicitando que você confirme que deseja atribuir uma nova classe. Selecione **[!UICONTROL Atribuir]** para confirmar.

![](../images/tutorials/create-schema/assign-confirm.png)

Após confirmar a alteração de classe, a tela será redefinida e todo o progresso da composição será perdido.