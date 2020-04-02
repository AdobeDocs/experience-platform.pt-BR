---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia da interface do usuário do Construtor de segmentos
topic: ui guide
translation-type: tm+mt
source-git-commit: 91792f81a50d5752e46236d61b6ad645e3fda86c

---


# Guia do usuário do Construtor de segmentos

O Adobe Experience Platform Segmentation Service fornece uma API RESTful e uma interface de usuário para criar definições de segmento a partir dos dados de Perfil do cliente em tempo real.

## Introdução

Trabalhar com definições de segmento requer uma compreensão dos vários serviços da plataforma de experiência envolvidos com a segmentação. Antes de ler este guia do usuário, consulte a documentação dos seguintes serviços:

- [Serviço](../home.md)de segmentação: O Serviço de segmentação permite que você divida dados armazenados na plataforma da experiência que se relacionam a indivíduos (como clientes, prospectos, usuários ou organizações) em grupos menores que compartilham características semelhantes e responderão de forma semelhante às estratégias de marketing.
- [Perfil](../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
- [Serviço](../../identity-service/home.md)de identidade: Habilita o Perfil do cliente em tempo real, fazendo a ponte entre identidades de diferentes fontes de dados que estão sendo assimiladas na Plataforma.
- [Modelo de dados de experiência (XDM)](../../xdm/home.md): A estrutura padronizada pela qual a Plataforma organiza os dados de experiência do cliente.

Também é importante saber dois termos chave que são usados por meio desse documento e entender a diferença entre eles:
- **Definição** do segmento: O conjunto de regras usado para descrever as principais características ou comportamentos de uma audiência de público alvo.
- **Audiência**: O conjunto resultante de perfis que atendem aos critérios de uma definição de segmento.

## Acessar definições de segmento

Para começar a trabalhar com definições de segmento na Adobe Experience Platform, clique em **Segmentos** na navegação à esquerda. Para ver todas as definições de segmento para sua organização, clique na guia *Procurar* . Essa visualização lista informações sobre a definição do segmento, incluindo o método de avaliação, a data de criação e a data da última modificação.

O método de avaliação pode ser streaming ou lote. Segmentos de transmissão são constantemente avaliados à medida que os dados entram no sistema. Os segmentos de lote são avaliados de acordo com uma programação definida.

Os segmentos de lote têm informações adicionais exibidas, mostrando a última data de avaliação e a próxima data de avaliação do lote.

Clicar em **Criar segmento** no canto superior direito abre a área de trabalho do Construtor de segmentos, onde você pode começar a criar uma definição de segmento.

![](../images/segment-builder/segment-browse.png)

## Área de trabalho do Construtor de segmentos

O Construtor de segmentos fornece uma área de trabalho avançada que permite interagir com elementos de dados do Perfil. A área de trabalho fornece controles intuitivos para criar e editar regras, como os blocos de arrastar e soltar usados para representar propriedades de dados.

![](../images/segment-builder/segment-builder.png)

## Elementos básicos para definição de segmento

Os elementos básicos das definições de segmentos são **Atributos** e **Eventos**. Além disso, os atributos e eventos contidos nas **Audiências** existentes também podem ser usados como componentes para novas definições.

É possível ver esses blocos de construção na seção *Campos* no lado esquerdo da área de trabalho do Construtor de segmentos. *Os campos* contêm uma guia para cada um dos blocos de construção principais: **Atributos**, **Eventos** e **Audiências**.

![](../images/segment-builder/segment-fields.png)

### Atributos

A guia **Atributos** permite navegar pelos atributos de Perfil pertencentes à classe de Perfil individual XDM. Cada pasta pode ser expandida para revelar atributos adicionais, onde cada atributo é um bloco que pode ser arrastado para a tela do construtor de regras no centro da área de trabalho. A tela [do construtor de](#rule-builder-canvas) regras é discutida com mais detalhes posteriormente neste guia.

![](../images/segment-builder/attributes.png)

### Eventos

A guia **Eventos** permite que você crie uma audiência com base em eventos ou ações realizadas usando elementos de dados XDM ExperienceEvent. Você também pode encontrar Tipos de evento na guia **Eventos** , que são uma coleção de eventos usados com frequência para permitir que você crie seus segmentos mais rapidamente.

Além de poder procurar por elementos ExperienceEvent, você também pode procurar Tipos de evento. Os Tipos de evento usam a mesma lógica de codificação que ExperienceEvents, sem exigir que você pesquise pela classe XDM ExperienceEvent procurando pelo evento correto. Por exemplo, usar a barra de pesquisa para pesquisar &quot;carrinho&quot; retorna os Tipos de evento &quot;AddCart&quot; e &quot;RemoveCart&quot;, que são duas ações de carrinho muito usadas ao criar definições de segmento.

Qualquer tipo de componente pode ser pesquisado digitando seu nome na barra de pesquisa, que usa a sintaxe [de pesquisa de](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene. Os resultados da pesquisa começam a ser preenchidos à medida que palavras inteiras são inseridas. Por exemplo, para criar uma regra baseada no campo XDM `ExperienceEvent.commerce.productViews`, digite &quot;visualizações de produto&quot; no start de pesquisa. Depois que a palavra &quot;produto&quot; é digitada, os resultados da pesquisa começam a ser exibidos. Cada resultado inclui a hierarquia de objetos à qual pertence.

>[!NOTE] Os campos de schema personalizados definidos pela sua organização podem levar até 24 horas para serem exibidos e se tornarem disponíveis para uso nas regras de criação.

Você pode arrastar e soltar facilmente ExperienceEvents e Tipos de evento na definição do segmento.

![](../images/segment-builder/events-eventTypes.png)

Por padrão, somente os campos de schema preenchidos do armazenamento de dados são exibidos. Isso inclui Tipos de evento. Se a lista de Tipos de evento não estiver visível ou você só puder selecionar &quot;Qualquer&quot; como um Tipo de evento, clique no ícone de engrenagem ao lado de *Campos* e selecione **Mostrar schema** XDM completo em Campos ** disponíveis. Clique no ícone de engrenagem novamente para voltar à guia *Campos* e agora você pode visualização em vários Tipos de evento e campos de schema, independentemente de conterem ou não dados.

![](../images/segment-builder/show-populated.png)

### Audiences

A guia **Audiência** lista todas as audiências importadas de fontes externas, como o Adobe Audiência Manager, bem como as audiências criadas na plataforma Experience.

Na guia Audiências, é possível visualizar todas as fontes disponíveis como um grupo de pastas. À medida que você clica nessas pastas, as subpastas e audiências disponíveis podem ser vistas. Além disso, você pode clicar no ícone de pasta (como mostrado na imagem da extrema direita) para visualização da estrutura de pastas (uma marca de seleção indica a pasta em que você está atualmente) e navegar facilmente de volta pelas pastas clicando no nome de uma pasta na árvore.

Você pode passar o mouse sobre a ⓘ ao lado de uma audiência para visualização com informações sobre a audiência, incluindo sua ID, descrição e hierarquia de pastas para localizar a audiência.

![](../images/segment-builder/audience-folder-structure.png)

Você também pode pesquisar Audiências usando a barra de pesquisa, que utiliza a sintaxe [de pesquisa de](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene. Na guia *Audiência* , selecionar uma pasta de nível superior faz com que a barra de pesquisa apareça, permitindo que você pesquise dentro dessa pasta. Os resultados da pesquisa só começam a ser preenchidos depois que palavras inteiras são inseridas. Por exemplo, para localizar uma Audiência chamada `Online Shoppers`, start digitando &quot;Online&quot; na barra de pesquisa. Depois que a palavra &quot;Online&quot; for digitada na íntegra, os resultados da pesquisa contendo a palavra &quot;Online&quot; serão exibidos.

## Tela do construtor de regras

Uma definição de segmento é uma coleção de regras usadas para descrever as principais características ou comportamento de uma audiência de público alvo. Essas regras são criadas usando a tela *do construtor de* regras, localizada no centro do Construtor de segmentos.

Para adicionar uma nova regra à definição do segmento, arraste um bloco da guia *Campos* e solte-o na tela do construtor de regras. Você receberá então opções específicas de contexto, de acordo com o tipo de dados que está sendo adicionado. Os tipos de dados disponíveis incluem: sequências de caracteres, datas, ExperienceEvents, Tipos de evento e Audiências.

![](../images/segment-builder/rule-builder-canvas.png)

### Adicionar audiências

Você pode arrastar e soltar uma audiência da guia *Audiência* na tela do construtor de regras para fazer referência à associação de audiência na nova definição de segmento. Isso permite que você inclua ou exclua a associação de audiência como um atributo na nova regra de segmento.

Para audiências de plataforma criadas usando o Construtor de segmentos, você tem a opção de converter a audiência no conjunto de regras que foram usadas na definição de segmento para essa audiência. Essa conversão faz uma cópia da lógica da regra, que pode ser modificada sem afetar a definição do segmento original.

>[!NOTE] Ao adicionar uma audiência de uma fonte externa, somente a associação de audiência é referenciada. Não é possível converter a audiência em regras e, portanto, as regras usadas para criar a audiência original não podem ser modificadas na nova definição de segmento.

![](../images/segment-builder/add-audience-to-segment.png)

## Contêineres

As regras de segmento são avaliadas na ordem em que são listadas. Os Container permitem o controle da ordem de execução por meio do uso de query aninhados.

Depois de adicionar pelo menos um bloco à tela do construtor de regras, você pode começar a adicionar container. Para criar um novo container, clique nas elipses (...) no canto superior direito do bloco e clique em **Adicionar container**.

![](../images/segment-builder/add-container.png)

Um novo container é exibido como filho do primeiro container, mas você pode ajustar a hierarquia arrastando e movendo os container. O comportamento padrão de um container é &quot;Incluir&quot; o atributo, o evento ou a audiência fornecida. Você pode definir a regra como &quot;Excluir&quot; perfis que correspondam aos critérios do container clicando em **Incluir** no canto superior esquerdo do bloco e selecionando &quot;Excluir&quot;.

Um container filho também pode ser extraído e adicionado em linha ao container pai clicando em &quot;desvincular container&quot; no container filho. Clique nas elipses (...) no canto superior direito do container filho para acessar essa opção.

![](../images/segment-builder/include-exclude.png)

Depois de clicar em **Desvincular container** , o container filho será removido e os critérios aparecerão em linha.

>[!NOTE] Ao desvincular container, tenha cuidado para que a lógica continue a atender à definição de segmento desejada.

![](../images/segment-builder/unwrapped-container-inline.png)

## Mesclar políticas

A plataforma Experience permite que você reúna dados de várias fontes e os combine para ver uma visualização completa de cada um de seus clientes individuais. Ao reunir esses dados, as políticas de mesclagem são as regras que a Plataforma usa para determinar como os dados serão priorizados e quais dados serão combinados para criar um perfil.

Você pode selecionar uma política de mesclagem que corresponda à sua finalidade de marketing para essa audiência ou usar a política de mesclagem padrão fornecida pela Plataforma. Você pode criar várias políticas de mesclagem exclusivas da sua organização, incluindo a criação de sua própria política de mesclagem padrão. Para obter instruções passo a passo sobre como criar políticas de mesclagem para sua organização, consulte o tutorial sobre como [trabalhar com políticas de mesclagem usando a interface do usuário](../../profile/ui/merge-policies.md).

Para selecionar uma política de mesclagem para a definição do segmento, clique no ícone de engrenagem na guia *Campos* e use o menu *suspenso Política de* mesclagem para selecionar a política de mesclagem que deseja usar.

![](../images/segment-builder/merge-policy-selector.png)

## Propriedades do segmento

Ao criar uma definição de segmento, a seção Propriedades *do* segmento no lado direito do espaço de trabalho exibe uma estimativa do tamanho do segmento resultante, permitindo que você ajuste sua definição de segmento conforme necessário antes de criar a própria audiência.

A seção Propriedades *do* segmento também é onde você pode especificar informações importantes sobre a definição do segmento, incluindo o *Nome* e a *Descrição*. Os nomes de definição de segmento são usados para identificar seu segmento entre aqueles definidos pela organização e, portanto, devem ser descritivos, concisos e exclusivos.

À medida que você continua a criar sua definição de segmento, é possível visualização uma pré-visualização paginada da audiência selecionando Perfis **de** Visualização.

![](../images/segment-builder/segment-properties.png)

>[!NOTE] As estimativas de Audiência são geradas usando um tamanho de amostra dos dados de amostra desse dia. Se houver menos de 1 milhão de entidades em sua loja de perfis, o conjunto de dados completo será usado; para entre 1 e 20 milhões de entidades, são utilizadas 1 milhão de entidades; e para mais de 20 milhões de entidades, são utilizados 5% do total de entidades. Mais informações sobre a geração de estimativas de segmentos podem ser encontradas na seção [de geração de](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) estimativas do tutorial de criação de segmentos.

## Ativar a segmentação programada

Depois que as definições de segmento forem criadas, você poderá avaliá-las por meio de uma avaliação sob demanda ou programada (contínua). Avaliação significa mover dados de Perfil do cliente em tempo real por meio de definições de segmento para produzir audiências correspondentes. Depois de criadas, as audiências são salvas e armazenadas para que possam ser exportadas usando as APIs da plataforma de experiência.

A avaliação sob demanda envolve o uso da API para realizar a avaliação e criar audiências conforme necessário, enquanto a avaliação programada (também conhecida como &quot;segmentação programada&quot;) permite criar um agendamento recorrente para avaliar definições de segmentos em um horário específico (no máximo, uma vez por dia).

A ativação das definições de segmento para avaliação programada pode ser feita usando a interface do usuário ou a API. Na interface do usuário, volte para a guia *Procurar* em **Segmentos** e alterne para **Avaliar todos os segmentos**. Isso fará com que todos os segmentos sejam avaliados com base na programação definida pela sua organização.

>[!NOTE] A avaliação agendada pode ser ativada para caixas de proteção com um máximo de cinco (5) políticas de mesclagem para o Perfil individual XDM. Se sua organização tiver mais de cinco políticas de mesclagem para o Perfil individual XDM em um único ambiente de caixa de proteção, você não poderá usar a avaliação programada.

No momento, os agendamentos só podem ser criados usando a API. Para obter etapas detalhadas sobre como criar, editar e trabalhar com programações usando a API, siga o tutorial para avaliar e acessar os resultados do segmento, especificamente a seção sobre avaliação [programada usando a API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![](../images/segment-builder/scheduled-segmentation.png)

## Ativar a segmentação de streaming

>[!NOTE] A segmentação de fluxo contínuo é um recurso beta e está disponível quando solicitado.

Além disso, uma definição de segmento pode ser ativada para a segmentação de fluxo contínuo antes ou depois de ter sido criada. A segmentação de transmissão avalia instantaneamente um cliente assim que um evento entra em um grupo de segmentos específico. Com esse recurso, a maioria das regras de segmento agora pode ser avaliada à medida que os dados são passados para a Plataforma, o que significa que a associação de segmento será mantida atualizada sem executar trabalhos de segmentação programados. Para obter informações mais detalhadas sobre a segmentação de streaming, leia a documentação [de segmentação de](../api/streaming-segmentation.md)streaming.

A ativação das definições de segmento para transmissão pode ser feita usando a interface do usuário ou a API. Para habilitar uma definição de segmento nova ou existente para streaming na interface do usuário, é necessário alternar a opção *Streaming* para **ON**.

![](../images/segment-builder/enable-streaming-segmentation.png)

Uma vez que a segmentação de fluxo esteja ativada, uma linha de base deve ser estabelecida (essa é a execução inicial após a qual o segmento sempre estará atualizado). O sistema lida com a definição de linha de base automaticamente, no entanto, isso só é possível se a segmentação programada tiver sido ativada. Para obter detalhes sobre como ativar a segmentação programada, consulte [a seção anterior neste guia](#enable-scheduled-segmentation)do usuário.

## Violações da política DULE

>[!NOTE] As violações da política DULE só se aplicam se você estiver criando um segmento que foi atribuído a um destino.

Quando terminar de criar seu segmento, ele será analisado pelo Data Governance para garantir que não haja violações de política no segmento. Para obter detalhes sobre DULE e violações de política, consulte a visão geral [do rótulo de uso de](../../data-governance/labels/overview.md)dados.

![](../images/segment-builder/segment-dule-policy-violations.png)

## Próximas etapas

O Construtor de segmentos fornece um fluxo de trabalho avançado que permite isolar audiências comercializáveis dos dados do Perfil do cliente em tempo real. Depois de ler este guia, você pode:

- Crie definições de segmento usando uma combinação de atributos, eventos e audiências existentes como blocos de construção.
- Use a tela e os container do construtor de regras para controlar a ordem na qual as regras de segmento são executadas.
- Estimativas de Visualização de sua audiência potencial, permitindo que você ajuste suas definições de segmento conforme necessário.
- Ative todas as definições de segmento para segmentação programada.
- Habilitar definições de segmento especificadas para a segmentação de streaming.

Para obter instruções passo a passo sobre como trabalhar com o Serviço de segmentação usando a API Perfil do cliente em tempo real, consulte o tutorial [Criação de segmentos de audiência usando APIs](../tutorials/create-a-segment.md) .