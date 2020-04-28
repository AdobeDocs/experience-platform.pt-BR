---
keywords: Experience Platform;getting started;customer ai;popular topics
solution: Experience Platform
title: Entrada e saída de IA do cliente
topic: Getting started
translation-type: tm+mt
source-git-commit: 66ccea896846c1da4310c1077e2dc7066a258063

---


# Entrada e saída de IA do cliente

O documento a seguir descreve as diferentes entradas e saídas utilizadas na IA do cliente.

## Dados de entrada de IA do cliente

A IA do cliente usa os dados do Evento de experiência do consumidor para calcular as pontuações de propensão. Para obter mais detalhes sobre o Evento de experiência do consumidor, consulte [Preparar dados para uso na documentação](../data-preparation.md)dos Serviços inteligentes.

## Dados de saída da IA do cliente

A IA do cliente gera vários atributos para perfis individuais considerados elegíveis. Há duas maneiras de consumir a pontuação com base no que você forneceu. Se o Perfil do cliente em tempo real estiver ativado para o seu conjunto de dados, você poderá consumi-lo por meio do Perfil do cliente em tempo real. Se você não tiver um Perfil de cliente em tempo real, é possível baixar o conjunto de dados de saída AI do cliente disponível no lago de dados.

>[!NOTE]
>Os valores de saída são consumidos pelo Perfil de cliente em tempo real, que pode ser usado para criar e definir segmentos.

A tabela abaixo descreve os vários atributos encontrados na saída da IA do cliente:

| Atributo | Descrição |
| ----- | ----------- |
| Pontuação | A probabilidade relativa de um cliente atingir a meta prevista dentro do intervalo de tempo definido. Este valor não deve ser considerado como uma percentagem de probabilidade, mas sim a probabilidade de um indivíduo em comparação com a população global. Essa pontuação varia de 0 a 100. |
| Probabilidade | Este atributo é a real probabilidade de um perfil alcançar a meta prevista dentro do intervalo de tempo definido. Ao comparar resultados em diferentes metas, é recomendável considerar a probabilidade em relação ao percentil ou à pontuação. A probabilidade deve ser sempre utilizada para determinar a probabilidade média na população elegível, uma vez que a probabilidade tende a estar no lado inferior para eventos que não ocorrem com frequência. Valores para o intervalo de probabilidade entre 0 e 1. |
| Percentil | Esse valor fornece informações relacionadas ao desempenho de um perfil em relação a outros perfis com pontuação semelhante. Por exemplo, um perfil com uma classificação de percentil de 99 para churn indica que ele está com um risco maior de churning em comparação com 99% de todos os outros perfis que foram pontuados. Os percentis variam de 1 a 100. |
| Tipo de propensão | O tipo de propensão selecionado. |
| Data da pontuação | A data em que a pontuação ocorreu. |
| Fatores influentes | Motivos previstos para o motivo pelo qual um perfil é susceptível de converter ou gerar uma taxa. Os fatores são constituídos pelos seguintes atributos:<ul><li>Código: O atributo perfil ou comportamental que influencia positivamente a pontuação prevista de um perfil. </li><li>Valor: O valor do perfil ou do atributo comportamental.</li><li>Importância: Indica o peso do perfil ou do atributo comportamental na pontuação prevista (baixa, média, alta)</li></ul> |

## Próximas etapas {#next-steps}

Depois de preparar seus dados e ter todas as suas credenciais e schemas no lugar, siga o guia [Configurar uma instância](./user-guide/configure.md) do AI do cliente. Este guia o orienta a criar uma instância para a IA do cliente.