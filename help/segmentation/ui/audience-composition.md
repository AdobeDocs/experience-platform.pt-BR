---
solution: Experience Platform
title: Guia da interface do usuário de públicos
description: A Composição de público-alvo na interface do usuário do Adobe Experience Platform fornece um espaço de trabalho avançado que permite interagir com elementos de dados do perfil. O espaço de trabalho fornece controles intuitivos para criação e edição de públicos-alvo para sua organização.
exl-id: 0dda0cb1-49e0-478b-8004-84572b6cf625
source-git-commit: 3c0fdab5d7561238a64e79e5bab5fd4843fccb0a
workflow-type: tm+mt
source-wordcount: '1952'
ht-degree: 0%

---

# Guia da interface do usuário da Composição de público-alvo

>[!NOTE]
>
>Este guia explica como criar públicos-alvo usando a Composição de público-alvo. Para saber como criar públicos-alvo por meio de definições de segmento usando o Construtor de segmentos, leia o [guia da interface do Construtor de segmentos](./segment-builder.md).

A Composição de público-alvo fornece um espaço de trabalho para criar e editar públicos-alvo, usando blocos usados para representar ações diferentes.

![A interface do usuário de composição de público-alvo.](../images/ui/audience-composition/audience-composition.png)

Para alterar os detalhes da composição, incluindo o título e a descrição, selecione o botão ![controles deslizantes](/help/images/icons/properties.png).

O popover **[!UICONTROL Propriedades de composição]** é exibido. Você pode inserir detalhes da sua composição, incluindo o título e a descrição aqui.

![O popover Propriedades de composição é exibido.](../images/ui/audience-composition/composition-properties.png)

>[!NOTE]
>
>Se você **não** der um título à sua composição, ela terá um título de &quot;Composição&quot; seguido pela data e hora de criação por padrão. Além disso, cada composição **deve** ter seu próprio nome exclusivo.

Depois de atualizar os detalhes da sua composição, selecione **[!UICONTROL Salvar]** para confirmar essas atualizações. A tela de composição do público-alvo é exibida novamente.

