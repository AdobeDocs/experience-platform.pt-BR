---
keywords: Experience Platform;perfil;perfil do cliente em tempo real;políticas de mesclagem;interface do usuário;interface do usuário;carimbo de data e hora solicitado;precedência do conjunto de dados
title: Guia da interface do usuário de políticas de mesclagem
topic: guide
type: Documentation
description: 'A Adobe Experience Platform permite que você reúna fragmentos de dados de várias fontes e os combine para ver uma visualização completa de cada um de seus clientes individuais. Ao reunir esses dados, as políticas de mesclagem são as regras que a Plataforma usa para determinar como os dados serão priorizados e quais dados serão combinados para criar uma visualização unificada. '
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '3017'
ht-degree: 0%

---


# Guia da interface do usuário para unir políticas

A Adobe Experience Platform permite que você reúna fragmentos de dados de várias fontes e os combine para ver uma visualização completa de cada um de seus clientes individuais. Ao reunir esses dados, as políticas de mesclagem são as regras que [!DNL Platform] usa para determinar como os dados serão priorizados e quais dados serão combinados para criar uma visualização unificada.

Por exemplo, se um cliente interagir com sua marca em vários canais, sua organização terá vários fragmentos de perfil relacionados a esse único cliente que aparece em vários conjuntos de dados. Quando esses fragmentos são ingeridos na Plataforma, eles são unidos para criar um único perfil para o cliente. Quando os dados de várias fontes entram em conflito (por exemplo, um fragmento lista o cliente como &quot;único&quot; enquanto o outro lista o cliente como &quot;casado&quot;), a política de mesclagem determina quais informações devem ser incluídas no perfil do indivíduo.

Usando RESTful APIs ou a interface do usuário, você pode criar novas políticas de mesclagem, gerenciar políticas existentes e definir uma política de mesclagem padrão para sua organização. Este guia fornece instruções passo a passo para trabalhar com políticas de mesclagem usando a interface do usuário Adobe Experience Platform (UI).

Se preferir trabalhar com políticas de mesclagem usando a API [!DNL Real-time Customer Profile], siga as instruções descritas no [guia da API de políticas de mesclagem](../api/merge-policies.md).

## Introdução

Este guia requer uma compreensão funcional de vários recursos importantes [!DNL Experience Platform]. Antes de seguir este guia ou usar as APIs de Perfil, consulte a documentação dos seguintes serviços:

* [Perfil](../home.md) do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
* [Serviço](../../identity-service/home.md) de identidade Adobe Experience Platform: Habilita o Perfil do cliente em tempo real, fazendo a ponte entre identidades de diferentes fontes de dados que estão sendo assimiladas  [!DNL Platform].
* [Modelo de dados de experiência (XDM)](../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Platform] organiza os dados de experiência do cliente.

## Mesclar métodos {#merge-methods}

Cada fragmento de perfil contém informações para apenas uma identidade do número total de identidades que podem existir para um indivíduo. Ao unir esses dados para formar um perfil do cliente, há o potencial para que essas informações entrem em conflito e a prioridade deve ser especificada. Selecionar um método de mesclagem permite especificar quais atributos de conjunto de dados priorizarão se ocorrer um conflito de mesclagem entre conjuntos de dados.

Há dois métodos de mesclagem possíveis disponíveis para políticas de mesclagem. Cada um desses métodos é resumido abaixo com detalhes adicionais fornecidos nas seções a seguir:

