---
keywords: Experience Platform;user guide;customer ai;popular topics;configure instance;create instance;
solution: Experience Platform
title: Configuração de uma instância do AI do cliente
topic: Instance creation
description: Os Serviços inteligentes fornecem IA do cliente como um serviço Adobe Sensei simples de usar que pode ser configurado para diferentes casos de uso. As seções a seguir fornecem etapas para configurar uma instância da API do cliente.
translation-type: tm+mt
source-git-commit: 0b92346065b7c9615d8aef4c9b13c84e0383b4b9
workflow-type: tm+mt
source-wordcount: '1284'
ht-degree: 0%

---


# Configuração de uma instância do AI do cliente

A IA do cliente, como parte dos Serviços inteligentes, permite que você gere pontuações de propensão personalizadas sem precisar se preocupar com o aprendizado da máquina.

Os Serviços inteligentes fornecem IA do cliente como um serviço Adobe Sensei simples de usar que pode ser configurado para diferentes casos de uso. As seções a seguir fornecem etapas para configurar uma instância da API do cliente.

## Configurar sua instância {#set-up-your-instance}

Na interface do usuário da plataforma, selecione **[!UICONTROL Serviços]** na navegação à esquerda. O navegador **[!UICONTROL Serviços]** é exibido e exibe todos os serviços disponíveis à sua disposição. No container para API do cliente, selecione **[!UICONTROL Abrir]**.

![](../images/user-guide/navigate-to-service.png)

A interface do usuário da IA **do** cliente é exibida e exibe todas as suas instâncias de serviço.

- Você pode encontrar a métrica **[!UICONTROL Total de perfis pontuados]** localizada no lado inferior direito do container de instância **** Criar. Essa métrica rastreia o número total de perfis pontuados pela AI do cliente para o ano civil atual, incluindo todos os ambientes da caixa de proteção e quaisquer instâncias de serviço excluídas.

![](../images/user-guide/total-profiles.png)

As instâncias de serviço podem ser editadas, clonadas e excluídas usando os controles no lado direito da interface. Para exibir esses controles, selecione uma instância de suas instâncias **[!UICONTROL de]** Serviço existentes. Os controles contêm o seguinte:

- **[!UICONTROL Editar]**: Selecionar **[!UICONTROL Editar]** permite modificar uma instância de serviço existente. Você pode editar o nome, a descrição e a frequência de pontuação da instância.
- **[!UICONTROL Clonar]**: Selecionar **[!UICONTROL Clonar]** copia a configuração da instância de serviço atualmente selecionada. Em seguida, você pode modificar o fluxo de trabalho para fazer ajustes secundários e renomeá-lo como uma nova instância.
- **[!UICONTROL Excluir]**: Você pode excluir uma instância de serviço, incluindo quaisquer execuções históricas.
- **[!UICONTROL Fonte]** de dados: Um link para o conjunto de dados usado por esta instância.
- **[!UICONTROL Detalhes]** da última execução: Isso só é exibido quando uma execução falha. Informações sobre por que a execução falhou, como códigos de erro, são exibidas aqui.
- **[!UICONTROL Definição]** da pontuação: Uma visão geral rápida da meta configurada para esta instância.

![](../images/user-guide/service-instance-panel.png)

Para criar uma nova instância, selecione **[!UICONTROL Criar instância]**.

![](../images/user-guide/dashboard.png)

O fluxo de trabalho de criação da instância é exibido, começando na etapa **[!UICONTROL Configuração]** .

Abaixo estão informações importantes sobre valores que devem ser fornecidos à instância com:

- O nome da instância é usado em todos os locais onde as pontuações da AI do cliente são exibidas. Assim, os nomes devem descrever o que as pontuações de previsão representam, por exemplo, &quot;Probabilidade de cancelar a subscrição de revistas&quot;.

