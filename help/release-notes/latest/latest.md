---
title: Notas da versão de fevereiro de 2026 da Adobe Experience Platform
description: Notas da versão de fevereiro de 2026 da Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: a11c00c218ffbbd5618616f401613a604c35859a
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 32%

---

# Notas de versão da Adobe Experience Platform

>[!TIP]
>
>Consulte a documentação a seguir para obter as notas de versão de outros aplicativos da Adobe Experience Platform:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/releases/latest)
>- [Composição de público-alvo federado](https://experienceleague.adobe.com/pt-br/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/pt-br/docs/real-time-cdp-collaboration/using/latest)

**Data de lançamento: quarta-feira, 17 de fevereiro de 2026**

Novos recursos e atualizações dos recursos existentes no Adobe Experience Platform:

- [Alertas](#alerts)
- [Destinos](#destinations)
- [Fontes](#sources)
- [Experience Data Model (XDM)](#xdm)

## Alertas {#alerts}

O Experience Platform permite assinar alertas baseados em eventos para várias atividades do Experience Platform. Você pode assinar diferentes regras de alerta por meio da guia [!UICONTROL Alerts] na interface do usuário do Experience Platform e pode optar por receber mensagens de alerta na própria interface do usuário ou por notificações de email.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Integração do [!DNL Slack] para alertas voltados para o cliente | Agora você pode enviar alertas voltados para o cliente para [!DNL Slack]. Siga o [tutorial passo a passo](../../observability/alerts/slack-integration.md) para configurar a integração do [!DNL Slack] e receber notificações de alerta diretamente no espaço de trabalho [!DNL Slack]. |

{style="table-layout:auto"}

Para obter mais informações, leia a visão geral[&#128279;](../../observability/home.md) do [!DNL Observability Insights] .

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Destinos novos ou atualizados**

| Destino | Descrição |
| --- | --- |
| [[!DNL Snowflake] Lote](../../destinations/catalog/warehouses/snowflake-batch.md) geralmente disponível | O destino em lote [!DNL Snowflake] agora está disponível. Os clientes da Real-Time CDP em todo o mundo agora podem usar esse conector para ativar dados em suas contas da Snowflake sem precisar copiar fisicamente os dados. Todas as limitações da versão limitada foram levantadas (disponibilidade para clientes somente dos EUA, suporte para públicos pertencentes somente à política de mesclagem padrão). |

{style="table-layout:auto"}

**Correções e melhorias**

| Correção | Descrição |
| --- | --- |
| Alerta de Taxa de Falha de Ativação Excedida | O alerta de destino Taxa de falha de ativação excedida agora usa corretamente o limite que você configura ao avaliar e enviar o alerta. Anteriormente, o alerta era disparado em uma taxa de falha de 1%, independentemente da porcentagem configurada. Consulte [regras de alerta padrão](../../observability/alerts/rules.md#destinations) para obter mais detalhes sobre este alerta. |
| Relatórios de identidades excluídas da Correspondência de clientes do Google | Correção de um bug na lógica de contagem de registros ignorados que fazia com que as contagens infladas de perfis excluídos fossem exibidas para os destinos de Correspondência de clientes do Google. O comportamento de ativação e exportação não foi afetado; somente os números relatados estavam incorretos. |

{style="table-layout:auto"}

Para obter mais informações, leia a [Visão geral dos Destinos](../../destinations/home.md).

## Fontes {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de ingestão e gerenciar a taxa de transferência de ingestão de dados.

**Fontes novas ou atualizadas**

| Fonte | Descrição |
| --- | --- |
| Suporte ao Catálogo de Unity no conector de origem [!DNL Databricks] | O conector de origem [!DNL Databricks] agora dá suporte ao Catálogo de Unidade. Leia a documentação atualizada do [[!DNL Databricks]](../../sources/connectors/databases/databricks.md) para saber como usar o Catálogo do Unity ao configurar sua conexão de origem. |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral de fontes](../../sources/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Experience Platform. Ao aderir aos padrões do XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

| Recurso | Descrição |
| --- | --- |
| Edição restrita para esquemas com conjuntos de dados | A edição de operações que resultam em alterações de quebra agora é restrita assim que um conjunto de dados existe para um esquema. Quando um conjunto de dados é associado, não é mais possível renomear ou excluir campos, alterar tipos ou formatos de dados de campo, modificar descritores de identidade, gerenciar campos relacionados para remover campos existentes ou alterar a classe atribuída; alterações aditivas e reprovação de campo permanecem compatíveis. |

Para obter mais informações, leia a [visão geral do XDM](../../xdm/home.md).

