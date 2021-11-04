---
keywords: Experience Platform, home, tópicos populares, DULE, dule
solution: Experience Platform
title: Introdução à API do serviço de política
topic-legacy: developer guide
description: A API do Serviço de política permite criar e gerenciar vários recursos relacionados à Governança de dados do Adobe Experience Platform. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API do serviço de política.
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---

# Introdução ao [!DNL Policy Service] API

O [!DNL Policy Service] A API permite criar e gerenciar vários recursos relacionados à Governança de dados do Adobe Experience Platform. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para o [!DNL Policy Service] API.

## Pré-requisitos

O uso do guia do desenvolvedor requer uma compreensão funcional das várias [!DNL Experience Platform] serviços envolvidos no trabalho com recursos de Governança de dados. Antes de começar a trabalhar com a variável [!DNL Policy Service API], revise a documentação dos seguintes serviços:

* [Governança de dados](../home.md): A estrutura pela qual [!DNL Experience Platform] aplica a conformidade do uso de dados.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
* [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Lendo exemplos de chamadas de API

O [!DNL Policy Service] A documentação da API fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

## Cabeçalhos obrigatórios

A documentação da API também requer que você tenha completado o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas para [!DNL Platform] endpoints. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo aqueles pertencentes à Governança de dados, são isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho adicional:

* `Content-Type: application/json`

## Recursos principais vs. personalizados

No [!DNL Policy Service] Todas as políticas e ações de marketing são referidas como `core` ou `custom` recursos.

`core` os recursos são os definidos e mantidos por Adobe, enquanto `custom` Os recursos são aqueles criados e mantidos pela organização e, portanto, são exclusivos e visíveis apenas pela organização IMS. Assim, operações de listagem e pesquisa (`GET`) são as únicas operações permitidas em `core` recursos, enquanto as operações de listagem, pesquisa e atualização (`POST`, `PUT`, `PATCH`e `DELETE`) estão disponíveis para `custom` recursos.

## Próximas etapas

Para começar a fazer chamadas usando a API do serviço de política, selecione um dos guias de ponto de extremidade disponíveis.
