---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation Service;api;
solution: Experience Platform
title: Guia do desenvolvedor do Serviço de segmentação
topic: developer guide
description: A documentação a seguir fornece informações adicionais que você precisa saber para trabalhar com a API de segmentação com êxito.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# Introdução a [!DNL Segmentation Service] {#getting-started}

O Adobe Experience Platform [!DNL Segmentation Service] permite que você crie segmentos e gere audiências no Adobe Experience Platform a partir de seus dados [!DNL Real-time Customer Profile].

O guia do desenvolvedor requer uma compreensão funcional dos vários [!DNL Experience Platform] serviços envolvidos com o uso de [!DNL Segmentation Service].

- [[!DNL Segmentation]](../home.md): Permite que você crie segmentos de audiência a partir de  [!DNL Real-time Customer Profile] dados.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
- [Caixas de proteção](../../sandboxes/home.md):  [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para trabalhar com êxito com a API [!DNL Segmentation].

## Lendo chamadas de exemplo da API

A documentação da API [!DNL Segmentation Service] fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção em [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

## Cabeçalhos obrigatórios

A documentação da API também exige que você tenha concluído o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para [!DNL Platform] pontos de extremidade. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em [!DNL Experience Platform] chamadas de API, como mostrado abaixo:

- Autorização: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção na qual a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre como trabalhar com caixas de proteção em [!DNL Experience Platform], consulte a [documentação de visão geral das caixas de proteção](../../sandboxes/home.md).

## Próximas etapas

Para fazer chamadas usando a API [!DNL Segmentation Service], selecione um dos guias de ponto final disponíveis usando a navegação à esquerda ou dentro da [visão geral do guia do desenvolvedor](./overview.md)