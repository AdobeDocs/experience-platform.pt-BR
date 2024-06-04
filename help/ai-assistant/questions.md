---
title: Guia de perguntas do Assistente de IA
description: Leia este documento para conhecer exemplos de perguntas que você pode usar ao consultar o Assistente de IA.
source-git-commit: a1092e21940c5e4ba9b598bc51ba1243b57a0051
workflow-type: tm+mt
source-wordcount: '1224'
ht-degree: 0%

---

# Guia de perguntas do Assistente de IA

Leia este documento no para obter um conjunto de exemplos de perguntas que você pode usar ao consultar o Assistente de IA.

Você também pode usar este documento para obter dicas sobre [como formular suas perguntas](#phrasing-your-questions) para obter respostas ideais do Assistente de IA.

## Perguntas baseadas em objetivos {#objectives-questions}

As seguintes perguntas de exemplo são agrupadas por objetivos que você pode realizar ao usar o Assistente de IA:

| Objetivo | Descrição | Exemplo |
| --- | --- | --- |
| Conceitos de aprendizado e fluxos de trabalho contínuos | <ul><li>Como usuário iniciante, você pode usar o AI Assistant para aprender conceitos do Real-Time CDP e do Adobe Journey Optimizer e integrar-se a produtos e recursos com os quais não está familiarizado.</li><li>Como um usuário experiente, você pode usar o AI Assistant para resolver um caso de borda que pode estar bloqueando seu fluxo de trabalho. | <ul><li>Como configurar um painel no Jornada Analytics?</li><li>Conte-me alguns casos de uso para o Real-Time CDP.</li></ul> |
| Solução de problemas | Use o Assistente de IA para saber como depurar erros básicos que você pode encontrar no fluxo de trabalho. | <ul><li>O que faz esse erro {ERROR_MESSAGE} quer dizer?</li><li>Por que não consigo excluir o público-alvo chamado &quot;Luma: Público-alvo de email&quot;?</li></ul> |
| Higiene da sandbox | Use o Assistente de IA para identificar objetos duplicados ou não utilizados, para que você possa manter sua sandbox com eficiência. | <ul><li>Você pode me mostrar públicos semelhantes?</li><li>Há esquemas que não tenham um conjunto de dados associado?</li></ul> |
| Análise de valor | Use o Assistente de IA para identificar os objetos de dados mais usados e avaliar os indicadores de desempenho ou encontrar os objetos de dados mais valiosos. | <ul><li>Quantos perfis estão em nossa definição de segmento &quot;Luma: Público-alvo de email&quot;?</li><li>Quando os públicos-alvo foram ativados para o destino do Experience Cloud Audiences?</li></ul> |
| Pesquisa | Use o AI Assistant para encontrar objetos de Experience Platform compatíveis, como públicos-alvo, conjuntos de dados, destinos, esquemas e fontes. | <ul><li>Liste os públicos-alvo que contêm &quot;Luma&quot; no nome que foram criados no último trimestre.</li><li>Quais atributos estão no esquema XDM &quot;Luma: Ações personalizadas&quot;?</li></ul> |
| Análise de impacto | Use o Assistente do AI para identificar objetos de dados que foram usados em determinados workflows para que você possa avaliar o impacto de quaisquer alterações. | <ul><li>Quais públicos-alvo usam `homeAddress.city` no esquema &quot;Luma: PersonProfiles&quot;?</li><li>Quais conjuntos de dados são os `consents.marketing.push.val` atributo de perfil armazenado em?</li></ul> |

{style="table-layout:auto"}

## Insights operacionais por entidade e perguntas de conhecimento do produto{#objects-questions}

As perguntas a seguir são agrupadas por objetos de dados e são classificadas como [insights operacionais](./home.md#operational-insights) ou [conhecimento do produto](./home.md#product-knowledge).

| Objeto | Descrição |
| --- | --- |
| Públicos-alvo - insights operacionais | <ul><li>Quais públicos-alvo usam outros públicos-alvo?</li><li>Qual é a distribuição do número de perfis entre os públicos-alvo?</li><li>Mostre-me os públicos que foram modificados pela última vez antes {RELATIVE_DATE}.</li><li>Quais públicos-alvo têm 0 perfis?</li><li>É {USE_AUTOCOMPLETE_TO_FILL_AUDIENCE_NAME} usado em qualquer outro público-alvo?</li></ul> |
| Atributos - Insights operacionais | <ul><li>Quais públicos-alvo têm atributo XDM {ATTRIBUTE_PATH} na definição do segmento?</li><li>Quantos atributos de esquema XDM não são usados em nenhum público-alvo?</li><li>Quais esquemas têm atributo XDM {ATTRIBUTE_PATH} neles?</li><li>Quais atributos XDM são ativados?</li><li>Quais atributos XDM são usados em públicos-alvo com mais de 10 perfis</li></ul> |
| Fluxos de dados - Insights operacionais | <ul><li>Para quais fluxos de dados contribuem {DATASET_NAME} conjunto de dados?</li><li>Quais fluxos de dados de origem não estão sendo usados ou não têm mais dados chegando?</li><li> |
| Conjuntos de dados - Insights operacionais | <ul><li>Quantos conjuntos de dados foram assimilados usando o mesmo esquema?</li><li>A qual conector de origem está associado {DATASET_NAME} conjunto de dados</li><li>Quais conjuntos de dados são usados em cada público-alvo?</li><li>Quais esquemas não são usados em nenhum conjunto de dados?</li><li>Quantos conjuntos de dados eu tenho?</li></ul> |
| Destinos - Insights operacionais | <ul><li>Quais destinos estão em um estado ativo?</li><li>Quais contas de destino têm 0 públicos-alvo ativados?</li><li> |
| Jornada - Insights operacionais | <ul><li>Quantas jornadas eu tenho?</li><li>Quais jornadas foram criadas em {RELATIVE_DATE} (por exemplo, semana passada) ou {RELATIVE_DATE} (por exemplo, antes/depois/em uma data específica)?</li><li>Mostre-me a lista de jornadas que foram modificadas em {RELATIVE_DATE} (por exemplo, semana passada) ou {RELATIVE_DATE} (por exemplo, antes/depois/em uma data específica)?</li><li>Listar as jornadas que eu tenho.</li><li>Liste os públicos-alvo que são usados em jornadas ativas.</li></ul> |
| Esquemas - Insights operacionais | <ul><li>Quais campos do esquema contribuíram para a maioria dos públicos-alvo?</li><li>Quantos esquemas são ativados por perfil?</li><li>Lista todos os esquemas modificados na última semana.</li><li>Quais esquemas não são usados em nenhum conjunto de dados?</li><li>Lista todos os esquemas criados na última semana.</li></ul> |
| Origens - Insights operacionais | <ul><li>Quais origens estão em um estado ativo?</li><li>Qual conector de origem está associado ao conjunto de dados {DATASET_NAME}?</li><li>Qual conector de origem tem o número mais alto de contas associadas?</li><li>Mostre-me os fluxos de dados e seus conectores de origem associados.</li></ul> |
| Aprendizado direcionado - Conhecimento do produto (Real-Time CDP e Journey Optimizer) | <ul><li>Com o que o Assistente de IA pode ajudar?</li><li>O que são públicos-alvo semelhantes?</li><li>Como os grupos de usuários estão relacionados às funções?</li><li>Quando devo usar um tipo de dados vs um grupo de campos?</li><li>Qual é a diferença entre uma identidade e uma chave primária ou estrangeira?</li><li>Como a riqueza do perfil é calculada?</li></ul> |
| Solução de problemas - Conhecimento do produto (Real-Time CDP e Journey Optimizer) | <ul><li>Com o que o Assistente de IA pode ajudar?</li><li>Posso excluir um esquema habilitado para perfil depois que os dados forem assimilados?</li><li>Por que não posso excluir um público-alvo?</li><li>Quanto tempo leva para que os públicos-alvo sejam avaliados e os resultados sejam disponibilizados para direcionamento?</li></ul> |

{style="table-layout:auto"}

## Formular suas perguntas {#phrasing-your-questions}

Você deve enviar suas perguntas ao Assistente de IA com clareza e contexto para obter uma resposta o mais precisa possível. Consulte a seguinte lista de dicas para obter orientação sobre como fazer uma pergunta clara com contexto:

* Apresente sua tarefa e/ou pergunta de maneira concisa.
* Evite linguagem ambígua ou sintaxe excessivamente complexa para facilitar a compreensão.
* Forneça contexto relevante em relação à sua tarefa e/ou pergunta, pois o contexto pode ajudar o Assistente de IA a gerar respostas mais relevantes.

Leia as tabelas abaixo para obter mais orientações sobre as práticas recomendadas a serem seguidas ao fazer perguntas ao Assistente de IA.

As tabelas a seguir descrevem as práticas recomendadas que você pode seguir ao usar o Assistente de IA:

| Fazer | Exemplo |
| --- | --- |
| <ul><li>Seja específico sobre o objeto ou as informações que deseja recuperar ou analisar.</li><li>Tente colocar os nomes dos objetos de dados entre aspas. Se você souber apenas uma parte do nome do objeto, também poderá especificá-lo na pergunta.</li><li>Uso [preenchimento automático do objeto](./ui-guide.md#use-auto-complete) para ajudar o Assistente de IA a entender melhor o contexto da consulta.</li></ul> | <ul><li>Quais conjuntos de dados usam o esquema &quot;Luma - Fidelidade&quot;?</li><li>Mostre-me os segmentos ativados que têm &quot;Luma&quot; em seus nomes. Classificá-los por contagem de perfis.</li></ul> |
| <ul><li>Evite ambiguidades e use linguagem clara</li><li>Use terminologia precisa para garantir mais clareza em seu query.</li><li>Ao fazer perguntas sobre o Adobe Experience Platform, tente usar a terminologia específica do Experience Platform para melhorar a relevância das respostas.</li></ul> | <ul><li>Quantos perfis eu tenho em &quot;ACME Audience&quot;.</li><li>Mostre-me os 5 principais atributos XDM usados em públicos ativados.</li></ul> |
| <ul><li>Forneça contexto ou especifique um critério para filtrar os resultados.</li><li>Use um critério de filtro nas perguntas para limitar o volume de dados na resposta.</li></ul> | <ul><li>Mostre-me públicos que não foram ativados e foram criados há mais de 6 meses e que nunca foram modificados.</li><li>Mostre-me públicos ativados para &quot;ACME Destination&quot; e têm mais de 10000 perfis.</li></ul> |

{style="table-layout:auto"}

| Não | Exemplo |
| --- | --- |
| Use uma linguagem vaga ou ambígua. | <ul><li>Forneça-me informações sobre conjuntos de dados.</li><li>Quantos usuários eu tenho em &quot;ACME Audience&quot;?</li><li>Mostrar segmentos.</li><li>Listar atributos.</li></ul> |
| Faça solicitações incompletas. | &quot;Luma - Conjunto de dados de fidelidade&quot; |
| Assumir conhecimento sem contextos. | <ul><li>Públicos nos últimos 6 meses.</li><li>Criar uma consulta para mim.</li></ul> |
| Formular consultas muito complexas. | Fornecer uma análise abrangente da linhagem de dados em todos os objetos e suas dependências. |
| Omitir critérios ou parâmetros. | Mostre-me conjuntos de dados. |

{style="table-layout:auto"}

## Próximas etapas

Após a leitura deste documento, você compreenderá como otimizar suas perguntas para o Assistente de IA. Para obter informações sobre como usar o recurso durante os workflows, leia o [Guia da interface do assistente de IA](ui-guide.md).
