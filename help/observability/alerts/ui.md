---
keywords: Experience Platform;página inicial;tópicos populares;intervalo de datas
title: Guia da interface de alertas
description: Saiba como gerenciar alertas na interface do usuário do Experience Platform.
feature: Alerts
exl-id: 4ba3ef2b-7394-405e-979d-0e5e1fe676f3
source-git-commit: ed18ecea98497e0c20d44617436a013bf83b69d2
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# Guia da interface de alertas

A interface do usuário do Adobe Experience Platform permite visualizar um histórico de alertas recebidos com base em métricas reveladas pelos Adobe Experience Platform Observability Insights. A interface também permite exibir, ativar, desativar e assinar as regras de alerta disponíveis.

>[!NOTE]
>
>Para obter uma introdução aos alertas no Experience Platform, consulte [visão geral dos alertas](./overview.md).

Para começar, selecione **[!UICONTROL Alertas]** no painel de navegação esquerdo.

![](../images/alerts/ui/workspace.png)

## Gerenciar regras de alerta

A variável **[!UICONTROL Procurar]** A guia lista as regras disponíveis que podem acionar um alerta.

![](../images/alerts/ui/rules.png)

Selecione uma regra na lista para exibir sua descrição e seus parâmetros de configuração no painel direito, incluindo limite e severidade.

![](../images/alerts/ui/rule-details.png)

Selecione as reticências (**..**) ao lado do nome de uma regra, e uma lista suspensa exibe controles para ativar ou desativar o alerta (dependendo de seu status atual) e para assinar ou cancelar a assinatura de notificações por email para o alerta.

![](../images/alerts/ui/disable-subscribe.png)

## Ativar alertas de email

As notificações de alerta podem ser enviadas diretamente ao seu email.

Selecione o ícone de sino (![ícone de sino](../images/alerts/ui/bell-icon.png)) localizado na faixa superior à direita para exibir notificações e anúncios. Na lista suspensa exibida, selecione o ícone de engrenagem (![ícone cog](../images/alerts/ui/cog-icon.png)) para acessar a página de preferências de Experience Cloud.

![](../images/alerts/ui/edit-preferences.png)

A variável **Perfil** é exibida. Selecione o **[!UICONTROL Notificação]** na navegação à esquerda para acessar as preferências de alertas de email.

![](../images/alerts/ui/profile.png)

Role para a **Emails** na parte inferior da página e selecione **[!UICONTROL Notificações instantâneas]**

![](../images/alerts/ui/notifications.png)

Todos os alertas que você assina agora serão entregues no endereço de email que está conectado à sua conta da Adobe ID.

## Exibir histórico de alertas

A variável **[!UICONTROL Histórico]** A guia mostra o histórico de alertas recebidos para sua organização, incluindo a regra que acionou o alerta, a data de acionamento e a data de resolução (se aplicável).

![](../images/alerts/ui/history.png)

Selecione um alerta listado e mais detalhes serão exibidos no painel direito, incluindo um breve resumo do evento que acionou o alerta.

![](../images/alerts/ui/history-details.png)

## Próximas etapas

Este documento forneceu uma visão geral sobre como visualizar e gerenciar alertas na interface do usuário da Platform. Consulte a visão geral em [Insights de capacidade de observação](../home.md) para obter mais informações sobre os recursos do serviço.
