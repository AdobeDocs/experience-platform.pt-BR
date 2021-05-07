---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, API
title: Introdução a atributos calculados
topic-legacy: guide
type: Documentation
description: Atributos calculados são funções para agregar dados a nível de evento em atributos a nível de perfil. Essas funções são calculadas automaticamente para que possam ser usadas na segmentação, ativação e personalização.
exl-id: 13878363-589d-4a3c-811c-21d014a5f3c2
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 1%

---

# (Alfa) Visão geral dos atributos calculados

>[!IMPORTANT]
>
>A funcionalidade de atributo calculado está atualmente em alfa e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

Atributos calculados são funções usadas para agregar dados no nível do evento em atributos no nível do perfil. Essas funções são calculadas automaticamente para que possam ser usadas na segmentação, ativação e personalização.

Cada atributo calculado contém uma expressão, ou &quot;regra&quot;, que avalia os dados recebidos e armazena o valor resultante em um atributo de perfil. Esses cálculos ajudam você a responder facilmente perguntas relacionadas a coisas como valor de compra vitalícia, tempo entre compras ou número de aberturas de aplicativos, sem exigir a execução manual de cálculos complexos sempre que as informações forem necessárias. Esses valores de atributos calculados podem ser visualizados em um perfil, usados para criar um segmento ou acessados por meio de vários padrões de acesso diferentes.

Este guia ajudará você a entender melhor a função dos atributos calculados no Adobe Experience Platform.

## Como entender atributos calculados

O Adobe Experience Platform permite importar e mesclar facilmente dados de várias fontes para gerar [!DNL Real-time Customer Profiles]. Cada perfil contém informações importantes relacionadas a um indivíduo, como informações de contato, preferências e histórico de compras, fornecendo uma visualização de 360 graus do cliente.

Algumas das informações coletadas no perfil são facilmente compreendidas ao ler os campos de dados diretamente (por exemplo, &quot;nome&quot;), enquanto outros dados exigem a execução de vários cálculos ou a dependência de outros campos e valores para gerar as informações (por exemplo, &quot;total da compra vitalícia&quot;). Para facilitar rapidamente a compreensão desses dados, [!DNL Platform] permite criar atributos calculados que executam automaticamente essas referências e cálculos, retornando o valor no campo apropriado.

Os atributos calculados incluem a criação de uma expressão, ou &quot;regra&quot;, que opera nos dados recebidos e armazena o valor resultante em um atributo de perfil. As expressões podem ser definidas de várias maneiras diferentes, permitindo especificar que uma regra avalie somente eventos recebidos, um evento e dados de perfil recebidos ou um evento recebido, dados de perfil e eventos históricos.

### Casos de uso

Os casos de uso para atributos calculados podem variar desde cálculos simples até referências muito complexas. Estes são alguns exemplos de casos de uso para atributos calculados:

1. **[!UICONTROL Percentages]:** um atributo calculado simples pode incluir a captura de dois campos numéricos em um registro e a divisão para criar uma porcentagem. Por exemplo, você pode pegar o número total de emails enviados para um indivíduo e dividi-lo pelo número de emails que o indivíduo abre. Olhar para o campo de atributo calculado resultante mostraria rapidamente a porcentagem do total de emails abertos pelo indivíduo.
1. **[!UICONTROL Application use]:** Outro exemplo inclui a capacidade de agregar o número de vezes que um usuário abre seu aplicativo. Ao rastrear o número total de aberturas do aplicativo, com base em eventos individuais abertos, você pode fornecer ofertas ou mensagens especiais aos usuários na 100ª abertura, incentivando um envolvimento mais profundo com a sua marca.
1. **[!UICONTROL Lifetime values]:** reunir totais em execução, como um valor de compra vitalício para um cliente, pode ser muito difícil. Isso requer a atualização do total histórico sempre que um novo evento de compra ocorrer. Um atributo calculado permite fazer isso com muito mais facilidade, mantendo o valor vitalício em um único campo que é atualizado automaticamente após cada evento de compra bem-sucedido relacionado ao cliente.

## Limitações conhecidas

### Disponibilidade atrasada de novos atributos calculados

A disponibilidade de novos atributos calculados pode ser atrasada até 2 horas após o atributo de esquema correspondente ser adicionado ao schema de união.

Esse atraso é devido à configuração atual de armazenamento em cache. Pós-alfa, a frequência de atualização do cache pode ser aumentada.

### Rastreamento de dependência em segmentos

Os atributos de esquema que já foram usados em uma expressão de definição de segmento, mas posteriormente transformados em um atributo calculado, não serão rastreados como uma dependência desse segmento.

Devido ao fato de que nenhuma dependência foi detectada, o Experience Platform não avaliará automaticamente o atributo calculado associado sempre que a definição do segmento for avaliada.

Como alternativa, a criação de atributos calculados pode ser gerenciada por meio de um grupo de campos de esquema específico que adiciona novos atributos calculados que não estão em conflito com atributos existentes. Outra alternativa é simplesmente recriar o segmento com o rastreamento de dependência correto para os novos atributos calculados.
