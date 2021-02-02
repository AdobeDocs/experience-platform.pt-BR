---
keywords: Experience Platform;perfil;perfil do cliente em tempo real;solução de problemas;API
title: Introdução à API de Perfil do cliente em tempo real
topic: guide
type: Documentation
description: O guia de introdução à API do Perfil descreve os conceitos principais e a funcionalidade básica que você precisa saber para usar os pontos finais da API do Perfil do cliente em tempo real para executar operações CRUD básicas em relação aos dados do Perfil.
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---


# Introdução à API [!DNL Real-time Customer Profile] {#getting-started}

Usando os pontos de extremidade da API de Perfil do cliente em tempo real, é possível executar operações CRUD básicas em relação aos dados do Perfil, como configurar atributos calculados, acessar entidades, exportar dados do Perfil e excluir conjuntos de dados ou lotes desnecessários.

O uso do guia do desenvolvedor requer uma compreensão funcional dos vários serviços da Adobe Experience Platform envolvidos no trabalho com [!DNL Profile] dados. Antes de começar a trabalhar com a API [!DNL Real-time Customer Profile], consulte a documentação dos seguintes serviços:

* [[!DNL Real-time Customer Profile]](../home.md): Fornece um perfil unificado e em tempo real para o cliente, com base em dados agregados de várias fontes.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Obtenha uma melhor visualização de seu cliente e de seu comportamento ao unir identidades entre dispositivos e sistemas.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md): Permite criar segmentos de audiência a partir de dados de Perfil do cliente em tempo real.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual a Plataforma organiza os dados de experiência do cliente.
* [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para [!DNL Profile] pontos de extremidade da API.

## Lendo chamadas de exemplo da API

A documentação da API [!DNL Real-time Customer Profile] fornece exemplos de chamadas de API para demonstrar como formatar corretamente as solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção em [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

## Cabeçalhos obrigatórios

A documentação da API também exige que você tenha concluído o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para [!DNL Platform] pontos de extremidade. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em [!DNL Experience Platform] chamadas de API, como mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para caixas de proteção virtuais específicas. As solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a [documentação de visão geral da caixa de proteção](../../sandboxes/home.md).

Todas as solicitações com uma carga no corpo da solicitação (como chamadas de POST, PUT e PATCH) devem incluir um cabeçalho `Content-Type`. Valores aceitos específicos para cada chamada são fornecidos nos parâmetros da chamada.

## Próximas etapas

Para começar a fazer chamadas usando a API [!DNL Real-time Customer Profile], selecione um dos guias de ponto de extremidade disponíveis.