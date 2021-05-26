---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, interface do usuário, interface do usuário, personalização, painel de perfil, painel
title: Painel de perfis
description: A Adobe Experience Platform fornece um painel pelo qual você pode visualizar informações importantes sobre os dados do Perfil do cliente em tempo real da sua organização.
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: 36aaccddeb207e22a22d5124ec8592ac8dddf8bc
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 0%

---

#  Painel de perfis

A interface do usuário do Adobe Experience Platform (UI) fornece um painel pelo qual você pode visualizar informações importantes sobre seus dados [!DNL Real-time Customer Profile], conforme capturados durante um instantâneo diário. Este guia descreve como acessar e trabalhar com o painel [!UICONTROL Perfis] na interface do usuário e fornece informações sobre as métricas exibidas no painel.

Para obter uma visão geral de todos os recursos de Perfil na interface do usuário do Experience Platform, visite o [Guia da interface do usuário de perfil do cliente em tempo real](../../profile/ui/user-guide.md).

## Dados do painel de perfis

O painel [!UICONTROL Profiles] exibe um instantâneo dos dados do atributo (registro) que sua organização tem no armazenamento de Perfis no Experience Platform. O instantâneo não inclui nenhum dado de evento (série de tempo).

Os dados do atributo no instantâneo mostram os dados exatamente como aparecem no momento específico em que o instantâneo foi tirado. Em outras palavras, o instantâneo não é uma aproximação ou amostra dos dados, e o painel de Perfil não está sendo atualizado em tempo real.

>[!NOTE]
>
>Quaisquer alterações ou atualizações feitas nos dados desde que o instantâneo foi tirado não serão refletidas no painel até que o próximo instantâneo seja tirado.

## Explorar o painel [!UICONTROL Perfis]

Para navegar até o painel [!UICONTROL Profiles] na interface do usuário da plataforma, selecione **[!UICONTROL Profiles]** no painel esquerdo e selecione a guia **[!UICONTROL Overview]** para exibir o painel.

![](../images/profiles/dashboard-overview.png)

### Modificar o painel [!UICONTROL Perfis]

Você pode modificar a aparência do painel [!UICONTROL Profiles] selecionando **[!UICONTROL Modificar painel]**. Isso permite mover, adicionar e remover widgets do painel, bem como acessar a [!UICONTROL biblioteca de widgets] para explorar os widgets disponíveis e criar widgets personalizados para sua organização.

Consulte a documentação [modificando painéis](../modify.md) e [biblioteca de widgets](../widget-library.md) para saber mais.

## Mesclar políticas

As métricas exibidas no painel [!UICONTROL Profiles] são baseadas em políticas de mesclagem aplicadas aos dados do Perfil do cliente em tempo real. Quando os dados são reunidos de várias fontes para criar o perfil do cliente, é possível que os dados contenham valores conflitantes (por exemplo, um conjunto de dados pode listar um cliente como &quot;único&quot;, enquanto outro conjunto de dados pode listá-lo como &quot;casado&quot;). É tarefa da política de mesclagem determinar quais dados priorizar e exibir como parte do perfil.

Para obter mais informações sobre políticas de mesclagem, incluindo como criar, editar e declarar uma política de mesclagem padrão para sua organização, comece lendo a [visão geral das políticas de mesclagem](../../profile/merge-policies/overview.md).

O painel selecionará automaticamente uma política de mesclagem a ser exibida, mas você poderá alterar a política de mesclagem selecionada usando o menu suspenso. Para escolher uma política de mesclagem diferente, selecione o menu suspenso ao lado do nome da política de mesclagem e selecione a política de mesclagem que deseja exibir.

>[!NOTE]
>
>O menu suspenso mostra apenas as políticas de mesclagem relacionadas à Classe de Perfil Individual XDM. No entanto, se sua organização tiver criado várias políticas de mesclagem, pode significar que você precisará rolar para exibir a lista completa das políticas de mesclagem disponíveis.

![](../images/profiles/select-merge-policy.png)

## Widgets e métricas

O painel é composto de widgets, que são métricas somente leitura, fornecendo informações importantes sobre os dados do perfil.

A data e a hora da &quot;última atualização&quot; em um widget mostram quando o último instantâneo dos dados foi tirado. A data e a hora do instantâneo são fornecidas em UTC; não está no fuso horário do usuário individual ou da Organização IMS.

## Widgets disponíveis

