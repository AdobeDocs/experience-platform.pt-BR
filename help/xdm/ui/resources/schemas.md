---
keywords: Experience Platform;página inicial;tópicos populares;api;API;XDM;sistema XDM;modelo de dados de experiência;modelo de dados;ui;espaço de trabalho;esquema;esquemas;
solution: Experience Platform
title: Criar e editar esquemas na interface
description: Saiba mais sobre as noções básicas sobre como criar e editar esquemas na interface do usuário do Experience Platform.
exl-id: be83ce96-65b5-4a4a-8834-16f7ef9ec7d1
source-git-commit: 943d1360e80caef58d09b8502507a3ad72edda03
workflow-type: tm+mt
source-wordcount: '3571'
ht-degree: 1%

---

# Criar e editar esquemas na interface

Este guia fornece uma visão geral de como criar, editar e gerenciar esquemas do Experience Data Model (XDM) para sua organização na interface do usuário do Adobe Experience Platform.

>[!IMPORTANT]
>
>Os esquemas XDM são extremamente personalizáveis e, portanto, as etapas envolvidas na criação de um esquema podem variar dependendo do tipo de dados que você deseja que o esquema capture. Como resultado, este documento abrange apenas as interações básicas que você pode fazer com esquemas na interface e exclui etapas relacionadas, como personalizar classes, grupos de campos de esquema, tipos de dados e campos.
>
>Para obter um tour completo do processo de criação de esquema, siga juntamente com a [tutorial de criação de esquema](../../tutorials/create-schema-ui.md) para criar um schema de exemplo completo e familiarizar-se com os vários recursos do [!DNL Schema Editor].

## Pré-requisitos

Este guia requer uma compreensão funcional do Sistema XDM. Consulte a [Visão geral do XDM](../../home.md) para obter uma introdução ao papel do XDM no ecossistema de Experience Platform, e a [noções básicas da composição do esquema](../../schema/composition.md) para obter uma visão geral de como os esquemas são construídos.

## Criar um novo esquema {#create}

>[!NOTE]
>
>Esta seção aborda como criar manualmente um novo esquema na interface do usuário do. Se estiver assimilando dados CSV na Platform, você pode optar por [mapear esses dados para um esquema XDM criado por recomendações geradas por IA](../../../ingestion/tutorials/map-csv/recommendations.md) (atualmente na versão beta) sem precisar criar manualmente o esquema.

No [!UICONTROL Esquemas] espaço de trabalho, selecione **[!UICONTROL Criar esquema]** no canto superior direito.

![O espaço de trabalho Esquemas com [!UICONTROL Criar esquema] destacado.](../../images/ui/resources/schemas/create-schema.png)

A variável [!UICONTROL Criar esquema] workflow aparece. Você pode escolher uma classe base para o esquema selecionando **[!UICONTROL Perfil individual]**, **[!UICONTROL Evento de experiência]** ou **[!UICONTROL Outro]**, seguido por **[!UICONTROL Próxima]** para confirmar sua escolha. Consulte a [Perfil individual XDM](../../classes/individual-profile.md) e [XDM ExperienceEvent](../../classes/experienceevent.md) para obter mais informações sobre essas classes.

![A variável [!UICONTROL Criar esquema] fluxo de trabalho com as três opções de classe e [!UICONTROL Próxima] destacado.](../../images/ui/resources/schemas/schema-class-options.png)

Depois de selecionar uma classe, a variável [!UICONTROL Nome e revisão] é exibida. Nesta seção, você fornece um nome e uma descrição para identificar o esquema. &#x200B;A estrutura base do esquema (fornecida pela classe) é mostrada na tela para que você revise e verifique a classe selecionada e a estrutura do esquema.

Entre em um [!UICONTROL Nome de exibição do esquema] no campo de texto. Em seguida, insira uma descrição adequada para ajudar a identificar seu esquema. Quando tiver revisado a estrutura do esquema e estiver satisfeito com as configurações, selecione **[!UICONTROL Concluir]** para criar seu esquema.

![A variável [!UICONTROL Nome e revisão] seção do [!UICONTROL Criar esquema] fluxo de trabalho com o [!UICONTROL Nome de exibição do esquema], [!UICONTROL Descrição], e [!UICONTROL Concluir] destacado.](../../images/ui/resources/schemas/name-and-review.png)

