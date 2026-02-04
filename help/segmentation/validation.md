---
title: Validação de público-alvo
description: Saiba como o Experience Platform valida seus públicos para garantir que eles tenham bom desempenho downstream.
source-git-commit: 52439e55d3c48631488b17b6b04256bcbbe37bcb
workflow-type: tm+mt
source-wordcount: '1630'
ht-degree: 1%

---


# Validação de público

Ao escrever uma definição de público-alvo no Adobe Experience Platform, a validação de público-alvo fornece validações e medidas de proteção integradas para garantir que seus públicos-alvo não sejam apenas precisos, mas também estáveis e escaláveis.

Ao seguir as práticas recomendadas de definição de público-alvo, você garante que os públicos-alvo possam avaliar mais rápido, garante que a lógica permaneça eficiente mesmo quando o tamanho do público-alvo aumentar e reduz o risco de falhas de avaliação durante períodos de alto tráfego. Públicos otimizados também melhoram a velocidade de ativação para destinos, reduzem a latência de personalização em tempo real e mantêm a estabilidade geral da sandbox.

O Experience Platform executa essas validações em tempo real à medida que você constrói seu público-alvo no Construtor de segmentos. Ao adicionar eventos ou atributos que excedem os limites de validação, você recebe feedback imediato na interface do Construtor de segmentos.

## Tipos de validação {#validation-types}

Quando a validação de público-alvo é executada nos públicos-alvo, há dois tipos diferentes de construções que podem ser violadas: construções de validação críticas e construções de otimização de desempenho.

Se uma construção de validação crítica for violada, o sistema impedirá que você salve o público-alvo para proteger a estabilidade da sandbox. Se uma construção de otimização de desempenho for violada, você poderá salvar seu público-alvo, mas é *altamente recomendado* atualizar sua definição de público-alvo para evitar problemas de desempenho.

## Verificações de validação {#validation-checks}

Atualmente, as seguintes validações são aceitas:

| Verificação de validação | Tipo | Limite |
| ---------------- | ---- | --------- |
| Complexidade lógica | Validação crítica | A definição do público-alvo contém muitas consultas, resultando em complexidade lógica desnecessária. |
| Eventos sequenciais | Validação crítica | Há mais de seis eventos sequenciais em uma definição de público-alvo. |
| Contagem agregada | Otimização do desempenho | Há mais de três funções de agregação em uma definição de público-alvo. |
| Dados aninhados | Otimização do desempenho | Há mais de dois níveis de profundidade de dados aninhados (tipos de dados de matriz ou mapa) em uma definição de público-alvo. |
| Tamanho do público-alvo | Otimização do desempenho | O tamanho da qualificação de público é maior que 30% do número total de perfis na sandbox. |

### [!BADGE Validação crítica]{type=Negative} Complexidade lógica {#logical-complexity}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_rewritescheck"
>title="Alerta de eficiência da consulta"
>abstract="Seu público-alvo contém muitas consultas, o que resulta em complexidade lógica desnecessária. Simplifique a definição de público-alvo antes de continuar."

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_cnfcomplexitycheck"
>title="Complexidade lógica"
>abstract="Seu público-alvo contém muitas consultas, o que resulta em complexidade lógica desnecessária. Simplifique a definição de público-alvo antes de continuar."

A validação da complexidade lógica analisa a estrutura das declarações lógicas (AND, OR, NOT) dentro da definição do público-alvo. Especificamente, ela busca definições de público-alvo que forçarão o sistema a executar um número excessivo de comparações por perfil.

Se a definição do público-alvo tiver um número excessivo de comparações por perfil, essa maior complexidade levará a uma avaliação mais lenta com base no perfil. Como resultado, isso aumenta o tempo geral necessário para a avaliação do público-alvo.

Para evitar o acionamento dessa validação, mantenha a definição do público-alvo simples. Se você não conseguir entender sua própria definição de público-alvo, ela é muito complicada e o Experience Platform pode levar mais tempo para avaliar o público-alvo.

**Exemplo**

Digamos que você queira encontrar clientes que vivem em determinados estados. Você _poderia_ gravar isso de maneira ineficiente verificando se o perfil tem o valor de um estado que corresponde a um dos 45 valores listados, como a seguir:

+++ Definição de público-alvo ineficiente

```
State.equals("AL", "AK", "AZ", "AR", "CA", "CO", "CT", "DE", "FL", "GA","HI", "ID", "IL", "IN", "IA", "KS", "KY", "LA", "ME", "MD", "MA", "MI", "MN", "MS", "MO", "MT", "NE", "NV", "NH", "NJ", "NM", "NY", "NC", "ND", "OH", "OK", "OR", "PA", "RI", "SC", "SD", "TN", "TX", "UT")
```

