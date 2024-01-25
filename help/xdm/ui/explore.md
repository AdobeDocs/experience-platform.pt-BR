---
keywords: Experience Platform;página inicial;tópicos populares;interface do usuário;XDM;sistema XDM;modelo de dados de experiência;modelo de dados de experiência;modelo de dados de experiência;modelo de dados;modelo de dados;explorar;classe;grupo de campos;tipo de dados;esquema;
solution: Experience Platform
title: Explorar recursos do esquema na interface do
description: Saiba como explorar esquemas, classes, grupos de campos de esquema e tipos de dados existentes na interface do usuário do Experience Platform.
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 0%

---

# Explorar recursos de esquema na interface do

No Adobe Experience Platform, todos os recursos do esquema do Experience Data Model (XDM) são armazenados no [!DNL Schema Library], incluindo recursos padrão fornecidos pelo Adobe e recursos personalizados definidos pela sua organização. Na interface do usuário do Experience Platform, é possível visualizar a estrutura e os campos de qualquer esquema, classe, grupo de campos ou tipo de dados existente no [!DNL Schema Library]. Isso é especialmente útil ao planejar e se preparar para a assimilação de dados, pois a interface do usuário fornece informações sobre os tipos de dados e casos de uso esperados de cada campo fornecido por esses recursos XDM.

Este tutorial aborda as etapas para explorar esquemas, classes, grupos de campos e tipos de dados existentes na interface do usuário do Experience Platform.

## Pesquisar um recurso de esquema {#lookup}

Na interface do usuário da Platform, selecione **[!UICONTROL Esquemas]** no painel de navegação esquerdo. A variável [!UICONTROL Esquemas] o espaço de trabalho fornece uma **[!UICONTROL Procurar]** para explorar todos os esquemas em sua organização, juntamente com guias dedicadas adicionais para exploração **[!UICONTROL Classes]**, **[!UICONTROL Grupos de campos]**, e **[!UICONTROL Tipos de dados]** respectivamente.

![](../images/ui/explore/tabs.png)

O ícone de filtro (![Filtrar imagem do ícone](../images/ui/explore/icon.png)) revela controles no painel esquerdo para restringir os resultados listados. Os controles exibidos diferem dependendo do tipo de recurso que está sendo listado.

Por exemplo, para filtrar a lista de forma a mostrar apenas os tipos de dados padrão fornecidos pelo Adobe, selecione **[!UICONTROL Tipo de dados]** e **[!UICONTROL Adobe]** no **[!UICONTROL Tipo]** e **[!UICONTROL Proprietário]** seções, respectivamente.

A variável **[!UICONTROL Incluído no perfil]** permite filtrar os resultados para mostrar apenas os recursos usados em esquemas que foram habilitados para uso em [Perfil do cliente em tempo real](../../profile/home.md). A variável **[!UICONTROL Mostrar esquemas adhoc]** ativar/desativar filtra a lista de esquemas criados com campos com namespace para uso somente por um único conjunto de dados.

![A variável [!UICONTROL Esquemas] espaço de trabalho [!UICONTROL Procurar] com o painel filtros realçado.](../images/ui/explore/filter.png)

Ao listar recursos no **[!UICONTROL Classes]**, **[!UICONTROL Grupos de campos]** ou **[!UICONTROL Tipos de dados]** , é possível selecionar **[!UICONTROL Adobe]** para mostrar apenas os recursos padrão ou **[!UICONTROL Cliente]** para mostrar apenas os recursos criados por sua organização.

![](../images/ui/explore/filter-data-type.png)

Você também pode usar a barra de pesquisa para restringir ainda mais os resultados.

![](../images/ui/explore/search.png)

Os recursos exibidos nos resultados da pesquisa são ordenados primeiro por correspondências de título e, em seguida, por correspondências de descrição. Por sua vez, quanto mais palavras corresponderem em uma dessas categorias, maior será o recurso exibido na lista.

Depois de encontrar o recurso que deseja explorar, selecione o nome dele na lista para exibir sua estrutura na tela.

## Explorar um recurso XDM na tela {#explore}

Depois de selecionar um recurso, sua estrutura é aberta na tela.

![](../images/ui/explore/canvas.png)

