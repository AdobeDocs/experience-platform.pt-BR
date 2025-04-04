---
keywords: Experience Platform;perfil;perfil do cliente em tempo real;solução de problemas;API
title: Introdução à API de assimilação de dados
type: Documentation
description: O guia de introdução à API de assimilação de dados descreve os principais conceitos e funcionalidades básicas que você precisa saber antes de começar a assimilar dados no Experience Platform usando APIs.
exl-id: 0653de2b-3268-478b-a23f-c458b6d3df7c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 6%

---

# Introdução à API de assimilação de dados {#getting-started}

Usando endpoints da API de assimilação de dados, você pode executar operações CRUD básicas para assimilar dados no Adobe Experience Platform.

A utilização dos guias de API exige uma compreensão funcional de vários serviços da Adobe Experience Platform envolvidos no trabalho com dados. Antes de usar a API de assimilação de dados, consulte a documentação dos seguintes serviços:

* [Assimilação em lote](./overview.md): permite assimilar dados na Adobe Experience Platform como arquivos em lote.
* [[!DNL Real-Time Customer Profile]](../home.md): fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para pontos de extremidade de API [!DNL Profile].

## Leitura de chamadas de API de amostra

A documentação da API de assimilação de dados fornece exemplos de chamadas de API para demonstrar como formatar solicitações corretamente. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

## Cabeçalhos obrigatórios

A documentação da API também requer que você tenha concluído o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para pontos de extremidade [!DNL Experience Platform]. Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários nas chamadas de API [!DNL Experience Platform], conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todas as solicitações com uma carga no corpo da solicitação (como chamadas POST, PUT e PATCH) devem incluir um cabeçalho `Content-Type`. Os valores aceitos específicos para cada chamada são fornecidos nos parâmetros de chamada.

Todos os recursos em [!DNL Experience Platform] estão isolados em sandboxes virtuais específicas. As solicitações para [!DNL Experience Platform] APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Para obter mais informações sobre sandboxes em [!DNL Experience Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).
