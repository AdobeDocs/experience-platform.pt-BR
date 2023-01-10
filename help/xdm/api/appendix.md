---
keywords: Experience Platform, home, tópicos populares, api, API, XDM, sistema XDM, modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados, Modelo de dados, Registro de esquema, Registro de esquema, compatibilidade, modo de compatibilidade, modo de compatibilidade, tipo de campo, tipos de campo,
solution: Experience Platform
title: Apêndice do Guia da API do Registro de Schema
description: Este documento fornece informações complementares relacionadas ao trabalho com a API do Registro de Esquema.
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 1%

---

# Apêndice do guia da API do Registro de Schema

Este documento fornece informações complementares relacionadas ao trabalho com a [!DNL Schema Registry] API.

## Uso de parâmetros de consulta {#query}

O [!DNL Schema Registry] O suporta o uso de parâmetros de consulta para página e filtrar resultados ao listar recursos.

>[!NOTE]
>
>Ao combinar vários parâmetros de consulta, eles devem ser separados por &quot;E&quot; comercial (`&`).

### Paginação {#paging}

Os parâmetros de consulta mais comuns para paginação incluem:

| Parâmetro | Descrição |
| --- | --- |
| `orderby` | Classifique os resultados por uma propriedade específica. Exemplo: `orderby=title` classificará os resultados por título em ordem crescente (A-Z). Adicionar um `-` antes do valor do parâmetro (`orderby=-title`) classificará os itens por título em ordem decrescente (Z-A). |
| `limit` | Quando usado em conjunto com um `orderby` parâmetro, `limit` restringe o número máximo de itens que devem ser retornados para uma determinada solicitação. Este parâmetro não pode ser usado sem um `orderby` presente.<br><br>O `limit` especifica um inteiro positivo (entre `0` e `500`) como um *dica* quanto ao número máximo de itens que devem ser retornados. Por exemplo, `limit=5` retorna apenas cinco recursos na lista. No entanto, esse valor não é rigorosamente respeitado. O tamanho real da resposta pode ser menor ou maior, tal como restringido pela necessidade de fornecer o funcionamento fiável da `start` , se uma for fornecida. |
| `start` | Quando usado em conjunto com um `orderby` parâmetro, `start` especifica o início da lista subdefinida de itens. Este parâmetro não pode ser usado sem um `orderby` presente. Esse valor pode ser obtido da variável `_page.next` de uma resposta de lista e usado para acessar a próxima página de resultados. Se a variável `_page.next` for nulo, então não haverá página adicional disponível.<br><br>Normalmente, esse parâmetro é omitido para obter a primeira página de resultados. Depois disso, `start` deve ser definido como o valor máximo da propriedade de classificação primária do `orderby` recebido na página anterior. A resposta da API retorna entradas que começam com aquelas que têm uma propriedade de classificação primária de `orderby` estritamente maior que (para crescente) ou estritamente menor que (para decrescente) o valor especificado.<br><br>Por exemplo, se a variável `orderby` é definido como `orderby=name,firstname`, o `start` conteria um valor para a variável `name` propriedade. Nesse caso, se você quiser mostrar as próximas 20 entradas de um recurso imediatamente após o nome &quot;Miller&quot;, você usaria: `?orderby=name,firstname&start=Miller&limit=20`. |

{style=&quot;table-layout:auto&quot;}

### Filtragem {#filtering}

Você pode filtrar resultados usando a variável `property` , que é usado para aplicar um operador específico em relação a uma determinada propriedade JSON dentro dos recursos recuperados. Os operadores compatíveis incluem:

| Operador | Descrição | Exemplo |
| --- | --- | --- |
| `==` | Filtra se a propriedade é igual ao valor fornecido. | `property=title==test` |
| `!=` | Filtra se a propriedade não é igual ao valor fornecido. | `property=title!=test` |
| `<` | Filtra se a propriedade é menor que o valor fornecido. | `property=version<5` |
| `>` | Filtra se a propriedade é maior que o valor fornecido. | `property=version>5` |
| `<=` | Filtra se a propriedade é menor ou igual ao valor fornecido. | `property=version<=5` |
| `>=` | Filtra se a propriedade é maior ou igual ao valor fornecido. | `property=version>=5` |
| `~` | Filtra se a propriedade corresponde a uma expressão regular fornecida. | `property=title~test$` |
| (None) | Declarar somente o nome da propriedade retorna somente entradas nas quais a propriedade existe. | `property=title` |

