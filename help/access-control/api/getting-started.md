---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia do desenvolvedor do Controle de acesso
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 1%

---


# Guia do desenvolvedor do Controle de acesso

O Controle de acesso for Experience Platform é administrado por meio do [Adobe Admin Console](https://adminconsole.adobe.com). Essa funcionalidade aproveita perfis de produtos no Admin Console, que vinculam usuários com permissões e caixas de proteção. Consulte a visão geral [do](../home.md) controle de acesso para obter mais informações.

Este guia do desenvolvedor fornece informações sobre como formatar suas solicitações para a API [do](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml)Controle de acesso e abrange as seguintes operações:

- [Nomes de Listas de permissões e tipos de recursos](./permissions-and-resource-types.md)
- [Políticas eficazes de Visualização para o usuário atual](./effective-policies.md)

## Introdução

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas bem-sucedidas para a API do Registro do Schema.

### Lendo chamadas de exemplo da API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de solução de problemas do Experience Platform.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para as APIs da Platform, você deve primeiro concluir o tutorial [de](../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API de Experience Platform, como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos no Experience Platform são isolados para caixas de proteção virtuais específicas. Todas as solicitações às APIs do Platform exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção no Platform, consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Próximas etapas

Agora que você reuniu as credenciais necessárias, pode continuar a ler o restante do guia do desenvolvedor. Cada seção fornece informações importantes sobre seus pontos de extremidade e demonstra exemplos de chamadas de API para executar operações CRUD. Cada chamada inclui o formato **geral da** API, uma **solicitação** de amostra mostrando os cabeçalhos necessários e cargas formatadas corretamente e uma **resposta** de amostra para uma chamada bem-sucedida.