---
keywords: Experience Platform; home; tópicos populares; interface do usuário; XDM; sistema XDM; modelo de dados de experiência; Modelo de dados de experiência; Modelo de dados de experiência; Modelo de dados; Modelo de dados; explorar; classe; grupo de campos; tipo de dados; esquema;
solution: Experience Platform
title: Explore recursos XDM na interface do usuário
description: Saiba como explorar esquemas, classes, grupos de campos de esquema e tipos de dados existentes na interface do usuário do Experience Platform.
topic-legacy: tutorial
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 0%

---

# Explore recursos XDM na interface do usuário

No Adobe Experience Platform, todos os recursos do Experience Data Model (XDM) são armazenados no [!DNL Schema Library], incluindo os recursos padrão fornecidos pelo Adobe e os recursos personalizados definidos pela sua organização. Na interface do usuário do Experience Platform, é possível visualizar a estrutura e os campos de qualquer esquema, classe, grupo de campos de esquema ou tipo de dados existente no [!DNL Schema Library]. Isso é especialmente útil ao planejar e preparar a assimilação de dados, pois a interface do usuário fornece informações sobre os tipos de dados esperados e casos de uso de cada campo fornecido por esses recursos XDM.

Este tutorial aborda as etapas para explorar esquemas, classes, grupos de campos e tipos de dados existentes na interface do usuário do Experience Platform.

## Pesquisar um recurso XDM {#lookup}

Na interface do usuário da plataforma, selecione **[!UICONTROL Schemas]** no painel de navegação esquerdo. O espaço de trabalho [!UICONTROL Schemas] fornece uma guia **[!UICONTROL Browse]** para explorar todos os recursos XDM existentes na organização, juntamente com guias dedicadas adicionais para explorar **[!UICONTROL Classes]**, **[!UICONTROL Field groups]** e **[!UICONTROL Data types]** especificamente.

![](../images/ui/explore/tabs.png)

Na guia [!UICONTROL Browse] , você pode usar o ícone de filtro (![Filtrar imagem ícone](../images/ui/explore/icon.png)) para revelar controles no painel esquerdo para restringir os resultados listados.

Por exemplo, para filtrar a lista para mostrar apenas os tipos de dados padrão fornecidos pelo Adobe, selecione **[!UICONTROL Datatype]** e **[!UICONTROL Adobe]** nas seções **[!UICONTROL Type]** e **[!UICONTROL Owner]**, respectivamente.

A opção **[!UICONTROL Included in Profile]** permite filtrar resultados para mostrar apenas recursos que são usados em esquemas que foram habilitados para uso em [Perfil do cliente em tempo real](../../profile/home.md).

![](../images/ui/explore/filter.png)

Você também pode usar a barra de pesquisa para limitar mais os resultados. Quando você pesquisa por um termo, os itens principais representam recursos cujos nomes correspondem à consulta de pesquisa. Abaixo desses itens, em **[!UICONTROL Standard Fields]**, quaisquer recursos contendo campos que correspondam ao query serão listados. Isso permite procurar recursos XDM com base no tipo de dados que eles contêm, sem precisar saber o nome do recurso antecipadamente.

![](../images/ui/explore/search.png)

Quando encontrar o recurso que deseja explorar, selecione o nome na lista para exibir sua estrutura na tela.

## Explore um recurso XDM na tela {#explore}

Após selecionar um recurso, sua estrutura é aberta na tela.

![](../images/ui/explore/canvas.png)

Todos os campos do tipo de objeto que contêm subpropriedades são recolhidos por padrão quando aparecem pela primeira vez na tela. Para mostrar as subpropriedades de qualquer campo, selecione o ícone ao lado de seu nome.

![](../images/ui/explore/field-expand.png)

### Campos gerados pelo sistema {#system-fields}

