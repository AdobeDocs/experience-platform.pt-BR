---
title: Criar uma conexão de origem de Marketo Engage e um fluxo de dados na interface
description: Este tutorial fornece etapas para criar uma conexão de origem de Marketo Engage e fluxo de dados na interface do usuário para trazer dados B2B para o Adobe Experience Platform.
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
source-git-commit: 744098777141c61ac27fe6f150c05469d5705dee
workflow-type: tm+mt
source-wordcount: '1831'
ht-degree: 2%

---

# Criar um [!DNL Marketo Engage] conexão de origem e fluxo de dados na interface do

>[!IMPORTANT]
>
>Antes de criar uma [!DNL Marketo Engage] conexão de origem e um fluxo de dados, primeiro verifique se você tem [ID da organização do Adobe mapeada](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html) in [!DNL Marketo]. Além disso, você também deve garantir que concluiu [preenchimento automático [!DNL Marketo] Namespaces e esquemas B2B](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md) antes de criar uma conexão de origem e um fluxo de dados.

Este tutorial fornece etapas para a criação de um [!DNL Marketo Engage] (a seguir designado por &quot;[!DNL Marketo]&quot;) conector de origem na interface do para trazer dados B2B para o Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Utilitário de geração automática de esquemas e namespaces B2B](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md): o utilitário de geração automática de esquemas e namespaces B2B permite usar [!DNL Postman] para gerar automaticamente valores para seus namespaces e esquemas B2B. Você deve concluir os namespaces e esquemas B2B primeiro, antes de criar um [!DNL Marketo] conexão de origem e fluxo de dados.
* [Origens](../../../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Experience Data Model (XDM)](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Criar e editar esquemas na interface](../../../../../xdm/ui/resources/schemas.md): saiba como criar e editar esquemas na interface do usuário.
* [Namespaces de identidade](../../../../../identity-service/features/namespaces.md): os namespaces de identidade são um componente de [!DNL Identity Service] que servem como indicadores do contexto ao qual uma identidade está relacionada. Uma identidade totalmente qualificada inclui um valor de ID e um namespace.
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
* [Sandboxes](../../../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Coletar credenciais necessárias

Para acessar seu [!DNL Marketo] conta no Experience Platform, você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---- | ---- |
| `munchkinId` | A ID do Munchkin é o identificador exclusivo de um [!DNL Marketo] instância. |
| `clientId` | A ID exclusiva do cliente do [!DNL Marketo] instância. |
| `clientSecret` | O segredo exclusivo do cliente do [!DNL Marketo] instância. |

Para obter mais informações sobre como adquirir esses valores, consulte o [[!DNL Marketo] guia de autenticação](../../../../connectors/adobe-applications/marketo/marketo-auth.md).

Depois de obter as credenciais necessárias, você poderá seguir as etapas da próxima seção.

## Conecte seu [!DNL Marketo] account

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No *aplicativos Adobe* categoria, selecione **[!UICONTROL Marketo Engage]** e selecione **[!UICONTROL Adicionar dados]**.

>[!TIP]
>
>As origens no catálogo de origens exibem a variável **[!UICONTROL Configurar]** opção quando uma determinada fonte ainda não tiver uma conta autenticada. Quando uma conta autenticada existir, essa opção será alterada para **[!UICONTROL Adicionar dados]**.

![O catálogo de origens com a origem de Marketo Engage selecionada.](../../../../images/tutorials/create/marketo/catalog.png)

A variável **[!UICONTROL Conectar conta Marketo Engage]** é exibida. Nesta página, você pode usar uma nova conta ou acessar uma conta existente.

>[!BEGINTABS]

>[!TAB Criar uma nova conta]

Para criar uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e suas credenciais.

Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para estabelecer a nova conexão.

![A nova interface de conta para autenticar uma nova conta do Marketo.](../../../../images/tutorials/create/marketo/new.png)

>[!TAB Usar uma conta existente]

Para usar uma conta existente, selecione **[!UICONTROL Conta existente]** e selecione a conta que deseja usar no catálogo de contas existente.

Selecione **[!UICONTROL Próximo]** para continuar.

![A interface de conta existente, onde é possível selecionar uma conta existente do Marketo.](../../../../images/tutorials/create/marketo/existing.png)

>[!ENDTABS]

## Selecionar um conjunto de dados

Depois de criar o [!DNL Marketo] conta, a próxima etapa fornece uma interface para você explorar [!DNL Marketo] conjuntos de dados.

A metade esquerda da interface é um navegador de diretórios, exibindo as 10 [!DNL Marketo] conjuntos de dados. Um sistema de [!DNL Marketo] a conexão de origem requer a assimilação dos nove conjuntos de dados diferentes. Se você também estiver usando a variável [!DNL Marketo] de marketing baseado em conta (ABM), você também deverá criar um 10º fluxo de dados para assimilar a [!UICONTROL Contas Nomeadas] conjunto de dados.

>[!NOTE]
>
>Para fins de brevidade, o tutorial a seguir usa [!UICONTROL Oportunidades] exemplo, mas as etapas descritas abaixo aplicam-se a qualquer um dos 10 [!DNL Marketo] conjuntos de dados.

Selecione o conjunto de dados que você deseja assimilar. Isso atualiza a interface para exibir uma visualização do conjunto de dados. Quando terminar, selecione **[!UICONTROL Próxima]**.

![A interface de visualização](../../../../images/tutorials/create/marketo/preview.png)

## Fornecer detalhes do conjunto de dados e do fluxo de dados {#provide-dataset-and-dataflow-details}

Em seguida, você deve fornecer informações sobre seu conjunto de dados e seu fluxo de dados.

### Detalhes do conjunto de dados {#dataset-details}

Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados, normalmente uma tabela, que contém um esquema (colunas) e campos (linhas). Os dados assimilados com sucesso no Experience Platform são armazenados no data lake como conjuntos de dados. Durante essa etapa, você pode criar um novo conjunto de dados ou usar um conjunto de dados existente.

>[!BEGINTABS]

>[!TAB Usar um novo conjunto de dados]

Para usar um novo conjunto de dados, selecione **[!UICONTROL Novo conjunto de dados]** e forneça um nome e uma descrição opcional para seu conjunto de dados. Você também deve selecionar um esquema do Experience Data Model (XDM) ao qual seu conjunto de dados adere.

![A nova interface de seleção do conjunto de dados.](../../../../images/tutorials/create/marketo/new-dataset.png)

>[!TAB Usar um conjunto de dados existente]

Se você já tiver um conjunto de dados, selecione **[!UICONTROL Conjunto de dados existente]** e, em seguida, use o **[!UICONTROL Pesquisa avançada]** opção para exibir uma janela de todos os conjuntos de dados em sua organização, incluindo seus respectivos detalhes, como se eles estão habilitados para assimilação no Perfil do cliente em tempo real ou não.

![A interface de seleção do conjunto de dados existente.](../../../../images/tutorials/create/marketo/existing-dataset.png)

>[!ENDTABS]

### Configurações de fluxo de dados {#dataflow-configurations}

>[!IMPORTANT]
>
>A variável [!DNL Marketo] A origem usa a assimilação em lote para assimilar todos os registros históricos e a assimilação por transmissão para atualizações em tempo real. Isso permite que a origem continue a transmitir enquanto assimila registros incorretos. Ativar o **[!UICONTROL Assimilação parcial]** alterne e defina o [!UICONTROL Limite de erro %] ao máximo para evitar a falha do fluxo de dados.

Se o conjunto de dados estiver ativado para o Perfil de cliente em tempo real, durante essa etapa é possível alternar **[!UICONTROL Conjunto de dados Perfil]** para ativar seus dados para assimilação de perfis. Você também pode usar esta etapa para habilitar **[!UICONTROL Diagnóstico de erro]** e **[!UICONTROL Assimilação parcial]**.

* **[!UICONTROL Diagnóstico de erro]**: Selecionar **[!UICONTROL Diagnóstico de erro]** para instruir a origem a produzir diagnósticos de erro que você poderá consultar posteriormente ao monitorar a atividade do conjunto de dados e o status do fluxo de dados.
* **[!UICONTROL Assimilação parcial]**: [Assimilação parcial de lote](../../../../../ingestion/batch-ingestion/partial.md) é a capacidade de assimilar dados que contêm erros, até um determinado limite configurável. Esse recurso permite assimilar com sucesso todos os seus dados precisos no Experience Platform, enquanto todos os seus dados incorretos são armazenados em lote separadamente com informações sobre por que são inválidos.

Durante essa etapa, é possível ativar **[!UICONTROL Fluxo de dados de exemplo]** limitar a assimilação de dados e evitar custos adicionais decorrentes da assimilação de todos os dados históricos, incluindo identidades de pessoa.

>[!BEGINSHADEBOX]

**Guia rápido sobre como usar amostra de fluxo de dados**

A amostra de fluxo de dados é uma configuração que pode ser definida para o seu [!DNL Marketo] fluxo de dados para limitar a taxa de assimilação e experimentar os recursos de Experience Platform sem precisar assimilar grandes quantidades de dados.

* Ative o fluxo de dados de amostra para limitar os dados históricos, assimilando até 100 mil (da maior ID de registro) registros ou até os últimos 10 dias de atividade durante o trabalho de preenchimento retroativo.
* Ao usar a configuração de fluxo de dados de amostra para todas as entidades B2B, você deve considerar que é possível que alguns registros relacionados possam estar ausentes, pois todo o histórico dos dados de origem não é assimilado.

>[!ENDSHADEBOX]

![A seção de configurações do fluxo de dados da página de detalhes do fluxo de dados.](../../../../images/tutorials/create/marketo/dataflow-configurations.png)

Além disso, se estiver assimilando dados do conjunto de dados das empresas, você pode ativar **[!UICONTROL Excluir contas não solicitadas]** para excluir da assimilação contas não solicitadas.

Quando indivíduos preenchem um formulário, [!DNL Marketo] cria um registro de conta fantasma com base no Nome da empresa que não contém outros dados. Para novos fluxos de dados, a alternância para excluir contas não solicitadas é habilitada por padrão. Para fluxos de dados existentes, você pode ativar ou desativar o recurso, com alterações aplicáveis a dados recém-assimilados e a dados não existentes.

![Excluir contas não solicitadas](../../../../images/tutorials/create/marketo/unclaimed-accounts.png)

## Mapeie seu [!DNL Marketo] campos de origem do conjunto de dados para campos XDM de destino

A variável [!UICONTROL Mapeamento] é exibida, fornecendo uma interface para mapear os campos de origem do esquema de origem para os campos XDM de destino apropriados no esquema de destino.

Each [!DNL Marketo] O conjunto de dados tem suas próprias regras de mapeamento específicas a serem seguidas. Consulte o seguinte para obter mais informações sobre como mapear [!DNL Marketo] conjuntos de dados para XDM:

* [Atividades](../../../../connectors/adobe-applications/mapping/marketo.md#activities)
* [Programas](../../../../connectors/adobe-applications/mapping/marketo.md#programs)
* [Associações ao programa](../../../../connectors/adobe-applications/mapping/marketo.md#program-memberships)
* [Empresas](../../../../connectors/adobe-applications/mapping/marketo.md#companies)
* [Listas estáticas](../../../../connectors/adobe-applications/mapping/marketo.md#static-lists)
* [Associações de lista estática](../../../../connectors/adobe-applications/mapping/marketo.md#static-list-memberships)
* [Contas Nomeadas](../../../../connectors/adobe-applications/mapping/marketo.md#named-accounts)
* [Oportunidades](../../../../connectors/adobe-applications/mapping/marketo.md#opportunities)
* [Funções do contato da oportunidade](../../../../connectors/adobe-applications/mapping/marketo.md#opportunity-contact-roles)
* [Pessoas](../../../../connectors/adobe-applications/mapping/marketo.md#persons)

Com base nas suas necessidades, você pode optar por mapear campos diretamente ou usar funções de preparação de dados para transformar dados de origem para derivar valores calculados ou calculados. Para obter etapas abrangentes sobre como usar a interface de mapeamento, consulte [Guia da interface de preparação de dados](../../../../../data-prep/ui/mapping.md).

![A interface de mapeamento dos dados do Marketo.](../../../../images/tutorials/create/marketo/mapping.png)

Quando os conjuntos de mapeamento estiverem prontos, selecione **[!UICONTROL Próxima]** e aguarde alguns instantes para que o novo fluxo de dados seja criado.

## Revisar seu fluxo de dados

A variável **[!UICONTROL Revisão]** é exibida, permitindo que você revise seu novo fluxo de dados antes de ele ser criado. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: mostra o tipo de origem, o caminho relevante da entidade de origem escolhida e a quantidade de colunas nessa entidade de origem.
* **[!UICONTROL Atribuir conjunto de dados e mapear campos]**: mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o esquema ao qual o conjunto de dados adere.

Depois de revisar o fluxo de dados, selecione **[!UICONTROL Salvar e assimilar]** e aguarde algum tempo para criar o fluxo de dados.

![A página de revisão onde é possível confirmar os detalhes do fluxo de dados antes da assimilação.](../../../../images/tutorials/create/marketo/review.png)

## Monitorar seu fluxo de dados

Depois que o fluxo de dados for criado, você poderá monitorar os dados que estão sendo assimilados por meio dele para ver informações sobre taxas de assimilação, sucesso e erros. Para obter mais informações sobre como monitorar fluxos de dados, consulte o tutorial sobre [monitoramento de fluxos de dados na interface do](../../../../../dataflows/ui/monitor-sources.md).

## Excluir seus atributos

Os atributos personalizados em conjuntos de dados não podem ser ocultos ou removidos retroativamente. Se quiser ocultar ou remover um atributo personalizado de um conjunto de dados existente, você deverá criar um novo conjunto de dados sem esse atributo personalizado, um novo esquema XDM e configurar um novo fluxo de dados para o novo conjunto de dados criado. Você também deve desativar ou excluir o fluxo de dados original que consiste no conjunto de dados com o atributo personalizado que deseja ocultar ou remover.

## Excluir seu fluxo de dados

É possível excluir fluxos de dados que não são mais necessários ou que foram criados incorretamente usando o **[!UICONTROL Excluir]** disponível na [!UICONTROL Fluxos de dados] espaço de trabalho. Para obter mais informações sobre como excluir fluxos de dados, consulte o tutorial sobre [exclusão de fluxos de dados na interface](../../delete.md).

## Próximas etapas

Ao seguir este tutorial, você criou com sucesso um fluxo de dados para assimilar dados B2B de suas [!DNL Marketo Engage] origem para Experience Platform.

## Apêndice {#appendix}

As seções a seguir fornecem diretrizes adicionais que você pode seguir ao usar o [!DNL Marketo] origem.

### Mensagens de erro na interface {#error-messages}

As seguintes mensagens de erro são exibidas na interface do usuário quando o Platform detecta problemas com sua configuração:

#### [!DNL Munchkin ID] não está mapeado para a organização apropriada

A autenticação será negada se o [!DNL Munchkin ID] não está mapeado para a organização de plataforma que você está usando. Configure o mapeamento entre as [!DNL Munchkin ID] e sua organização usando o [[!DNL Marketo] interface](https://app-sjint.marketo.com/#MM0A1).

![Uma mensagem de erro que exibe que a instância do Marketo não está mapeada corretamente para a organização Adobe.](../../../../images/tutorials/create/marketo/munchkin-not-mapped.png)

#### Identidade principal ausente

Um fluxo de dados não será salvo e assimilado se uma identidade principal estiver ausente. Assegure que [existe uma identidade primária em seu esquema XDM](../../../../../xdm/tutorials/create-schema-ui.md), antes de tentar configurar um fluxo de dados.

![Uma mensagem de erro que exibe que a identidade principal está ausente do esquema XDM.](../../../../images/tutorials/create/marketo/no-primary-identity.png)

