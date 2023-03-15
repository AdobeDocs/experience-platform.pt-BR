---
title: (Beta) Exportar arquivos sob demanda para destinos em lote usando a interface do Experience Platform
type: Tutorial
description: Saiba como exportar arquivos sob demanda para destinos em lote usando a interface do usuário do Experience Platform.
exl-id: 0cbe5089-b73d-4584-8451-2fc34d47c357
source-git-commit: 29962e07aa50c97b6098f4c892facf48508d28cf
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---

# (Beta) Exportar arquivos sob demanda para destinos em lote usando a interface do Experience Platform

>[!IMPORTANT]
>
>A variável **[!UICONTROL Exportar arquivo agora]** no Adobe Experience Platform está atualmente na versão beta. A documentação e a funcionalidade estão sujeitas a alterações.
>Entre em contato com o representante da Adobe para obter acesso a essa funcionalidade.

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

## **[!UICONTROL Exportar arquivo agora]** visão geral {#overview}

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_activatenow"
>title="Exportar arquivo agora"
>abstract="Selecione este controle para fornecer uma exportação de arquivo completa além de quaisquer exportações programadas anteriormente. A exportação de arquivos é acionada imediatamente e obtém os resultados mais recentes das execuções de segmentação de Experience Platform."

Este artigo explica como usar a interface do Experience Platform para exportar arquivos sob demanda para destinos em lote, como [armazenamento na nuvem](/help/destinations/catalog/cloud-storage/overview.md) e [marketing por email](/help/destinations/catalog/email-marketing/overview.md) destinos.

A variável **[!UICONTROL Exportar arquivo agora]** o controle permite exportar um arquivo completo sem interromper a programação de exportação atual de um segmento programado anteriormente. Essa exportação ocorre além das exportações programadas anteriormente e não altera a frequência de exportação do segmento. A exportação de arquivos é acionada imediatamente e obtém os resultados mais recentes das execuções de segmentação de Experience Platform.

Também é possível usar as APIs de Experience Platform para essa finalidade. Ler como [ativar segmentos de público-alvo sob demanda para destinos em lote por meio da API de ativação ad-hoc](/help/destinations/api/ad-hoc-activation-api.md).

## Pré-requisitos {#prerequisites}

Para exportar arquivos sob demanda para destinos em lote, você deve ter o [conectado a um destino](./connect-destination.md). Se ainda não tiver feito isso, acesse o [catálogo de destinos](../catalog/overview.md), navegue pelos destinos compatíveis e configure o destino que deseja usar.

## Como exportar arquivos por demanda {#how-to-export-files-on-demand}

1. Ir para **[!UICONTROL Conexões > Destinos]**, selecione o **[!UICONTROL Procurar]** e o símbolo de filtro para mostrar as conexões existentes aos destinos em lote desejados.

   ![Imagem que destaca como acessar a guia de navegação e filtrar fluxos de dados existentes.](../assets/ui/activate-on-demand/browse-tab.png)

2. Selecione a conexão de destino desejada para inspecionar o fluxo de dados existente para o destino.

   ![Imagem destacando um fluxo de dados filtrado.](../assets/ui/activate-on-demand/filtered-dataflow.png)

3. Selecione o **[!UICONTROL Dados de ativação]** e selecione o segmento para o qual deseja exportar um arquivo por demanda e selecione o **[!UICONTROL Exportar arquivo agora]** controle para acionar uma exportação única que entregará um arquivo ao destino do lote.

   >[!IMPORTANT]
   >
   >No momento, não há suporte na interface do usuário para selecionar vários segmentos para exportar arquivos por demanda em massa. Use o [API de ativação ad-hoc](/help/destinations/api/ad-hoc-activation-api.md) para esse efeito.

   ![Imagem destacando o botão Exportar arquivo agora.](../assets/ui/activate-on-demand/activate-segment-on-demand.png)

4. Selecionar **[!UICONTROL Sim]** para confirmar e acionar a exportação do arquivo.

   ![Imagem mostrando a caixa de diálogo de confirmação Exportar arquivo agora.](../assets/ui/activate-on-demand/confirm-activation.png)

5. Uma mensagem de confirmação é exibida, informando que a exportação de arquivo foi iniciada.

   ![Imagem mostrando a confirmação de ativação ad-hoc bem-sucedida.](../assets/ui/activate-on-demand/ad-hoc-success.png)

6. Você também pode alternar para a variável **[!UICONTROL O fluxo de dados é executado]** para confirmar se a exportação do arquivo foi iniciada.

## Considerações {#considerations}

Lembre-se das seguintes considerações ao usar o **[!UICONTROL Exportar arquivo agora]** controle:

* **[!UICONTROL Exportar arquivo agora]** O funciona somente para segmentos cujo agendamento no fluxo de dados de ativação em lote se sobrepõe à data atual. Isso inclui segmentos com programações sem data final (frequência de exportação de **[!UICONTROL Uma vez]**), ou quando a data final ainda não tiver passado.
* Ao adicionar um segmento a um fluxo de dados existente, aguarde pelo menos 15 minutos até usar o **[!UICONTROL Exportar arquivo agora]** controle.
* Se você alterar a política de mesclagem de um segmento ou se criar um segmento que use uma nova política de mesclagem, aguarde 24 horas até usar o **[!UICONTROL Exportar arquivo agora]** controle.

## Mensagens de erro da interface do usuário {#ui-error-messages}

Ao usar o **[!UICONTROL Exportar arquivo agora]** controle, você poderá encontrar qualquer uma das mensagens de erro listadas abaixo. Revise a tabela para entender como abordá-los quando eles forem exibidos.

| Mensagem de erro | Resolução |
|---------|----------|
| Execução já em andamento para o segmento `segment ID` para pedido `dataflow ID` com id de execução `flow run ID` | Essa mensagem de erro indica que um fluxo de ativação ad-hoc está em andamento para um segmento. Aguarde a conclusão do trabalho antes de acionar o trabalho de ativação novamente. |
| Segmentos `<segment name>` não fazem parte desse fluxo de dados ou estão fora do intervalo programado! | Essa mensagem de erro indica que os segmentos selecionados para ativação não estão mapeados para o fluxo de dados ou que o agendamento de ativação configurado para os segmentos expirou ou ainda não foi iniciado. Verifique se o segmento é de fato mapeado para o fluxo de dados e se a programação de ativação do segmento se sobrepõe à data atual. |

## Informações relacionadas {#related-information}

* [Ative segmentos de público-alvo para destinos em lote sob demanda usando as APIs do Experience Platform](/help/destinations/api/ad-hoc-activation-api.md)
* [Ativar dados do público-alvo para destinos de exportação de perfil em lote](/help/destinations/ui/activate-batch-profile-destinations.md)
