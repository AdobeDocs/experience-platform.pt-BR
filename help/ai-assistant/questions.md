---
title: Guia de perguntas do Assistente de IA
description: Leia este documento para conhecer exemplos de perguntas que você pode usar ao consultar o Assistente de IA.
exl-id: d16d1262-cc2d-45c9-94c4-b86132183442
source-git-commit: 7268895d0b1924f9d3e7cee24e549c79245ef099
workflow-type: tm+mt
source-wordcount: '2105'
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
| Solução de problemas | Use o Assistente de IA para saber como depurar erros básicos que você pode encontrar no fluxo de trabalho. | <ul><li>O que este erro {ERROR_MESSAGE} significa?</li><li>Por que não consigo excluir o público-alvo chamado &quot;Luma: Público-alvo de email&quot;?</li></ul> |
| Higiene da sandbox | Use o Assistente de IA para identificar objetos duplicados ou não utilizados, para que você possa manter sua sandbox com eficiência. | <ul><li>Você pode me mostrar públicos semelhantes?</li><li>Há esquemas que não tenham um conjunto de dados associado?</li></ul> |
| Análise de valor | Use o Assistente de IA para identificar os objetos de dados mais usados e avaliar os indicadores de desempenho ou encontrar os objetos de dados mais valiosos. | <ul><li>Quantos perfis estão em nossa definição de segmento &quot;Luma: Público-alvo de email&quot;?</li><li>Quando os públicos-alvo foram ativados para o destino do Experience Cloud Audiences?</li></ul> |
| Pesquisa | Use o AI Assistant para encontrar objetos de Experience Platform compatíveis, como públicos-alvo, conjuntos de dados, destinos, esquemas e fontes. | <ul><li>Liste os públicos-alvo que contêm &quot;Luma&quot; no nome que foram criados no último trimestre.</li><li>Quais atributos estão no esquema XDM &quot;Luma: Ações personalizadas&quot;?</li></ul> |
| Análise de impacto | Use o Assistente do AI para identificar objetos de dados que foram usados em determinados workflows para que você possa avaliar o impacto de quaisquer alterações. | <ul><li>Quais públicos-alvo usam `homeAddress.city` no esquema &quot;Luma: PersonProfiles&quot;?</li><li>Em quais conjuntos de dados o atributo de perfil `consents.marketing.push.val` está armazenado?</li></ul> |

{style="table-layout:auto"}

## Insights operacionais por entidade e perguntas de conhecimento do produto{#objects-questions}

