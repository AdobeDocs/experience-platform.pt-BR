---
keywords: Experience Platform;página inicial;tópicos populares;DULE;dule
solution: Experience Platform
title: Introdução à API de serviço de política
description: A API de serviço de política permite criar e gerenciar vários recursos relacionados à Governança de dados do Adobe Experience Platform. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API do serviço de política.
role: Developer
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 8%

---

# Introdução à API [!DNL Policy Service]

A API [!DNL Policy Service] permite criar e gerenciar vários recursos relacionados à Governança de dados do Adobe Experience Platform. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API [!DNL Policy Service].

## Pré-requisitos

O uso do guia do desenvolvedor requer uma compreensão funcional dos vários serviços do [!DNL Experience Platform] envolvidos no trabalho com os recursos de Governança de dados. Antes de começar a trabalhar com o [!DNL Policy Service API], reveja a documentação dos seguintes serviços:

* [Governança de dados](../home.md): a estrutura pela qual o [!DNL Experience Platform] impõe conformidade com o uso de dados.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
* [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Leitura de chamadas de API de amostra

A documentação da API [!DNL Policy Service] fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

## Cabeçalhos obrigatórios

A documentação da API também requer que você tenha concluído o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para pontos de extremidade [!DNL Experience Platform]. Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários nas chamadas de API [!DNL Experience Platform], conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos os recursos em [!DNL Experience Platform], incluindo aqueles pertencentes à Governança de dados, estão isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Experience Platform] APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Experience Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm um conteúdo (POST, PUT, PATCH) exigem um cabeçalho adicional:

* `Content-Type: application/json`

## Recursos principais vs. personalizados

Na API [!DNL Policy Service], todas as políticas e ações de marketing são chamadas de recursos `core` ou `custom`.

`core` recursos são aqueles definidos e mantidos pela Adobe, enquanto `custom` recursos são aqueles criados e mantidos pela sua organização e, portanto, são exclusivos e visíveis apenas para a sua organização. Sendo assim, as operações de listagem e pesquisa (`GET`) são as únicas operações permitidas em `core` recursos, enquanto as operações de listagem, pesquisa e atualização (`POST`, `PUT`, `PATCH` e `DELETE`) estão disponíveis para `custom` recursos.

## Próximas etapas

Para começar a fazer chamadas usando a API de serviço de política, selecione um dos manuais de endpoint disponíveis.
