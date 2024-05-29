---
keywords: Experience Platform;página inicial;tópicos populares;conjunto de dados;conjunto de dados;tempo de vida;ttl;tempo de vida;pseudônimo;perfis pseudônimos;expiração de dados;expiração;
solution: Experience Platform
title: Expiração de dados do perfil pseudônimo
description: Este documento fornece orientação geral sobre como configurar a expiração de dados para Perfis pseudônimos no Adobe Experience Platform.
exl-id: e8d31718-0b50-44b5-a15b-17668a063a9c
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 0%

---

# Expiração de dados de perfis pseudônimos

No Adobe Experience Platform, você pode configurar as horas de expiração para perfis pseudônimos, permitindo remover automaticamente dados do armazenamento de perfis que não são mais válidos ou úteis para seus casos de uso.

## Perfil pseudônimo {#pseudonymous-profile}

Um perfil é considerado para expiração de dados pseudônimos se atender às seguintes condições:

- Os namespaces de identidade do perfil compilado correspondem ao que o cliente especificou como um namespace de identidade pseudônimo ou desconhecido.
   - Por exemplo, se o namespace de identidade do perfil for `ECID`, `GAID`ou `AAID`. O perfil compilado não tem IDs de nenhum outro namespace de identidade. Neste exemplo, um perfil compilado faz **não** têm uma identidade de email ou CRM.
- Nenhuma atividade ocorreu em um período definido pelo usuário. A atividade é definida por qualquer evento de experiência que esteja sendo assimilado ou por atualizações iniciadas pelo cliente nos atributos do perfil.
   - Por exemplo, um novo evento de exibição de página ou atualização de atributo de página é considerado uma atividade. No entanto, uma atualização de associação de público-alvo iniciada por não usuários é **não** como uma atividade. Atualmente, para calcular a expiração dos dados, o rastreamento em nível de perfil se baseia na hora do evento para Eventos de experiência e na hora da assimilação dos atributos de perfil.

## Acesso {#access}

A expiração de dados do perfil de pseudônimo não pode ser configurada por meio da interface do usuário da plataforma ou de APIs. Em vez disso, entre em contato com o suporte para ativar esse recurso. Ao entrar em contato com o suporte, inclua as seguintes informações:

- Os namespaces de identidade a serem considerados para exclusões de perfil pseudônimo.
   - Por exemplo: `ECID` somente, `AAID` ou uma combinação de `ECID` e `AAID`.
- O tempo de espera antes da exclusão de um perfil com pseudônimo. A recomendação padrão para clientes é 14 dias. No entanto, esse valor pode ser diferente com base no seu caso de uso.

## Perguntas frequentes {#faq}

A seção a seguir lista as perguntas frequentes sobre a expiração dos dados de perfis pseudônimos:

### Como a expiração de dados do Perfil de pseudônimo difere da expiração de dados do Evento de experiência?

A expiração de dados do Perfil de pseudônimo e a expiração de dados do Evento de experiência são recursos complementares.

#### Granularidade

A expiração de dados do perfil de pseudônimo funciona em um **sandbox** nível. Como resultado, a expiração dos dados afetará todos os perfis na sandbox.

A expiração de dados do evento de experiência funciona em um **conjunto de dados** nível. Como resultado, cada conjunto de dados pode ter uma configuração de expiração de dados diferente.

#### Tipos de identidade

Expiração de dados do perfil pseudônimo **somente** O considera perfis que têm gráficos de identidade que contêm namespaces de identidade selecionados pelo cliente, como `ECID`, `AAID`ou outros tipos de cookies. Se o perfil contiver **qualquer** namespace de identidade adicional que foi **não** na lista selecionada pelo cliente, o perfil **não** ser excluídos.

A expiração dos dados do evento de experiência remove os eventos **somente** com base no carimbo de data e hora do registro do evento. Os namespaces de identidade incluídos são **ignorado** para fins de expiração.

#### Itens Removidos