As perguntas a seguir são agrupadas por objetos de dados e são classificadas como [insights operacionais](./home.md#operational-insights) ou [conhecimento sobre o produto](./home.md#product-knowledge).

![](./images/prompt.png)

* **Públicos-alvo - Insights operacionais**
   * Quais públicos-alvo usam outros públicos-alvo?
   * Qual é a distribuição do número de perfis entre os públicos-alvo?
   * Mostre-me os públicos que foram modificados pela última vez antes de {RELATIVE_DATE}.
   * Quais públicos-alvo têm 0 perfis?
   * {USE_AUTO_COMPLETE_TO_FILL_AUDIENCE_NAME} está sendo usado em algum outro público-alvo?
* **Atributos - Insights operacionais**
   * Quais públicos-alvo têm o atributo xdm {ATTRIBUTE_PATH} na definição de seu segmento?
   * Quantos atributos de esquema XDM não são usados em nenhum público-alvo?
   * Quais esquemas contêm o atributo xdm {ATTRIBUTE_PATH}?
   * Quais atributos XDM são ativados?
   * Quais atributos XDM são usados em públicos-alvo com mais de 10 perfis?
* **Fluxos de dados - Insights operacionais**
   * Quais fluxos de dados contribuem para o conjunto de dados {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME}?
   * Quais fluxos de dados de origem não estão sendo usados ou não têm mais dados chegando?
   * Listar os fluxos de dados de origem que tenho.
   * Quais fluxos de dados são configurados para cada conector de origem?
* **Conjuntos de dados - Insights operacionais**
   * Quantos conjuntos de dados foram assimilados usando o mesmo esquema?
   * Qual conector de origem está associado ao conjunto de dados {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME}?
   * Quais conjuntos de dados são usados em cada público-alvo?
   * Quais esquemas não são usados em nenhum conjunto de dados?
   * Quantos conjuntos de dados eu tenho?
* **Destinos - Insights operacionais**
   * Quais destinos estão em um estado ativo?
   * Quais contas de destino têm 0 públicos-alvo ativados?
   * Quantos públicos-alvo são ativados para cada destino?
   * Quais destinos têm o maior número de públicos ativados?
* **Jornadas - Insights operacionais**
   * Quantas jornadas eu tenho?
   * Quais jornadas foram criadas em {RELATIVE_DATE} (por exemplo, a última semana) ou {RELATIVE_DATE} (por exemplo, antes/depois/em uma data específica)?
   * Mostrar a lista de jornadas que foram modificadas em {RELATIVE_DATE} (por exemplo, a última semana) ou {RELATIVE_DATE} (por exemplo, antes/depois/em uma data específica)?
   * Listar as jornadas ao vivo que eu tenho.
   * Liste os públicos-alvo que são usados em jornadas ativas.
* **Fontes - Insights operacionais**
   * Quais origens estão em um estado ativo?
   * Qual conector de origem está associado ao conjunto de dados {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME}.
   * Qual conector de origem tem o número mais alto de contas associadas?
   * Mostre-me os fluxos de dados e seus conectores de origem associados.
* **Aprendizado pontual - Conhecimento do produto (Real-Time CDP e Journey Optimizer)**
   * O que são públicos-alvo semelhantes?
   * Como os grupos de usuários estão relacionados às funções?
   * Quando devo usar um tipo de dados vs um grupo de campos?
   * Qual é a diferença entre uma identidade e uma chave primária ou estrangeira?
* **Solução de problemas - Conhecimento do produto (Real-Time CDP e Journey Optimizer)**
   * Em que o assistente de IA pode ajudar?
   * Posso excluir um esquema ativado por perfil depois que os dados forem assimilados?
   * Por que não posso excluir um público-alvo?
   * Quanto tempo leva para que os públicos-alvo sejam avaliados e os resultados sejam disponibilizados para direcionamento?

## Formular suas perguntas {#phrasing-your-questions}

Você deve enviar suas perguntas ao Assistente de IA com clareza e contexto para obter uma resposta o mais precisa possível. Consulte a seguinte lista de dicas para obter orientação sobre como fazer uma pergunta clara com contexto:

* Apresente sua tarefa e/ou pergunta de maneira concisa.
* Evite linguagem ambígua ou sintaxe excessivamente complexa para facilitar a compreensão.
* Forneça contexto relevante em relação à sua tarefa e/ou pergunta, pois o contexto pode ajudar o Assistente de IA a gerar respostas mais relevantes.

Leia as tabelas abaixo para obter mais orientações sobre as práticas recomendadas a serem seguidas ao fazer perguntas ao Assistente de IA.

As tabelas a seguir descrevem as práticas recomendadas que você pode seguir ao usar o Assistente de IA:

| Fazer | Exemplo |
| --- | --- |
| <ul><li>Seja específico sobre o objeto ou as informações que deseja recuperar ou analisar.</li><li>Tente colocar os nomes dos objetos de dados entre aspas. Se você souber apenas uma parte do nome do objeto, também poderá especificá-lo na pergunta.</li><li>Use o [preenchimento automático do objeto](./ui-guide.md#use-auto-complete) para ajudar o Assistente de IA a entender melhor o contexto da sua consulta.</li></ul> | <ul><li>Quais conjuntos de dados usam o esquema &quot;Luma - Fidelidade&quot;?</li><li>Mostre-me os segmentos ativados que têm &quot;Luma&quot; em seus nomes. Classificá-los por contagem de perfis.</li></ul> |
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

## Observabilidade do conjunto de dados {#dataset-observability}

O AI Assistant agora pode responder a perguntas sobre métricas específicas do conjunto de dados, como tamanho do armazenamento e contagem de linhas.

* Quais são meus maiores conjuntos de dados por tamanho?
* Quais são meus maiores conjuntos de dados por linhas?
* Quantos conjuntos de dados estão vazios?
* Quais conjuntos de dados estão vazios?

Além disso, você pode transmitir uma intenção semelhante por meio de várias variações para as quatro perguntas acima.

+++Selecione para exibir variações aceitas de perguntas de observabilidade do conjunto de dados

* Quais são os cinco principais conjuntos de dados por tamanho?
* Qual conjunto de dados tem o maior número de linhas?
* Quantos conjuntos de dados não têm dados?
* Listar os conjuntos de dados com tamanho >10 MB?
* Listar os conjuntos de dados com linhas menores que 10.
* Você pode me mostrar os conjuntos de dados que estão completamente vazios?
* Qual conjunto de dados é o maior por tamanho de armazenamento?
* Qual é o menor conjunto de dados em termos de contagem de linhas?
* Quantos dos meus conjuntos de dados têm dados e quantos estão vazios?
* Qual é a contagem de linhas do conjunto de dados chamado {DATASET_NAME}?
* Como o tamanho de {DATASET_NAME} se compara aos meus outros conjuntos de dados?
* Qual é o tamanho de {DATASET_NAME}?
* Quantas linhas {DATASET_NAME} tem?
* Qual é o tamanho e a contagem de linhas de {DATASET_NAME}?
* Você pode listar os maiores e menores conjuntos de dados por tamanho de armazenamento?

+++

Você também pode refinar suas perguntas de observabilidade de dados com um qualificador para filtrar sua consulta por um determinado período de tempo:

* Conjuntos de dados que recebem lotes nos últimos (x) dias
* Conjuntos de dados que não recebem lotes nos últimos (x) dias
* Conjuntos de dados com mais dados assimilados nos últimos (x) dias
* Contagem de registros de um conjunto de dados específico nos últimos (x) dias

+++Selecione para exibir variações aceitas de perguntas de observabilidade do conjunto de dados

* Quantos conjuntos de dados receberam lotes nos últimos (x) dias?
* Quais conjuntos de dados receberam lotes nos últimos (x) dias?
* Você pode listar os conjuntos de dados que tiveram dados assimilados nos últimos (x) dias?
* Quantos conjuntos de dados receberam novos lotes nos (x) dias anteriores?
* Quais são os conjuntos de dados que foram atualizados com novos dados nos últimos (x) dias?
* Listar conjuntos de dados que tiveram atividade em lote nos últimos (x) dias.
* Quantos conjuntos de dados não receberam lotes nos últimos (x) dias?
* Quais conjuntos de dados não receberam nenhum lote nos últimos (x) dias?
* Você consegue identificar conjuntos de dados sem assimilação de dados nos últimos (x) dias?
* Quantos conjuntos de dados não receberam atualizações nos últimos (x) dias?
* Quais conjuntos de dados ficaram inativos nos últimos (x) dias?
* Liste conjuntos de dados que não obtiveram novos lotes nos últimos (x) dias.
* Quando foi a última vez que os dados foram assimilados no conjunto de dados (x)?
* Quais são os 10 principais conjuntos de dados nos quais a maioria dos dados foi assimilada nos últimos (x) dias?
* Quais são os 10 principais conjuntos de dados por volume de dados assimilados nos últimos (x) dias?
* Quais foram os 10 conjuntos de dados que tiveram a maior assimilação de dados nos últimos (x) dias?
* Mostre os 10 principais conjuntos de dados com a maior assimilação de dados nos (x) dias anteriores.
* Quais são os principais conjuntos de dados por dados recebidos nos últimos (x) dias?
* Liste os 10 principais conjuntos de dados que assimilaram mais dados nos últimos (x) dias.
* Quantos registros foram recebidos no conjunto de dados (x), nos últimos (y) dias?
* Quantos registros o conjunto de dados (x) recebeu nos últimos (y) dias?
* Qual é a contagem de registros assimilada para o conjunto de dados (x) nos últimos (y) dias?
* Você pode fornecer o número de registros adicionados ao conjunto de dados (x) nos últimos (y) dias?
* Quantos dados foram recebidos por conjunto de dados (x) nos últimos (y) dias?
* Qual é o volume de registros assimilados para o conjunto de dados (x) nos (y) dias anteriores?

+++


## Exemplos de perguntas não suportadas {#unsupported-questions}

Veja a seguir uma lista de exemplos de perguntas que não são suportadas no momento pelo Assistente de IA.

+++Selecione para exibir exemplos de perguntas não suportadas

### Insights operacionais

* Quantos perfis nesta sandbox vivem na Califórnia? (**Observação**: para perguntas semelhantes, você deve fornecer um critério específico para fornecer contexto suficiente para a sua solicitação; neste caso, o critério específico é &quot;live in California&quot;).
* Quais são os segmentos deste perfil {PROFILE_INFO/ATTRIBUTE_VALUE}?
* Quantos perfis no conjunto de dados têm um email?
* Qual conjunto de dados constitui o número máximo de perfis nesta sandbox?
* Qual conjunto de dados tem o número mais alto de registros?
* Quantos segmentos foram excluídos em {RELATIVE_DATE}?
* Qual dos meus conjuntos de dados tem o maior tamanho?
* Dê-me um perfil no {AUDIENCE_NAME}.
* Qual é o número total de perfis em minha sandbox
* Quantos namespaces de identidade estão associados ao público-alvo {AUDIENCE_NAME}?
* Mostrar um relatório de todos os segmentos de público avaliados hoje
* Quantos segmentos têm perfis sobrepostos?
* Quantos lotes estão sendo carregados em {DATASET_NAME}
* Quantas ofertas ativas eu tenho?
* Quantas campanhas ativas eu tenho?
* De onde vêm minhas fontes de dados?
* Qual é o maior conjunto de dados ou fonte de dados?
* Posso obter a lista de usuários que criaram esses esquemas?

### Solução de problemas

* Por que esse lote {BATCH_NAME/BATCH_ID} ainda está sendo processado?
* Por que ninguém está qualificado para este público-alvo {AUDIENCE_NAME}?
* Não consigo ver a IA do cliente, por que e como faço para corrigi-la?
* Não consigo ver a visualização do conjunto de dados, por que e como faço para corrigi-lo?
* Por que não posso excluir {SEGMENT/DATASET/SCHEMA_NAME}?
* Tenho acesso ao Serviço de consulta?

### Tarefa e automação

* Escreva uma consulta que forneça um registro de {DATASET_NAME}.
* Grave uma chamada de API de exemplo em /schemas/{schemaId}/fields/{fieldPath}/values.
* Configurar uma origem/destino para mim.
* Criar uma audiência para mim com o critério {USER_SPECIFIC_CRITERIA}.

+++

## Próximas etapas

Após a leitura deste documento, você compreenderá como otimizar suas perguntas para o Assistente de IA. Para obter informações sobre como usar o recurso durante os fluxos de trabalho, leia o [guia da interface do assistente do AI](ui-guide.md).
