---
keywords: Experience Platform;página inicial;tópicos populares;api;API;XDM;sistema XDM;modelo de dados de experiência;modelo de dados de experiência;modelo de dados de experiência;modelo de dados;modelo de dados;modelo de dados;registro de esquemas;compatibilidade;Compatibilidade;modo de compatibilidade;modo de compatibilidade;tipo de campo;tipos de campo;
solution: Experience Platform
title: Apêndice do guia da API do registro de esquema
description: Este documento fornece informações adicionais relacionadas ao trabalho com a API do Registro de esquema.
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: 28891cf37dc9ffcc548f4c0565a77f62432c0b44
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 0%

---

# Apêndice do guia da API do registro de esquema

Este documento fornece informações adicionais relacionadas ao trabalho com a API [!DNL Schema Registry].

## Uso de parâmetros de consulta {#query}

O [!DNL Schema Registry] dá suporte ao uso de parâmetros de consulta para página e filtrar resultados ao listar recursos.

>[!NOTE]
>
>Ao combinar vários parâmetros de consulta, eles devem ser separados por &quot;E&quot; comercial (`&`).

### Paginação {#paging}

Os parâmetros de consulta mais comuns para paginação incluem:

| Parâmetro | Descrição |
| --- | --- |
| `orderby` | Classificar os resultados por uma propriedade específica. Exemplo: `orderby=title` classificará os resultados por título em ordem crescente (A-Z). Adicionar um `-` antes do valor do parâmetro (`orderby=-title`) classificará os itens por título em ordem decrescente (Z-A). |
| `limit` | Quando usado em conjunto com um parâmetro `orderby`, `limit` restringe o número máximo de itens que devem ser retornados para uma determinada solicitação. Este parâmetro não pode ser usado sem um parâmetro `orderby` presente.<br><br>O parâmetro `limit` especifica um inteiro positivo (entre `0` e `500`) como uma *dica* quanto ao número máximo de itens que devem ser retornados. Por exemplo, `limit=5` retorna somente cinco recursos na lista. No entanto, esse valor não é estritamente honrado. O tamanho real da resposta pode ser menor ou maior, conforme restringido pela necessidade de fornecer a operação confiável do parâmetro `start`, se fornecido. |
| `start` | Quando usado em conjunto com um parâmetro `orderby`, `start` especifica onde a lista subdefinida de itens deve começar. Este parâmetro não pode ser usado sem um parâmetro `orderby` presente. Esse valor pode ser obtido do atributo `_page.next` de uma resposta de lista e usado para acessar a próxima página de resultados. Se o valor `_page.next` for nulo, então não há página adicional disponível.<br><br>Normalmente, esse parâmetro é omitido para obter a primeira página de resultados. Depois disso, `start` deve ser definido como o valor máximo da propriedade de classificação primária do campo `orderby` recebido na página anterior. A resposta da API retorna entradas que começam com aquelas que têm uma propriedade de classificação primária de `orderby` estritamente maior que (para crescente) ou estritamente menor que (para decrescente) o valor especificado.<br><br>Por exemplo, se o parâmetro `orderby` estiver definido como `orderby=name,firstname`, o parâmetro `start` conterá um valor para a propriedade `name`. Nesse caso, se você quiser mostrar as próximas 20 entradas de um recurso imediatamente após o nome &quot;Miller&quot;, você usaria: `?orderby=name,firstname&start=Miller&limit=20`. |

{style="table-layout:auto"}

### Filtragem {#filtering}

Você pode filtrar os resultados usando o parâmetro `property`, que é usado para aplicar um operador específico em uma determinada propriedade JSON nos recursos recuperados. Os operadores compatíveis incluem:

| Operador | Descrição | Exemplo |
| --- | --- | --- |
| `==` | Define se a propriedade é igual ao valor fornecido. | `property=title==test` |
| `!=` | Define se a propriedade não é igual ao valor fornecido. | `property=title!=test` |
| `<` | Define se a propriedade é menor que o valor fornecido. | `property=version<5` |
| `>` | Filtra especificando se a propriedade é maior que o valor fornecido. | `property=version>5` |
| `<=` | Filtra se a propriedade é menor ou igual ao valor fornecido. | `property=version<=5` |
| `>=` | Filtra se a propriedade é maior ou igual ao valor fornecido. | `property=version>=5` |
| (Nenhum) | Declarar apenas o nome da propriedade retorna somente as entradas nas quais a propriedade existe. | `property=title` |

{style="table-layout:auto"}

