---
title: Modelos integrados
description: Saiba como reutilizar várias condições em várias consultas com modelos em linha.
exl-id: 78959070-f9e5-4736-b72a-a8ef518bfa4f
source-git-commit: ef4c7f20710f56ca0de7c0dfdb99751ff2fe8ebe
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 1%

---

# Modelos em linha

Modelos em linha permitem reutilizar várias condições em várias consultas. Você pode salvar os critérios em um modelo e reutilizá-los em várias consultas. Modelos SQL reutilizáveis reduzem os esforços de desenvolvimento e também o risco de erros ao copiar longas instruções entre consultas. Com modelos em linha, é possível fazer alterações em um local e fazer com que elas sejam refletidas em qualquer consulta que faça referência a esse modelo.

Este documento aborda o uso e as limitações de modelos em linha no Editor de consultas.

## Pré-requisitos

Os modelos em linha são compatíveis com a interface do usuário e a API do serviço de consulta. Antes de continuar com este guia, leia a documentação sobre como [criar um modelo de consulta por meio da API](../api/query-templates.md#create-a-query-template) ou com o [Editor de Consultas](../ui/user-guide.md#query-authoring).

## Sintaxe de modelo embutido {#syntax}

Depois que uma consulta é salva, ela é conhecida como template. Quando o template faz referência a outro template na instrução, ele é chamado de template incorporado. Os modelos em linha são indicados no SQL usando o símbolo de hash (#) seguido pelo nome do modelo. Um exemplo dessa sintaxe é `#YOUR_TEMPLATE_NAME`.

## Caso de uso {#use-case}

Os modelos SQL a seguir demonstram a utilidade de modelos em linha, com um exemplo para contar o número de clientes dos EUA de qualquer região que gastaram mais do que a &quot;receita máxima&quot; e solicitados antes de junho de 2023. O benefício do modelo em linha é que você pode editar facilmente o modelo filho (nesse caso, a receita máxima e a data do pedido) e não precisa alterar o modelo pai.

**Exemplo**

```sql
#parent_template : SELECT count(*) FROM customer WHERE region=NA AND country=US AND revenue > #revenue_max
#revenue_max: SELECT max(revenue) FROM revenue_table WHERE order_date > '01-06-2023'
```

Ao executar a consulta, o Serviço de consulta substitui o nome do modelo começando do símbolo de hash pela instrução SQL do modelo nomeado.

>[!NOTE]
>
>Os templates de query podem chamar qualquer número de outros templates embutidos. Não há restrição no número de templates embutidos que podem ser chamados a partir de uma única query. Os modelos também podem ser aninhados em outros modelos em linha.

Você pode usar modelos para armazenar uma ou várias condições. Eles não precisam ser uma consulta completa por si só. Se o modelo contiver uma consulta válida, você poderá executar a consulta simplesmente chamando o nome do modelo precedido por um símbolo de hash. Por exemplo, se você armazenasse `SELECT * FROM JUNE_2023_LOYALTY_MEMBERS;` como um modelo chamado `JUNE_2023_LOYALTY_MEMBERS`, o comando `#JUNE_2023_LOYALTY_MEMBERS;` executaria a consulta válida contida no modelo.

>[!NOTE]
>
>Na interface do usuário do Adobe Experience Platform, os modelos em linha na forma de consultas parametrizadas só são suportados no nível principal. Isso significa que as consultas parametrizadas só funcionam quando usadas no template original. O modelo filho deve ser um modelo estático e não pode ter parâmetros dinâmicos. Consulte a [documentação de consultas parametrizadas](../ui/parameterized-queries.md) para saber mais.

## Próximas etapas

Depois de ler este documento, agora você sabe como fazer referência a outros modelos no SQL, no Editor de consultas ou por meio da API do Serviço de consulta.

Além disso, você deve ler o [guia de bloco anônimo](./anonymous-block.md), que explica como minimizar as despesas gerais de desenvolvimento, encadeando uma ou mais instruções SQL que são executadas em sequência.