{style=&quot;table-layout:auto&quot;}

>[!TIP]
>
>Você pode usar o `property` para filtrar grupos de campos de esquema por sua classe compatível. Por exemplo, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` retorna somente grupos de campos compatíveis com o [!DNL XDM Individual Profile] classe .

## Modo de compatibilidade {#compatibility}

[!DNL Experience Data Model] (XDM) é uma especificação documentada publicamente, impulsionada pelo Adobe para melhorar a interoperabilidade, a expressividade e o poder das experiências digitais. O Adobe mantém o código-fonte e as definições formais do XDM em um [projeto de código aberto no GitHub](https://github.com/adobe/xdm/). Essas definições são escritas em Notação padrão XDM, usando JSON-LD (Notação de objeto JavaScript para dados vinculados) e Esquema JSON como a gramática para definir esquemas XDM.

Ao analisar as definições formais do XDM no repositório público, você pode ver que o XDM padrão é diferente do que vê no Adobe Experience Platform. O que você está vendo [!DNL Experience Platform] é chamado de Modo de Compatibilidade e fornece um mapeamento simples entre o XDM padrão e a forma como é usado no [!DNL Platform].

### Como o Modo de compatibilidade funciona

O Modo de Compatibilidade permite que o modelo JSON-LD XDM funcione com a infraestrutura de dados existente, alterando valores no XDM padrão e mantendo a semântica igual. Usa uma estrutura JSON aninhada, exibindo esquemas em um formato de árvore.

A principal diferença que você notará entre o XDM padrão e o Modo de compatibilidade é a remoção do prefixo &quot;xdm:&quot; para nomes de campo.

Veja a seguir uma comparação lado a lado que mostra campos relacionados ao aniversário (com atributos de &quot;descrição&quot; removidos) no XDM padrão e no Modo de compatibilidade. Observe que os campos Modo de compatibilidade incluem uma referência ao campo XDM e seu tipo de dados nos atributos &quot;meta:xdmField&quot; e &quot;meta:xdmType&quot;.

<table style="table-layout:auto">
  <th>XDM padrão</th>
  <th>Modo de compatibilidade</th>
  <tr>
  <td>
  <pre class=" language-json">
{ "xdm:birthDate": { "title": "Birth Date", "type": "string", "format": "date" }, "xdm:birthDayAndMonth": { "title": "Birth Date", "type": "string", "pattern": "[0-1][0-9]-[0-9][0-9]" }, "xdm:birthYear": { "title": "Ano de nascimento", "tipo": "integer", "Minimum": 1, "máximo": 32767 }
  </pre>
  </td>
  <td>
  <pre class=" language-json">
{ "birthDate": { "title": "Birth Date", "type": "string", "format": "date", "meta:xdmField": "xdm:birthDate", "meta:xdmType": "date" }, "birthDayAndMonth": { "title": "Birth Date", "type": "string", "pattern": "[0-1][0-9]-[0-9][0-9]", "meta:xdmField": "xdm:birthDayAndMonth", "meta:xdmType": "string" }, "birthYear": { "title": "Ano de nascimento", "tipo": "integer", "Minimum": 1, "máximo": 32767, "meta:xdmField": "xdm:birthYear", "meta:xdmType": "short" }
      </pre>
  </td>
  </tr>
</table>

### Por que o Modo de Compatibilidade é necessário?

A Adobe Experience Platform foi criada para trabalhar com várias soluções e serviços, cada um com seus próprios desafios e limitações técnicas (por exemplo, como determinadas tecnologias lidam com caracteres especiais). Para superar estas limitações, foi desenvolvido o Modo de Compatibilidade.

Mais [!DNL Experience Platform] serviços, incluindo [!DNL Catalog], [!DNL Data Lake]e [!DNL Real-Time Customer Profile] use [!DNL Compatibility Mode] em vez do XDM padrão. O [!DNL Schema Registry] A API também usa [!DNL Compatibility Mode]e os exemplos neste documento são mostrados usando [!DNL Compatibility Mode].

Vale a pena saber que ocorre um mapeamento entre o XDM padrão e a forma como ele é operacionalizado no [!DNL Experience Platform], mas não deve afetar o uso de [!DNL Platform] serviços.

O projeto de código aberto está disponível para você, mas quando se trata de interagir com recursos por meio do [!DNL Schema Registry], os exemplos de API neste documento fornecem as práticas recomendadas que você deve conhecer e seguir.
