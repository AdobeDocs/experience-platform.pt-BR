---
title: Guia da API de autorização do Data Distiller
description: Saiba como usar a API de autorização do Data Distiller para aplicar restrições de IP baseadas em rede para conexões seguras por meio do SQL. Use essa API para aprimorar o controle de acesso aos dados do Adobe Experience Platform.
role: Developer
exl-id: bcc5ea0e-cb6d-4c7b-bf9f-a0336f76c4c8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 2%

---

# Guia da API de autorização do Data Distiller

>[!AVAILABILITY]
>
>Essa funcionalidade está disponível para clientes que compraram o complemento Data Distiller. Para obter mais informações, entre em contato com o(a) representante da Adobe.

Use a API de autorização do Data Distiller para aplicar restrições baseadas em IP. A aplicação dessas medidas garante que somente redes aprovadas e máquinas clientes possam acessar dados via SQL no Adobe Experience Platform. Esses controles ajudam você a atender padrões rigorosos de segurança e, ao mesmo tempo, fornecer alertas e monitoramento de acesso em tempo real.

Com essa API, você pode configurar, aplicar e monitorar restrições de IP para acessar dados por meio da interface SQL. Este documento fornece uma visão geral de alto nível dos recursos principais da API, das funções de endpoint e dos recursos futuros.

## Recursos principais

Os seguintes recursos permitem definir restrições de acesso baseadas em IP, monitorar tentativas de acesso e personalizar as configurações de segurança da rede para o Serviço de consulta:

- **Definir controles de acesso a dados baseados na rede**: especifique intervalos IP permitidos para o acesso ao Serviço de Consulta. Essa restrição se aplica especificamente a conexões de banco de dados SQL, incluindo aquelas feitas por meio de ferramentas Business Intelligence (BI), clientes de banco de dados ou interfaces de programação como JDBC.
- **Habilite monitoramento e alertas abrangentes**: todas as tentativas de acesso, incluindo conexões negadas, são registradas e enviadas aos [Logs de Auditoria do Adobe Experience Platform](../../landing/governance-privacy-security/audit-logs/overview.md) para rastreamento em tempo real. Use esse recurso para monitorar os padrões de acesso e detectar possíveis violações de segurança.
- **Configurar restrições flexíveis de IP**: especifique IPs permitidos nos formatos de bloco individual de IP e CIDR. Essas configurações se aplicam por sandbox, permitindo adaptar as restrições de rede às suas necessidades específicas de segurança.

## Recursos de auditoria e monitoramento

Para oferecer suporte a práticas seguras de acesso a dados, o Serviço de consulta registra todos os IPs de cliente que acessam ou tentam acessar o Experience Platform. Os eventos de auditoria, incluindo conexões negadas, são enviados aos Logs de auditoria do Experience Platform. Isso permite:

- **Monitoramento em tempo real**: controle os padrões de acesso baseados em IP para garantir a conformidade.
- **Alerta sobre Acesso Não Autorizado**: identifique e responda a tentativas de acesso de IPs não autorizados.

Consulte a [Visão geral dos logs de auditoria](../../landing/governance-privacy-security/audit-logs/overview.md) para obter mais detalhes.

## Próximas etapas

Comece a usar a API de Autorização do Data Distiller revisando o [Guia de Introdução](./getting-started.md) para obter as etapas de configuração essenciais, incluindo os cabeçalhos e as convenções de chamada da API necessários. Em seguida, explore os guias específicos do ponto de extremidade em [Acesso IP](./ip-access.md) e [Validação de IP](./validate.md) para configurar e gerenciar o acesso seguro aos dados.

Consulte a [documentação de referência da OpenAPI de Autorização do Data Distiller](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/) para exibir um formato padronizado e legível por máquina para facilitar a integração, o teste e a exploração.

Para obter informações sobre os vários parâmetros de resposta para cada conjunto de dados retornado, consulte a [documentação do desenvolvedor da API de Conjuntos de Dados](https://developer.adobe.com/experience-platform-apis/references/catalog/#tag/Datasets/operation/listDatasets).
