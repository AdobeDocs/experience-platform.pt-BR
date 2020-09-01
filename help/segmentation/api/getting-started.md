---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;api;
solution: Experience Platform
title: Guia do desenvolvedor do Serviço de segmentação
topic: developer guide
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---


# Getting started with [!DNL Segmentation Service] {#getting-started}

A Adobe Experience Platform [!DNL Segmentation Service] permite que você crie segmentos e gere audiências no Adobe Experience Platform a partir de seus [!DNL Real-time Customer Profile] dados.

O guia do desenvolvedor requer uma compreensão funcional dos diversos [!DNL Experience Platform] serviços envolvidos no uso [!DNL Segmentation Service].

- [[!Segmentação DNL]](../home.md): Permite que você crie segmentos de audiência a partir de [!DNL Real-time Customer Profile] dados.
- [Sistema do [!DNL Experience Data Model (XDM)](../../xdm/home.md): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
- [[!DNL Perfil do cliente em tempo real]](../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
- [Caixas de proteção](../../sandboxes/home.md): [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para trabalhar com a [!DNL Segmentation] API.

## Lendo chamadas de exemplo da API

A documentação da [!DNL Segmentation Service] API fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de [!DNL Experience Platform] solução de problemas.

## Cabeçalhos obrigatórios

A documentação da API também exige que você tenha concluído o tutorial [de](../../tutorials/authentication.md) autenticação para fazer chamadas com êxito para [!DNL Platform] pontos de extremidade. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em chamadas de [!DNL Experience Platform] API, como mostrado abaixo:

- Autorização: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção na qual a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre como trabalhar com caixas de proteção em [!DNL Experience Platform], consulte a documentação [de visão geral das](../../sandboxes/home.md)caixas de proteção.

## Próximas etapas

Para fazer chamadas usando a [!DNL Segmentation Service] API, selecione um dos guias de ponto de extremidade disponíveis usando a navegação esquerda ou dentro da visão geral do guia do [desenvolvedor](./overview.md)