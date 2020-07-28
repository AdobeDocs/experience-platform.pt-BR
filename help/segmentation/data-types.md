---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tipos de dados do Serviço de segmentação de Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 96b6f820e5d372446c4927e7719aedadb2b11bc9
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 3%

---


# Tipos de dados suportados pelo Adobe Experience Platform [!DNL Segmentation Service]

Todos os tipos de dados XDM são suportados dentro [!DNL Segmentation Service]. As regras que constituem uma definição de segmento são contextualizadas pelos seguintes tipos de dados.

## Dados da string

As definições de segmento usam dados de string para definir restrições não numéricas para audiências de segmento, como &quot;nome do país&quot; ou &quot;nível de programa de fidelidade&quot;.

Os dados de sequência de caracteres são incluídos nas definições de segmento usando declarações lógicas, inclusivas/exclusivas e comparativas. Depois que um atributo de string é adicionado à definição do segmento, você pode usar declarações relevantes de string para avaliá-lo em relação a outros campos de string.

| Tipo de declaração | Exemplos |
| -------------- | -------- |
| Lógica | `and`, `or`, `not` |
| Inclusivo/exclusivo | `include`, `must` `exist`, `exclude`, `must not exist` |
| Comparação | `equals`, `does not equal`, `contains`, `starts with` |

## Dados de data

Os dados de data permitem que você atribua contexto baseado em tempo às definições de segmento, usando datas de start/término específicas ou usando declarações relevantes de data, conforme mostrado na tabela abaixo. Uma implementação pode estar criando uma audiência de clientes que interagiram com a sua marca a qualquer momento *neste ano* e também tem estado ativo *nos últimos* dias.

| Exemplo de campo | Declarações relevantes à data | Linha do tempo |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`, `yesterday`, `this month`, `this year` | Relevante para o dia em que o segmento foi construído. |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | Relevante dentro de uma determinada semana/mês. |

## Eventos de experiência

Como um schema Adobe Experience Platform, [!DNL XDM ExperienceEvents] registre interações explícitas e implícitas do cliente com aplicativos [!DNL Platform]integrados, incluindo um instantâneo do sistema no momento em que a interação ocorreu. [!DNL ExperienceEvents] são registros de fatos. Dessa forma, eles são uma fonte de dados disponível para você durante a definição do segmento.

Conforme visto na tabela abaixo, os dados do evento são renderizados usando palavras-chave que ajudam a refinar o comportamento do evento e a especificar atributos do evento.

| Palavra-chave | Use |
| ------- | --- |
| Incluir/excluir | Descreve o comportamento do evento através da inclusão ou omissão de dados. |
| Qualquer/todos | Ajuda a determinar o número de segmentos qualificados. |
| Botão de alternância &quot;Aplicar regra de tempo&quot; | Incorpora dados de data. |
| É igual, não é igual, start com, não start, termina com, não termina com, contém, não contém, existe, não existe | Incorpora dados de string. |

### Compartilhamento de público

audiências externas também podem ser usadas como componentes de uma nova definição de segmento, adicionando suas regras de atributo ao novo segmento.

Atualmente, apenas o Adobe Audience Manager é suportado como uma audiência externa, com fontes adicionais sendo ativadas no futuro. Para obter mais informações sobre como usar o Adobe Audience Manager audiência com o Platform, consulte o guia de compartilhamento de [audiências na documentação](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)do Adobe Audience Manager.

### Compartilhamento de segmentos

Os segmentos criados no Platform podem ser usados em outros [Adobe Experience Cloud Core Services](https://docs.adobe.com/content/help/pt-BR/core-services/interface/experience-cloud.html). Para ativar este recurso, você precisará entrar em contato com o arquiteto da solução ou com seu consultor.

## Outros tipos de dados

Além dos tipos de dados mencionados acima, a lista de tipos de dados suportados também inclui:

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