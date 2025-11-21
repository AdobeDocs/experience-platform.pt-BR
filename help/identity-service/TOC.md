---
audience: user
user-guide-title: Serviço de identidade da Adobe Experience Platform
breadcrumb-title: Guia do Serviço de identidade da Experience Platform
user-guide-description: Une as identidades dos clientes em todos os dispositivos e sistemas para entregar experiências digitais personalizadas.
feature: Identities
role: Admin,Developer
source-git-commit: 6690854048324567f9a8a1f000bd10f45d7c8340
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 36%

---


# Serviço de identidade da Adobe Experience Platform {#identity}

- [Visão geral do serviço de identidade](home.md)
- [Serviço de identidade e perfil do cliente em tempo real](identity-and-profile.md)
- Recursos {#features}
   - [Namespace de identidade](./features/namespaces.md)
   - [Lógica de vinculação de identidade](./features/identity-linking-logic.md)
   - [Visualizador de gráficos de identidade](./features/identity-graph-viewer.md)
   - [Exclusões no serviço de identidade](./features/deletion.md)
   - Regras de vinculação do gráfico de identidade {#identity-graph-linking-rules}
      - [Visão geral do recurso](./identity-graph-linking-rules/overview.md)
      - [Algoritmo de otimização de identidades](./identity-graph-linking-rules/identity-optimization-algorithm.md)
      - [Guia de implementação para regras de vinculação do gráfico de identidade](./identity-graph-linking-rules/implementation-guide.md)
      - [Guia de configurações](./identity-graph-linking-rules/example-configurations.md)
      - [Solução de problemas das regras de vinculação do gráfico de identidade](./identity-graph-linking-rules/troubleshooting.md)
      - [Prioridade de namespace](./identity-graph-linking-rules/namespace-priority.md)
      - [Interface de simulação de gráfico](./identity-graph-linking-rules/graph-simulation.md)
      - [Interface de configurações de identidade](./identity-graph-linking-rules/identity-settings-ui.md)
   - [Visão geral da ECID](./features/ecid.md)
- [Guia de implementação](implementation.md)
- [Medidas de proteção de dados de identidade](guardrails.md)
- API do serviço de identidade {#api}
   - [Introdução](api/getting-started.md)
   - [Rotular um campo como identidade](api/label-identities.md)
   - [Listar identidades de cluster](api/list-cluster-identites.md)
   - [Listar histórico de cluster de uma identidade](api/list-cluster-history.md)
   - [Listar mapeamentos de identidade](api/list-identity-mappings.md)
   - [Listar namespaces disponíveis](api/list-namespaces.md)
   - [Criar um namespace personalizado](api/create-custom-namespace.md)
   - [Listar a ID nativa de uma identidade](api/list-native-id.md)
   - [Referência da API](https://www.adobe.io/experience-platform-apis/references/identity-service)
- [Definir campos de identidade na interface](label-identities.md)
- [Processamento de solicitação de privacidade](privacy.md)
- [Manual de solução de problemas](troubleshooting-guide.md)
- [Notas de versão da Experience Platform](https://experienceleague.adobe.com/pt-br/docs/experience-platform/release-notes/latest)