A variável [!UICONTROL Esquema] [!UICONTROL Procurar] é exibida. O esquema criado recentemente está disponível para edição no [!DNL Schema Editor] e aparece na lista de schemas disponíveis.

![O Editor de esquemas exibe o esquema criado recentemente.](../../images/ui/resources/schemas/schema-details.png)

Agora você pode começar a criar a estrutura do esquema [adição de grupos de campos de esquema](#add-field-groups) no [!DNL Schema Editor].

## Editar um esquema existente {#edit}

>[!NOTE]
>
>Depois que um esquema é salvo e usado na assimilação de dados, somente alterações adicionais podem ser feitas nele. Consulte a [regras de evolução do schema](../../schema/composition.md#evolution) para obter mais informações.

Para editar um esquema existente, selecione o **[!UICONTROL Procurar]** e selecione o nome do schema que deseja editar. Você também pode usar a barra de pesquisa para restringir a lista de opções disponíveis.

![O espaço de trabalho Esquema com um esquema realçado.](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
>Você pode usar os recursos de pesquisa e filtragem do espaço de trabalho para facilitar a localização do esquema. Consulte o guia sobre [exploração de recursos XDM](../explore.md) para obter mais informações.

Depois de selecionar um esquema, a variável [!DNL Schema Editor] é exibida com a estrutura do esquema mostrada na tela. Agora você pode [adicionar grupos de campos](#add-field-groups) ao esquema (ou [adicionar campos individuais](#add-individual-fields) desses grupos), [editar nomes de exibição de campo](#display-names)ou [editar grupos de campos personalizados existentes](./field-groups.md#edit) se o schema utilizar algum.

## Alternância do nome de exibição {#display-name-toggle}

Para sua conveniência, o Editor de esquemas fornece uma alternância entre os nomes de campo originais e os nomes de exibição mais legíveis. Essa flexibilidade permite uma melhor descoberta de campo e edição de seus esquemas. O botão de alternância é encontrado na parte superior direita da visualização Editor de esquemas.

>[!NOTE]
>
>A alteração de nomes de campo para nomes de exibição é meramente cosmética e não altera nenhum recurso downstream.

![O Editor de esquemas com [!UICONTROL Mostrar nomes de exibição para campos] destacado.](../../images/ui/resources/schemas/display-name-toggle.png)

Os nomes de exibição para grupos de campos padrão são gerados pelo sistema, mas podem ser personalizados, conforme descrito na seção [nomes para exibição](#display-names) seção. Os nomes de exibição são refletidos em várias exibições de interface do usuário, incluindo mapeamento e visualizações de conjunto de dados. A configuração padrão está desativada e mostra os nomes dos campos de acordo com os valores originais.

## Adicionar grupos de campos a um esquema {#add-field-groups}

>[!NOTE]
>
>Esta seção aborda como adicionar grupos de campos existentes a um esquema. Se quiser criar um novo grupo de campos personalizado, consulte o manual sobre [criação e edição de grupos de campos](./field-groups.md#create) em vez disso.

Depois de abrir um esquema na variável [!DNL Schema Editor], é possível adicionar campos ao esquema por meio do uso de grupos de campos. Para começar, selecione **[!UICONTROL Adicionar]** ao lado de **[!UICONTROL Grupos de campos]** no painel esquerdo.

![O Editor de esquemas com o [!UICONTROL Adicionar] do [!UICONTROL Grupos de campos] seção realçada.](../../images/ui/resources/schemas/add-field-group-button.png)

Uma caixa de diálogo é exibida, mostrando uma lista de grupos de campos que você pode selecionar para o esquema. Como os grupos de campos são compatíveis apenas com uma classe, somente os grupos de campos associados à classe selecionada do esquema serão listados. Por padrão, os grupos de campos listados são classificados com base na popularidade do uso em sua organização.

![A variável [!UICONTROL Adicionar grupos de campos] caixa de diálogo realçada com o [!UICONTROL População] realçada.](../../images/ui/resources/schemas/field-group-popularity.png)

Se você souber a atividade geral ou a área comercial dos campos que deseja adicionar, selecione uma ou mais categorias verticais do setor no painel à esquerda para filtrar a lista exibida de grupos de campos.

![A variável [!UICONTROL Adicionar grupos de campos] caixa de diálogo realçada com o [!UICONTROL Setor] filtros e a variável [!UICONTROL Setor] realçada.](../../images/ui/resources/schemas/industry-filter.png)

>[!NOTE]
>
>Para obter mais informações sobre as práticas recomendadas para modelagem de dados específica do setor no XDM, consulte a documentação sobre [modelos de dados do setor](../../schema/industries/overview.md).

Você também pode usar a barra de pesquisa para ajudar a localizar o grupo de campos desejado. Os grupos de campos cujo nome corresponde à consulta são exibidos na parte superior da lista. Em **[!UICONTROL Campos padrão]**, grupos de campos que contêm campos que descrevem os atributos de dados desejados são exibidos.

![A variável [!UICONTROL Adicionar grupos de campos] com a [!UICONTROL Campos padrão] função de pesquisa realçada.](../../images/ui/resources/schemas/field-group-search.png)

Marque a caixa de seleção ao lado do nome do grupo de campos que você deseja adicionar ao esquema. É possível selecionar vários grupos de campos na lista, com cada grupo de campos selecionado aparecendo no painel direito.

![A variável [!UICONTROL Adicionar grupos de campos] caixa de diálogo com o recurso de seleção de caixa de seleção realçado.](../../images/ui/resources/schemas/add-field-group.png)

>[!TIP]
>
>Para qualquer grupo de campos listado, é possível passar o mouse ou focalizar o ícone de informações (![](../../images/ui/resources/schemas/info-icon.png)) para exibir uma breve descrição do tipo de dados que o grupo de campos captura. Também é possível selecionar o ícone de visualização (![](../../images/ui/resources/schemas/preview-icon.png)) para exibir a estrutura dos campos que o grupo de campos fornece antes de decidir adicioná-lo ao esquema.

Depois de escolher os grupos de campos, selecione **[!UICONTROL Adicionar grupos de campos]** para adicioná-los ao esquema.

![A variável [!UICONTROL Adicionar grupos de campos] caixa de diálogo com grupos de campos selecionados e [!UICONTROL Adicionar grupos de campos] destacado.](../../images/ui/resources/schemas/add-field-group-finish.png)

A variável [!DNL Schema Editor] reaparece com os campos fornecidos pelo grupo de campos representados na tela.

![A variável [!DNL Schema Editor] com um schema de exemplo exibido.](../../images/ui/resources/schemas/field-groups-added.png)

Depois de adicionar um grupo de campos a um esquema, você pode [remover campos existentes](#remove-fields) ou [adicionar novos campos personalizados](#add-fields) para esses grupos, dependendo das suas necessidades.

### Remover campos adicionados de grupos de campos {#remove-fields}

Depois de adicionar um grupo de campos a um esquema, você pode remover os campos desnecessários.

>[!NOTE]
>
>A remoção de campos de um grupo de campos afeta apenas o esquema que está sendo trabalhado e não afeta o próprio grupo de campos. Se você remover campos em um esquema, esses campos ainda estarão disponíveis em todos os outros esquemas que empregam o mesmo grupo de campos.

No exemplo a seguir, o grupo de campos padrão **[!UICONTROL Detalhes demográficos]** foi adicionado a um esquema. Para remover um único campo, como `taxId`, selecione o campo na tela e selecione **[!UICONTROL Remover]** no painel direito.

![A variável [!DNL Schema Editor] com [!UICONTROL Remover] destacado. Esta ação remove um único campo.](../../images/ui/resources/schemas/remove-single-field.png)

Se houver vários campos que você deseja remover, é possível gerenciar o grupo de campos como um todo. Selecione um campo pertencente ao grupo na tela e selecione **[!UICONTROL Gerenciar campos relacionados]** no painel direito.

![A variável [!DNL Schema Editor] com [!UICONTROL Gerenciar campos relacionados] destacado.](../../images/ui/resources/schemas/manage-related-fields.png)

Uma caixa de diálogo é exibida mostrando a estrutura do grupo de campos em questão. Aqui, é possível usar as caixas de seleção fornecidas para marcar ou desmarcar os campos necessários. Quando estiver satisfeito, selecione **[!UICONTROL Confirmar o]**.

![A variável [!UICONTROL Gerenciar campos relacionados] com campos selecionados e [!UICONTROL Confirmar o] destacado.](../../images/ui/resources/schemas/select-fields.png)

A tela reaparece com apenas os campos selecionados presentes na estrutura do esquema.

![Campos adicionados](../../images/ui/resources/schemas/fields-added.png)

### Adicionar campos personalizados a grupos de campos {#add-fields}

Depois de ter adicionado um grupo de campos a um esquema, você pode definir campos adicionais para esse grupo. No entanto, todos os campos adicionados a um grupo de campos em um esquema também aparecerão em todos os outros esquemas que empregam esse mesmo grupo de campos.

Além disso, se um campo personalizado for adicionado a um grupo de campos padrão, esse grupo de campos será convertido em um grupo de campos personalizado e o grupo de campos padrão original não estará mais disponível.

Se quiser adicionar um campo personalizado a um grupo de campos padrão, consulte o [seção abaixo](#custom-fields-for-standard-groups) para obter instruções específicas. Se estiver adicionando campos a um grupo de campos personalizado, consulte a seção sobre [edição de grupos de campos personalizados](./field-groups.md) no guia da interface dos grupos de campos.

Se não quiser alterar nenhum grupo de campos existente, você poderá [criar um novo grupo de campos personalizado](./field-groups.md#create) para definir campos adicionais.

## Adicionar campos individuais a um esquema {#add-individual-fields}

O Editor de esquemas permite adicionar campos individuais diretamente a um esquema se você não quiser adicionar um grupo de campos inteiro para um caso de uso específico. Você pode [adicionar campos individuais a partir de grupos de campos padrão](#add-standard-fields) ou [adicionar seus próprios campos personalizados](#add-custom-fields) em vez disso.

>[!IMPORTANT]
>
>Embora o Editor de esquemas funcionalmente permita adicionar campos individuais diretamente a um esquema, isso não altera o fato de que todos os campos em um esquema XDM devem ser fornecidos por sua classe ou por um grupo de campos compatível com essa classe. Conforme explicado nas seções abaixo, todos os campos individuais ainda estão associados a uma classe ou grupo de campos como uma etapa principal quando são adicionados a um esquema.

### Adicionar campos padrão {#add-standard-fields}

Você pode adicionar campos de grupos de campos padrão diretamente a um esquema sem precisar saber seu grupo de campos correspondente antecipadamente. Para adicionar um campo padrão a um esquema, selecione o sinal de mais (**+**) ao lado do nome do esquema na tela. Um **[!UICONTROL Campo sem título]** o espaço reservado é exibido na estrutura do esquema e o painel direito é atualizado para revelar controles para configurar o campo.

![Espaço reservado do campo](../../images/ui/resources/schemas/root-custom-field.png)

Em **[!UICONTROL Nome do campo]**, comece digitando o nome do campo que deseja adicionar. O sistema procura automaticamente por campos padrão que correspondam à consulta e os lista em **[!UICONTROL Campos padrão recomendados]**, incluindo os grupos de campos aos quais pertencem.

![Campos padrão recomendados](../../images/ui/resources/schemas/standard-field-search.png)

Embora alguns campos padrão compartilhem o mesmo nome, sua estrutura pode variar dependendo do grupo de campos de onde vêm. Se um campo padrão estiver aninhado em um objeto principal na estrutura do grupo de campos, o campo principal também será incluído no esquema se o campo secundário for adicionado.

Selecione o ícone de visualização (![Ícone Visualizar](../../images/ui/resources/schemas/preview-icon.png)) ao lado de um campo padrão para exibir a estrutura do grupo de campos e entender melhor como ele pode estar aninhado. Para adicionar o campo padrão ao esquema, selecione o ícone de adição (![Ícone de adição](../../images/ui/resources/schemas/add-icon.png)).

![Adicionar campo padrão](../../images/ui/resources/schemas/add-standard-field.png)

A tela é atualizada para mostrar o campo padrão adicionado ao esquema, incluindo todos os campos principais sob os quais ele está aninhado dentro da estrutura do grupo de campos. O nome do grupo de campos também está listado em **[!UICONTROL Grupos de campos]** no painel esquerdo. Se quiser adicionar mais campos do mesmo grupo, selecione **[!UICONTROL Gerenciar campos relacionados]** no painel direito.

![Campo padrão adicionado](../../images/ui/resources/schemas/standard-field-added.png)

### Adicionar campos personalizados {#add-custom-fields}

Semelhante ao fluxo de trabalho para campos padrão, também é possível adicionar seus próprios campos personalizados diretamente a um esquema.

Para adicionar campos ao nível raiz de um esquema, selecione o sinal de mais (**+**) ao lado do nome do esquema na tela. Um **[!UICONTROL Campo sem título]** o espaço reservado é exibido na estrutura do esquema e o painel direito é atualizado para revelar controles para configurar o campo.

![Campo personalizado da raiz](../../images/ui/resources/schemas/root-custom-field.png)

Comece a digitar o nome do campo que deseja adicionar e o sistema inicia automaticamente a pesquisa por campos padrão correspondentes. Para criar um novo campo personalizado, selecione a opção superior anexada com **([!UICONTROL Novo campo])**.

![Novo campo](../../images/ui/resources/schemas/custom-field-search.png)

Depois de fornecer um nome de exibição e um tipo de dados para o campo, a próxima etapa é atribuir o campo a um recurso XDM principal. Se o esquema usar uma classe personalizada, você poderá optar por [adicionar o campo à classe atribuída](#add-to-class) ou um [grupo de campos](#add-to-field-group) em vez disso. No entanto, se o esquema usar uma classe padrão, você só poderá atribuir o campo personalizado a um grupo de campos.

#### Atribuir o campo a um grupo de campos personalizado {#add-to-field-group}

>[!NOTE]
>
>Esta seção aborda apenas como atribuir o campo a um grupo de campos personalizados. Se, em vez disso, você quiser estender um grupo de campos padrão com o novo campo personalizado, consulte a seção sobre [adição de campos personalizados a grupos de campos padrão](#custom-fields-for-standard-groups).

Em **[!UICONTROL Atribuir a]**, selecione **[!UICONTROL Grupo de campos]**. Se o esquema usar uma classe padrão, essa será a única opção disponível e será selecionada por padrão.

Em seguida, é necessário selecionar um grupo de campos ao qual o novo campo será associado. Comece a digitar o nome do grupo de campos na entrada de texto fornecida. Se você tiver grupos de campos personalizados que correspondam à entrada, eles serão exibidos na lista suspensa. Como alternativa, você pode digitar um nome exclusivo para criar um novo grupo de campos.

![Selecionar grupo de campos](../../images/ui/resources/schemas/select-field-group.png)

>[!WARNING]
>
>Se você selecionar um grupo de campos personalizado existente, todos os outros esquemas que empregam esse grupo de campos também herdarão o campo recém-adicionado depois que você salvar as alterações. Por esse motivo, somente selecione um grupo de campos existente se desejar esse tipo de propagação. Caso contrário, você deve optar por criar um novo grupo de campos personalizados.

Depois de selecionar o grupo de campos na lista, selecione **[!UICONTROL Aplicar]**.

![Aplicar campo](../../images/ui/resources/schemas/apply-field.png)

O novo campo é adicionado à tela e seu namespace é alterado em [ID do inquilino](../../api/getting-started.md#know-your-tenant_id) para evitar conflitos com campos XDM padrão. O grupo de campos ao qual você associou o novo campo também aparece em **[!UICONTROL Grupos de campos]** no painel esquerdo.

![ID do inquilino](../../images/ui/resources/schemas/tenantId.png)

>[!NOTE]
>
>O restante dos campos fornecidos pelo grupo de campos personalizados selecionado são removidos do esquema por padrão. Se quiser adicionar alguns desses campos ao esquema, selecione um campo pertencente ao grupo e selecione **[!UICONTROL Gerenciar campos relacionados]** no painel direito.

#### Atribuir o campo a uma classe personalizada {#add-to-class}

Em **[!UICONTROL Atribuir a]**, selecione **[!UICONTROL Classe]**. O campo de entrada abaixo é substituído pelo nome da classe personalizada do esquema atual, indicando que o novo campo será atribuído a essa classe.

![A variável [!UICONTROL Classe] opção que está sendo selecionada para a nova atribuição de campo.](../../images/ui/resources/schemas/assign-field-to-class.png)

Continue a configurar o campo conforme desejado e selecione **[!UICONTROL Aplicar]** quando terminar.

![[!UICONTROL Aplicar] selecionado para o novo campo.](../../images/ui/resources/schemas/assign-field-to-class-apply.png)

O novo campo é adicionado à tela e seu namespace é alterado em [ID do inquilino](../../api/getting-started.md#know-your-tenant_id) para evitar conflitos com campos XDM padrão. Selecionar o nome da classe no painel à esquerda revela o novo campo como parte da estrutura da classe.

![O novo campo aplicado à estrutura da classe personalizada, representado na tela.](../../images/ui/resources/schemas/assign-field-to-class-applied.png)

### Adicionar campos personalizados à estrutura de grupos de campos padrão {#custom-fields-for-standard-groups}

Se o esquema em que você está trabalhando tiver um campo do tipo objeto fornecido por um grupo de campos padrão, será possível adicionar seus próprios campos personalizados a esse objeto padrão.

>[!WARNING]
>
>Quaisquer campos adicionados a um grupo de campos em um esquema também aparecerão em todos os outros esquemas que empregam esse mesmo grupo de campos. Além disso, se um campo personalizado for adicionado a um grupo de campos padrão, esse grupo de campos será convertido em um grupo de campos personalizado e o grupo de campos padrão original não estará mais disponível.
>
>Se você participou da versão beta desse recurso, você receberá uma caixa de diálogo informando sobre os grupos de campos padrão que você personalizou anteriormente. Depois de selecionar **[!UICONTROL Confirmar]**, os recursos listados são convertidos em grupos de campos personalizados.
>
>![Caixa de diálogo de confirmação para converter grupos de campos padrão](../../images/ui/resources/schemas/beta-extension-confirmation.png)

Para começar, selecione o sinal de mais (**+**) ao lado da raiz do objeto fornecido pelo grupo de campos padrão.

![Adicionar campo ao objeto padrão](../../images/ui/resources/schemas/add-field-to-standard-object.png)

Uma mensagem de aviso é exibida, solicitando que você confirme se deseja converter o grupo de campos padrão. Selecionar **[!UICONTROL Continuar criando grupo de campos]** para continuar.

![Confirmar conversão de grupo de campos](../../images/ui/resources/schemas/confirm-field-group-conversion.png)

A tela de desenho reaparece com um espaço reservado sem título para o novo campo. Observe que o nome do grupo de campos padrão foi anexado com &quot;([!UICONTROL Estendido])&quot; para indicar que foi modificado em relação à versão original. Aqui, use os controles no painel direito para definir as propriedades do campo.

![Campo adicionado ao objeto padrão](../../images/ui/resources/schemas/standard-field-group-converted.png)

Depois de aplicar as alterações, o novo campo aparece sob o namespace da ID do locatário dentro do objeto padrão. Esse namespace aninhado impede conflitos de nome de campo dentro do próprio grupo de campos para evitar alterações em outros esquemas que usam o mesmo grupo de campos.

![Campo adicionado ao objeto padrão](../../images/ui/resources/schemas/added-to-standard-object.png)

## Ativar um esquema para o Perfil de cliente em tempo real {#profile}

>[!CONTEXTUALHELP]
>id="platform_schemas_enableforprofile"
>title="Habilitar um esquema para o perfil"
>abstract="Quando um esquema é ativado para o perfil, qualquer conjunto de dados criado a partir desse esquema participa do perfil do cliente em tempo real, que mescla dados de fontes diferentes para construir uma visualização completa de cada cliente. Depois que um esquema é usado para assimilar dados no perfil, ele não pode ser desabilitado. Consulte a documentação para obter mais informações."

[Perfil do cliente em tempo real](../../../profile/home.md) O mescla dados de fontes diferentes para criar uma visualização completa de cada cliente individual. Se quiser que os dados capturados por um schema participem desse processo, ative o schema para uso em [!DNL Profile].

>[!IMPORTANT]
>
>Para ativar um esquema para [!DNL Profile], ele deve ter um campo de identidade principal definido. Consulte o guia sobre [definição de campos de identidade](../fields/identity.md) para obter mais informações.

Para ativar o esquema, comece selecionando o nome do esquema no painel à esquerda e selecione o **[!UICONTROL Perfil]** no painel direito.

![](../../images/ui/resources/schemas/profile-toggle.png)

Um popover é exibido, avisando que, uma vez que um esquema tenha sido ativado e salvo, ele não poderá ser desativado. Selecionar **[!UICONTROL Ativar]** para continuar.

![](../../images/ui/resources/schemas/profile-confirm.png)

A tela reaparece com a tag [!UICONTROL Perfil] alternância ativada.

>[!IMPORTANT]
>
>Como o esquema ainda não foi salvo, esse é o ponto sem volta se você mudar de ideia sobre como permitir que o esquema participe do Perfil do cliente em tempo real: depois de salvar um esquema ativado, ele não poderá mais ser desativado. Selecione o **[!UICONTROL Perfil]** alterne novamente para desativar o esquema.

Para concluir o processo, selecione **[!UICONTROL Salvar]** para salvar o esquema.

![](../../images/ui/resources/schemas/profile-enabled.png)

O esquema agora está ativado para uso no Perfil do cliente em tempo real. Quando a Platform assimila dados em conjuntos de dados com base nesse esquema, esses dados são incorporados aos dados do perfil amalgamados.

## Editar nomes de exibição para campos de esquema {#display-names}

Depois de atribuir uma classe e adicionar grupos de campos a um esquema, você pode editar os nomes de exibição de qualquer um dos campos do esquema, independentemente de esses campos terem sido fornecidos por recursos XDM padrão ou personalizados.

>[!NOTE]
>
>Lembre-se de que os nomes de exibição dos campos que pertencem a classes ou grupos de campos padrão só podem ser editados no contexto de um esquema específico. Em outras palavras, alterar o nome de exibição de um campo padrão em um esquema não afeta outros esquemas que empregam a mesma classe ou grupo de campos associado.
>
>Depois de fazer alterações nos nomes de exibição dos campos de um esquema, essas alterações são refletidas imediatamente em qualquer conjunto de dados existente com base nesse esquema.

Para editar o nome de exibição de um campo de esquema, selecione o campo na tela. No painel direito, forneça o novo nome em **[!UICONTROL Nome de exibição]**.

![](../../images/ui/resources/schemas/display-name.png)

Selecionar **[!UICONTROL Aplicar]** no painel direito, e a tela é atualizada para mostrar o novo nome de exibição do campo. Selecionar **[!UICONTROL Salvar]** para aplicar as alterações ao esquema.

![](../../images/ui/resources/schemas/display-name-changed.png)

## Alterar a classe de um esquema {#change-class}

Você pode alterar a classe de um esquema em qualquer momento durante o processo de composição inicial, antes que o esquema tenha sido salvo.

>[!WARNING]
>
>A reatribuição da classe para um schema deve ser feita com extremo cuidado. Os grupos de campos são compatíveis apenas com determinadas classes e, portanto, alterar a classe redefinirá a tela e quaisquer campos adicionados.

Para reatribuir uma classe, selecione **[!UICONTROL Atribuir]** no lado esquerdo da tela.

![](../../images/ui/resources/schemas/assign-class-button.png)

Uma caixa de diálogo é exibida, mostrando uma lista de todas as classes disponíveis, inclusive as definidas por sua organização (sendo o proprietário &quot;[!UICONTROL Cliente]&quot;), bem como as classes padrão definidas pelo Adobe.

Selecione uma classe na lista para exibir sua descrição no lado direito da caixa de diálogo. Também é possível selecionar **[!UICONTROL Visualizar estrutura de classe]** para ver os campos e metadados associados à classe. Selecionar **[!UICONTROL Atribuir classe]** para continuar.

![](../../images/ui/resources/schemas/assign-class.png)

Uma nova caixa de diálogo é aberta, pedindo que você confirme se deseja atribuir uma nova classe. Selecionar **[!UICONTROL Atribuir]** para confirmar.

![](../../images/ui/resources/schemas/assign-confirm.png)

Depois de confirmar a alteração de classe, a tela será redefinida e todo o progresso da composição será perdido.

## Próximas etapas

Este documento abordou as noções básicas de criação e edição de esquemas na interface do usuário da Platform. É altamente recomendável que você analise a [tutorial de criação de esquema](../../tutorials/create-schema-ui.md) para obter um fluxo de trabalho abrangente para criar um esquema completo na interface do usuário, incluindo a criação de grupos de campos personalizados e tipos de dados para casos de uso exclusivos.

Para obter mais informações sobre os recursos do [!UICONTROL Esquemas] espaço de trabalho, consulte a [[!UICONTROL Esquemas] visão geral do espaço de trabalho](../overview.md).

Para saber como gerenciar esquemas na [!DNL Schema Registry] , consulte a [manual de endpoint de esquemas](../../api/schemas.md).