+++

No entanto, usando uma não verificação, você só precisa verificar se o perfil não tem um dos 5 valores listados, resultando em uma consulta muito mais eficiente.

+++ Definição de público-alvo eficiente

```
not(State.equals("VT", "VA", "WA", "WV", "WI", "WY" ))
```

+++

Como alternativa, digamos que você queira encontrar clientes que sejam canadenses em seu plano de avaliação. Uma abordagem menos eficiente seria procurar canadenses em seu plano de teste excluindo manualmente todos os outros planos, um por um, e verificando se o perfil não está em nenhum deles.

+++ Definição de público-alvo ineficiente

```
NOT(
    plan.equals("basic") OR
    plan.equals("standard") OR
    plan.equals("premium") OR
    plan.equals("enterprise")
) AND NOT (
    region.equals("us-east") OR
    region.equals("us-west") OR
    region.equals("eu-central") OR
    region.equals("apac")
)
```

+++

Em vez disso, você deve ser direto e direcionar o plano específico que deseja incluir.

+++ Definição de público-alvo eficiente

```
plan.equals("trial") AND region.equals("canada")
```

+++

### [!BADGE Validação crítica]{type=Negative} Complexidade de evento sequencial {#sequential-event-complexity}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_chaincountcheck"
>title="Limite de sequência de eventos"
>abstract="Seu público-alvo contém muitos eventos sequenciais. Você pode ter no máximo 6 eventos sequenciais na definição do público-alvo. Remova alguns eventos sequenciais da definição de público-alvo antes de continuar."

A validação da complexidade do evento sequencial limita o número de eventos sequenciais em uma sequência a 6 eventos.

A segmentação sequencial é uma das operações mais complicadas computacionalmente no Experience Platform, já que o sistema precisa verificar todo o histórico de eventos de experiência de um cliente, classificá-los por carimbo de data e hora e verificar se a ordem especificada corresponde à sua consulta. Como resultado, quando a cadeia cresce, o número de permutações que o sistema precisa calcular aumenta drasticamente.

Para evitar o acionamento dessa validação, concentre-se nas noções básicas da cadeia sequencial definindo o início, o meio e o fim da jornada. Etapas imediatas geralmente estão implicadas na conversão final.

**Exemplo**

Digamos que você queira direcionar os usuários que visualizaram um produto, o adicionaram ao carrinho e o compraram. Uma abordagem menos eficiente verificaria cada estado individual do caminho do usuário. Por exemplo, a seguinte consulta passa por essa sequência de eventos: Logs no site -> Pesquisas por produto -> Visualiza uma página de produto -> Adiciona ao carrinho -> Navega até o check-out -> Evento de compra

+++ Definição de público-alvo ineficiente

```
chain(xEvent, timestamp, [ A: WHAT(eventType = "login"), B: WHAT(eventType = "search"), C: WHAT(eventType = "productView"), D: WHAT(eventType = "addToCart"), E: WHAT(eventType = "checkout"), F: WHAT(eventType = "purchase") ])
```

+++

No entanto, ao reduzir a sequência para seu início, meio e fim, você só precisa ter uma sequência de eventos com duração de 3 eventos, resultando em uma consulta mais eficiente. Por exemplo, a seguinte consulta passa por essa sequência de eventos: Visualiza uma página de produto -> Adiciona ao carrinho -> Evento de compra

+++ Definição de público-alvo eficiente

```
chain(xEvent, timestamp, [ A: WHAT(eventType = "productView"), B: WHAT(eventType = "addToCart"), C: WHAT(eventType = "purchase") ])
```

+++

### [!BADGE Otimização de desempenho]{type=Caution} Contagem agregada {#aggregated-count}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_countaggregationcheck"
>title="Aviso de filtro de contagem"
>abstract="Seu público-alvo tem muitos eventos de agregação. Você deve usar no máximo 3 eventos de agregação no público-alvo. Para evitar problemas de desempenho, remova alguns eventos de agregação da definição de público-alvo."

A verificação de contagem agregada limita o número de eventos de agregação usados em seu público-alvo a três condições.

Um evento padrão só precisa encontrar um único evento correspondente para qualificar um usuário. No entanto, um evento de agregação precisa ler e analisar o **histórico completo** de eventos de um usuário para que ele possa tomar uma decisão, resultando em tempos de processamento mais lentos com mais eventos de agregação usados.

Para evitar o acionamento dessa validação, use contagens específicas apenas quando for estritamente necessário para a definição do público-alvo. Por exemplo, se você precisar saber apenas se um usuário se engajou uma vez, é possível usar a lógica padrão &quot;Existe&quot;, em vez de usar um evento &quot;Contagem > 0&quot;.

