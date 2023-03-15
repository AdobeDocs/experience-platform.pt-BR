---
keywords: Experience Platform;perfil;perfil de cliente em tempo real;solução de problemas;API
title: Introdução à API de assimilação de dados
type: Documentation
description: O guia de introdução à API de assimilação de dados descreve os principais conceitos e funcionalidades básicas que você precisa saber antes de começar a assimilar dados no Experience Platform usando APIs.
exl-id: 0653de2b-3268-478b-a23f-c458b6d3df7c
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# Introdução à API de assimilação de dados {#getting-started}

Usando endpoints da API de assimilação de dados, você pode executar operações CRUD básicas para assimilar dados no Adobe Experience Platform.

A utilização dos guias de API exige uma compreensão funcional de vários serviços da Adobe Experience Platform envolvidos no trabalho com dados. Antes de usar a API de assimilação de dados, consulte a documentação dos seguintes serviços:

* [Assimilação em lote](./overview.md): permite assimilar dados na Adobe Experience Platform como arquivos em lote.
* [[!DNL Real-Time Customer Profile]](../home.md): fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): a estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para o [!DNL Profile] Endpoints de API.

## Leitura de chamadas de API de amostra

A documentação da API de assimilação de dados fornece exemplos de chamadas de API para demonstrar como formatar solicitações corretamente. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O exemplo de JSON retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

## Cabeçalhos obrigatórios

A documentação da API também exige que você tenha concluído a [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para o [!DNL Platform] pontos finais. Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários no [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todas as solicitações com uma carga no corpo da solicitação (como chamadas POST, PUT e PATCH) devem incluir uma `Content-Type` cabeçalho. Os valores aceitos específicos para cada chamada são fornecidos nos parâmetros de chamada.

Todos os recursos em [!DNL Experience Platform] são isolados em sandboxes virtuais específicas. Solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Para obter mais informações sobre sandboxes no [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).
