---
title: Exportar arquivos sob demanda para destinos em lote usando a interface do usuário do Experience Platform
type: Tutorial
description: Saiba como exportar arquivos por demanda para destinos em lote usando a interface do usuário do Experience Platform.
exl-id: 0cbe5089-b73d-4584-8451-2fc34d47c357
source-git-commit: 111f6d5093a0b66a683745b1da8d8909eb17f7eb
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 8%

---


# Exportar arquivos sob demanda para destinos em lote usando a interface do usuário do Experience Platform

>[!IMPORTANT]
> 
>Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

## Visão geral do **[!UICONTROL Export file now]** {#overview}

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_activatenow"
>title="Exportar arquivo agora"
>abstract="Selecione esse controle para fornecer uma exportação de arquivo completa, além de qualquer exportação agendada anteriormente. A exportação de arquivos é acionada imediatamente e obtém os resultados mais recentes das execuções de segmentação da Experience Platform."

Este artigo explica como usar a interface do Experience Platform para exportar arquivos sob demanda para destinos em lote, como destinos de [armazenamento na nuvem](/help/destinations/catalog/cloud-storage/overview.md) e [marketing por email](/help/destinations/catalog/email-marketing/overview.md).

O controle **[!UICONTROL Export file now]** permite exportar um arquivo completo sem interromper o agendamento de exportação atual de um público agendado anteriormente. Essa exportação ocorre além das exportações previamente agendadas e não altera a frequência de exportação do público-alvo. A exportação de arquivos é acionada imediatamente e obtém os resultados mais recentes das execuções de segmentação da Experience Platform.

Também é possível usar as APIs do Experience Platform para essa finalidade. Leia como [ativar públicos-alvo sob demanda para destinos em lote por meio da API de ativação ad-hoc](/help/destinations/api/ad-hoc-activation-api.md).

## Pré-requisitos {#prerequisites}

Para exportar arquivos por demanda para destinos em lote, você deve ter [se conectado com êxito a um destino](./connect-destination.md). Se ainda não tiver feito isso, vá para o [catálogo de destinos](../catalog/overview.md), navegue pelos destinos compatíveis e configure o destino que deseja usar.

## Como exportar arquivos por demanda {#how-to-export-files-on-demand}

1. Vá para **[!UICONTROL Connections > Destinations]**, selecione a guia **[!UICONTROL Browse]** e o símbolo de filtro para mostrar as conexões existentes aos destinos em lote desejados.

   ![Imagem destacando como chegar à guia de navegação e filtrar fluxos de dados existentes.](../assets/ui/activate-on-demand/browse-tab.png)

2. Selecione a conexão de destino desejada para inspecionar o fluxo de dados existente para o destino.

   ![Imagem destacando um fluxo de dados filtrado.](../assets/ui/activate-on-demand/filtered-dataflow.png)

3. Selecione a guia **[!UICONTROL Activation data]**, selecione os públicos para os quais deseja exportar arquivos por demanda e selecione o controle **[!UICONTROL Export file now]** para acionar uma exportação única que fornecerá um arquivo para cada público selecionado para o destino do lote.

   ![Imagem destacando o botão Exportar arquivo agora.](../assets/ui/activate-on-demand/bulk-export-file-now.png)

4. Selecione **[!UICONTROL Yes]** para confirmar e acionar a exportação de arquivo.

   ![Imagem mostrando a caixa de diálogo de confirmação Exportar arquivo agora.](../assets/ui/activate-on-demand/confirm-activation.png)

5. Uma mensagem de confirmação é exibida, informando que a exportação de arquivo foi iniciada.

   ![Imagem mostrando a confirmação de ativação ad-hoc bem-sucedida.](../assets/ui/activate-on-demand/ad-hoc-success.png)

6. Você também pode alternar para a guia **[!UICONTROL Dataflow runs]** para confirmar que a exportação de arquivo foi iniciada.

## Considerações {#considerations}

Lembre-se das seguintes considerações ao usar o controle **[!UICONTROL Export file now]**:

* **[!UICONTROL Export file now]** funciona somente para públicos cujo agendamento no fluxo de dados de ativação em lote se sobrepõe à data atual. Isso inclui públicos com agendamentos sem data de término (frequência de exportação de **[!UICONTROL Once]**) ou em que a data de término ainda não tenha passado.
* Ao adicionar um público a um fluxo de dados existente, aguarde pelo menos **uma hora** antes de usar o controle **[!UICONTROL Export file now]**.
* Se você alterar a política de mesclagem de um público ou se criar um público que use uma nova política de mesclagem, aguarde 24 horas até usar o controle **[!UICONTROL Export file now]**.
* **[!UICONTROL Export file now]** usa somente dados de exportações de instantâneo agendadas. Ele não coleta dados de trabalhos de exportação acionados por API. Para exportar os dados mais recentes após um trabalho de exportação acionado por API, aguarde a próxima exportação agendada para executar.

## Mensagens de erro da interface do usuário {#ui-error-messages}

Ao usar o controle **[!UICONTROL Export file now]**, você pode encontrar qualquer uma das mensagens de erro listadas abaixo. Revise a tabela para entender como abordá-los quando eles forem exibidos.

| Mensagem de erro | Resolução |
|---------|----------|
| Execução já em andamento para a audiência `segment ID` para a ordem `dataflow ID` com a ID de execução `flow run ID` | Essa mensagem de erro indica que um fluxo de ativação ad-hoc está em andamento para um público-alvo. Aguarde a conclusão do trabalho antes de acionar o trabalho de ativação novamente. |
| Os públicos-alvo `<segment name>` não fazem parte desse fluxo de dados ou estão fora do intervalo programado! | Essa mensagem de erro indica que os públicos selecionados para ativação não estão mapeados para o fluxo de dados ou que o agendamento de ativação configurado para os públicos expirou ou ainda não foi iniciado. Verifique se o público-alvo está realmente mapeado para o fluxo de dados e se o agendamento de ativação de público-alvo se sobrepõe à data atual. |

## Informações relacionadas {#related-information}

* [Ative públicos para destinos em lote sob demanda usando as APIs do Experience Platform](/help/destinations/api/ad-hoc-activation-api.md)
* [Ativar dados do público-alvo para destinos de exportação de perfil em lote](/help/destinations/ui/activate-batch-profile-destinations.md)
