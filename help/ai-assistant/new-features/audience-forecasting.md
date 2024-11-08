---
title: Monitoramento de alterações significativas e previsão de público-alvo com o Assistente de IA
description: Saiba como usar o Assistente de IA para monitorar alterações significativas e prever públicos no Adobe Experience Platform.
badge: Alfa
source-git-commit: 37d2886cc5d7b3a019d23f76973d79547865298b
workflow-type: tm+mt
source-wordcount: '1909'
ht-degree: 0%

---

# Monitore alterações significativas e preveja o crescimento do público com o Assistente de IA

>[!AVAILABILITY]
>
>Esse recurso está na Alpha e pode não estar disponível para sua organização. Para participar do programa Alpha e acessar esse recurso, entre em contato com a equipe de conta do Adobe.

No cenário de marketing orientado por dados de hoje, insights oportunos e precisos são essenciais. Seja você um usuário empresarial ou em operações de marketing, precisa da capacidade de interagir consistentemente com seus públicos-alvo e fazer ajustes rápidos e impactantes com base em insights claros. Para manter o alinhamento ou atingir suas metas de negócios, você deve ter as informações acionáveis necessárias para impulsionar campanhas eficazes e otimizar recursos.

Você pode usar o AI Assistant para Adobe Experience Platform a fim de monitorar alterações significativas e fornecer previsões de crescimento para seu público-alvo e tamanhos de conjunto de dados. Você pode então usar essas informações para garantir a integridade dos dados do público-alvo e oferecer projeções prospetivas para dar suporte à tomada de decisões com base em dados.

Leia este documento para saber como monitorar alterações significativas e prever o crescimento e as flutuações do público-alvo usando o Assistente de IA.

## Terminologia e definições principais {#key-terminology-and-definitions}

Consulte a tabela a seguir para obter uma lista de terminologias importantes e suas definições correspondentes.

| Terminologia | Definição |
| --- | --- |
| Mudança significativa | Uma alteração significativa é uma grande alteração baseada em porcentagem no público-alvo ou no tamanho do conjunto de dados, definida por limites específicos (por exemplo, 10% para públicos-alvo grandes). Alterações significativas ajudam a identificar anomalias que afetam a estabilidade dos dados. |
| Anomalias | As anomalias são variações inesperadas nos dados, como um crescimento súbito de 20% em um público de **Compradores de alto valor**. Uma anomalia pode ser causada por um problema potencial de assimilação de dados ou por uma alteração na definição do público-alvo. |
| Dados Históricos | Os dados históricos referem-se a dados de longo prazo, geralmente de um a três anos. Você pode usar dados históricos para rastrear padrões. **Observação**: durante o estágio de Alpha, o Assistente de IA fornece dados históricos de até 13 meses. |
| Dados emergentes/recentes | Dados emergentes ou recentes se referem a pontos de dados observados por um curto período, normalmente por uma semana ou até 30 dias. Você pode usar dados emergentes ou recentes para destacar tendências imediatas e fazer ajustes rápidos. |
| Previsão | As previsões são previsões de público-alvo futuro ou tamanhos de conjuntos de dados com base em tendências passadas. Você pode usar os dados de previsão para suportar o planejamento de longo prazo. |
| Tamanho do público-alvo | O tamanho do público refere-se ao número total de perfis em um público-alvo. O tamanho do público é atualizado a cada iteração de assimilação de dados. |
| Período de comparação | O Assistente de IA usa intervalos de tempo de comparação predefinidos. As anomalias recentes assumem o padrão de um retrospectivo de sete dias, enquanto as anomalias anteriores cobrem 30 dias. As tendências históricas abrangem até 13 meses. |

{style="table-layout:auto"}

## Exemplos de caso de uso {#use-case-examples}

A capacidade do Assistente de IA de monitorar alterações significativas e prever públicos pode ser particularmente útil para os seguintes casos de uso:

### Operações de marketing

