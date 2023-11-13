---
keywords: Experience Platform;perfil;perfil de cliente em tempo real;solução de problemas;API
title: Introdução à API de perfil do cliente em tempo real
type: Documentation
description: O guia de introdução à API de perfil descreve os principais conceitos e a funcionalidade básica que você precisa saber para usar os endpoints da API de perfil do cliente em tempo real para executar operações CRUD básicas em relação aos dados do perfil.
exl-id: 7e30610a-a7e7-43ab-a45d-fd84ef6e36ef
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 12%

---

# Introdução ao [!DNL Real-Time Customer Profile] API {#getting-started}

Usando endpoints da API de perfil do cliente em tempo real, você pode executar operações CRUD básicas em relação aos dados do perfil, como configurar atributos calculados, acessar entidades, exportar dados do perfil e excluir conjuntos de dados ou lotes desnecessários.

O uso do guia do desenvolvedor requer uma compreensão funcional dos vários serviços da Adobe Experience Platform envolvidos no trabalho com o [!DNL Profile] dados. Antes de começar a trabalhar com o [!DNL Real-Time Customer Profile] , consulte a documentação dos seguintes serviços:

* [[!DNL Real-Time Customer Profile]](../home.md): fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): obtenha uma melhor visualização do cliente e do comportamento dele ao unir as identidades de vários dispositivos e sistemas.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md): permite criar públicos-alvo a partir dos dados do Perfil do cliente em tempo real.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): a estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para o [!DNL Profile] Endpoints de API.

## Leitura de chamadas de API de amostra

A variável [!DNL Real-Time Customer Profile] A documentação da API fornece exemplos de chamadas de API para demonstrar como formatar solicitações corretamente. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no manual de solução de problemas da [!DNL Experience Platform].

## Cabeçalhos obrigatórios

A documentação da API também exige que você tenha concluído a [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para o [!DNL Platform] pontos finais. Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários no [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos os recursos em [!DNL Experience Platform] são isolados em sandboxes virtuais específicas. Solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Para obter mais informações sobre sandboxes no [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações com uma carga no corpo da solicitação (como chamadas POST, PUT e PATCH) devem incluir uma `Content-Type` cabeçalho. Os valores aceitos específicos para cada chamada são fornecidos nos parâmetros de chamada.

## Próximas etapas

Para começar a fazer chamadas usando o [!DNL Real-Time Customer Profile] , selecione um dos manuais de endpoint disponíveis.
