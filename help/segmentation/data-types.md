---
solution: Experience Platform
title: Tipos de dados compatíveis no serviço de segmentação
description: Todos os tipos de dados do Experience Data Model (XDM) são compatíveis com o Serviço de segmentação de Adobe. As regras que constituem uma definição de segmento são contextualizadas pelos seguintes tipos de dados.
exl-id: 73f932a7-f864-4566-ade7-c148a12dc83c
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 3%

---

# Tipos de dados compatíveis no serviço de segmentação

Todos os tipos de dados do Experience Data Model (XDM) são compatíveis com o Adobe Experience Platform Segmentation Service. As regras que constituem uma definição de segmento são contextualizadas pelos seguintes tipos de dados.

## Dados de string

As definições de segmento usam dados de sequência para definir restrições não numéricas para públicos, como &quot;nome do país&quot; ou &quot;nível do programa de fidelidade&quot;.

Os dados de string são incluídos nas definições de segmento usando instruções lógicas, inclusivas/exclusivas e de comparação. Depois que um atributo de string é adicionado à definição do segmento, é possível usar instruções relevantes para string para avaliá-lo em relação a outros campos de string.

| Tipo de instrução | Exemplos |
| -------------- | -------- |
| Lógico | `and`, `or`, `not` |
| Inclusivo/exclusivo | `include`, `must` `exist`, `exclude`, `must not exist` |
| Comparação | `equals`, `does not equal`, `contains`, `starts with` |

## Dados de data

Dados de data permitem atribuir contexto baseado em tempo às definições de segmento, usando datas de início/término específicas ou usando instruções relevantes à data, conforme mostrado na tabela abaixo. Uma implementação pode estar criando um público-alvo de clientes que interagiram com sua marca a qualquer momento *este ano* e que também estiveram ativos *nos* últimos dias.

| Exemplo de campo | Demonstrativos relevantes à data | Linha do tempo |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`, `yesterday`, `this month`, `this year` | Relevante para o dia em que a definição do segmento foi criada. |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | Relevante em uma determinada semana/mês. |

## Eventos de experiência

Como um esquema do Adobe Experience Platform, [!DNL XDM ExperienceEvents] registra interações explícitas e implícitas do cliente com aplicativos integrados ao [!DNL Platform], incluindo um instantâneo do sistema no momento em que a interação ocorreu. [!DNL ExperienceEvents] são registros de fatos. Dessa forma, elas são uma fonte de dados disponível durante a definição do segmento.

Como visto na tabela abaixo, os dados do evento são renderizados usando palavras-chave que ajudam a refinar o comportamento do evento e especificar atributos do evento.

| Palavra-chave | Uso |
| ------- | --- |
| Incluir/excluir | Descreve o comportamento do evento por meio da inclusão ou omissão de dados. |
| Qualquer/todos | Ajuda a determinar o número de definições de segmento qualificado. |
| Botão de alternância &quot;Aplicar regra de tempo&quot; | Incorpora dados de data. |
| É igual a, não é igual, começa com, não começa com, termina com, não termina com, contém, não contém, existe, não existe | Incorpora dados de sequência de caracteres. |

### Compartilhamento de público

Públicos-alvo externos também podem ser usados como componentes de uma nova definição de segmento, adicionando suas regras de atributo às novas definições de segmento.

Atualmente, somente o Adobe Audience Manager é compatível como público-alvo externo, com fontes adicionais sendo ativadas no futuro. Mais informações sobre como usar os públicos da Adobe Audience Manager com a Platform podem ser encontradas no [guia de compartilhamento de público-alvo na documentação da Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html).

### Compartilhamento de definição de segmento

As definições de segmento criadas na Platform podem ser usadas em outros [Adobe Experience Cloud Core Services](https://experienceleague.adobe.com/docs/core-services/interface/experience-cloud.html?lang=pt-BR). Para ativar esse recurso, entre em contato com seu arquiteto de soluções ou consultor.

## Outros tipos de dados

Além dos tipos de dados mencionados acima, a lista de tipos de dados compatíveis também inclui:

- URI (Uniform Resource Identifier)
- Enumeração
- Número
- Longo
- Número inteiro
- Curto
- Byte
- Booleano
- Matriz
- Objeto
- Mapa
