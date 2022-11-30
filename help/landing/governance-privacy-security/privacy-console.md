---
title: Visão geral do console de privacidade
description: Saiba como monitorar seus fluxos de trabalho relacionados à privacidade na interface do usuário do Adobe Experience Platform.
source-git-commit: 1fac36a0fd767add92283cd256d8bcea783ecf3b
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 4%

---

# Visão geral do console Privacidade

O [!UICONTROL Console de privacidade] A guia da interface do usuário do Adobe Experience Platform fornece uma exibição de painel de suas operações relacionadas à privacidade no Platform, incluindo pedidos de trabalho de Higiene de dados, solicitações de titular de dados do Privacy Service e logs de auditoria para atividades de usuário do Platform.

Para acessar o painel, selecione **[!UICONTROL Console de privacidade]** no painel de navegação esquerdo.

![Imagem mostrando [!UICONTROL Console de privacidade] ser selecionado na navegação à esquerda na interface do usuário da plataforma](../images/governance-privacy-security/privacy-console/left-nav.png)

A partir daqui, você pode revisar as [widgets de monitoramento](#widgets) fornecido pelo console ou você pode explorar um dos vários [guias de caso de uso](#use-case-guides) sobre os recursos de privacidade da Platform.

## Widgets

[!UICONTROL Console de privacidade] O fornece vários widgets para ajudar a monitorar suas operações de privacidade.

![Imagem mostrando [!UICONTROL Console de privacidade] ser selecionado na navegação à esquerda na interface do usuário da plataforma](../images/governance-privacy-security/privacy-console/widgets.png)

>[!NOTE]
>
>Dependendo dos SKUs que sua organização adquiriu, alguns dos widgets mencionados abaixo podem não estar disponíveis.

A função de cada widget é explicada abaixo:

| Nome do widget | Descrição |
| --- | --- |
| Status da ordem da higiene de dados | Mostra os status dos processos de exclusão de registro em [Higiene de dados](../../hygiene/home.md) para o período de tempo selecionado. Use o menu suspenso para alterar o período entre os últimos 7 dias, 14 dias e 30 dias. |
| Recentes pedidos de higiene de dados | Mostra o mais recente [Higiene de dados](../../hygiene/home.md) ordens de serviço sendo processadas pelo sistema. Use a lista suspensa para alternar entre ordens de serviço criadas recentemente e ordens de serviço atualizadas recentemente. |
| Ações mais frequentes | Mostra as ações mais frequentes no Platform capturadas por [logs de auditoria](./audit-logs/overview.md) para o período de tempo selecionado. Use o menu suspenso para alterar o período entre os últimos 7 dias, 14 dias e 30 dias. |
| Usuários mais ativos | Mostra os usuários mais ativos da Plataforma em sua organização, capturados pelo [logs de auditoria](./audit-logs/overview.md) para o período de tempo selecionado. Use o menu suspenso para alterar o período entre os últimos 7 dias, 14 dias e 30 dias. |
| Solicitações do titular dos dados | Mostra o número de solicitações do titular de dados enviadas e concluídas por [Privacy Service](../../privacy-service/home.md) para um determinado dia. |

{style=&quot;table-layout:auto&quot;}

## Guias de caso de uso

O console fornece vários guias no produto que apresentam a você fluxos de trabalho de privacidade comuns na Platform, incluindo instruções concisas sobre como configurar uma implementação básica.

![Imagem mostrando [!UICONTROL Console de privacidade] ser selecionado na navegação à esquerda na interface do usuário da plataforma](../images/governance-privacy-security/privacy-console/use-case-guide.png)

## Próximas etapas

Para obter mais informações sobre os vários serviços da plataforma que se vinculam a casos de uso de privacidade, consulte a seguinte documentação:

* [Controle de acesso baseado em atributos](../../access-control/abac/overview.md)
* [Logs de auditoria](./audit-logs/overview.md)
* [Governança de dados](../../data-governance/home.md)
* [Higiene de dados](../../hygiene/home.md)
* [Privacy Service](../../privacy-service/home.md)
