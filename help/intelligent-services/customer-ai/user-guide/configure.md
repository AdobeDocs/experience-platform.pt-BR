---
keywords: Experience Platform;user guide;customer ai;popular topics;configure instance;create instance;
solution: Experience Platform
title: Configuração de uma instância do AI do cliente
topic: Instance creation
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---


# Configuração de uma instância do AI do cliente

A IA do cliente, como parte dos Serviços inteligentes, permite que você gere pontuações de propensão personalizadas sem precisar se preocupar com o aprendizado da máquina.

Os Serviços inteligentes fornecem IA do cliente como um serviço Adobe Sensei simples de usar que pode ser configurado para diferentes casos de uso. As seções a seguir fornecem etapas para configurar uma instância da API do cliente.

## Configurar sua instância {#set-up-your-instance}

Na interface do usuário do Platform, clique em **[!UICONTROL Serviços]** no painel de navegação esquerdo. O navegador **[!UICONTROL Serviços]** é exibido e exibe todos os serviços disponíveis à sua disposição. No container para API do cliente, clique em **[!UICONTROL Abrir]**.

![](../images/user-guide/navigate-to-service.png)

A tela *Customer AI* (AI do cliente) exibe todas as instâncias existentes do Customer AI. Clique em **[!UICONTROL Criar instância]**.

![](../images/user-guide/dashboard.png)

O fluxo de trabalho de criação da instância é exibido, começando na etapa *Configuração* .

Abaixo estão informações importantes sobre valores que devem ser fornecidos à instância com:

* O nome da instância será usado em todos os locais onde a pontuação da AI do cliente for exibida. Assim, os nomes devem descrever o que as pontuações de previsão representam, por exemplo, &quot;Probabilidade de cancelar a subscrição de revistas&quot;.

* O tipo de propensão determina a intenção da pontuação e da polaridade da métrica. Você pode escolher **[!UICONTROL Churn]** ou **[!UICONTROL Conversion]**. Consulte a nota em [um resumo](./discover-insights.md#scoring-summary) de pontuação no documento de insights de descoberta para obter mais informações sobre como o tipo de propensão afeta sua instância.

* A fonte de dados é o local onde os dados estão localizados. Conjunto de dados é o conjunto de dados de entrada usado para prever pontuações. Por padrão, a IA do cliente usa os dados do Evento da experiência do consumidor para calcular as pontuações de propensão. Ao selecionar um conjunto de dados no seletor suspenso, somente os que são compatíveis com a IA do cliente são listados.

* Por padrão, as pontuações de propensão são geradas para todos os perfis, a menos que uma população qualificada seja especificada. Você pode especificar uma população qualificada definindo condições para incluir ou excluir perfis com base em eventos.

Forneça os valores necessários e clique em **[!UICONTROL Avançar]**.

![](../images/user-guide/setup.png)

### Definir uma meta {#define-a-goal}

A etapa *Definir meta* é exibida e fornece um ambiente interativo para que você defina visualmente uma meta. Uma meta é composta de um ou mais eventos, nos quais cada ocorrência de evento é baseada na condição que contém. O objetivo de uma instância da API do cliente é determinar a probabilidade de atingir sua meta dentro de um determinado intervalo de tempo.

Clique em **[!UICONTROL Inserir nome]** do campo e selecione um campo na lista suspensa. Clique na segunda entrada e selecione uma cláusula para a condição do evento, em seguida, forneça o valor do público alvo para concluir o evento. eventos adicionais podem ser configurados clicando em **[!UICONTROL Adicionar evento]**. Por fim, conclua a meta aplicando um período de previsão em número de dias e clique em **[!UICONTROL Avançar]**.

![](../images/user-guide/goal.png)

### Configurar um agendamento *(opcional)* {#configure-a-schedule}

A etapa *avançada* é exibida. Esta etapa opcional permite configurar uma programação para automatizar execuções de previsão, definir exclusões de previsão para filtrar determinados eventos ou clicar em **[!UICONTROL Concluir]** se nada for necessário.

Configure um agendamento de pontuação configurando a Frequência *de* Pontuação. As execuções de previsão automatizadas podem ser programadas para serem executadas semanalmente ou mensalmente.

![](../images/user-guide/schedule.png)

Abaixo da configuração da programação, você pode definir exclusões de previsão para impedir que eventos que atendem a determinadas condições sejam avaliados ao gerar pontuações. Este recurso pode ser usado para filtrar entradas de dados irrelevantes.

Para excluir determinados eventos, clique em **[!UICONTROL Adicionar exclusão]** e defina o evento da mesma forma que a meta é definida. Para remover uma exclusão, clique nas elipses (**[!UICONTROL ...]**) na parte superior direita do container do evento e clique em **[!UICONTROL Remover Container]**.

![](../images/user-guide/exclusion.png)

Exclua eventos conforme necessário e clique em **[!UICONTROL Concluir]** para criar a instância.

![](../images/user-guide/advanced.png)

Se a instância for criada com êxito, uma execução de previsão será acionada imediatamente e as execuções subsequentes serão executadas de acordo com a programação definida.

>[!NOTE]
>
>Dependendo do tamanho dos dados de entrada, as execuções de previsão podem levar até 24 horas para serem concluídas.

Ao seguir esta seção, você configurou uma instância do AI do cliente e uma execução de previsão foi executada. Após a conclusão bem-sucedida da execução, insights pontuados preenchem automaticamente perfis com pontuações previstas. Aguarde até 24 horas antes de continuar com a próxima seção deste tutorial.

## Próximas etapas {#next-steps}

Ao seguir este tutorial, você configurou com êxito uma instância da IA do cliente e gerou pontuações de propensão. Agora você pode optar por usar o Construtor de segmentos para [criar segmentos de clientes com pontuações](./create-segment.md) previstas ou [descobrir insights com a IA](./discover-insights.md)do cliente.

## Recursos adicionais

O vídeo a seguir foi projetado para oferecer suporte à sua compreensão do fluxo de trabalho de configuração para a IA do cliente. Além disso, as práticas recomendadas e exemplos de casos de uso são fornecidos.

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)

