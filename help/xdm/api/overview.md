---
keywords: Experience Platform;início;tópicos populares;api;API;XDM;sistema XDM;modelo de dados de experiência;modelo de dados de experiência;modelo de dados de experiência;modelo de dados;modelo de dados;modelo de dados;registro de esquema;Registro de esquema;
solution: Experience Platform
title: Guia da API do registro de esquema
description: A API do registro de esquema permite que os desenvolvedores gerenciem programaticamente todos os esquemas e recursos relacionados do Experience Data Model (XDM) no Adobe Experience Platform. Siga este manual para saber como executar operações importantes usando a API.
exl-id: 9e693d29-303e-462a-a1e2-93c0d517b8e3
source-git-commit: 6e58f070c0a25d7434f1f165543f92ec5a081e66
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 5%

---

# [!DNL Schema Registry] Manual da API

A variável [!DNL Schema Registry] O é usado para acessar a Biblioteca de esquemas no Adobe Experience Platform, fornecendo uma interface de usuário e a API RESTful a partir da qual todos os recursos disponíveis da biblioteca são acessíveis.

A API do Registro de esquema fornece vários endpoints que permitem gerenciar programaticamente todos os esquemas e os recursos relacionados do Experience Data Model (XDM) disponíveis na Platform. Isso inclui aqueles definidos pela Adobe, [!DNL Experience Platform] parceiros e fornecedores cujos aplicativos você usa.

