---
keywords: Experience Platform; home; tópicos populares; segmentação; Segmentação; Serviço de segmentação; api;
solution: Experience Platform
title: Introdução à API do serviço de segmentação
topic-legacy: developer guide
description: A documentação a seguir fornece informações adicionais que você precisa saber para trabalhar com êxito com a API de segmentação.
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 1%

---

# Introdução à API do serviço de segmentação {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] permite criar segmentos e gerar públicos no Adobe Experience Platform a partir de [!DNL Real-time Customer Profile] dados.

O guia do desenvolvedor requer uma compreensão funcional das várias [!DNL Experience Platform] serviços envolvidos na utilização de [!DNL Segmentation Service].

- [[!DNL Segmentation]](../home.md): Permite criar segmentos de público-alvo a partir de [!DNL Real-time Customer Profile] dados.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente. Para utilizar melhor a Segmentação, verifique se os dados são assimilados como perfis e eventos de acordo com a variável [práticas recomendadas para modelagem de dados](../../xdm/schema/best-practices.md).
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para trabalhar com o [!DNL Segmentation] API.

## Lendo exemplos de chamadas de API

O [!DNL Segmentation Service] A documentação da API fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

## Cabeçalhos obrigatórios

A documentação da API também requer que você tenha completado o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas para [!DNL Platform] endpoints. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

- Autorização: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] são isoladas em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre como trabalhar com sandboxes no [!DNL Experience Platform], consulte o [documentação de visão geral das sandboxes](../../sandboxes/home.md).

## Próximas etapas

Para fazer chamadas usando o [!DNL Segmentation Service] API, selecione um dos guias de ponto de extremidade disponíveis usando a navegação à esquerda ou dentro do [visão geral do guia do desenvolvedor](./overview.md)
