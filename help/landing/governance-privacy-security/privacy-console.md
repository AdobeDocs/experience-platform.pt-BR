---
title: Visão geral do console de privacidade
description: Saiba como monitorar seus fluxos de trabalho relacionados à privacidade na interface do usuário do Adobe Experience Platform.
feature: Privacy
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 4%

---

# Visão geral do Console de privacidade

A guia [!UICONTROL Console de privacidade] da interface do usuário do Adobe Experience Platform fornece uma exibição de painel das operações relacionadas à privacidade na Platform, incluindo ordens de trabalho de Higiene de dados, solicitações de titulares de dados do Privacy Service e logs de auditoria das atividades de usuário da Platform.

Para acessar o painel, selecione **[!UICONTROL Console de privacidade]** na navegação à esquerda.

![Imagem mostrando o [!UICONTROL Console de Privacidade] sendo selecionado na navegação à esquerda na interface do usuário da plataforma](../images/governance-privacy-security/privacy-console/left-nav.png)

Aqui, você pode revisar os [widgets de monitoramento](#widgets) disponíveis fornecidos pelo console ou explorar um dos vários [guias de caso de uso](#use-case-guides) sobre os recursos de privacidade da Platform.

## Widgets

O [!UICONTROL Console de Privacidade] fornece vários widgets para ajudar a monitorar suas operações de privacidade.

![Imagem mostrando o [!UICONTROL Console de Privacidade] sendo selecionado na navegação à esquerda na interface do usuário da plataforma](../images/governance-privacy-security/privacy-console/widgets.png)

>[!NOTE]
>
>Dependendo dos SKUs que sua organização adquiriu, alguns dos widgets mencionados abaixo podem não estar disponíveis.

A função de cada widget é explicada abaixo:

| Nome do widget | Descrição |
| --- | --- |
| Status da ordem de trabalho de higiene de dados | Mostra os status dos processos de exclusão de registros em [Higiene de Dados](../../hygiene/home.md) para o período selecionado. Use o menu suspenso para alterar o período entre os últimos 7 dias, 14 dias e 30 dias. |
| Ordens de trabalho recentes de higiene de dados | Mostra as ordens de trabalho da [Higiene de Dados](../../hygiene/home.md) mais recentes que estão sendo processadas pelo sistema. Use a lista suspensa para alternar entre ordens de serviço criadas recentemente e ordens de serviço atualizadas recentemente. |
| Ações mais frequentes | Mostra as ações mais frequentes na Platform capturadas pelos [logs de auditoria](./audit-logs/overview.md) para o período selecionado. Use o menu suspenso para alterar o período entre os últimos 7 dias, 14 dias e 30 dias. |
| Usuários mais ativos | Mostra os usuários mais ativos da Platform em sua organização, conforme capturados pelos [logs de auditoria](./audit-logs/overview.md) para o período selecionado. Use o menu suspenso para alterar o período entre os últimos 7 dias, 14 dias e 30 dias. |
| Solicitações do titular dos dados | Mostra o número de solicitações de titulares de dados enviadas e concluídas por [Privacy Service](../../privacy-service/home.md) em um determinado dia. |

{style="table-layout:auto"}

## Guias de caso de uso

O console fornece vários guias no produto que apresentam fluxos de trabalho comuns de privacidade na Platform, incluindo instruções concisas sobre como configurar uma implementação básica.

![Imagem mostrando o [!UICONTROL Console de Privacidade] sendo selecionado na navegação à esquerda na interface do usuário da plataforma](../images/governance-privacy-security/privacy-console/use-case-guide.png)

## Próximas etapas

Para obter mais informações sobre os vários serviços da Platform que se vinculam aos casos de uso de privacidade, consulte a seguinte documentação:

* [Controle de acesso baseado em atributos](../../access-control/abac/overview.md)
* [Logs de auditoria](./audit-logs/overview.md)
* [Governança de dados](../../data-governance/home.md)
* [Higiene de dados](../../hygiene/home.md)
* [Privacy Service](../../privacy-service/home.md)
