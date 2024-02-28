---
keywords: Experience Platform;página inicial;tópicos populares;segmentação;Segmentação;Serviço de segmentação;api;
solution: Experience Platform
title: Introdução à API do serviço de segmentação
description: A documentação a seguir fornece informações adicionais que você precisa saber para trabalhar com êxito com a API de segmentação.
role: Developer
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 7%

---

# Introdução à API do serviço de segmentação {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] O permite criar públicos-alvo por meio de definições de segmento ou outras fontes no Adobe Experience Platform a partir do [!DNL Real-Time Customer Profile] dados.

O guia do desenvolvedor requer uma compreensão funcional dos vários [!DNL Experience Platform] serviços envolvidos na utilização [!DNL Segmentation Service].

- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): permite criar públicos-alvo a partir do [!DNL Real-Time Customer Profile] dados.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente. Para melhor usar a segmentação, verifique se seus dados são assimilados como perfis e eventos de acordo com a [práticas recomendadas para modelagem de dados](../../xdm/schema/best-practices.md).
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem as informações adicionais que você precisará saber para trabalhar com a [!DNL Segmentation] API.

## Leitura de chamadas de API de amostra

A variável [!DNL Segmentation Service] A documentação da API fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

## Cabeçalhos obrigatórios

A documentação da API também exige que você tenha concluído a [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para o [!DNL Platform] pontos finais. Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários no [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

- Autorização: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] são isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre como trabalhar com sandboxes no [!DNL Experience Platform], consulte o [documentação de visão geral das sandboxes](../../sandboxes/home.md).

## Próximas etapas

Para fazer chamadas usando o [!DNL Segmentation Service] , selecione um dos manuais de endpoint disponíveis, usando a navegação à esquerda ou no [visão geral do guia do desenvolvedor](./overview.md)
