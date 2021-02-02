---
keywords: Experience Platform;home;popular topics;DULE;dule
solution: Experience Platform
title: Introdução à API do Serviço de Política
topic: developer guide
description: A API do Serviço de Política permite que você crie e gerencie vários recursos relacionados ao Adobe Experience Platform Data Governance. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API de serviço de política.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---


# Introdução à API [!DNL Policy Service]

A API [!DNL Policy Service] permite que você crie e gerencie vários recursos relacionados ao Adobe Experience Platform [!DNL Data Governance]. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API [!DNL Policy Service].

## Pré-requisitos

O uso do guia do desenvolvedor requer um entendimento prático dos vários [!DNL Experience Platform] serviços envolvidos no trabalho com os recursos de controle de dados. Antes de começar a trabalhar com [!DNL Policy Service API], consulte a documentação dos seguintes serviços:

* [[!DNL Data Governance]](../home.md): A estrutura pela qual  [!DNL Experience Platform] aplica a conformidade de uso de dados.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
* [Caixas de proteção](../../sandboxes/home.md):  [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

## Lendo chamadas de exemplo da API

A documentação da API [!DNL Policy Service] fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção em [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

## Cabeçalhos obrigatórios

A documentação da API também exige que você tenha concluído o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para [!DNL Platform] pontos de extremidade. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em [!DNL Experience Platform] chamadas de API, como mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo os pertencentes a [!DNL Data Governance], são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a [documentação de visão geral da caixa de proteção](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

* `Content-Type: application/json`

## Recursos principais vs. personalizados

Na API [!DNL Policy Service], todas as políticas e ações de marketing são referidas como recursos `core` ou `custom`.

`core` os recursos são aqueles definidos e mantidos pelo Adobe, enquanto  `custom` os recursos são aqueles criados e mantidos pela sua organização e, portanto, são exclusivos e visíveis apenas para a sua Organização IMS. Dessa forma, as operações de listagem e pesquisa (`GET`) são as únicas operações permitidas nos recursos `core`, enquanto as operações de listagem, pesquisa e atualização (`POST`, `PUT`, `PATCH` e `DELETE`) estão disponíveis para os recursos `custom`.

## Próximas etapas

Para começar a fazer chamadas usando a API de serviço de política, selecione um dos guias de ponto de extremidade disponíveis.