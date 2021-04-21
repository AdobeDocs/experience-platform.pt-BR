---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, interface do usuário, interface do usuário, personalização, painel de perfil, painel
title: Painel de perfis
description: A Adobe Experience Platform fornece um painel pelo qual você pode visualizar informações importantes sobre os dados do Perfil do cliente em tempo real da sua organização.
topic-legacy: guide
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 1%

---

# (Beta) [!UICONTROL Profiles] painel

>[!IMPORTANT]
>
>A funcionalidade do painel descrita neste documento está atualmente em beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

A interface do usuário do Adobe Experience Platform (UI) fornece um painel pelo qual você pode visualizar informações importantes sobre seus dados [!DNL Real-time Customer Profile], conforme capturados durante um instantâneo diário. Este guia descreve como acessar e trabalhar com o painel [!UICONTROL Profiles] na interface do usuário e fornece informações sobre as métricas exibidas no painel.

Para obter uma visão geral de todos os recursos de Perfil na interface do usuário do Experience Platform, visite o [Guia da interface do usuário de perfil do cliente em tempo real](../../profile/ui/user-guide.md).

## Dados do painel de perfis

O painel [!UICONTROL Profiles] exibe um instantâneo dos dados do atributo (registro) que sua organização tem no armazenamento de Perfil no Experience Platform. O instantâneo não inclui nenhum dado de evento (série de tempo).

Os dados do atributo no instantâneo mostram os dados exatamente como aparecem no momento específico em que o instantâneo foi tirado. Em outras palavras, o instantâneo não é uma aproximação ou amostra dos dados, e o painel de Perfil não está sendo atualizado em tempo real.

>[!NOTE]
>
>Quaisquer alterações ou atualizações feitas nos dados desde que o instantâneo foi tirado não serão refletidas no painel até que o próximo instantâneo seja tirado.

## Explorar o painel [!UICONTROL Profiles]

Para navegar até o painel [!UICONTROL Profiles] na interface do usuário da plataforma, selecione **[!UICONTROL Profiles]** no painel à esquerda e selecione a guia **[!UICONTROL Overview]** para exibir o painel.

![](../images/profiles/dashboard-overview.png)

### Selecionar políticas de mesclagem

As métricas exibidas no painel [!UICONTROL Profiles] são baseadas nas políticas de mesclagem aplicadas aos dados do Perfil do cliente em tempo real. Quando os dados são reunidos de várias fontes, é possível que os dados contenham valores conflitantes (por exemplo, um conjunto de dados pode listar um cliente como &quot;único&quot;, enquanto outro conjunto de dados pode listar o cliente como &quot;casado&quot;) e é tarefa da política de mesclagem determinar quais dados priorizar e exibir como parte do perfil.

O painel selecionará automaticamente uma política de mesclagem a ser exibida, mas você poderá alterar a política de mesclagem selecionada usando o menu suspenso. Para escolher uma política de mesclagem diferente, selecione o menu suspenso ao lado do nome da política de mesclagem e selecione a política de mesclagem que deseja exibir.

>[!NOTE]
>
>O menu suspenso mostra apenas as políticas de mesclagem relacionadas à Classe de Perfil Individual XDM. No entanto, se sua organização tiver criado várias políticas de mesclagem, pode significar que você precisará rolar para exibir a lista completa das políticas de mesclagem disponíveis.

Para obter mais informações sobre políticas de mesclagem, incluindo como criar, editar e declarar uma política de mesclagem padrão para sua organização, visite o [guia da interface do usuário de políticas de mesclagem](../../profile/ui/merge-policies.md).

![](../images/profiles/select-merge-policy.png)

### Widgets e métricas

O painel é composto de widgets, que são métricas somente leitura, fornecendo informações importantes sobre os dados do perfil. A data e a hora da &quot;última atualização&quot; em um widget mostram quando o último instantâneo dos dados foi tirado.

![](../images/profiles/dashboard-timestamp.png)

## Widgets disponíveis

O Experience Platform fornece vários widgets que você pode usar para visualizar métricas diferentes relacionadas aos dados do seu perfil. Selecione o nome de um widget abaixo para saber mais:

