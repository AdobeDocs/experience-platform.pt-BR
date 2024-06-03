---
title: Visão geral do Assistente de IA no Adobe Experience Platform
description: Saiba mais sobre o AI Assistant, suas nuances e casos de uso e como você pode usá-lo para acelerar seu fluxo de trabalho com o Adobe Experience Platform e o Real-time Customer Data Platform.
hide: true
hidefromtoc: true
source-git-commit: fe87a487079f5154f238b2d425cdd249a4724762
workflow-type: tm+mt
source-wordcount: '2294'
ht-degree: 0%

---

# Assistente de IA no Adobe Experience Platform

Leia este documento para saber mais sobre o Assistente de IA na Adobe Experience Platform.

O Assistente de IA no Adobe Experience Platform é uma experiência de conversação que você pode usar para acelerar seus fluxos de trabalho em aplicativos Adobe. Você pode usar o AI Assistant para entender melhor o conhecimento do produto, solucionar problemas ou pesquisar informações e encontrar insights operacionais. O Assistente de IA é compatível com Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer e Customer Journey Analytics.

>[!IMPORTANT]
>
>* Você deve concordar com [um contrato de usuário](https://adobe.sharepoint.com/:w:/s/ExCUserExperience/EVzJv1jFBiZGnaFEufsfIqwBC_9ehv3KaXTkEMTGpQFRpg?e=qzwOo8) antes de usar o Assistente de IA. O contrato de usuário também contém o contrato público beta. Para que você possa usar os recursos adicionais do Assistente de IA à medida que eles forem implantados na capacidade beta.

![A interface do Assistente de IA com a experiência do usuário acionada pela primeira vez.](./images/blank.png)

## Entendendo o assistente de IA {#understanding-ai-assistant}

O Assistente de IA responde às perguntas enviadas consultando um banco de dados e, em seguida, traduzindo os dados do banco de dados em uma resposta legível.

Essa representação interna de dados subjacentes também é conhecida como **[!DNL Knowledge Graph]** - uma ampla rede de conceitos, dados e metadados para uma determinada resposta.

A variável [!DNL Knowledge Graph] consiste em subgráficos que são referenciados sempre que as consultas são enviadas:

* Insights operacionais do cliente.
* Insights operacionais do cliente em várias meta lojas.
* Documentação do Experience League.

Há duas classes de perguntas a serem consideradas antes de consultar o Assistente de IA:

### Conhecimento do produto {#product-knowledge}

O conhecimento do produto refere-se aos conceitos e tópicos baseados na documentação do Experience League. As perguntas sobre o conhecimento do produto podem ser especificadas mais detalhadamente nos seguintes subgrupos:

| Conhecimento do produto | Exemplos |
| --- | --- |
| Aprendizado apontado | <ul><li>Qual é a diferença entre uma identidade e uma chave primária ou estrangeira?</li><li>Como a riqueza do perfil é calculada?</li></ul> |
| Abrir descoberta | <ul><li>Como posso exportar esse conjunto de dados?</li><li>Existem esquemas para clientes de assistência médica?</li></ul> |
| Solução de problemas | <ul><li>Por que não posso ativar um esquema de propriedade do Adobe para perfil?</li><li>Por que não posso excluir um segmento?</li></ul> |

{style="table-layout:auto"}

### Insights operacionais {#operational-insights}

>[!IMPORTANT]
>
>As respostas dos insights operacionais estão na versão beta. Qualquer pessoa que tenha acesso à **Exibir Insights Operacionais** A permissão do terá acesso às respostas dos insights operacionais.

Os insights operacionais se referem às respostas que o AI Assistant gera sobre os objetos de metadados (atributos, públicos, fluxos de dados, conjuntos de dados, destinos, jornadas, esquemas e fontes), incluindo contagens, pesquisas e impacto de linhagem. Ele não analisa dados na sandbox.

* Quantos conjuntos de dados eu tenho?
* Quantos atributos de esquema nunca foram usados?
* Quais públicos-alvo foram ativados?

Você pode fazer perguntas ao Assistente de IA sobre seus insights operacionais nos seguintes domínios:

* Atributos
* Públicos-alvo
* Fluxos de dados
* Conjuntos de dados
* Destinos _(Perguntas sobre contas e algumas perguntas sobre fluxo de dados não podem ser respondidas no momento.)_
* Jornadas
* Esquemas _(Perguntas relacionadas a grupos de campos não podem ser respondidas neste momento.)_
* Origens _(Perguntas relacionadas a contas não podem ser respondidas neste momento.)_

Para perguntas sobre insights operacionais, as respostas podem não refletir o estado atual da interface do usuário. Os dados que sustentam essas perguntas são atualizados uma vez a cada 24 horas. Por exemplo, as alterações que os usuários fazem no Real-Time CDP durante o dia são sincronizadas com os armazenamentos de dados à noite e, em seguida, ficam disponíveis para perguntas do usuário de manhã. Você precisará fazer logon em uma sandbox para consultar sobre dados específicos relacionados a objetos.

## Acesso ao recurso {#feature-access}

O acesso ao AI Assistant é regido pelos seguintes parâmetros:

* **Acesse o aplicativo:** Você pode acessar o Assistente de IA no Adobe Experience Platform, Adobe Real-Time CDP, Adobe Journey Optimizer e [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant).
* **Acesso contratual:** Sua empresa deve concordar com determinados [!DNL GenAI]Termos legais relacionados ao antes que sua organização possa usar o Assistente de IA. Entre em contato com o administrador da organização ou com a equipe de conta do Adobe se não conseguir acessar o Assistente de IA.
* **Permissões:** Use o [Interface de permissões](../access-control/abac/ui/permissions.md) para conceder ou revogar o acesso ao Assistente de IA na sua organização. Para usar o Assistente de IA, um determinado usuário deve pertencer a uma função provisionada com o **Habilitar o assistente de IA** e **Exibir Insights Operacionais** permissões.
   * Como administrador, você pode adicionar a variável **Habilitar o assistente de IA** a uma determinada função e adicionar um usuário a essa função, para permitir que eles acessem o Assistente de IA na organização.
   * Como administrador, você pode adicionar a variável **Exibir Insights Operacionais** a uma determinada função e adicionar um usuário a essa função, para permitir que eles usem os recursos de insights operacionais do Assistente de IA. Os insights operacionais estão atualmente na versão beta.

![A página da interface de permissões com as permissões Ativar assistente de IA e Exibir insights operacionais incluídas em uma determinada função.](./images/permissions.png)

## Exemplo de perguntas {#example-questions}

Esta seção descreve exemplos de perguntas que você pode consultar durante os workflows. As perguntas são agrupadas em três seções: insights operacionais, objetivos e objetos.

### Exemplo de perguntas agrupadas por insights operacionais {#operational-insights-questions}

+++Selecione para exibir exemplos de perguntas de insights operacionais e seus respectivos casos de uso:

| Tipo de pergunta | Caso de uso | Exemplos |
| --- | --- | --- | 
| Linhagem de dados | Rastrear o uso de um ou vários objetos em outros objetos Experience Platform | <ul><li>Quais conjuntos de dados usam o esquema &quot;ACME schema&quot;?</li><li>Quantos conjuntos de dados foram assimilados usando o mesmo esquema?</li><li>Quais conjuntos de dados foram usados nos públicos ativados?</li><li>Liste os esquemas que têm atributos usados em públicos ativados.</li><li>Mostre os públicos que são ativados para &quot;ACME Destinations&quot; e têm mais de 1000 perfis.</li><li>Mostre os atributos usados nos públicos ativados que foram modificados após janeiro de 2023.</li><li>Quais são os conjuntos de dados assimilados pela fonte &quot;ACME Amazon S3&quot;?</li><li>Quais fluxos de dados estão associados ao &quot;Fluxo de dados de fidelidade do ACME&quot;?</li><li>Liste os esquemas relacionados a públicos ativados e que foram criados nos últimos 1 ano.</li></ul> |
| Distribuição e agregações | Perguntas baseadas em resumo sobre o uso do objeto Experience Platform | <ul><li>Qual é a porcentagem de públicos ativados?</li><li>Quantos campos são usados na segmentação?</li><li>Quais públicos-alvo são ativados para o maior número de destinos?</li><li>Listar públicos duplicados.</li><li>Mostre-me os públicos ativados para &quot;ACME Destinations&quot; e classifique-os por tamanho de perfil.</li><li>Qual é a porcentagem dos públicos-alvo que não foram ativados, mas têm mais de 100 perfis. Mostre-me os nomes deles.</li><li>Listar os 3 conectores de origem que assimilam dados nos meus conjuntos de dados.</li><li>Liste os 5 principais atributos usados em públicos ativados com base em sua ocorrência.</li></ul> |
| Pesquisa de objeto | Recupere ou acesse um objeto Experience Platform ou suas propriedades. | <ul><li>Quais conjuntos de dados não têm nenhum esquema associado a eles</li><li>Listar os atributos usados para o &quot;Público-alvo da ACME&quot;?</li><li>Forneça a lista de esquemas que estão habilitados para perfil, mas que não foram modificados desde sua criação.</li><li>Quais públicos-alvo foram modificados na semana passada?</li><li>Liste os públicos-alvo que têm as mesmas definições de segmento, juntamente com a data de criação.</li><li>Quais conjuntos de dados são ativados por perfil e também incluem quantos públicos-alvo foram criados de cada conjunto de dados.</li><li>Quais contas de origem estão associadas ao conjunto de dados XYZ?</li><li>Mostre-me a definição de segmento e a data de modificação de &quot;Público-alvo da ACME&quot;.</li></ul> |
| Comparação de objetos | Identifique públicos-alvo duplicados. | <ul><li>Com base na definição de segmento, liste os públicos-alvo que são duplicados.</li><li>Quais públicos-alvo duplicados são ativados para &quot;Destinos ACME&quot;.</li></ul> |

{style="table-layout:auto"}

+++

### Exemplo de perguntas agrupadas por objetivos {#objectives-questions}

+++Selecione para exibir uma lista de objetivos que você pode realizar com o Assistente de IA

| Objetivo | Descrição | Exemplo |
| --- | --- | --- |
| Conceitos de aprendizado e fluxos de trabalho contínuos | <ul><li>Como usuário iniciante, você pode usar o AI Assistant para aprender conceitos do Real-Time CDP e do Adobe Journey Optimizer e integrar-se a produtos e recursos com os quais não está familiarizado.</li><li>Como um usuário experiente, você pode usar o AI Assistant para resolver um caso de borda que pode estar bloqueando seu fluxo de trabalho. | <ul><li>Como configurar um painel no Jornada Analytics?</li><li>Conte-me alguns casos de uso para o Real-Time CDP.</li></ul> |
| Solução de problemas | Use o Assistente de IA para saber como depurar erros básicos que você pode encontrar no fluxo de trabalho. | <ul><li>O que faz esse erro {ERROR_MESSAGE} quer dizer?</li><li>Por que não consigo excluir o público-alvo chamado &quot;Luma: Público-alvo de email&quot;?</li></ul> |
| Higiene da sandbox | Use o Assistente de IA para identificar objetos duplicados ou não utilizados, para que você possa manter sua sandbox com eficiência. | <ul><li>Você pode me mostrar públicos semelhantes?</li><li>Há esquemas que não tenham um conjunto de dados associado?</li></ul> |
| Análise de valor | Use o Assistente de IA para identificar os objetos de dados mais usados e avaliar os indicadores de desempenho ou encontrar os objetos de dados mais valiosos. | <ul><li>Quantos perfis estão em nossa definição de segmento &quot;Luma: Público-alvo de email&quot;?</li><li>Quando os públicos-alvo foram ativados para o destino do Experience Cloud Audiences?</li></ul> |
| Pesquisa | Use o AI Assistant para encontrar objetos de Experience Platform compatíveis, como públicos-alvo, conjuntos de dados, destinos, esquemas e fontes. | <ul><li>Liste os públicos-alvo que contêm &quot;Luma&quot; no nome que foram criados no último trimestre.</li><li>Quais atributos estão no esquema XDM &quot;Luma: Ações personalizadas&quot;?</li></ul> |
| Análise de impacto | Use o Assistente do AI para identificar objetos de dados que foram usados em determinados workflows para que você possa avaliar o impacto de quaisquer alterações. | <ul><li>Quais públicos-alvo usam `homeAddress.city` no esquema &quot;Luma: PersonProfiles&quot;?</li><li>Quais conjuntos de dados são os `consents.marketing.push.val` atributo de perfil armazenado em?</li></ul> |

{style="table-layout:auto"}

+++

### Exemplo de perguntas agrupadas por objetos {#objects-questions}

+++Selecione para exibir a lista de perguntas de exemplo com as quais o Assistente de IA pode ajudá-lo:

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

+++

## Formular suas perguntas {#phrasing-your-questions}

Você deve enviar suas perguntas ao Assistente de IA com clareza e contexto para obter uma resposta o mais precisa possível. Consulte a seguinte lista de dicas para obter orientação sobre como fazer uma pergunta clara com contexto:

* Apresente sua tarefa e/ou pergunta de maneira concisa.
* Evite linguagem ambígua ou sintaxe excessivamente complexa para facilitar a compreensão.
* Forneça contexto relevante em relação à sua tarefa e/ou pergunta, pois o contexto pode ajudar o Assistente de IA a gerar respostas mais relevantes.

Leia as tabelas abaixo para obter mais orientações sobre as práticas recomendadas a serem seguidas ao fazer perguntas ao Assistente de IA.

+++Selecione para exibir exemplos de práticas recomendadas a serem seguidas ao formular suas perguntas

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

+++

## Próximas etapas

Agora que você tem uma compreensão geral do Assistente de IA, pode continuar e usar o Assistente de IA durante seus fluxos de trabalho. Consulte a seguinte documentação para obter mais informações:

* [Guia da interface do assistente de IA](./ui-guide.md)
* [Privacidade, segurança e governança no Assistente de IA](./privacy.md)
* [Perguntas frequentes](./faq.md)