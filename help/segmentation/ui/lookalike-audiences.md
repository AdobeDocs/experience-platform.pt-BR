---
solution: Experience Platform
title: Públicos-alvo semelhantes
description: Saiba como direcionar novos públicos-alvo de alto valor no Adobe Experience Platform usando públicos-alvo semelhantes.
badgeLimitedAvailability: label="Disponibilidade limitada" type=Caution
hide: true
hidefromtoc: true
source-git-commit: d0b839dfc35ff9f8b4db34c61d2cdd820bfd448b
workflow-type: tm+mt
source-wordcount: '1937'
ht-degree: 0%

---


# Guia de públicos-alvo semelhantes

>[!IMPORTANT]
>
>Observe que os insights de semelhança e os Públicos-alvo de semelhança estão em **disponibilidade limitada**.

No Adobe Experience Platform, os Públicos-alvo semelhantes fornecem insights inteligentes sobre cada um dos públicos-alvo, aproveitando insights baseados em aprendizado de máquina para identificar e direcionar clientes de alto valor com suas campanhas de marketing.

Com Públicos-alvo semelhantes, é possível criar públicos-alvo expandidos que direcionem os clientes semelhantes aos seus públicos-alvo de alto desempenho ou que direcionem os clientes semelhantes aos públicos-alvo convertidos anteriormente.

## Terminologia {#terminology}

Antes de começar a usar Públicos-alvo semelhantes, compreenda os seguintes conceitos:

- **Público base**: o público-alvo base é aquele sobre o qual você deseja obter mais insights. Este é o público-alvo do modelo semelhante **baseado** em.
- **Modelo semelhante**: um modelo semelhante é um modelo de aprendizado de máquina treinado em cada público-alvo básico elegível sem nenhuma contribuição do cliente. Cada modelo semelhante cria os fatores influentes e gráficos de similaridade. Um modelo semelhante não **não** obtenha pontuação.
- **Público-alvo semelhante**: um Público-alvo semelhante é o público-alvo criado quando um modelo semelhante com um limite de similaridade selecionado é aplicado ao público-alvo base. Você pode criar vários Públicos-alvo semelhantes usando o mesmo modelo semelhante. O Público-alvo semelhante é o que recebe a pontuação.
- **Tamanho total do público endereçável**: o tamanho total do público-alvo endereçável é o número total de perfis nos últimos 30 dias menos a população base do público-alvo nos últimos 30 dias. Por exemplo, se um cliente tiver 10 milhões de perfis nos últimos 30 dias e o público base tiver 1 milhão de perfis nos últimos 30 dias, o tamanho total do público endereçável será de 9 milhões de perfis.

## Detalhes do modelo semelhante {#details}

No Adobe Experience Platform, o modelo semelhante consome três tipos diferentes de pontos de dados:

- Associação de público-alvo nos últimos 30 dias
- Eventos de experiência dos últimos 30 dias que foram assimilados no Perfil do cliente em tempo real
- Atributos de perfil nos últimos 30 dias que foram assimilados no Perfil do cliente em tempo real

Todos esses pontos de dados são transformados em pares de valores principais que são alimentados no modelo semelhante. Somente os pares de valores principais com uma porcentagem significativa de perfis correspondentes serão mantidos.

O modelo semelhante é executado com frequência, criando e recriando os fatores influentes e gráficos de similaridade para os públicos-alvo básicos. A pontuação para públicos-alvo semelhantes também é executada com frequência.

## Direitos {#entitlements}

Os seguintes direitos se aplicam ao uso de Públicos-alvo semelhantes:

- Os clientes do Real-Time CDP Prime têm direito a **5** Públicos-alvo semelhantes ativos em sandboxes de produção
- Os clientes do Real-Time CDP Ultimate têm direito a **20** Públicos-alvo semelhantes ativos em sandboxes de produção
- As sandboxes de desenvolvimento estão limitadas a **5** Públicos-alvo semelhantes para todos os clientes da Real-Time CDP

Estão disponíveis pacotes complementares que aumentam os direitos para sandboxes de produção em 20 públicos-alvo semelhantes por pacote.

