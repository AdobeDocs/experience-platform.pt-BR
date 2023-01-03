---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, API
title: Introdução à API de assimilação de dados
type: Documentation
description: O guia de introdução à API de assimilação de dados descreve os principais conceitos e a funcionalidade básica que você precisa saber antes de começar a assimilar dados no Experience Platform usando APIs.
exl-id: 0653de2b-3268-478b-a23f-c458b6d3df7c
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# Introdução à API de assimilação de dados {#getting-started}

Usando pontos de extremidade da API de assimilação de dados, é possível executar operações básicas de CRUD para assimilar dados no Adobe Experience Platform.

O uso dos guias da API requer uma compreensão funcional de vários serviços da Adobe Experience Platform envolvidos no trabalho com dados. Antes de usar a API de assimilação de dados, revise a documentação dos seguintes serviços:

* [Ingestão em lote](./overview.md): Permite assimilar dados no Adobe Experience Platform como arquivos em lote.
* [[!DNL Real-Time Customer Profile]](../home.md): Fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas para o [!DNL Profile] Pontos de extremidade da API.

## Lendo exemplos de chamadas de API

A documentação da API de assimilação de dados fornece exemplos de chamadas de API para demonstrar como formatar corretamente as solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

## Cabeçalhos obrigatórios

A documentação da API também requer que você tenha completado o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas para [!DNL Platform] endpoints. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todas as solicitações com uma carga no corpo da solicitação (como chamadas de POST, PUT e PATCH) devem incluir uma `Content-Type` cabeçalho. Os valores aceitos específicos para cada chamada são fornecidos nos parâmetros de chamada .

Todos os recursos em [!DNL Experience Platform] são isoladas em sandboxes virtuais específicas. Solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Para obter mais informações sobre sandboxes em [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).
