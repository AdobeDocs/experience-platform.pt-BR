---
keywords: Experience Platform;página inicial;tópicos populares;Serviço de segmentação;segmentação;serviço de segmentação;guia do usuário;guia da interface do usuário;guia da interface do usuário de públicos-alvo;construtor de público-alvo;público-alvo;públicos-alvo;guia da interface do usuário de públicos-alvo;
solution: Experience Platform
title: Guia da interface do usuário de públicos
description: O Construtor de público-alvo na interface do usuário do Adobe Experience Platform fornece um espaço de trabalho avançado que permite a interação com elementos de dados do perfil. O espaço de trabalho fornece controles intuitivos para criação e edição de públicos-alvo para sua organização.
hide: true
hidefromtoc: true
exl-id: 0dda0cb1-49e0-478b-8004-84572b6cf625
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 1%

---

# Guia da interface do usuário do Audience Builder

>[!IMPORTANT]
>
>No momento, o Construtor de público-alvo está na versão beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

O Construtor de público-alvo fornece um espaço de trabalho para construir e editar públicos-alvo, usando blocos usados para representar ações diferentes.

![A interface do usuário do Audience Builder.](../images/ui/audience-builder/audience-builder.png)

A tela de composição de público-alvo é composta por cinco tipos diferentes de blocos: **[[!UICONTROL Público]](#audience-block)**, **[[!UICONTROL Excluir]](#exclude-block)**, **[[!UICONTROL Ingressar]](#join-block)**, **[[!UICONTROL Classificação]](#rank-block)**, e **[[!UICONTROL Split]](#split-block)**.

## [!UICONTROL Público-alvo] {#audience-block}

A variável **[!UICONTROL Público]** O tipo de bloco permite adicionar os subpúblicos que você deseja compor para seu novo público-alvo maior. Por padrão, uma variável **[!UICONTROL Público]** bloco é incluído na parte superior da tela de composição.

Ao selecionar a variável **[!UICONTROL Público]** , o painel direito exibe controles para rotular e adicionar públicos-alvo ao bloco.

![Os detalhes do bloco de Público-alvo são exibidos.](../images/ui/audience-builder/select-audience.png)

Depois de selecionar **[!UICONTROL Adicionar público-alvo]**, uma lista de públicos-alvo é exibida. Selecione os públicos que deseja incluir, seguido por **[!UICONTROL Adicionar]** para anexá-los ao bloco de público-alvo.

![Uma lista de públicos-alvo é exibida. Você pode selecionar qual público-alvo deseja adicionar nesta caixa de diálogo.](../images/ui/audience-builder/select-audience.png)

Os públicos-alvo selecionados agora aparecem no painel direito quando a **[!UICONTROL Público]** for selecionado. Aqui, é possível alterar o tipo de mesclagem dos públicos-alvo combinados.

![Os possíveis tipos de mesclagem para os públicos-alvo são destacados.](../images/ui/audience-builder/merge-types.png)

| Tipo de mesclagem | Descrição |
| ---------- | ----------- |
| [!UICONTROL União] | Os públicos são combinados em um único público. Isso seria equivalente a uma operação OR. |
| [!UICONTROL Interseção] | Os públicos-alvo são combinados, com apenas os públicos-alvo compartilhados no **all** delas sendo adicionadas. Isso seria equivalente a uma operação AND. |
| [!UICONTROL Excluir sobreposição] | Os públicos-alvo são combinados, com apenas os públicos-alvo compartilhados no **um, mas não todos** delas sendo adicionadas. Isso seria o equivalente a uma operação XOR. |

## [!UICONTROL Excluir] {#exclude-block}

A variável **[!UICONTROL Excluir]** o tipo de bloco permite excluir subpúblicos-alvo ou atributos especificados do novo público-alvo maior.

Para adicionar um **[!UICONTROL Excluir]** selecione o **+** ícone, seguido por **[!UICONTROL Excluir]**.

![A opção Excluir está selecionada.](../images/ui/audience-builder/add-exclude-block.png)

A variável **[!UICONTROL Excluir]** bloco é adicionado. Quando esse bloco for selecionado, os detalhes sobre a exclusão aparecerão no painel direito. Isso inclui o rótulo do bloco e o tipo de exclusão. Você pode excluir [por público-alvo](#exclude-audience) ou [por atributo](#exclude-attribute).

![O bloco Excluir, destacando os dois tipos de exclusão diferentes disponíveis.](../images/ui/audience-builder/exclude.png)

### Excluir por público {#exclude-audience}

Se excluir por público, você pode selecionar quais públicos deseja excluir selecionando **[!UICONTROL Adicionar público-alvo]**.

![O botão Adicionar público-alvo é selecionado e permite escolher qual público-alvo deseja excluir.](../images/ui/audience-builder/add-excluded-audience.png)

Uma lista de públicos-alvo é exibida. Selecionar **[!UICONTROL Adicionar]** para adicionar os públicos-alvo que você deseja excluir ao bloco excluir.

![Uma lista de públicos-alvo é exibida. Você pode selecionar qual público-alvo deseja adicionar nesta caixa de diálogo.](../images/ui/audience-builder/select-audience.png)

### Excluir por atributo {#exclude-attribute}

Se você excluir por atributo, poderá selecionar quais atributos deseja excluir selecionando o ![filtro](../images/ui/audience-builder/filter-attribute.png) ícone dentro do **[!UICONTROL Regra de exclusão]** seção.

![A seção attribute é destacada, mostrando onde escolher o atributo a ser excluído.](../images/ui/audience-builder/exclude-attribute.png)

Uma lista de atributos de perfil é exibida. Selecione o tipo de atributo que deseja excluir, seguido por **[!UICONTROL Selecionar]** para adicioná-los ao bloco excluir.

![Uma lista de atributos é exibida.](../images/ui/audience-builder/select-attribute.png)

## [!UICONTROL Ingressar] {#join-block}

A variável **[!UICONTROL Ingressar]** o tipo de bloco permite adicionar públicos-alvo externos de conjuntos de dados que ainda não foram processados pelo Adobe Experience Platform.

Para adicionar um **[!UICONTROL Ingressar]** selecione o **+** ícone, seguido por **[!UICONTROL Ingressar]**.

![A opção Unir está selecionada.](../images/ui/audience-builder/add-join-block.png)

Ao selecionar o bloco, os detalhes sobre a associação são mostrados no painel direito, incluindo o rótulo do bloco e a opção para adicionar públicos-alvo ao conjunto de dados de enriquecimento.

![O bloco de junção é destacado, incluindo detalhes sobre o bloco de junção.](../images/ui/audience-builder/join.png)

Depois de selecionar **[!UICONTROL Adicionar público-alvo]**, uma lista de públicos-alvo é exibida. Selecione os públicos que deseja incluir, seguido por **[!UICONTROL Adicionar]** para adicioná-los ao seu bloco de junção.

![Uma lista de públicos-alvo é exibida. Você pode selecionar qual público-alvo deseja adicionar nesta caixa de diálogo.](../images/ui/audience-builder/select-audience.png)

Os públicos-alvo selecionados agora aparecem no painel direito quando a **[!UICONTROL Ingressar]** for selecionado.

![Os públicos-alvo que foram adicionados como parte da associação são mostrados.](../images/ui/audience-builder/selected-audiences.png)

## [!UICONTROL Classificação] {#rank-block}

A variável **[!UICONTROL Classificação]** o tipo de bloco permite classificar os públicos-alvo antes que o novo público-alvo seja publicado.

Para adicionar um **[!UICONTROL Classificação]** selecione o **+** ícone, seguido por **[!UICONTROL Classificação]**.

![A opção Rank é selecionada.](../images/ui/audience-builder/add-rank-block.png)

Ao selecionar o bloco, os detalhes sobre a classificação são mostrados no painel direito, incluindo o rótulo do bloco, o atributo para classificar, a ordem de classificação e um botão para limitar o número de perfis a serem classificados.

![O bloco de classificação é destacado, bem como os detalhes do bloco de classificação.](../images/ui/audience-builder/rank.png)

Para selecionar por atributo classificar os públicos, selecione o ![filtro](../images/ui/audience-builder/filter-attribute.png) ícone.

![O ícone de filtro é realçado, mostrando o que selecionar para acessar a tela de seleção de atributo de perfil.](../images/ui/audience-builder/select-rank-attribute.png)

Uma lista de atributos de perfil é exibida. Nesse popover, você pode selecionar o tipo de atributo pelo qual deseja classificar seu público-alvo. Selecionar **[!UICONTROL Selecionar]** para adicioná-lo ao bloco de classificação. Observe que o atributo selecionado pode **somente** ser do tipo `int`.

![Uma lista de atributos é exibida.](../images/ui/audience-builder/select-attribute.png)

Depois de selecionar o atributo, você pode selecionar a ordem pela qual ele será classificado. É em ordem crescente (do mais baixo para o mais alto) ou decrescente (do mais alto para o mais baixo).

Além disso, é possível limitar o número de públicos-alvo retornados ativando o **[!UICONTROL Adicionar limite de perfil]** alternar. Quando essa opção estiver ativada, você poderá definir o número máximo de públicos-alvo retornados na variável **[!UICONTROL Perfis incluídos]** campo.

![A opção Add profile limit está realçada, o que permite limitar o número de públicos-alvo retornados.](../images/ui/audience-builder/add-profile-limit.png)

## [!UICONTROL Dividir] {#split-block}

A variável **[!UICONTROL Split]** o tipo de bloco permite dividir o novo público em vários subpúblicos. Você pode dividir esse público com base na porcentagem ou por um atributo.

Para adicionar um **[!UICONTROL Split]** selecione o **+** ícone, seguido por **[!UICONTROL Split]**.

![A opção Split é selecionada.](../images/ui/audience-builder/add-split-block.png)

### Dividir por porcentagem {#split-percentage}

Ao dividir por porcentagem, os públicos-alvo serão divididos aleatoriamente, com base no número de caminhos e porcentagens fornecidos.

Por exemplo, você pode ter três caminhos, cada um com uma porcentagem diferente de perfis.

![O detalhamento em número de públicos-alvo salvos e porcentagens é exibido.](../images/ui/audience-builder/percentages.png)

Além disso, você pode marcar um dos públicos-alvo divididos como o grupo de controle.

![A alternância do grupo de controle está habilitada. Isso permite marcar um dos públicos-alvo divididos para ser um grupo de controle.](../images/ui/audience-builder/control-group.png)

### Dividir por atributo {#split-attribute}

Ao dividir por atributo, os públicos-alvo serão divididos com base nos atributos fornecidos. Para selecionar o atributo pelo qual dividir, selecione o **[!UICONTROL Split]** bloco, seguido pelo ![filtro](../images/ui/audience-builder/filter-attribute.png) ícone.

![O botão de filtro é selecionado, mostrando como filtrar por atributo.](../images/ui/audience-builder/select-attribute-split.png)

Uma lista de atributos de perfil é exibida. Selecione o tipo de atributo, seguido por **[!UICONTROL Selecionar]** para adicioná-lo ao bloco dividido.

![Uma lista de atributos é exibida.](../images/ui/audience-builder/select-attribute.png)

Depois de selecionar o atributo, escolha a quais perfis pertencerão cada subpúblico-alvo adicionando os valores em **[!UICONTROL Valores]** campo.

![Os valores pelos quais você deseja dividir os atributos são adicionados.](../images/ui/audience-builder/attribute-split-values.png)

Além disso, você pode ativar a variável **[!UICONTROL Outros perfis]** alterne para criar um subpúblico-alvo que inclua todos os perfis não selecionados.

![A opção Other profiles é realçada.](../images/ui/audience-builder/attribute-split-other-profiles.png)

## Publicar seu público

Depois de compor o público-alvo, você pode salvá-lo e publicá-lo selecionando **[!UICONTROL Publish]**.

![O botão Publicar é realçado, mostrando como salvar e publicar seu público-alvo.](../images/ui/audience-builder/publish-audience.png)

Se houver erros ao criar o público-alvo, um alerta será exibido, informando como resolver o problema.

![O botão Publicar é realçado, mostrando como salvar e publicar seu público-alvo.](../images/ui/audience-builder/audience-alert.png)

## Próximas etapas

O Construtor de público-alvo fornece um fluxo de trabalho avançado que permite criar públicos-alvo a partir de diferentes tipos de blocos. Para saber mais sobre outras partes da interface do usuário do Serviço de segmentação, leia o [Guia do usuário do Serviço de segmentação](./overview.md).
