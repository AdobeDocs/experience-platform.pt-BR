---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia do desenvolvedor do Privacy Service
description: Use a RESTful API para gerenciar os dados pessoais das pessoas em questão nos aplicativos da Adobe Experience Cloud
topic: developer guide
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46

---


# Guia do desenvolvedor do Privacy Service

O Adobe Experience Platform Privacy Service fornece uma API RESTful e uma interface de usuário que permitem gerenciar (acessar e excluir) os dados pessoais de suas pessoas de dados (clientes) nos aplicativos da Adobe Experience Cloud. O Privacy Service também fornece um mecanismo central de auditoria e registro que permite acessar o status e os resultados de trabalhos que envolvem aplicativos da Experience Cloud.

Este guia aborda como usar a API Privacy Service. Para obter detalhes sobre como usar a interface do usuário, consulte a visão geral [da interface do usuário do](../ui/overview.md)Privacy Service. Para obter uma lista abrangente de todos os pontos de extremidade disponíveis na API do Privacy Service, consulte a referência [à](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html)API.

## Introdução

Este guia exige uma compreensão do trabalho sobre os seguintes recursos da plataforma de experiência:

* [Privacy Service](../home.md): Fornece uma API RESTful e uma interface de usuário que permitem gerenciar o acesso e a exclusão de solicitações de seus participantes de dados (clientes) nos aplicativos da Adobe Experience Cloud.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para a API do Privacy Service.

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md) de API de exemplo no guia de solução de problemas da plataforma Experience.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para APIs de plataforma, você deve primeiro concluir o tutorial [de](../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas da API da plataforma da experiência, como mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

* Tipo de conteúdo: application/json

## Próximas etapas

Agora que você entende quais cabeçalhos devem ser usados, você está pronto para começar a fazer chamadas para a API do Privacy Service. O documento em trabalhos [de](privacy-jobs.md) privacidade percorre as várias chamadas de API que você pode fazer usando a API do Privacy Service. Cada chamada de exemplo inclui o formato de API geral, uma solicitação de amostra mostrando os cabeçalhos necessários e uma resposta de amostra.
