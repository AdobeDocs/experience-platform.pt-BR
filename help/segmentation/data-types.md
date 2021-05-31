---
keywords: Experience Platform; home; tópicos populares; tipo de dados; tipos de dados; Tipo de dados; Tipo de dados; Tipos de dados de segmentação; Segmentação; Segmentação; Serviço de segmentação; tipos de dados do serviço de segmentação;
solution: Experience Platform
title: Tipos de dados compatíveis no serviço de segmentação
topic-legacy: overview
description: Todos os tipos de dados do Experience Data Model (XDM) são suportados no Serviço de segmentação do Adobe. As regras que constituem uma definição de segmento são contextualizadas pelos seguintes tipos de dados.
exl-id: 73f932a7-f864-4566-ade7-c148a12dc83c
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 1%

---

# Tipos de dados compatíveis no Serviço de segmentação

Todos os tipos de dados do Experience Data Model (XDM) são compatíveis com o Serviço de segmentação da Adobe Experience Platform. As regras que constituem uma definição de segmento são contextualizadas pelos seguintes tipos de dados.

## Dados da string

As definições de segmento usam dados de string para definir restrições não numéricas para públicos de segmento, como &quot;nome do país&quot; ou &quot;nível de programa de fidelidade&quot;.

Os dados da string são incluídos nas definições do segmento usando declarações lógicas, inclusivas/exclusivas e de comparação. Depois que um atributo de string é adicionado à definição do segmento, você pode usar instruções relevantes à string para avaliá-lo em relação a outros campos de string.

| Tipo de instrução | Exemplos |
| -------------- | -------- |
| Lógica | `and`, `or`, `not` |
| Inclusivo/exclusivo | `include`, `must` `exist`, `exclude`, `must not exist` |
| Comparação | `equals`,  `does not equal`,  `contains`,  `starts with` |

## Dados da data

Os dados de data permitem atribuir o contexto com base no tempo às definições do segmento, usando datas de início/término específicas ou usando declarações relevantes à data, conforme mostrado na tabela abaixo. Uma implementação pode ser a criação de um público-alvo de clientes que interagiram com sua marca a qualquer momento *este ano* e também esteve ativo *dentro* nos últimos dias.

| Exemplo de campo | Declarações relevantes para a data | Linha do tempo |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`,  `yesterday`,  `this month`,  `this year` | Relevante para o dia em que o segmento foi criado. |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | Relevante em qualquer semana/mês. |

## Eventos de experiência

Como um esquema Adobe Experience Platform, [!DNL XDM ExperienceEvents] registre interações explícitas e implícitas com aplicativos [!DNL Platform] integrados, incluindo um instantâneo do sistema no momento em que a interação ocorreu. [!DNL ExperienceEvents] são registros de fatos. Dessa forma, elas são uma fonte de dados disponível para você durante a definição do segmento.

Conforme visto na tabela abaixo, os dados do evento são renderizados usando palavras-chave que ajudam a refinar o comportamento do evento e especificar atributos do evento.

| Palavra-chave | Use |
| ------- | --- |
| Incluir/excluir | Descreve o comportamento do evento por meio da inclusão ou omissão de dados. |
| Qualquer/todos | Ajuda a determinar o número de segmentos qualificados. |
| Botão de alternância &quot;Aplicar regra de tempo&quot; | Incorpora dados de data. |
| É igual a, não é igual, começa com, não começa com, termina com, não termina com, contém, não contém, existe, não existe | Incorpora dados de string. |

### Compartilhamento de público

Públicos externos também podem ser usados como componentes de uma nova definição de segmento, adicionando suas regras de atributo ao novo segmento.

Atualmente, somente o Adobe Audience Manager é compatível como um público externo, com fontes adicionais ativadas no futuro. Mais informações sobre o uso de públicos do Adobe Audience Manager com a Platform podem ser encontradas no [guia de compartilhamento de público-alvo na documentação do Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html).

### Compartilhamento de segmentos

Os segmentos criados na plataforma podem ser usados em outros [Serviços principais da Adobe Experience Cloud](https://experienceleague.adobe.com/docs/core-services/interface/experience-cloud.html). Para ativar esse recurso, você precisará entrar em contato com o arquiteto da solução ou com seu consultor.

## Outros tipos de dados

Além dos tipos de dados mencionados acima, a lista de tipos de dados compatíveis também inclui:

- Identificador de recurso uniforme (URI)
- Enum
- Número
- Longo
- Número inteiro
- Curto
- Byte
- Booleano
- Matriz
- Objeto
- Mapa
