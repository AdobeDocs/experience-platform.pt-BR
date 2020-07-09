---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um esquema usando o Editor de esquemas.
topic: tutorials
translation-type: tm+mt
source-git-commit: d55dc9776968099901325c58506c5e322449368e
workflow-type: tm+mt
source-wordcount: '3462'
ht-degree: 0%

---


# Criar um esquema usando o Editor de esquemas.

O Registro do Schema fornece uma interface de usuário e uma RESTful API a partir da qual você pode visualização e gerenciar todos os recursos na Biblioteca de Schemas do Adobe Experience Platform. A Biblioteca de Schemas contém recursos disponibilizados pela Adobe, parceiros de Experience Platform e fornecedores cujos aplicativos você usa, bem como recursos que você define e salva no Registro de Schemas.

Este tutorial aborda as etapas para a criação de um schema usando o Editor de Schemas no Experience Platform. Se você preferir compor um schema usando a API do Registro do Schema, comece lendo o guia [do desenvolvedor do Registro do](../api/getting-started.md) Schema antes de tentar que o tutorial [crie um schema usando a API](create-schema-api.md).

Este tutorial também inclui etapas para [definir uma nova classe](#create-new-class) que você poderia usar para compor um schema.

## Introdução

Este tutorial requer uma compreensão funcional dos vários aspectos do Adobe Experience Platform envolvido no uso do Editor de Schemas. Antes de iniciar este tutorial, reveja a documentação para obter os seguintes conceitos:

* [Modelo de dados de experiência (XDM)](../home.md): A estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.
* [Noções básicas da composição](../schema/composition.md)do schema: Uma visão geral dos schemas XDM e seus blocos de construção, incluindo classes, misturas, tipos de dados e campos.
* [Perfil](../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Este tutorial requer que você tenha acesso ao Experience Platform. Se você não tiver acesso a uma Organização IMS no Experience Platform, fale com o administrador do sistema antes de prosseguir.

## Procurar schemas existentes na área de trabalho Schemas {#browse}

A área de trabalho Schema fornece uma visualização da Biblioteca de Schemas, permitindo que você visualização e gerencie todos os schemas disponíveis para você, bem como componha novos. A área de trabalho também inclui o Editor de Schemas, a tela na qual você irá compor um schema neste tutorial.

Depois de fazer logon no Experience Platform, clique em **Schemas** na navegação à esquerda e você será direcionado para a área de trabalho de Schemas. Você verá uma lista de schemas (uma representação da Biblioteca de Schemas) onde poderá visualização, gerenciar e personalizar todos os schemas disponíveis. A lista inclui o nome, o tipo, a classe e o comportamento (registro ou série de tempo) em que o schema se baseia, bem como a data e a hora em que o schema foi modificado pela última vez.

Clique no ícone de filtro ao lado da barra Pesquisar para usar os recursos de filtragem para todos os recursos no registro, incluindo classes, mixins e tipos de dados.

![Visualização da biblioteca de Schemas](../images/tutorials/create-schema/schemas_filter.png)

## Criar e nomear um schema {#create}

Para começar a compor um schema, clique em **Criar Schema** no canto superior direito da área de trabalho dos Schemas.

![Botão Criar Schema](../images/tutorials/create-schema/create_schema_button.png)

O Editor *de Schemas* é exibido. Esta é a tela sobre a qual você irá compor seu schema. Quando você chega ao editor, um &quot;Schema sem título&quot; na seção *Estrutura* da tela é automaticamente criado para que você comece a personalizar.

![Editor de Schemas](../images/tutorials/create-schema/schema_editor.png)

No lado direito do editor estão Propriedades *do* Schema, onde é possível fornecer um nome para o schema (usando o campo Nome **de** exibição). Depois que um nome é inserido, a tela é atualizada para refletir o novo nome do schema.

![Tela do Schema](../images/tutorials/create-schema/name_schema.png)

Há várias considerações importantes a serem feitas ao decidir um nome para o seu schema:

* Os nomes de Schemas devem ser curtos e descritivos para que o schema possa ser facilmente encontrado na biblioteca posteriormente.
* Os nomes dos Schemas devem ser exclusivos, o que significa que também devem ser específicos o suficiente para que não sejam reutilizados no futuro. Por exemplo, se sua organização tivesse programas de fidelidade separados para diferentes marcas, seria aconselhável nomear seu schema como &quot;Membros de fidelidade da Marca A&quot; para facilitar a distinção entre outros schemas relacionados à fidelidade que você possa definir posteriormente.
* Como opção, você pode fornecer informações adicionais sobre o schema usando o campo **Descrição** .

Este tutorial compõe um schema para assimilar dados relacionados aos membros de um programa de fidelidade, portanto, o schema é denominado &quot;Membros de fidelidade&quot;.

## Atribuir uma classe {#class}

No lado esquerdo do editor está a seção *Composição* . Atualmente, contém duas subseções: *Schema* e *classe*.

Agora que o schema tem um nome, é hora de atribuir a classe que o schema implementará. Clique em **Atribuir** ao lado de *Classe*.

![](../images/tutorials/create-schema/assign_class_button.png)

A caixa de diálogo *Atribuir classe* é exibida. Esta janela exibe uma lista de todas as classes disponíveis, incluindo qualquer classe definida por sua organização (o proprietário sendo &quot;Cliente&quot;), bem como as classes padrão definidas pela Adobe.

Clique no nome da classe para exibir a descrição da classe. Você também pode optar por **Pré-visualização da estrutura** de classe para ver os campos e os metadados associados à classe.

Este tutorial usa a classe de Perfil individual XDM. Clique no botão de opção ao lado da classe para selecioná-la e clique em **Atribuir classe**.

![Caixa de diálogo Atribuir classe](../images/tutorials/create-schema/assign_class.png)

A tela reaparece. A seção *Classe* agora contém a classe selecionada (Perfil individual XDM) e os campos contribuídos pela classe Perfil individual XDM agora são visíveis na seção *Estrutura* .

![Classe de Perfil Individual XDM Atribuída](../images/tutorials/create-schema/class_assigned_structure.png)

Os campos aparecem no formato &quot;fieldName | Tipo de dados&quot;. As etapas para definir campos de schema na interface do usuário são fornecidas posteriormente neste tutorial.

>[!NOTE]
>
>Você pode [alterar a classe de um schema](#change-class) em qualquer ponto durante o processo de composição inicial antes que o schema seja salvo, mas isso deve ser feito com extrema cautela. Misturas são compatíveis somente com certas classes, portanto, alterar a classe redefinirá a tela de desenho e quaisquer campos adicionados.

## Adicionar uma mistura {#mixin}

Agora que uma classe foi atribuída, a seção *Composição* contém uma terceira subseção: *Misturas*.

Agora você pode começar a adicionar campos ao seu schema adicionando mixins. Uma combinação é um grupo de um ou mais campos que descrevem um conceito específico. Este tutorial usa mixins para descrever os membros do programa de fidelidade e capturar informações-chave como nome, aniversário, número de telefone, endereço e muito mais.

Para adicionar uma mistura, clique em **Adicionar** na subseção *Misturas* .

![](../images/tutorials/create-schema/add_mixin_button.png)

A caixa de diálogo *Adicionar mistura* é exibida. As misturas só se destinam ao uso com classes específicas, portanto, a lista de misturas mostra somente aquelas compatíveis com a classe selecionada (neste caso, a classe Perfil individual XDM).

Selecionar o botão de opção ao lado de uma combinação lhe dará a opção de **Pré-visualização da estrutura** de mistura. Selecione a combinação &quot;Detalhes da pessoa do Perfil&quot; e clique em **Adicionar combinação**.

![](../images/tutorials/create-schema/add_mixin_person_details.png)

A tela do schema é exibida novamente. A seção *Misturas* agora lista a combinação &quot;Detalhes da pessoa do Perfil&quot; e a seção *Estrutura* inclui os campos contribuídos pela mistura.

![](../images/tutorials/create-schema/person_details_structure.png)

Esse mixin contribui com vários campos sob o nome de nível superior &quot;pessoa&quot; com o tipo de dados &quot;Pessoa&quot;. Este grupo de campos descreve informações sobre um indivíduo, incluindo nome, data de nascimento e sexo.

>[!NOTE]
>
>Lembre-se de que os campos podem usar tipos escalares (como string, integer, array ou data) como seu tipo de dados, bem como qualquer &quot;tipo de dados&quot; (um grupo de campos que representa um conceito comum) no Registro do Schema.

Observe que o campo &quot;nome&quot; tem um tipo de dados de &quot;Nome da pessoa&quot;, o que significa que também descreve um conceito comum e contém subcampos relacionados ao nome, como nome, sobrenome e nome completo.

Clique em diferentes campos na tela para ver quaisquer campos adicionais que contribuem para a estrutura do schema.

## Adicionar outra mistura {#mixin-2}

Agora você pode repetir as mesmas etapas para adicionar outra mixin. Ao visualização da caixa de diálogo *Adicionar mistura* desta vez, observe que a mistura &quot;Detalhes da pessoa do Perfil&quot; está esmaecida e o botão de opção ao lado dela não pode ser selecionado. Isso evita que você duplique acidentalmente misturas que já foram incluídas no schema atual.

Agora você pode adicionar a combinação &quot;Detalhes pessoais do Perfil&quot; na caixa de diálogo *Adicionar combinação* .

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

Depois de adicionada, a tela de desenho reaparece. Os &quot;Detalhes pessoais do Perfil&quot; agora estão listados em *Mixins* na seção *Composição* , e os campos para endereço residencial, telefone celular e muito mais foram adicionados em *Estrutura*.

Semelhante ao campo &quot;nome&quot;, os campos que você acabou de adicionar representam os conceitos de vários campos. Por exemplo, &quot;homeAddress&quot; tem um tipo de dados de &quot;Address&quot; e &quot;mobilePhone&quot; tem um tipo de dados de &quot;Número de telefone&quot;. Você pode clicar em cada um desses campos para expandi-los e ver os campos adicionais incluídos no tipo de dados.

![](../images/tutorials/create-schema/personal_details_structure.png)

## Definir uma nova mistura {#define-mixin}

O schema &quot;Membros de Fidelidade&quot; destina-se a capturar dados relacionados aos membros de um programa de fidelidade, de modo que serão necessários alguns campos específicos relacionados à fidelidade. Não há combinações padrão disponíveis que contenham os campos necessários, portanto, será necessário definir uma nova mistura.

Desta vez, ao abrir a caixa de diálogo *Adicionar mistura* , selecione **Criar nova mistura**. Você será solicitado a fornecer um Nome **de** exibição e uma **Descrição** para sua combinação.

![](../images/tutorials/create-schema/mixin_create_new.png)

Assim como com os nomes de classe, o nome da mistura deve ser curto e simples, descrevendo o que a mistura contribuirá para o schema. Eles também são únicos, portanto, você não poderá reutilizar o nome e deve, portanto, garantir que seja suficientemente específico.

Para este tutorial, nomeie a nova combinação como &quot;Detalhes da fidelidade&quot;.

Clique em **Adicionar mistura** para retornar ao editor de schemas. Os &quot;Detalhes de fidelidade&quot; agora devem aparecer em *Mixins* no lado esquerdo da tela, mas não há campos associados a ela ainda e, portanto, nenhum campo novo aparece em *Estrutura*.

## Adicionar campos ao mixin {#mixin-fields}

Agora que você criou a combinação &quot;Detalhes da Fidelidade&quot;, é hora de definir os campos que a combinação contribuirá para o schema.

Para começar, clique no nome da mistura na seção *Misturas* . Assim que você fizer isso, as Propriedades *de* combinação aparecerão no lado direito do editor e um botão **Adicionar campo** aparecerá ao lado do nome do schema em *Estrutura*.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

Clique em **Adicionar campo** ao lado de &quot;Membros de fidelidade&quot; para criar um novo nó na estrutura. Esse nó (chamado &quot;_locatárioId&quot; neste exemplo) representa a ID de locatário da organização IMS, precedida de um sublinhado. A presença da ID do locatário indica que os campos que você está adicionando estão contidos na namespace de sua organização.

Em outras palavras, os campos que você está adicionando são exclusivos à sua organização e serão salvos no Registro do Schema em uma área específica acessível apenas à sua Organização IMS. Os campos definidos devem ser sempre adicionados à namespace para evitar colisões com nomes de outras classes padrão, misturas, tipos de dados e campos.

Dentro desse nó com namespaces há um &quot;Novo campo&quot;. Este é o começo da mistura &quot;Detalhes da Fidelidade&quot;.

![](../images/tutorials/create-schema/new_field_loyalty.png)

Usando Propriedades *de* campo no lado direito do editor, crie um campo de &quot;fidelidade&quot; com o tipo &quot;Objeto&quot; que será usado para manter seus campos relacionados à fidelidade. Quando terminar, clique em **Aplicar**.

![](../images/tutorials/create-schema/loyalty_object.png)

As alterações são aplicadas e o objeto de &quot;fidelidade&quot; recém-criado é exibido. Clique em **Adicionar campo** ao lado do objeto para adicionar outros campos relacionados à fidelidade. Um &quot;Novo campo&quot; é exibido e a seção Propriedades *do* campo é visível no lado direito da tela.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

Cada campo requer as seguintes informações:

* **Nome do campo:** O nome do campo, escrito em caso de camelo. Exemplo: leyaltyLevel
* **Nome de exibição:** O nome do campo, escrito em caso de título. Exemplo: Nível de Fidelidade
* **Tipo:** O tipo de dados do campo. Isso inclui tipos escalares básicos e quaisquer tipos de dados definidos no Registro do Schema. Exemplos: string, integer, booleano, Pessoa, Endereço, Número de telefone etc.
* **Descrição:** Uma descrição opcional do campo deve ser incluída, escrita em caso de sentença. (máximo de 200 caracteres)

O primeiro campo para o objeto Loyalty será uma string chamada &quot;loyaltyId&quot;. Ao definir o tipo do novo campo como &quot;String&quot;, a janela Propriedades *do* campo é preenchida com várias opções para aplicar restrições, incluindo Valor **** padrão, **Formato** e Comprimento **** máximo.

![](../images/tutorials/create-schema/string_constraints.png)

Diferentes opções de restrição estão disponíveis dependendo do tipo de dados selecionado. Como &quot;loyaltyId&quot; será um endereço de email, selecione &quot;email&quot; no menu suspenso **Formato** . Selecione **Aplicar** para aplicar suas alterações.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## Adicionar mais campos para mixagem {#mixin-fields-2}

Agora que você adicionou o campo &quot;loyaltyId&quot;, é possível adicionar campos adicionais para capturar informações relacionadas à fidelidade, como:

* Pontos (Inteiro)
* Membro Desde (Data)

Cada campo é adicionado clicando em **Adicionar campo** no objeto de fidelidade e preenchendo as informações necessárias.

Quando concluído, o objeto Fidelidade conterá campos para: ID de Fidelidade, Pontos e Membro Desde.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## Adicionar campo &#39;enum&#39; para mixagem {#enum}

Ao definir campos no Editor de Schemas, há algumas opções adicionais que podem ser aplicadas a tipos de campos básicos para fornecer restrições adicionais aos dados que o campo pode conter.

Um exemplo disso seria um campo &quot;Nível de Fidelidade&quot;, onde o valor pode ser apenas uma das quatro opções possíveis. Para adicionar esse campo ao schema, clique em **Adicionar campo** ao lado do objeto &quot;fidelidade&quot; e preencha os campos obrigatórios em Propriedades *do* campo.

Para **Tipo**, selecione &quot;String&quot; e você verá caixas de seleção adicionais exibidas para **Matriz**, **enumeração** e **identidade**.

Marque a caixa de seleção **Enum** para abrir a seção Valores *de* enumeração abaixo. Aqui, você pode inserir o **Valor** (em camelCase) e o **Rótulo** (um nome opcional e amigável para o leitor no Título Case) para cada nível de fidelidade aceitável.

Depois de concluir todas as propriedades do campo, clique em **Aplicar** e o campo &quot;fidelidadeNível&quot; será adicionado ao objeto &quot;fidelidade&quot;.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

Mais informações sobre restrições adicionais disponíveis:

* **Obrigatório:** Indica que o campo é obrigatório para a ingestão de dados. Todos os dados carregados em um conjunto de dados com base nesse schema que não contém esse campo falharão após a ingestão.
* **Matriz:** Indica que o campo contém uma matriz de valores, cada um com o tipo de dados especificado. Por exemplo, selecionar um tipo de dados de &quot;String&quot; e marcar a caixa de seleção &quot;Array&quot; significa que o campo conterá uma matriz de strings.
* **Enum:** Indica que esse campo deve conter um dos valores de uma lista enumerada de valores possíveis.
* **Identidade:** Indica que este campo é um campo de identidade. Mais informações sobre campos de identidade são fornecidas [posteriormente neste tutorial](#identity-field).

## Converter um objeto de vários campos em um tipo de dados {#datatype}

Depois de adicionar vários campos específicos de fidelidade, o objeto &quot;fidelidade&quot; agora contém uma estrutura de dados comum que pode ser útil em outros schemas.

Quando você sente que uma estrutura de vários campos pode ser reutilizável e gostaria de ter a flexibilidade para usar essa mesma estrutura de dados em outro lugar, o Editor de Schemas possibilita a conversão dessa estrutura em um tipo de dados.

Os tipos de dados permitem o uso consistente de estruturas de vários campos e proporcionam mais flexibilidade do que uma combinação, pois podem ser usados em qualquer lugar dentro de um schema. Isso é feito configurando o **Tipo** de um campo em uma combinação para qualquer tipo de dados definido no registro.

Para converter o objeto &quot;fidelidade&quot; em um tipo de dados, clique no campo &quot;fidelidade&quot; em *Estrutura* e selecione **Converter em novo tipo** de dados no lado direito do editor em Propriedades *de* campo. Um pequeno pop-up verde é exibido confirmando &quot;Objeto convertido em tipo de dados&quot;.

Agora, quando você olha em *Estrutura*, você pode ver que o campo &quot;fidelidade&quot; tem um tipo de dados de &quot;Fidelidade&quot; e os campos têm pequenos ícones de cadeado ao lado deles, indicando que não são mais campos individuais, mas sim parte de uma estrutura de vários campos.

Em um schema futuro, agora é possível atribuir a um campo o **Tipo** de &quot;Fidelidade&quot; e ele incluirá automaticamente os campos Nível de Fidelidade, Pontos, Desde Membro e ID de Fidelidade.

![](../images/tutorials/create-schema/loyalty_data_type.png)

## Definir um campo de schema como um campo de identidade {#identity-field}

Schemas são usados para ingerir dados no Experience Platform, e esses dados são usados para identificar indivíduos e unir informações provenientes de várias fontes. Para ajudar nesse processo, os campos principais podem ser marcados como campos &quot;Identidade&quot;.

O Experience Platform facilita a identificação de um campo de identidade através do uso de uma caixa de seleção **Identidade** no Editor de Schemas.

Por exemplo, pode haver milhares de membros do programa de fidelidade pertencentes ao mesmo &quot;nível&quot;, mas cada membro do programa de fidelidade tem uma &quot;loyaltyId&quot; exclusiva (que, neste caso, é o endereço de email do membro individual). O fato de &quot;loyaltyId&quot; ser um identificador exclusivo para cada membro faz dele um bom candidato para um campo de identidade, enquanto &quot;level&quot; não é.

Na seção *Estrutura* do editor, clique no campo &quot;loyaltyId&quot; que você criou e você verá a caixa de seleção **Identity** aparecer em Propriedades *de* campo. Marque a caixa e você terá a opção de definir isso como a Identidade **** principal. Marque essa caixa também.

Em seguida, você deve fornecer um Nome **de identidade**. Existem várias namespaces predefinidas, mas como &quot;loyaltyId&quot; é o endereço de email do membro, selecione &quot;Email&quot; na lista suspensa. Agora você pode clicar em **Aplicar** para confirmar as atualizações do campo &quot;idelityId&quot;.

Agora, todos os dados ingeridos no campo &quot;leyaltyId&quot; serão usados para ajudar a identificar esse indivíduo e unir uma única visualização do cliente.

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>Depois que um campo de schema for definido como a identidade primária, você receberá uma mensagem de erro se tentar definir outro campo no schema como principal. Cada schema pode conter apenas um campo de identidade principal.

Para saber mais sobre como trabalhar com identidades, consulte a documentação do Serviço [de](../../identity-service/home.md) identidade.

<!-- ## Relationship

Schemas define a static view of a concept, but do not provide specific details on how data based on these schemas (datasets, etc) may relate to one another. Adobe Experience Platform allows you to describe these relationships through the **Relationship** checkbox in the schema editor. 

In order to define a relationship, click on the field and check the **Relationship** checkbox on the right-side of the canvas. 

![](../images/tutorials/create-schema/relationship.png)

More information about relationships and other schema metadata can be found in the [Schema Registry API Developer Guide](../schema_registry_developer_guide.md). -->

## Ative o schema para uso no Perfil do cliente em tempo real {#profile}

O Editor de Schemas fornece a capacidade de habilitar um schema para uso com o Perfil [Cliente em tempo](../../profile/home.md)real. O Perfil fornece uma visualização holística de cada cliente individual, criando um perfil robusto de 360° dos atributos do cliente, bem como uma conta com carimbo de data e hora de cada interação que o cliente teve em qualquer sistema integrado ao Experience Platform.

Para que um schema seja habilitado para uso com o Perfil de cliente em tempo real, ele deve ter uma identidade primária definida. Você receberá uma mensagem de erro &quot;Missing Primary Identity&quot; (Identidade primária ausente) se tentar habilitar um schema sem primeiro definir uma identidade primária.

![](../images/tutorials/create-schema/missing_primary_identity.png)

Para ativar o schema &quot;Membros da Fidelidade&quot; para uso no Perfil, comece clicando em &quot;Membros da Fidelidade&quot; na seção *Estrutura* do editor.

No lado direito do editor, em Propriedades *do* Schema, são mostradas informações sobre o schema, incluindo seu nome de exibição, descrição e tipo. Além dessas informações, há um botão de alternância intitulado **Perfil**.

![](../images/tutorials/create-schema/unified_profile_toggle.png)

Clique em **Perfil** e um pop-up será exibido, solicitando que você confirme que deseja ativar o schema para Perfil.

![](../images/tutorials/create-schema/enable_unified_profile.png)

>[!NOTE]
>
>Uma vez que um schema tenha sido ativado para Perfil do cliente em tempo real e salvo, ele não poderá ser desativado.

## Próximos passos e recursos adicionais

Agora que você terminou de compor um schema de &quot;Membros da Fidelidade&quot;, você pode ver o schema completo na seção *Estrutura* do editor. Clique em **Salvar** e o schema será salvo na Biblioteca de Schemas, tornando-o acessível pelo Registro de Schemas.

Seu novo schema agora pode ser usado para assimilar dados no Platform. Lembre-se de que, uma vez que o schema tenha sido usado para ingerir dados, somente alterações aditivas poderão ser feitas. Consulte as [noções básicas da composição](../schema/composition.md) do schema para obter mais informações sobre o controle de versão do schema.

O schema &quot;Membros da fidelidade&quot; também está disponível para exibição e gerenciamento usando a API do Registro do Schema. Para começar a trabalhar com a API, leia o guia [do desenvolvedor da API do Registro do](../api/getting-started.md)Schema.

>[!WARNING]
>
>A [!DNL Platform] interface do usuário exibida nos vídeos a seguir está desatualizada. Consulte a documentação acima para obter as capturas de tela e a funcionalidade mais recentes da interface do usuário.

O vídeo a seguir mostra como criar um schema simples na [!DNL Platform] interface do usuário.

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

O vídeo a seguir destina-se a reforçar sua compreensão sobre como trabalhar com mixins e classes.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## Apêndice

As informações a seguir são complementares ao Tutorial do Editor de Schemas.

### Create a new class {#create-new-class}

O Experience Platform oferece a flexibilidade para definir um schema com base em uma classe exclusiva de sua organização.

Abra a caixa de diálogo *Atribuir classe* clicando em **Atribuir** na seção *Classe* do Editor de Schemas. Na caixa de diálogo, selecione **Criar nova classe**.

Em seguida, você pode atribuir a sua nova classe um Nome **de** exibição (um nome curto, descritivo, exclusivo e amigável para a classe), uma **Descrição** e um **Comportamento** (&quot;Registro&quot; ou &quot;Série de tempo&quot;) para os dados que o schema definirá.

![Detalhes da nova classe](../images/tutorials/create-schema/create_new_class.png)

>[!NOTE]
>
>Ao criar um schema que implemente uma classe definida pela sua organização, lembre-se de que as combinações estão disponíveis para uso somente com classes compatíveis. Como a classe definida é nova, não há combinações compatíveis listadas na caixa de diálogo *Adicionar mistura* . Em vez disso, será necessário selecionar **Criar nova mistura** e definir uma mistura para uso com essa classe. Na próxima vez que você redigir um schema que implementa a nova classe, a combinação definida será listada e estará disponível para uso.

### Alterar a classe de um schema {#change-class}

A qualquer momento durante o processo inicial de composição do schema, antes de o schema ser salvo, é possível alterar a classe na qual o schema se baseia.

>[!WARNING]
>
>Tenha cuidado antes de mudar de classe. Misturas são compatíveis apenas com certas classes, portanto, alterar a classe redefine a tela e remove quaisquer campos adicionados a esse ponto.

Para alterar a classe, clique em **Atribuir** ao lado de *Classe* na seção *Composição* do editor.

Quando a caixa de diálogo *Atribuir classe* é aberta, você pode escolher uma nova classe na lista disponível. Clique em **Atribuir classe** e uma nova caixa de diálogo será aberta solicitando que você confirme que deseja atribuir uma nova classe.

![Alterar classe](../images/tutorials/create-schema/assign_new_class_warning.png)

Se você confirmar a alteração da classe, a tela será redefinida e todo o progresso da composição será perdido.