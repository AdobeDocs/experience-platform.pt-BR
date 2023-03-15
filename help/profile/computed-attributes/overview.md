---
keywords: Experience Platform;perfil;perfil de cliente em tempo real;solução de problemas;API
title: Introdução a atributos computados
type: Documentation
description: Os atributos computados são funções para agregar dados de nível de evento em atributos de nível de perfil. Essas funções são computadas automaticamente para que possam ser usadas na segmentação, ativação e personalização.
exl-id: 13878363-589d-4a3c-811c-21d014a5f3c2
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 1%

---

# (Alfa) Visão geral de atributos computados

>[!IMPORTANT]
>
>No momento, a funcionalidade de atributo computada está em alfa e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

Os atributos computados são funções usadas para agregar dados no nível do evento em atributos no nível do perfil. Essas funções são computadas automaticamente para que possam ser usadas na segmentação, ativação e personalização.

Cada atributo calculado contém uma expressão, ou &quot;regra&quot;, que avalia os dados recebidos e armazena o valor resultante em um atributo de perfil. Esses cálculos ajudam a responder facilmente a perguntas relacionadas a coisas como valor de compra vitalício, tempo entre compras ou número de aberturas de aplicativo, sem exigir que você realize cálculos complexos manualmente sempre que as informações forem necessárias. Esses valores de atributos calculados podem ser exibidos em um perfil, usados para criar um segmento ou acessados por meio de vários padrões de acesso diferentes.

Este guia ajudará você a entender melhor a função dos atributos computados no Adobe Experience Platform.

## Noções básicas sobre atributos computados

O Adobe Experience Platform permite importar e mesclar dados facilmente de várias fontes para gerar [!DNL Real-Time Customer Profiles]. Cada perfil contém informações importantes relacionadas a um indivíduo, como suas informações de contato, preferências e histórico de compras, fornecendo uma visualização de 360 graus do cliente.

Algumas das informações coletadas no perfil são facilmente compreendidas ao ler os campos de dados diretamente (por exemplo, &quot;nome&quot;), enquanto outros dados exigem a execução de vários cálculos ou a confiança em outros campos e valores para gerar as informações (por exemplo, &quot;total de compras vitalícias&quot;). Para facilitar a compreensão rápida desses dados, [!DNL Platform] O permite criar atributos calculados que executam automaticamente essas referências e cálculos, retornando o valor no campo apropriado.

Os atributos computados incluem a criação de uma expressão, ou &quot;regra&quot;, que opera nos dados recebidos e armazena o valor resultante em um atributo de perfil. As expressões podem ser definidas de várias maneiras diferentes, permitindo especificar que uma regra avalie somente eventos de entrada, um evento de entrada e dados de perfil ou um evento de entrada, dados de perfil e eventos históricos.

### Casos de uso

Os casos de uso para atributos calculados podem variar de cálculos simples a referências muito complexas. Estes são alguns exemplos de casos de uso para atributos computados:

1. **[!UICONTROL Porcentagens]:** Um atributo calculado simples pode incluir a utilização de dois campos numéricos em um registro e sua divisão para criar uma porcentagem. Por exemplo, você pode pegar o número total de emails enviados a um indivíduo e dividi-lo pelo número de emails que o indivíduo abre. O campo de atributo calculado resultante mostraria rapidamente a porcentagem do total de emails abertos pelo indivíduo.
1. **[!UICONTROL Uso do aplicativo]:** Outro exemplo inclui a capacidade de agregar o número de vezes que um usuário abre seu aplicativo. Ao rastrear o número total de aberturas de aplicativos, com base em eventos individuais abertos, você pode fornecer ofertas ou mensagens especiais aos usuários em sua centésima abertura, incentivando um engajamento mais profundo com sua marca.
1. **[!UICONTROL Valores vitalícios]:** Pode ser muito difícil coletar os totais acumulados, como um valor de compra vitalício para um cliente. Isso requer a atualização do total do histórico sempre que um novo evento de compra ocorrer. Um atributo calculado permite fazer isso muito mais facilmente, mantendo o valor do tempo de vida em um único campo que é atualizado automaticamente após cada evento de compra bem-sucedido relacionado ao cliente.

## Limitações conhecidas

### Disponibilidade atrasada de novos atributos computados

A disponibilidade dos novos atributos computados pode ser atrasada em até 2 horas após o atributo de esquema correspondente ser adicionado ao esquema de união.

Esse atraso se deve à configuração atual de armazenamento em cache. Pós-Alfa, a frequência de atualização do cache podia ser aumentada.

### Rastreamento de dependência em segmentos

Os atributos de esquema que já foram usados em uma expressão de definição de segmento, mas posteriormente transformados em um atributo calculado, não serão rastreados como uma dependência desse segmento.

Devido ao fato de que nenhuma dependência foi detectada, o Experience Platform não avaliará automaticamente o atributo calculado associado sempre que a definição do segmento for avaliada.

Como alternativa, a criação de atributos computados pode ser gerenciada por meio de um grupo de campos de esquema específico que adiciona novos atributos computados que não entram em conflito com atributos existentes. Outra alternativa é simplesmente recriar o segmento com o rastreamento de dependência correto para os novos atributos calculados.