Os profissionais de operações de marketing (ops de marketing) são responsáveis por garantir a integridade e a consistência dos dados do público-alvo. Como membro de uma equipe de operações de marketing, suas responsabilidades podem incluir o monitoramento da qualidade dos dados, a resposta a mudanças inesperadas e a manutenção de uma base estável para todos os esforços de marketing. Você pode usar a detecção de anomalias do Assistente de IA para detectar e solucionar alterações significativas no público-alvo ou no conjunto de dados, evitando assim interrupções que podem afetar o desempenho da campanha.

### Usuários empresariais e profissionais de marketing

Como usuário empresarial e profissional de marketing, você pode confiar em insights precisos do público-alvo para tomar decisões orientadas por dados e garantir que suas campanhas atinjam seus públicos-alvo desejados de maneira eficaz. Com os recursos de previsão do Assistente de IA, é possível antecipar o crescimento ou a redução do público-alvo e habilitar ajustes estratégicos em recursos e direcionamento ao longo do tempo.

## Recursos principais

>[!IMPORTANT]
>
>Os seguintes recursos estão em Alpha e estão focados em recursos essenciais de monitoramento e previsão. Como esse recurso está no Alpha, você deve verificar novamente a precisão das respostas recebidas do Assistente de IA.

### Monitorar alterações significativas no público-alvo e nos dados

Você pode usar o Assistente de IA para identificar alterações significativas no tamanho do público-alvo e do conjunto de dados, rastreando desvios dos padrões típicos. Cada alteração significativa é baseada em limites predefinidos de acordo com a escala do público-alvo.

| Tamanho do público-alvo | Número de perfis | Descrição |
| --- | --- | --- |
| Pequenos públicos-alvo | 1 a 100.000 perfis | Sinaliza uma alteração de 30% ou mais, a menos que uma porcentagem específica seja especificada. |
| Públicos da Medium | 100.000 a 500.000 perfis | Sinaliza uma alteração de 25% ou mais, a menos que uma porcentagem específica seja especificada. |
| Grandes públicos-alvo | 500.000 a 1 milhão de perfis | Sinaliza uma alteração de 20% ou mais, a menos que uma porcentagem específica seja especificada. |
| Públicos muito grandes | Mais de 1 milhão de perfis | Sinaliza uma alteração de 10% ou mais, a menos que uma porcentagem específica seja especificada. |

{style="table-layout:auto"}

>[!BEGINSHADEBOX]

#### Exemplo de cenário

Alterações significativas indicam anomalias que podem afetar a estabilidade do público ou a confiabilidade dos dados. Por exemplo, se um público-alvo de **Compradores de alto valor** sofrer uma queda repentina de 15% no tamanho, o Assistente de IA sinalizará isso como uma alteração significativa. Você pode usar essas informações para investigar e resolver possíveis problemas antes que eles afetem suas campanhas.

>[!ENDSHADEBOX]

>[!TIP]
>
>O Assistente de IA não notifica automaticamente a ocorrência de alterações significativas no tamanho do público-alvo. Você deve iniciar uma conversa com o Assistente de IA e perguntar quais públicos-alvo foram alterados significativamente ou por uma margem específica, em um período específico.

### Previsão do crescimento do público-alvo e do conjunto de dados

Você pode usar o Assistente de IA para fazer referência a tendências de dados históricos e projetar públicos-alvo futuros e tamanhos de conjuntos de dados. Você pode usar esses insights para apoiar o planejamento de recursos e os ajustes de estratégia. Atualmente, você pode usar o Assistente de IA para prever o crescimento do público-alvo e do conjunto de dados por 30 dias. Ao entender o crescimento ou o declínio esperado do público-alvo, é possível ajustar as estratégias de direcionamento e alocar os recursos de acordo.

### Insights sobre tamanhos históricos de público

