---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;compatibility;Compatibility;compatibility mode;Compatibility mode;field type;field types;
solution: Experience Platform
title: Apêndice do desenvolvedor do Registro do schema
description: Este documento fornece informações complementares relacionadas ao trabalho com a API de registro do Schema.
topic: developer guide
translation-type: tm+mt
source-git-commit: 0b55f18eabcf1d7c5c233234c59eb074b2670b93
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 0%

---


# Apêndice

Este documento fornece informações complementares relacionadas ao trabalho com a [!DNL Schema Registry] API.

## Uso de parâmetros de query {#query}

O [!DNL Schema Registry] oferece suporte ao uso de parâmetros de query para a página e filtrar resultados ao listar recursos.

>[!NOTE]
>
>Ao combinar vários parâmetros de query, eles devem ser separados por E comercial (`&`).

### Paginação {#paging}

Os parâmetros de query mais comuns para paginação incluem:

| Parâmetro | Descrição |
| --- | --- |
| `start` | Especifique onde os resultados listados devem começar. Esse valor pode ser obtido a partir do `_page.next` atributo de uma resposta de lista e usado para acessar a próxima página de resultados. Se o `_page.next` valor for nulo, então não há nenhuma página adicional disponível. |
| `limit` | Limite o número de recursos retornados. Exemplo: `limit=5` retornará uma lista de cinco recursos. |
| `orderby` | Classifique os resultados por uma propriedade específica. Exemplo: `orderby=title` classificará os resultados por título em ordem crescente (A-Z). A adição de um valor `-` antes do valor do parâmetro (`orderby=-title`) classificará os itens por título em ordem decrescente (Z-A). |

### Filtragem {#filtering}

Você pode filtrar os resultados usando o `property` parâmetro, que é usado para aplicar um operador específico em relação a uma determinada propriedade JSON dentro dos recursos recuperados. Os operadores suportados incluem:

| Operador | Descrição | Exemplo |
| --- | --- | --- |
| `==` | Filtros se a propriedade é igual ao valor fornecido. | `property=title==test` |
| `!=` | Filtros se a propriedade não é igual ao valor fornecido. | `property=title!=test` |
| `<` | Filtros se a propriedade é menor que o valor fornecido. | `property=version<5` |
| `>` | Filtros se a propriedade é maior que o valor fornecido. | `property=version>5` |
| `<=` | Filtros se a propriedade é menor ou igual ao valor fornecido. | `property=version<=5` |
| `>=` | Filtros se a propriedade é maior ou igual ao valor fornecido. | `property=version>=5` |
| `~` | Filtros se a propriedade corresponde a uma expressão regular fornecida. | `property=title~test$` |
| (None) | A indicação apenas do nome da propriedade retorna somente entradas nas quais a propriedade existe. | `property=title` |

>[!TIP]
>
>Você pode usar o `property` parâmetro para filtrar as misturas por sua classe compatível. Por exemplo, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` retorna somente misturas compatíveis com a [!DNL XDM Individual Profile] classe.

## Modo de compatibilidade

[!DNL Experience Data Model] (XDM) é uma especificação publicamente documentada, impulsionada pela Adobe para melhorar a interoperabilidade, a expressividade e o poder das experiências digitais. O Adobe mantém o código fonte e as definições XDM formais em um projeto de código [aberto no GitHub](https://github.com/adobe/xdm/). Essas definições são escritas na notação XDM Standard, usando a notação JSON-LD (JavaScript Object Notation for Linked Data) e o Schema JSON como a gramática para definir schemas XDM.

Ao analisar as definições formais de XDM no repositório público, você pode ver que o XDM padrão é diferente do que você vê no Adobe Experience Platform. O que você está vendo no modo de compatibilidade [!DNL Experience Platform] é chamado de Modo de compatibilidade, e ele fornece um mapeamento simples entre o XDM padrão e a forma como ele é usado no [!DNL Platform].

### Como o Modo de compatibilidade funciona

O Modo de compatibilidade permite que o modelo XDM JSON-LD funcione com a infraestrutura de dados existente, alterando valores dentro do XDM padrão e mantendo a semântica igual. Ele usa uma estrutura JSON aninhada, exibindo schemas em um formato semelhante a uma árvore.

A principal diferença que você observará entre o XDM padrão e o Modo de compatibilidade é a remoção do prefixo &quot;xdm:&quot; para nomes de campos.

A seguir está uma comparação lado a lado mostrando campos relacionados ao aniversário (com atributos de &quot;descrição&quot; removidos) no XDM padrão e no Modo de compatibilidade. Observe que os campos Modo de compatibilidade incluem uma referência ao campo XDM e seu tipo de dados nos atributos &quot;meta:xdmField&quot; e &quot;meta:xdmType&quot;.

<table>
  <th>XDM padrão</th>
  <th>Modo de compatibilidade</th>
  <tr>
  <td>
  <pre class="JSON language-JSON hljs">
        { "xdm:bornDate": { "title": "Data de nascimento", "tipo": "string", "format": "date", }, "xdm:bornDayAndMonth": { "title": "Data de nascimento", "tipo": "string", "pattern": "[0-1][0-9]-[0-9][0-9]", }, "xdm:bornYear": { "title": "Ano de nascimento", "tipo": "número inteiro", "mínimo": 1, "máximo": 32767 }
  </pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
        { "bornDate": { "title": "Data de nascimento", "tipo": "string", "format": "date", "meta:xdmField": "xdm:bornDate", "meta:xdmType": "date" }, "bornDayAndMonth": { "title": "Data de nascimento", "tipo": "string", "pattern": "[0-1][0-9]-[0-9][0-9]", "meta:xdmField": "xdm:bornDayAndMonth", "meta:xdmType": "string" }, "bornYear": { "title": "Ano de nascimento", "tipo": "número inteiro", "mínimo": 1, "máximo": 32767, "meta:xdmField": "xdm:bornYear", "meta:xdmType": "short" }
      </pre>
  </td>
  </tr>
</table>

### Por que o Modo de compatibilidade é necessário?

A Adobe Experience Platform foi projetada para trabalhar com várias soluções e serviços, cada um com seus próprios desafios e limitações técnicas (por exemplo, como determinadas tecnologias lidam com caracteres especiais). A fim de ultrapassar estas limitações, foi desenvolvido o Modo de Compatibilidade.

A maioria dos [!DNL Experience Platform] serviços inclui [!DNL Catalog], [!DNL Data Lake]e [!DNL Real-time Customer Profile] uso [!DNL Compatibility Mode] no lugar do XDM padrão. A [!DNL Schema Registry] API também usa [!DNL Compatibility Mode]e os exemplos nesse documento são mostrados usando [!DNL Compatibility Mode].

Vale a pena saber que um mapeamento ocorre entre o XDM padrão e a forma como ele é operacionalizado no [!DNL Experience Platform], mas não deve afetar seu uso de [!DNL Platform] serviços.

O projeto de código aberto está disponível para você, mas quando se trata de interagir com recursos por meio do [!DNL Schema Registry], os exemplos de API neste documento fornecem as práticas recomendadas que você deve conhecer e seguir.