* **[!UICONTROL Carimbo de data e hora ordenado]:** No evento de um conflito, é dada prioridade ao fragmento do perfil que foi atualizado mais recentemente.
   * **Carimbos de data e hora personalizados:** [!UICONTROL Carimbo de data e hora ] solicitado também oferece suporte a carimbos de data e hora personalizados que têm prioridade sobre os carimbos de data e hora do sistema ao mesclar dados dentro do mesmo conjunto de dados (várias identidades) ou entre conjuntos de dados. Para saber mais, consulte a seção em [usando carimbos de data e hora personalizados](#custom-timestamps).
* **[!UICONTROL Precedência] do conjunto de dados:** no evento de um conflito, dê prioridade aos fragmentos do perfil com base no conjunto de dados de onde eles vieram. Ao selecionar essa opção, você deve escolher os conjuntos de dados relacionados e sua ordem de prioridade.

### Carimbo de data e hora solicitado {#timestamp-ordered}

Como os registros de perfis são ingeridos no Experience Platform, um carimbo de data e hora do sistema é obtido no momento da ingestão e adicionado ao registro. Quando **[!UICONTROL Carimbo de data e hora solicitado]** é selecionado como o método de mesclagem para uma política de mesclagem, os perfis são mesclados com base no carimbo de data e hora do sistema. Em outras palavras, a mesclagem é feita com base no carimbo de data e hora para quando o registro foi ingerido na Plataforma.

#### Uso de carimbos de data e hora personalizados {#custom-timestamps}

Ocasionalmente, pode haver casos de uso em que é necessário fornecer um carimbo de data e hora personalizado e fazer com que a política de mesclagem cumpra o carimbo de data e hora personalizado em vez do carimbo de data e hora do sistema. Exemplos disso incluem preenchimento retroativo de dados ou garantia da ordem correta de eventos se os registros forem ingeridos fora de ordem.

Para usar um carimbo de data e hora personalizado, a **[!UICONTROL Mixin]** Detalhes da Auditoria do Sistema de Origem Externa deve ser adicionada ao schema do Perfil. Depois de adicionada, o carimbo de data e hora personalizado pode ser preenchido usando o campo `lastUpdatedDate`. Quando um registro for ingerido com o campo `lastUpdatedDate` preenchido, o Experience Platform usará esse campo para unir registros em conjuntos de dados. Se `lastUpdatedDate` não estiver presente ou não estiver preenchida, a Plataforma continuará a usar o carimbo de data e hora do sistema.

>[!NOTE]
>
>Você deve garantir que o carimbo de data e hora `lastUpdatedDate` seja preenchido ao assimilar uma atualização no mesmo registro.

A seguinte captura de tela exibe os campos na [!UICONTROL Mixin] Detalhes da Auditoria do Sistema de Origem Externa. Para obter instruções passo a passo sobre como trabalhar com schemas usando a interface do usuário da plataforma, incluindo como adicionar combinações a schemas, visite o tutorial [para criar um schema usando a interface do usuário](../../xdm/tutorials/create-schema-ui.md).

![](../images/merge-policies/custom-timestamp-mixin.png)

Para trabalhar com carimbos de data e hora personalizados usando a API, consulte a seção [guia de ponto de extremidade de políticas de mesclagem sobre como usar carimbos de data e hora personalizados](../api/merge-policies.md#custom-timestamps).

### Precedência do conjunto de dados {#dataset-precedence}

Quando **[!UICONTROL Prioridade do conjunto de dados]** for selecionado como o método de mesclagem para uma política de mesclagem, você poderá dar prioridade aos fragmentos do perfil com base no conjunto de dados de onde eles vieram. Um exemplo de caso de uso seria se sua organização tivesse informações presentes em um conjunto de dados que seja preferencial ou confiável em relação aos dados em outro conjunto de dados.

Para criar uma política de mesclagem usando **[!UICONTROL precedência do conjunto de dados]**, você deve selecionar os conjuntos de dados do Perfil e do ExperienceEvent incluídos e, em seguida, pode ordenar manualmente os conjuntos de dados do Perfil para precedência. Depois que os conjuntos de dados forem selecionados e ordenados, o conjunto de dados principal terá prioridade máxima, o segundo conjunto de dados será o segundo mais alto e assim por diante.

## [!UICONTROL costura de ID] {#id-stitching}

A identificação de fragmentos ([!UICONTROL identificação de identificação]) é o processo de identificação de fragmentos de dados e sua combinação para formar um registro de perfil completo. Para ajudar a ilustrar os diferentes comportamentos de ajuste, considere um único cliente que interage com uma marca usando dois endereços de email diferentes.

* **[!UICONTROL Nenhuma]:** quando essa opção é selecionada, as IDs não serão agrupadas. Quando a segmentação ocorrer, as identidades que podem pertencer à mesma pessoa não serão agrupadas em conjunto e a segmentação considerará apenas os atributos anexados a cada ID individual ao determinar se um cliente se qualifica para associação de segmento. Isso pode resultar em um único cliente com vários perfis e cada perfil pode se qualificar para diferentes segmentos, resultando no envio de várias mensagens de marketing ao mesmo cliente.
* **[!UICONTROL Gráfico] privado:** quando o gráfico privado é selecionado, várias identidades relacionadas ao mesmo indivíduo são unidas. Isso resulta em um único perfil para o cliente e permite que a segmentação considere vários atributos de várias identidades relacionadas ao determinar a qualificação do segmento. Nesse cenário, o cliente provavelmente terá um único perfil, estará qualificado para um segmento com base na combinação de atributos em identidades e receberá apenas uma mensagem de marketing.

Para saber mais sobre identidades e sua função na geração de perfis e segmentos, comece lendo a [visão geral do Serviço de Identidade](../../identity-service/home.md).

## Política de mesclagem padrão {#default-merge-policy}

Uma organização pode criar uma política de mesclagem padrão para que sua organização use ao mesclar fragmentos de perfil. Isso permite que os usuários selecionem facilmente a política padrão ao executar ações no Experience Platform, como visualizar perfis de clientes ou criar segmentos. Na maioria dos casos, a menos que outra política de mesclagem seja especificada, a política de mesclagem padrão será usada.

Cada organização pode criar várias políticas de mesclagem relacionadas a uma única classe de schema XDM, no entanto, só pode ter uma política de mesclagem padrão declarada para cada classe. Por exemplo, sua organização pode ter uma política de mesclagem padrão relacionada à classe [!DNL XDM Individual Profile] e uma política de mesclagem padrão diferente para uma classe de Inventário de Produto criada personalizada.

Se você criar uma nova política de mesclagem e defini-la como padrão, a política de mesclagem padrão anterior será automaticamente atualizada pelo sistema para não ser mais o padrão.

>[!WARNING]
>
>Contagens de perfis e segmentos com uma política de mesclagem padrão existente associada podem ser afetados. Qualquer segmento que tenha uma política de mesclagem padrão aplicada será atualizado para a nova política de mesclagem padrão.

## políticas de mesclagem de visualização {#view-merge-policies}

Na interface do usuário [!DNL Experience Platform], você pode começar a trabalhar com políticas de mesclagem selecionando **[!UICONTROL Perfis]** no menu de navegação esquerdo e selecionando a guia **[!UICONTROL Mesclar políticas]**. Esta guia inclui uma lista de todas as políticas de mesclagem existentes para sua organização, bem como detalhes de cada política de mesclagem, incluindo o nome da política, se a política de mesclagem é a política de mesclagem padrão e a classe de schema à qual a política de mesclagem se relaciona.

![Landing page de políticas de mesclagem](../images/merge-policies/landing.png)

Para selecionar quais detalhes estão visíveis ou para adicionar outras colunas à exibição, selecione **[!UICONTROL Configurar colunas]** e clique no nome de uma coluna para adicioná-la ou removê-la da visualização.

![](../images/merge-policies/adjust-view.png)

## Criar uma política de mesclagem {#create-a-merge-policy}

Para criar uma nova política de mesclagem, selecione **[!UICONTROL Criar política de mesclagem]** na guia políticas de mesclagem.

![Mesclar a landing page de políticas com o botão criar realçado.](../images/merge-policies/create-new.png)

Na tela de fluxo de trabalho **[!UICONTROL Nova política de mesclagem]**, você pode fornecer informações importantes para sua nova política de mesclagem por meio de uma série de etapas guiadas.

![O novo fluxo de trabalho da política de mesclagem.](../images/merge-policies/create.png)

### [!UICONTROL Configurar] {#configure}

A primeira etapa do fluxo de trabalho permite que você configure sua política de mesclagem fornecendo informações básicas. Essas informações incluem:

* **[!UICONTROL Nome]**: O nome da sua política de mesclagem deve ser descritivo, mas conciso.
* **[!UICONTROL Classe]** de schema: A classe de schema XDM associada à política de mesclagem. Isso especifica a classe de schema para a qual essa política de mesclagem é criada. As organizações podem criar várias políticas de mesclagem por classe de schema. Atualmente, somente a classe [!UICONTROL Perfil individual XDM] está disponível na interface do usuário. Você pode pré-visualização a schema de união para a classe de schema selecionando **[!UICONTROL Schema de União de Visualização]**. Para obter mais informações, consulte a seção [exibindo o schema de união](#view-union-schema) a seguir.
* **[!UICONTROL Arranque]** de ID: Este campo define como determinar as identidades relacionadas de um cliente. Consulte a seção sobre [costura de ID](#id-stitching) mais cedo neste guia para saber mais. Há dois valores possíveis:
   * **[!UICONTROL Nenhum]**: Não execute nenhum ajuste de identidade.
   * **[!UICONTROL Gráfico]** privado: Realize a identificação com base no seu gráfico de identidade particular.
* **[!UICONTROL Política]** de mesclagem padrão: Um botão de alternância que permite selecionar se essa política de mesclagem será ou não o padrão para sua organização. Se o seletor estiver ativado, um aviso será exibido solicitando que você confirme que deseja alterar a política de mesclagem padrão da sua organização. Consulte a seção sobre [políticas de mesclagem padrão](#default-merge-policy) neste guia para saber mais.
   ![](../images/merge-policies/create-make-default.png)

Depois que os campos obrigatórios forem preenchidos, você poderá selecionar **[!UICONTROL Próximo]** para continuar com o fluxo de trabalho.

![Uma tela Complete Configure (Configurar) com o botão Next (Avançar) realçado.](../images/merge-policies/create-complete.png)

#### [!UICONTROL Schema União visualização] {#view-union-schema}

Ao criar ou editar uma política de mesclagem, você pode visualização o schema de união para a classe de schema escolhida selecionando **[!UICONTROL Schema de União de Visualização]**.

![](../images/merge-policies/view-union-schema.png)

Isso abre a caixa de diálogo [!UICONTROL Schema de União de Visualização], mostrando todos os schemas, identidades e relacionamentos de contribuição associados ao schema de união. Você pode usar a caixa de diálogo para explorar o schema da união da mesma forma que faria acessando a guia [!UICONTROL Schema] na seção [!UICONTROL Perfis] da interface do usuário da plataforma.

Para obter informações detalhadas sobre schemas de união, incluindo como interagir com eles na guia [!UICONTROL Schema] ou na caixa de diálogo [!UICONTROL Schema de União] mostrada no fluxo de trabalho das políticas de mesclagem, visite o [guia da interface do usuário do união schema](union-schema.md).

![](../images/merge-policies/view-union-schema-dialog.png)


### [!UICONTROL Selecionar conjuntos de dados de Perfil] {#select-profile-datasets}

Na tela **[!UICONTROL Selecionar conjuntos de dados de Perfil]**, você deve selecionar o **[!UICONTROL método de mesclagem]** que deseja usar para sua política de mesclagem. Também é exibido na tela o número total de [!UICONTROL conjuntos de dados de Perfil] em sua organização relacionados à classe de schema que foi selecionada na tela anterior.

Dependendo do método de mesclagem escolhido, todos os conjuntos de dados de Perfil serão mesclados pela ordem em que foram atualizados pela última vez (carimbo de data e hora solicitado) ou será necessário selecionar quais conjuntos de dados de Perfil serão incluídos na política de mesclagem e na ordem em que serão mesclados (precedência do conjunto de dados). Para obter mais informações sobre métodos de mesclagem, reveja a seção [métodos de mesclagem](#merge-methods) fornecida anteriormente neste documento.

#### Carimbo de data e hora solicitado {#timestamp-ordered-profile}

Selecionar **[!UICONTROL Carimbo de data e hora ordenado]** como método de mesclagem significa que os atributos dos conjuntos de dados atualizados mais recentemente terão prioridade. Isso se aplica a todos os conjuntos de dados de Perfil.

![](../images/merge-policies/timestamp-ordered.png)

#### Precedência do conjunto de dados {#dataset-precedence-profile}

Selecionar **[!UICONTROL Prioridade do conjunto de dados]** como o método de mesclagem requer que você selecione conjuntos de dados de Perfil e priorize-os manualmente. Cada conjunto de dados listado também inclui o status do último lote ingerido ou exibe um aviso de que nenhum lote foi ingerido nesse conjunto de dados.

Você pode selecionar até 50 conjuntos de dados da lista de conjunto de dados para incluir na política de mesclagem. À medida que os conjuntos de dados são selecionados, eles são adicionados à seção **[!UICONTROL Selecionar conjuntos de dados]**, permitindo que você arraste e solte os conjuntos de dados e os ordene de acordo com a precedência desejada. À medida que os conjuntos de dados são ajustados na lista, o ordinal (1, 2, 3, etc) próximo ao conjunto de dados será atualizado, exibindo a prioridade (1 sendo atribuída a prioridade mais alta, depois 2 e depois).

Selecionar um conjunto de dados também atualiza a seção **[!UICONTROL schema de União]**, mostrando os campos no schema de união para os quais cada conjunto de dados contribui com dados. Para obter mais informações sobre schemas de união, incluindo como interagir com as visualizações na interface do usuário, consulte o [guia da interface do schema de união](union-schema.md)

![](../images/merge-policies/dataset-precedence.png)

### [!UICONTROL Selecionar conjuntos de dados ExperienceEvent] {#select-experienceevent-datasets}

A próxima etapa do fluxo de trabalho requer a seleção de conjuntos de dados ExperienceEvent. Essa tela é influenciada pelo método de mesclagem selecionado na tela [[!UICONTROL Selecionar conjuntos de dados de Perfil]](#select-profile-datasets).

Também é exibido nesta tela o número total de **[!UICONTROL conjuntos de dados ExperienceEvent]** criados pela organização relacionados à classe de schema selecionada na tela de configuração da política de mesclagem.

#### Carimbo de data e hora solicitado {#timestamp-ordered-experienceevent}

Se você selecionou **[!UICONTROL Carimbo de data e hora ordenado]** como o método de mesclagem para conjuntos de dados de Perfil, os atributos dos conjuntos de dados ExperienceEvent atualizados mais recentemente também terão prioridade aqui.

![](../images/merge-policies/timestamp-experienceevent.png)

#### Precedência do conjunto de dados {#dataset-precedence-experienceevent}

Se você selecionou **[!UICONTROL Precedência do conjunto de dados]** como o método de mesclagem para conjuntos de dados de Perfil, será necessário selecionar conjuntos de dados ExperienceEvent a serem incluídos. Você pode selecionar até 50 conjuntos de dados ExperienceEvent a partir da lista de conjunto de dados. À medida que os conjuntos de dados são selecionados, eles aparecem na seção [!UICONTROL Selecionar conjuntos de dados].

Os conjuntos de dados ExperienceEvent não podem ser ordenados manualmente, em vez disso, os atributos nos conjuntos de dados ExperienceEvent são anexados aos conjuntos de dados do Perfil se fizerem parte do mesmo fragmento do perfil.

Semelhante à seleção de conjuntos de dados de Perfil, a seleção de um conjunto de dados ExperienceEvent também atualiza a seção **[!UICONTROL schema de União]**, mostrando os campos no schema de união para o qual cada conjunto de dados contribui com dados. Para obter mais informações sobre schemas de união, incluindo como interagir com as visualizações na interface do usuário, consulte o [guia da interface do schema de união](union-schema.md)

![](../images/merge-policies/dataset-precedence-experienceevent.png)

### [!UICONTROL Revisão] {#review}

A etapa final do fluxo de trabalho é revisar sua política de mesclagem. A tela **[!UICONTROL Revisar]** exibe o nome da nova política de mesclagem, a classe de schema na qual ela se baseia, a opção [!UICONTROL costura de ID] selecionada, bem como o método de mesclagem e os conjuntos de dados incluídos na política de mesclagem. Para visualização de todos os conjuntos de dados de Perfil ou ExperienceEvent incluídos, selecione o número de conjuntos de dados para expandir a lista suspensa.

Certifique-se de revisar sua política de mesclagem cuidadosamente antes de selecionar **[!UICONTROL Concluir]** para concluir o fluxo de trabalho de criação.

#### Carimbo de data e hora solicitado {#timestamp-ordered-review}

Se você selecionou **[!UICONTROL Carimbo de data e hora solicitado]** como o método de mesclagem para sua política de mesclagem, a lista de conjuntos de dados de Perfil incluirá todos os conjuntos de dados que foram criados pela organização relacionados à classe de schema, em ordem de carimbo de data e hora. A lista de conjuntos de dados ExperienceEvent inclui todos os conjuntos de dados criados pela sua organização para a classe de schema escolhida e serão anexados aos conjuntos de dados de Perfil.

![](../images/merge-policies/timestamp-review.png)

#### Precedência do conjunto de dados {#dataset-precedence-review}

Se você selecionou **[!UICONTROL Precedência do conjunto de dados]** como método de mesclagem para sua política de mesclagem, as listas dos conjuntos de dados do Perfil e do ExperienceEvent incluirão apenas os conjuntos de dados do Perfil e do ExperienceEvent selecionados durante o fluxo de trabalho de criação, respectivamente. A ordem dos conjuntos de dados do Perfil deve corresponder à precedência especificada durante a criação. Caso contrário, use o botão [!UICONTROL Voltar] para retornar às etapas anteriores do fluxo de trabalho e ajustar a prioridade.

![](../images/merge-policies/dataset-precedence-review.png)

### Lista atualizada das políticas de mesclagem {#updated-list}

Depois de concluir o fluxo de trabalho para criar uma nova política de mesclagem, você retornará à guia **[!UICONTROL Mesclar políticas]**. A lista de políticas de mesclagem para sua organização agora deve incluir a política de mesclagem que você acabou de criar.

![](../images/merge-policies/new-merge-policy-created.png)

## Editar uma política de mesclagem

Na guia [!UICONTROL Mesclar políticas], você pode modificar uma política de mesclagem existente criada para a classe [!DNL XDM Individual Profile] selecionando **[!UICONTROL Nome da política]** para a política de mesclagem que deseja editar.

![Landing page de políticas de mesclagem](../images/merge-policies/select-edit.png)

Quando a tela **[!UICONTROL Editar política de mesclagem]** for exibida, você poderá fazer alterações no nome e [!UICONTROL costura de ID], bem como alterar se essa política é ou não a política de mesclagem padrão da sua organização.

Selecione **[!UICONTROL Próximo]** para continuar pelo fluxo de trabalho da política de mesclagem para atualizar o método de mesclagem e os conjuntos de dados incluídos na política de mesclagem.

![](../images/merge-policies/edit-screen.png)

Depois de fazer as alterações necessárias, reveja sua política de mesclagem e selecione **[!UICONTROL Concluir]** para retornar à guia **[!UICONTROL Mesclar políticas]**.

>[!WARNING]
>
>Alterar uma política de mesclagem pode afetar a segmentação e os resultados do perfil, pois alterará a forma como os conflitos de dados são resolvidos.

![](../images/merge-policies/edit-review.png)

## Violações da política de gestão de dados

Ao criar ou atualizar uma política de mesclagem, é realizada uma verificação para determinar se a política de mesclagem viola qualquer uma das políticas de uso de dados definidas pela organização. As políticas de uso de dados fazem parte do Adobe Experience Platform [!DNL Data Governance] e são regras que descrevem os tipos de ações de marketing às quais você tem permissão ou é restrito para realizar [!DNL Platform] dados específicos. Por exemplo, se uma política de mesclagem foi usada para criar um segmento que foi ativado para um destino de terceiros e sua organização tiver uma política de uso de dados que impedia a exportação de dados específicos para terceiros, você receberá uma notificação **[!UICONTROL Violação da política de controle de dados detectada]** ao tentar salvar sua política de mesclagem.

Esta notificação inclui uma lista de políticas de uso de dados que foram violadas e permite que você visualização os detalhes da violação selecionando uma política na lista. Ao selecionar uma política violada, a guia **[!UICONTROL Linha de dados]** fornece o motivo para a violação e as ativações afetadas, cada uma fornecendo mais detalhes sobre como a política de uso de dados foi violada.

Para saber mais sobre como o controle de dados é executado no Adobe Experience Platform, comece lendo a [visão geral do Data Governance](../../data-governance/home.md).

![](../images/merge-policies/policy-violation.png)

## Próximas etapas

Agora que você criou e configurou políticas de mesclagem para sua organização, é possível usá-las para ajustar a visualização dos perfis do cliente na Plataforma e criar segmentos de audiência a partir dos dados do Perfil. Consulte a [Visão geral da segmentação](../../segmentation/home.md) para obter mais informações sobre como criar e trabalhar com segmentos usando a interface do usuário e as APIs [!DNL Experience Platform].