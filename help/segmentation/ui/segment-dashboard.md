---
keywords: Experience Platform;perfil;segmento;segmentos;segmentação;interface do usuário;UI;personalização;painel de segmento;painel;;;segment;segmentation;user interface;personalization;segment;
title: Guia da interface do usuário do Painel de segmento
description: 'Este guia descreve o painel de segmento disponível na interface do usuário do Adobe Experience Platform. '
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 1%

---


# (Alfa) painel de segmento {#segment-dashboard}

>[!IMPORTANT]
>
>A funcionalidade do painel descrita neste documento está atualmente em alfa e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

A interface do usuário do Adobe Experience Platform (UI) fornece um painel através do qual você pode visualização informações importantes sobre seus segmentos, conforme capturado durante um instantâneo diário. Este guia descreve como acessar e trabalhar com o painel de segmento na interface do usuário e fornece mais informações sobre as visualizações exibidas no painel.

Para obter uma visão geral de todos os recursos do Adobe Experience Platform Segmentation Service na interface do usuário da plataforma, visite o [guia da interface do usuário do Serviço de segmentação](overview.md).

## Dados do painel do segmento

O painel do segmento exibe um instantâneo dos dados do atributo (registro) que sua organização tem no repositório de Perfis no Experience Platform. O instantâneo não inclui nenhum dado de evento (série cronológica).

Os dados do atributo no instantâneo mostram os dados exatamente como aparecem no momento específico em que o instantâneo foi realizado. Em outras palavras, o instantâneo não é uma aproximação ou amostra dos dados, e o painel de segmento não está sendo atualizado em tempo real.

>[!NOTE]
>
>Quaisquer alterações ou atualizações feitas nos dados desde que o instantâneo foi realizado não serão refletidas no painel até que o próximo instantâneo seja realizado.

## Explorar o painel de segmento

Para navegar até o painel de segmento na interface do usuário da plataforma, selecione **[!UICONTROL Segmentos]** no painel esquerdo, em seguida, selecione a guia **[!UICONTROL Visão geral]** para exibir o painel.

![](../images/ui/segment-dashboard/dashboard-overview.png)

### Selecionar um segmento

Para selecionar um segmento para visualização no painel, escolha o seletor de diálogo para a caixa de texto **[!UICONTROL Selecionar segmento]**.

![](../images/ui/segment-dashboard/select-segment.png)

>[!NOTE]
>
>Se um segmento já estiver selecionado, use `X` para remover o segmento primeiro e o seletor de diálogo será exibido.
>
>![](../images/ui/segment-dashboard/remove-segment.png)

A caixa de diálogo **[!UICONTROL Selecionar segmento]** é aberta, permitindo que você escolha o segmento que deseja visualização. Depois de escolher o segmento desejado, use **[!UICONTROL Select]** para voltar ao painel.

![](../images/ui/segment-dashboard/select-segment-dialog.png)

### Política de mesclagem

Após selecionar um segmento, a caixa de texto da política de mesclagem será preenchida automaticamente com a política de mesclagem relacionada a esse segmento.

Para saber mais sobre como criar segmentos no Experience Platform, visite o [guia da interface do usuário do Construtor de segmentos](segment-builder.md). Para obter mais informações sobre políticas de mesclagem, comece lendo a [visão geral do Perfil do cliente em tempo real](../../profile/home.md).

![](../images/ui/segment-dashboard/merge-policy.png)

### Widgets e métricas

O painel de segmento é composto de widgets, que são métricas somente leitura que fornecem informações importantes sobre o segmento selecionado. A data e a hora &quot;última atualização&quot; no widget mostram quando o último instantâneo dos dados foi realizado.

![](../images/ui/segment-dashboard/widget-timestamp.png)

## Widgets disponíveis

O Experience Platform fornece vários widgets que você pode usar para visualizar diferentes métricas relacionadas ao seu segmento. Selecione o nome de um widget abaixo para saber mais:

* [[!UICONTROL Tamanho do segmento]](#segment-size)
* [[!UICONTROL Perfis por namespace]](#profiles-by-namespace)

### [!UICONTROL Tamanho do segmento] {#segment-size}

O widget **[!UICONTROL Tamanho do segmento]** exibe o número total de perfis unidos no segmento selecionado no momento em que o snapshot foi realizado. Esse número é o resultado da aplicação da política de mesclagem de segmentos aos dados do Perfil para unir os fragmentos do perfil e formar um único perfil para cada indivíduo no segmento.

Para obter mais informações sobre fragmentos e perfis mesclados, comece lendo [Visão geral do Perfil do cliente em tempo real](../home.md).

![](../images/ui/segment-dashboard/segment-size.png)

### [!UICONTROL Perfis por namespace] {#profiles-by-namespace}

O widget **[!UICONTROL Perfis por namespace]** exibe o detalhamento das namespaces em todos os perfis unidos no segmento selecionado. O número total de perfis por [!UICONTROL namespace de ID] (em outras palavras, adicionar os valores mostrados para cada namespace) geralmente será maior que o número total de perfis no segmento, pois um perfil pode ter várias namespaces associadas a ele. Por exemplo, se um cliente interage com sua marca em mais de um canal, várias namespaces podem ser associadas a esse cliente individual.

Para saber mais sobre namespaces de identidade, visite a [documentação do Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/ui/segment-dashboard/profiles-by-namespace.png)

## Painéis adicionais

A interface do usuário da plataforma fornece painéis adicionais para visualizar instantâneos de seus dados no Experience Platform. Esses painéis incluem o Perfil do cliente em tempo real e [!UICONTROL Uso da licença]. Para obter mais informações sobre esses painéis adicionais, selecione um dos seguintes links:

* [[!DNL Profile] painel](../../profile/ui/profile-dashboard.md)
* [[!UICONTROL Licença ] usagedashboard](../../landing/license-usage-dashboard.md)

## Próximas etapas

Ao seguir esse documento, você deve ser capaz de localizar o painel de segmento e selecionar um segmento para visualização. Você também deve entender as métricas exibidas nos widgets disponíveis. Para saber mais sobre como trabalhar com segmentos na interface do usuário do Experience Platform, consulte o [guia da interface do usuário do serviço de segmentação](overview.md).