---
keywords: Experience Platform;perfil;perfil; do cliente em tempo real;interface do usuário;personalização;painel do perfil;painel;user interface;customization;;
title: Painel perfis
description: A Adobe Experience Platform fornece um painel através do qual você pode visualização informações importantes sobre os dados do Perfil do cliente em tempo real da sua organização.
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 2f2459c1c88c97a3ab322b08ee178463fbb4a592
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 0%

---


# (Beta) painel [!UICONTROL Perfis]

>[!IMPORTANT]
>
>A funcionalidade do painel descrita neste documento está atualmente em beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

A interface do usuário do Adobe Experience Platform (UI) fornece um painel através do qual você pode visualização informações importantes sobre seus dados [!DNL Real-time Customer Profile], conforme capturados durante um instantâneo diário. Este guia descreve como acessar e trabalhar com o painel [!UICONTROL Perfis] na interface do usuário e fornece informações relacionadas às métricas exibidas no painel.

Para obter uma visão geral de todos os recursos do Perfil na interface do usuário do Experience Platform, visite o [Guia da interface do usuário do Perfil do cliente em tempo real](../../profile/ui/user-guide.md).

## Dados do painel do perfil

O painel [!UICONTROL Perfis] exibe um instantâneo dos dados do atributo (registro) que sua organização tem no repositório de Perfis no Experience Platform. O instantâneo não inclui nenhum dado de evento (série cronológica).

Os dados do atributo no instantâneo mostram os dados exatamente como aparecem no momento específico em que o instantâneo foi realizado. Em outras palavras, o instantâneo não é uma aproximação ou amostra dos dados, e o painel do Perfil não está sendo atualizado em tempo real.

>[!NOTE]
>
>Quaisquer alterações ou atualizações feitas nos dados desde que o instantâneo foi realizado não serão refletidas no painel até que o próximo instantâneo seja realizado.

## Explorar o painel [!UICONTROL Perfis]

Para navegar até o painel [!UICONTROL Perfis] na interface do usuário da plataforma, selecione **[!UICONTROL Perfis]** no painel esquerdo e selecione a guia **[!UICONTROL Visão geral]** para exibir o painel.

![](../images/profiles/dashboard-overview.png)

### Selecionar políticas de mesclagem

As métricas exibidas no painel [!UICONTROL Perfis] são baseadas nas políticas de mesclagem aplicadas aos dados do Perfil do cliente em tempo real. Quando os dados são reunidos de várias fontes, é possível que os dados contenham valores conflitantes (por exemplo, um conjunto de dados pode lista um cliente como &quot;único&quot;, enquanto outro conjunto de dados pode lista o cliente como &quot;casado&quot;) e é tarefa da política de mesclagem determinar quais dados priorizar e exibir como parte do perfil.

O painel selecionará automaticamente uma política de mesclagem a ser exibida, mas é possível alterar a política de mesclagem selecionada usando o menu suspenso. Para escolher uma política de mesclagem diferente, selecione a lista suspensa ao lado do nome da política de mesclagem e selecione a política de mesclagem que deseja visualização.

>[!NOTE]
>
>O menu suspenso mostra somente as políticas de mesclagem relacionadas à Classe de Perfil Individual XDM. No entanto, se sua organização tiver criado várias políticas de mesclagem, isso pode significar que você precisará rolar para visualização da lista completa das políticas de mesclagem disponíveis.

Para obter mais informações sobre políticas de mesclagem, incluindo como criar, editar e declarar uma política de mesclagem padrão para sua organização, visite o [guia da interface do usuário das políticas de mesclagem](../../profile/ui/merge-policies.md).

![](../images/profiles/select-merge-policy.png)

### Widgets e métricas

O painel é composto de widgets, que são métricas somente leitura que fornecem informações importantes sobre os dados do Perfil. A data e a hora &quot;última atualização&quot; em um widget mostra quando o último instantâneo dos dados foi realizado.

![](../images/profiles/dashboard-timestamp.png)

## Widgets disponíveis

O Experience Platform fornece vários widgets que você pode usar para visualizar diferentes métricas relacionadas aos dados do Perfil. Selecione o nome de um widget abaixo para saber mais:

