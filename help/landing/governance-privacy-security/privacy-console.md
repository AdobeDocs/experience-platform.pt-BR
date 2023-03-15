---
title: Visão geral do console de privacidade
description: Saiba como monitorar seus fluxos de trabalho relacionados à privacidade na interface do usuário do Adobe Experience Platform.
source-git-commit: 1fac36a0fd767add92283cd256d8bcea783ecf3b
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 3%

---

# Visão geral do Console de privacidade

A variável [!UICONTROL Console de privacidade] guia A interface do usuário do Adobe Experience Platform fornece uma visualização de painel das operações relacionadas à privacidade na Platform, incluindo ordens de trabalho da Higiene de dados, solicitações de titulares de dados do Privacy Service e logs de auditoria das atividades de usuário da Platform.

Para acessar o painel, selecione **[!UICONTROL Console de privacidade]** no painel de navegação esquerdo.

![Imagem mostrando [!UICONTROL Console de privacidade] sendo selecionado na navegação à esquerda na interface do usuário da Platform](../images/governance-privacy-security/privacy-console/left-nav.png)

Aqui, você pode revisar as [widgets de monitoramento](#widgets) fornecido pelo console, ou você pode explorar um dos vários [guias de casos de uso](#use-case-guides) nos recursos de privacidade da Platform.

## Widgets

[!UICONTROL Console de privacidade] O fornece vários widgets para ajudar a monitorar as operações de privacidade.

![Imagem mostrando [!UICONTROL Console de privacidade] sendo selecionado na navegação à esquerda na interface do usuário da Platform](../images/governance-privacy-security/privacy-console/widgets.png)

>[!NOTE]
>
>Dependendo dos SKUs que sua organização adquiriu, alguns dos widgets mencionados abaixo podem não estar disponíveis.

A função de cada widget é explicada abaixo:

| Nome do widget | Descrição |
| --- | --- |
| Status da ordem de trabalho de higiene de dados | Mostra os status dos processos de exclusão de registro em [Higiene de dados](../../hygiene/home.md) para o período selecionado. Use o menu suspenso para alterar o período entre os últimos 7 dias, 14 dias e 30 dias. |
| Ordens de trabalho recentes de higiene de dados | Mostra os mais recentes [Higiene de dados](../../hygiene/home.md) ordens de serviço sendo processadas pelo sistema. Use a lista suspensa para alternar entre ordens de serviço criadas recentemente e ordens de serviço atualizadas recentemente. |
| Ações mais frequentes | Mostra as ações mais frequentes na Platform conforme capturadas pelo [logs de auditoria](./audit-logs/overview.md) para o período selecionado. Use o menu suspenso para alterar o período entre os últimos 7 dias, 14 dias e 30 dias. |
| Usuários mais ativos | Mostra os usuários mais ativos da Platform em sua organização, conforme capturados pelo [logs de auditoria](./audit-logs/overview.md) para o período selecionado. Use o menu suspenso para alterar o período entre os últimos 7 dias, 14 dias e 30 dias. |
| Solicitações do titular dos dados | Mostra o número de solicitações do titular de dados enviadas e concluídas por [Privacy Service](../../privacy-service/home.md) para um determinado dia. |

{style="table-layout:auto"}

## Guias de caso de uso

O console fornece vários guias no produto que apresentam fluxos de trabalho comuns de privacidade na Platform, incluindo instruções concisas sobre como configurar uma implementação básica.

![Imagem mostrando [!UICONTROL Console de privacidade] sendo selecionado na navegação à esquerda na interface do usuário da Platform](../images/governance-privacy-security/privacy-console/use-case-guide.png)

## Próximas etapas

Para obter mais informações sobre os vários serviços da Platform que se vinculam aos casos de uso de privacidade, consulte a seguinte documentação:

* [Controle de acesso baseado em atributos](../../access-control/abac/overview.md)
* [Logs de auditoria](./audit-logs/overview.md)
* [Governança de dados](../../data-governance/home.md)
* [Higiene de dados](../../hygiene/home.md)
* [Privacy Service](../../privacy-service/home.md)
