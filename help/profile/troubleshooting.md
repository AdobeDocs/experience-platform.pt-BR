---
keywords: Experience Platform;perfil;perfil do cliente em tempo real;solução de problemas;API
title: Guia de solução de problemas do Perfil do cliente em tempo real
type: Documentation
description: Este documento fornece respostas a perguntas frequentes sobre o Perfil do cliente em tempo real, bem como um guia de solução de problemas para erros comuns ao trabalhar com dados de perfil usando o Adobe Experience Platform.
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---

# Guia de solução de problemas do Perfil do cliente em tempo real

Este documento fornece respostas a perguntas frequentes sobre o Perfil do cliente em tempo real, bem como um guia de solução de problemas para erros comuns. Para perguntas e soluções de problemas relacionadas a outros serviços no Adobe Experience Platform, consulte o [guia de solução de problemas do Experience Platform](../landing/troubleshooting.md).

Com o [!DNL Real-Time Customer Profile], você pode ter uma visão holística de cada cliente individual ao combinar dados de vários canais, incluindo online, offline, CRM e de terceiros. Isso permite que os profissionais de marketing promovam experiências coordenadas, consistentes e relevantes para clientes em vários canais.

## Perguntas frequentes

Veja a seguir uma lista de respostas para perguntas frequentes sobre o Perfil do cliente em tempo real.

### Que tipos de dados são aceitos para o Perfil do cliente em tempo real?

O perfil aceita dados de **registro** e **série temporal**, desde que os dados em questão contenham pelo menos um valor de identidade que associe os dados a uma pessoa individual exclusiva.

Como todos os serviços da Experience Platform, o Perfil exige que seus dados sejam semanticamente estruturados em um esquema do Experience Data Model (XDM). Por sua vez, este esquema deve ter uma **identidade principal** definida e estar habilitada para uso no Perfil.

Se você não estiver familiarizado com o XDM, comece com a [visão geral do XDM](../xdm/home.md) para saber mais. Em seguida, consulte o guia do usuário XDM para obter etapas sobre como [definir campos de identidade](../xdm/tutorials/create-schema-ui.md#identity-field) e [habilitar um esquema para o Perfil](../xdm/tutorials/create-schema-ui.md#profile).

### Onde os dados do perfil são armazenados?

O Perfil do cliente em tempo real mantém seu próprio armazenamento de dados (conhecido como &quot;Armazenamento de perfis&quot;), separado do Data Lake que contém outros dados assimilados do Experience Platform.

### Se já assimilei dados na Experience Platform, posso disponibilizá-los na loja de perfis?

Se os dados tiverem sido assimilados em um conjunto de dados que não seja de Perfil, você deverá assimilá-los novamente em um conjunto de dados habilitado para torná-lo disponível no armazenamento de Perfil. É possível habilitar um conjunto de dados existente para o Perfil, no entanto, os dados assimilados antes dessa configuração ainda não aparecerão no armazenamento do Perfil.

Se quiser adicionar dados assimilados anteriormente ao repositório de perfis, siga o [tutorial de configuração de conjunto de dados](./tutorials/dataset-configuration.md) para criar um novo conjunto de dados ou converter um conjunto de dados existente para ser habilitado para o Perfil e, em seguida, assimile novamente os dados desejados nesse conjunto de dados.

### Como posso exibir meus dados de perfil assimilados?

Há vários métodos de exibição de Dados de perfil, dependendo se você está usando a API ou a interface do usuário.

#### Uso da API

Se você souber as IDs das entidades de Perfil que deseja acessar, poderá usar o ponto de extremidade `/entities` (acesso ao perfil) na API de Perfil para pesquisar essas entidades. Consulte a seção sobre [entidades](./api/entities.md) no guia do desenvolvedor para obter mais informações.

Você também pode usar a API do Serviço de segmentação do Adobe Experience Platform para acessar perfis individuais de clientes que se qualificaram para uma associação de público-alvo. Consulte a [visão geral do Serviço de segmentação](../segmentation/home.md) para obter mais informações.

#### Uso da interface

Na interface do usuário do Experience Platform, a guia **[!UICONTROL Procurar]** no espaço de trabalho **[!UICONTROL Perfis]** permite que você exiba a contagem total de perfis e pesquise por perfis individuais por seu valor de identidade. Consulte o [Guia do usuário do perfil](./ui/user-guide.md) para obter mais informações.

Você também pode exibir uma lista de seus públicos na guia **[!UICONTROL Procurar]** do espaço de trabalho **[!UICONTROL Públicos-alvo]**. Após selecionar um público-alvo, uma amostra de perfis qualificados para esse público-alvo é exibida. Em seguida, você pode selecionar qualquer um desses perfis listados para exibir seus detalhes. Consulte a [Visão geral da interface do usuário de segmentação](../segmentation/ui/overview.md) para obter mais informações.

## Códigos de erro

Veja a seguir uma lista de mensagens de erro que você pode encontrar ao trabalhar com a API de perfil do cliente em tempo real. Se o erro encontrado não estiver listado aqui, você poderá encontrá-lo no [guia geral de solução de problemas do Experience Platform](../landing/troubleshooting.md).

### Não foi possível pesquisar o esquema do atributo computado para o caminho fornecido

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

Ao criar um novo atributo calculado, esse erro ocorre quando o sistema não pôde encontrar o esquema fornecido na carga da solicitação. Verifique se você forneceu a ID de locatário correta na propriedade `path` da carga e se os valores de `schema.name` são um nome de esquema válido.

Se você não souber sua ID de locatário, poderá recuperá-la seguindo as etapas no [guia do desenvolvedor do Registro de Esquemas](../xdm/api/getting-started.md).

### Já existe uma função com o mesmo nome para o esquema especificado ou definedOn

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

Ao criar um novo atributo computado, esse erro ocorre quando a propriedade `name` fornecida já está sendo usada para o esquema indicado em `schema.name`. Substitua o valor por um nome exclusivo antes de tentar novamente.

### O esquema de retorno da expressão não é igual ao esquema do atributo calculado no esquema XDM

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

Ao criar um novo atributo computado, esse erro ocorre quando a propriedade `name` fornecida já está sendo usada para o esquema indicado em `schema.name`. Substitua o valor por um nome exclusivo antes de tentar novamente.

### Solicitação de exclusão inválida (Trabalho do Sistema de Perfil)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

Esse erro ocorre quando uma carga inválida é fornecida para um trabalho de exclusão do sistema. Verifique se você está fornecendo um conjunto de dados ou ID de lote válido na propriedade `dataSetID` ou `batchID` da carga, respectivamente. Consulte a seção sobre [criação de uma solicitação de exclusão](./api/profile-system-jobs.md#create-a-delete-request) no guia do desenvolvedor de perfis para obter mais informações.

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

Esse erro ocorre quando um lote válido não pode ser encontrado ao tentar criar uma solicitação de exclusão para dados de perfil. Verifique se você inseriu a ID correta para um conjunto de dados habilitado para perfil antes de tentar novamente.

### Tipo de mídia incompatível

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

Esse erro ocorre ao enviar uma solicitação POST ou PUT com um cabeçalho Content-Type inválido. Verifique se você está fornecendo um valor Content-Type válido para o endpoint que está usando.

A maioria dos endpoints de perfil aceita &quot;application/json&quot; para o cabeçalho Content-Type, com as seguintes exceções:

| Endpoint | Tipo de conteúdo |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json; version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json; version=1 |
