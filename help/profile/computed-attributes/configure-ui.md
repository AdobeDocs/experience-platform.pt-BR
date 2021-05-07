---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, API
title: Como configurar um campo de atributo calculado
topic-legacy: guide
type: Documentation
description: Atributos calculados são funções usadas para agregar dados no nível do evento em atributos no nível do perfil. Para configurar um atributo calculado, primeiro é necessário identificar o campo que manterá o valor do atributo calculado. Esse campo pode ser criado usando um grupo de campo de esquema para adicionar o campo a um schema existente ou selecionando um campo que já foi definido em um schema.
translation-type: tm+mt
source-git-commit: 6e0f7578d0818f88e13b963f64cb2de6729f0574
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 1%

---


# (Alfa) Configurar um campo de atributo calculado na interface do usuário

>[!IMPORTANT]
>
>A funcionalidade de atributo calculado está atualmente em alfa e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

Para configurar um atributo calculado, primeiro é necessário identificar o campo que manterá o valor do atributo calculado. Esse campo pode ser criado usando um grupo de campo de esquema para adicionar o campo a um schema existente ou selecionando um campo que já foi definido em um schema.

>[!NOTE]
>
>Atributos calculados não podem ser adicionados a campos dentro de grupos de campos definidos por Adobe. O campo deve estar dentro do namespace `tenant`, o que significa que ele deve ser um campo definido e adicionado a um schema.

Para definir com êxito um campo de atributo calculado, o schema deve ser ativado para [!DNL Profile] e aparecer como parte do schema de união para a classe em que o schema se baseia. Para obter mais informações sobre schemas e uniões habilitados para [!DNL Profile], consulte a seção da seção do [!DNL Schema Registry] guia do desenvolvedor em [habilitar um schema para Perfil e visualizar schemas de união](../../xdm/api/getting-started.md). Também é recomendável revisar a seção [em uniões](../../xdm/schema/composition.md) na documentação básica da composição do schema.

O workflow neste tutorial usa um schema habilitado para [!DNL Profile] e segue as etapas para definir um novo grupo de campos que contém o campo de atributo calculado e garantir que ele seja o namespace correto. Se você já tiver um campo que esteja no namespace correto em um esquema Perfil ativado, poderá prosseguir diretamente para a etapa para [criar um atributo calculado](#create-a-computed-attribute).

## Exibir um esquema

As etapas a seguir usam a interface do usuário do Adobe Experience Platform para localizar um esquema, adicionar um grupo de campos e definir um campo. Se preferir usar a API [!DNL Schema Registry], consulte o [Guia do desenvolvedor do Registro de Schema](../../xdm/api/getting-started.md) para obter etapas sobre como criar um grupo de campos, adicionar um grupo de campos a um esquema e ativar um esquema para uso com [!DNL Real-time Customer Profile].

Na interface do usuário, clique em **[!UICONTROL Schemas]** no painel à esquerda e use a barra de pesquisa na guia **[!UICONTROL Browse]** para localizar rapidamente o schema que deseja atualizar.

![](../images/computed-attributes/Schemas-Browse.png)

Após localizar o schema, clique em seu nome para abrir o [!DNL Schema Editor], onde é possível fazer edições no schema.

![](../images/computed-attributes/Schema-Editor.png)

## Criar um grupo de campos

Para criar um novo grupo de campos, clique em **[!UICONTROL Add]** ao lado de **[!UICONTROL Field groups]** na seção **[!UICONTROL Composition]** no lado esquerdo do editor. Isso abre a caixa de diálogo **[!UICONTROL Add field group]** onde é possível visualizar grupos de campos existentes. Clique no botão de opção para **[!UICONTROL Create new field group]** para definir o novo grupo de campos.

Dê um nome e uma descrição ao grupo de campos e clique em **[!UICONTROL Add field group]** ao concluir.

![](../images/computed-attributes/Add-field-group.png)

## Adicionar um campo de atributo calculado ao esquema

Seu novo grupo de campos agora deve aparecer na seção &quot;[!UICONTROL Field groups]&quot; em &quot;[!UICONTROL Composition]&quot;. Clique no nome do grupo de campos e vários botões **[!UICONTROL Add field]** aparecerão na seção **[!UICONTROL Structure]** do editor.

Selecione **[!UICONTROL Add field]** ao lado do nome do schema para adicionar um campo de nível superior ou selecione para adicionar o campo em qualquer lugar dentro do schema desejado.

Depois de clicar em **[!UICONTROL Add field]** um novo objeto é aberto, nomeado para a ID do locatário, mostrando que o campo está no namespace correto. Dentro desse objeto, um **[!UICONTROL New field]** é exibido. Isso se o campo no qual você definirá o atributo calculado.

![](../images/computed-attributes/New-field.png)

## Configurar o campo

Usando a seção **[!UICONTROL Field properties]** no lado direito do editor, forneça as informações necessárias para seu novo campo, incluindo nome, nome de exibição e tipo.

>[!NOTE]
>
>O tipo do campo deve ser do mesmo tipo que o valor do atributo calculado. Por exemplo, se o valor do atributo calculado for uma string, o campo que está sendo definido no schema deverá ser uma string.

Quando terminar, clique em **[!UICONTROL Apply]** e o nome do campo, bem como seu tipo, aparecerão na seção **[!UICONTROL Structure]** do editor.

![](../images/computed-attributes/Apply.png)

## Habilitar esquema para [!DNL Profile]

Antes de continuar, verifique se o schema foi ativado para [!DNL Profile]. Clique no nome do schema na seção **[!UICONTROL Structure]** do editor para que a guia **[!UICONTROL Schema Properties]** seja exibida. Se o controle deslizante **[!UICONTROL Profile]** estiver azul, o esquema foi ativado para [!DNL Profile].

>[!NOTE]
>
>Não é possível desfazer a ativação de um esquema para [!DNL Profile], portanto, se você clicar no controle deslizante depois de ativá-lo, não será necessário arriscar desabilitá-lo.

![](../images/computed-attributes/Profile.png)

Agora você pode clicar em **[!UICONTROL Save]** para salvar o esquema atualizado e continuar com o resto do tutorial usando a API.

## Próximas etapas

Agora que você criou um campo no qual o valor do atributo calculado será armazenado, é possível criar o atributo calculado usando o endpoint da API `/computedattributes` . Para obter etapas detalhadas para criar um atributo calculado na API, siga as etapas fornecidas no [guia do ponto de extremidade da API de atributos calculados](ca-api.md).