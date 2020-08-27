---
keywords: Experience Platform;getting started;customer ai;popular topics;customer ai input;customer ai output
solution: Experience Platform
title: Entrada e saída de IA do cliente
topic: Getting started
description: O documento a seguir descreve as diferentes entradas e saídas utilizadas na IA do cliente.
translation-type: tm+mt
source-git-commit: c30bbaead775e68f869b080e24e18d4a23cda973
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 1%

---


# Entrada e saída de IA do cliente

O documento a seguir descreve as diferentes entradas e saídas utilizadas na IA do cliente.

## Dados de entrada de IA do cliente

A IA do cliente usa os dados do Evento de experiência do consumidor para calcular as pontuações de propensão. Para obter mais detalhes sobre o Evento de experiência do consumidor, consulte [Preparar dados para uso na documentação](../data-preparation.md)dos Serviços inteligentes.

### Dados históricos

A IA do cliente exige dados históricos para o treinamento do modelo, mas a quantidade de dados necessária se baseia em dois elementos principais: janela de resultados e população elegível.

Por padrão, a API do cliente procura que um usuário tenha tido atividade nos últimos 120 dias se nenhuma definição de população qualificada for fornecida durante a configuração do aplicativo. Além da quantidade mínima de dados de Evento de experiência do consumidor que é necessária, a IA do cliente também precisa de uma quantidade mínima de eventos bem-sucedidos com base em uma definição de meta prevista. Atualmente, a API do cliente precisa de no mínimo 500 eventos bem-sucedidos.

Os exemplos a seguir fornecidos usam uma fórmula simples para ajudar a determinar a quantidade mínima de dados necessária. Se você tiver mais do que o requisito mínimo, seu modelo provavelmente fornecerá resultados mais precisos. Se você tiver menos do que a quantidade mínima necessária, o modelo falhará, pois não há uma quantidade suficiente de dados para o treinamento do modelo.

**Fórmula**:

Comprimento mínimo dos dados necessários = população elegível + janela do resultado

>[!NOTE]
>
> 30 é o número mínimo de dias necessário para a população elegível. Se isso não for fornecido, o padrão será 120 dias.

Exemplos :

- Você deseja prever se um cliente provavelmente comprará um relógio nos próximos 30 dias. Você também deseja marcar os usuários que têm alguma atividade da Web nos últimos 60 dias. Neste caso, a duração mínima dos dados é de 60 dias + 30 dias. A população elegível é de 60 dias e a janela de resultados é de 30 dias, totalizando 90 dias.

- Você deseja prever se o usuário provavelmente comprará um relógio nos próximos 7 dias. Neste caso, o comprimento mínimo de dados exigido é de 120 dias + 7 dias. O padrão da população elegível é 120 dias e a janela de resultados é 7 dias, totalizando 127 dias.

- Você deseja prever se o cliente provavelmente comprará um relógio nos próximos 7 dias. Você também deseja marcar os usuários que têm alguma atividade da Web nos últimos 7 dias. Neste caso, a duração mínima dos dados é de 30 dias + 7 dias. A população elegível requer um mínimo de 30 dias e a janela de resultados é de 7 dias, totalizando 37 dias.

Além dos dados mínimos necessários, a IA do cliente também funciona melhor com os dados recentes. Neste caso de uso, a IA do cliente está fazendo uma previsão para o futuro com base nos dados comportamentais recentes do usuário. Em outras palavras, dados mais recentes provavelmente gerarão uma previsão mais precisa.

## Dados de saída da IA do cliente

A IA do cliente gera vários atributos para perfis individuais considerados elegíveis. Há duas maneiras de consumir a pontuação com base no que você forneceu. Se o Perfil do cliente em tempo real estiver ativado para o seu conjunto de dados, você poderá consumi-lo por meio do Perfil do cliente em tempo real. Se você não tiver um Perfil de cliente em tempo real, é possível baixar o conjunto de dados de saída AI do cliente disponível no lago de dados.

>[!NOTE]
>
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