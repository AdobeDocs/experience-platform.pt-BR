---
keywords: Experience Platform, home, tópicos populares, Serviço de segmentação, segmentação, serviço de segmentação, guia do usuário, guia da interface do usuário, guia da interface de segmentação, construtor de segmentos, construtor de segmentos;
solution: Experience Platform
title: Guia da interface do usuário do Construtor de segmentos
topic-legacy: ui guide
description: O Construtor de segmentos na interface do usuário do Adobe Experience Platform fornece um espaço de trabalho avançado que permite interagir com elementos de dados do perfil. O espaço de trabalho oferece controles intuitivos para criar e editar regras, como blocos de arrastar e soltar usados para representar propriedades de dados.
exl-id: b27516ea-8749-4b44-99d0-98d3dc2f4c65
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 0%

---

# [!DNL Segment Builder] Guia da interface do usuário

[!DNL Segment Builder] O fornece um espaço de trabalho avançado que permite interagir com elementos  [!DNL Profile] de dados. O espaço de trabalho oferece controles intuitivos para criar e editar regras, como blocos de arrastar e soltar usados para representar propriedades de dados.

![](../images/ui/segment-builder/segment-builder.png)

## Elementos básicos da definição de segmentos

Os elementos básicos das definições de segmento são atributos e eventos. Além disso, os atributos e eventos contidos nos públicos-alvo existentes também podem ser usados como componentes para novas definições.

Você pode ver esses blocos fundamentais na seção **[!UICONTROL Fields]** no lado esquerdo do espaço de trabalho [!DNL Segment Builder]. **[!UICONTROL Fields]** contém uma guia para cada um dos blocos fundamentais: &quot;[!UICONTROL Attributes]&quot;, &quot;[!UICONTROL Events]&quot; e &quot;[!UICONTROL Audiences]&quot;.

![](../images/ui/segment-builder/segment-fields.png)

### Atributos

