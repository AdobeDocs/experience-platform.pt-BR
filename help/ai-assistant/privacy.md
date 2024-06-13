---
title: Privacidade, segurança e governança no Assistente de IA
description: Saiba mais sobre as práticas de privacidade, segurança e governança do Assistente de IA.
exl-id: 371e065d-c2dd-4233-b78e-a42757fce853
source-git-commit: e14bf4191319d646c6c4bfd55656fc6de141e9ca
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Privacidade, segurança e governança no Assistente de IA

O Assistente de IA no Adobe Experience Platform é criado com privacidade, segurança e governança na vanguarda.

Leia este documento para saber mais sobre os recursos focados na confiança do cliente que você pode esperar do Assistente de IA:

* Nenhum dado pessoal está sendo usado pelo Assistente de IA hoje, mesmo para fins de treinamento.
* O Assistente de IA não tem conhecimento dos dados do consumidor.
* Todos os existentes [controle de acesso](../access-control/home.md) As políticas do serão respeitadas pelo Assistente de IA.
   * Quaisquer novas políticas de controle de acesso baseadas em atributos serão refletidas no Assistente de IA após um máximo de 24 horas*
* Você deve receber permissão explícita para interagir com o Assistente de IA.
   * É possível definir permissões de forma diferente para o Experience Platform e o Journey Optimizer usando o [Interface de permissões](../access-control/abac/ui/permissions.md) e você pode usar o [Admin Console](../access-control/ui/browse.md) para atribuir permissões para Customer Journey Analytics.
   * As permissões são granulares e o administrador da sandbox pode configurar quais dos seus usuários podem fazer diferentes categorias de perguntas (perguntas baseadas em conhecimento do produto com o Assistente de IA ou perguntas sobre insights operacionais).
* O AI Assistant é um recurso pronto para HIPAA quando usado em combinação com o Adobe Experience Platform Healthcare Shield.
* Você pode exibir um log de suas interações anteriores com o AI Assistant com uma política de retenção de 30 dias.
* O Assistente de IA é baseado em dados específicos da sandbox e na documentação de Adobe pública ao responder aos prompts do usuário. Os dados não são compartilhados em sandboxes.
* Os prompts fornecidos ao Assistente de IA não são compartilhados com outros clientes.

**Isso significa que, se algum novo rótulo for adicionado aos campos e objetos ou se qualquer nova política for criada, o AI Assistant levará até 24 horas para respeitá-los. Durante essas 24 horas, os usuários com acesso recém-restrito ainda podem acessar esses campos e objetos.*
