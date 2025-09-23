---
keywords: Experience Platform;página inicial;tópicos populares;intervalo de datas
title: Guia da interface de alertas
description: Saiba como gerenciar alertas na interface do usuário do Experience Platform.
feature: Alerts
exl-id: 4ba3ef2b-7394-405e-979d-0e5e1fe676f3
source-git-commit: 57261ca37bf10e394f47ea4bb3c01856a18b197d
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 5%

---

# Guia da interface de alertas

A interface do usuário do Adobe Experience Platform permite visualizar um histórico de alertas recebidos com base em métricas reveladas pelos Adobe Experience Platform Observability Insights. A interface também permite exibir, ativar, desativar e assinar as regras de alerta disponíveis.

>[!NOTE]
>
>Para obter uma introdução aos alertas no Experience Platform, consulte a [visão geral dos alertas](./overview.md).

Para começar, selecione **[!UICONTROL Alertas]** na navegação à esquerda.

![Página de Alertas destacando [!UICONTROL Alertas] na navegação à esquerda.](../images/alerts/ui/workspace.png)

## Gerenciar regras de alerta {#manage-rules}

A guia **[!UICONTROL Procurar]** lista as regras disponíveis que podem disparar um alerta.

![Uma lista de alertas disponíveis é exibida na guia [!UICONTROL Procurar].](../images/alerts/ui/rules.png)

Selecione uma regra na lista para exibir sua descrição e seus parâmetros de configuração no painel direito, incluindo limite e severidade.

![Uma regra de alerta foi destacada mostrando detalhes no painel direito.](../images/alerts/ui/rule-details.png)

Selecione as reticências (**...**) ao lado do nome de uma regra e uma lista suspensa exibe controles para habilitar ou desabilitar o alerta (dependendo de seu status atual) e para assinar ou cancelar a assinatura de notificações por email para o alerta.

![As reticências selecionadas revelam o menu suspenso.](../images/alerts/ui/disable-subscribe.png)

## Gerenciar inscrições nos alertas {#manage-subscribers}

>[!NOTE]
>
> Para atribuir um alerta a uma ID de usuário do Adobe, um endereço de email externo ou uma lista de grupo de email, você deve ser um administrador.

A guia **[!UICONTROL Procurar]** lista as regras disponíveis que podem disparar um alerta.

![Uma lista de regras de alerta disponíveis mostrada na guia [!UICONTROL Procurar].](../images/alerts/ui/rules.png)

Selecione as reticências (**...**) ao lado do nome de uma regra, uma lista suspensa exibe controles. Selecione **[!UICONTROL Gerenciar assinantes de alertas]**.

![Selecione as reticências para exibir o menu suspenso. A opção [!UICONTROL Gerenciar assinantes de alerta] está realçada.](../images/alerts/ui/manage-alert-subscribers.png)

A página [!UICONTROL Gerenciar assinantes de alerta] é exibida. Para atribuir notificações a usuários específicos, digite a ID de usuário da Adobe, o endereço de email externo ou uma lista de grupo de email e pressione Enter.

>[!NOTE]
>
>Para enviar este aviso a vários usuários de uma só vez, forneça uma lista de IDs de usuário ou endereços de email separados por vírgulas.

![A página Gerenciar assinantes de alertas mostra os endereços de email inseridos.](../images/alerts/ui/manage-alert-add-email.png)

Os endereços de email são exibidos na lista de assinantes atuais listados. Selecione **[!UICONTROL Atualizar]**.

![A página Gerenciar assinantes de alerta que destaca os assinantes e [!UICONTROL Atualização].](../images/alerts/ui/manage-alert-subscribers-added-email.png)

Você adicionou usuários com sucesso à sua lista de notificações de alerta. Os usuários enviados agora receberão notificações por email sobre esse alerta, como pode ser visto na imagem abaixo.

![Um exemplo de email da notificação de alerta recebida.](../images/alerts/ui/manage-alert-subscribers-email.png)