### [!BADGE Complexidade de dados aninhados]{type=Caution} para otimização de desempenho {#nested-data-complexity}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_arraydepthcheck"
>title="Aviso de dados aninhados"
>abstract="Seu público-alvo tem muitas camadas de dados aninhadas. Você deve usar no máximo 2 camadas de dados no público-alvo. Para evitar problemas de desempenho, você deve nivelar a definição de público-alvo."

A validação da complexidade de dados aninhados limita o número de dados aninhados em uma definição de público-alvo a duas camadas.

Embora o Experience Platform seja compatível com o uso de objetos de matriz e de mapa para armazenar tipos de dados complexos, descompactar estruturas aninhadas para localizar um valor requer uma lógica de passagem mais complexa. Quanto mais profundos os dados forem aninhados em um array, mais tempo levará para serem recuperados para validação.

Se você costuma realizar a segmentação em um atributo profundamente aninhado, talvez seja necessário entrar em contato com a equipe de engenharia de dados para copiar o atributo para um nível superior no esquema do perfil para facilitar o acesso.

### [!BADGE Otimização de desempenho]{type=Caution} Tamanho do público {#audience-size}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_profilestorecheck"
>title="Aviso de tamanho do público"
>abstract="Seu público-alvo é escrito de forma muito ampla. Você deve evitar escrever uma definição de público-alvo que qualifique mais de 30% do total de perfis em sua sandbox. Para evitar problemas de desempenho, você deve restringir a definição de público-alvo."

A validação do tamanho do público verifica se a definição de público-alvo é tão ampla que mais de 30% do total de perfis em sua sandbox se qualificam para o público-alvo.

Embora o Experience Platform possa lidar com públicos-alvo grandes, uma definição de público-alvo muito vaga (como Todos os clientes ativos) pode aumentar o tempo de avaliação e a latência de ativação.

Se você precisar criar um público-alvo que qualifique mais de 30% do seu armazenamento de perfis, verifique se a primeira avaliação do público-alvo é feita usando uma avaliação de público-alvo flexível. A avaliação do público-alvo com uma avaliação sob demanda pode reduzir o impacto geral de um grande público-alvo no trabalho diário de segmentação.

## Próximas etapas

Depois de ler este guia, você compreenderá melhor como o Experience Platform executa validações automáticas para melhorar a avaliação, a estabilidade e a escalabilidade. Para obter mais informações sobre como criar públicos-alvo usando a interface, leia a [documentação sobre o Construtor de segmentos](./ui/segment-builder.md).

## Apêndice

O apêndice a seguir lista as perguntas frequentes sobre a validação de público-alvo no Experience Platform.

### Perguntas frequentes {#faq}

**O que acontece se eu ignorar os avisos e salvar o público?**

+++ Resposta

Para avisos de otimização de desempenho, o público-alvo será salvo e o sistema tentará avaliá-lo. No entanto, você pode enfrentar tempos de processamento significativamente mais lentos. Em situações extremas, se o volume de dados for alto o suficiente, o trabalho de segmentação pode falhar ou atingir o tempo limite, forçando você a reprojetar o público-alvo.

Para erros críticos de validação, não será possível salvar o público-alvo.

+++

**Posso solicitar um aumento para o limite de &quot;Eventos Sequenciais&quot;?**

+++ Resposta

Não pode. Essa é uma proteção rígida projetada para proteger a estabilidade de todo o ambiente do Experience Platform. Se a sequência exigir mais de 6 etapas, é um forte indicador de que a lógica deve ser simplificada ou dividida em dois públicos diferentes (como um público-alvo de &quot;Envolvimento&quot; e um público de &quot;Conversão&quot;).

+++

**Essas novas validações interromperão meus públicos existentes?**

+++ Resposta

Estas validações são executadas no momento da **criação**. Como resultado, os públicos-alvo existentes continuarão sendo executados como estão. No entanto, se você tentar editar um público-alvo que viole essas regras, será necessário otimizá-lo para poder salvar as alterações.

+++

**Tenho requisitos de dados complexos. Como posso evitar o aviso &quot;Dados Aninhados&quot;?**

+++ Resposta

Evitar o aviso de &quot;Dados aninhados&quot; é melhor resolver na camada de modelagem de dados. Algumas dicas incluem trabalhar com a equipe de engenharia de dados para nivelar o esquema XDM e trazer atributos críticos (como `subscriptionStatus` e `loyaltyTier`) para o nível superior do perfil.

+++

**Estas verificações se aplicam aos públicos Rascunho e Publicado?**

+++ Resposta

Sim, essas verificações se aplicam a *todos* os públicos-alvo avaliados na Experience Platform.

+++