- O tipo de propensão determina a intenção da pontuação e da polaridade da métrica. Você pode escolher **[!UICONTROL Churn]** ou **[!UICONTROL Conversion]**. Consulte a nota em [um resumo](./discover-insights.md#scoring-summary) de pontuação no documento de insights de descoberta para obter mais informações sobre como o tipo de propensão afeta sua instância.

- A fonte de dados é o local onde os dados estão localizados. Conjunto de dados é o conjunto de dados de entrada usado para prever pontuações. Por padrão, a IA do cliente usa os dados do Evento da experiência do consumidor para calcular as pontuações de propensão. Ao selecionar um conjunto de dados no seletor suspenso, somente os que são compatíveis com a IA do cliente são listados.

- Por padrão, as pontuações de propensão são geradas para todos os perfis, a menos que uma população qualificada seja especificada. Você pode especificar uma população qualificada definindo condições para incluir ou excluir perfis com base em eventos.

Forneça os valores necessários e selecione **[!UICONTROL Avançar]**.

![](../images/user-guide/setup.png)

### Definir uma meta {#define-a-goal}

A etapa **[!UICONTROL Definir meta]** é exibida e fornece um ambiente interativo para que você defina visualmente uma meta de previsão. Uma meta é composta de um ou mais eventos, nos quais cada ocorrência de evento é baseada na condição que contém. O objetivo de uma instância da API do cliente é determinar a probabilidade de atingir sua meta dentro de um determinado intervalo de tempo.

Para criar uma meta, selecione **[!UICONTROL Inserir nome]** do campo e selecione um campo na lista suspensa. Selecione a segunda entrada e selecione uma cláusula para a condição do evento, em seguida, forneça o valor do público alvo para concluir o evento. Eventos adicionais podem ser configurados selecionando **[!UICONTROL Adicionar evento]**. Por fim, conclua a meta aplicando um período de previsão em número de dias e selecione **[!UICONTROL Próximo]**.

![](../images/user-guide/goal.png)

#### Ocorrerá e não ocorrerá

Ao definir sua meta, você tem a opção de selecionar **[!UICONTROL Ocorrerá]** ou não **[!UICONTROL Ocorrerá]**. Selecionar **[!UICONTROL Ocorrerá]** significa que as condições do evento definidas precisam ser atendidas para que os dados do evento de um cliente sejam incluídos na interface do usuário do insights.

Por exemplo, se você deseja configurar um aplicativo para prever se um cliente fará uma compra, selecione **[!UICONTROL Ocorrerá]** seguido de **[!UICONTROL Todos]** e, em seguida, insira **commerce.purch.id** e **existe** como operador.

![ocorrerá](../images/user-guide/occur.png)

No entanto, pode haver casos em que você esteja interessado em prever se algum evento não ocorrerá em um determinado período de tempo. Para configurar uma meta com essa opção, selecione **[!UICONTROL Não ocorrerá]** na lista suspensa de nível superior.

Por exemplo, se você estiver interessado em prever quais clientes ficam menos envolvidos e não visitam sua página de logon de conta no próximo mês. Selecione **[!UICONTROL Não ocorrerá]** seguido de **[!UICONTROL Todos]** e digite **web.webInteraction.URL** e **[!UICONTROL é igual]** ao operador com login **de** conta como o valor.

![não ocorrerá](../images/user-guide/not-occur.png)

#### Todos e qualquer um de

Em alguns casos, talvez você queira prever se uma combinação de eventos ocorrerá e, em outros casos, talvez você queira prever a ocorrência de qualquer evento a partir de um conjunto predefinido. Para prever se um cliente terá uma combinação de eventos, selecione a opção **[!UICONTROL Todos]** na lista suspensa de segundo nível na página **[!UICONTROL Definir meta]** .

Por exemplo, você pode querer prever se um cliente compra um produto específico. Esta meta de previsão é definida por duas condições: um `commerce.order.purchaseID` existe **e o valor** é `productListItems.SKU` igual **** a algum valor específico.

![Todos os exemplos](../images/user-guide/all-of.png)

Para prever se um cliente terá algum evento de um determinado conjunto, você pode usar a opção **[!UICONTROL Qualquer um dos]** .

Por exemplo, você pode desejar prever se um cliente visita um determinado URL ou uma página da Web com um nome específico. Esta meta de previsão é definida por duas condições: `web.webPageDetails.URL` **start com** um valor específico e `web.webPageDetails.name` start com **** um valor específico.

![Qualquer exemplo](../images/user-guide/any-of.png)

### Configurar um agendamento *(opcional)* {#configure-a-schedule}

A etapa **[!UICONTROL Avançado]** é exibida. Esta etapa opcional permite configurar uma programação para automatizar execuções de previsão, definir exclusões de previsão para filtrar determinados eventos ou selecionar **[!UICONTROL Concluir]** se nada for necessário.

Configure um agendamento de pontuação configurando a Frequência **[!UICONTROL de]** Pontuação. As execuções de previsão automatizadas podem ser programadas para serem executadas semanalmente ou mensalmente.

![](../images/user-guide/schedule.png)

Abaixo da configuração da programação, você pode definir exclusões de previsão para impedir que eventos que atendem a determinadas condições sejam avaliados ao gerar pontuações. Este recurso pode ser usado para filtrar entradas de dados irrelevantes.

Para excluir determinados eventos, selecione **[!UICONTROL Adicionar exclusão]** e defina o evento da mesma forma que a meta é definida. Para remover uma exclusão, selecione as elipses (**[!UICONTROL ...]**) na parte superior direita do container do evento e selecione **[!UICONTROL Remover Container]**.

![](../images/user-guide/exclusion.png)

Exclua eventos conforme necessário e selecione **[!UICONTROL Concluir]** para criar a instância.

![](../images/user-guide/advanced.png)

Se a instância for criada com êxito, uma execução de previsão será acionada imediatamente e as execuções subsequentes serão executadas de acordo com a programação definida.

>[!NOTE]
>
>Dependendo do tamanho dos dados de entrada, as execuções de previsão podem levar até 24 horas para serem concluídas.

Ao seguir esta seção, você configurou uma instância do AI do cliente e uma execução de previsão foi executada. Após a conclusão bem-sucedida da execução, insights pontuados preenchem automaticamente perfis com pontuações previstas. Aguarde até 24 horas antes de continuar com a próxima seção deste tutorial.

## Próximas etapas {#next-steps}

Ao seguir este tutorial, você configurou com êxito uma instância da IA do cliente e gerou pontuações de propensão. Agora você pode optar por usar o Construtor de segmentos para [criar segmentos de clientes com pontuações](./create-segment.md) previstas ou [descobrir insights com a IA](./discover-insights.md)do cliente.

## Recursos adicionais

O vídeo a seguir foi projetado para oferecer suporte à sua compreensão do fluxo de trabalho de configuração para a API do cliente. Além disso, as práticas recomendadas e exemplos de casos de uso são fornecidos.

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)

