---
keywords: Experience Platform; home; tópicos populares; segmentação; Segmentação; Serviço de segmentação; api;
solution: Experience Platform
title: Introdução à API do serviço de segmentação
topic-legacy: developer guide
description: A documentação a seguir fornece informações adicionais que você precisa saber para trabalhar com êxito com a API de segmentação.
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# Introdução à API do serviço de segmentação {#getting-started}

O Adobe Experience Platform [!DNL Segmentation Service] permite que você crie segmentos e gere públicos no Adobe Experience Platform a partir de seus dados [!DNL Real-time Customer Profile].

O guia do desenvolvedor requer uma compreensão funcional dos vários serviços [!DNL Experience Platform] envolvidos com o uso de [!DNL Segmentation Service].

- [[!DNL Segmentation]](../home.md): Permite criar segmentos de público-alvo a partir de  [!DNL Real-time Customer Profile] dados.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
- [Sandboxes](../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para trabalhar com êxito com a API [!DNL Segmentation].

## Lendo exemplos de chamadas de API

A documentação da API [!DNL Segmentation Service] fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

## Cabeçalhos obrigatórios

A documentação da API também requer que você tenha concluído o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para pontos de extremidade [!DNL Platform]. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em chamadas de API [!DNL Experience Platform], conforme mostrado abaixo:

- Autorização: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre como trabalhar com sandboxes em [!DNL Experience Platform], consulte a [documentação de visão geral das sandboxes](../../sandboxes/home.md).

## Próximas etapas

Para fazer chamadas usando a API [!DNL Segmentation Service], selecione um dos guias de ponto de extremidade disponíveis usando a navegação à esquerda ou dentro da [visão geral do guia do desenvolvedor](./overview.md)