A guia **[!UICONTROL Attributes]** permite navegar pelos atributos [!DNL Profile] pertencentes à classe [!DNL XDM Individual Profile]. Cada pasta pode ser expandida para revelar atributos adicionais, onde cada atributo é um bloco que pode ser arrastado para a tela do construtor de regras no centro do espaço de trabalho. A [tela do construtor de regras](#rule-builder-canvas) é discutida com mais detalhes posteriormente neste guia.

![](../images/ui/segment-builder/attributes.png)

### Eventos

A guia **[!UICONTROL Events]** permite criar um público-alvo com base em eventos ou ações que ocorreram usando elementos de dados [!DNL XDM ExperienceEvent]. Você também pode encontrar Tipos de evento na guia **[!UICONTROL Events]** , que são uma coleção de eventos comumente usados para permitir que você crie seus segmentos mais rapidamente.

Além de poder procurar elementos [!DNL ExperienceEvent], você também pode procurar por Tipos de evento. Os Tipos de evento usam a mesma lógica de codificação de [!DNL ExperienceEvents], sem exigir que você pesquise a classe [!DNL XDM ExperienceEvent] procurando pelo evento correto. Por exemplo, usar a barra de pesquisa para pesquisar &quot;carrinho&quot; retorna os Tipos de evento &quot;[!UICONTROL AddCart]&quot; e &quot;[!UICONTROL RemoveCart]&quot;, que são duas ações de carrinho muito usadas ao criar definições de segmento.

Qualquer tipo de componente pode ser pesquisado digitando seu nome na barra de pesquisa, que usa a sintaxe de pesquisa de [Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Os resultados da pesquisa começam a ser preenchidos à medida que palavras inteiras são inseridas. Por exemplo, para criar uma regra baseada no campo XDM `ExperienceEvent.commerce.productViews`, comece a digitar &quot;visualizações de produto&quot; no campo de pesquisa. Depois que a palavra &quot;produto&quot; é digitada, os resultados da pesquisa começam a aparecer. Cada resultado inclui a hierarquia de objeto à qual pertence.

>[!NOTE]
>
>Os campos de esquema personalizados definidos pela organização podem levar até 24 horas para serem exibidos e ficarem disponíveis para uso na criação de regras.

Em seguida, você pode arrastar e soltar facilmente [!DNL ExperienceEvents] e &quot;[!UICONTROL Event Types]&quot; na definição do segmento.

![](../images/ui/segment-builder/events-eventTypes.png)

Por padrão, somente os campos de esquema preenchidos do armazenamento de dados são mostrados. Isso inclui &quot;[!UICONTROL Event Types]&quot;. Se a lista &quot;[!UICONTROL Event Types]&quot; não estiver visível, ou você só puder selecionar &quot;[!UICONTROL Any]&quot; como um &quot;[!UICONTROL Event Type]&quot;, selecione o **ícone de engrenagem** ao lado de **[!UICONTROL Fields]** e selecione **[!UICONTROL Show full XDM schema]** em **[!UICONTROL Available Fields]**. Selecione o **ícone de engrenagem** novamente para retornar à guia **[!UICONTROL Fields]** e agora é possível exibir vários &quot;[!UICONTROL Event Types]&quot; e campos de esquema, independentemente de apresentarem ou não dados.

![](../images/ui/segment-builder/show-populated.png)

### Públicos-alvo

A guia **[!UICONTROL Audiences]** lista todos os públicos-alvo importados de fontes externas, como o Adobe Audience Manager, bem como os criados em [!DNL Experience Platform].

Na guia **[!UICONTROL Audiences]** , é possível ver todas as fontes disponíveis como um grupo de pastas. À medida que você seleciona as pastas, as subpastas e os públicos-alvo disponíveis podem ser vistos. Além disso, é possível selecionar o ícone de pasta (como mostrado na imagem da extrema direita) para visualizar a estrutura de pastas (uma marca de seleção indica a pasta em que você está no momento) e navegar facilmente de volta pelas pastas selecionando o nome de uma pasta na árvore.

Você pode passar o mouse sobre a ⓘ ao lado de um público-alvo para exibir as informações sobre ele, incluindo a ID, a descrição e a hierarquia de pastas para localizar o público-alvo.

![](../images/ui/segment-builder/audience-folder-structure.png)

Você também pode pesquisar públicos-alvo usando a barra de pesquisa, que utiliza a [sintaxe de pesquisa do Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Na guia **[!UICONTROL Audiences]** , selecionar uma pasta de nível superior faz com que a barra de pesquisa apareça, permitindo pesquisar dentro dessa pasta. Os resultados da pesquisa só começam a ser preenchidos depois que palavras inteiras são inseridas. Por exemplo, para encontrar um público chamado `Online Shoppers`, comece a digitar &quot;Online&quot; na barra de pesquisa. Quando a palavra &quot;Online&quot; tiver sido digitada na íntegra, os resultados da pesquisa contendo a palavra &quot;Online&quot; serão exibidos.

## Tela do construtor de regras {#rule-builder-canvas}

Uma definição de segmento é uma coleção de regras usadas para descrever as principais características ou o comportamento de um público-alvo. Essas regras são criadas usando a tela do construtor de regras, localizada no centro de [!DNL Segment Builder].

Para adicionar uma nova regra à definição do segmento, arraste um bloco da guia **[!UICONTROL Fields]** e solte-o na tela do construtor de regras. Em seguida, você verá opções específicas do contexto de acordo com o tipo de dados que está sendo adicionado. Os tipos de dados disponíveis incluem: strings, datas, [!DNL ExperienceEvents], &quot;[!UICONTROL Event Types]&quot; e públicos-alvo.

![](../images/ui/segment-builder/rule-builder-canvas.png)

>[!IMPORTANT]
>
>As alterações mais recentes no Adobe Experience Platform atualizaram o uso dos operadores lógicos `OR` e `AND` entre eventos. Essas atualizações não afetarão os segmentos existentes. No entanto, todas as atualizações subsequentes de segmentos existentes e novas criações de segmentos serão afetadas por essas alterações. Leia as [atualizações de constantes de tempo](./segment-refactoring.md) para obter mais informações.

### Adição de públicos-alvo

Você pode arrastar e soltar um público-alvo da guia **[!UICONTROL Audience]** na tela do construtor de regras para fazer referência à associação do público-alvo na nova definição de segmento. Isso permite incluir ou excluir a associação do público-alvo como um atributo na nova regra de segmento.

Para públicos-alvo [!DNL Platform] criados usando [!DNL Segment Builder], você tem a opção de converter o público-alvo no conjunto de regras que foram usadas na definição de segmento para esse público-alvo. Essa conversão faz uma cópia da lógica da regra, que pode ser modificada sem afetar a definição do segmento original. Certifique-se de ter salvo as alterações recentes na definição do segmento antes de convertê-lo para a lógica da regra.

>[!NOTE]
>
>Ao adicionar um público-alvo de uma fonte externa, somente a associação de público-alvo é referenciada. Não é possível converter o público-alvo em regras e, portanto, as regras usadas para criar o público-alvo original não podem ser modificadas na nova definição de segmento.

![](../images/ui/segment-builder/add-audience-to-segment.png)

Se surgirem conflitos ao converter públicos-alvo em regras, [!DNL Segment Builder] tentará preservar as opções existentes da melhor maneira.

### Visualização de código

Como alternativa, você pode exibir uma versão baseada em código de uma regra criada no [!DNL Segment Builder]. Depois de criar sua regra na tela do construtor de regras, você pode selecionar **[!UICONTROL Code view]** para ver seu segmento como PQL.

![](../images/ui/segment-builder/code-view.png)

A Visualização de código fornece um botão que permite copiar o valor do segmento para usar em chamadas de API. Para obter a versão mais recente do segmento, certifique-se de ter salvo suas alterações mais recentes no segmento.

![](../images/ui/segment-builder/copy-code.png)

### Funções de agregação

Um agregado em [!DNL Segment Builder] é um cálculo em um grupo de atributos XDM cujo tipo de dados é um número (um número duplo ou um inteiro). As quatro funções de agregação compatíveis no Construtor de segmentos são SUM, MÉDIA, MIN e MAX.

Para criar uma função de agregação, selecione um evento no painel à esquerda e insira-o no container [!UICONTROL Events].

![](../images/ui/segment-builder/select-event.png)

Depois de colocar o evento no contêiner de Eventos, selecione o ícone de elipses (..), seguido por **[!UICONTROL Aggregate]**.

![](../images/ui/segment-builder/add-aggregation.png)

A agregação agora é adicionada. Agora é possível selecionar a função de agregação, escolher qual atributo agregar, a função de igualdade e o valor. Para o exemplo abaixo, esse segmento qualificaria qualquer perfil que tivesse uma soma de valores comprados maior que $100, mesmo se cada compra individual fosse menor que $100.

![](../images/ui/segment-builder/filled-aggregation.png)

### Funções de contagem

Funções de contagem no Construtor de segmentos são usadas para procurar eventos específicos e contar o número de vezes que foram feitas. As funções de contagem compatíveis no Construtor de segmentos são &quot;No mínimo&quot;, &quot;No máximo&quot;, &quot;Exatamente&quot;, &quot;Entre&quot; e &quot;Todos&quot;.

Para criar uma função de contagem, selecione um evento no painel à esquerda e insira-o no container [!UICONTROL Events].

![](../images/ui/segment-builder/add-event.png)

Depois de colocar o evento no contêiner Eventos , selecione o botão [!UICONTROL At least 1] .

![](../images/ui/segment-builder/add-count.png)

A função de contagem agora é adicionada. Agora é possível selecionar a função de contagem e o valor da função . O exemplo abaixo seria incluir qualquer evento que tenha pelo menos um clique.

![](../images/ui/segment-builder/select-count.png)

## Contêineres

As regras de segmento são avaliadas na ordem em que são listadas. Os containers permitem controlar a ordem de execução por meio do uso de consultas aninhadas.

Depois de ter adicionado pelo menos um bloco à tela do construtor de regras, você pode começar a adicionar contêineres. Para criar um novo contêiner, selecione os elipses (..) no canto superior direito do bloco e selecione **[!UICONTROL Add container]**.

![](../images/ui/segment-builder/add-container.png)

Um novo contêiner é exibido como filho do primeiro contêiner, mas você pode ajustar a hierarquia arrastando e movendo os contêineres. O comportamento padrão de um contêiner é &quot;[!UICONTROL Include]&quot; o atributo, evento ou público-alvo fornecido. É possível definir a regra para perfis &quot;[!UICONTROL Exclude]&quot; que correspondam aos critérios do contêiner ao selecionar **[!UICONTROL Include]** no canto superior esquerdo do bloco e selecionar &quot;[!UICONTROL Exclude]&quot;.

Um contêiner filho também pode ser extraído e adicionado em linha ao contêiner pai ao selecionar &quot;cancelar o contêiner&quot; no contêiner filho. Selecione as reticências (...) no canto superior direito do contêiner filho para acessar essa opção.

![](../images/ui/segment-builder/include-exclude.png)

Depois de selecionar **[!UICONTROL Unwrap container]** o contêiner filho é removido e os critérios são exibidos em linha.

>[!NOTE]
>
>Ao desvincular contêineres, tenha cuidado para que a lógica continue a atender à definição de segmento desejada.

![](../images/ui/segment-builder/unwrapped-container-inline.png)

## Mesclar políticas

[!DNL Experience Platform] O permite reunir dados de várias fontes e combiná-los para ver uma visualização completa de cada um dos clientes individuais. Ao reunir esses dados, as políticas de mesclagem são as regras que [!DNL Platform] usa para determinar como os dados serão priorizados e quais dados serão combinados para criar um perfil.

Você pode selecionar uma política de mesclagem que corresponda à sua finalidade de marketing para esse público-alvo ou usar a política de mesclagem padrão fornecida por [!DNL Platform]. É possível criar várias políticas de mesclagem exclusivas de sua organização, incluindo a criação de sua própria política de mesclagem padrão. Para obter instruções passo a passo sobre como criar políticas de mesclagem para sua organização, consulte o tutorial em [trabalhar com políticas de mesclagem usando a interface do usuário](../../profile/ui/merge-policies.md).

Para selecionar uma política de mesclagem para a definição do segmento, selecione o ícone de engrenagem na guia **[!UICONTROL Fields]** e use o menu suspenso **[!UICONTROL Merge Policy]** para selecionar a política de mesclagem que deseja usar.

![](../images/ui/segment-builder/merge-policy-selector.png)

## Propriedades do segmento

Ao criar uma definição de segmento, a seção **[!UICONTROL Segment Properties]** no lado direito do espaço de trabalho exibe uma estimativa do tamanho do segmento resultante, permitindo ajustar a definição do segmento, conforme necessário, antes de criar o próprio público-alvo.

A seção **[!UICONTROL Segment Properties]** também é onde você pode especificar informações importantes sobre a definição do segmento, incluindo o nome e a descrição. Os nomes de definição de segmento são usados para identificar seu segmento entre aqueles definidos pela organização e, portanto, devem ser descritivos, concisos e exclusivos.

À medida que você continua a criar a definição do segmento, é possível visualizar uma visualização paginada do público selecionando **[!UICONTROL View Profiles]**.

![](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
>As estimativas de público-alvo são geradas usando um tamanho de amostra dos dados de amostra desse dia. Se houver menos de 1 milhão de entidades em seu armazenamento de perfil, o conjunto de dados completo será usado; para entre 1 e 20 milhões de entidades, são utilizadas 1 milhão de entidades; e para mais de 20 milhões de entidades, são utilizados 5% do total de entidades. Mais informações sobre a geração de estimativas de segmento podem ser encontradas na [seção de geração de estimativa](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) do tutorial de criação de segmento.

## Próximas etapas {#next-steps}

O Construtor de segmentos fornece um fluxo de trabalho avançado que permite isolar públicos comercializáveis dos dados [!DNL Real-time Customer Profile] . Após a leitura deste guia, você deve ser capaz de:

- Crie definições de segmento usando uma combinação de atributos, eventos e públicos-alvo existentes como blocos de construção.
- Use a tela e os contêineres do construtor de regras para controlar a ordem em que as regras de segmento são executadas.
- Visualize estimativas do seu público-alvo potencial, permitindo ajustar as definições do segmento, conforme necessário.
- Ativar todas as definições de segmento para segmentação agendada.
- Ativar definições de segmento especificadas para a segmentação de fluxo.

Para saber mais sobre [!DNL Segmentation Service], continue lendo a documentação e complemente seu aprendizado assistindo aos vídeos relacionados. Para saber mais sobre as outras partes da interface do usuário [!DNL Segmentation Service], leia o [[!DNL Segmentation Service] guia do usuário](./overview.md)