* [[!UICONTROL tamanho da audiência]](#audience-size)
* [[!UICONTROL Perfis adicionados]](#profiles-added)
* [[!UICONTROL Perfis adicionados ao longo do tempo]](#profiles-added-over-time)
* [[!UICONTROL Perfis por namespace]](#profiles-by-namespace)
* [[!UICONTROL sobreposição de namespace]](#namespace-overlap)

### [!UICONTROL tamanho da audiência] {#audience-size}

O widget **[!UICONTROL Audiência size]** exibe o número total de perfis unidos no armazenamento de dados do Perfil no momento em que o snapshot foi realizado. Esse número é o resultado da política de mesclagem selecionada que está sendo aplicada aos dados do Perfil para unir os fragmentos do perfil e formar um único perfil para cada indivíduo.

Para obter mais informações sobre fragmentos e perfis mesclados, comece lendo a seção *fragmentos de Perfil vs perfis mesclados* da [Visão geral do Perfil do cliente em tempo real](../../profile/home.md).

>[!NOTE]
>
>A política de mesclagem usada para calcular essa métrica não é igual à política de mesclagem gerada pelo sistema usada para calcular [!UICONTROL audiências endereçáveis] no painel [!UICONTROL Uso da licença], portanto, é improvável que a contagem de audiências nos painéis [!UICONTROL Perfis] e [!UICONTROL Uso da licença] seja exatamente a mesma ...

![](../images/profiles/audience-size.png)

### [!UICONTROL Perfis adicionados] {#profiles-added}

O widget **[!UICONTROL Perfis adicionados]** exibe o número total de perfis unidos que foram adicionados ao repositório de dados do Perfil desde que o último snapshot foi realizado. Esse número é o resultado da política de mesclagem selecionada que está sendo aplicada aos dados do Perfil para unir os fragmentos do perfil e formar um único perfil para cada indivíduo.

![](../images/profiles/profiles-added.png)

### [!UICONTROL Perfis adicionados ao longo do tempo] {#profiles-added-over-time}

O widget **[!UICONTROL Perfis adicionados ao longo do tempo]** exibe o número total de perfis unidos que foram adicionados ao armazenamento de dados do Perfil diariamente nos últimos 30 dias. Esse número é atualizado todos os dias quando o instantâneo é realizado, portanto, se você ingressar perfis na Plataforma, o número de perfis não será refletido até que o próximo instantâneo seja realizado.

A contagem de perfis adicionados é o resultado da política de mesclagem selecionada ser aplicada aos dados do Perfil para unir os fragmentos do perfil e formar um único perfil para cada indivíduo.

![](../images/profiles/profiles-added-over-time.png)

### [!UICONTROL Perfis por namespace] {#profiles-by-namespace}

O widget **[!UICONTROL Perfis por namespace]** exibe o detalhamento das namespaces de identidade em todos os perfis mesclados na loja de Perfis. O número total de perfis por [!UICONTROL namespace de ID] (em outras palavras, adicionar os valores mostrados para cada namespace) pode ser maior que o número total de perfis de mesclagem, pois um perfil pode ter várias namespaces associadas a ele. Por exemplo, se um cliente interagir com sua marca em mais de um canal, várias namespaces serão associadas a esse cliente individual.

Para saber mais sobre namespaces de identidade, visite a [documentação do Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/profiles/profiles-by-namespace.png)

### [!UICONTROL sobreposição de namespace] {#namespace-overlap}

O widget **[!UICONTROL sobreposição de Namespace]** exibe um diagrama Venn, ou um diagrama de conjunto, que mostra a sobreposição de perfis na loja de Perfis que contém várias namespaces de identidade.

Depois de usar os menus suspensos no widget para selecionar as namespaces de identidade que você deseja comparar, os círculos aparecem exibindo o tamanho relativo de cada namespace, com o número de perfis contendo ambas as namespaces sendo representado pelo tamanho da sobreposição entre os círculos.

Se um cliente interagir com sua marca em mais de um canal, várias namespaces serão associadas a esse cliente individual, portanto, é provável que sua organização tenha vários perfis contendo fragmentos de mais de uma namespace de identidade.

Para saber mais sobre namespaces de identidade, visite a [documentação do Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/profiles/namespace-overlap.png)

## Próximas etapas

Ao seguir este documento, você deve agora ser capaz de localizar o painel de Perfis e entender as métricas exibidas nos widgets disponíveis. Para saber mais sobre como trabalhar com [!DNL Profile] dados na interface do usuário do Experience Platform, consulte o [Guia da interface do usuário do Perfil do cliente em tempo real](../../profile/ui/user-guide.md).