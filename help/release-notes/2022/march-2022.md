---
title: Notas de versão da Adobe Experience Platform
description: As notas de versão mais recentes do Adobe Experience Platform.
source-git-commit: 7145867795bcd8e1093c09df3fefdee518f9578a
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 9%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 30 de março de 2022**

Novos recursos no Adobe Experience Platform:

- [[!DNL Audit Logs]](#audit-logs)

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Alertas](#alerts)
- [Fontes](#sources)

## [!DNL Audit Logs] {#audit-logs}

O Experience Platform permite auditar a atividade do usuário para vários serviços e recursos. Os logs de auditoria fornecem informações sobre quem fez o quê e quando.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Logs de auditoria para conjunto de dados, esquema, classe, grupo de campos, tipo de dados, sandbox, destino, segmento, política de mesclagem, atributo calculado, perfil do produto e conta (Adobe) | Esses são os recursos que são registrados por logs de auditoria. Se o recurso estiver ativado, os logs de auditoria serão coletados automaticamente quando a atividade ocorrer. Não é necessário ativar manualmente a coleta de log. |
| Exportar logs de auditoria | Os logs de auditoria podem ser baixados como um `CSV` ou `JSON` arquivo. Os arquivos gerados são salvos diretamente no computador. |

Para obter mais informações sobre logs de auditoria na Platform, consulte [visão geral dos logs de auditoria](../../landing/governance-privacy-security/audit-logs/overview.md).

## Alertas {#alerts}

O Experience Platform permite assinar alertas baseados em eventos para várias atividades da plataforma. É possível assinar diferentes regras de alerta por meio do [!UICONTROL Alertas] na interface do usuário da plataforma e pode optar por receber mensagens de alerta na própria interface do usuário ou por meio de notificações por email.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Novas regras de alerta | Duas novas regras de alerta estão disponíveis para fontes relacionadas à assimilação de dados. Consulte a visão geral em [regras de alerta](../../observability/alerts/rules.md) para obter a lista atualizada de tipos de alertas. |

Para obter mais informações sobre alertas na Platform, consulte [visão geral dos alertas](../../observability/alerts/overview.md).

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Novas fontes agora disponíveis para uso B2B | Agora você pode usar todas as fontes disponíveis na Plataforma para casos de uso B2B. Consulte a [catálogo de origens](../../sources/home.md) para obter uma lista completa das fontes disponíveis. |
| Disponibilidade geral de novos [!DNL Oracle Eloqua] source | Agora você pode usar o [!DNL Oracle Eloqua] fonte para assimilar dados com facilidade de sua [!DNL Oracle Eloqua] instância (conta, campanha, contatos) da Platform. Consulte a documentação em [criar um [!DNL Oracle Eloqua] conexão de origem](../../sources/connectors/oracle-eloqua.md) para obter mais informações. |
| Aprimoramentos de API para [!DNL Data Landing Zone] | O [!DNL Data Landing Zone] A origem agora oferece suporte à detecção automática de propriedades de arquivo ao usar o [!DNL Flow Service] API. Consulte a documentação em [criar um [!DNL Data Landing Zone] conexão de origem](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) para obter mais informações. |

Para saber mais sobre fontes, consulte o [visão geral das fontes](../../sources/home.md).