Além de detectar alterações significativas, você pode usar o Assistente de IA para recuperar insights históricos e comparar o público-alvo ou o tamanho do conjunto de dados atual com os dados anteriores. Esse recurso oferece suporte ao rastreamento de tendências de longo prazo e à avaliação do impacto de atividades de marketing anteriores.

Você pode fazer perguntas sobre o Assistente de IA, como &quot;Qual era o tamanho do meu público-alvo de &quot;Clientes de fidelidade&quot; no mês passado? para ver dados históricos sobre o crescimento ou o declínio desse público específico.

## Exemplo de perguntas para monitorar alterações significativas

Você pode enquadrar as perguntas do Assistente de IA de várias maneiras.

* Se a sua pergunta incluir uma porcentagem, como **&quot;Quais públicos-alvo mudaram em 30% ou mais?&quot;**, o Assistente de IA usará a porcentagem como um ponto de referência.
* Se a pergunta não especificar uma porcentagem, o AI Assistant interpretará as alterações significativas com base nas configurações padrão.

Consulte as tabelas a seguir para obter exemplos de consultas que ilustram como o Assistente de IA interpreta alterações significativas com base no tamanho do público-alvo:

| Informações de público ou alteração de público | Exemplo |
| --- | --- |
| <ul><li>Qual é o tamanho atual de {AUDIENCE_NAME}?</li><li>Mostre os públicos que apresentaram uma mudança de {PERCENT} em {DATE_DURATION}.</li></ul> | <ul><li>Qual é o tamanho atual do público-alvo de compradores de alto valor?</li><li>Mostre os públicos que mostraram uma mudança de 20% na última semana.</li></ul> |

{style="table-layout:auto"}

| Consultas específicas do público | Exemplo |
| --- | --- |
| <ul><li>Quais públicos foram alterados além de {PERCENT} em {DATE_OR_DURATION}?</li><li>Mostre-me públicos-alvo com uma mudança significativa em relação a {DATE_OR_DURATION}.</li><li>Mostre-me a distribuição de públicos com as maiores alterações em {DATE_OR_DURATION}.</li><li>Mostre-me os públicos que diminuíram mais de {PERCENT} em {DATE_OR_DURATION}.</li></ul> | <ul><li>Quais públicos-alvo mudaram mais de 20% na última semana?</li><li>Mostre-me os públicos-alvo com uma mudança significativa nos últimos seis meses.</li><li>Mostre-me a distribuição de públicos-alvo com as maiores alterações de 1º de outubro a 31 de outubro.</li><li> Mostre-me públicos que diminuíram mais de 20% desde 31 de agosto. |

{style="table-layout:auto"}

## Informações adicionais

### Compreender o limite de &quot;alteração significativa&quot;

Você pode especificar uma porcentagem específica ao consultar o Assistente de IA para obter informações sobre alterações significativas. Se você não fornecer uma porcentagem específica, o AI Assistant referenciará um conjunto predefinido de limites para determinar o que se qualifica como uma alteração significativa. Os limites padrão são baseados no tamanho de um determinado público-alvo. Consulte a tabela a seguir para obter informações sobre o que constitui uma alteração significativa, com base no tamanho do público-alvo:

| Tamanho do público-alvo | O que é significativo? |
| --- | --- |
| 1 milhão ou mais | 10% ou mais |
| 500k a 1 milhão | 20% ou mais |
| 100k a 500k | 25% ou mais |
| Menos de 100k | 30% ou mais |

### Linhas do tempo genéricas e datas específicas

O Assistente de IA suporta comparações específicas e genéricas baseadas em tempo para tamanhos de público-alvo, interpretando-as com base no contexto fornecido na consulta.

>[!BEGINTABS]

>[!TAB Linhas de tempo genéricas]

As linhas do tempo genéricas se referem a consultas que usam idioma, como &quot;esta semana&quot; ou &quot;semana passada&quot;. Se você fizer uma pergunta como &quot;Quais públicos foram alterados em mais de 20% na semana passada?&quot;, o AI Assistant calculará e comparará o tamanho de **público-alvo médio** durante o período especificado.