A tela de composição de público é composta por quatro tipos diferentes de blocos: **[[!UICONTROL Público-alvo]](#audience-block)**, **[[!UICONTROL Excluir]](#exclude-block)**, **[[!UICONTROL Classificação]](#rank-block)** e **[[!UICONTROL Divisão]](#split-block)**.

## [!UICONTROL Público-alvo] {#audience-block}

O tipo de bloco **[!UICONTROL Público]** permite adicionar os subpúblicos que você deseja compor para seu novo público maior. Por padrão, um bloco **[!UICONTROL Público-alvo]** está incluído na parte superior da tela de composição.

Ao selecionar o bloco **[!UICONTROL Público-alvo]**, o painel direito exibe controles para rotular o público-alvo, adicionar públicos-alvo ao bloco, bem como criar regras personalizadas para o bloco de público-alvo.

>[!NOTE]
>
>Você pode adicionar públicos-alvo **ou** criar uma regra personalizada. Estas duas funcionalidades **não podem** ser usadas juntas.

![Os detalhes do bloco de público-alvo são exibidos.](../images/ui/audience-composition/audience-block.png)

### [!UICONTROL Adicionar público-alvo] {#add-audience}

Para adicionar públicos-alvo ao bloco Público-alvo. selecione **[!UICONTROL Adicionar público-alvo]**.

![O botão Adicionar público-alvo está realçado.](../images/ui/audience-composition/add-audience.png)

>[!IMPORTANT]
>
>Observe que **somente** públicos-alvo definidos com a política de mesclagem padrão serão exibidos.
>
>Além disso, somente **públicos-alvo** publicados criados com o Construtor de segmentos podem ser usados. Públicos criados usando a Composição de público-alvo e públicos gerados externamente estão **não** disponíveis.

Uma lista de públicos-alvo é exibida. Selecione os públicos que você deseja incluir, seguido por **[!UICONTROL Adicionar]** para anexá-los ao seu bloco de público.

![Uma lista de públicos-alvo é exibida. Você pode selecionar qual público-alvo deseja adicionar desta caixa de diálogo.](../images/ui/audience-composition/select-audience.png)

Os públicos selecionados agora aparecem no painel direito quando o bloco **[!UICONTROL Público]** é selecionado. Aqui, é possível alterar o tipo de mesclagem dos públicos-alvo combinados.

![Os tipos de mesclagem possíveis para os públicos-alvo estão realçados.](../images/ui/audience-composition/merge-types.png)

| Tipo de mesclagem | Descrição |
| ---------- | ----------- |
| [!UICONTROL União] | Os públicos são combinados em um único público. Isso seria equivalente a uma operação OR. |
| [!UICONTROL Interseção] | Os públicos são combinados, com apenas os públicos compartilhados em **todos** sendo adicionados. Isso seria equivalente a uma operação AND. |
| [!UICONTROL Excluir sobreposição] | Os públicos são combinados, com apenas os públicos compartilhados em **um, mas não todos** adicionados. Isso seria o equivalente a uma operação XOR. |

### [!UICONTROL Regra de compilação] {#build-rule}

Para adicionar uma regra personalizada ao bloco Público-alvo, selecione **[!UICONTROL Criar regra]**.

![O botão Criar regra está realçado.](../images/ui/audience-composition/build-rule.png)

O Construtor de segmentos é exibido. Você pode usar o Construtor de segmentos para criar uma regra personalizada a ser seguida pelo público-alvo. Mais informações sobre como usar o Construtor de segmentos podem ser encontradas no [guia do Construtor de segmentos](./segment-builder.md).

![A interface do usuário do Construtor de segmentos é exibida.](../images/ui/audience-composition/segment-builder.png)

Depois de adicionar uma regra personalizada, selecione **[!UICONTROL Salvar]** para adicionar a regra ao seu público-alvo.

![](../images/ui/audience-composition/custom-rule.png)

## [!UICONTROL Excluir] {#exclude-block}

O tipo de bloco **[!UICONTROL Excluir]** permite excluir um subpúblico ou atributos especificados de seu novo público-alvo maior.

Para adicionar um bloco **[!UICONTROL Excluir]**, selecione o ícone **+**, seguido por **[!UICONTROL Excluir]**.

![A opção Excluir está selecionada.](../images/ui/audience-composition/add-exclude-block.png)

O bloco **[!UICONTROL Excluir]** foi adicionado. Quando esse bloco for selecionado, os detalhes sobre a exclusão aparecerão no painel direito. Isso inclui o rótulo do bloco e o tipo de exclusão. Você pode excluir [por público](#exclude-audience) ou [por atributo](#exclude-attribute).

![O bloco Excluir, destacando os dois tipos de exclusão diferentes disponíveis.](../images/ui/audience-composition/exclude.png)

### Excluir por público {#exclude-audience}

Se você excluir por público-alvo, poderá selecionar qual público-alvo deseja excluir selecionando **[!UICONTROL Adicionar público-alvo]**.

![O botão [!UICONTROL Adicionar público-alvo] está selecionado, o que permite escolher qual público-alvo você deseja excluir.](../images/ui/audience-composition/add-excluded-audience.png)

>[!IMPORTANT]
>
>Somente **públicos-alvo** publicados criados com o Construtor de segmentos podem ser usados. Públicos criados usando a Composição de público-alvo e públicos gerados externamente estão **não** disponíveis.

Uma lista de públicos-alvo é exibida. Selecione **[!UICONTROL Adicionar]** para adicionar o público-alvo que você deseja excluir ao bloco de exclusão.

![Uma lista de públicos-alvo é exibida. Você pode selecionar qual público-alvo deseja adicionar desta caixa de diálogo.](../images/ui/audience-composition/select-audience.png)

### Excluir por atributo {#exclude-attribute}

Se você excluir por atributo, poderá selecionar quais atributos deseja excluir selecionando o ícone ![filtro](/help/images/icons/project-edit.png) na seção **[!UICONTROL Regra de exclusão]**.

![A seção de atributo está realçada, mostrando onde escolher o atributo a ser excluído.](../images/ui/audience-composition/exclude-attribute.png)

Uma lista de atributos de perfil é exibida. Selecione o tipo de atributo que deseja excluir, seguido por **[!UICONTROL Selecionar]** para adicioná-los ao bloco de exclusão.

![Uma lista de atributos é exibida.](../images/ui/audience-composition/select-attribute-exclude.png)

>[!IMPORTANT]
>
>Ao excluir por atributo, você só pode especificar **um** valor para excluir. Usar qualquer tipo de separador, como vírgula ou ponto e vírgula, resultará apenas na exclusão desse valor exato. Por exemplo, definir o valor como `red, blue` resultará na exclusão do termo `red, blue` do atributo, mas **não** resultará na exclusão do termo `red` ou `blue`.

## [!UICONTROL Enriquecer] {#enrich-block}

>[!IMPORTANT]
>
>Neste momento, os atributos de enriquecimento podem **somente** ser usados em cenários de downstream do Adobe Journey Optimizer.

O tipo de bloco **[!UICONTROL Enrich]** permite enriquecer o público com atributos adicionais de um conjunto de dados. Você pode usar esses atributos em casos de uso de personalização.

Para adicionar um bloco **[!UICONTROL Enrich]**, selecione o ícone **+**, seguido por **[!UICONTROL Enrich]**.

![A opção [!UICONTROL Enriquecer] está selecionada.](../images/ui/audience-composition/add-enrich-block.png)

O bloco **[!UICONTROL Enrich]** foi adicionado. Quando esse bloco for selecionado, os detalhes sobre o enriquecimento aparecerão no painel direito. Isso inclui o rótulo do bloco e o conjunto de dados de enriquecimento.

Para selecionar o conjunto de dados com o qual o público será enriquecido, selecione o ícone ![filtro](/help/images/icons/project-edit.png).

![O botão de filtro está realçado. Selecionar isso leva ao popover [!UICONTROL Selecionar conjunto de dados].](../images/ui/audience-composition/enrich-select-dataset.png)

O popover **[!UICONTROL Selecionar conjunto de dados]** é exibido. Selecione o conjunto de dados que você deseja adicionar para enriquecimento, seguido de **[!UICONTROL Selecionar]** para adicionar o conjunto de dados para enriquecimento.

![O conjunto de dados escolhido está selecionado.](../images/ui/audience-composition/enrich-dataset-selected.png)

>[!IMPORTANT]
>
>O conjunto de dados selecionado **deve** atender aos seguintes critérios:
>
>- O conjunto de dados **deve** ser do tipo de registro.
>   - O conjunto de dados **não pode** ser do tipo de evento, ser gerado pelo sistema ou ser marcado para Perfil.
>- O conjunto de dados **deve** ter 1 GB ou menos.

A seção **[!UICONTROL Critérios de enriquecimento]** agora aparece no painel direito. Nesta seção, você pode selecionar a **[!UICONTROL Chave de junção do Source]** e a **[!UICONTROL Chave de junção do conjunto de dados de enriquecimento]**, que permite vincular o conjunto de dados de enriquecimento ao público que você está tentando criar.

![A área [!UICONTROL Critérios de enriquecimento] está realçada.](../images/ui/audience-composition/enrichment-criteria.png)

Para selecionar a **[!UICONTROL chave de junção do Source]**, selecione o ícone ![filtro](/help/images/icons/project-edit.png).

![O ícone de filtro da [!UICONTROL chave de junção do Source] está realçado.](../images/ui/audience-composition/enrich-select-source-join-key.png)

O popover **[!UICONTROL Selecionar um atributo de perfil]** é exibido. Selecione o atributo de perfil que você deseja usar como chave de junção de origem, seguido por **[!UICONTROL Selecionar]** para escolher esse atributo como sua chave de junção de origem.

![O atributo que você deseja usar como chave de junção de origem está realçado.](../images/ui/audience-composition/enrich-select-profile-attribute.png)

Para selecionar a chave de junção do conjunto de dados de **[!UICONTROL Enriquecimento]**, selecione o ícone ![filtro](/help/images/icons/project-edit.png).

![O ícone de filtro da [!UICONTROL Chave de junção do conjunto de dados de Enriquecimento] está realçado.](../images/ui/audience-composition/enrich-select-enrichment-dataset-join-key.png)

O popover **[!UICONTROL Atributos de enriquecimento]** é exibido. Selecione o atributo que deseja usar como chave de junção do conjunto de dados de enriquecimento, seguido por **[!UICONTROL Selecionar]** para escolher esse atributo como sua chave de junção do conjunto de dados de enriquecimento.

![O atributo que você deseja usar como chave de junção do conjunto de dados de enriquecimento está realçado.](../images/ui/audience-composition/enrich-select-enrichment-dataset-attribute.png)

Agora que você adicionou ambas as chaves de junção, a seção **[!UICONTROL Atributos de enriquecimento]** é exibida. Agora você pode adicionar o atributo com o qual deseja aprimorar seu público-alvo. Para adicionar esses atributos, selecione **[!UICONTROL Adicionar atributo]**.

![O botão [!UICONTROL Adicionar atributo] está realçado.](../images/ui/audience-composition/enrich-select-add-attribute.png)

O popover **[!UICONTROL Atributos de enriquecimento]** é exibido. Você pode selecionar os atributos do conjunto de dados com os quais enriquecer seu público, seguido de **[!UICONTROL Selecionar]** para adicionar os atributos ao seu público.

![Os atributos de enriquecimento que você deseja adicionar estão realçados.](../images/ui/audience-composition/enrich-add-enrichment-attributes.png)

<!-- ## [!UICONTROL Join] {#join-block}

The **[!UICONTROL Join]** block type allows you to add in external audiences from datasets that have not yet been processed by Adobe Experience Platform.

To add a **[!UICONTROL Join]** block, select the **+** icon, followed by **[!UICONTROL Join]**.

![The Join option is selected.](../images/ui/audience-composition/add-join-block.png)

When you select the block, details about the join are shown in the right rail, including the block's label and the option to add audiences to the enrichment dataset.

![The join block is highlighted, including details about the join block.](../images/ui/audience-composition/join.png)

After selecting **[!UICONTROL Add Audience]**, a list of audiences appears. Select the audiences you want to include, followed by **[!UICONTROL Add]** to add them to your join block.

![A list of audiences appears. You can select which audience you want to add from this dialog.](../images/ui/audience-composition/select-audience.png)

Your selected audiences now appear within the right rail when the **[!UICONTROL Join]** block is selected. 

![The audiences that were added as part of the Join are shown.](../images/ui/audience-composition/selected-audiences.png) -->

## [!UICONTROL Classificação] {#rank-block}

O tipo de bloco **[!UICONTROL Rank]** permite classificar e classificar perfis com base em um atributo especificado e incluir esses perfis classificados na sua composição.

Para adicionar um bloco **[!UICONTROL Rank]**, selecione o ícone **+**, seguido por **[!UICONTROL Rank]**.

![A opção Rank está selecionada.](../images/ui/audience-composition/add-rank-block.png)

Ao selecionar o bloco, os detalhes sobre a classificação são mostrados no painel direito, incluindo o rótulo do bloco, o atributo para classificar, a ordem de classificação e um botão para limitar o número de perfis a serem classificados.

![O bloco de classificação está realçado, bem como os detalhes do bloco de classificação.](../images/ui/audience-composition/rank.png)

Para selecionar por qual atributo classificar os públicos-alvo, selecione o ícone ![filtro](/help/images/icons/project-edit.png).

![O ícone de filtro está realçado, mostrando o que selecionar para acessar a tela de seleção de atributo de perfil.](../images/ui/audience-composition/select-rank-attribute.png)

Uma lista de atributos de perfil é exibida. Nesse popover, você pode selecionar o tipo de atributo pelo qual deseja classificar seu público-alvo. Selecione **[!UICONTROL Selecionar]** para adicioná-lo ao bloco de classificação. Observe que o atributo selecionado pode **ser apenas** números.

![Uma lista de atributos é exibida.](../images/ui/audience-composition/select-attribute-rank.png)

Depois de selecionar o atributo, você pode selecionar a ordem pela qual ele será classificado. É em ordem crescente (do mais baixo para o mais alto) ou decrescente (do mais alto para o mais baixo).

Além disso, é possível limitar o número de perfis retornados habilitando a opção **[!UICONTROL Adicionar limite de perfil]**. Quando esta opção estiver habilitada, você poderá definir o número máximo de perfis retornados no campo **[!UICONTROL Perfis incluídos]**.

![A opção Adicionar limite de perfil está realçada, o que permite limitar o número de perfis retornados.](../images/ui/audience-composition/add-profile-limit.png)

## [!UICONTROL Split] {#split-block}

O tipo de bloco **[!UICONTROL Split]** permite dividir o novo público em vários subpúblicos. Você pode dividir esse público com base na porcentagem ou por um atributo. Ao dividir o público em subpúblicos, essa divisão é **não** persistente. Isso significa que os perfis podem estar em subpúblicos diferentes para cada avaliação.

Para adicionar um bloco **[!UICONTROL Split]**, selecione o ícone **+**, seguido por **[!UICONTROL Split]**.

![A opção Dividir está selecionada.](../images/ui/audience-composition/add-split-block.png)

Ao dividir o público, você pode dividir por porcentagem ou dividir por atributo.

### Dividir por porcentagem {#split-percentage}

Ao dividir por porcentagem, os públicos-alvo serão divididos aleatoriamente, com base no número de caminhos e porcentagens fornecidos.

Por exemplo, você pode ter três caminhos, cada um com uma porcentagem diferente de perfis.

![O detalhamento em número de públicos salvos e porcentagens é mostrado.](../images/ui/audience-composition/percentages.png)

### Dividir por atributo {#split-attribute}

Ao dividir por atributo, os públicos-alvo serão divididos com base nos atributos fornecidos. Para selecionar o atributo para divisão, selecione o bloco **[!UICONTROL Split]**, seguido pelo ícone ![filtro](/help/images/icons/project-edit.png).

![O botão Filtrar está selecionado, mostrando como filtrar por atributo.](../images/ui/audience-composition/select-split-attribute.png)

Uma lista de atributos de perfil é exibida. Selecione o tipo de atributo, seguido por **[!UICONTROL Selecionar]** para adicioná-lo ao bloco dividido.

![Uma lista de atributos é exibida.](../images/ui/audience-composition/select-attribute-exclude.png)

Após selecionar o atributo, você pode escolher quais perfis pertencerão a qual subpúblico-alvo adicionando os valores no campo **[!UICONTROL Valores]**.

![Os valores pelos quais você deseja dividir os atributos são adicionados.](../images/ui/audience-composition/attribute-split-values.png)

Além disso, você pode habilitar a opção **[!UICONTROL Outros perfis]** para criar um subpúblico-alvo que inclua todos os perfis não selecionados.

![A opção Outros perfis está realçada.](../images/ui/audience-composition/split-other-profiles.png)

## Publicar seu público

>[!IMPORTANT]
>
>Ao publicar sua composição de público-alvo, observe que pode levar até 48 horas para que ela seja avaliada e ativada para uso em serviços downstream, como um destino do Real-Time CDP ou canal do Adobe Journey Optimizer.

Depois de criar sua composição, você pode salvá-la e publicá-la selecionando **[!UICONTROL Publish]**.

![O botão Publish está realçado, mostrando como salvar e publicar sua composição.](../images/ui/audience-composition/publish.png)

Se houver erros ao criar o público-alvo, um alerta será exibido, informando como resolver o problema.

![O botão Publish está realçado, mostrando como salvar e publicar sua composição.](../images/ui/audience-composition/audience-alert.png)

## Próximas etapas

A Composição de público-alvo fornece um fluxo de trabalho avançado que permite criar composições a partir dos diferentes tipos de blocos. Para saber mais sobre outras partes da interface do usuário do Serviço de segmentação, leia o [Guia do usuário do Serviço de segmentação](./overview.md).
