---
keywords: Experience Platform;página inicial;tópicos populares;interface do usuário;XDM;sistema XDM;modelo de dados de experiência;modelo de dados de experiência;modelo de dados de experiência;modelo de dados;modelo de dados;explorar;classe;grupo de campos;tipo de dados;esquema;
solution: Experience Platform
title: Explorar recursos do esquema na interface do
description: Saiba como explorar esquemas, classes, grupos de campos de esquema e tipos de dados existentes na interface do usuário do Experience Platform.
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 0%

---

# Explorar recursos de esquema na interface do

No Adobe Experience Platform, todos os recursos de esquema do Experience Data Model (XDM) são armazenados no [!DNL Schema Library], incluindo os recursos padrão fornecidos pelo Adobe e os recursos personalizados definidos pela sua organização. Na interface do usuário do Experience Platform, você pode exibir a estrutura e os campos de qualquer esquema, classe, grupo de campos ou tipo de dados existente no [!DNL Schema Library]. Isso é especialmente útil ao planejar e se preparar para a assimilação de dados, pois a interface do usuário fornece informações sobre os tipos de dados e casos de uso esperados de cada campo fornecido por esses recursos XDM.

Este tutorial aborda as etapas para explorar esquemas, classes, grupos de campos e tipos de dados existentes na interface do Experience Platform.

## Pesquisar um recurso de esquema {#lookup}

Na interface do usuário do Experience Platform, selecione **[!UICONTROL Esquemas]** na navegação à esquerda. O espaço de trabalho [!UICONTROL Esquemas] fornece uma guia **[!UICONTROL Procurar]** para explorar todos os esquemas em sua organização, juntamente com guias dedicadas adicionais para explorar **[!UICONTROL Classes]**, **[!UICONTROL Grupos de campos]**, **[!UICONTROL Tipos de dados]** e **[!UICONTROL Relações]**, respectivamente.

![O espaço de trabalho Esquemas com várias guias realçadas.](../images/ui/explore/tabs.png)

O ícone de filtro (![Imagem do ícone de filtro](/help/images/icons/filter.png)) revela controles no painel esquerdo para restringir os resultados listados. Os filtros de recursos estão disponíveis para esquemas e relações nas guias **[!UICONTROL Procurar]** e **[!UICONTROL Relações]**, respectivamente.

Na guia [!UICONTROL Procurar] do espaço de trabalho [!UICONTROL Esquemas], você pode filtrar o inventário de esquemas. Use a opção **[!UICONTROL Incluído no Perfil]** para mostrar apenas esquemas que foram habilitados para uso no [Perfil de Cliente em Tempo Real](../../profile/home.md). Use a opção **[!UICONTROL Mostrar esquemas adhoc]** para filtrar a lista de esquemas criados com campos com namespace para uso apenas por um único conjunto de dados.

![A guia [!UICONTROL Procurar] do espaço de trabalho [!UICONTROL Esquemas] com o painel de filtros realçado.](../images/ui/explore/filters.png)

Na guia [!UICONTROL Relação] do espaço de trabalho [!UICONTROL Esquemas], você pode filtrar a lista de relações com base em quatro critérios. Os filtros incluem [!UICONTROL esquema Source], [!UICONTROL esquema Destino], [!UICONTROL classe Source] e a [!UICONTROL classe Destino]. A tabela abaixo fornece uma descrição dos filtros.

| Filtro | Descrição |
|-----------------------------------|------------|
| [!UICONTROL Esquema do Source] | Para ver todas as relações em que o esquema selecionado é o ponto de partida ou &quot;origem&quot;, selecione um esquema no menu suspenso [!UICONTROL Esquema do Source]. |
| [!UICONTROL Esquema de destino] | Para exibir todas as relações em que o esquema selecionado é o destino ou &quot;destino&quot;, selecione um esquema no menu suspenso [!UICONTROL Esquema de destino]. |
| [!UICONTROL classe Source] | Para filtrar relações com base na classe do esquema inicial, selecione uma classe no menu suspenso [!UICONTROL classe Source]. |
| [!UICONTROL Classe de destino] | Para exibir relações que terminam com esquemas de uma classe específica, selecione uma classe no menu suspenso [!UICONTROL Classe de destino]. |

{style="table-layout:auto"}

![A guia Relações com a seção de filtros foi realçada.](../images/ui/explore/relationships-filter.png)

Você também pode usar a barra de pesquisa para restringir ainda mais os resultados.

![A guia Procurar do espaço de trabalho Esquemas com o campo de pesquisa realçado.](../images/ui/explore/search.png)

Os recursos exibidos nos resultados da pesquisa são ordenados primeiro por correspondências de título e, em seguida, por correspondências de descrição. Por sua vez, quanto mais palavras corresponderem em uma dessas categorias, maior será o recurso exibido na lista.

Depois de encontrar o recurso que deseja explorar, selecione o nome dele na lista para exibir sua estrutura na tela.

## Explorar um recurso XDM na tela {#explore}

Depois de selecionar um recurso, sua estrutura é aberta na tela.

![A tela de espaço de trabalho do Tipo de Dados exibindo o tipo de dados Commerce.](../images/ui/explore/canvas.png)

Todos os campos do tipo de objeto que contêm subpropriedades são recolhidos por padrão quando aparecem pela primeira vez na tela. Para mostrar as subpropriedades de qualquer campo, selecione o ícone ao lado do nome.

![A tela de espaço de trabalho do Tipo de Dados com campos expandidos e subpropriedades realçadas.](../images/ui/explore/field-expand.png)

### Indicador padrão de classe e grupo de campos {#standard-class-and-field-group-indicator}

