---
keywords: Experience Platform, home, tópicos populares, DULE, dule
solution: Experience Platform
title: Introdução à API do serviço de política
topic-legacy: developer guide
description: A API do Serviço de política permite criar e gerenciar vários recursos relacionados à Governança de dados do Adobe Experience Platform. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API do serviço de política.
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# Introdução à API [!DNL Policy Service]

A API [!DNL Policy Service] permite criar e gerenciar vários recursos relacionados ao Adobe Experience Platform [!DNL Data Governance]. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API [!DNL Policy Service].

## Pré-requisitos

O uso do guia do desenvolvedor requer uma compreensão funcional dos vários serviços [!DNL Experience Platform] envolvidos no trabalho com os recursos de Governança de dados. Antes de começar a trabalhar com o [!DNL Policy Service API], reveja a documentação dos seguintes serviços:

* [[!DNL Data Governance]](../home.md): A estrutura pela qual  [!DNL Experience Platform] aplica a conformidade do uso de dados.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
* [Sandboxes](../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Lendo exemplos de chamadas de API

A documentação da API [!DNL Policy Service] fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

## Cabeçalhos obrigatórios

A documentação da API também requer que você tenha concluído o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para pontos de extremidade [!DNL Platform]. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em chamadas de API [!DNL Experience Platform], conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo aqueles pertencentes a [!DNL Data Governance], são isolados para sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho adicional:

* `Content-Type: application/json`

## Recursos principais vs. personalizados

Na API [!DNL Policy Service], todas as políticas e ações de marketing são chamadas de recursos `core` ou `custom`.

`core` os recursos são aqueles definidos e mantidos pelo Adobe, enquanto  `custom` os recursos são aqueles criados e mantidos pela sua organização, e, portanto, são exclusivos e visíveis apenas na sua Organização IMS. Dessa forma, as operações de listagem e pesquisa (`GET`) são as únicas operações permitidas nos recursos `core`, enquanto as operações de listagem, pesquisa e atualização (`POST`, `PUT`, `PATCH` e `DELETE`) estão disponíveis para os recursos `custom`.

## Próximas etapas

Para começar a fazer chamadas usando a API do serviço de política, selecione um dos guias de ponto de extremidade disponíveis.