Esses endpoints são descritos abaixo. Acesse os manuais de endpoint individuais para obter detalhes e consulte a [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, ler chamadas de API de exemplo e muito mais.

>[!IMPORTANT]
>
>O XDM usa a formatação do esquema JSON para descrever e validar a estrutura dos dados de experiência do cliente assimilados. Antes de trabalhar com a API do Registro de esquema, é altamente recomendável revisar a [Documentação oficial do esquema JSON](https://json-schema.org/) para compreender melhor essa tecnologia subjacente.

Para exibir todos os endpoints e operações CRUD disponíveis, visite o [Referência da API do registro de esquema](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## Esquemas

Os esquemas XDM representam e validam a estrutura e o formato dos dados assimilados na Platform. Um esquema é composto por uma classe e zero ou mais grupos de campos de esquema. Você pode criar, exibir, editar e excluir esquemas usando o `/schemas` terminal. Para saber como usar este endpoint, consulte a [manual de endpoint de esquemas](./schemas.md).

Para obter um guia passo a passo sobre como criar manualmente um esquema completo na API do Registro de esquema, incluindo a criação e a adição de grupos de campos e tipos de dados, consulte o [Tutorial de criação de esquema de API](../tutorials/create-schema-api.md).

Se estiver assimilando dados CSV, consulte a seção sobre [CSV para conversão de esquema](#csv-to-schema).

## Comportamentos

Os comportamentos definem a natureza dos dados que um esquema descreve. Cada classe XDM deve fazer referência a um comportamento específico, que todos os esquemas que empregam essa classe herdarão. Consulte a [guia de endpoint de comportamentos](./behaviors.md) para saber como visualizar os comportamentos disponíveis na API.

## Classes

Uma classe define a estrutura básica de propriedades comuns que todos os esquemas baseados nessa classe devem conter e determina quais grupos de campos são elegíveis para uso nesses esquemas. Todas as classes devem ser associadas a um comportamento existente. Consulte a [manual de endpoint de classes](./classes.md) para obter detalhes sobre como trabalhar com classes na API.

## Grupos de campos

Os grupos de campos são componentes reutilizáveis que definem um ou mais campos que representam um conceito específico, como uma pessoa individual, um endereço de correspondência ou um ambiente de navegador da Web. Os grupos de campos devem ser incluídos como parte de um esquema que implementa uma classe compatível, dependendo do comportamento dos dados que representam (registro ou série de tempo). Consulte a [guia de ponto de extremidade de grupos de campos](./field-groups.md) para saber como trabalhar com grupos de campos na API.

## Tipos de dados

Os tipos de dados são usados como campos do tipo referência em classes ou grupos de campos da mesma forma que os campos literais básicos, com a principal diferença sendo que os tipos de dados podem definir vários subcampos. Embora semelhantes a grupos de campos, pois permitem o uso consistente de uma estrutura de vários campos, os tipos de dados são mais flexíveis porque podem ser incluídos em qualquer lugar na estrutura do esquema, enquanto os grupos de campos só podem ser adicionados no nível raiz. Consulte a [guia de endpoint de tipos de dados](./data-types.md) para obter mais informações sobre como trabalhar com tipos de dados na API.

>[!NOTE]
>
>Se um campo for definido como um tipo de dados específico, você não poderá criar o mesmo campo com um tipo de dados diferente em outro esquema. Essa restrição se aplica ao locatário da organização.

## Descritores

Descritores são conjuntos de metadados atribuídos a campos específicos em um esquema, fornecendo vários detalhes contextuais, incluindo como esses campos (e o próprio esquema) estão relacionados a outros esquemas. Cada esquema pode ter uma ou mais entidades de descritor aplicadas a ele e há vários tipos diferentes de descritor para fins diferentes. Consulte a [guia de endpoint de descritores](./descriptors.md) para obter mais informações sobre como trabalhar com descritores na API e uma visão geral dos diferentes tipos de descritores e seus casos de uso.

## Uniões

Embora a Platform permita compor esquemas para casos de uso específicos, ela também permite compor uma &quot;união&quot; de esquemas pertencentes a uma classe específica. Um esquema de união agrega os campos de todos os esquemas que compartilham a mesma classe em uma única representação. Ao ativar um esquema para uso com [Perfil do cliente em tempo real](../../profile/home.md), esse esquema se torna incluído na união para sua classe específica. Dessa forma, os esquemas de união não podem ser editados diretamente e só podem ser afetados pela inclusão ou exclusão de esquemas para uso no Perfil.

Para saber como exibir uniões na API do Registro de esquema, consulte a [manual de endpoint de uniões](./unions.md).

## CSV para conversão de esquema {#csv-to-schema}

Você pode gerar automaticamente um esquema XDM usando um arquivo CSV como modelo, permitindo criar modelos para importar campos de esquema em massa e reduzir o trabalho manual da API ou da interface do usuário.

Consulte a [CSV para manual de endpoint de conversão de esquema](./export.md) para obter mais informações.

>[!NOTE]
>
>Também é possível usar a interface do usuário para [mapear um CSV para um esquema usando recomendações geradas por IA](../../ingestion/tutorials/map-csv/recommendations.md) (atualmente em beta).

## Exportar {#export}

A API do registro de esquema permite transferir e compartilhar recursos XDM entre sandboxes e organizações. Para qualquer esquema, grupo de campos ou tipo de dados, você pode gerar uma carga de exportação contendo a estrutura do recurso e quaisquer recursos dependentes. Essa carga pode ser usada para importar o recurso para uma sandbox e uma organização de destino.

Consulte a [exportar guia de endpoint](./export.md) para obter mais informações sobre como criar uma carga de exportação para um recurso XDM existente.

## Importar

Se você usar o [exportar](#export) ou [CSV para conversão de esquema](./import.md) Para criar uma carga de exportação, você pode enviar essa carga para uma organização de destino e uma sandbox para importar os recursos especificados.

Consulte a [guia de endpoint de importação](./export.md) para obter mais informações sobre como gerar recursos XDM a partir de cargas úteis de exportação.

## Dados de exemplo

Você pode gerar dados de amostra para qualquer esquema especificado na Biblioteca de esquemas. O objeto de resposta retornado pode ser usado como uma fonte de assimilação de dados.

Consulte a [exemplo de manual de endpoint de dados](./sample-data.md) para obter mais informações sobre o uso desse endpoint.

## Log de auditoria

O Registro de esquema mantém um log de todas as alterações que ocorreram em um recurso (classe, grupo de campos, tipo de dados ou esquema) entre diferentes atualizações. Você pode recuperar o log de um recurso específico fornecendo suas `$id` ou `meta:altId` no caminho de uma solicitação GET para esse endpoint.

Consulte a [manual de endpoint do log de auditoria](./audit-log.md) para obter mais informações sobre o uso desse endpoint.

## Próximas etapas

Para começar a fazer chamadas usando a API do registro de esquema, leia o [guia de introdução](./getting-started.md) e selecione um dos manuais de endpoint para saber como usar endpoints específicos.
