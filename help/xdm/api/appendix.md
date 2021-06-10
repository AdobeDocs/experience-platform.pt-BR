---
keywords: Experience Platform, home, tópicos populares, api, API, XDM, sistema XDM, modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados, Modelo de dados, Registro de esquema, Registro de esquema, compatibilidade, modo de compatibilidade, modo de compatibilidade, tipo de campo, tipos de campo,
solution: Experience Platform
title: Apêndice do Guia da API do Registro de Schema
description: Este documento fornece informações complementares relacionadas ao trabalho com a API do Registro de Esquema.
topic-legacy: developer guide
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: d70f297130ec04dd799d60c70b95777ee79bbfef
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 1%

---

# Apêndice do guia da API do Registro de Schema

Este documento fornece informações complementares relacionadas ao trabalho com a API [!DNL Schema Registry].

## Uso de parâmetros de consulta {#query}

O [!DNL Schema Registry] suporta o uso de parâmetros de consulta para página e filtrar resultados ao listar recursos.

>[!NOTE]
>
>Ao combinar vários parâmetros de consulta, eles devem ser separados por &quot;E&quot; comercial (`&`).

### Paginação {#paging}

Os parâmetros de consulta mais comuns para paginação incluem:

| Parâmetro | Descrição |
| --- | --- |
| `start` | Especifique onde os resultados listados devem começar. Esse valor pode ser obtido do atributo `_page.next` de uma resposta de lista e usado para acessar a próxima página de resultados. Se o valor `_page.next` for nulo, então não há página adicional disponível. |
| `limit` | Limite o número de recursos retornados. Exemplo: `limit=5` retornará uma lista de cinco recursos. |
| `orderby` | Classifique os resultados por uma propriedade específica. Exemplo: `orderby=title` classificará os resultados por título em ordem crescente (A-Z). Adicionar um `-` antes do valor do parâmetro (`orderby=-title`) classificará os itens por título em ordem decrescente (Z-A). |

{style=&quot;table-layout:auto&quot;}

### Filtragem {#filtering}

Você pode filtrar resultados usando o parâmetro `property` , que é usado para aplicar um operador específico a uma determinada propriedade JSON dentro dos recursos recuperados. Os operadores compatíveis incluem:

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
>Você pode usar o parâmetro `property` para filtrar grupos de campos de esquema por sua classe compatível. Por exemplo, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` retorna somente grupos de campos compatíveis com a classe [!DNL XDM Individual Profile].

## Modo de compatibilidade {#compatibility}

[!DNL Experience Data Model] (XDM) é uma especificação documentada publicamente, impulsionada pelo Adobe para melhorar a interoperabilidade, a expressividade e o poder das experiências digitais. O Adobe mantém o código-fonte e as definições formais do XDM em um [projeto de código-fonte aberto no GitHub](https://github.com/adobe/xdm/). Essas definições são escritas em Notação padrão XDM, usando JSON-LD (Notação de objeto JavaScript para dados vinculados) e Esquema JSON como a gramática para definir esquemas XDM.

Ao analisar as definições formais do XDM no repositório público, você pode ver que o XDM padrão é diferente do que vê no Adobe Experience Platform. O que você está vendo em [!DNL Experience Platform] é chamado de Modo de Compatibilidade e fornece um mapeamento simples entre o XDM padrão e a maneira como ele é usado em [!DNL Platform].

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
        {
          "xdm:birthDate": {
              "Título": "Data de nascimento",
              "type": "string",
              "format": "date",
          },
          "xdm:birthDayAndMonth": {
              "Título": "Data de nascimento",
              "type": "string",
              "padrão": "[0-1][0-9]-[0-9][0-9]",
          },
          "xdm:birthYear": {
              "Título": "Ano de nascimento",
              "type": "integer",
              "mínimo": 1,
              "máximo": 32767
        }
  </pre>
  </td>
  <td>
  <pre class=" language-json">
        {
          "birthDate": {
              "Título": "Data de nascimento",
              "type": "string",
              "format": "date",
              "meta:xdmField": "xdm:birthDate",
              "meta:xdmType": "date"
          },
          "birthDayAndMonth": {
              "Título": "Data de nascimento",
              "type": "string",
              "padrão": "[0-1][0-9]-[0-9][0-9]",
              "meta:xdmField": "xdm:birthDayAndMonth",
              "meta:xdmType": "string"
          },
          "birthYear": {
              "Título": "Ano de nascimento",
              "type": "integer",
              "mínimo": 1,
              "máximo": 32767
              "meta:xdmField": "xdm:birthYear",
              "meta:xdmType": "short"
        }
      </pre>
  </td>
  </tr>
</table>

### Por que o Modo de Compatibilidade é necessário?

A Adobe Experience Platform foi criada para trabalhar com várias soluções e serviços, cada um com seus próprios desafios e limitações técnicas (por exemplo, como determinadas tecnologias lidam com caracteres especiais). Para superar estas limitações, foi desenvolvido o Modo de Compatibilidade.

A maioria dos serviços [!DNL Experience Platform], incluindo [!DNL Catalog], [!DNL Data Lake] e [!DNL Real-time Customer Profile] usam [!DNL Compatibility Mode] no lugar do XDM padrão. A API [!DNL Schema Registry] também usa [!DNL Compatibility Mode], e os exemplos neste documento são mostrados usando [!DNL Compatibility Mode].

Vale a pena saber que um mapeamento ocorre entre o XDM padrão e a maneira como ele é operacionalizado em [!DNL Experience Platform], mas não deve afetar o uso dos serviços [!DNL Platform].

O projeto de código aberto está disponível para você, mas quando se trata de interagir com recursos por meio do [!DNL Schema Registry], os exemplos de API neste documento fornecem as práticas recomendadas que você deve conhecer e seguir.
