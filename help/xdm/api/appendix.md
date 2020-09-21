---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;compatibility;Compatibility;compatibility mode;Compatibility mode;field type;field types;
solution: Experience Platform
title: Apêndice do desenvolvedor do Registro do schema
description: Este documento fornece informações complementares relacionadas ao trabalho com a API de registro do Schema.
topic: developer guide
translation-type: tm+mt
source-git-commit: 42d3bed14c5f926892467baeeea09ee7a140ebdc
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# Apêndice

Este documento fornece informações complementares relacionadas ao trabalho com a [!DNL Schema Registry] API.

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