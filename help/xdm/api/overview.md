---
keywords: Experience Platform;página inicial;tópicos populares;api;API;XDM;sistema XDM;modelo de dados de experiência;modelo de dados de experiência;modelo de dados de experiência;modelo de dados;modelo de dados;modelo de dados;registro de esquemas;Registro de esquemas;
solution: Experience Platform
title: Guia da API do registro de esquema
description: A API do registro de esquema permite que os desenvolvedores gerenciem programaticamente todos os esquemas e recursos relacionados do Experience Data Model (XDM) no Adobe Experience Platform. Siga este manual para saber como executar operações importantes usando a API.
exl-id: 9e693d29-303e-462a-a1e2-93c0d517b8e3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 5%

---

# [!DNL Schema Registry] Manual da API

O [!DNL Schema Registry] é usado para acessar a Biblioteca de Esquemas no Adobe Experience Platform, fornecendo uma interface de usuário e a API RESTful a partir da qual todos os recursos de biblioteca disponíveis podem ser acessados.

A API do Registro de esquema fornece vários endpoints que permitem gerenciar programaticamente todos os esquemas e os recursos relacionados do Experience Data Model (XDM) disponíveis no Experience Platform. Isso inclui aqueles definidos pela Adobe, parceiros [!DNL Experience Platform] e fornecedores cujos aplicativos você usa.

