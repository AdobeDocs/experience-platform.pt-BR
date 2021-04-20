---
keywords: Experience Platform;perfil;perfil do cliente em tempo real;solução de problemas;API
title: Como configurar um campo de atributo calculado
topic: guide
type: Documentation
description: Atributos calculados são funções usadas para agregação de dados no nível do evento em atributos no nível do perfil. Para configurar um atributo calculado, primeiro é necessário identificar o campo que manterá o valor do atributo calculado. Esse campo pode ser criado usando uma combinação para adicionar o campo a um schema existente ou selecionando um campo que você já definiu dentro de um schema.
translation-type: tm+mt
source-git-commit: 92533f732cc14b57d2a0a34ce9afe99554f9af04
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 1%

---


# (Alfa) Configurar um campo de atributo calculado na interface do usuário

>[!IMPORTANT]
>
>A funcionalidade de atributo calculado está atualmente em alfa e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

Para configurar um atributo calculado, primeiro é necessário identificar o campo que manterá o valor do atributo calculado. Esse campo pode ser criado usando uma combinação para adicionar o campo a um schema existente ou selecionando um campo que você já definiu dentro de um schema.

>[!NOTE]
>
>Atributos calculados não podem ser adicionados a campos em combinações definidas por Adobe. O campo deve estar dentro da namespace `tenant`, o que significa que deve ser um campo definido e adicionado a um schema.

Para definir com êxito um campo de atributo calculado, o schema deve ser ativado para [!DNL Profile] e aparecer como parte do schema de união para a classe na qual o schema se baseia. Para obter mais informações sobre uniões e schemas habilitados para [!DNL Profile], consulte a seção do [!DNL Schema Registry] guia do desenvolvedor em [habilitar um schema para Perfis e exibir schemas uniões](../../xdm/api/getting-started.md). Também é recomendável revisar a seção [no união](../../xdm/schema/composition.md) na documentação básica da composição do schema.

O fluxo de trabalho neste tutorial usa um schema habilitado para [!DNL Profile] e segue as etapas para definir uma nova combinação que contém o campo de atributo calculado e garante que seja a namespace correta. Se você já tiver um campo que esteja na namespace correta dentro de um schema habilitado para Perfis, poderá prosseguir diretamente para a etapa para [criar um atributo calculado](#create-a-computed-attribute).

## Visualização de um schema

As etapas a seguir usam a interface do usuário do Adobe Experience Platform para localizar um schema, adicionar uma combinação e definir um campo. Se você preferir usar a API [!DNL Schema Registry], consulte o [Guia do desenvolvedor do Registro de Schemas](../../xdm/api/getting-started.md) para obter as etapas sobre como criar uma combinação, adicionar uma mistura a um schema e ativar um schema para uso com [!DNL Real-time Customer Profile].

Na interface do usuário, clique em **[!UICONTROL Schemas]** no painel esquerdo e use a barra de pesquisa na guia **[!UICONTROL Procurar]** para encontrar rapidamente o schema que deseja atualizar.

![](../images/computed-attributes/Schemas-Browse.png)

Depois de localizar o schema, clique em seu nome para abrir [!DNL Schema Editor], onde você pode fazer edições no schema.

![](../images/computed-attributes/Schema-Editor.png)

## Criar uma mistura

Para criar uma nova mistura, clique em **[!UICONTROL Adicionar]** ao lado de **[!UICONTROL Mixins]** na seção **[!UICONTROL Composição]** no lado esquerdo do editor. Isso abre a caixa de diálogo **[!UICONTROL Adicionar mixin]**, onde você pode ver as misturas existentes. Clique no botão de opção para **[!UICONTROL Criar nova mixin]** para definir sua nova mixin.

Dê um nome e uma descrição ao mixin e clique em **[!UICONTROL Adicionar mixin]** ao concluir.

![](../images/computed-attributes/Add-mixin.png)

## Adicionar um campo de atributo calculado ao schema

Sua nova mistura agora deve aparecer na seção &quot;[!UICONTROL Mixins]&quot; em &quot;[!UICONTROL Composição]&quot;. Clique no nome da combinação e vários botões **[!UICONTROL Adicionar campo]** aparecerão na seção **[!UICONTROL Estrutura]** do editor.

Selecione **[!UICONTROL Adicionar campo]** ao lado do nome do schema para adicionar um campo de nível superior ou selecione para adicionar o campo em qualquer lugar dentro do schema que você preferir.

Depois de clicar em **[!UICONTROL Adicionar campo]**, um novo objeto é aberto, nomeado para sua ID de locatário, mostrando que o campo está na namespace correta. Dentro desse objeto, um **[!UICONTROL Novo campo]** é exibido. Isso se o campo no qual você definirá o atributo calculado.

![](../images/computed-attributes/New-field.png)

## Configurar o campo

Usando a seção **[!UICONTROL Propriedades de campo]** no lado direito do editor, forneça as informações necessárias para o novo campo, incluindo seu nome, nome de exibição e tipo.

>[!NOTE]
>
>O tipo do campo deve ser do mesmo tipo que o valor do atributo calculado. Por exemplo, se o valor do atributo calculado for uma string, o campo que está sendo definido no schema deverá ser uma string.

Quando terminar, clique em **[!UICONTROL Aplicar]** e o nome do campo, bem como o seu tipo, aparecerão na seção **[!UICONTROL Estrutura]** do editor.

![](../images/computed-attributes/Apply.png)

## Ativar schema para [!DNL Profile]

Antes de continuar, verifique se o schema foi ativado para [!DNL Profile]. Clique no nome do schema na seção **[!UICONTROL Estrutura]** do editor para que a guia **[!UICONTROL Propriedades do Schema]** seja exibida. Se o controle deslizante **[!UICONTROL Perfil]** estiver azul, o schema foi ativado para [!DNL Profile].

>[!NOTE]
>
>Não é possível desfazer a ativação de um schema para [!DNL Profile], portanto, se você clicar no controle deslizante depois que ele for ativado, não será necessário arriscar desabilitá-lo.

![](../images/computed-attributes/Profile.png)

Agora você pode clicar em **[!UICONTROL Salvar]** para salvar o schema atualizado e continuar com o restante do tutorial usando a API.

## Próximas etapas

Agora que você criou um campo no qual seu valor de atributo calculado será armazenado, é possível criar o atributo calculado usando o endpoint da API `/computedattributes`. Para obter etapas detalhadas para a criação de um atributo calculado na API, siga as etapas fornecidas no [guia do endpoint da API de atributos calculados](ca-api.md).