O Experience Platform fornece vários widgets que você pode usar para visualizar métricas diferentes relacionadas aos dados do seu perfil. Selecione o nome de um widget abaixo para saber mais:

* [[!UICONTROL Contagem de perfis]](#profile-count)
* [[!UICONTROL Perfis adicionados]](#profiles-added)
* [[!UICONTROL Tendência da contagem de perfis]](#profiles-count-trend)
* [[!UICONTROL Perfis por identidade]](#profiles-by-identity)
* [[!UICONTROL Sobreposição de identidade]](#identity-overlap)

### [!UICONTROL Contagem de perfis] {#profile-count}

O widget **[!UICONTROL Profile count]** exibe o número total de perfis mesclados no armazenamento de dados do perfil no momento em que o instantâneo foi tirado. Esse número é o resultado da política de mesclagem selecionada ser aplicada aos dados do Perfil para unir fragmentos de perfil para formar um único perfil para cada indivíduo.

Para obter mais informações sobre fragmentos e perfis mesclados, comece lendo a seção *Perfil de fragmentos vs perfis mesclados* da [Visão geral do perfil do cliente em tempo real](../../profile/home.md).

![](../images/profiles/profile-count.png)

### [!UICONTROL Perfis adicionados] {#profiles-added}

O widget **[!UICONTROL Perfis adicionados]** exibe o número total de perfis mesclados que foram adicionados ao armazenamento de dados do Perfil a partir do último instantâneo tirado. Esse número é o resultado da política de mesclagem selecionada ser aplicada aos dados do Perfil para unir fragmentos de perfil para formar um único perfil para cada indivíduo.

Você pode usar o seletor suspenso para exibir os perfis adicionados nos últimos 30 dias, 90 dias ou 12 meses.

![](../images/profiles/profiles-added.png)

### [!UICONTROL Tendência da contagem de perfis] {#profiles-count-trend}

O widget **[!UICONTROL Profiles count tend]** exibe o número total de perfis mesclados que foram adicionados ao armazenamento de dados do perfil diariamente nos últimos 30 dias, 90 dias ou 12 meses. Esse número é atualizado todos os dias quando o instantâneo é tirado. Portanto, se você assimilasse perfis na Platform, o número de perfis não seria refletido até que o próximo instantâneo fosse tirado.

A contagem de perfis adicionada é o resultado da política de mesclagem selecionada ser aplicada aos dados do perfil para unir fragmentos de perfil para formar um único perfil para cada indivíduo.

![](../images/profiles/profile-count-trend.png)

### [!UICONTROL Perfis por identidade] {#profiles-by-identity}

O widget **[!UICONTROL Perfis por identidade]** exibe o detalhamento das identidades em todos os perfis mesclados no armazenamento de Perfis. O número total de perfis por identidade (em outras palavras, adicionar os valores mostrados para cada namespace) pode ser maior que o número total de perfis mesclados, pois um perfil pode ter vários namespaces associados a ele. Por exemplo, se um cliente interagir com sua marca em mais de um canal, vários namespaces serão associados a esse cliente individual.

Para saber mais sobre identidades, visite a [documentação do Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/profiles/profiles-by-identity.png)

### [!UICONTROL Sobreposição de identidade] {#identity-overlap}

O widget **[!UICONTROL Sobreposição de identidade]** exibe um diagrama Venn ou um diagrama de conjunto, mostrando a sobreposição de perfis em seu armazenamento de perfil que contém várias identidades.

Depois de usar os menus suspensos no widget para selecionar as identidades que deseja comparar, os círculos aparecem exibindo o tamanho relativo de cada identidade, com o número de perfis contendo ambos os namespaces sendo representado pelo tamanho da sobreposição entre os círculos.

Se um cliente interagir com sua marca em mais de um canal, várias identidades serão associadas a esse cliente individual, portanto, é provável que sua organização tenha vários perfis contendo fragmentos de mais de uma identidade.

Para saber mais sobre identidades, visite a [documentação do Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/profiles/identity-overlap.png)

## Próximas etapas

Agora, ao seguir este documento, você pode localizar o painel Perfis e entender as métricas exibidas nos widgets disponíveis. Para saber mais sobre como trabalhar com dados [!DNL Profile] na interface do usuário do Experience Platform, consulte o [Guia da interface do usuário do perfil do cliente em tempo real](../../profile/ui/user-guide.md).
