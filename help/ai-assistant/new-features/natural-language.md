---
title: Estimativa de linguagem natural com o assistente de IA
description: Saiba como usar os recursos de estimativa de linguagem natural do Assistente de IA.
badge: Alfa
source-git-commit: aef3be05ca23abe9ed8275aa562fdd3313a7e2d0
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 0%

---

# Estimativa de linguagem natural com o Assistente de IA

>[!AVAILABILITY]
>
>Esse recurso está na Alpha e pode não estar disponível para sua organização. Para participar do programa Alpha e acessar esse recurso, entre em contato com a equipe de conta do Adobe.

Você pode usar os recursos de Estimativa de linguagem natural do Assistente de IA para Adobe Experience Platform a fim de estimar o tamanho do público e prever as propensões do público com base em perguntas simples e conversacionais. Com esse recurso, você pode tornar os insights do público-alvo mais acessíveis e intuitivos. Isso pode ser particularmente útil para seus casos de uso de operações de marketing e negócios, especialmente se você estiver gerenciando seus públicos diariamente e estiver confiando nesses insights para moldar estratégias de marketing eficazes.

Com os recursos de processamento de linguagem natural do Assistente de IA, você pode fazer perguntas como: &quot;Quantos perfis eu tenho na Califórnia entre 25 e 35 anos&quot; ou &quot;Quantos clientes de alto valor nós temos?&quot; ou até mesmo &quot;Qual porcentagem do meu público-alvo provavelmente comprará no próximo mês?&quot; O Assistente de IA interpreta essas perguntas e retorna estimativas ou pontuações de propensão que você pode usar para tomar decisões informadas por dados.

Leia este documento para saber como você pode usar os recursos de estimativa de linguagem natural do Assistente de IA.

## Terminologia e definições principais {#key-terminology-and-definitions}

Consulte a tabela a seguir para obter uma lista de terminologias importantes e suas definições correspondentes.

| Terminologia | Definição |
| --- | --- |
| Estimativa de tamanho do público | O processo de calcular o número de membros em um público específico com base em um critério definido. É possível basear as estimativas de tamanho nos dados do perfil, incluindo perfis que não estão em um público-alvo. Além disso, você pode recuperar estimativas de tamanho de público-alvo sem ter que criar um público-alvo primeiro. Use esse insight para entender a escala do seu alcance para campanhas direcionadas. |
| Estimativa de propensão | Uma previsão da probabilidade de os membros de um público-alvo exibirem comportamentos específicos (como: fazer uma compra, churning) em um determinado período. A estimativa de propensão é específica para públicos-alvo no Real-time Customer Data Platform, mas pode incluir dados de perfil, incluindo perfis em qualquer público-alvo. Você pode consultar esse insight ao otimizar suas campanhas e gerenciar estratégias de retenção de público-alvo. |
| Processamento de linguagem natural | A capacidade do Assistente de IA de interpretar e responder a perguntas feitas na linguagem do dia a dia, permitindo que você interaja conversacionalmente e receba insights relevantes sem usar consultas técnicas. |
| Intervalos de tempo predefinidos | Intervalos de tempo padrão ( &quot;mês passado&quot;, &quot;próximos 30 dias&quot;) compatíveis com o Assistente de IA para estimar o tamanho e as propensões do público-alvo. **Observação**: intervalos de tempo personalizados podem não ter suporte completo durante o estágio de Alpha. |
| Dados de instantâneo | O conjunto de dados usado pelo Assistente de IA para fornecer estimativas. Esses dados são atualizados no Real-time Customer Data Platform a cada 24-48 horas e, portanto, os insights podem não refletir as alterações no público-alvo em tempo real. |

{style="table-layout:auto"}

## Exemplos de caso de uso {#use-case-examples}

Os recursos de estimativa de linguagem natural do Assistente de IA podem ser especialmente úteis nos seguintes casos de uso:

### Operações de marketing

Como profissional de operações de marketing, suas responsabilidades podem incluir o gerenciamento e o monitoramento de dados de público-alvo para garantir que se alinhem aos objetivos de negócios. Com o recurso de estimativa de linguagem natural do Assistente de IA, você pode coletar rapidamente insights sobre tamanhos e propensões de público-alvo sem precisar criar um público-alvo primeiro ou um conhecimento abrangente de análise de dados.

ajudando-os a manter uma abordagem consistente e orientada por dados em seus fluxos de trabalho.

### Usuários empresariais e profissionais de marketing

Como usuário empresarial e profissional de marketing, o acesso rápido aos dados do público-alvo pode ser fundamental para o sucesso do planejamento, do direcionamento e da avaliação da campanha. Com o recurso de estimativa em linguagem natural do Assistente de IA, você pode simplificar seu acesso às informações do público-alvo, fazer perguntas diretas e receber insights acionáveis que ajudam na criação de público-alvo e na otimização de campanha.

## Recursos principais

>[!IMPORTANT]
>
>Os seguintes recursos estão em Alpha e são focados em recursos fundamentais de estimativa de linguagem natural. Como esse recurso está no Alpha, você deve verificar novamente a precisão das respostas recebidas do Assistente de IA.

### Estimativa de tamanho do público

