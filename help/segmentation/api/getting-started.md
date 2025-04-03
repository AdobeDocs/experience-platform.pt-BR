---
keywords: Experience Platform;home;popular tópicos;segmentação;Segmentação;Serviço de segmentação;api;
solution: Experience Platform
title: Introdução à API do serviço de segmentação
description: A documentação a seguir fornece informações adicionais que você precisa saber para trabalhar com êxito com a API de segmentação.
role: Developer
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 7%

---

# Introdução à API do serviço de segmentação {#getting-started}

O Adobe Experience Platform [!DNL Segmentation Service] permite criar públicos-alvo por meio de definições de segmento ou outras fontes no Adobe Experience Platform a partir dos dados do [!DNL Real-Time Customer Profile].

O guia do desenvolvedor requer uma compreensão funcional dos vários serviços do [!DNL Experience Platform] envolvidos no uso do [!DNL Segmentation Service].

- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): permite que você compile públicos a partir de dados de [!DNL Real-Time Customer Profile].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente. Para melhor usar a Segmentação, verifique se seus dados são assimilados como perfis e eventos de acordo com as [práticas recomendadas para modelagem de dados](../../xdm/schema/best-practices.md).
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para trabalhar com êxito com a API [!DNL Segmentation].

## Leitura de chamadas de API de amostra

A documentação da API [!DNL Segmentation Service] fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

## Cabeçalhos obrigatórios

A documentação da API também requer que você tenha concluído o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para pontos de extremidade [!DNL Experience Platform]. Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários nas chamadas de API [!DNL Experience Platform], conforme mostrado abaixo:

- Autorização: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] estão isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Experience Platform] APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre como trabalhar com sandboxes em [!DNL Experience Platform], consulte a [documentação de visão geral das sandboxes](../../sandboxes/home.md).

## Próximas etapas

Para fazer chamadas usando a API [!DNL Segmentation Service], selecione um dos manuais de endpoint disponíveis, usando a navegação à esquerda ou na [visão geral do guia do desenvolvedor](./overview.md)
