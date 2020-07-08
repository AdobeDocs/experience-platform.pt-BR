---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Introdução à API de Perfil do cliente em tempo real
topic: guide
translation-type: tm+mt
source-git-commit: d1656635b6d082ce99f1df4e175d8dd69a63a43a
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---


# Introdução à API do Perfil do cliente em tempo real {#getting-started}

Usando a API Perfil do cliente em tempo real, você pode executar operações CRUD básicas em relação aos recursos do Perfil, como configurar atributos calculados, acessar entidades, exportar dados do Perfil e excluir conjuntos de dados ou lotes desnecessários.

O uso do guia do desenvolvedor requer uma compreensão funcional dos vários serviços de Adobe Experience Platform para trabalhar com dados de Perfis. Antes de começar a trabalhar com a API de Perfil do cliente em tempo real, consulte a documentação dos seguintes serviços:

* [Perfil](../home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o cliente, com base em dados agregados de várias fontes.
* [Serviço](../../identity-service/home.md)de identificação de Adobe Experience Platform: Obtenha uma melhor visualização de seu cliente e de seu comportamento ao unir identidades entre dispositivos e sistemas.
* [Serviço](../../segmentation/home.md)de segmentação de Adobe Experience Platform: Permite criar segmentos de audiência a partir de dados de Perfil do cliente em tempo real.
* [Modelo de dados de experiência (XDM)](../../xdm/home.md): A estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.
* [Caixas de proteção](../../sandboxes/home.md): O Experience Platform fornece caixas de proteção virtuais que particionam uma única instância do Platform em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para pontos de extremidade da API do Perfil.

## Lendo chamadas de exemplo da API

A documentação da API Perfil do cliente em tempo real fornece exemplos de chamadas de API para demonstrar como formatar as solicitações corretamente. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de solução de problemas do Experience Platform.

## Cabeçalhos obrigatórios

A documentação da API também exige que você tenha concluído o tutorial [de](../../tutorials/authentication.md) autenticação para fazer chamadas com êxito para pontos de extremidade da Platform. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em chamadas de API de Experience Platform, como mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos no Experience Platform são isolados para caixas de proteção virtuais específicas. As solicitações às APIs da Platform exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Para obter mais informações sobre caixas de proteção no Platform, consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

Todas as solicitações com uma carga no corpo da solicitação (como chamadas POST, PUT e PATCH) devem incluir um `Content-Type` cabeçalho. Valores aceitos específicos para cada chamada são fornecidos nos parâmetros da chamada.

## Próximas etapas

Para começar a fazer chamadas usando a API Perfil do cliente em tempo real, selecione um dos guias de ponto de extremidade disponíveis.