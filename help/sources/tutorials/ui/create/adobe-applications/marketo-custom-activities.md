---
title: Criar uma conexão Marketo Engage Source e um fluxo de dados para dados de Atividade personalizados na interface
description: Este tutorial fornece etapas para criar uma conexão de origem de Marketo Engage e um fluxo de dados na interface do usuário para trazer dados de atividades personalizadas para o Adobe Experience Platform.
exl-id: 05a7b500-11d2-4d58-be43-a2c4c0ceeb87
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# Criar uma conexão de origem e um fluxo de dados [!DNL Marketo Engage] para dados de atividade personalizados na interface

>[!NOTE]
>
>Este tutorial fornece etapas específicas sobre como configurar e trazer dados da **atividade personalizada** de [!DNL Marketo] para o Experience Platform. Para obter etapas sobre como trazer dados da **atividade padrão**, leia o [[!DNL Marketo] guia da interface](./marketo.md).

Além das [atividades padrão](../../../../connectors/adobe-applications/mapping/marketo.md#activities), você também pode usar a fonte [!DNL Marketo] para trazer dados de atividades personalizadas para a Adobe Experience Platform. Este documento fornece etapas sobre como criar uma conexão de origem e um fluxo de dados para dados de atividade personalizados usando a origem [!DNL Marketo] na interface.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Utilitário de geração automática de esquemas e namespaces B2B](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md): o utilitário de geração automática de esquemas e namespaces B2B permite usar [!DNL Postman] para gerar valores automaticamente para seus esquemas e namespaces B2B. Você deve concluir seus namespaces e esquemas B2B primeiro, antes de criar uma conexão de origem e um fluxo de dados do [!DNL Marketo].
* [Fontes](../../../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Experience Data Model (XDM)](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Criar e editar esquemas na interface](../../../../../xdm/ui/resources/schemas.md): saiba como criar e editar esquemas na interface.
* [Namespaces de identidade](../../../../../identity-service/features/namespaces.md): os namespaces de identidade são um componente de [!DNL Identity Service] que serve como indicadores do contexto ao qual uma identidade está relacionada. Uma identidade totalmente qualificada inclui um valor de ID e um namespace.
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
* [Sandboxes](../../../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Recupere os detalhes de sua atividade personalizada

A primeira etapa para trazer dados de atividade personalizados do [!DNL Marketo] para o Experience Platform é recuperar o nome da API e o nome de exibição da sua atividade personalizada.

Faça logon em sua conta usando a interface [[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1). Na navegação à esquerda, em [!DNL Database Management], selecione **Atividades personalizadas do Marketo**.

A interface é atualizada para uma exibição de suas atividades personalizadas, incluindo informações sobre seus respectivos nomes de exibição e nomes de API. Você também pode usar o painel direito para selecionar e exibir outras atividades personalizadas da sua conta.

![A interface de Atividades Personalizadas na Interface do Usuário do Adobe Marketo Engage.](../../../../images/tutorials/create/marketo-custom-activities/marketo-custom-activity.png)

Selecione **Campos** no cabeçalho superior para exibir os campos associados à sua atividade personalizada. Nesta página, você pode exibir os nomes, os nomes das APIs, as descrições e os tipos de dados dos campos na atividade personalizada. Detalhes sobre campos individuais serão usados em uma etapa posterior, ao criar um esquema.

![A página Detalhes dos Campos de Atividade Personalizados do Marketo na Interface do Usuário do Marketo Engage.](../../../../images/tutorials/create/marketo-custom-activities/marketo-custom-activity-fields.png)

## Configurar grupos de campos para atividades personalizadas no esquema de atividades B2B

No painel *[!UICONTROL Esquemas]* da interface do usuário do Experience Platform, selecione **[!UICONTROL Procurar]** e selecione **[!UICONTROL Atividade B2B]** da lista de esquemas.

>[!TIP]
>
>Use a barra de pesquisa para acelerar sua navegação pela lista de schemas.

![O espaço de trabalho de esquemas na interface do usuário do Experience Platform com o esquema de Atividade B2B selecionado.](../../../../images/tutorials/create/marketo-custom-activities/b2b-activity.png)

### Criar um novo grupo de campos para uma atividade personalizada

Em seguida, adicione um novo grupo de campos ao esquema [!DNL B2B Activity]. Este grupo de campos deve corresponder à atividade personalizada que você deseja assimilar e deve usar o nome para exibição da atividade personalizada que você recuperou anteriormente.

Para adicionar um novo grupo de campos, selecione **[!UICONTROL + Adicionar]** ao lado do painel *[!UICONTROL Grupos de campos]* em *[!UICONTROL Composição]*.

![A estrutura do esquema.](../../../../images/tutorials/create/marketo-custom-activities/add-new-field-group.png)

A janela *[!UICONTROL Adicionar grupos de campos]* é exibida. Selecione **[!UICONTROL Criar novo grupo de campos]** e forneça o mesmo nome para exibição para a atividade personalizada que você recuperou em uma etapa anterior e forneça uma descrição opcional para seu novo grupo de campos. Quando terminar, selecione **[!UICONTROL Adicionar grupos de campos]**.

![A janela para rotular e criar um novo grupo de campos.](../../../../images/tutorials/create/marketo-custom-activities/create-new-field-group.png)

Depois de criado, seu novo grupo de campos para atividade personalizada aparece no catálogo [!UICONTROL Grupos de campos].

![A estrutura de esquema com um novo grupo de campos adicionado sob o painel do grupo de campos.](../../../../images/tutorials/create/marketo-custom-activities/new-field-group-created.png)

### Adicionar um novo campo à estrutura do esquema

Em seguida, adicione um novo campo ao esquema. Este novo campo deve ser definido como `type: object` e conterá os campos individuais da atividade personalizada.

Para adicionar um novo campo, selecione o sinal de adição (`+`) ao lado do nome do esquema. Uma entrada para *[!UICONTROL Campo sem título | Tipo]* é exibido. Em seguida, configure as propriedades do campo usando o painel *[!UICONTROL Propriedades do campo]*. Defina o nome do campo como o nome da API da atividade personalizada e defina o nome de exibição como o nome de exibição da atividade personalizada. Em seguida, defina o tipo como `object` e atribua o grupo de campos ao grupo de campos de atividade personalizado criado na etapa anterior. Quando terminar, selecione **[!UICONTROL Aplicar]**.

![A estrutura do esquema com o sinal de mais (`+`) selecionado para que um novo campo possa ser adicionado.](../../../../images/tutorials/create/marketo-custom-activities/add-new-object.png)

O novo campo aparece no esquema.

![Um novo campo adicionado ao esquema.](../../../../images/tutorials/create/marketo-custom-activities/new-object-field-added.png)

### Adicionar subcampos ao campo de objeto {#add-sub-fields-to-the-object-field}

A última etapa na preparação do esquema é adicionar campos individuais dentro do campo criado na etapa anterior.

![Um grupo de subcampos adicionados a um campo dentro do esquema.](../../../../images/tutorials/create/marketo-custom-activities/add-sub-fields.png)

## Criar um fluxo de dados

Com a configuração do esquema concluída, agora é possível prosseguir para criar um fluxo de dados para seus dados de atividade personalizados.

Na interface da Platform, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

Na categoria [!UICONTROL Adobe applications], selecione **[!UICONTROL Marketo Engage]**. Em seguida, selecione **[!UICONTROL Adicionar dados]** para criar um novo fluxo de dados [!DNL Marketo].

![O catálogo de origens na interface do usuário do Experience Platform com a origem de Marketo Engage selecionada.](../../../../images/tutorials/create/marketo/catalog.png)

### Selecionar dados

Selecione **[!UICONTROL Atividades]** da lista de [!DNL Marketo] conjuntos de dados e selecione **[!UICONTROL Próximo]**.

![A etapa de seleção de dados no fluxo de trabalho de fontes com o conjunto de dados de atividades selecionado.](../../../../images/tutorials/create/marketo-custom-activities/select-data.png)

### Detalhes do fluxo de dados

Em seguida, [forneça informações para o fluxo de dados](./marketo.md#provide-dataflow-details), incluindo nomes e descrições para o conjunto de dados e o fluxo de dados, o esquema que você usará e as configurações para assimilação [!DNL Profile], diagnóstico de erros e assimilação parcial.

![A etapa de detalhes do fluxo de dados.](../../../../images/tutorials/create/marketo-custom-activities/dataflow-detail.png)

### Mapeamento

Os mapeamentos para campos de atividade padrão são preenchidos automaticamente, mas os campos de atividade personalizados devem ser mapeados manualmente para os campos de destino correspondentes.

Para começar a mapear os campos de atividade personalizados, selecione **[!UICONTROL Novo tipo de campo]** e **[!UICONTROL Adicionar novo campo]**.

![A etapa de mapeamento com o menu suspenso para adicionar um novo campo.](../../../../images/tutorials/create/marketo-custom-activities/add-new-mapping-field.png)

Navegue pela estrutura de dados de origem e localize o campo de atividade personalizado que você deseja assimilar. Quando terminar, selecione **[!UICONTROL Selecionar]**.

>[!TIP]
>
>Para evitar confusão e lidar com nomes de campo duplicados, os campos de atividade personalizados recebem o prefixo do nome da API.

![A estrutura de dados de origem.](../../../../images/tutorials/create/marketo-custom-activities/select-new-mapping-field.png)

Para adicionar um campo de destino, selecione o ícone de esquema ![ícone de esquema](/help/images/icons/schema.png) e selecione os campos de atividade personalizados no esquema de destino.

![A estrutura do esquema de destino.](../../../../images/tutorials/create/marketo-custom-activities/add-target-mapping-field.png)

Repita as etapas para adicionar o restante dos campos de mapeamento de atividade personalizados. Quando terminar, selecione **[!UICONTROL Próximo]**.

![Todos os mapeamentos para dados de origem e de destino.](../../../../images/tutorials/create/marketo-custom-activities/all-mappings.png)

### Revisar

A etapa *[!UICONTROL Revisão]* é exibida, permitindo que você revise seu novo fluxo de dados antes de ele ser criado. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: mostra o tipo de origem, o caminho relevante da entidade de origem escolhida e a quantidade de colunas nessa entidade de origem.
* **[!UICONTROL Atribuir campos de conjunto de dados e mapa]**: mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o esquema ao qual o conjunto de dados pertence.

Depois de revisar o fluxo de dados, selecione **[!UICONTROL Salvar e assimilar]** e aguarde algum tempo para que o fluxo de dados seja criado.

![A etapa de revisão final que resume informações sobre os campos de conexão, conjunto de dados e mapeamento.](../../../../images/tutorials/create/marketo-custom-activities/review.png)

### Adicionar atividades personalizadas a um fluxo de dados de atividades existente {#add-to-existing-dataflows}

Para adicionar dados de atividade personalizados a um fluxo de dados existente, modifique os mapeamentos de um fluxo de dados de atividades existente com os dados de atividade personalizados que deseja assimilar. Isso permite assimilar atividades personalizadas no mesmo conjunto de dados de atividades existente. Para obter mais informações sobre como atualizar os mapeamentos de um fluxo de dados existente, leia o manual sobre [atualização de fluxos de dados na interface](../../update-dataflows.md).

### Usar [!DNL Query Service] para filtrar atividades para atividades personalizadas {#query-service-filter}

Depois que o fluxo de dados for concluído, você poderá usar o [Serviço de consulta](../../../../../query-service/home.md) para filtrar atividades para seus dados de atividade personalizados.

Quando atividades personalizadas são assimiladas na Platform, o nome da API da atividade personalizada automaticamente se torna seu `eventType`. Use `eventType={API_NAME}` para filtrar por dados de atividade personalizados.

```sql
SELECT * FROM with_custom_activities_ds_today WHERE eventType='aepCustomActivityDemo1' 
```

Use a cláusula `IN` para filtrar várias atividades personalizadas:

```sql
SELECT * FROM $datasetName WHERE eventType='{API_NAME}'
SELECT * FROM $datasetName WHERE eventType IN ('aepCustomActivityDemo1', 'aepCustomActivityDemo2')
```

A imagem abaixo mostra um exemplo de instrução SQL no [Editor de Consulta](../../../../../query-service/ui/user-guide.md) que filtra os dados de atividade personalizados.

![A interface do usuário da Platform exibindo um exemplo de consulta para atividades personalizadas.](../../../../images/tutorials/create/marketo-custom-activities/queries.png)

## Próximas etapas

Seguindo este tutorial, você configurou um esquema da Platform para [!DNL Marketo] dados de atividade personalizados e criou um fluxo de dados para trazer esses dados para a Platform. Para obter informações gerais sobre a origem [!DNL Marketo], leia a [[!DNL Marketo] visão geral da origem](../../../../connectors/adobe-applications/marketo/marketo.md).