A expiração de dados do perfil de pseudônimo remove **ambos** registros de eventos e perfis. Como resultado, os dados da classe de perfil também serão removidos.

Expiração de dados do evento de experiência **somente** remove eventos e faz **não** remover dados da classe de perfil. Os dados da classe de perfil só são removidos quando todos os dados são removidos **all** conjuntos de dados e há **não** registros de classe de perfil restantes para o perfil.

### Como a expiração de dados do Perfil de pseudônimo pode ser usada juntamente com a expiração de dados do Evento de experiência?

A expiração de dados do perfil de pseudônimo e a expiração de dados do evento de experiência podem ser usadas para se complementar.

Você deve **sempre** Configure a expiração de dados do Evento de experiência em seus conjuntos de dados com base nas necessidades de retenção de dados sobre clientes conhecidos. Depois que a expiração de dados do evento de experiência for configurada, você poderá usar a expiração de dados do perfil de pseudônimo para remover automaticamente os perfis de pseudônimo. Normalmente, o período de expiração dos dados para perfis pseudônimos é menor que o período de expiração dos dados para eventos de experiência.

Para um caso de uso típico, você pode definir a expiração de dados do evento de experiência com base nos valores dos dados do usuário conhecidos e definir a expiração de dados do perfil pseudônimo para uma duração muito mais curta para limitar o impacto dos perfis pseudônimos na conformidade de licença da plataforma.

### Quais usuários devem usar a expiração de dados de perfis pseudônimos?

- Se você estiver usando o SDK da Web para enviar dados diretamente para a Platform.
- Se você tiver um site que atende clientes não autenticados em massa.
- Se você tiver contagens excessivas de perfis em seus conjuntos de dados e tiver confirmado que essa contagem excessiva de perfis se deve ao namespace de identidade anônimo baseado em cookies.
   - Para determinar isso, você deve usar o relatório de sobreposição de namespace de identidade. Mais informações sobre este relatório podem ser encontradas no [seção relatório de sobreposição de identidade](./api/preview-sample-status.md#identity-overlap-report) do guia da API de status da amostra de visualização.

### Quais são alguns avisos que você deve estar ciente antes de usar a expiração de dados de perfis pseudônimos?

- A expiração de dados de perfil pseudônimo é executada em um **sandbox** nível. Você pode optar por ter configurações diferentes para sandboxes de produção e desenvolvimento.
- Depois de ativar esse recurso, a exclusão de perfis é **permanente**. Há **não** forma de reverter ou restaurar os perfis excluídos.
- Isso é **não** um trabalho de limpeza único. A expiração de dados de perfil pseudônimo será executada uma vez por dia e excluirá perfis que correspondam à entrada do cliente.
- **Todos** Os perfis definidos como perfis pseudônimos serão afetados pela expiração dos dados do perfil pseudônimo. Ele faz **não** importante se o perfil for somente Evento de experiência ou se contiver apenas atributos de perfil.
- Essa limpeza **somente** ocorrer no Perfil. O Serviço de identidade pode continuar mostrando as identidades excluídas no gráfico após a limpeza nos casos em que o perfil tem duas ou mais identidades com pseudônimos associadas (como `AAID` e `ECID`). Esta discrepância será abordada num futuro próximo.
- A expiração de dados de perfil pseudônimo faz **não** executada imediatamente e pode levar até três dias para ser processada.

### Como a expiração de dados de perfis pseudônimos interage com as medidas de proteção para dados do Serviço de identidade?

- O serviço de identidade [sistema de exclusão &quot;primeiro a entrar, primeiro a sair&quot;](../identity-service/guardrails.md) O pode excluir ECIDs do gráfico de identidade, que são armazenados no Serviço de identidade.
- Se esse comportamento de exclusão resultar no armazenamento de um perfil somente ECID no Perfil do cliente em tempo real (armazenamento de perfil), a expiração dos dados do perfil pseudônimo excluirá esse perfil do armazenamento de perfil.
