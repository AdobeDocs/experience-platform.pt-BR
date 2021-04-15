---
keywords: Experience Platform, guia do usuário, atendimento ao cliente, tópicos populares, configurar instância, criar instância;
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Configurar uma instância do Customer AI
topic: Criação da instância
description: Os Serviços inteligentes fornecem a API do cliente como um serviço de Adobe Sensei simples de usar que pode ser configurado para diferentes casos de uso. As seções a seguir fornecem etapas para configurar uma instância do Customer AI.
exl-id: 78353dab-ccb5-4692-81f6-3fb3f6eca886
translation-type: tm+mt
source-git-commit: 2ef2a6431865e8ffdc2abd6cf527249e8b5ca4d0
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 0%

---

# Configurar uma instância do Customer AI

O Customer AI, como parte dos Serviços inteligentes, permite gerar pontuações de propensão personalizadas sem se preocupar com o aprendizado de máquina.

Os Serviços inteligentes fornecem a API do cliente como um serviço de Adobe Sensei simples de usar que pode ser configurado para diferentes casos de uso. As seções a seguir fornecem etapas para configurar uma instância do Customer AI.

## Configure sua instância {#set-up-your-instance}

Na interface do usuário da plataforma, selecione **[!UICONTROL Services]** no painel de navegação esquerdo. O navegador **[!UICONTROL Services]** é exibido e exibe todos os serviços disponíveis à sua disposição. No contêiner do Customer AI, selecione **[!UICONTROL Open]**.

![](../images/user-guide/navigate-to-service.png)

A interface do usuário **Customer AI** é exibida e exibe todas as instâncias de serviço.

- Você pode encontrar a métrica **[!UICONTROL Total profiles scored]** localizada no lado inferior direito do contêiner **[!UICONTROL Create instance]**. Essa métrica rastreia o número total de perfis pontuados pelo Customer AI para o ano civil atual, incluindo todos os ambientes sandbox e quaisquer instâncias de serviço excluídas.

![](../images/user-guide/total-profiles.png)

As instâncias de serviço podem ser editadas, clonadas e excluídas usando os controles no lado direito da interface do usuário. Para exibir esses controles, selecione uma instância de seu **[!UICONTROL Service instances]** existente. Os controles contêm o seguinte:

- **[!UICONTROL Edit]**: Selecionar  **[!UICONTROL Edit]** permite modificar uma instância de serviço existente. É possível editar o nome, a descrição e a frequência de pontuação da instância.
- **[!UICONTROL Clone]**: A seleção  **[!UICONTROL Clone]** copia a configuração da instância de serviço atualmente selecionada. Em seguida, você pode modificar o workflow para fazer pequenos ajustes e renomeá-lo como uma nova instância.
- **[!UICONTROL Delete]**: Você pode excluir uma instância de serviço, incluindo quaisquer execuções históricas.
- **[!UICONTROL Data source]**: Um link para o conjunto de dados usado por esta instância.
- **[!UICONTROL Last run details]**: Isso só é exibido quando uma execução falha. Informações sobre por que a execução falhou, como códigos de erro, são exibidas aqui.
- **[!UICONTROL Score definition]**: Uma visão geral rápida da meta que você configurou para esta instância.

![](../images/user-guide/service-instance-panel.png)

Para criar uma nova instância, selecione **[!UICONTROL Create instance]**.

![](../images/user-guide/dashboard.png)

O fluxo de trabalho de criação da instância é exibido, começando na etapa **[!UICONTROL Setup]**.

Abaixo estão informações importantes sobre valores que você deve fornecer à instância com:

- O nome da instância é usado em todos os lugares onde as pontuações do Customer AI são exibidas. Assim, os nomes devem descrever o que as pontuações de previsão representam, por exemplo, &quot;Probabilidade de cancelar a assinatura de uma revista&quot;.

