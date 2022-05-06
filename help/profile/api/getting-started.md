---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, API
title: Introdução à API do perfil do cliente em tempo real
topic-legacy: guide
type: Documentation
description: O guia de introdução à API de perfil descreve os principais conceitos e a funcionalidade básica que você precisa saber para usar os pontos de extremidade da API de perfil do cliente em tempo real para executar operações básicas de CRUD em relação aos dados de perfil.
exl-id: 7e30610a-a7e7-43ab-a45d-fd84ef6e36ef
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# Introdução ao [!DNL Real-time Customer Profile] API {#getting-started}

Usando os pontos de extremidade da API de perfil do cliente em tempo real, é possível executar operações básicas de CRUD em relação aos dados do perfil, como configurar atributos calculados, acessar entidades, exportar dados do perfil e excluir conjuntos de dados ou lotes desnecessários.

O uso do guia do desenvolvedor requer uma compreensão funcional dos vários serviços da Adobe Experience Platform envolvidos em trabalhar com a [!DNL Profile] dados. Antes de começar a trabalhar com a variável [!DNL Real-time Customer Profile] Consulte a documentação para obter os seguintes serviços:

* [[!DNL Real-time Customer Profile]](../home.md): Fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Obtenha uma melhor visão de seu cliente e de seu comportamento ao unir identidades em dispositivos e sistemas.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md): Permite criar segmentos de público-alvo a partir de dados do Perfil do cliente em tempo real.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas para o [!DNL Profile] Pontos de extremidade da API.

## Lendo exemplos de chamadas de API

O [!DNL Real-time Customer Profile] A documentação da API fornece exemplos de chamadas de API para demonstrar como formatar corretamente as solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

## Cabeçalhos obrigatórios

A documentação da API também requer que você tenha completado o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas para [!DNL Platform] endpoints. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos os recursos em [!DNL Experience Platform] são isoladas em sandboxes virtuais específicas. Solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Para obter mais informações sobre sandboxes em [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações com uma carga no corpo da solicitação (como chamadas de POST, PUT e PATCH) devem incluir uma `Content-Type` cabeçalho. Os valores aceitos específicos para cada chamada são fornecidos nos parâmetros de chamada .

## Próximas etapas

Para começar a fazer chamadas usando a variável [!DNL Real-time Customer Profile] Selecione um dos guias de endpoint disponíveis para a API.