No Editor de esquemas, classes e grupos de campos padrão (gerados pela Adobe) são indicados com o ícone de cadeado (![Um ícone de cadeado.](/help/images/icons/lock-closed.png). O cadeado é exibido no painel à esquerda, ao lado do nome da classe ou do grupo de campos, e também ao lado de qualquer campo no diagrama de esquema que faça parte de um recurso gerado pelo sistema.

![O Editor de Esquemas com o ícone de cadeado realçado](../images/ui/explore/schema-editor-padlock-icon.png)

Consulte a documentação [Adicionar campos personalizados a grupos de campos padrão](./resources/schemas.md) para obter orientação. Não é possível editar uma classe padrão.

### Campos gerados pelo sistema {#system-fields}

Alguns nomes de campos recebem um sublinhado como prefixo, por exemplo, `_repo` e `_id`. Eles representam espaços reservados para campos que o sistema gerará e atribuirá automaticamente à medida que os dados forem assimilados.

Dessa forma, a maioria desses campos deve ser excluída da estrutura dos dados ao assimilar na Experience Platform. A principal exceção para essa regra é o campo [`_{TENANT_ID}` &#x200B;](../api/getting-started.md#know-your-tenant_id), no qual todos os campos XDM criados em sua organização devem ter o namespace.

### Tipos de dados {#data-types}

Para cada campo mostrado na tela, seu tipo de dados correspondente é mostrado ao lado do nome, indicando rapidamente o tipo de dados que o campo espera para assimilação.

![O tipo de dados Endereço Postal exibido na tela com seus tipos de dados associados realçados.](../images/ui/explore/data-types.png)

Qualquer tipo de dados com colchetes (`[]`) anexados representa uma matriz desse tipo de dados específico. Por exemplo, um tipo de dados de **[!UICONTROL Cadeia de caracteres]\[]** indica que o campo espera uma matriz de valores de cadeia de caracteres. Um tipo de dados de **[!UICONTROL Item de Pagamento]\[]** indica uma matriz de objetos que estão em conformidade com o tipo de dados [!UICONTROL Item de Pagamento].

Se um campo de matriz é baseado em um tipo de objeto, você pode selecionar seu ícone na tela para mostrar os atributos esperados para cada item de matriz.

![Um objeto na tela com um campo de matriz realçado e os atributos esperados para cada item de matriz exibido.](../images/ui/explore/array-type.png)

### [!UICONTROL Propriedades do campo] {#field-properties}

Ao selecionar o nome de qualquer campo na tela, o painel direito é atualizado para mostrar detalhes sobre esse campo em **[!UICONTROL Propriedades do campo]**. Isso pode incluir uma descrição do caso de uso pretendido do campo, valores padrão, padrões, formatos, se o campo é obrigatório ou não e muito mais.

![Um campo selecionado do tipo de dados Commerce com as propriedades do campo realçadas.](../images/ui/explore/field-properties.png)

Se o campo que você está inspecionando for um campo de enumeração, o painel direito também exibirá os valores aceitáveis que o campo espera receber.

![O Editor de Esquemas com um campo selecionado e valores de enumeração e nomes para exibição realçados no painel de propriedades do campo.](../images/ui/explore/enum-field.png)

### Campos de identidade {#identity}

Ao inspecionar esquemas que contêm campos de identidade, esses campos são listados no painel à esquerda na classe ou no grupo de campos que os fornece ao esquema. Selecione o nome do campo de identidade no painel à esquerda para revelar o campo na tela, independentemente da profundidade em que ele está aninhado.

Os campos de identidade são realçados na tela com um ícone de impressão digital (![Imagem do ícone de impressão digital](/help/images/icons/identity-service.png)). Se você selecionar o nome do campo de identidade, poderá exibir informações adicionais, como o [namespace de identidade](../../identity-service/features/namespaces.md) e se o campo é ou não a identidade principal do esquema.

![O Editor de Esquemas com a identidade do esquema realçada no painel à esquerda, o campo realçado no diagrama de esquema e o namespace de identidade realçado nas propriedades do campo.](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>Consulte o manual sobre [definição de campos de identidade](./fields/identity.md) para obter mais informações sobre campos de identidade e suas relações com os serviços downstream do Experience Platform.

### Campos de relacionamento {#relationship}

Se você estiver inspecionando um esquema que contém um campo de relação, o campo será listado no painel esquerdo em **[!UICONTROL Relações]**. Selecione o nome do campo de relacionamento no painel à esquerda para revelar o campo na tela, independentemente da profundidade em que ele está aninhado. Os campos de relacionamento também são destacados exclusivamente na tela, mostrando o nome do esquema de referência ao qual o campo é vinculado. Para organizações com recursos B2B, os nomes de relacionamentos personalizados podem ser escritos e serão exibidos na tela nesses casos.

![O Editor de Esquemas com o campo de relação e Editar relação realçados.](../images/ui/explore/relationship-field.png)

Para exibir o namespace de identidade da identidade primária do esquema de referência, selecione o campo de relação e **[!UICONTROL Editar relação]** na barra lateral [!UICONTROL Propriedades de campo]. Os parâmetros da relação são exibidos na caixa de diálogo [!UICONTROL Editar relação] exibida.

![A caixa de diálogo Editar relação com os parâmetros de relação exibidos.](../images/ui/explore/edit-relationship-dialog.png)

Consulte o tutorial sobre [criação de uma relação na interface](../tutorials/relationship-ui.md) para obter mais informações sobre o uso de relações em esquemas XDM.

## Próximas etapas

Este documento abordou como explorar os recursos XDM existentes na interface do usuário do Experience Platform. Para obter mais informações sobre os diferentes recursos do espaço de trabalho [!UICONTROL Esquemas] e [!DNL Schema Editor], consulte a [[!UICONTROL visão geral dos esquemas] do espaço de trabalho](./overview.md).
