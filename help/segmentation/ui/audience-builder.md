---
keywords: Experience Platform, inicial, tópicos populares, Serviço de segmentação, segmentação, serviço de segmentação, guia do usuário, guia da interface do usuário, guia de interface do público-alvo, construtor de público-alvo, público-alvo, públicos-alvo, guia de interface do usuário de públicos-alvo;
solution: Experience Platform
title: Guia da interface do usuário do Audiences
topic-legacy: ui guide
description: O Audience Builder na interface do usuário do Adobe Experience Platform fornece um espaço de trabalho avançado que permite interagir com elementos de dados do perfil. A área de trabalho oferece controles intuitivos para criar e editar públicos-alvo para sua organização.
hide: true
hidefromtoc: true
source-git-commit: f71d49b576059e687c337cbacd6dd3d525e97834
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 1%

---

# Guia da interface do usuário do Audience Builder

>[!IMPORTANT]
>
>O Audience Builder está atualmente na versão beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

O Audience Builder fornece um espaço de trabalho para criar e editar públicos, usando blocos usados para representar ações diferentes.

![A interface do usuário do Audience Builder.](../images/ui/audience-builder/audience-builder.png)

A tela de composição do público-alvo é composta por cinco tipos diferentes de blocos: **[[!UICONTROL Público]](#audience-block)**, **[[!UICONTROL Excluir]](#exclude-block)**, **[[!UICONTROL Associar-se]](#join-block)**, **[[!UICONTROL Classificação]](#rank-block)** e **[[!UICONTROL Split]](#split-block)**.

## [!UICONTROL Público-alvo] {#audience-block}

O **[!UICONTROL Público]** O tipo de bloco permite adicionar os subpúblicos-alvo que você deseja compor ao novo público-alvo maior. Por padrão, uma **[!UICONTROL Público]** é incluído na parte superior da tela de composição.

Ao selecionar a variável **[!UICONTROL Público]** , o painel direito exibe controles para rotular e adicionar públicos ao bloco.

![Os detalhes do bloco Público-alvo são exibidos.](../images/ui/audience-builder/select-audience.png)

Depois de selecionar **[!UICONTROL Adicionar público-alvo]**, uma lista de públicos-alvo é exibida. Selecione os públicos que deseja incluir, seguido de **[!UICONTROL Adicionar]** para anexá-los ao bloco de público-alvo.

![Uma lista de públicos-alvo é exibida. Você pode selecionar qual público-alvo deseja adicionar nesta caixa de diálogo.](../images/ui/audience-builder/select-audience.png)

Seus públicos-alvo selecionados agora aparecem no painel direito quando a variável **[!UICONTROL Público]** estiver selecionado. A partir daqui, você pode alterar o tipo de mesclagem dos públicos-alvo combinados.

![Os possíveis tipos de mesclagem para os públicos-alvo são destacados.](../images/ui/audience-builder/merge-types.png)

| Tipo de mesclagem | Descrição |
| ---------- | ----------- |
| [!UICONTROL União] | Os públicos-alvo são combinados em um único público-alvo. Isso seria equivalente a uma operação OR. |
| [!UICONTROL Interseção] | Os públicos-alvo são combinados, somente com os públicos-alvo compartilhados em **all** dos quais foram adicionados. Isso seria equivalente a uma operação AND. |
| [!UICONTROL Excluir sobreposição] | Os públicos-alvo são combinados, somente com os públicos-alvo compartilhados em **um, mas não todos** dos quais foram adicionados. Isso seria equivalente a uma operação XOR. |

## [!UICONTROL Excluir] {#exclude-block}

O **[!UICONTROL Excluir]** O tipo de bloco permite excluir subpúblicos ou atributos especificados do novo público-alvo maior.

Para adicionar uma **[!UICONTROL Excluir]** , selecione o **+** ícone, seguido por **[!UICONTROL Excluir]**.

![A opção Exclude está selecionada.](../images/ui/audience-builder/add-exclude-block.png)

O **[!UICONTROL Excluir]** é adicionado. Quando este bloco é selecionado, os detalhes sobre a exclusão são exibidos no painel direito. Isso inclui o rótulo do bloco e o tipo de exclusão. Você pode excluir [por público](#exclude-audience) ou [por atributo](#exclude-attribute).

![O bloco Excluir , destacando os dois tipos de exclusão diferentes disponíveis.](../images/ui/audience-builder/exclude.png)

### Excluir por público-alvo {#exclude-audience}

Se você excluir por público-alvo, é possível selecionar quais públicos deseja excluir selecionando **[!UICONTROL Adicionar público-alvo]**.

![O botão Add audience é selecionado, que permite escolher qual público-alvo deseja excluir.](../images/ui/audience-builder/add-excluded-audience.png)

Uma lista de públicos-alvo é exibida. Selecionar **[!UICONTROL Adicionar]** para adicionar os públicos-alvo que deseja excluir ao seu bloco de exclusão.

![Uma lista de públicos-alvo é exibida. Você pode selecionar qual público-alvo deseja adicionar nesta caixa de diálogo.](../images/ui/audience-builder/select-audience.png)

### Excluir por atributo {#exclude-attribute}

Se você excluir por atributo, é possível selecionar quais atributos deseja excluir selecionando o ![filter](../images/ui/audience-builder/filter-attribute.png) no ícone **[!UICONTROL Regra de exclusão]** seção.

![A seção do atributo é realçada, mostrando onde selecionar o atributo a ser excluído.](../images/ui/audience-builder/exclude-attribute.png)

Uma lista de atributos de perfil é exibida. Selecione o tipo de atributo que deseja excluir, seguido de **[!UICONTROL Selecionar]** para adicioná-las ao bloco de exclusão.

![Uma lista de atributos é exibida.](../images/ui/audience-builder/select-attribute.png)

## [!UICONTROL Ingressar] {#join-block}

O **[!UICONTROL Associar-se]** tipo de bloco permite adicionar públicos externos a partir de conjuntos de dados que ainda não foram processados pelo Adobe Experience Platform.

Para adicionar uma **[!UICONTROL Associar-se]** , selecione o **+** ícone, seguido por **[!UICONTROL Associar-se]**.

![A opção Join é selecionada.](../images/ui/audience-builder/add-join-block.png)

Ao selecionar o bloco, os detalhes sobre a associação são mostrados no painel direito, incluindo o rótulo do bloco e a opção para adicionar públicos ao conjunto de dados de enriquecimento.

![O bloco de associação é destacado, incluindo detalhes sobre o bloco de associação.](../images/ui/audience-builder/join.png)

Depois de selecionar **[!UICONTROL Adicionar público-alvo]**, uma lista de públicos-alvo é exibida. Selecione os públicos que deseja incluir, seguido de **[!UICONTROL Adicionar]** para adicioná-las ao bloco de associação.

![Uma lista de públicos-alvo é exibida. Você pode selecionar qual público-alvo deseja adicionar nesta caixa de diálogo.](../images/ui/audience-builder/select-audience.png)

Seus públicos-alvo selecionados agora aparecem no painel direito quando a variável **[!UICONTROL Associar-se]** estiver selecionado.

![Os públicos-alvo adicionados como parte da Junção são mostrados.](../images/ui/audience-builder/selected-audiences.png)

## [!UICONTROL Classificação] {#rank-block}

O **[!UICONTROL Classificação]** O tipo de bloco permite classificar e classificar os públicos-alvo antes que o novo público-alvo seja publicado.

Para adicionar uma **[!UICONTROL Classificação]** , selecione o **+** ícone, seguido por **[!UICONTROL Classificação]**.

![A opção Classificação está selecionada.](../images/ui/audience-builder/add-rank-block.png)

Ao selecionar o bloco, os detalhes sobre a classificação são mostrados no painel direito, incluindo o rótulo do bloco, o atributo para classificar, a ordem de classificação e um botão para limitar o número de perfis a serem classificados.

![O bloco de classificação é realçado, bem como os detalhes do bloco de classificação.](../images/ui/audience-builder/rank.png)

Para selecionar qual atributo deve ser classificado pelos públicos-alvo, selecione o ![filter](../images/ui/audience-builder/filter-attribute.png) ícone .

![O ícone de filtro é realçado e mostra o que selecionar para acessar a tela de seleção de atributos do perfil.](../images/ui/audience-builder/select-rank-attribute.png)

Uma lista de atributos de perfil é exibida. Nesse caso, você pode selecionar o tipo de atributo pelo qual deseja classificar seu público-alvo. Selecionar **[!UICONTROL Selecionar]** para adicioná-lo ao bloco de classificação. Observe que o atributo selecionado pode **only** ser do tipo `int`.

![Uma lista de atributos é exibida.](../images/ui/audience-builder/select-attribute.png)

Após selecionar o atributo, você pode selecionar a ordem para classificá-lo. Isso é em ordem crescente (do mais baixo ao mais alto) ou decrescente (do mais alto ao mais baixo).

Além disso, é possível limitar o número de públicos-alvo retornados ao ativar a **[!UICONTROL Adicionar limite de perfil]** alternar. Quando essa alternância estiver ativada, você poderá definir o número máximo de públicos-alvo retornados na variável **[!UICONTROL Perfis incluídos]** campo.

![A opção Add profile limit é realçada, permitindo limitar o número de públicos-alvo retornados.](../images/ui/audience-builder/add-profile-limit.png)

## [!UICONTROL Dividir] {#split-block}

O **[!UICONTROL Split]** tipo de bloco permite dividir o novo público em vários subpúblicos. Você pode dividir esse público-alvo com base na porcentagem ou por um atributo.

Para adicionar uma **[!UICONTROL Split]** , selecione o **+** ícone, seguido por **[!UICONTROL Split]**.

![A opção Split é selecionada.](../images/ui/audience-builder/add-split-block.png)

### Dividir por porcentagem {#split-percentage}

Ao dividir por porcentagem, os públicos-alvo serão divididos aleatoriamente, com base no número de caminhos e porcentagens fornecidas.

Por exemplo, você pode ter três caminhos, cada um com uma porcentagem diferente de perfis.

![O detalhamento em número de públicos-alvo salvos e porcentagens é mostrado.](../images/ui/audience-builder/percentages.png)

Além disso, você pode marcar um dos públicos-alvo divididos para ser o grupo de controle.

![A alternância de grupo de controle está ativada. Isso permite marcar um dos públicos-alvo divididos como um grupo de controle.](../images/ui/audience-builder/control-group.png)

### Dividir por atributo {#split-attribute}

Ao dividir por atributo, os públicos-alvo serão divididos com base nos atributos fornecidos. Para selecionar o atributo que será dividido por, selecione o **[!UICONTROL Split]** , seguido pelo ![filter](../images/ui/audience-builder/filter-attribute.png) ícone .

![O botão de filtro é selecionado, mostrando como filtrar por atributo.](../images/ui/audience-builder/select-attribute-split.png)

Uma lista de atributos de perfil é exibida. Selecione o tipo de atributo, seguido por **[!UICONTROL Selecionar]** para adicioná-lo ao bloco dividido.

![Uma lista de atributos é exibida.](../images/ui/audience-builder/select-attribute.png)

Após selecionar o atributo , você pode escolher quais perfis pertencerão a qual subpúblico-alvo, adicionando os valores em **[!UICONTROL Valores]** campo.

![Os valores que você deseja dividir os atributos por são adicionados.](../images/ui/audience-builder/attribute-split-values.png)

Além disso, é possível ativar a variável **[!UICONTROL Outros perfis]** alterne para criar um subpúblico-alvo que inclua todos os perfis não selecionados.

![A opção Other profiles é realçada.](../images/ui/audience-builder/attribute-split-other-profiles.png)

## Publicar seu público

Depois de compor seu público-alvo, você pode salvá-lo e publicá-lo selecionando **[!UICONTROL Publicar]**.

![O botão Publicar é destacado, mostrando como salvar e publicar seu público-alvo.](../images/ui/audience-builder/publish-audience.png)

Se houver erros na criação do público-alvo, será exibido um alerta informando como resolver o problema.

![O botão Publicar é destacado, mostrando como salvar e publicar seu público-alvo.](../images/ui/audience-builder/audience-alert.png)

## Próximas etapas

O Audience Builder fornece um fluxo de trabalho avançado que permite criar públicos-alvo a partir de diferentes tipos de blocos. Para saber mais sobre outras partes da interface do usuário do serviço de segmentação, leia o [Guia do usuário do Serviço de segmentação](./overview.md).