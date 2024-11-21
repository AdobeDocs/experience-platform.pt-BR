---
keywords: Experience Platform; Serviço de consulta; Controle de acesso IP; autorização; API; introdução
title: Guia da API de autorização do Data Distiller
description: Saiba como começar a usar restrições de autorização e intervalo de IP para obter acesso seguro a dados no Serviço de consulta da Adobe Experience Platform.
role: Developer
exl-id: d93ce774-c8b2-4f15-a4d9-117d9aa5d9e7
source-git-commit: ac29d10d3774a736d1e54255508ba244ff72f278
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 5%

---

# Introdução à API de autorização do Data Distiller

>[!AVAILABILITY]
>
>Essa funcionalidade está disponível para clientes que compraram o complemento Data Distiller. Para obter mais informações, entre em contato com o(a) representante da Adobe.

A API de autorização do Data Distiller fornece às organizações controle mais rígido sobre o acesso aos dados por meio da interface SQL no Adobe Experience Platform. Você pode usar essa API para definir restrições de IP, limitar o acesso aos dados a redes especificadas e aprimorar o monitoramento de segurança.

Este guia descreve como configurar as credenciais de autorização e as permissões necessárias para fazer chamadas à API de autorização do Data Distiller.

## Introdução {#getting-started}

As seções a seguir fornecem informações sobre como preparar os valores de autorização necessários e fazer suas primeiras solicitações para a API de autorização do Data Distiller.

### Permissões necessárias {#required-permissions}

Para habilitar restrições de acesso seguro a dados no Serviço de Consulta, você precisa da permissão **[!UICONTROL Gerenciar Lista de permissões]**. Essa permissão permite que as organizações definam intervalos IP específicos (no formato IPv4 ou IPv6) autorizados a acessar dados na Platform por meio da interface SQL. O acesso é gerenciado no nível da sandbox, onde os usuários podem configurar uma lista de endereços IP aprovados ou blocos CIDR que restringem o acesso somente a redes permitidas.

>[!NOTE]
>
>Os administradores do sistema podem configurar permissões de usuário no Adobe [Admin Console](https://adminconsole.adobe.com/). Para obter mais informações, consulte o [Manual do usuário do Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html).

As seguintes funcionalidades estão disponíveis com a permissão **[!UICONTROL Gerenciar Lista de permissões]**:

- **Definir intervalos IP permitidos**: somente endereços IP ou blocos CIDR desses intervalos definidos podem acessar dados na Plataforma usando SQL pelo Serviço de Consulta.
- **Impor verificações de intervalo de IP**: as conexões de IPs fora dos intervalos permitidos são negadas.
- **Recursos de auditoria e alerta**: todas as tentativas de acesso, incluindo conexões negadas, são registradas como eventos de auditoria. Esses eventos estão disponíveis nos [Logs de auditoria do Adobe Experience Platform](../../landing/governance-privacy-security/audit-logs/overview.md), permitindo o monitoramento de possíveis violações de segurança.

### Coletar valores para cabeçalhos necessários {#gather-values-for-required-headers}

Para fazer chamadas para a API de autorização do Data Distiller, você deve concluir o [tutorial de autenticação da API da plataforma](../../landing/api-authentication.md), que fornece valores para os cabeçalhos necessários nas chamadas de API. Inclua os seguintes cabeçalhos em cada solicitação:

- **Autorização**: `Bearer {ACCESS_TOKEN}`
- **x-api-key**: `{API_KEY}`
- **x-gw-ims-org-id**: `{ORG_ID}`
- **x-sandbox-name**: `{SANDBOX_NAME}`

>[!NOTE]
>
> Para obter mais informações sobre sandboxes, consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) também exigem este cabeçalho:

- **Tipo de Conteúdo**: `application/json`

### Próximas etapas

Com as permissões necessárias e os valores de cabeçalho coletados, você está pronto para começar a configurar restrições de IP para o Serviço de consulta. Prossiga para a documentação do endpoint para obter exemplos detalhados de operações CRUD, que incluem:

- Formato da API e pares de amostra de solicitação/resposta.
- Cabeçalhos, cargas e códigos de resposta para cada operação.

Cada exemplo de chamada de API demonstra como formatar solicitações e interpretar respostas, ajudando a impor acesso seguro aos seus dados no Serviço de consulta.

Para obter instruções específicas sobre como configurar e validar restrições de IP, consulte a [documentação do ponto de extremidade de Acesso a IP](./ip-access.md) e a [documentação do ponto de extremidade de Validação de IP](./validate.md).
