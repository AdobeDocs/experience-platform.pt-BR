---
keywords: serviço de catálogo, perguntas, perguntas frequentes, perguntas frequentes, perguntas frequentes sobre conjuntos de dados
title: Perguntas frequentes
description: Respostas às perguntas mais frequentes sobre o Adobe Experience Platform Catalog Service e conjuntos de dados.
exl-id: 70d2a352-75bd-4bbc-98e6-aeea16306f63
source-git-commit: 38f63f1fc985601c53925a529e603f47dc7fb58b
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 1%

---

# Perguntas frequentes {#faq}

Este documento fornece respostas a perguntas frequentes sobre o Serviço de catálogo e conjuntos de dados da Adobe Experience Platform. Para perguntas e soluções de problemas relacionados a outros serviços da Experience Platform, incluindo problemas encontrados em todas as APIs do Experience Platform, consulte o [guia de solução de problemas do Experience Platform](../landing/troubleshooting.md).

## Políticas e regras de retenção {#retention-policies-and-rules}

### A quais tipos de conjuntos de dados posso aplicar regras de política de retenção?

+++Resposta

Você pode configurar políticas de retenção em conjuntos de dados criados usando a classe ExperienceEvent XDM. Para o Serviço de perfil, as políticas de retenção só podem ser aplicadas aos conjuntos de dados ExperienceEvent após serem habilitados para o Perfil.

+++

### Posso definir políticas de retenção diferentes para o data lake e o serviço de perfil?

+++Resposta

>[!NOTE]
>
>O período de retenção do Serviço de perfil só pode ser atualizado uma vez a cada 30 dias.

Sim, você pode aplicar políticas de retenção diferentes para o data lake e o Serviço de perfil.

+++

## Tempo e execução do trabalho de retenção {#retention-job-execution-and-timing}

### Quando o trabalho de retenção do conjunto de dados excluirá os dados dos serviços do data lake?

+++Resposta

As expirações do conjunto de dados são avaliadas e processadas semanalmente, excluindo todos os registros que expiraram. Um evento será considerado expirado se tiver sido assimilado no Experience Platform por mais de 30 dias (data de assimilação > 30 dias) e sua data de evento exceder o período de retenção definido.

+++

### Quando o trabalho de retenção do conjunto de dados excluirá os dados dos serviços de perfil?

+++Resposta

Depois que uma política de retenção é definida, os eventos existentes são imediatamente excluídos do Experience Platform se o carimbo de data e hora do evento exceder o período de retenção. Novos eventos são excluídos assim que o carimbo de data e hora ultrapassar o período de retenção.

Por exemplo, se você aplicar uma política de expiração de 30 dias em 15 de maio, ocorre o seguinte:

- Os novos eventos recebem uma expiração de 30 dias à medida que são assimilados.
- Os eventos existentes com um carimbo de data e hora anterior a 15 de abril são excluídos imediatamente.
- Os eventos existentes com um carimbo de data e hora após 15 de abril são definidos para expirar 30 dias após seu carimbo de data e hora. Por exemplo, um evento de 18 de abril seria excluído em 18 de maio.

+++

## Uso e monitoramento do conjunto de dados

### Como posso verificar o uso do meu conjunto de dados atual?

+++Resposta

Você pode exibir o tamanho de armazenamento em nível de conjunto de dados mais recente no data lake e no Perfil como métricas separadas na página de inventário [!UICONTROL Conjuntos de dados]. Também é possível classificar as colunas para identificar os maiores conjuntos de dados e garantir que as políticas de retenção sejam aplicadas. O uso em nível de sandbox está disponível no painel Uso da licença. Consulte a [documentação de Uso da Licença](../dashboards/guides/license-usage.md) para obter detalhes.

+++

### Como posso verificar se o trabalho de retenção de dados foi bem-sucedido?

+++Resposta

Você pode verificar o carimbo de data/hora do último trabalho de retenção de dados na [Interface de configuração de retenção do conjunto de dados](./datasets/user-guide.md#data-retention-policy) e na página de inventário [!UICONTROL Conjuntos de dados]. Os relatórios para uso do conjunto de dados histórico não estão disponíveis no momento, mas estão planejados para versões futuras.

+++

## Recuperação de dados {#data-recovery}

### Posso recuperar dados excluídos?

+++Resposta

Não, uma vez aplicada a política de retenção, todos os dados anteriores ao período de retenção serão permanentemente excluídos e não poderão ser recuperados.

+++