>[!TIP]
>
>Você pode usar o parâmetro `property` para filtrar grupos de campos de esquema por sua classe compatível. Por exemplo, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` retorna somente grupos de campos compatíveis com a classe [!DNL XDM Individual Profile].

## Modo de compatibilidade {#compatibility}

O [!DNL Experience Data Model] (XDM) é uma especificação documentada publicamente, orientada pela Adobe para melhorar a interoperabilidade, a expressividade e o poder das experiências digitais. O Adobe mantém o código-fonte e as definições formais do XDM em um [projeto de código aberto no GitHub](https://github.com/adobe/xdm/). Essas definições são escritas em Notação padrão XDM, usando JSON-LD (Notação de objeto JavaScript para dados vinculados) e Esquema JSON como a gramática para definir esquemas XDM.

Ao observar as definições formais de XDM no repositório público, é possível observar que o XDM padrão é diferente do que você vê no Adobe Experience Platform. O que você está vendo no [!DNL Experience Platform] é chamado de Modo de Compatibilidade e fornece um mapeamento simples entre o XDM padrão e a maneira como é usado no [!DNL Platform].

### Como o modo de compatibilidade funciona

O modo de compatibilidade permite que o modelo XDM JSON-LD funcione com a infraestrutura de dados existente, alterando os valores no XDM padrão e mantendo a semântica igual. Ele usa uma estrutura JSON aninhada, exibindo esquemas em um formato em árvore.

A principal diferença observada entre o XDM padrão e o Modo de compatibilidade é a remoção do prefixo &quot;xdm:&quot; para nomes de campo.

Veja a seguir uma comparação lado a lado que mostra campos relacionados ao aniversário (com atributos de &quot;descrição&quot; removidos) no XDM padrão e no Modo de compatibilidade. Observe que os campos Modo de compatibilidade incluem uma referência ao campo XDM e seu tipo de dados nos atributos &quot;meta:xdmField&quot; e &quot;meta:xdmType&quot;.

<table style="table-layout:auto">
  <th>XDM padrão</th>
  <th>Modo de compatibilidade</th>
  <tr>
  <td>
  <pre class=" language-json">
{
  "xdm:birthDate": {
    "title": "Birth Date",
    "type": "string",
    "format": "date"
  },
  "xdm:birthDayAndMonth": {
    "title": "Birth Date",
    "type": "string",
    "padrão": "[0-1][0-9]-[0-9][0-9]"
  },
  "xdm:birthYear": {
    "title": "Birth year",
    "type": "integer",
    "minimum": 1,
    "maximum": 32767
  }
}
  </pre>
  </td>
  <td>
  <pre class=" language-json">
{
  "birthDate": {
    "title": "Birth Date",
    "type": "string",
    "format": "date",
    "meta:xdmField": "xdm:birthDate",
    "meta:xdmType": "date"
  },
  "birthDayAndMonth": {
    "title": "Birth Date",
    "type": "string",
    "padrão": "[0-1][0-9]-[0-9][0-9]",
    "meta:xdmField": "xdm:birthDayAndMonth",
    "meta:xdmType": "string"
  },
  "birthYear": {
    "title": "Birth year",
    "type": "integer",
    "minimum": 1,
    "maximum": 32767,
    "meta:xdmField": "xdm:birthYear",
    "meta:xdmType": "short"
  }
}
      </pre>
  </td>
  </tr>
</table>

### Por que o modo de compatibilidade é necessário?

A Adobe Experience Platform foi projetada para trabalhar com várias soluções e serviços, cada um com seus próprios desafios e limitações técnicas (por exemplo, como determinadas tecnologias lidam com caracteres especiais). Para superar essas limitações, o Modo de compatibilidade foi desenvolvido.

A maioria dos serviços do [!DNL Experience Platform], incluindo [!DNL Catalog], [!DNL Data Lake] e [!DNL Real-Time Customer Profile], usa [!DNL Compatibility Mode] no lugar do XDM padrão. A API [!DNL Schema Registry] também usa [!DNL Compatibility Mode], e os exemplos neste documento são todos mostrados usando [!DNL Compatibility Mode].

Vale a pena saber que um mapeamento ocorre entre o XDM padrão e a forma como ele é operacionalizado no [!DNL Experience Platform], mas não deve afetar o uso dos serviços do [!DNL Platform].

O projeto de código aberto está disponível para você, mas quando se trata de interagir com recursos por meio do [!DNL Schema Registry], os exemplos de API neste documento fornecem as práticas recomendadas que você deve conhecer e seguir.