* [[!UICONTROL Audience size]](#audience-size)
* [[!UICONTROL Profiles added]](#profiles-added)
* [[!UICONTROL Profiles added over time]](#profiles-added-over-time)
* [[!UICONTROL Profiles by namespace]](#profiles-by-namespace)
* [[!UICONTROL Namespace overlap]](#namespace-overlap)

### [!UICONTROL Audience size] {#audience-size}

O widget **[!UICONTROL Audience size]** exibe o número total de perfis mesclados no armazenamento de dados do Perfil no momento em que o instantâneo foi tirado. Esse número é o resultado da política de mesclagem selecionada ser aplicada aos dados do Perfil para unir fragmentos de perfil para formar um único perfil para cada indivíduo.

Para obter mais informações sobre fragmentos e perfis mesclados, comece lendo a seção *Perfil de fragmentos vs perfis mesclados* da [Visão geral do perfil do cliente em tempo real](../../profile/home.md).

>[!NOTE]
>
>A política de mesclagem usada para calcular essa métrica não é a mesma que a política de mesclagem gerada pelo sistema usada para calcular [!UICONTROL Addressable audiences] no painel [!UICONTROL License usage], portanto, é improvável que a contagem de públicos-alvo nos painéis [!UICONTROL Profiles] e [!UICONTROL License usage] seja exatamente a mesma.

![](../images/profiles/audience-size.png)

### [!UICONTROL Profiles added] {#profiles-added}

O widget **[!UICONTROL Profiles added]** exibe o número total de perfis mesclados que foram adicionados ao armazenamento de dados do Perfil desde que o último instantâneo foi tirado. Esse número é o resultado da política de mesclagem selecionada ser aplicada aos dados do Perfil para unir fragmentos de perfil para formar um único perfil para cada indivíduo.

![](../images/profiles/profiles-added.png)

### [!UICONTROL Profiles added over time] {#profiles-added-over-time}

O widget **[!UICONTROL Profiles added over time]** exibe o número total de perfis mesclados que foram adicionados ao armazenamento de dados do perfil diariamente nos últimos 30 dias. Esse número é atualizado todos os dias quando o instantâneo é tirado. Portanto, se você assimilasse perfis na Platform, o número de perfis não seria refletido até que o próximo instantâneo fosse tirado.

A contagem de perfis adicionada é o resultado da política de mesclagem selecionada ser aplicada aos dados do perfil para unir fragmentos de perfil para formar um único perfil para cada indivíduo.

![](../images/profiles/profiles-added-over-time.png)

### [!UICONTROL Profiles by namespace] {#profiles-by-namespace}

O widget **[!UICONTROL Profiles by namespace]** exibe o detalhamento dos namespaces de identidade em todos os perfis mesclados no armazenamento de Perfil. O número total de perfis por [!UICONTROL ID namespace] (em outras palavras, adicionar os valores mostrados para cada namespace) pode ser maior que o número total de perfis de mesclagem, pois um perfil pode ter vários namespaces associados a ele. Por exemplo, se um cliente interagir com sua marca em mais de um canal, vários namespaces serão associados a esse cliente individual.

Para saber mais sobre os namespaces de identidade, visite a [documentação do Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/profiles/profiles-by-namespace.png)

### [!UICONTROL Namespace overlap] {#namespace-overlap}

O widget **[!UICONTROL Namespace overlap]** exibe um diagrama Venn ou um diagrama de conjunto que mostra a sobreposição de perfis em seu armazenamento de perfil que contém vários namespaces de identidade.

Depois de usar os menus suspensos no widget para selecionar os namespaces de identidade que deseja comparar, os círculos aparecem exibindo o tamanho relativo de cada namespace, com o número de perfis contendo ambos os namespaces sendo representado pelo tamanho da sobreposição entre os círculos.

Se um cliente interagir com sua marca em mais de um canal, vários namespaces serão associados a esse cliente individual, portanto, é provável que sua organização tenha vários perfis contendo fragmentos de mais de um namespace de identidade.

Para saber mais sobre os namespaces de identidade, visite a [documentação do Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/profiles/namespace-overlap.png)

## Próximas etapas

Agora, ao seguir este documento, você pode localizar o painel Perfis e entender as métricas exibidas nos widgets disponíveis. Para saber mais sobre como trabalhar com dados [!DNL Profile] na interface do usuário do Experience Platform, consulte o [Guia da interface do usuário do perfil do cliente em tempo real](../../profile/ui/user-guide.md).
