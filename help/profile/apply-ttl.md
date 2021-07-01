---
keywords: Experience Platform; home; tópicos populares; conjunto de dados; conjunto de dados; tempo de vida; ttl; tempo de vida;
solution: Experience Platform
title: Tempo de vida útil em conjuntos de dados
description: Este documento fornece orientação geral sobre TTL (time-to-live) para conjuntos de dados no armazenamento de perfil da Adobe Experience Platform.
source-git-commit: 878c04c688268f8cf1850c3e8d40f958a6d2d69b
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---


# TTL (Tempo de vida útil) do Serviço de perfil

O Serviço de perfil permite que os usuários apliquem o TTL (time-to-live) aos dados na Loja de perfis. O TTL é um mecanismo que limita a quantidade de tempo em que os dados vivem em um conjunto de dados. Isso permite remover automaticamente os dados da Loja de perfis que não são mais úteis para seus casos de uso.

No momento, o perfil é compatível somente com o TTL do evento da experiência.

## TTL do evento de experiência

O TTL de eventos de experiência permite aplicar o TTL em conjuntos de dados habilitados para o perfil do cliente em tempo real para remover dados do armazenamento de perfis que não é mais válido.

>[!NOTE]
>
>Você precisará entrar em contato com o suporte para ativar o TTL do Evento de experiência em seus conjuntos de dados.

Depois de habilitar o TTL do evento de experiência em um conjunto de dados habilitado para perfil, a Platform aplicará automaticamente o valor de expiração do TTL nos dados do evento de experiência em um processo de duas etapas:

1. Todos os novos dados assimilados no conjunto de dados terão o valor de expiração de TTL aplicado no momento da assimilação.
2. Todos os dados existentes no conjunto de dados terão o valor de expiração de TTL aplicado retroativamente como uma tarefa de sistema de preenchimento retroativo única. Depois que o valor de expiração do TTL for colocado no conjunto de dados, os eventos mais antigos que o valor de expiração do TTL serão descartados imediatamente assim que o trabalho do sistema for executado. Todos os outros eventos serão descartados assim que atingirem seus valores de expiração de TTL no carimbo de data e hora do evento.

>[!NOTE]
>
>Depois que o TTL for aplicado, todos os dados anteriores ao número de dias do TTL serão **excluídos permanentemente** e não poderão ser restaurados.
> 
>Além disso, verifique se a janela de lookback do segmento está dentro do limite TTL. Caso contrário, os resultados do segmento podem ficar incorretos após a aplicação do TTL. Assim, por exemplo, se você aplicasse um TTL de 30 dias e tivesse um segmento que tentasse exibir dados de até 45 dias atrás, o segmento produziria Perfis incorretos.
> 
>Como resultado, você deve manter o mesmo TTL para todos os conjuntos de dados, se possível, para evitar o impacto de diferentes valores de TTL em diferentes conjuntos de dados na lógica de segmentação.

Assim, por exemplo, se você aplicasse um valor TTL de 30 dias em 15 de maio, as seguintes etapas ocorriam:

1. Todos os novos eventos receberão um valor TTL de 30 dias, quando for assimilado.
2. Todos os eventos existentes com um carimbo de data e hora anterior a 15 de abril serão imediatamente excluídos com o trabalho do sistema.
3. Todos os eventos existentes que têm um carimbo de data e hora que é mais recente que 15 de abril terão um valor de expiração de TTL 30 dias após o carimbo de data e hora do evento. Portanto, se um evento tiver um carimbo de data e hora de 18 de abril, ele será excluído trinta dias após a data desse carimbo de data e hora, que seria 18 de maio.

