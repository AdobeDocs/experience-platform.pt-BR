---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, API
title: Introdução à API do perfil do cliente em tempo real
topic: guide
type: Documentation
description: O guia de introdução à API de perfil descreve os principais conceitos e a funcionalidade básica que você precisa saber para usar os pontos de extremidade da API de perfil do cliente em tempo real para executar operações básicas de CRUD em relação aos dados de perfil.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# Introdução à API [!DNL Real-time Customer Profile] {#getting-started}

Usando os pontos de extremidade da API de perfil do cliente em tempo real, é possível executar operações básicas de CRUD em relação aos dados do perfil, como configurar atributos calculados, acessar entidades, exportar dados do perfil e excluir conjuntos de dados ou lotes desnecessários.

O uso do guia do desenvolvedor requer uma compreensão funcional dos vários serviços da Adobe Experience Platform envolvidos no trabalho com dados [!DNL Profile] . Antes de começar a trabalhar com a API [!DNL Real-time Customer Profile], reveja a documentação dos seguintes serviços:

* [[!DNL Real-time Customer Profile]](../home.md): Fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Obtenha uma melhor visão de seu cliente e de seu comportamento ao unir identidades em dispositivos e sistemas.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md): Permite criar segmentos de público-alvo a partir de dados do Perfil do cliente em tempo real.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.
* [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para os endpoints da API [!DNL Profile].

## Lendo exemplos de chamadas de API

A documentação da API [!DNL Real-time Customer Profile] fornece exemplos de chamadas de API para demonstrar como formatar corretamente as solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

## Cabeçalhos obrigatórios

A documentação da API também requer que você tenha concluído o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para pontos de extremidade [!DNL Platform]. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em chamadas de API [!DNL Experience Platform], conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para sandboxes virtuais específicas. As solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Para obter mais informações sobre sandboxes em [!DNL Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações com uma carga no corpo da solicitação (como chamadas POST, PUT e PATCH) devem incluir um cabeçalho `Content-Type`. Os valores aceitos específicos para cada chamada são fornecidos nos parâmetros de chamada .

## Próximas etapas

Para começar a fazer chamadas usando a API [!DNL Real-time Customer Profile], selecione um dos guias de ponto de extremidade disponíveis.