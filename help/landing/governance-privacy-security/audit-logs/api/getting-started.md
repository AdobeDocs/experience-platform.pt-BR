---
title: Introdução à API de consulta de auditoria
description: A API de Consulta de auditoria permite recuperar dados de métricas para vários recursos do Adobe Experience Platform. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API de consulta de auditoria.
exl-id: 20eab0a8-98f7-4fee-8f91-88324e54ab18
source-git-commit: c2c5778e0a3fff7f488ad7a672123c813cca59f1
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 9%

---

# Introdução à API de consulta de auditoria

O Adobe Experience Platform permite auditar a atividade do usuário em vários serviços e recursos na forma de logs de eventos de auditoria. Cada ação registrada em um log contém metadados que indicam o tipo de ação, a data e a hora, a ID do email do usuário que executou a ação e atributos adicionais relevantes ao tipo de ação.

A API de Consulta de auditoria permite auditar a atividade do usuário em vários serviços e recursos na forma de logs de eventos de auditoria. Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API de consulta de auditoria.

## Pré-requisitos

Para gerenciar eventos de auditoria, você deve ter a **[!UICONTROL Exibir log de atividades do usuário]** permissão de controle de acesso concedida (encontrada sob o [!UICONTROL Governança de dados] categoria). Para saber como gerenciar permissões individuais para recursos da Platform, consulte a [documentação de controle de acesso](../../../../access-control/home.md).

### Leitura de chamadas de API de amostra

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O exemplo de JSON retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas de Experience Platform.

### Coletar valores para cabeçalhos obrigatórios

Este guia requer que você tenha concluído o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para APIs da Platform. Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API de Experience Platform, conforme mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] são isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá. Para obter mais informações sobre sandboxes no [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT e PATCH) exigem um cabeçalho adicional:

* Tipo de conteúdo: application/json

## Próximas etapas

Para começar a fazer chamadas usando o [!DNL Audit Query] API, consulte a [manual de endpoint de eventos](./events.md) e a variável [exportar guia de endpoint](./export.md).
