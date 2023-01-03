---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, API
title: Como configurar um campo de atributo calculado
topic-legacy: guide
type: Documentation
description: Atributos calculados são funções usadas para agregar dados no nível do evento em atributos no nível do perfil. Para configurar um atributo calculado, primeiro é necessário identificar o campo que manterá o valor do atributo calculado. Esse campo pode ser criado usando um grupo de campo de esquema para adicionar o campo a um schema existente ou selecionando um campo que já foi definido em um schema.
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 1%

---


# (Alfa) Configurar um campo de atributo calculado na interface do usuário

>[!IMPORTANT]
>
>A funcionalidade de atributo calculado está atualmente em alfa e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

Para configurar um atributo calculado, primeiro é necessário identificar o campo que manterá o valor do atributo calculado. Esse campo pode ser criado usando um grupo de campo de esquema para adicionar o campo a um schema existente ou selecionando um campo que já foi definido em um schema.

>[!NOTE]
>
>Atributos calculados não podem ser adicionados a campos dentro de grupos de campos definidos por Adobe. O campo deve estar dentro do `tenant` namespace, o que significa que deve ser um campo definido e adicionado a um schema.

Para definir com êxito um campo de atributo calculado, o schema deve ser ativado para [!DNL Profile] e aparecem como parte do schema de união para a classe em que o schema se baseia. Para obter mais informações sobre [!DNL Profile]Esquemas e sindicatos habilitados para o , reveja a seção da [!DNL Schema Registry] seção do guia do desenvolvedor em [habilitar um esquema para Perfil e exibir schemas de união](../../xdm/api/getting-started.md). Também é recomendável revisar a [seção sobre sindicatos](../../xdm/schema/composition.md) na documentação de noções básicas da composição do schema.

O fluxo de trabalho neste tutorial usa um [!DNL Profile]-enabled e segue as etapas para definir um novo grupo de campos contendo o campo de atributo calculado e garantir que ele seja o namespace correto. Se você já tiver um campo que esteja no namespace correto em um esquema Perfil ativado, poderá prosseguir diretamente para a etapa de [criação de um atributo calculado](#create-a-computed-attribute).

## Exibir um esquema

As etapas a seguir usam a interface do usuário do Adobe Experience Platform para localizar um esquema, adicionar um grupo de campos e definir um campo. Se preferir usar a variável [!DNL Schema Registry] Consulte a API [Guia do desenvolvedor do Registro de Schema](../../xdm/api/getting-started.md) para obter etapas sobre como criar um grupo de campos, adicionar um grupo de campos a um schema e ativar um schema para uso com [!DNL Real-Time Customer Profile].

Na interface do usuário, clique em **[!UICONTROL Esquemas]** no painel à esquerda e use a barra de pesquisa no **[!UICONTROL Procurar]** para localizar rapidamente o schema que deseja atualizar.

![](../images/computed-attributes/Schemas-Browse.png)

Depois de localizar o esquema, clique no nome para abrir o [!DNL Schema Editor] onde é possível fazer edições no schema.

![](../images/computed-attributes/Schema-Editor.png)

## Criar um grupo de campos

Para criar um novo grupo de campos, clique em **[!UICONTROL Adicionar]** ao lado de **[!UICONTROL Grupos de campos]** no **[!UICONTROL Composição]** no lado esquerdo do editor. Isso abre o **[!UICONTROL Adicionar grupo de campos]** onde é possível visualizar grupos de campos existentes. Clique no botão de opção para **[!UICONTROL Criar novo grupo de campos]** para definir o novo grupo de campos.

Dê um nome e uma descrição ao grupo de campos e clique em **[!UICONTROL Adicionar grupo de campos]** quando concluído.

![](../images/computed-attributes/Add-field-group.png)

## Adicionar um campo de atributo calculado ao esquema

O novo grupo de campos agora deve aparecer no &quot;[!UICONTROL Grupos de campos]&quot; seção sob &quot;[!UICONTROL Composição]&quot;. Clique no nome do grupo de campos e em vários **[!UICONTROL Adicionar campo]** os botões aparecerão no **[!UICONTROL Estrutura]** do editor.

Selecionar **[!UICONTROL Adicionar campo]** ao lado do nome do schema para adicionar um campo de nível superior, ou você pode selecionar para adicionar o campo em qualquer lugar dentro do schema desejado.

Depois de clicar **[!UICONTROL Adicionar campo]** um novo objeto é aberto, nomeado para a ID do locatário, mostrando que o campo está no namespace correto. Dentro desse objeto, uma **[!UICONTROL Novo campo]** é exibido. Isso se o campo no qual você definirá o atributo calculado.

![](../images/computed-attributes/New-field.png)

## Configurar o campo

Usar o **[!UICONTROL Propriedades do campo]** no lado direito do editor, forneça as informações necessárias para o novo campo, incluindo o nome, o nome de exibição e o tipo.

>[!NOTE]
>
>O tipo do campo deve ser do mesmo tipo que o valor do atributo calculado. Por exemplo, se o valor do atributo calculado for uma string, o campo que está sendo definido no schema deverá ser uma string.

Quando terminar, clique em **[!UICONTROL Aplicar]** e o nome do campo, bem como seu tipo, aparecerão na função **[!UICONTROL Estrutura]** do editor.

![](../images/computed-attributes/Apply.png)

## Habilitar esquema para [!DNL Profile]

Antes de continuar, verifique se o schema foi ativado para [!DNL Profile]. Clique no nome do schema no **[!UICONTROL Estrutura]** seção do editor para que a função **[!UICONTROL Propriedades do esquema]** será exibida. Se a variável **[!UICONTROL Perfil]** o controle deslizante está azul, o esquema foi ativado para [!DNL Profile].

>[!NOTE]
>
>Ativação de um esquema para [!DNL Profile] não pode ser desfeito, portanto, se você clicar no controle deslizante depois de ativá-lo, não será necessário arriscar desabilitá-lo.

![](../images/computed-attributes/Profile.png)

Agora você pode clicar em **[!UICONTROL Salvar]** para salvar o schema atualizado e continuar com o restante do tutorial usando a API.

## Próximas etapas

Agora que você criou um campo no qual o valor do atributo calculado será armazenado, é possível criar o atributo calculado usando o `/computedattributes` Ponto de extremidade da API. Para obter etapas detalhadas sobre como criar um atributo calculado na API, siga as etapas fornecidas no [guia do endpoint da API de atributos calculados](ca-api.md).