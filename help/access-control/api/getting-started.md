---
keywords: Experience Platform;home;popular topics;controle de acesso;api;introdução
solution: Experience Platform
title: Guia da API do controle de acesso
topic: developer guide
description: O controle de acesso no Adobe Experience Platform permite gerenciar funções e permissões para vários recursos da plataforma usando o Adobe Admin Console. As seções a seguir fornecem informações adicionais que os desenvolvedores precisarão saber para fazer chamadas bem-sucedidas para a API do Registro do Schema.
translation-type: tm+mt
source-git-commit: e649ab3da077cdd8e98562199b8bdece6108a572
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 3%

---


# [!DNL Access Control] Guia de API

[!DNL Access control] for  [!DNL Experience Platform] administrado através do  [Adobe Admin Console](https://adminconsole.adobe.com). Essa funcionalidade aproveita perfis de produtos no Admin Console, que vinculam usuários com permissões e caixas de proteção. Consulte a [visão geral do controle de acesso](../home.md) para obter mais informações.

Este guia do desenvolvedor fornece informações sobre como formatar suas solicitações para [[!DNL Access Control API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) e abrange as seguintes operações:

- [Nomes de listas de permissões e tipos de recursos](./permissions-and-resource-types.md)
- [Políticas eficazes de visualização para o usuário atual](./effective-policies.md)

## Introdução

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para a API [!DNL Schema Registry].

### Lendo chamadas de exemplo da API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção em [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a [documentação de visão geral da caixa de proteção](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Próximas etapas

Agora que você reuniu as credenciais necessárias, pode continuar a ler o restante do guia do desenvolvedor. Cada seção fornece informações importantes sobre seus pontos de extremidade e demonstra exemplos de chamadas de API para executar operações CRUD. Cada chamada inclui o formato de API geral, uma solicitação de amostra mostrando os cabeçalhos necessários e as cargas formatadas corretamente e uma resposta de amostra para uma chamada bem-sucedida.