Esses endpoints são descritos abaixo. Visite os manuais de endpoint individuais para obter detalhes e consulte o [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, como ler chamadas de API de exemplo e muito mais.

>[!IMPORTANT]
>
>O XDM usa a formatação do esquema JSON para descrever e validar a estrutura dos dados de experiência do cliente assimilados. Antes de trabalhar com a API do Registro de Esquema, é altamente recomendável que você revise a [documentação oficial do Esquema JSON](https://json-schema.org/) para obter uma melhor compreensão dessa tecnologia subjacente.

Para exibir todos os pontos de extremidade e operações CRUD disponíveis, visite a [Referência da API do Registro de Esquema](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## Esquemas

Os esquemas XDM representam e validam a estrutura e o formato dos dados assimilados na Experience Platform. Um esquema é composto por uma classe e zero ou mais grupos de campos de esquema. Você pode criar, exibir, editar e excluir esquemas usando o ponto de extremidade `/schemas`. Para saber como usar este ponto de extremidade, consulte o [manual de ponto de extremidade de esquemas](./schemas.md).

Para obter um guia passo a passo sobre como criar manualmente um esquema completo na API do Registro de Esquemas, incluindo a criação e adição de grupos de campos e tipos de dados, consulte o [tutorial de criação de esquema de API](../tutorials/create-schema-api.md).

Se você estiver assimilando dados CSV, consulte a seção sobre [CSV para conversão de esquema](#csv-to-schema).

## Comportamentos

Os comportamentos definem a natureza dos dados que um esquema descreve. Cada classe XDM deve fazer referência a um comportamento específico, que todos os esquemas que empregam essa classe herdarão. Consulte o [manual de endpoint de comportamentos](./behaviors.md) para saber como visualizar os comportamentos disponíveis na API.

## Classes

Uma classe define a estrutura básica de propriedades comuns que todos os esquemas baseados nessa classe devem conter e determina quais grupos de campos são elegíveis para uso nesses esquemas. Todas as classes devem ser associadas a um comportamento existente. Consulte o [manual de ponto de extremidade de classes](./classes.md) para obter detalhes sobre como trabalhar com classes na API.

## Grupos de campos

Os grupos de campos são componentes reutilizáveis que definem um ou mais campos que representam um conceito específico, como uma pessoa individual, um endereço de correspondência ou um ambiente de navegador da Web. Os grupos de campos devem ser incluídos como parte de um esquema que implementa uma classe compatível, dependendo do comportamento dos dados que representam (registro ou série de tempo). Consulte o [manual de endpoint de grupos de campos](./field-groups.md) para saber como trabalhar com grupos de campos na API.

## Tipos de dados

Os tipos de dados são usados como campos do tipo referência em classes ou grupos de campos da mesma forma que os campos literais básicos, com a principal diferença sendo que os tipos de dados podem definir vários subcampos. Embora semelhantes a grupos de campos, pois permitem o uso consistente de uma estrutura de vários campos, os tipos de dados são mais flexíveis porque podem ser incluídos em qualquer lugar na estrutura do esquema, enquanto os grupos de campos só podem ser adicionados no nível raiz. Consulte o [manual de ponto de extremidade de tipos de dados](./data-types.md) para obter mais informações sobre como trabalhar com tipos de dados na API.

>[!NOTE]
>
>Se um campo for definido como um tipo de dados específico, você não poderá criar o mesmo campo com um tipo de dados diferente em outro esquema. Essa restrição se aplica ao locatário da organização.

## Descritores

Descritores são conjuntos de metadados atribuídos a campos específicos em um esquema, fornecendo vários detalhes contextuais, incluindo como esses campos (e o próprio esquema) estão relacionados a outros esquemas. Cada esquema pode ter uma ou mais entidades de descritor aplicadas a ele e há vários tipos diferentes de descritor para fins diferentes. Consulte o [manual de endpoint de descritores](./descriptors.md) para obter mais informações sobre como trabalhar com descritores na API e uma visão geral dos diferentes tipos de descritores e seus casos de uso.

## Uniões

Embora o Experience Platform permita compor esquemas para casos de uso específicos, ele também permite compor uma &quot;união&quot; de esquemas pertencentes a uma classe específica. Um esquema de união agrega os campos de todos os esquemas que compartilham a mesma classe em uma única representação. Ao habilitar um esquema para uso com o [Perfil de Cliente em Tempo Real](../../profile/home.md), esse esquema é incluído na união para sua classe específica. Dessa forma, os esquemas de união não podem ser editados diretamente e só podem ser afetados pela inclusão ou exclusão de esquemas para uso no Perfil.

Para saber como exibir uniões na API do Registro de Esquema, consulte o [manual de ponto de extremidade de uniões](./unions.md).

## CSV para conversão de esquema {#csv-to-schema}

Você pode gerar automaticamente um esquema XDM usando um arquivo CSV como modelo, permitindo criar modelos para importar campos de esquema em massa e reduzir o trabalho manual da API ou da interface do usuário.

Consulte o [guia do ponto de extremidade de conversão de CSV para esquema](./export.md) para obter mais informações.

>[!NOTE]
>
>Você também pode usar a interface do usuário para [mapear um CSV para um esquema usando recomendações geradas por IA](../../ingestion/tutorials/map-csv/recommendations.md) (atualmente na versão beta).

## Exportar {#export}

A API do registro de esquema permite transferir e compartilhar recursos XDM entre sandboxes e organizações. Para qualquer esquema, grupo de campos ou tipo de dados, você pode gerar uma carga de exportação contendo a estrutura do recurso e quaisquer recursos dependentes. Essa carga pode ser usada para importar o recurso para uma sandbox e uma organização de destino.

Consulte o [manual de endpoint de exportação](./export.md) para obter mais informações sobre como criar uma carga de exportação para um recurso XDM existente.

## Importar

Se você usar os pontos de extremidade [exportar](#export) ou [CSV para conversão de esquema](./import.md) para criar uma carga de exportação, poderá enviar essa carga para uma organização de destino e uma sandbox para importar os recursos especificados.

Consulte o [manual de endpoint de importação](./export.md) para obter mais informações sobre como gerar recursos XDM a partir de cargas de exportação.

## Dados de amostra

Você pode gerar dados de amostra para qualquer esquema especificado na Biblioteca de esquemas. O objeto de resposta retornado pode ser usado como uma fonte de assimilação de dados.

Consulte o [manual de ponto de extremidade de dados de exemplo](./sample-data.md) para obter mais informações sobre o uso desse ponto de extremidade.

## Log de auditoria

O Registro de esquema mantém um log de todas as alterações que ocorreram em um recurso (classe, grupo de campos, tipo de dados ou esquema) entre diferentes atualizações. Você pode recuperar o log de um recurso específico fornecendo seu `$id` ou `meta:altId` no caminho de uma solicitação GET para esse ponto de extremidade.

Consulte o [manual de ponto de extremidade de log de auditoria](./audit-log.md) para obter mais informações sobre o uso desse ponto de extremidade.

## Próximas etapas

Para começar a fazer chamadas usando a API do registro de esquema, leia o [guia de introdução](./getting-started.md) e selecione um dos manuais de endpoint para saber como usar endpoints específicos.
