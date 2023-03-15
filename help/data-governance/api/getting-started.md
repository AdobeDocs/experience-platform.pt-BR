---
keywords: Experience Platform;página inicial;tópicos populares;DULE;dule
solution: Experience Platform
title: Introdução à API de serviço de política
description: A API de serviço de política permite criar e gerenciar vários recursos relacionados à Governança de dados do Adobe Experience Platform. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API do serviço de política.
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---

# Introdução ao [!DNL Policy Service] API

A variável [!DNL Policy Service] A API permite criar e gerenciar vários recursos relacionados à Governança de dados do Adobe Experience Platform. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para o [!DNL Policy Service] API.

## Pré-requisitos

O uso do guia do desenvolvedor requer um entendimento prático dos vários [!DNL Experience Platform] serviços envolvidos no trabalho com os recursos de governança de dados. Antes de começar a trabalhar com o [!DNL Policy Service API], consulte a documentação dos seguintes serviços:

* [Governança de dados](../home.md): a estrutura pela qual [!DNL Experience Platform] aplica a conformidade com o uso de dados.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
* [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Leitura de chamadas de API de amostra

A variável [!DNL Policy Service] A documentação da API fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O exemplo de JSON retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

## Cabeçalhos obrigatórios

A documentação da API também exige que você tenha concluído a [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para o [!DNL Platform] pontos finais. Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários no [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos os recursos em [!DNL Experience Platform], incluindo aqueles pertencentes ao Data Governance, são isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes no [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

* `Content-Type: application/json`

## Recursos principais vs. personalizados

No prazo de [!DNL Policy Service] API, todas as políticas e ações de marketing são chamadas de `core` ou `custom` recursos.

`core` os recursos são os definidos e mantidos pela Adobe, enquanto `custom` Os recursos são aqueles criados e mantidos por sua organização e, portanto, são exclusivos e visíveis apenas para sua organização IMS. Como tal, operações de listagem e pesquisa (`GET`) são as únicas operações permitidas em `core` recursos, enquanto as operações de listagem, pesquisa e atualização (`POST`, `PUT`, `PATCH`, e `DELETE`) estão disponíveis para `custom` recursos.

## Próximas etapas

Para começar a fazer chamadas usando a API de serviço de política, selecione um dos manuais de endpoint disponíveis.
