---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, API
title: Guia de solução de problemas de perfil do cliente em tempo real
topic-legacy: guide
type: Documentation
description: Este documento fornece respostas a perguntas frequentes sobre o Perfil do cliente em tempo real, bem como um guia de solução de problemas para erros comuns ao trabalhar com dados de perfil usando o Adobe Experience Platform.
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---

# Guia de solução de problemas do Perfil do cliente em tempo real

Este documento fornece respostas a perguntas frequentes sobre o Perfil do cliente em tempo real, bem como um guia de solução de problemas para erros comuns. Para dúvidas e solução de problemas relacionados a outros serviços no Adobe Experience Platform, consulte o [Guia de solução de problemas do Experience Platform](../landing/troubleshooting.md).

Com [!DNL Real-time Customer Profile], você pode ver uma visualização holística de cada cliente individual ao combinar dados de vários canais, incluindo online, offline, CRM e de terceiros. Isso permite que os profissionais de marketing conduzam experiências coordenadas, consistentes e relevantes para os clientes em vários canais.

## Perguntas frequentes

Veja a seguir uma lista de respostas para perguntas frequentes sobre o Perfil do cliente em tempo real.

### Que tipos de dados são aceitos para o Perfil do cliente em tempo real?

O perfil aceita os dados **record** e **time-series**, desde que os dados em questão contenham pelo menos um valor de identidade que associe os dados a uma pessoa individual exclusiva.

Como todos os serviços da plataforma, o Perfil requer que seus dados sejam estruturados semanticamente em um esquema do Experience Data Model (XDM). Por sua vez, esse schema deve ter uma **identidade primária** definida e deve ser habilitado para uso no Perfil.