- O tipo de propensão determina a intenção da pontuação e da polaridade da métrica. Você pode escolher **[!UICONTROL Churn]** ou **[!UICONTROL Conversion]**. Consulte a nota em [resumo de pontuação](./discover-insights.md#scoring-summary) no documento de insights de descoberta para obter mais informações sobre como o tipo de propensão afeta sua instância.

- A fonte de dados é onde os dados estão localizados. Conjunto de dados é o conjunto de dados de entrada usado para prever pontuações. Por design, o Customer AI usa os dados do Evento de experiência do consumidor, do Adobe Analytics e do Adobe Audience Manager para calcular as pontuações de propensão. Ao selecionar um conjunto de dados no seletor suspenso, somente aqueles que são compatíveis com a API do cliente serão listados.

- Por padrão, as pontuações de propensão são geradas para todos os perfis, a menos que uma população qualificada seja especificada. Você pode especificar uma população elegível definindo condições para incluir ou excluir perfis com base em eventos.

Forneça os valores necessários e selecione **[!UICONTROL Next]**.

![](../images/user-guide/setup.png)

### Definir uma meta {#define-a-goal}

A etapa **[!UICONTROL Define goal]** é exibida e fornece um ambiente interativo para que você defina visualmente uma meta de previsão. Um objetivo é composto por um ou mais eventos, em que a ocorrência de cada evento se baseia na condição que ele contém. O objetivo de uma instância do Customer AI é determinar a probabilidade de atingir sua meta em um determinado período.

Para criar uma meta, selecione **[!UICONTROL Enter Field Name]** e selecione um campo na lista suspensa. Selecione a segunda entrada e selecione uma cláusula para a condição do evento, em seguida, forneça o valor de destino para concluir o evento. Eventos adicionais podem ser configurados selecionando **[!UICONTROL Add event]**. Por fim, complete a meta aplicando um período de previsão em número de dias e selecione **[!UICONTROL Next]**.

![](../images/user-guide/goal.png)

#### Ocorrerá e não ocorrerá

Ao definir sua meta, você tem a opção de selecionar **[!UICONTROL Will occur]** ou **[!UICONTROL Will not occur]**. Selecionar **[!UICONTROL Will occur]** significa que as condições do evento definidas precisam ser atendidas para que os dados do evento de um cliente sejam incluídos na interface do usuário do insights.

Por exemplo, se você quiser configurar um aplicativo para prever se um cliente fará uma compra, poderá selecionar **[!UICONTROL Will occur]** seguido por **[!UICONTROL All of]** e inserir **commerce.purchase.id** e **exists** como operador.

![ocorrerá](../images/user-guide/occur.png)

No entanto, pode haver casos em que você esteja interessado em prever se algum evento não acontecerá em um determinado período. Para configurar uma meta com essa opção, selecione **[!UICONTROL Will not occur]** na lista suspensa de nível superior.

Por exemplo, se você estiver interessado em prever quais clientes se tornam menos envolvidos e não visitar sua página de logon de conta no próximo mês. Selecione **[!UICONTROL Will not occur]** seguido por **[!UICONTROL All of]** e insira **web.webInteraction.URL** e **[!UICONTROL equals]** como operador com **account-login** como o valor.

![não ocorrerá](../images/user-guide/not-occur.png)

#### Todos e qualquer um de

Em alguns casos, você pode desejar prever se uma combinação de eventos ocorrerá e, em outros casos, pode prever a ocorrência de qualquer evento a partir de um conjunto predefinido. Para prever se um cliente terá uma combinação de eventos, selecione a opção **[!UICONTROL All of]** no menu suspenso de segundo nível na página **[!UICONTROL Define Goal]**.

Por exemplo, você pode querer prever se um cliente compra um produto específico. Essa meta de previsão é definida por duas condições: um `commerce.order.purchaseID` **existe** e `productListItems.SKU` **é igual a** a um valor específico.

![Todos os exemplos](../images/user-guide/all-of.png)

Para prever se um cliente terá algum evento de um determinado conjunto, você pode usar a opção **[!UICONTROL Any of]** .

Por exemplo, você pode querer prever se um cliente visita um determinado URL ou uma página da Web com um nome específico. Essa meta de previsão é definida por duas condições: `web.webPageDetails.URL` **começa com** um valor específico e `web.webPageDetails.name` **começa com** um valor específico.

![Qualquer exemplo](../images/user-guide/any-of.png)

### Configurar um agendamento *(opcional)* {#configure-a-schedule}

A etapa **[!UICONTROL Advanced]** é exibida. Essa etapa opcional permite configurar um agendamento para automatizar execuções de previsão, definir exclusões de previsão para filtrar determinados eventos ou selecionar **[!UICONTROL Finish]** se nada for necessário.

Configure um agendamento de pontuação configurando o **[!UICONTROL Scoring Frequency]**. As execuções de previsão automatizada podem ser programadas para serem executadas semanalmente ou mensalmente.

![](../images/user-guide/schedule.png)

Abaixo da configuração da programação, você tem a capacidade de definir exclusões de previsão para evitar que eventos que atendem a determinadas condições sejam avaliados ao gerar pontuações. Esse recurso pode ser usado para filtrar entradas de dados irrelevantes.

Para excluir determinados eventos, selecione **[!UICONTROL Add exclusion]** e defina o evento da mesma maneira que a meta é definida. Para remover uma exclusão, selecione os elipses (**[!UICONTROL ...]**) no canto superior direito do contêiner de evento e selecione **[!UICONTROL Remove Container]**.

![](../images/user-guide/exclusion.png)

Exclua eventos conforme necessário e selecione **[!UICONTROL Finish]** para criar a instância.

![](../images/user-guide/advanced.png)

Se a instância for criada com êxito, uma execução de previsão será imediatamente acionada e as execuções subsequentes serão executadas de acordo com sua programação definida.

>[!NOTE]
>
>Dependendo do tamanho dos dados de entrada, as execuções de previsão podem levar até 24 horas para serem concluídas.

Ao seguir esta seção, você configurou uma instância do Customer AI e uma execução de previsão foi executada. Após a conclusão bem-sucedida da execução, os insights pontuados preenchem automaticamente os perfis com pontuações previstas. Aguarde até 24 horas antes de continuar para a próxima seção deste tutorial.

## Próximas etapas {#next-steps}

Ao seguir este tutorial, você configurou com sucesso uma instância do Customer AI e gerou pontuações de propensão. Agora você pode optar por usar o Construtor de segmentos para [criar segmentos de clientes com pontuações previstas](./create-segment.md) ou [descobrir insights com o Customer AI](./discover-insights.md).

## Recursos adicionais

O vídeo a seguir foi criado para oferecer suporte à compreensão do fluxo de trabalho de configuração do Customer AI. Além disso, práticas recomendadas e exemplos de casos de uso são fornecidos.

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)
