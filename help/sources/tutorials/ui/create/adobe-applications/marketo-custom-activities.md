---
title: Criar uma conexão de fonte de Marketo Engage e um fluxo de dados para dados de atividade personalizada na interface do usuário
description: Este tutorial fornece etapas para criar uma conexão de fonte Marketo Engage e um fluxo de dados na interface do usuário para trazer dados de atividades personalizadas para o Adobe Experience Platform.
source-git-commit: d049a29d4c39fa41917e8da1dde530966f4cbaf4
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 0%

---

# Crie um [!DNL Marketo Engage] conexão de origem e fluxo de dados para dados de atividade personalizados na interface do usuário

>[!NOTE]
>
>Este tutorial fornece etapas específicas sobre como configurar e trazer **atividade personalizada** dados de [!DNL Marketo] para Experience Platform. Para obter etapas sobre como trazer **atividade padrão** , leia a [[!DNL Marketo] Guia da interface do usuário](./marketo.md).

Além de [atividades padrão](../../../../connectors/adobe-applications/mapping/marketo.md#activities), também é possível usar o [!DNL Marketo] fonte para trazer dados de atividades personalizadas para o Adobe Experience Platform. Este documento fornece etapas sobre como criar uma conexão de origem e um fluxo de dados para dados de atividade personalizados usando o [!DNL Marketo] na interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Namespaces B2B e utilitário de geração automática de esquema](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md): Os namespaces B2B e o utilitário de geração automática de schema permitem usar [!DNL Postman] para gerar valores automaticamente para seus namespaces e esquemas B2B. Você deve concluir seus namespaces e esquemas B2B primeiro, antes de criar um [!DNL Marketo] conexão de origem e fluxo de dados.
* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Experience Data Model (XDM)](../../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Criar e editar esquemas na interface do usuário](../../../../../xdm/ui/resources/schemas.md): Saiba como criar e editar esquemas na interface do usuário.
* [Namespaces de identidade](../../../../../identity-service/namespaces.md): Os namespaces de identidade são um componente do [!DNL Identity Service] que servem como indicadores do contexto a que uma identidade se refere. Uma identidade totalmente qualificada inclui um valor de ID e um namespace.
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
* [Sandboxes](../../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Recupere os detalhes da atividade personalizada

A primeira etapa para trazer dados de atividade personalizados do [!DNL Marketo] para o Experience Platform é recuperar o nome da API e o nome de exibição da atividade personalizada.

Faça logon em sua conta usando o [[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1) interface. Na navegação à esquerda, em [!DNL Database Management], selecione **Atividades personalizadas do Marketo**.

A interface é atualizada para exibir suas atividades personalizadas, incluindo informações sobre seus respectivos nomes de exibição e nomes de API. Você também pode usar o painel direito para selecionar e exibir outras atividades personalizadas de sua conta.

![A interface Atividades personalizadas na interface do usuário do Adobe Marketo Engage.](../../../../images/tutorials/create/marketo-custom-activities/marketo-custom-activity.png)

Selecionar **Campos** no cabeçalho superior para exibir os campos associados à atividade personalizada. Nesta página, você pode exibir os nomes, nomes das APIs, descrições e tipos de dados dos campos em sua atividade personalizada. Os detalhes relativos aos campos individuais serão usados em uma etapa posterior, ao criar um schema.

![A página Detalhes dos campos de atividade personalizados do Marketo na interface do usuário do Marketo Engage.](../../../../images/tutorials/create/marketo-custom-activities/marketo-custom-activity-fields.png)

## Configurar grupos de campos para atividades personalizadas no esquema de atividades B2B

No *[!UICONTROL Esquemas]* no painel da interface do usuário do Experience Platform, selecione **[!UICONTROL Procurar]** e depois selecione **[!UICONTROL Atividade B2B]** na lista de schemas.

>[!TIP]
>
>Use a barra de pesquisa para acelerar sua navegação pela lista de schemas.

![O espaço de trabalho de schemas na interface do usuário do Experience Platform com o schema de atividade B2B selecionado.](../../../../images/tutorials/create/marketo-custom-activities/b2b-activity.png)

### Criar um novo grupo de campos para atividade personalizada

Em seguida, adicione um novo grupo de campos ao [!DNL B2B Activity] esquema. Esse grupo de campos deve corresponder à atividade personalizada que você deseja assimilar e deve usar o nome de exibição da atividade personalizada que você recuperou anteriormente.

Para adicionar um novo grupo de campos, selecione **[!UICONTROL + Adicionar]** ao lado do *[!UICONTROL Grupos de campos]* painel abaixo *[!UICONTROL Composição]*.

![A estrutura do schema.](../../../../images/tutorials/create/marketo-custom-activities/add-new-field-group.png)

O *[!UICONTROL Adicionar grupos de campos]* será exibida. Selecionar **[!UICONTROL Criar novo grupo de campos]** e, em seguida, forneça o mesmo nome de exibição para a atividade personalizada recuperada em uma etapa anterior e forneça uma descrição opcional para o novo grupo de campos. Quando terminar, selecione **[!UICONTROL Adicionar grupos de campos]**.

![A janela para rotular e criar um novo grupo de campos.](../../../../images/tutorials/create/marketo-custom-activities/create-new-field-group.png)

Depois de criado, o novo grupo de campos para atividade personalizada aparece na variável [!UICONTROL Grupos de campos] catálogo.

![A estrutura do schema com um novo grupo de campos adicionado sob o painel Grupo de campos.](../../../../images/tutorials/create/marketo-custom-activities/new-field-group-created.png)

### Adicionar um novo campo à estrutura do schema

Em seguida, adicione um novo campo ao esquema. Este novo campo deve ser definido como `type: object` e conterão os campos individuais da atividade personalizada.

Para adicionar um novo campo, selecione o sinal de adição (`+`) ao lado do nome do schema. Uma entrada para *[!UICONTROL Campo sem título | Tipo]* é exibido. Em seguida, configure as propriedades do campo usando o *[!UICONTROL Propriedades do campo]* painel. Defina o nome do campo como o nome da API da atividade personalizada e defina o nome de exibição como o nome de exibição da atividade personalizada. Em seguida, defina o tipo como `object` e atribua o grupo de campos ao grupo de campos de atividade personalizado criado na etapa anterior. Quando terminar, selecione **[!UICONTROL Aplicar]**.

![A estrutura do schema com o sinal de mais (`+`) para que um novo campo possa ser adicionado.](../../../../images/tutorials/create/marketo-custom-activities/add-new-object.png)

O novo campo aparece no esquema.

![Um novo campo adicionado ao schema.](../../../../images/tutorials/create/marketo-custom-activities/new-object-field-added.png)

### Adicionar subcampos ao campo de objeto {#add-sub-fields-to-the-object-field}

A última etapa na preparação do esquema é adicionar campos individuais dentro do campo criado na etapa anterior.

![Um grupo de subcampos adicionados a um campo dentro do schema .](../../../../images/tutorials/create/marketo-custom-activities/add-sub-fields.png)

## Criar um fluxo de dados

Com a configuração do esquema concluída, agora você pode continuar a criar um fluxo de dados para seus dados de atividade personalizada.

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

Em [!UICONTROL Aplicativos Adobe] categoria , selecione **[!UICONTROL Marketo Engage]**. Em seguida, selecione **[!UICONTROL Adicionar dados]** para criar um novo [!DNL Marketo] fluxo de dados.

![O catálogo de origens na interface do usuário do Experience Platform com a fonte de Marketo Engage selecionada.](../../../../images/tutorials/create/marketo/catalog.png)

### Selecionar dados

Selecionar **[!UICONTROL Atividades]** na lista de [!DNL Marketo] conjuntos de dados e, em seguida, selecione **[!UICONTROL Próximo]**.

![A etapa selecionar dados no fluxo de trabalho de fontes com o conjunto de dados de atividades selecionado.](../../../../images/tutorials/create/marketo-custom-activities/select-data.png)

### Detalhes do fluxo de dados

Em seguida, [fornecer informações para o seu fluxo de dados](./marketo.md#provide-dataflow-details), incluindo nomes e descrições para seu conjunto de dados e fluxo de dados, o esquema que você usará e as configurações para [!DNL Profile] ingestão, diagnósticos de erros e ingestão parcial.

![A etapa de detalhes do fluxo de dados.](../../../../images/tutorials/create/marketo-custom-activities/dataflow-detail.png)

### Mapeamento

Os mapeamentos para campos de atividade padrão são preenchidos automaticamente, mas os campos de atividade personalizados devem ser mapeados manualmente para os campos de destino correspondentes.

Para começar a mapear os campos de atividade personalizados, selecione **[!UICONTROL Novo tipo de campo]** e depois selecione **[!UICONTROL Adicionar novo campo]**.

![A etapa de mapeamento com o menu suspenso para adicionar um novo campo.](../../../../images/tutorials/create/marketo-custom-activities/add-new-mapping-field.png)

Navegue pela estrutura de dados de origem e localize o campo de atividade personalizado que deseja assimilar. Quando terminar, selecione **[!UICONTROL Selecionar]**.

>[!TIP]
>
>Para evitar confusão e manipular nomes de campos duplicados, os campos de atividade personalizados recebem o prefixo do nome da API.

![A estrutura de dados de origem.](../../../../images/tutorials/create/marketo-custom-activities/select-new-mapping-field.png)

Para adicionar um campo de target, selecione o ícone schema ![ícone de esquema](../../../../images/tutorials/create/marketo-custom-activities/schema-icon.png) e, em seguida, selecione os campos de atividade personalizados no schema de target.

![A estrutura do schema de target.](../../../../images/tutorials/create/marketo-custom-activities/add-target-mapping-field.png)

Repita as etapas para adicionar o restante dos campos de mapeamento de atividade personalizados. Quando terminar, selecione **[!UICONTROL Próximo]**.

![Todos os mapeamentos para dados de origem e de destino.](../../../../images/tutorials/create/marketo-custom-activities/all-mappings.png)

### Consulte a seção

O *[!UICONTROL Revisão]* é exibida, permitindo que você revise o novo fluxo de dados antes de criá-lo. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: Mostra o tipo de origem, o caminho relevante da entidade de origem escolhida e a quantidade de colunas dentro dessa entidade de origem.
* **[!UICONTROL Atribuir conjunto de dados e mapear campos]**: Mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o esquema ao qual o conjunto de dados adere.

Depois de revisar o fluxo de dados, selecione **[!UICONTROL Salvar e assimilar]** e permitir que o fluxo de dados seja criado.

![A etapa final de revisão que resume informações sobre a conexão, o conjunto de dados e os campos de mapeamento.](../../../../images/tutorials/create/marketo-custom-activities/review.png)

>[!NOTE]
>
>Quando a assimilação estiver concluída, o conjunto de dados assimilado conterá todas as atividades, incluindo atividades padrão e personalizadas, de [!DNL Marketo] instância. Para selecionar seus registros de atividade personalizados no Platform, você deve usar [Serviço de query](../../../../../query-service/home.md) e fornecer os predicados adequados.

## Próximas etapas

Ao seguir este tutorial, você configurou um esquema da plataforma para [!DNL Marketo] dados de atividade personalizados e um fluxo de dados foi criado para trazer esses dados para a plataforma. Para obter informações gerais sobre o [!DNL Marketo] fonte, leia o [[!DNL Marketo] visão geral da fonte](../../../../connectors/adobe-applications/marketo/marketo.md).