Se você não estiver familiarizado com o XDM, comece com a [Visão geral do XDM](../xdm/home.md) para saber mais. Em seguida, consulte o guia do usuário XDM para obter etapas sobre como [definir campos de identidade](../xdm/tutorials/create-schema-ui.md#identity-field) e [ativar um esquema para Perfil](../xdm/tutorials/create-schema-ui.md#profile).

### Onde os dados do Perfil são armazenados?

O Perfil do cliente em tempo real mantém seu próprio armazenamento de dados (conhecido como &quot;Armazenamento de perfil&quot;), separado do Data Lake que contém outros dados de plataforma assimilados.

### Se eu já tiver assimilado dados na Platform, posso disponibilizá-los na Loja de perfis?

Se os dados tiverem sido assimilados em um conjunto de dados que não seja de Perfil, será necessário assimilar novamente esses dados em um conjunto de dados habilitado para perfil para torná-los disponíveis no armazenamento de Perfil. É possível ativar um conjunto de dados existente para o Perfil, no entanto, todos os dados assimilados antes dessa configuração ainda não aparecerão no armazenamento de Perfil.

Se desejar adicionar dados assimilados anteriormente ao armazenamento do Perfil, siga o [tutorial de configuração do conjunto de dados](./tutorials/dataset-configuration.md) para criar um novo conjunto de dados ou converter um conjunto de dados existente para ser ativado para o Perfil e, em seguida, assimile novamente os dados desejados nesse conjunto de dados.

### Como posso visualizar meus dados de perfil assimilados?

Existem vários métodos de visualização de dados de perfil, dependendo se você está usando a API ou a interface do usuário.

#### Uso da API

Se você souber as IDs das entidades de Perfil que deseja acessar, poderá usar o endpoint `/entities` (Acesso ao perfil) na API de perfil para pesquisar essas entidades. Consulte a seção sobre [entities](./api/entities.md) no guia do desenvolvedor para obter mais informações.

Você também pode usar a API do Serviço de segmentação da Adobe Experience Platform para acessar os perfis individuais dos clientes que se qualificaram para uma associação de segmento. Consulte a [Visão geral do serviço de segmentação](../segmentation/home.md) para obter mais informações.

#### Uso da interface do usuário

Na interface do usuário do Experience Platform, a guia **[!UICONTROL Browse]** no espaço de trabalho **[!UICONTROL Profiles]** permite visualizar a contagem total de perfis e procurar perfis individuais pelo valor de identidade. Consulte o [Guia do usuário de perfil](./ui/user-guide.md) para obter mais informações.

Você também pode exibir uma lista dos segmentos na guia **[!UICONTROL Browse]** no espaço de trabalho **[!UICONTROL Segments]**. Depois de selecionar um segmento, uma amostra de perfis qualificados para esse segmento é exibida. Você pode selecionar qualquer um desses perfis listados para exibir seus detalhes. Consulte a [Visão geral da interface do usuário de segmentação](../segmentation/ui/overview.md) para obter mais informações.

## Códigos de erro

Veja a seguir uma lista de mensagens de erro que podem ser encontradas ao trabalhar com a API do perfil do cliente em tempo real. Se o erro que você está encontrando não estiver listado aqui, você pode encontrá-lo no [Guia geral de solução de problemas da plataforma](../landing/troubleshooting.md) em vez disso.

### Não foi possível pesquisar o esquema do atributo calculado para o caminho fornecido

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

Ao criar um novo atributo calculado, esse erro ocorre quando o sistema não pôde localizar o schema fornecido na carga da solicitação. Verifique se você forneceu a ID correta do locatário na propriedade `path` do payload e se os valores de `schema.name` são um nome de schema válido.

Se você não souber a ID do locatário, poderá recuperá-la seguindo as etapas do [Guia do desenvolvedor do Registro de Schema](../xdm/api/getting-started.md).

### Já existe uma função com o mesmo nome para o esquema especificado ou definedOn

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

Ao criar um novo atributo calculado, esse erro ocorre quando a propriedade `name` fornecida já está sendo usada para o schema indicado em `schema.name`. Substitua o valor por um nome exclusivo antes de tentar novamente.

### O esquema de retorno da expressão não é igual ao esquema do atributo calculado no esquema XDM

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

Ao criar um novo atributo calculado, esse erro ocorre quando a propriedade `name` fornecida já está sendo usada para o schema indicado em `schema.name`. Substitua o valor por um nome exclusivo antes de tentar novamente.

### Solicitação de exclusão inválida (Tarefa do Sistema de Perfil)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

Este erro ocorre quando uma carga inválida é fornecida para um trabalho de sistema de exclusão. Verifique se você está fornecendo um conjunto de dados ou ID de lote válido nas propriedades `dataSetID` ou `batchID` da carga, respectivamente. Consulte a seção [criar uma solicitação de exclusão](./api/profile-system-jobs.md#create-a-delete-request) no Guia do desenvolvedor de perfil para obter mais informações.

### Lote não encontrado para o conjunto de dados do perfil

```json
{
  "requestId":"LlTmQkhgHKFGHGHnIkmUxcIL4YTFSpQw",
  "errors":{
    "400":[
      {
        "code":"400",
        "message":"Batch not found for profile dataset '5da688d2c4e60518ad25b7b1'"
      }
    ]
  }
}
```

Este erro ocorre quando não foi possível localizar um lote válido ao tentar criar uma solicitação de exclusão para dados do perfil. Verifique se você inseriu a ID correta para um conjunto de dados habilitado para perfil antes de tentar novamente.

### O destino de projeção ainda não foi criado

```json
{
  "status":404,
  "title":"The projection destination has not yet been created.",
  "type":"http://ns.adobe.com/adobecloud/problem/missing-entity"
}
```

Esse erro ocorre quando o `destinationId` fornecido em uma solicitação `POST /config/projections` é inválido. Verifique novamente se você forneceu uma ID de destino válida antes de tentar novamente. Para criar um novo destino, siga as etapas descritas no [Guia do desenvolvedor de perfil](./api/edge-projections.md#create-a-destination).

### Tipo de mídia não suportado

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

Este erro ocorre ao enviar uma solicitação POST ou PUT com um cabeçalho Content-Type inválido. Verifique novamente se você está fornecendo um valor válido de Tipo de conteúdo para o endpoint que está usando.

A maioria dos pontos de extremidade do perfil aceita &quot;application/json&quot; para o cabeçalho Content-Type, com as seguintes exceções:

| Endpoint | Tipo de conteúdo |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json; versão=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json; versão=1 |
