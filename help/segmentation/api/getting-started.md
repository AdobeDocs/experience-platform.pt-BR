---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia do desenvolvedor do Serviço de segmentação
topic: developer guide
translation-type: tm+mt
source-git-commit: aff81a4f3243ef77cbdfc776220a5de46e360084
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# Getting started with [!DNL Segmentation Service] {#getting-started}

O Serviço de segmentação de Adobe Experience Platform permite que você crie segmentos e gere audiências no Adobe Experience Platform a partir de seus [!DNL Real-time Customer Profile] dados.

O guia do desenvolvedor requer uma compreensão funcional dos vários serviços de Experience Platform envolvidos com o uso [!DNL Segmentation Service].

- [!DNL Segmentation](../home.md): Permite criar segmentos de audiência a partir de dados de Perfil do cliente em tempo real.
- [!DNL Experience Data Model (XDM) System](../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
- [!DNL Real-time Customer Profile](../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
- [Caixas de proteção](../../sandboxes/home.md): O Experience Platform fornece caixas de proteção virtuais que particionam uma única instância do Platform em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para trabalhar com a [!DNL Segmentation] API.

## Lendo chamadas de exemplo da API

A documentação da [!DNL Segmentation Service] API fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de solução de problemas do Experience Platform.

## Cabeçalhos obrigatórios

A documentação da API também exige que você tenha concluído o tutorial [de](../../tutorials/authentication.md) autenticação para fazer chamadas com êxito para pontos de extremidade da Platform. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em chamadas de API de Experience Platform, como mostrado abaixo:

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