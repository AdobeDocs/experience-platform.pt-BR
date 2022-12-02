---
title: Introdução à API de consulta de auditoria
description: A API Consulta de auditoria permite recuperar dados de métrica para vários recursos do Adobe Experience Platform. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API de consulta de auditoria.
source-git-commit: 5b3459711f41430977f9d7b06f8b35801739207c
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 9%

---

# Introdução à API de consulta de auditoria

O Adobe Experience Platform permite auditar a atividade do usuário para vários serviços e recursos na forma de logs de eventos de auditoria. Cada ação registrada em um log contém metadados que indicam o tipo de ação, a data e a hora, a ID do email do usuário que executou a ação e atributos adicionais relevantes ao tipo de ação.

A API Audit Query permite auditar a atividade do usuário para vários serviços e recursos na forma de logs de eventos de auditoria. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API de consulta de auditoria.

## Pré-requisitos

Para gerenciar eventos de auditoria, é necessário ter a variável **[!UICONTROL Exibir registro de atividades do usuário]** permissão de controle de acesso concedida (encontrada no [!UICONTROL Governança de dados] categoria). Para saber como gerenciar permissões individuais para recursos da plataforma, consulte [documentação de controle de acesso](../../../../access-control/home.md).

### Lendo exemplos de chamadas de API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas do Experience Platform.

### Coletar valores para cabeçalhos necessários

Este guia requer que você tenha completado o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para APIs da plataforma. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API do Experience Platform, conforme mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] são isoladas em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá. Para obter mais informações sobre sandboxes em [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

Todas as solicitações que contêm uma carga útil (POST, PUT e PATCH) exigem um cabeçalho adicional:

* Tipo de conteúdo: application/json

## Próximas etapas

Para começar a fazer chamadas usando a variável [!DNL Audit Query] Consulte a API [guia de endpoint de eventos](./events.md) e [guia de endpoint de exportação](./export.md).
