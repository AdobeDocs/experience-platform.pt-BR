---
keywords: Experience Platform, home, tópicos populares, api, API, XDM, sistema XDM, modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados, Modelo de dados, Registro do esquema, Registro do esquema;
solution: Experience Platform
title: Guia da API do Registro de Schema
description: A API do Registro de Esquema permite aos desenvolvedores gerenciar programaticamente todos os esquemas e recursos relacionados do Experience Data Model (XDM) no Adobe Experience Platform. Siga este manual para saber como executar operações importantes usando a API.
topic-legacy: developer guide
exl-id: 9e693d29-303e-462a-a1e2-93c0d517b8e3
source-git-commit: 2a58236031834bbe298576e2fcab54b04ec16ac3
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 5%

---

# [!DNL Schema Registry] Manual da API

O [!DNL Schema Registry] O é usado para acessar a Biblioteca de esquemas no Adobe Experience Platform, fornecendo uma interface de usuário e uma RESTful API da qual todos os recursos de biblioteca disponíveis são acessíveis.

A API do Registro de Esquema fornece vários endpoints que permitem gerenciar programaticamente todos os esquemas e recursos relacionados do Experience Data Model (XDM) disponíveis para você na Platform. Isso inclui os definidos por Adobe, [!DNL Experience Platform] parceiros e fornecedores cujos aplicativos você usa.