Você pode usar consultas de linguagem natural para solicitar que o Assistente de IA estime o tamanho de públicos específicos. Esse recurso pode ser particularmente útil para medir o alcance e o impacto dos públicos-alvo. Por exemplo, como estrategista de marketing, você pode fazer perguntas como:

* &quot;Quantos perfis vivem em Nova York?&quot;
* &quot;Quantos perfis eu tenho com um email e consenti?&quot;

Use esse recurso para simplificar o processo de estimativa de tamanhos de público-alvo e obter respostas imediatas sem precisar navegar por filtros de dados complexos ou definições de segmento.

### Estimativa de propensão de público

>[!TIP]
>
>Sua conta Experience Platform deve ser provisionada com a [IA do cliente](../../intelligent-services/customer-ai/overview.md) para usar os recursos de estimativa de propensão do Assistente de IA.

Você pode usar a estimativa de propensão do público-alvo para identificar a probabilidade de comportamentos ou ações específicos em um público-alvo. Por exemplo, você pode fazer perguntas como:

* &quot;Qual porcentagem do meu público-alvo atual deve comprar no próximo mês?&quot;
* &quot;Quantos perfis tenho com alta propensão para conversão?&quot;

Ao fazer perguntas em linguagem natural, você pode recuperar pontuações de propensão que indicam a porcentagem ou a probabilidade de membros do público-alvo exibirem determinados comportamentos, ajudando você a fazer ajustes proativos em suas campanhas ou estratégias de retenção.

## Exemplo de perguntas para o tamanho do público e a estimativa de propensão

A seguir, apresentamos exemplos de perguntas que você pode fazer ao Assistente de IA para ajudá-lo a entender o tamanho do público-alvo e as propensões comportamentais:

### Estimativa de tamanho do público

* &quot;Quantos perfis eu tenho com um email ou número de celular?&quot;
* &quot;Quantos perfis eu tenho em Nova York?&quot;
* &quot;Quais são os cinco principais estados em que meus clientes vivem?&quot;

### Estimativa de propensão de público

* &quot;Qual porcentagem do meu público-alvo provavelmente comprará no próximo mês?&quot;
* &quot;Quantos clientes devem ser convertidos no próximo trimestre?&quot;

Você pode usar a flexibilidade que os queries de linguagem natural fornecem para obter insights rápidos sobre a dinâmica do público-alvo sem precisar de conhecimento técnico.

## Perguntas frequentes

Leia esta seção para obter respostas a perguntas frequentes sobre a estimativa de linguagem natural com o Assistente de IA.

### Com que frequência o Assistente de IA atualiza os dados de público-alvo?

Os dados do Assistente de IA são atualizados a cada 24-48 horas. Por conseguinte, as estimativas podem refletir ligeiros atrasos. Isso significa que quando você pergunta sobre os dados &quot;atuais&quot;, a resposta reflete o instantâneo mais recente, que pode ter até 48 horas.

### Posso solicitar tamanhos de público ou tendências com intervalos de datas personalizados?

Atualmente, o Assistente de IA suporta intervalos de datas predefinidos, como &quot;último mês&quot; ou &quot;próximos 30 dias&quot;. Intervalos de datas personalizados além dessas opções predefinidas não são totalmente compatíveis com o estágio Alpha. Se um período personalizado for solicitado, o Assistente de IA fornecerá insights com base no período disponível mais próximo.

### Como o Assistente de IA calcula as pontuações de propensão?

As pontuações de propensão são calculadas usando a [IA do cliente](../../intelligent-services/customer-ai/overview.md). O Assistente de IA usa modelos de aprendizado de máquina para prever a probabilidade de comportamentos de público-alvo específicos, como compras e churn, dentro do intervalo de tempo solicitado. Durante o estágio de Alpha, o cálculo da pontuação de propensão no Assistente de IA não usa eventos de experiência ou dados comportamentais.

### O Assistente de IA estimará os tamanhos ou as tendências do público-alvo com base em dados em tempo real?

Não, os dados em tempo real não estão disponíveis neste momento. As estimativas são baseadas em instantâneos de dados recentes, atualizados a cada 24-48 horas. As atualizações em tempo real estão fora do escopo durante o estágio de Alpha.

### Como as propensões são calculadas?

O Assistente de IA depende de modelos de IA do cliente para responder a qualquer pontuação de probabilidade ou propensão.

## Recursos fora do escopo

Os seguintes recursos não são suportados no momento:

### Estimativas de tamanho de público com base no evento de dados comportamentais

No momento, o Assistente de IA não pode responder a perguntas com base em dados comportamentais, como **&quot;Quantos usuários adicionaram um produto ao carrinho nos últimos 30 dias&quot;**. No entanto, você pode criar um atributo calculado no Real-Time CDP que pode pré-calcular esses valores. Esses atributos calculados ficam disponíveis no Assistente de IA. Para obter mais informações, leia a documentação sobre [atributos computados](../../profile/computed-attributes/overview.md).

### Atualizações de dados em tempo real

As estimativas fornecidas pelo Assistente de IA são baseadas em instantâneos de dados recentes, mas não em tempo real. Os dados são atualizados a cada 24-48 horas, portanto, os insights refletem esse atraso. Essa limitação significa que os usuários não poderão receber atualizações instantâneas se um segmento ou conjunto de dados for alterado significativamente em um curto período.