Alguns nomes de campo são anexados com um sublinhado, como `_repo` e `_id`. Eles representam espaços reservados para campos que o sistema gerará e atribuirá automaticamente quando os dados forem assimilados.

Dessa forma, a maioria desses campos deve ser excluída da estrutura de seus dados ao assimilar na Platform. A principal exceção para essa regra é o campo [`_{TENANT_ID}`](../api/getting-started.md#know-your-tenant_id), no qual todos os campos XDM criados em sua organização devem ser namespacados.

### Tipos de dados {#data-types}

Para cada campo mostrado na tela, o tipo de dados correspondente é mostrado ao lado do nome, indicando imediatamente o tipo de dados que o campo espera para assimilação.

![](../images/ui/explore/data-types.png)

Qualquer tipo de dados anexado com colchetes (`[]`) representa uma matriz desse tipo de dados específico. Por exemplo, um tipo de dados de **[!UICONTROL String]\[]** indica que o campo espera uma matriz de valores da string. Um tipo de dados **[!UICONTROL Payment Item]\[]** indica uma matriz de objetos que estão em conformidade com o tipo de dados [!UICONTROL Payment Item].

Se um campo de matriz for baseado em um tipo de objeto, você poderá selecionar seu ícone na tela para mostrar os atributos esperados para cada item de matriz.

![](../images/ui/explore/array-type.png)

### [!UICONTROL Field properties] {#field-properties}

Ao selecionar o nome de qualquer campo na tela, o painel direito é atualizado para mostrar detalhes sobre esse campo em **[!UICONTROL Field properties]**. Isso pode incluir uma descrição do caso de uso pretendido do campo, valores padrão, padrões, formatos, se o campo é obrigatório ou não, e muito mais.

![](../images/ui/explore/field-properties.png)

Se o campo que você está inspecionando for um campo enum, o painel direito também exibirá os valores aceitáveis que o campo espera receber.

![](../images/ui/explore/enum-field.png)

### Campos de identidade {#identity}

Ao inspecionar esquemas que contêm campos de identidade, esses campos são listados no painel à esquerda, na classe ou grupo de campos que os fornece ao esquema. Selecione o nome do campo de identidade no painel esquerdo para exibir o campo na tela, independentemente de quão profundo ele esteja aninhado.

Os campos de identidade são realçados na tela com um ícone de impressão digital (![Imagem do ícone de impressão digital](../images/ui/explore/identity-symbol.png)). Se você selecionar o nome do campo de identidade, poderá exibir informações adicionais, como [identity namespace](../../identity-service/namespaces.md) e se o campo é ou não a identidade primária para o esquema.

![](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>Consulte o guia em [definindo campos de identidade](./fields/identity.md) para obter mais informações sobre campos de identidade e seu relacionamento com serviços downstream da plataforma.

### Campos de relacionamento {#relationship}

Se você estiver inspecionando um schema que contém um campo de relação, o campo será listado no painel esquerdo em **[!UICONTROL Relationships]**. Selecione o nome do campo de relação no painel esquerdo para revelar o campo na tela, independentemente de quão profundo ele esteja aninhado.

Os campos de relacionamento também são destacados exclusivamente na tela, mostrando o nome do schema de destino ao qual o campo faz referência. Se você selecionar o nome do campo de relação, poderá exibir o namespace de identidade da identidade primária do esquema de destino no painel direito.

![](../images/ui/explore/relationship-field.png)

>[!NOTE]
>
>Consulte o tutorial em [criar uma relação na interface do usuário](../tutorials/create-schema-ui.md) para obter mais informações sobre o uso de relações em esquemas XDM.

## Próximas etapas

Este documento cobriu como explorar recursos XDM existentes na interface do usuário do Experience Platform. Para obter mais informações sobre os diferentes recursos do [!UICONTROL Schemas] espaço de trabalho e [!DNL Schema Editor], consulte a [[!UICONTROL Schemas] visão geral do espaço de trabalho](./overview.md).