Esses endpoints são descritos abaixo. Visite os guias de ponto de extremidade individuais para obter detalhes e consulte [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, ler chamadas de API de exemplo e muito mais.

>[!IMPORTANT]
>
>O XDM usa a formatação Esquema JSON para descrever e validar a estrutura dos dados de experiência do cliente assimilados. Antes de trabalhar com a API do Registro de Schema, é altamente recomendável revisar a [documentação oficial do Esquema JSON](https://json-schema.org/) para uma melhor compreensão desta tecnologia subjacente.

Para exibir todos os endpoints e operações CRUD disponíveis, visite a [Referência da API do Registro de Schema](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## Esquemas

Os esquemas XDM representam e validam a estrutura e o formato dos dados assimilados no Platform. Um schema é composto de uma classe e zero ou mais grupos de campos de schema. Você pode criar, exibir, editar e excluir esquemas usando o `/schemas` endpoint . Para saber como usar esse terminal, consulte a [guia do endpoint de schemas](./schemas.md).

Para obter um guia passo a passo sobre como criar um esquema completo na API do Registro de Schema, incluindo a criação e adição de grupos de campos e tipos de dados, consulte [Tutorial de criação de esquema da API](../tutorials/create-schema-api.md).

## Comportamentos

Os comportamentos definem a natureza dos dados descritos por um schema. Cada classe XDM deve referenciar um comportamento específico, que todos os esquemas que empregam essa classe herdarão. Consulte a [guia do endpoint de comportamentos](./behaviors.md) para saber como visualizar os comportamentos disponíveis na API.

## Classes

Uma classe define a estrutura base das propriedades comuns que todos os schemas baseados nessa classe devem conter e determina quais grupos de campos estão qualificados para uso nesses schemas. Cada classe deve ser associada a um comportamento existente. Consulte a [guia de endpoint de classes](./classes.md) para obter detalhes sobre como trabalhar com classes na API.

## Grupos de campos

Grupos de campos são componentes reutilizáveis que definem um ou mais campos que representam um conceito específico, como uma pessoa individual, um endereço de correspondência ou um ambiente de navegador da Web. Os grupos de campos devem ser incluídos como parte de um schema que implementa uma classe compatível, dependendo do comportamento dos dados que representam (registro ou série de tempo). Consulte a [guia do ponto de extremidade de grupos de campos](./field-groups.md) para saber como trabalhar com grupos de campo na API.

## Tipos de dados

Os tipos de dados são usados como campos do tipo referência em classes ou grupos de campos da mesma forma que os campos literais básicos, sendo a principal diferença que os tipos de dados podem definir vários subcampos. Embora semelhantes a grupos de campos, na medida em que permitem o uso consistente de uma estrutura de vários campos, os tipos de dados são mais flexíveis porque podem ser incluídos em qualquer lugar na estrutura do schema, enquanto os grupos de campos só podem ser adicionados no nível raiz. Consulte a [guia do endpoint de tipos de dados](./data-types.md) para obter mais informações sobre como trabalhar com tipos de dados na API.

## Descritores

Os descritores são conjuntos de metadados que são atribuídos a campos específicos em um esquema, fornecendo vários detalhes contextuais, incluindo como esses campos (e o próprio schema) estão relacionados a outros esquemas. Cada esquema pode ter uma ou mais entidades de descritor aplicadas a ele, e há vários tipos diferentes de descritor para servir fins diferentes. Consulte a [guia do endpoint de descritores](./descriptors.md) para obter mais informações sobre como trabalhar com descritores na API, e uma visão geral dos diferentes tipos de descritor e seus casos de uso.

## Uniões

Embora a Platform permita compor esquemas para casos de uso específicos, também permite compor uma &quot;união&quot; de esquemas pertencentes a uma classe específica. Um schema de união agrega os campos de todos os schemas que compartilham a mesma classe em uma única representação. Ao ativar um schema para uso com [Perfil do cliente em tempo real](../../profile/home.md), esse schema será incluído na união para sua classe específica. Dessa forma, os schemas de união não podem ser editados diretamente e só podem ser afetados pela inclusão ou exclusão de schemas para uso no Perfil.

Para saber como visualizar sindicatos na API do Registro de Schema, consulte o [guia de endpoint de sindicatos](./unions.md).

## CSV para conversão do schema {#csv-to-schema}

Você pode gerar automaticamente um esquema XDM usando um arquivo CSV como modelo, permitindo criar modelos para importar campos de esquema em massa e reduzir o trabalho manual da API ou da interface do usuário.

Consulte a [CSV para o guia do endpoint de conversão do schema](./export.md) para obter mais informações.

## Exportar {#export}

A API do Registro de Schema permite transferir e compartilhar recursos XDM entre sandboxes e organizações IMS. Para qualquer esquema, grupo de campos ou tipo de dados, é possível gerar uma carga de exportação contendo a estrutura do recurso e quaisquer recursos dependentes. Essa carga pode ser usada para importar o recurso para uma sandbox de destino e a IMS Org.

Consulte a [guia de endpoint de exportação](./export.md) para obter mais informações sobre como criar uma carga de exportação para um recurso XDM existente.

## Importar

Se você usar a variável [exportar](#export) ou [CSV para conversão do schema](./import.md) endpoints para criar uma carga de exportação, é possível enviar essa carga para uma organização de destino e uma sandbox para importar os recursos especificados.

Consulte a [guia de endpoint de importação](./export.md) para obter mais informações sobre como gerar recursos XDM a partir de cargas de exportação.

## Dados de exemplo

Você pode gerar dados de amostra para qualquer esquema especificado na Biblioteca de Esquemas. O objeto de resposta retornado pode ser usado como uma fonte de assimilação de dados.

Consulte a [guia do endpoint de dados de exemplo](./sample-data.md) para obter mais informações sobre o uso desse endpoint.

## Log de auditoria

O Registro de Esquema mantém um log de todas as alterações que ocorreram em um recurso (classe, grupo de campos, tipo de dados ou esquema) entre diferentes atualizações. Você pode recuperar o log de um recurso específico fornecendo seu `$id` ou `meta:altId` no caminho de uma solicitação do GET para esse endpoint.

Consulte a [guia do endpoint de log de auditoria](./audit-log.md) para obter mais informações sobre o uso desse endpoint.

## Próximas etapas

Para começar a fazer chamadas usando a API do registro de esquema, leia o [guia de introdução](./getting-started.md) e selecione um dos manuais de endpoint para saber como usar endpoints específicos.
