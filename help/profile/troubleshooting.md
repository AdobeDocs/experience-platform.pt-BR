---
keywords: Experience Platform;perfil;perfil do cliente em tempo real;solução de problemas;API
title: Guia de solução de problemas do Perfil do cliente em tempo real
topic: guide
type: Documentation
description: Este documento fornece respostas a perguntas frequentes sobre o Perfil do cliente em tempo real, bem como um guia de solução de problemas para erros comuns ao trabalhar com dados do Perfil usando o Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---


# Guia de solução de problemas do Perfil do cliente em tempo real

Este documento fornece respostas a perguntas frequentes sobre o Perfil do cliente em tempo real, bem como um guia de solução de problemas para erros comuns. Para questões e solução de problemas relacionados a outros serviços no Adobe Experience Platform, consulte o [guia de solução de problemas do Experience Platform](../landing/troubleshooting.md).

Com [!DNL Real-time Customer Profile], você pode ver uma visualização holística de cada cliente individual combinando dados de vários canais, incluindo on-line, off-line, CRM e de terceiros. Isso permite que os profissionais de marketing conduzam experiências coordenadas, consistentes e relevantes para os clientes em vários canais.

## Perguntas frequentes

Veja a seguir uma lista de respostas para perguntas frequentes sobre o Perfil do cliente em tempo real.

### Que tipos de dados são aceitos para o Perfil do cliente em tempo real?

O perfil aceita os dados **record** e **time-series**, desde que os dados em questão contenham pelo menos um valor de identidade que associe os dados a uma pessoa individual exclusiva.

Como todos os serviços da plataforma, o Perfil exige que seus dados sejam estruturados semanticamente em um schema do Modelo de Dados de Experiência (XDM). Por sua vez, esse schema deve ter uma **identidade primária** definida e estar habilitado para uso no Perfil.

