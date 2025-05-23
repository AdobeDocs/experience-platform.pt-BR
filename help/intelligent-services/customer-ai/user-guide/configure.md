---
keywords: Experience Platform;guia do usuário;ia do cliente;tópicos populares;configurar instância;criar instância;;user guide;customer ai;popular topics;configure instance;create instance;
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Configurar uma instância da IA do cliente
description: Os Serviços de IA/ML fornecem IA do cliente como um serviço da Adobe Sensei simples de usar que pode ser configurado para casos de uso diferentes. As seções a seguir fornecem etapas para configurar uma instância da IA do cliente.
exl-id: 78353dab-ccb5-4692-81f6-3fb3f6eca886
source-git-commit: 73dea391f8fcb1d2d491c814b453afb4e538459d
workflow-type: tm+mt
source-wordcount: '3092'
ht-degree: 0%

---


# Configurar uma instância da IA do cliente

A IA do cliente, como parte dos Serviços de IA/ML, permite gerar pontuações de propensão personalizadas sem precisar se preocupar com o aprendizado de máquina.

Os Serviços de IA/ML fornecem IA do cliente como um serviço da Adobe Sensei simples de usar que pode ser configurado para casos de uso diferentes. As seções a seguir fornecem etapas para configurar uma instância da IA do cliente.

## Criar uma instância {#set-up-your-instance}

Na interface do usuário do Experience Platform, selecione **[!UICONTROL Serviços]** na navegação à esquerda. O navegador **[!UICONTROL Serviços]** é exibido e exibe todos os serviços disponíveis à sua disposição. No contêiner da IA do cliente, selecione **[!UICONTROL Abrir]**.

![Navegue até o serviço IA do cliente na interface do usuário do Experience Platform.](../images/user-guide/navigate-to-service.png)

A interface do usuário da **IA do cliente** é exibida e mostra todas as instâncias de serviço.

- Você pode encontrar a métrica **[!UICONTROL Total de perfis pontuados]** localizada no lado inferior direito do contêiner **[!UICONTROL Criar instância]**. Essa métrica rastreia o número total de perfis pontuados pela IA do cliente no ano civil atual, incluindo todos os ambientes de sandbox e todas as instâncias de serviço excluídas.

![Métrica de total de perfis pontuados na IA do cliente.](../images/user-guide/total-profiles.png)

As instâncias de serviço podem ser editadas, clonadas e excluídas usando os controles no lado direito da interface. Para exibir esses controles, selecione uma instância de suas **[!UICONTROL Instâncias de serviço]** existentes. Os controles contêm o seguinte:

- **[!UICONTROL Editar]**: selecionar **[!UICONTROL Editar]** permite modificar uma instância de serviço existente. É possível editar o nome, a descrição e a frequência de pontuação da instância.
- **[!UICONTROL Clonar]**: selecionar **[!UICONTROL Clonar]** copia a configuração da instância de serviço selecionada no momento. Em seguida, você pode modificar o fluxo de trabalho para fazer pequenos ajustes e renomeá-lo como uma nova instância.
- **[!UICONTROL Excluir]**: é possível excluir uma instância de serviço, incluindo todas as execuções históricas. O conjunto de dados de saída correspondente será excluído do Experience Platform. No entanto, as pontuações que foram sincronizadas com o Perfil do cliente em tempo real não são excluídas.
- **[!UICONTROL Fonte de dados]**: um link para o conjunto de dados usado por esta instância. Se vários conjuntos de dados estiverem sendo usados, selecionar o texto do hiperlink abrirá o popover de visualização do conjunto de dados.
- **[!UICONTROL Detalhes da última execução]**: exibido somente quando uma execução falha. As informações sobre por que a execução falhou, como códigos de erro, são exibidas aqui.
- **[!UICONTROL Definição de pontuação]**: uma visão geral rápida da meta que você configurou para esta instância.

![Painel de instâncias de serviço na IA do cliente.](../images/user-guide/service-instance-panel.png)

Para criar uma nova instância, selecione **[!UICONTROL Criar instância]**.

![Painel da IA do cliente mostrando uma visão geral das instâncias de serviço e seus status.](../images/user-guide/dashboard.png)

## Configuração

O fluxo de trabalho de criação da instância é exibido, iniciando na etapa **[!UICONTROL Configurar]**.

