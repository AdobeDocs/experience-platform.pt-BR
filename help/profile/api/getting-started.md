---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Introdução à API de Perfil do cliente em tempo real
topic: guide
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# Introdução à [!DNL Real-time Customer Profile] API {#getting-started}

Usando a [!DNL Real-time Customer Profile] API, você pode executar operações CRUD básicas em relação aos recursos do Perfil, como configurar atributos calculados, acessar entidades, exportar dados do Perfil e excluir conjuntos de dados ou lotes desnecessários.

O uso do guia do desenvolvedor requer uma compreensão funcional dos vários serviços de Adobe Experience Platform para trabalhar com [!DNL Profile] dados. Antes de começar a trabalhar com a [!DNL Real-time Customer Profile] API, consulte a documentação dos seguintes serviços:

* [!DNL Real-time Customer Profile](../home.md): Fornece um perfil unificado e em tempo real para o cliente, com base em dados agregados de várias fontes.
* [!DNL Adobe Experience Platform Identity Service](../../identity-service/home.md): Obtenha uma melhor visualização de seu cliente e de seu comportamento ao unir identidades entre dispositivos e sistemas.
* [!DNL Adobe Experience Platform Segmentation Service](../../segmentation/home.md): Permite criar segmentos de audiência a partir de dados de Perfil do cliente em tempo real.
* [!DNL Experience Data Model (XDM)](../../xdm/home.md): A estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.
* [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para pontos de extremidade [!DNL Profile] da API.

## Lendo chamadas de exemplo da API

A documentação da [!DNL Real-time Customer Profile] API fornece exemplos de chamadas de API para demonstrar como formatar corretamente as solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de [!DNL Experience Platform] solução de problemas.

## Cabeçalhos obrigatórios

A documentação da API também exige que você tenha concluído o tutorial [de](../../tutorials/authentication.md) autenticação para fazer chamadas com êxito para [!DNL Platform] pontos de extremidade. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em chamadas de [!DNL Experience Platform] API, como mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para caixas de proteção virtuais específicas. As solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

Todas as solicitações com uma carga no corpo da solicitação (como chamadas de POST, PUT e PATCH) devem incluir um `Content-Type` cabeçalho. Valores aceitos específicos para cada chamada são fornecidos nos parâmetros da chamada.

## Próximas etapas

Para começar a fazer chamadas usando a [!DNL Real-time Customer Profile] API, selecione um dos guias de ponto de extremidade disponíveis.