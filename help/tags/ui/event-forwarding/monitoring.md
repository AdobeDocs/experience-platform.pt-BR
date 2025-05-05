---
title: Monitorar atividades no encaminhamento de eventos
description: Saiba como monitorar uso, erros e tempo de computação nas propriedades do encaminhamento de eventos.
feature: Event Forwarding
exl-id: 9d8572a3-816e-4b66-afe6-344fe8a15f22
source-git-commit: f8988d08e7009cc613a00f34e8151e8560c479d4
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# Monitorar atividades no encaminhamento de eventos (Beta)

>[!IMPORTANT]
>
>No momento, esse recurso está na versão beta e talvez sua organização ainda não tenha acesso a ele. A funcionalidade e a documentação estão sujeitas a alterações.

A guia **[!UICONTROL Monitoramento]** da interface da Coleção de dados permite monitorar padrões de uso, erros e o tempo de computação das propriedades de encaminhamento de eventos. Este guia fornece uma visão geral de alto nível sobre como visualizar e entender os relatórios mostrados na guia.

![Imagem mostrando a guia de monitoramento na interface da Coleção de Dados](../../images/ui/event-forwarding/monitoring/monitoring-tab.png)

## Pré-requisitos

Este guia pressupõe que você adquiriu o encaminhamento de eventos e que possui uma compreensão funcional de como funciona o encaminhamento de eventos. Consulte a [visão geral do encaminhamento de eventos](./overview.md) para obter mais informações.

## Visão geral do vídeo

Assista ao vídeo a seguir para obter uma visão geral de alto nível do recurso de monitoramento:

>[!VIDEO](https://video.tv.adobe.com/v/3412566?quality=12&learn=on&captions=por_br)

## Seleção de propriedades e ambientes

Você pode visualizar métricas em um ambiente e propriedade individuais ou em todas as propriedades e ambientes de propriedade de sua organização.

Para mostrar métricas para uma única propriedade, selecione o menu suspenso de propriedades e escolha a propriedade de interesse na lista. Depois de escolher uma propriedade, você também pode usar a lista suspensa de ambientes para selecionar um ambiente de interesse.

![Imagem mostrando os menus suspensos de ambiente de propriedade na interface do usuário](../../images/ui/event-forwarding/monitoring/property-environment.png)

## [!UICONTROL Uso]

>[!NOTE]
>
>Os dados de uso são atualizados todos os meses após o término do mês anterior.

O relatório **[!UICONTROL Uso]** mostra chamadas de entrada e saída para um determinado período. As chamadas de entrada representam dados enviados para o encaminhamento de eventos. Chamadas de saída representam dados enviados do encaminhamento de eventos. O número **[!UICONTROL Total de eventos]** no painel esquerdo é a soma das chamadas de entrada e saída para o período determinado.

## [!UICONTROL Eventos de erro]

O relatório **[!UICONTROL Eventos de Erro]** mostra erros na agregação e divididos por código de resposta HTTP quando você passa o cursor sobre o gráfico de linhas. Os erros exibidos são de chamadas de saída e os códigos de resposta são do endpoint com o qual o encaminhamento de eventos está interagindo.

Os erros são mostrados por um determinado período, que pode ser ajustado no menu suspenso fornecido.

![Imagem mostrando o menu suspenso de período de tempo do relatório de Eventos de Erro](../../images/ui/event-forwarding/monitoring/error-time.png)

A caixa de pesquisa do evento de erro permite consultar o encaminhamento de eventos para entender os erros de um determinado domínio de endpoint. Você deve inserir o domínio exato, pois o recurso de pesquisa não aceita aproximações ou correspondências difusas. Depois de fornecer um domínio exato para o qual há dados de erro de saída, pressione Enter e o relatório é atualizado para mostrar erros de saída para esse domínio. Por exemplo, para ver erros do ponto de extremidade da API de Conversões do Facebook, o domínio deve ser gravado como `https://graph.facebook.com`.

## [!UICONTROL Tempo de Computação]

O relatório **[!UICONTROL Tempo de Computação]** mostra o tempo de computação de todas as regras nos servidores de encaminhamento de eventos.

>[!NOTE]
>
>Os horários exibidos não representam a latência completa. O encaminhamento de eventos tem uma limitação de tempo de computação de 50 milissegundos. Se esse limite for excedido, os dados relacionados serão descartados.

Os seguintes fatores afetam o tempo de computação:

1. O número de regras
2. A complexidade das regras, geralmente impulsionada pela quantidade de JavaScript personalizados sendo executados

Por exemplo, se uma ação no encaminhamento de eventos atingir um endpoint e esse endpoint levar dois segundos para responder, essa latência de dois segundos não contará no tempo de computação, pois o encaminhamento de eventos está apenas aguardando e não calculando nada ativamente. O tempo de resposta não pode ser superior a 30 segundos; caso contrário, os dados serão descartados.