Abaixo estão informações importantes sobre valores que você deve fornecer à instância com:

-**[!UICONTROL Nome]:** o nome da instância é usado em todos os locais onde as pontuações da IA do Cliente são exibidas. Portanto, os nomes devem descrever o que as pontuações de previsão representam. Por exemplo, &quot;Probabilidade de cancelamento da assinatura de uma revista&quot;.

-**[!UICONTROL Descrição]:** Uma descrição indicando o que você está tentando prever.

-**[!UICONTROL Tipo de propensão]:** O tipo de propensão determina a intenção da pontuação e a polaridade da métrica. Você pode escolher **[!UICONTROL Churn]** ou **[!UICONTROL Conversão]**. Consulte a observação em [resumo de pontuação](./discover-insights.md#scoring-summary) no documento de descoberta de insights para obter mais informações sobre como o tipo de propensão afeta sua instância.

![Tela de Instalação mostrando o fluxo de trabalho de criação de instância na IA do Cliente.](../images/user-guide/create-instance.png)

Forneça os valores necessários e selecione **[!UICONTROL Avançar]** para continuar.

## Selecionar dados {#select-data}

Por design, a IA do cliente usa Adobe Analytics, Adobe Audience Manager, Eventos de experiência em geral e dados de Eventos de experiência do consumidor para calcular as pontuações de propensão. Ao selecionar um conjunto de dados, somente os compatíveis com a IA do cliente são listados. Para selecionar um conjunto de dados, selecione o símbolo (**+**) ao lado do nome do conjunto de dados ou marque a caixa de seleção para adicionar vários conjuntos de dados de uma vez. Use a opção de pesquisa para encontrar rapidamente os conjuntos de dados em que você está interessado.

![Tela de seleção do conjunto de dados mostrando a barra de pesquisa e as opções de salvar realçadas.](../images/user-guide/configure-dataset-page-save-and-exit-cai.png)

Depois de selecionar os conjuntos de dados que deseja usar, clique no botão **[!UICONTROL Adicionar]** para adicionar os conjuntos de dados ao painel de visualização do conjunto de dados.

![Tela de seleção do conjunto de dados mostrando os conjuntos de dados selecionados no painel de visualização.](../images/user-guide/select-datasets.png)

Selecionar o ícone de informações ![ícone de informações](/help/images/icons/info.png) ao lado do conjunto de dados abre o popover de visualização do conjunto de dados.

![Tela de seleção do conjunto de dados mostrando a barra de pesquisa e as informações do conjunto de dados.](../images/user-guide/dataset-info.png)

A visualização do conjunto de dados contém dados como o tempo da última atualização, o esquema de origem e uma visualização das primeiras dez colunas.

Selecione **[!UICONTROL Salvar]** para salvar os rascunhos à medida que você avança no fluxo de trabalho. Você também pode salvar configurações de modelo de rascunho e ir para a próxima etapa do fluxo de trabalho. Use **[!UICONTROL Salvar e continuar]** para criar e salvar rascunhos durante as configurações do modelo. O recurso permite criar e salvar rascunhos da configuração do modelo e é particularmente útil quando é necessário definir muitos campos no fluxo de trabalho de configuração.

![A guia Criar fluxo de trabalho da IA do cliente do Data Science Services com Salvar e Salvar e continue realçada.](../images/user-guide/cai-save-and-exit.png)

### Integridade do conjunto de dados {#dataset-completeness}

Há um valor percentual de integridade do conjunto de dados na visualização do conjunto de dados. Esse valor fornece um instantâneo rápido de quantas colunas em seu conjunto de dados estão vazias/nulas. Se um conjunto de dados contiver muitos valores ausentes e esses valores forem capturados em outro lugar, é altamente recomendável incluir o conjunto de dados que contém os valores ausentes. Neste exemplo, a ID de pessoa está vazia, no entanto, a ID de pessoa é capturada em um conjunto de dados separado que pode ser incluído.

>[!NOTE]
>
>A integridade do conjunto de dados é calculada usando a janela máxima de treinamento para a IA do cliente (um ano). Isso significa que os dados com mais de um ano não são considerados ao exibir o valor de integridade do conjunto de dados.

![Integridade do conjunto de dados mostrando uma visualização do conjunto de dados com porcentagem de integridade destacada.](../images/user-guide/dataset-info-2.png)

### Selecionar uma identidade {#identity}

Agora é possível unir vários conjuntos de dados uns aos outros com base no mapa de identidade (campo). Você deve selecionar um tipo de identidade (também conhecido como &quot;namespace de identidade&quot;) e um valor de identidade dentro desse namespace. Se você tiver atribuído mais de um campo como uma identidade no esquema no mesmo namespace, todos os valores de identidade atribuídos aparecerão na lista suspensa de identidades anexada ao namespace, como `EMAIL (personalEmail.address)` ou `EMAIL (workEmail.address)`.

![Tela de seleção do mapa de identidade mostrando o mesmo namespace sendo selecionado para vários conjuntos de dados.](../images/user-guide/cai-identity-map.png)

>[!IMPORTANT]
>
>O mesmo tipo de identidade (namespace) deve ser usado para cada conjunto de dados selecionado. Uma marca de seleção verde é exibida ao lado do tipo de identidade na coluna identidade, indicando que os conjuntos de dados são compatíveis. Por exemplo, ao usar o namespace Telefone e `mobilePhone.number` como o identificador, todos os identificadores para os conjuntos de dados restantes devem conter e usar o namespace Telefone.

Para selecionar uma identidade, selecione o valor sublinhado localizado na coluna de identidade. O popover Selecionar uma identidade é exibido.

![Tela de seleção do mapa de identidade mostrando o mesmo namespace sendo selecionado para vários conjuntos de dados.](../images/user-guide/cai-identity-namespace.png)

Caso haja mais de uma identidade disponível em um namespace, selecione o campo de identidade correto para seu caso de uso. Por exemplo, duas identidades de email estão disponíveis no namespace de email: um email comercial e pessoal. Dependendo do caso de uso, um email pessoal tem mais probabilidade de ser preenchido e ser mais útil em previsões individuais. Isso significa que `EMAIL (personalEmail.address)` seria selecionado como a identidade.

![Um exemplo mostrando uma chave de conjunto de dados não selecionada na tela de seleção do mapa de identidade.](../images/user-guide/select-identity.png)

>[!NOTE]
>
> Se não existir um tipo de identidade (namespace) válido para um conjunto de dados, você deve definir uma identidade primária e atribuí-la a um namespace de identidade usando o [editor de esquemas](../../../xdm/schema/composition.md#identity). Para saber mais sobre namespaces e identidades, visite a documentação dos [namespaces do Serviço de Identidade](../../../identity-service/features/namespaces.md).

## Definir meta {#define-a-goal}

A etapa **[!UICONTROL Definir meta]** é exibida e fornece um ambiente interativo para que você defina visualmente uma meta de previsão. Uma meta é composta por um ou mais eventos, em que a ocorrência de cada evento é baseada na condição que mantém. O objetivo de uma instância da IA do cliente é determinar a probabilidade de atingir sua meta em um determinado período de tempo.

Para criar uma meta, selecione **[!UICONTROL Inserir Nome do Campo]** e, em seguida, um campo da lista suspensa. Selecione a segunda entrada, uma cláusula para a condição do evento e, opcionalmente, forneça o valor de destino para concluir o evento. Eventos adicionais podem ser configurados selecionando **[!UICONTROL Adicionar evento]**. Por fim, complete a meta aplicando um período de tempo de previsão em número de dias e selecione **[!UICONTROL Próximo]**.

![Defina a etapa da meta na IA do cliente mostrando o ambiente interativo para definir uma meta de previsão.](../images/user-guide/cai-define-a-goal.png)

### Ocorrerá e não ocorrerá

Ao definir sua meta, você tem a opção de selecionar **[!UICONTROL Ocorrerá]** ou **[!UICONTROL Não ocorrerá]**. Selecionar **[!UICONTROL Ocorrerá]** significa que as condições do evento definidas precisam ser atendidas para que os dados do evento de um cliente sejam incluídos na interface do usuário de insights.

Por exemplo, se você deseja configurar um aplicativo para prever se um cliente fará uma compra, você pode selecionar **[!UICONTROL Ocorrerá]** seguido de **[!UICONTROL Todos de]** e inserir **commerce.purchases.id** (ou um campo semelhante) e **[!UICONTROL existe]** como operador.

<!-- ![will occur](../images/user-guide/occur.png) -->
![Um exemplo mostrando a configuração de uma meta em que um evento ocorrerá.](../images/user-guide/cai-will-occur.png)

No entanto, pode haver casos em que você esteja interessado em prever se algum evento não ocorrerá em um determinado período. Para configurar uma meta com esta opção, selecione **[!UICONTROL Não ocorrerá]** na lista suspensa de nível superior.

Por exemplo, se você estiver interessado em prever quais clientes se tornam menos engajados e não visitar a página de logon da conta no mês seguinte. Selecione **[!UICONTROL Não ocorrerá]** seguido por **[!UICONTROL Todos de]** e insira **web.webInteraction.URL** (ou um campo semelhante) e **[!UICONTROL é igual]** como o operador com **account-login** como o valor.

![Um exemplo mostrando a configuração de uma meta em que um evento não ocorrerá.](../images/user-guide/not-occur.png)

### Todos os e qualquer um de

Em alguns casos, você pode querer prever se uma combinação de eventos ocorrerá e, em outros casos, pode querer prever a ocorrência de qualquer evento de um conjunto predefinido. Para prever se um cliente terá uma combinação de eventos, selecione a opção **[!UICONTROL Todos os]** na lista suspensa de segundo nível na página **[!UICONTROL Definir meta]**.

Por exemplo, você pode querer prever se um cliente compra um produto específico. Esta meta de previsão é definida por duas condições: a `commerce.order.purchaseID` **existe** e a `productListItems.SKU` **é igual** a algum valor específico.

![Um exemplo mostrando a configuração de uma meta em que todas as condições devem ser atendidas.](../images/user-guide/all-of.png)

Para prever se um cliente terá algum evento de um determinado conjunto, você pode usar a opção **[!UICONTROL Qualquer um de]**.

Por exemplo, você pode querer prever se um cliente visita um determinado URL ou uma página da Web com um nome específico. Esta meta de previsão é definida por duas condições: `web.webPageDetails.URL` **começa com** um determinado valor e `web.webPageDetails.name` **começa com** um determinado valor.

![Um exemplo mostrando a configuração de uma meta em que qualquer condição pode ser atendida.](../images/user-guide/any-of.png)

### População qualificada *(opcional)*

Por padrão, as pontuações de propensão são geradas para todos os perfis, a menos que uma população qualificada seja especificada. Você pode especificar uma população elegível definindo condições para incluir ou excluir perfis com base em eventos.

![Um exemplo mostrando a configuração de uma população qualificada na IA do cliente.](../images/user-guide/eligible-population.png)

### Eventos personalizados (*opcional*) {#custom-events}

Se você tiver informações adicionais além dos [campos de evento padrão](../data-requirements.md#standard-events) usados pela IA do cliente para gerar pontuações de propensão, uma opção de eventos personalizados será fornecida. Usar essa opção permite adicionar outros eventos que você considera influentes, o que pode melhorar a qualidade do seu modelo e ajudar a fornecer resultados mais precisos. Se o conjunto de dados selecionado incluir eventos personalizados definidos no esquema, você poderá adicioná-los à sua instância.

>[!NOTE]
>
> Para obter uma explicação detalhada sobre como os eventos personalizados afetam os resultados de pontuação da IA do cliente, visite a seção [Exemplo de evento personalizado](#custom-event).

![Um exemplo mostrando a configuração de um recurso de evento na IA do cliente.](../images/user-guide/event-feature.png)

Para adicionar um evento personalizado, selecione **[!UICONTROL Adicionar evento personalizado]**. Em seguida, insira um nome de evento personalizado e mapeie-o para o campo de evento no esquema. Os nomes de eventos personalizados são exibidos no lugar do valor dos campos ao observar fatores influentes e outros insights. Isso significa que o nome do evento personalizado será usado em vez da ID/valor do evento. Para obter mais informações sobre como os eventos personalizados são exibidos, consulte a [seção de exemplo de evento personalizado](#custom-event). Esses eventos personalizados adicionais são usados pela IA do cliente para melhorar a qualidade do seu modelo e fornecer resultados mais precisos.

![Um exemplo mostrando a configuração de um campo de evento personalizado na IA do cliente.](../images/user-guide/custom-event.png)

Em seguida, selecione o operador que deseja usar no menu suspenso de operadores disponíveis. Somente os operadores compatíveis com o evento são listados.

![Um exemplo mostrando os operadores disponíveis para configurar um evento personalizado na IA do cliente.](../images/user-guide/custom-operator.png)

Por fim, insira os valores do campo se o operador selecionado exigir um. Neste exemplo, só precisamos ver se existe uma reserva de hotel ou restaurante. No entanto, se quisermos ser mais exatos, podemos usar o operador equals e inserir um valor exato no prompt de valor.

![Um exemplo mostrando a configuração de um valor de campo de evento personalizado na IA do cliente.](../images/user-guide/custom-value.png)

Depois de concluído, selecione **[!UICONTROL Próximo]** no canto superior direito para continuar.

### Atributos de perfil personalizados (*opcional*)

Você pode definir campos importantes do conjunto de dados do Perfil (com carimbos de data e hora) em seus dados, além dos [campos de evento padrão](../data-requirements.md#standard-events) usados pela IA do cliente para gerar pontuações de propensão. Usar essa opção permite adicionar outros atributos de perfil que você considera influentes, o que pode melhorar a qualidade do seu modelo e fornecer resultados mais precisos. Além disso, adicionar atributos de perfil personalizados permite que a IA do cliente mostre melhor como perfis específicos terminaram em um intervalo de propensão.

>[!NOTE]
>
>A adição de um atributo de perfil personalizado segue o mesmo fluxo de trabalho que a adição de um evento personalizado. Semelhante aos eventos personalizados, os atributos de perfil personalizados afetam a pontuação do modelo da mesma forma. Para uma explicação detalhada, visite a seção [Exemplo de evento personalizado](#custom-event).

![Um exemplo mostrando a configuração de um atributo de perfil personalizado na IA do cliente.](../images/user-guide/profile-attributes.png)

#### Selecione atributos de perfil na exportação de instantâneos do perfil

Você também pode optar por incluir atributos de perfil na exportação diária do instantâneo do Perfil. Esses atributos são sincronizados com a exportação de instantâneos do Perfil e exibem o valor disponível mais recentemente. Eles são exibidos automaticamente e não exigem que um conjunto de dados seja selecionado na etapa de configuração.

>[!WARNING]
>
> Não selecione um atributo de perfil que tenha sido atualizado como resultado da meta de previsão ou que esteja altamente correlacionado a ela. Isso resulta em vazamento de dados e ajuste excessivo do modelo. Por exemplo, `total_purchases_in_the_last_3_months` é um atributo que prevê a conversão de compra.

### Adicionar um exemplo de evento personalizado {#custom-event}

No exemplo a seguir, um evento personalizado e um atributo de perfil são adicionados a uma instância da IA do cliente. O objetivo da instância da IA do cliente é prever a probabilidade de um cliente comprar outro produto da Luma nos próximos 60 dias. Normalmente, os dados do produto são vinculados a uma SKU do produto. Nesse caso, o SKU é `prd1013`. Depois que o modelo de IA do cliente é treinado/pontuado, esse SKU pode ser vinculado a um evento e exibido como um fator influente para um intervalo de propensão.

A IA do cliente aplica automaticamente a geração de recursos como &quot;Dias desde&quot; ou &quot;Contagens de&quot; em relação a eventos personalizados como **Assistir à compra**. Se esse evento foi considerado um fator influente no motivo pelo qual os clientes têm alta, média ou baixa propensão, a IA do cliente o exibe como `Days since prd1013 purchase` ou `Count of prd1013 purchase`. Ao criar esse evento como um evento personalizado, você pode dar ao evento um novo nome, tornando os resultados muito mais fáceis de ler. Por exemplo, `Days since Watch purchase`. Além disso, a IA do cliente usa esse evento em seu treinamento e pontuação, mesmo que o evento não seja um evento padrão. Isso significa que é possível adicionar vários eventos que você acha que podem ser influentes e personalizar ainda mais seu modelo, incluindo dados como reservas, registros de visitantes e outros eventos. Adicionar esses pontos de dados aumenta ainda mais a precisão do modelo de IA do cliente.

![Um exemplo mostrando a configuração de um evento personalizado com um nome definido pelo usuário na IA do cliente.](../images/user-guide/custom-event-name.png)

## Definir opções

A etapa Definir opções permite configurar um agendamento para automatizar execuções de previsão, definir exclusões de previsão para filtrar determinados eventos e ativar/desativar **[!UICONTROL Perfil]**.

### Configurar um agendamento *(opcional)* {#configure-a-schedule}

Para definir um agendamento de pontuação, comece configurando a **[!UICONTROL Frequência de Pontuação]**. As execuções de previsão automatizadas podem ser programadas para serem executadas semanal ou mensalmente.

![Um exemplo mostrando as opções de configuração de agendamento de pontuação na IA do cliente.](../images/user-guide/schedule.png)

### Exclusões de previsão *(opcional)*

Se o conjunto de dados continha colunas adicionadas como dados de teste, é possível adicionar essa coluna ou evento a uma lista de exclusão selecionando **[!UICONTROL Adicionar exclusão]** e, em seguida, inserindo o campo que deseja excluir. Isso impede que os eventos que atendem a determinadas condições sejam avaliados ao gerar pontuações. Esse recurso pode ser usado para filtrar entradas ou promoções de dados irrelevantes.

Para excluir um evento, selecione **[!UICONTROL Adicionar exclusão]** e defina o evento. Para remover uma exclusão, selecione as reticências (**[!UICONTROL ...]**) no canto superior direito do contêiner de evento e selecione **[!UICONTROL Remover Contêiner]**.

![Um exemplo mostrando a configuração das exclusões de previsão na IA do cliente.](../images/user-guide/exclusion.png)

### Alternar perfil

A opção de Perfil permite que a IA do cliente exporte os resultados da pontuação para o Perfil do cliente em tempo real. Desativar essa alternância impede que os resultados da pontuação dos modelos sejam adicionados ao Perfil. Os resultados da pontuação da IA do cliente ainda estão disponíveis com esse recurso desativado.

Ao usar a IA do cliente pela primeira vez, é possível desativar esse recurso até que você esteja satisfeito com os resultados de saída do modelo. Isso impede que você faça upload de vários conjuntos de dados de pontuação para seus Perfis de cliente enquanto ajusta o modelo. Após concluir a calibração do modelo, você pode cloná-lo usando a [opção de clonagem](#set-up-your-instance) da página **Instâncias de serviço**. Isso permite criar uma cópia do modelo e alternar o perfil no.

![Um exemplo mostrando a opção de alternância Perfil no fluxo de trabalho avançado da IA do cliente.](../images/user-guide/advanced-workflow-save.png)

Depois de definir seu cronograma de pontuação, incluir exclusões de previsão e alternar o perfil para onde você deseja que esteja, selecione **[!UICONTROL Concluir]** no canto superior direito para criar sua instância da IA do cliente.

Se a instância for criada com sucesso, uma execução de previsão será acionada imediatamente e as execuções subsequentes serão executadas de acordo com o agendamento definido.

>[!NOTE]
>
>Dependendo do tamanho dos dados de entrada, as execuções de previsão podem levar até 24 horas para serem concluídas.

Ao seguir esta seção, você configurou uma instância da IA do cliente e executou uma execução de previsão. Após a conclusão bem-sucedida da execução, os insights pontuados preenchem automaticamente os perfis com pontuações previstas se a alternância do perfil estiver habilitada. Aguarde até 24 horas antes de prosseguir para a próxima seção deste tutorial.

## Próximas etapas {#next-steps}

Ao seguir este tutorial, você configurou com êxito uma instância da IA do cliente e gerou pontuações de propensão. Agora você pode optar por usar o Construtor de segmentos para [criar segmentos de clientes com pontuações previstas](./create-segment.md) ou [descobrir insights com a IA do cliente](./discover-insights.md).

## Recursos adicionais

O vídeo a seguir foi projetado para oferecer suporte à sua compreensão do fluxo de trabalho de configuração da IA do cliente. Além disso, são fornecidas práticas recomendadas e exemplos de casos de uso.

>[!IMPORTANT]
>
> O vídeo a seguir está desatualizado. Para obter as informações mais atualizadas, consulte a documentação.

>[!VIDEO](https://video.tv.adobe.com/v/36603?learn=on&quality=12&captions=por_br)