Se você não estiver familiarizado com o XDM, start com a [visão geral do XDM](../xdm/home.md) para saber mais. Em seguida, consulte o guia do usuário XDM para obter etapas sobre como [definir campos de identidade](../xdm/tutorials/create-schema-ui.md#identity-field) e [ativar um schema para Perfil](../xdm/tutorials/create-schema-ui.md#profile).

### Onde os dados do Perfil são armazenados?

O Perfil do cliente em tempo real mantém seu próprio armazenamento de dados (conhecido como &quot;repositório de Perfis&quot;), separado do Data Lake que contém outros dados de plataforma assimilados.

### Se eu já ingerir dados na Plataforma, posso disponibilizá-los na Perfil store?

Se os dados tiverem sido ingeridos em um conjunto de dados que não seja de Perfil, você deverá assimilá-los novamente em um conjunto de dados habilitado para Perfil para disponibilizá-los no repositório de Perfis. É possível habilitar um conjunto de dados existente para o Perfil, no entanto, quaisquer dados que foram ingeridos antes dessa configuração ainda não aparecerão no repositório de Perfis.

Se desejar adicionar dados ingeridos anteriormente ao repositório de Perfis, siga o tutorial de [configuração do conjunto de dados](./tutorials/dataset-configuration.md) para criar um novo conjunto de dados ou converter um conjunto de dados existente para ser ativado para o Perfil e, em seguida, assimile novamente os dados desejados nesse conjunto de dados.

### Como posso visualização meus dados de Perfil ingeridos?

Existem vários métodos de exibição de dados de Perfil, dependendo se você está usando a API ou a interface do usuário.

#### Uso da API

Se você souber as IDs das entidades de Perfil que deseja acessar, poderá usar o endpoint `/entities` (acesso ao Perfil) na API do Perfil para pesquisar essas entidades. Consulte a seção sobre [entidades](./api/entities.md) no guia do desenvolvedor para obter mais informações.

Você também pode usar a Adobe Experience Platform Segmentation Service API para acessar os perfis individuais dos clientes que se qualificaram para uma associação de segmento. Consulte [Visão geral do Serviço de segmentação](../segmentation/home.md) para obter mais informações.

#### Uso da interface

Na interface do usuário do Experience Platform, a guia **[!UICONTROL Procurar]** no espaço de trabalho **[!UICONTROL Perfis]** permite que você visualização a contagem total de perfis e procure perfis individuais pelo valor de identidade. Consulte o [Guia do usuário do Perfil](./ui/user-guide.md) para obter mais informações.

Você também pode visualização uma lista de seus segmentos na guia **[!UICONTROL Procurar]** na área de trabalho **[!UICONTROL Segmentos]**. Depois de selecionar um segmento, uma amostra de perfis qualificados para esse segmento é exibida. Você pode selecionar qualquer um desses perfis listados para visualização de seus detalhes. Consulte [Visão geral da interface de segmentação](../segmentation/ui/overview.md) para obter mais informações.

## Códigos de erro

Veja a seguir uma lista de mensagens de erro que você pode encontrar ao trabalhar com a API do Perfil do cliente em tempo real. Se o erro encontrado não estiver listado aqui, você pode encontrá-lo no [Guia geral de solução de problemas da plataforma](../landing/troubleshooting.md).

### Não foi possível pesquisar o schema do atributo calculado para o caminho fornecido

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

Ao criar um novo atributo calculado, esse erro ocorre quando o sistema não conseguiu localizar o schema fornecido na carga da solicitação. Verifique se você forneceu a ID de locatário correta na propriedade `path` da carga e se os valores de `schema.name` são um nome de schema válido.

Se você não souber sua ID de locatário, poderá recuperá-la seguindo as etapas no [Guia do desenvolvedor do Registro de Schemas](../xdm/api/getting-started.md).

### A função com o mesmo nome já existe para o schema especificado ou definedOn

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

Ao criar um novo atributo calculado, esse erro ocorre quando a propriedade `name` fornecida já está sendo usada para o schema indicado em `schema.name`. Substitua o valor por um nome exclusivo antes de tentar novamente.

### O schema de retorno da expressão não é igual ao schema do atributo calculado no schema XDM

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

Ao criar um novo atributo calculado, esse erro ocorre quando a propriedade `name` fornecida já está sendo usada para o schema indicado em `schema.name`. Substitua o valor por um nome exclusivo antes de tentar novamente.

### Solicitação de exclusão inválida (Trabalho do Sistema do Perfil)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

Esse erro ocorre quando uma carga inválida é fornecida para um trabalho de exclusão do sistema. Verifique se você está fornecendo um conjunto de dados ou uma ID de lote válidos sob as propriedades `dataSetID` ou `batchID` da carga, respectivamente. Consulte a seção [criar uma solicitação de exclusão](./api/profile-system-jobs.md#create-a-delete-request) no guia do desenvolvedor do Perfil para obter mais informações.

### Lote não encontrado para conjunto de dados de perfil

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

Este erro ocorre quando não é possível localizar um lote válido ao tentar criar uma solicitação de exclusão para dados de Perfil. Verifique se você inseriu a ID correta para um conjunto de dados habilitado para Perfis antes de tentar novamente.

### O destino da projeção ainda não foi criado

```json
{
  "status":404,
  "title":"The projection destination has not yet been created.",
  "type":"http://ns.adobe.com/adobecloud/problem/missing-entity"
}
```

Este erro ocorre quando `destinationId` fornecido em uma solicitação `POST /config/projections` é inválido. Verifique se você forneceu uma ID de destino válida antes de tentar novamente. Para criar um novo destino, siga as etapas descritas no [guia do desenvolvedor do Perfil](./api/edge-projections.md#create-a-destination).

### Tipo de mídia não suportado

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

Esse erro ocorre ao enviar uma solicitação POST ou PUT com um cabeçalho Content-Type inválido. Verifique se você está fornecendo um valor Content-Type válido para o terminal que está usando.

A maioria dos pontos de extremidade do Perfil aceita &quot;application/json&quot; para seu cabeçalho Content-Type, com as seguintes exceções:

| Ponto final | Tipo de conteúdo |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json; version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json; version=1 |