Todos os campos do tipo de objeto que contêm subpropriedades são recolhidos por padrão quando aparecem pela primeira vez na tela. Para mostrar as subpropriedades de qualquer campo, selecione o ícone ao lado do nome.

![](../images/ui/explore/field-expand.png)

### Campos gerados pelo sistema {#system-fields}

Alguns nomes de campo recebem um sublinhado como `_repo` e `_id`. Eles representam espaços reservados para campos que o sistema gerará e atribuirá automaticamente à medida que os dados forem assimilados.

Dessa forma, a maioria desses campos deve ser excluída da estrutura dos dados ao assimilar na Platform. A principal exceção a esta regra é a [`_{TENANT_ID}` campo](../api/getting-started.md#know-your-tenant_id), em que todos os campos XDM criados em sua organização devem ter o namespace.

### Tipos de dados {#data-types}

Para cada campo mostrado na tela, seu tipo de dados correspondente é mostrado ao lado do nome, indicando rapidamente o tipo de dados que o campo espera para assimilação.

![](../images/ui/explore/data-types.png)

Qualquer tipo de dados anexado com colchetes (`[]`) representa uma matriz desse tipo de dados específico. Por exemplo, um tipo de dados de **[!UICONTROL String]\[]** indica que o campo espera uma matriz de valores de sequência. Um tipo de dados de **[!UICONTROL Item de pagamento]\[]** indica uma matriz de objetos que estão em conformidade com [!UICONTROL Item de pagamento] tipo de dados.

Se um campo de matriz é baseado em um tipo de objeto, você pode selecionar seu ícone na tela para mostrar os atributos esperados para cada item de matriz.

![](../images/ui/explore/array-type.png)

### [!UICONTROL Propriedades do campo] {#field-properties}

Ao selecionar o nome de qualquer campo na tela, o painel direito é atualizado para mostrar detalhes sobre esse campo em **[!UICONTROL Propriedades do campo]**. Isso pode incluir uma descrição do caso de uso pretendido do campo, valores padrão, padrões, formatos, se o campo é obrigatório ou não e muito mais.

![](../images/ui/explore/field-properties.png)

Se o campo que você está inspecionando for um campo de enumeração, o painel direito também exibirá os valores aceitáveis que o campo espera receber.

![](../images/ui/explore/enum-field.png)

### Campos de identidade {#identity}

Ao inspecionar esquemas que contêm campos de identidade, esses campos são listados no painel à esquerda na classe ou no grupo de campos que os fornece ao esquema. Selecione o nome do campo de identidade no painel à esquerda para revelar o campo na tela, independentemente da profundidade em que ele está aninhado.

Os campos de identidade são realçados na tela com um ícone de impressão digital (![Imagem do ícone de impressão digital](../images/ui/explore/identity-symbol.png)). Se você selecionar o nome do campo de identidade, poderá exibir informações adicionais, como a variável [namespace de identidade](../../identity-service/features/namespaces.md) e se o campo é ou não a identidade principal do esquema.

![](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>Consulte o guia sobre [definição de campos de identidade](./fields/identity.md) para obter mais informações sobre campos de identidade e seu relacionamento com os serviços downstream da Platform.

### Campos de relacionamento {#relationship}

Se você estiver inspecionando um esquema que contém um campo de relação, o campo será listado no painel à esquerda em **[!UICONTROL Relações]**. Selecione o nome do campo de relacionamento no painel à esquerda para revelar o campo na tela, independentemente da profundidade em que ele está aninhado.

Os campos de relacionamento também são destacados exclusivamente na tela, mostrando o nome do esquema de referência ao qual o campo é vinculado. Se você selecionar o nome do campo de relacionamento, poderá exibir o namespace de identidade da identidade principal do esquema de referência no painel direito.

![](../images/ui/explore/relationship-field.png)

>[!NOTE]
>
>Veja o tutorial sobre [criação de um relacionamento na interface](../tutorials/relationship-ui.md) para obter mais informações sobre o uso de relacionamentos em esquemas XDM.

## Próximas etapas

Este documento abordou como explorar os recursos XDM existentes na interface do usuário do Experience Platform. Para obter mais informações sobre os diferentes recursos do [!UICONTROL Esquemas] Workspace e [!DNL Schema Editor], consulte o [[!UICONTROL Esquemas] visão geral do espaço de trabalho](./overview.md).
