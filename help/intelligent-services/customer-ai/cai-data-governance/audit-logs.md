---
keywords: insights, atendimento ao cliente, insights do atendimento ao cliente, serviço de consulta da CAI, consultas do atendimento ao cliente, pontuações do atendimento ao cliente
title: Visão geral dos logs de auditoria no Customer AI
description: Saiba como visualizar e gerenciar logs de auditoria no Customer AI.
source-git-commit: 6f386d859b8553050ead266fad0e473c7cf7095e
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 36%

---

# Logs de auditoria

Para aumentar a transparência e a visibilidade das atividades realizadas no sistema, a atividade do usuário no fluxo de trabalho do Customer AI agora é capturada nos logs de auditoria para entender quaisquer alterações orientadas pelo usuário nos modelos do Customer AI. Esses registros formam uma trilha de auditoria que pode ajudar na solução de problemas e ajudar sua empresa a cumprir com eficácia as políticas corporativas de gerenciamento de dados e os requisitos normativos.  Se você estiver sujeito à HIPAA (Health Insurance Portability and Accountability Act, Lei de Responsabilidade e Portabilidade do Seguro de Saúde) e estiver criando, recebendo, mantendo ou transmitindo dados pessoais confidenciais permitidos por meio do Attribution AI ou da AI do cliente, você será responsável pela execução de um BAA com Adobe e licenciamento do Healthcare Shield.

Basicamente, um log de auditoria informa quem executou qual ação e quando. Cada ação registrada em um log contém metadados que indicam o tipo de ação, a data e a hora, a ID do email do usuário que executou a ação e atributos adicionais relevantes ao tipo de ação. Ele acompanha as ações de criação, atualização e exclusão executadas pelos usuários no Customer AI.

[Os logs de auditoria selecionados na área de trabalho do Customer AI](../../customer-ai/images/data-governance/audit-logs-cai.png)

## Acesso a logs de auditoria

Quando o recurso é ativado para sua organização, os logs de auditoria são coletados automaticamente conforme a atividade ocorre. Não é necessário ativar manualmente a coleção de log.

Para visualizar e exportar logs de auditoria, você deve ter recebido a permissão de controle Acesso aos logs de auditoria no console da Adobe. Para saber como gerenciar permissões individuais para os recursos do Customer AI, consulte [documentação de controle de acesso](../cai-data-governance/access-controls.md).