---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Introdução à API do Serviço de Política
topic: developer guide
translation-type: tm+mt
source-git-commit: cb3a17aa08c67c66101cbf3842bf306ebcca0305
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---


# Introdução à [!DNL Policy Service] API

A [!DNL Policy Service] API permite que você crie e gerencie vários recursos relacionados ao Adobe Experience Platform [!DNL Data Governance]. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a [!DNL Policy Service] API.

## Pré-requisitos

O uso do guia do desenvolvedor requer uma compreensão trabalhada dos vários [!DNL Experience Platform] serviços envolvidos no trabalho com os recursos de controle de dados. Antes de começar a trabalhar com o [!DNL Policy Service API], consulte a documentação dos seguintes serviços:

* [[!DNL Data Governance]](../home.md): A estrutura pela qual [!DNL Experience Platform] aplica a conformidade de uso de dados.
* [Sistema do [!DNL Experience Data Model (XDM)](../../xdm/home.md): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
* [[!DNL Perfil do cliente em tempo real]](../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
* [Caixas de proteção](../../sandboxes/home.md): [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

## Lendo chamadas de exemplo da API

A documentação da [!DNL Policy Service] API fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de [!DNL Experience Platform] solução de problemas.

## Cabeçalhos obrigatórios

A documentação da API também exige que você tenha concluído o tutorial [de](../../tutorials/authentication.md) autenticação para fazer chamadas com êxito para [!DNL Platform] pontos de extremidade. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em chamadas de [!DNL Experience Platform] API, como mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo os pertencentes a [!DNL Data Governance], são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

* `Content-Type: application/json`

## Recursos principais vs. personalizados

Na [!DNL Policy Service] API, todas as políticas e ações de marketing são referidas como `core` `custom` recursos.

`core` os recursos são aqueles definidos e mantidos pelo Adobe, enquanto `custom` os recursos são aqueles criados e mantidos pela sua organização, e portanto são exclusivos e visíveis apenas para a sua Organização IMS. Dessa forma, as operações de listagem e pesquisa (`GET`) são as únicas operações permitidas em `core` recursos, enquanto as operações de listagem, pesquisa e atualização (`POST`, `PUT`, `PATCH`e `DELETE`) estão disponíveis para `custom` recursos.

## Próximas etapas

Para começar a fazer chamadas usando a API de serviço de política, selecione um dos guias de ponto de extremidade disponíveis.