Use essa abordagem para obter uma visão mais ampla das alterações de público-alvo ao longo do tempo, permitindo compreender melhor as tendências em intervalos semanais ou mensais.

>[!TAB Datas específicas]

Se a sua pergunta fizer referência a uma data específica, o AI Assistant comparará os **tamanhos exatos de público-alvo** em cada uma das datas fornecidas.

Use essa comparação precisa para analisar as alterações entre pontos específicos no tempo e esclarecer como o tamanho do público-alvo pode evoluir em dias específicos.

>[!ENDTABS]

Você pode aproveitar essa flexibilidade para entender melhor a dinâmica do público-alvo em intervalos de tempo amplos e precisos. Se você estiver rastreando tendências gerais ou examinando mudanças exatas entre datas específicas, é possível usar o mecanismo adaptável do Assistente do AI para recuperar a comparação mais relativa para sua consulta.

## Perguntas frequentes {#faq}

Leia esta seção para obter respostas a perguntas frequentes sobre o monitoramento de alterações significativas e a previsão de público-alvo com o Assistente de IA.

### Quantos dados históricos posso ver para ver se o tamanho do público aumenta ou diminui?

O Assistente de IA retém 12 meses de dados históricos de tamanho de público. Você pode fazer perguntas sobre as alterações de público-alvo nesse período para entender os padrões de crescimento ou declínio no ano passado.

### Até que ponto eu posso voltar na história para ver as mudanças de público?

O Assistente de IA rastreia as alterações de público-alvo a partir do dia em que é ativado em sua organização e retorna até a última alteração na definição de público-alvo. Depois de ativado, o AI Assistant monitora e registra continuamente as alterações de definição por até 12 meses, permitindo rastreamento e comparação futuros de dados.

### Quantos dados históricos são necessários para uma previsão?

São necessários pelo menos 30 dias de dados para fazer uma previsão confiável a partir da última alteração na definição do público-alvo. Em certos casos, como a previsão para [!DNL Black Friday], o Assistente de IA pode precisar de até 12 meses de dados históricos.

### Como o Assistente de IA interpreta &quot;recentemente&quot;?

O Assistente de IA interpreta &quot;recentemente&quot; como os últimos sete dias. Para perguntas que fazem referência a alterações recentes, o AI Assistant considera os dados desse período para identificar tendências ou turnos.

### Como o Assistente de IA compara os tamanhos de público-alvo?

Quando datas específicas são mencionadas, o Assistente de IA compara os tamanhos de público-alvo nesses dias específicos. Para perguntas mais gerais, como as que fazem referência aos &quot;últimos três meses&quot; ou à &quot;última semana&quot;, o Assistente de IA compara o tamanho médio desse período com a média do dia mais recente.

### Qual é a atualidade dos dados de público-alvo do Assistente de IA?

Pode levar de 24 a 48 horas para que o Assistente de IA atualize os dados do Real-time Customer Data Platform. Portanto, para perguntas que fazem referência a &quot;ontem&quot;, o Assistente de IA interpreta isso como um dia antes de os dados mais recentes que ele tem estarem disponíveis.

## Recursos fora do escopo

Os seguintes recursos não são suportados no momento:

### Análise avançada de causas básicas

Embora o Assistente de IA possa identificar alterações significativas, ele não pode, no momento, fornecer uma análise detalhada da causa principal dessas alterações. As iterações futuras do Assistente de IA têm como objetivo especificar quais conjuntos de dados ou atributos estão contribuindo para alterações significativas em seus públicos.

### Tamanhos abrangentes de conjuntos de dados históricos

O rastreamento histórico completo de tamanhos de dados não é suportado no momento. Atualmente, o Assistente de IA fornece histórico de público-alvo e conjunto de dados por até 13 meses.