## Ativar alertas de email {#enable-email}

As notificações de alerta podem ser enviadas diretamente ao seu email.

Selecione o ícone de sino (![ícone de sino](/help/images/icons/bell.png)) localizado na faixa superior à direita para exibir notificações e anúncios. Na lista suspensa exibida, selecione o ícone de engrenagem (![ícone de engrenagem](/help/images/icons/settings.png)) para acessar a página de preferências do Experience Cloud.

![Uma lista de alertas mostrados destacando o ícone de sino e o ícone de engrenagem.](../images/alerts/ui/edit-preferences.png)

A página **Perfil** é exibida. Selecione as **[!UICONTROL Notificações]** na navegação à esquerda para acessar as preferências de alertas de email.

![A página Perfil destacando [!UICONTROL Notificações] na navegação à esquerda.](../images/alerts/ui/profile.png)

Role até a seção **Emails** na parte inferior da página e selecione **[!UICONTROL Notificações instantâneas]**

![A seção Emails realçada na página Perfil.](../images/alerts/ui/notifications.png)

Todos os alertas que você assina agora serão entregues no endereço de email que está conectado à sua conta da Adobe ID.

## Personalizar limite de alerta {#alert-threshold}

Os limites de alerta podem ser personalizados para os seguintes tipos de alerta:

| Tipo de alerta | Parâmetro personalizado |
|---|---|
| Atraso na tarefa do segmento | Limite de atraso |
| Atraso na exportação do segmento | Limite de atraso |
| Atraso na execução do fluxo de destino | Limite de atraso |
| Atraso na execução do fluxo do serviço de identidade | Limite de atraso |
| Atraso na execução do fluxo de perfil | Limite de atraso |
| Taxa de falhas de assimilação de transmissão de perfis excedida | Limite de erro |
| Taxa de Ignorar Assimilação de Streaming de Perfil Excedida | Limite de erro |
| Atraso na execução do fluxo de fontes | Limite de atraso |
| Taxa de erro de assimilação de origens excedida | Limite de erro |
| Atraso da execução da consulta | Limite de atraso |
| Taxa de Ignorar Ativação Excedida | Limite de erro |

Selecione as reticências (**...**) ao lado do nome de uma regra, uma lista suspensa exibe controles. Selecione **[!UICONTROL Editar]**.

![A opção [!UICONTROL Editar] está realçada para a regra selecionada.](../images/alerts/ui/threshold-edit.png)

A página **[!UICONTROL Personalizar alerta]** é exibida. Atualize o limite para os minutos desejados e selecione **[!UICONTROL Confirmar]**.

![As opções Personalizar página de alerta destacando [!UICONTROL Limite] e [!UICONTROL Confirmar].](../images/alerts/ui/threshold-update.png)

Você retornou à página **[!UICONTROL Alertas]**. Para exibir as configurações de limite para o alerta, selecione a regra na lista. Você pode ver as configurações de limite para o alerta no painel direito, incluindo detalhes como status e gravidade.

![Um alerta realçado mostrando detalhes no painel direito e destacando o [!UICONTROL Limite].](../images/alerts/ui/threshold-view.png)

## Exibir histórico de alertas {#alert-history}

A guia **[!UICONTROL Histórico]** mostra o histórico de alertas recebidos para sua organização, incluindo a regra que acionou o alerta, a data de disparo e a data de resolução (se aplicável).

![Uma lista de alertas recebidos é exibida na guia [!UICONTROL Histórico].](../images/alerts/ui/history.png)

Selecione um alerta listado e mais detalhes serão exibidos no painel direito, incluindo um breve resumo do evento que acionou o alerta.

![Um alerta realçado mostrando detalhes no painel direito.](../images/alerts/ui/history-details.png)

## Próximas etapas

Este documento forneceu uma visão geral sobre como visualizar e gerenciar alertas na interface do usuário do Experience Platform. Consulte a visão geral em [Insights de capacidade de observação](../home.md) para obter mais informações sobre os recursos do serviço.
