---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guia do usuário de políticas de mesclagem
topic: guide
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '1104'
ht-degree: 0%

---


# Guia do usuário de políticas de mesclagem

O Adobe Experience Platform permite que você reúna dados de várias fontes e os combine para ver uma visualização completa de cada um de seus clientes individuais. Ao reunir esses dados, as políticas de mesclagem são as regras que [!DNL Platform] usam para determinar como os dados serão priorizados e quais dados serão combinados para criar essa visualização unificada.

Usando RESTful APIs ou a interface do usuário, você pode criar novas políticas de mesclagem, gerenciar políticas existentes e definir uma política de mesclagem padrão para sua organização. Este guia fornece instruções passo a passo para trabalhar com políticas de mesclagem usando a interface do usuário do Adobe Experience Platform.

Se preferir trabalhar com políticas de mesclagem usando a [!DNL Real-time Customer Profile] API, siga as instruções descritas no tutorial [da API de políticas de](../api/merge-policies.md)mesclagem.

## Introdução

Este guia exige uma compreensão funcional dos diversos [!DNL Experience Platform] serviços envolvidos nas políticas de fusão. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

* [!DNL Real-time Customer Profile](../home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
* [!DNL Identity Service](../../identity-service/home.md): Habilita [!DNL Real-time Customer Profile] a união de identidades de fontes de dados diferentes em [!DNL Platform]que estão sendo ingeridas.
* [!DNL Experience Data Model (XDM)](../../xdm/home.md): A estrutura padronizada pela qual [!DNL Platform] organiza os dados de experiência do cliente.

## políticas de mesclagem de Visualização

Na interface do [!DNL Experience Platform] usuário, você pode começar a trabalhar com políticas de mesclagem e ver uma lista das políticas de mesclagem existentes de sua organização clicando em **[!UICONTROL Perfil]** no painel esquerdo e selecionando a guia **[!UICONTROL Mesclar políticas]** .

![landing page de políticas de mesclagem](../images/merge-policies/landing.png)

Os detalhes de cada política de mesclagem disponível para sua organização estão visíveis na landing page, incluindo o Nome *[!UICONTROL da]* política, a Política *[!UICONTROL de mesclagem]* padrão e o *[!UICONTROL Schema]*.

Para selecionar quais detalhes estão visíveis ou para adicionar outras colunas à exibição, selecione o ícone do seletor de colunas à direita e clique no nome de uma coluna para adicioná-la ou removê-la da visualização.

![](../images/merge-policies/adjust-view.png)

## Criar uma política de mesclagem

Para criar uma nova política de mesclagem, clique em **[!UICONTROL Criar política]** de mesclagem perto da parte superior direita da guia **[!UICONTROL Mesclar políticas]** .

![landing page de políticas de mesclagem](../images/merge-policies/create-new.png)

A tela **[!UICONTROL Criar política]** de mesclagem é exibida, permitindo que você forneça informações importantes para sua nova política de mesclagem.

![](../images/merge-policies/create.png)

* **[!UICONTROL Nome]**: O nome da sua política de mesclagem deve ser descritivo, mas conciso.
* **[!UICONTROL Schema]**: O schema associado à política de mesclagem. Isso especifica o schema XDM para o qual essa política de mesclagem é criada. As organizações podem criar várias políticas de mesclagem por schema.
* **[!UICONTROL Arranque]** de ID: Este campo define como determinar as identidades relacionadas de um cliente. Há dois valores possíveis:
   * **[!UICONTROL Nenhum]**: Não execute nenhum ajuste de identidade.
   * **[!UICONTROL Gráfico]** privado: Realize a identificação com base no seu gráfico de identidade particular.
* **[!UICONTROL Mesclagem]** de atributos: Um fragmento de perfil são as informações do perfil para apenas uma identidade fora da lista de identidades existentes para um cliente individual. Quando o tipo de gráfico de identidade usado resulta em mais de uma identidade, há o potencial para valores de propriedade de perfil conflitantes e a prioridade deve ser especificada. Usar a mesclagem *de* atributos permite especificar quais valores de perfil de conjunto de dados priorizarão se ocorrer um conflito de mesclagem. Há dois valores possíveis:
   * **[!UICONTROL Carimbo de data e hora solicitado]**: Em caso de conflito, dê prioridade ao perfil que foi atualizado mais recentemente.
   * **[!UICONTROL Precedência]** do conjunto de dados: Atribua prioridade aos fragmentos do perfil com base no conjunto de dados de onde eles vieram. Ao selecionar essa opção, você deve selecionar os conjuntos de dados relacionados e sua ordem de prioridade. Consulte os detalhes sobre a precedência [do conjunto de](#dataset-precedence) dados abaixo para obter mais informações.
* **[!UICONTROL Política]** de mesclagem padrão: Um botão de alternância que permite selecionar se essa política de mesclagem será ou não o padrão para sua organização. Se o seletor estiver ativado e a nova política for salva, sua política padrão anterior será atualizada automaticamente para não ser mais o padrão.

### Precedência do conjunto de dados {#dataset-precedence}

Ao selecionar um valor de mesclagem *[!UICONTROL de]* Atributo, você pode selecionar a precedência *[!UICONTROL de]* Conjunto de Dados que permite que você atribua prioridade aos fragmentos de perfil com base no conjunto de dados de onde eles vieram.

Um exemplo de caso de uso seria se sua organização tivesse informações presentes em um conjunto de dados que seja preferencial ou confiável em relação aos dados em outro conjunto de dados.

Ao selecionar a precedência *[!UICONTROL do]* Conjunto de Dados, um painel separado é aberto, exigindo que você selecione dos conjuntos de dados ** Disponíveis (ou use a caixa de seleção para selecionar todos) quais conjuntos de dados serão incluídos. Em seguida, você pode arrastar e soltar esses conjuntos de dados no painel Conjuntos de dados ** selecionados e arrastá-los para a ordem de prioridade correta. O conjunto de dados principal terá prioridade máxima, o segundo conjunto de dados será o segundo mais alto e assim por diante.

![](../images/merge-policies/dataset-precedence.png)

Após terminar de criar a política de mesclagem, clique em **[!UICONTROL Salvar]** para retornar à guia *[!UICONTROL Mesclar políticas]* , onde sua nova política de mesclagem agora aparece na lista de políticas.

## Editar uma política de mesclagem

Você pode modificar uma política de mesclagem existente por meio da guia *[!UICONTROL Mesclar políticas]* clicando em Nome *[!UICONTROL da]* política para a política de mesclagem que deseja editar.

![landing page de políticas de mesclagem](../images/merge-policies/select-edit.png)

Quando a tela *[!UICONTROL Editar política]* de mesclagem for exibida, você poderá fazer alterações no *[!UICONTROL Nome]*, no *[!UICONTROL Schema]*, no tipo de agrupamento *[!UICONTROL de]* ID e no tipo de mesclagem ** ** Atributo, bem como selecionar se essa política será ou não a política de mesclagem Padrão para a sua organização.

>[!NObservação]
>Não é possível editar a ID da política de mesclagem, exibida na parte superior da tela de edição. Esta é uma ID gerada pelo sistema e somente leitura que não pode ser alterada.

![](../images/merge-policies/edit-screen.png)

Depois de fazer as alterações necessárias, clique em **[!UICONTROL Salvar]** para retornar à guia *[!UICONTROL Mesclar políticas]* , onde as informações atualizadas da política de mesclagem agora estão visíveis.

![](../images/merge-policies/edited.png)

## Violações da política de gestão de dados

Ao criar ou atualizar uma política de mesclagem, é realizada uma verificação para determinar se a política de mesclagem viola qualquer uma das políticas de uso de dados definidas pela organização. As políticas de uso de dados fazem parte do Adobe Experience Platform [!DNL Data Governance] e são regras que descrevem os tipos de ações de marketing às quais você tem permissão ou é restrito para executar em dados específicos [!DNL Platform] . Por exemplo, se uma política de mesclagem foi usada para criar um segmento que foi ativado para um destino de terceiros e sua organização tiver uma política de uso de dados que impedia a exportação de dados específicos para terceiros, você receberá uma notificação &quot;Violação de política de controle de dados detectada&quot; ao tentar salvar sua política de mesclagem.

Esta notificação inclui uma lista de políticas de uso de dados que foram violadas e permite que você visualização os detalhes da violação selecionando uma política na lista. Ao selecionar uma política violada, a guia de linhagem ** Dados fornece o *Motivo da violação* e as ativações ** Afetadas, cada uma fornecendo mais detalhes sobre como a política de uso de dados foi violada.

Para saber mais sobre como o controle de dados é executado no Adobe Experience Platform, comece lendo a visão geral [do](../../data-governance/home.md)Data Governance.

![](../images/merge-policies/policy-violation.png)

## Próximas etapas

Agora que você criou e configurou políticas de mesclagem para sua Organização IMS, é possível usá-las para criar segmentos de audiência a partir dos dados do perfil. Consulte a visão geral [da](../../segmentation/home.md) segmentação para obter mais informações sobre como criar e trabalhar com segmentos usando [!DNL Experience Platform].