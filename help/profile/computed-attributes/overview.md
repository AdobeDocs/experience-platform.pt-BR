---
keywords: Experience Platform;perfil;perfil do cliente em tempo real;solução de problemas;API
title: Introdução aos atributos calculados
topic: guide
type: Documentation
description: Atributos calculados são funções para agregação de dados no nível do evento em atributos no nível do perfil. Essas funções são computadas automaticamente para que possam ser usadas em segmentação, ativação e personalização.
translation-type: tm+mt
source-git-commit: 4ed2b80ebfd87f8920462ae0a918b01bb13d4210
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 1%

---


# (Alfa) Visão geral dos atributos calculados

>[!IMPORTANT]
>
>A funcionalidade de atributo calculado está atualmente em alfa e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

Atributos calculados são funções usadas para agregação de dados no nível do evento em atributos no nível do perfil. Essas funções são computadas automaticamente para que possam ser usadas em segmentação, ativação e personalização.

Cada atributo calculado contém uma expressão, ou &quot;regra&quot;, que avalia os dados recebidos e armazena o valor resultante em um atributo de perfil. Esses cálculos ajudam você a responder facilmente perguntas relacionadas a coisas como valor de compra vitalícia, tempo entre compras ou número de aberturas de aplicativos, sem exigir a execução manual de cálculos complexos sempre que as informações forem necessárias. Esses valores de atributos calculados podem ser exibidos em um perfil, usados para criar um segmento ou acessados por meio de vários padrões de acesso diferentes.

Este guia o ajudará a entender melhor a função dos atributos calculados no Adobe Experience Platform.

## Noções básicas sobre atributos calculados

A Adobe Experience Platform permite que você importe e mescle facilmente dados de várias fontes para gerar [!DNL Real-time Customer Profiles]. Cada perfil contém informações importantes relacionadas a um indivíduo, como informações de contato, preferências e histórico de compras, fornecendo uma visualização de 360 graus do cliente.

Algumas das informações coletadas no perfil são facilmente compreendidas ao ler os campos de dados diretamente (por exemplo, &quot;primeiro nome&quot;), enquanto outros dados exigem a execução de vários cálculos ou a confiança em outros campos e valores para gerar as informações (por exemplo, &quot;total da compra vitalícia&quot;). Para facilitar a compreensão rápida desses dados, [!DNL Platform] permite criar atributos calculados que executam automaticamente essas referências e cálculos, retornando o valor no campo apropriado.

Os atributos calculados incluem a criação de uma expressão, ou &quot;regra&quot;, que opera em dados recebidos e armazena o valor resultante em um atributo de perfil. As expressões podem ser definidas de várias maneiras diferentes, permitindo especificar que uma regra avalie somente eventos recebidos, dados de eventos e perfis recebidos ou eventos recebidos, dados de perfis e eventos históricos.

### Casos de uso

Casos de uso para atributos calculados podem variar de cálculos simples a referências muito complexas. Estes são alguns exemplos de casos de uso para atributos calculados:

1. **[!UICONTROL Porcentagens]:** um atributo calculado simples pode incluir a captura de dois campos numéricos em um registro e a divisão desses campos para criar uma porcentagem. Por exemplo, você pode pegar o número total de emails enviados para um indivíduo e dividi-lo pelo número de emails que o indivíduo abre. Olhar para o campo de atributo calculado resultante mostraria rapidamente a porcentagem do total de emails abertos pelo indivíduo.
1. **[!UICONTROL Uso] do aplicativo:** outro exemplo inclui a capacidade de agregação do número de vezes que um usuário abre seu aplicativo. Rastreando o número total de aberturas do aplicativo, com base em eventos individuais abertos, você pode fornecer ofertas ou mensagens especiais aos usuários em seus 100 anos abertos, encorajando um envolvimento mais profundo com a sua marca.
1. **[!UICONTROL Valores] de duração:** coletar totais em execução, como um valor de compra vitalício para um cliente, pode ser muito difícil. Isso requer a atualização do total histórico sempre que ocorrer um novo evento de compra. Um atributo calculado permite que você faça isso com muito mais facilidade, mantendo o valor do tempo de vida em um único campo que é atualizado automaticamente após cada evento de compra bem-sucedido relacionado ao cliente.

## Limitações conhecidas

### Disponibilidade atrasada de novos atributos calculados

A disponibilidade de novos atributos calculados pode ser atrasada até 2 horas após o atributo do schema correspondente ser adicionado ao schema da união.

Esse atraso ocorre devido à configuração atual do cache. A frequência de atualização do cache pode ser aumentada após o Alpha.

### Rastreamento de dependência em segmentos

Os atributos de schema que já foram usados em uma expressão de definição de segmento, mas posteriormente transformados em um atributo calculado, não serão rastreados como uma dependência desse segmento.

Devido ao fato de nenhuma dependência ter sido detectada, o Experience Platform não avaliará automaticamente o atributo calculado associado sempre que a definição do segmento for avaliada.

Como alternativa, a criação de atributos calculados poderia ser gerenciada por meio de uma combinação específica que adiciona novos atributos calculados que não entram em conflito com os atributos existentes. Outra alternativa é simplesmente recriar o segmento com o rastreamento de dependência correto para os novos atributos calculados.