Para confirmar se você tem acesso a Públicos-alvo semelhantes, entre em contato com o representante da Adobe.

## Exibir insights semelhantes {#view}

Os insights semelhantes são incorporados à página de detalhes do público-alvo. Para analisar os insights semelhantes de um público, selecione **[!UICONTROL Públicos-alvo]** na barra de navegação à esquerda, seguido por **[!UICONTROL Procurar]** e o público-alvo para o qual você deseja exibir os insights.

![O botão Públicos-alvo é realçado, assim como o público-alvo base que está sendo usado para modelagem semelhante.](../images/ui/lookalike-audiences/browse.png)

A página de detalhes do público-alvo é exibida. Selecionar **[!UICONTROL Insights semelhantes]** para exibir os insights semelhantes do público-alvo. A variável **[!UICONTROL Insights semelhantes]** é exibida. Esta página tem três elementos principais: o gráfico de similaridade e alcance, o Público-alvo semelhante e os fatores influentes.

![A guia Insights semelhantes é destacada, exibindo os insights semelhantes para o público-alvo base.](../images/ui/lookalike-audiences/look-alike-insights.png)

### Semelhança e alcance {#similarity-and-reach}

<!-- >[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_similarityAndReach"
>title="Similarity and reach"
>abstract="" -->

A seção similaridade e alcance exibe um gráfico que representa o alcance esperado de um público-alvo semelhante que consiste em perfis acima de uma pontuação de similaridade fornecida. A pontuação de similaridade representa a **distância** de semelhança entre o perfil do público-alvo básico e o perfil do insight semelhante.

![O gráfico de similaridade e alcance é destacado.](../images/ui/lookalike-audiences/similarity-and-reach.png)

Nesse gráfico, o eixo x mede a porcentagem de similaridade entre um perfil e os membros do público-alvo selecionado. A pontuação de similaridade varia de 0% a 100%, com uma pontuação de similaridade maior indicando que um perfil está mais próximo, em termos de valores de fatores influentes, dos membros do público selecionado.

O eixo y mostra a contagem esperada de perfis com o percentual de similaridade que corresponde ao valor correspondente do eixo x. Essa contagem esperada de perfis varia de 0 ao tamanho total do público-alvo endereçável ou 25 milhões de perfis, o que for menor. Esse eixo é medido em uma **escala logarítmica** para melhorar a legibilidade do gráfico.

Observe que o gráfico é **cumulativo** da direita para a esquerda. Isso significa que, em qualquer ponto do gráfico, o valor do eixo y é o número de perfis com similaridade **acima** o limite de similaridade. Por exemplo, se o eixo x estiver em 60% e o eixo y estiver em 10 milhões, isso significa que há 10 milhões de perfis com uma similaridade em ou acima de 60% para o público base.

Você pode passar o mouse sobre um ponto específico do gráfico para exibir a porcentagem de similaridade e a contagem de perfis esperada para o ponto destacado no momento.

### Públicos-alvo semelhantes {#list}

A seção Públicos-alvo semelhantes exibe uma lista de todos os Públicos-alvo semelhantes criados anteriormente para o público-alvo básico selecionado.

![A seção Públicos-alvo semelhantes é destacada.](../images/ui/lookalike-audiences/select-laa.png)

### Fatores influentes {#influential-factors}

<!-- >[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_influentialFactors"
>title="Influential factors"
>abstract="Influential factors are attributes, events and audience memberships that are important in explaining similarity of a profile to members of the base audience. Data usage labels and policies can be used to exclude certain data from being considered as influential factors in look-alike models."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/lookalike-audiences.html?lang=en#exclude" text="Exclude data" -->

A seção Fatores influentes exibe os 100 principais fatores que influenciam o modelo semelhante para o público-alvo básico selecionado. Esses fatores influentes são os atributos do perfil, os eventos de experiência e as associações de público-alvo que são os mais importantes para explicar as semelhanças no público-alvo básico. Entender os principais fatores influentes permite personalizar melhor o conteúdo de marketing para esse público-alvo e qualquer público semelhante criado a partir dele. Observe que nem todos os fatores influentes que afetam o modelo semelhante serão exibidos.

Para fatores influentes que são numéricos, os pares de valores principais podem ser colocados em compartimentos, dependendo do número de valores diferentes que a chave tem. Por exemplo, se você tiver uma chave de `income`, provavelmente haveria muitos valores únicos. Como resultado, os pares de valores principais serão colocados em compartimentos que podem ter a aparência de `income=[0 -> 30000]`, `income=[30000 -> 50000]`, e `income=[50000 -> 100000]`.

Esses buckets são recalculados regularmente para garantir que os dados sejam mantidos atualizados.

![A seção fatores influentes é destacada.](../images/ui/lookalike-audiences/influential-factors.png)

>[!NOTE]
>
>Os fatores influentes são ordenados por ordem de importância e são independentes uns dos outros.

| Campo | Descrição |
| ----- | ----------- |
| Tipo | O tipo de dados do qual o fator influente é derivado. Pode ser um atributo de perfil, um evento de experiência ou uma associação de público-alvo. |
| Chave | O nome do campo de dados. Para chaves do tipo de associação de público, esse valor representa o **namespace** do público-alvo de onde os dados vêm. Os valores possíveis incluem `ups` (Serviço de segmentação) e `AO` Orquestração de público-alvo. Para chaves de outros tipos, esse valor representa o caminho do campo XDM. Por exemplo, se a empresa Luma tiver um campo personalizado chamado receita, a chave será `_luma.income` |
| Valor | O valor varia dependendo do fator influente que ele representa. Para atributos de perfil ou eventos de experiência, esse campo representa o valor ou o intervalo de valores do campo de dados que indica a similaridade com os membros do público-alvo base. O intervalo de valores é gravado no formulário `[A -> B]`, onde `A` representa o intervalo inferior enquanto `B` representa o intervalo mais alto. Para associações de público, esse campo é o nome do público. |
| Importância | O nível relativo de importância do fator influente. Pode ser alto, médio ou baixo. |

## Criar um público-alvo semelhante {#create}

>[!IMPORTANT]
>
>Você **não é possível** use um Público-alvo semelhante como o público-alvo base de outro Público-alvo semelhante. Ou seja, você **não é possível** criar Públicos-alvo semelhantes encadeados.

Para criar um Público-alvo semelhante, será necessário selecionar o público-alvo do qual deseja basear o Público-alvo semelhante. Para acessar a lista de públicos disponíveis, selecione **[!UICONTROL Públicos-alvo]** na barra de navegação à esquerda, seguido por **[!UICONTROL Procurar]**. A lista de públicos-alvo é exibida. Nesta página, você pode selecionar o público-alvo que deseja usar como público-alvo base.

![O botão Públicos-alvo é realçado, assim como o público-alvo base que está sendo usado para modelagem semelhante.](../images/ui/lookalike-audiences/browse.png)

Na página de detalhes do público, selecione **[!UICONTROL Criar público-alvo semelhante]** para iniciar o processo de criação de um Público-alvo semelhante.

![A variável [!UICONTROL Criar público-alvo semelhante] é realçado.](../images/ui/lookalike-audiences/create-look-alike-audience.png)

A variável **[!UICONTROL Criar um público-alvo semelhante]** popover é exibido. Nesta página, é possível definir a porcentagem de similaridade para o Público-alvo semelhante.

![A variável [!UICONTROL Criar um público-alvo semelhante] o popover é exibido.](../images/ui/lookalike-audiences/create-audience.png)

Você pode definir essa porcentagem de similaridade de três maneiras diferentes:

- Mova o controle deslizante para definir a porcentagem de similaridade
- Digite a porcentagem de similaridade na caixa de entrada numérica ao lado do controle deslizante
- Passe o mouse sobre o gráfico e selecione o local desejado para definir a porcentagem de similaridade

Você também pode atualizar detalhes sobre o Público-alvo semelhante, incluindo o nome e a descrição. Por padrão, o nome do Público-alvo semelhante será gerado com base no nome do público-alvo base e na porcentagem de similaridade especificada anteriormente.

![As informações básicas são destacadas no campo [!UICONTROL Criar um público-alvo semelhante] popover.](../images/ui/lookalike-audiences/basic-info.png)

Selecionar **[!UICONTROL Criar]** para concluir a criação do Público-alvo semelhante.

![O botão create é realçado dentro do [!UICONTROL Criar um público-alvo semelhante] popover.](../images/ui/lookalike-audiences/create-audience.png)

O público-alvo semelhante recém-criado pode ser acessado na **[!UICONTROL Públicos-alvo semelhantes]** da página de detalhes do público-alvo e também está disponível no Portal de público-alvo e para outros usos downstream. Observe que levará algum tempo para que o Público-alvo semelhante seja pontuado. Até que seja pontuada, a contagem de perfis parecerá ser 0.

## Exibir detalhes do Público-alvo semelhante {#view-details}

Para exibir detalhes de um Público-alvo semelhante, selecione o Público-alvo semelhante na **[!UICONTROL Públicos-alvo semelhantes]** seção do público-alvo base.

![A seção Públicos-alvo semelhantes é destacada.](../images/ui/lookalike-audiences/select-laa.png)

A página de detalhes do público-alvo é exibida. Para obter mais informações nesta página, leia a [seção de detalhes do público-alvo do guia da interface do usuário do Serviço de segmentação](./overview.md#audience-details).

![Os detalhes do Público-alvo semelhante são exibidos.](../images/ui/lookalike-audiences/laa-details.png)

## Excluir campos de dados da modelagem semelhante {#exclude}

Os Públicos-alvo semelhantes podem ser configurados para excluir campos de dados restritos para a ação de marketing &quot;Ciência de dados&quot; aplicando os rótulos e as políticas de uso de dados relevantes. Os dados rotulados como restritos de uso para ciência de dados serão removidos da consideração ao treinar um modelo de Público-alvo semelhante e ao gerar um Público-alvo semelhante do modelo treinado. 

O rótulo &quot;C9&quot; padrão pode ser usado para rotular dados que não devem ser usados para ciência de dados e pode ser aplicado ativando a política &quot;Restringir ciência de dados&quot; padrão. Você também pode criar políticas adicionais para restringir o uso de dados com outros rótulos, incluindo rótulos confidenciais, para ciência de dados. Para obter mais informações sobre como gerenciar políticas de uso de dados, leia a [guia da interface de políticas de uso de dados](../../data-governance/policies/user-guide.md). Para obter mais informações sobre como gerenciar rótulos de uso de dados, leia a [guia da interface do usuário de rótulos de uso de dados](../../data-governance/labels/user-guide.md).

Por padrão, o processo de modelagem para Públicos-alvo semelhantes excluirá **qualquer** campo, conjunto de dados ou público-alvo com base na política de privacidade ativada para sua organização. Se o público-alvo base não tiver rótulos de contrato, o processo de modelagem excluirá **qualquer** campo, conjunto de dados ou público-alvo com base na política de privacidade ativada para sua organização.

Observe que **você** são responsáveis por garantir que os dados, incluindo os dados confidenciais, sejam rotulados adequadamente e que as políticas de uso de dados tenham sido definidas e ativadas para cumprir as obrigações legais e regulamentares sob as quais você opera. Você também deve estar ciente de que os campos de dados ou as associações de segmento que estão **não** diretamente correlacionada a campos de dados normalmente associados a tipos de dados confidenciais ou protegidos pode ser uma fonte de potencial viés. **Você** são responsáveis pela análise de seus dados para identificar, rotular e aplicar as políticas de uso de dados apropriadas aos seus dados, incluindo quaisquer campos de dados que possam servir de proxy para tipos de dados confidenciais ou protegidos e devem ser excluídos da modelagem.

## Próximas etapas

Depois de ler este guia, você aprendeu a visualizar insights semelhantes e criar Públicos-alvo semelhantes com base nesses insights. Para obter mais informações sobre públicos-alvo na interface do Adobe Experience Platform, leia a [Guia da interface do usuário do serviço de segmentação](./overview.md).