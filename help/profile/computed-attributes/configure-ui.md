---
keywords: Experience Platform;perfil;perfil de cliente em tempo real;solução de problemas;API
title: Como configurar um campo de atributo calculado
type: Documentation
description: Os atributos computados são funções usadas para agregar dados no nível do evento em atributos no nível do perfil. Para configurar um atributo calculado, primeiro é necessário identificar o campo que conterá o valor do atributo calculado. Este campo pode ser criado usando um grupo de campos de esquema para adicionar o campo a um esquema existente, ou selecionando um campo que você já definiu em um esquema.
hide: true
hidefromtoc: true
source-git-commit: 5ae7ddbcbc1bc4d7e585ca3e3d030630bfb53724
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 1%

---


# (Alfa) Configurar um campo de atributo calculado na interface do

>[!IMPORTANT]
>
>No momento, a funcionalidade de atributo computada está em alfa e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

Para configurar um atributo calculado, primeiro é necessário identificar o campo que conterá o valor do atributo calculado. Este campo pode ser criado usando um grupo de campos de esquema para adicionar o campo a um esquema existente, ou selecionando um campo que você já definiu em um esquema.

>[!NOTE]
>
>Atributos computados não podem ser adicionados a campos dentro de grupos de campos definidos por Adobe. O campo deve estar dentro de `tenant` namespace, o que significa que deve ser um campo definido e adicionado a um esquema.

Para definir com êxito um campo de atributo calculado, o esquema deve ser habilitado para [!DNL Profile] e aparecem como parte do esquema de união para a classe em que o esquema se baseia. Para obter mais informações sobre [!DNL Profile]esquemas e uniões habilitados para, revise a seção do [!DNL Schema Registry] seção guia do desenvolvedor sobre [ativação de um esquema para Perfil e visualização de esquemas de união](../../xdm/api/getting-started.md). É também recomendável rever a [seção sobre uniões](../../xdm/schema/composition.md) na documentação de noções básicas de composição de esquema.

O fluxo de trabalho deste tutorial usa um [!DNL Profile]Esquema habilitado para e segue as etapas para definir um novo grupo de campos contendo o campo de atributo calculado e garantir que ele seja o namespace correto. Se você já tiver um campo que esteja no namespace correto em um esquema ativado para perfil, continue diretamente para a etapa para [criação de um atributo calculado](#create-a-computed-attribute).

## Exibir um esquema

As etapas a seguir usam a interface do usuário do Adobe Experience Platform para localizar um esquema, adicionar um grupo de campos e definir um campo. Se preferir usar a variável [!DNL Schema Registry] API, consulte a [Guia do desenvolvedor do Registro de esquema](../../xdm/api/getting-started.md) para obter etapas sobre como criar um grupo de campos, adicionar um grupo de campos a um esquema e habilitar um esquema para uso com [!DNL Real-Time Customer Profile].

Na interface do usuário do, clique em **[!UICONTROL Esquemas]** no painel esquerdo e use a barra de pesquisa no **[!UICONTROL Procurar]** para localizar rapidamente o schema que deseja atualizar.

![](../images/computed-attributes/Schemas-Browse.png)

Depois de localizar o esquema, clique em seu nome para abrir a variável [!DNL Schema Editor] onde você pode fazer edições no esquema.

![](../images/computed-attributes/Schema-Editor.png)

## Crie um grupo de campos

Para criar um novo grupo de campos, clique em **[!UICONTROL Adicionar]** ao lado de **[!UICONTROL Grupos de campos]** no **[!UICONTROL Composição]** no lado esquerdo do editor. Isso abre o **[!UICONTROL Adicionar grupo de campos]** caixa de diálogo na qual você pode ver os grupos de campos existentes. Clique no botão de opção para **[!UICONTROL Criar novo grupo de campos]** para definir seu novo grupo de campos.

Dê um nome e uma descrição ao grupo de campos e clique em **[!UICONTROL Adicionar grupo de campos]** quando concluído.

![](../images/computed-attributes/Add-field-group.png)

## Adicionar um campo de atributo calculado ao esquema

Seu novo grupo de campos agora deve aparecer na tag &quot;[!UICONTROL Grupos de campos]seção &quot; em &quot;[!UICONTROL Composição]&quot;. Clique no nome do grupo de campos e selecione vários **[!UICONTROL Adicionar campo]** botões serão exibidos no **[!UICONTROL Estrutura]** seção do editor.

Selecionar **[!UICONTROL Adicionar campo]** ao lado do nome do schema para adicionar um campo de nível superior, ou você pode optar por adicionar o campo em qualquer lugar dentro do schema que preferir.

Depois de clicar em **[!UICONTROL Adicionar campo]** um novo objeto é aberto, nomeado de acordo com sua ID de locatário, mostrando que o campo está no namespace correto. Nesse objeto, uma **[!UICONTROL Novo campo]** é exibida. Isso se for o campo onde você definirá o atributo calculado.

![](../images/computed-attributes/New-field.png)

## Configurar o campo

Usar o **[!UICONTROL Propriedades do campo]** no lado direito do editor, forneça as informações necessárias para o novo campo, incluindo nome, nome de exibição e tipo.

>[!NOTE]
>
>O tipo do campo deve ser o mesmo tipo do valor de atributo calculado. Por exemplo, se o valor do atributo calculado for uma string, o campo que está sendo definido no esquema deverá ser uma string.

Quando terminar, clique em **[!UICONTROL Aplicar]** e o nome do campo, bem como seu tipo, aparecerão no campo **[!UICONTROL Estrutura]** seção do editor.

![](../images/computed-attributes/Apply.png)

## Ativar esquema para [!DNL Profile]

Antes de continuar, verifique se o esquema foi ativado para [!DNL Profile]. Clique no nome do schema no campo **[!UICONTROL Estrutura]** do editor para que a variável **[!UICONTROL Propriedades do esquema]** é exibida. Se a variável **[!UICONTROL Perfil]** estiver azul, o esquema foi ativado para [!DNL Profile].

>[!NOTE]
>
>Ativação de um esquema para [!DNL Profile] não pode ser desfeita, portanto, se você clicar no controle deslizante depois de ativá-lo, não será necessário correr o risco de desativá-lo.

![](../images/computed-attributes/Profile.png)

Clique agora em **[!UICONTROL Salvar]** para salvar o esquema atualizado e continuar com o restante do tutorial usando a API.

## Próximas etapas

Agora que você criou um campo no qual o valor do atributo calculado será armazenado, é possível criar o atributo calculado usando o `/computedattributes` Endpoint da API. Para obter etapas detalhadas sobre como criar um atributo calculado na API, siga as etapas fornecidas na [manual de endpoint da API de atributos computados](ca-api.md).