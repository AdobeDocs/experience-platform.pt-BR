---
keywords: Experience Platform, home, tópicos populares, conjunto de dados, conjunto de dados, tempo de vida, ttl, tempo de vida, pseudônimo, perfis pseudônimos, expiração de dados, expiração;
solution: Experience Platform
title: Expiração de dados do perfil pseudônimo
description: Este documento fornece orientação geral sobre como configurar a expiração de dados para perfis pseudônimos no Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: 6ba219162f6fde37d8bd258c43ed1bdbbbcdf569
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 0%

---


# Expiração de dados de perfis pseudônimos [!BADGE Versão limitada]

No Adobe Experience Platform, um perfil é considerado para a expiração de dados pseudônimos se atender às seguintes condições:

- Os namespaces de identidade do perfil corrigido correspondem ao que o cliente especificou como um namespace de identidade pseudônimo ou desconhecido.
   - Por exemplo, se o namespace de identidade do perfil for `ECID`, `GAID`ou `AAID`. O perfil corrigido não tem IDs de nenhum outro namespace de identidade. Neste exemplo, um perfil compilado faz **not** Ter uma identidade de email ou CRM.
- Nenhuma atividade ocorreu em um período definido pelo usuário. A atividade é definida por qualquer evento de experiência assimilado ou por atualizações iniciadas pelo cliente nos atributos do perfil.
   - Por exemplo, um novo evento de exibição de página ou uma atualização de atributo de página é considerado uma atividade do . No entanto, uma atualização de associação de segmento não iniciada pelo usuário é **not** considerada uma atividade. Atualmente, para calcular a expiração dos dados, o rastreamento em um nível de perfil é baseado no tempo de ingestão.

## Access {#access}

A expiração de dados de Perfil pseudônimo não pode ser configurada por meio da interface do usuário da plataforma ou das APIs. Em vez disso, você deve entrar em contato com o suporte para habilitar esse recurso. Ao entrar em contato com o suporte, inclua as seguintes informações:

- Os namespaces de identidade a serem considerados para exclusão de perfil pseudônimo.
   - Por exemplo: `ECID` somente, `AAID` somente ou uma combinação de `ECID` e `AAID`.
- O tempo de espera antes de excluir um perfil pseudônimo. A recomendação padrão para clientes é de 14 dias. No entanto, esse valor pode ser diferente com base no seu caso de uso.

## Perguntas frequentes {#faq}

A seção a seguir lista perguntas frequentes sobre a expiração de dados de perfis pseudônimos:

### Quais usuários devem usar a expiração de dados de perfis pseudônimos?

- Se você estiver usando o SDK da Web para enviar dados diretamente para a Platform.
- Se você tiver um site que forneça clientes não autenticados em massa.
- Se você tiver contagens de perfil excessivas em seus conjuntos de dados e tiver confirmado que essa contagem de perfil excessiva é devido ao namespace de identidade baseado em cookie anônimo.
   - Para determinar isso, você deve usar o relatório de sobreposição de namespace de identidade. Mais informações sobre este relatório podem ser encontradas no [seção de relatório de sobreposição de identidades](./api/preview-sample-status.md#identity-overlap-report) do guia da API de status de amostra de visualização.

### Quais são alguns avisos que você deve ter em mente antes de usar a expiração dos dados de perfis pseudônimos?

- A expiração de dados de perfil pseudônimo será executada no **produção** sandbox.
- Após ativar esse recurso, a exclusão de perfis é **permanente**. Existe **não** como reverter ou restaurar os perfis excluídos.
- Isso é **not** um trabalho de limpeza único. A expiração de dados de perfil pseudônimo será executada continuamente uma vez por dia e excluirá perfis que correspondam à entrada do cliente.
- **Todos** os perfis definidos como perfis pseudônimos serão afetados pela expiração dos dados do perfil pseudônimo. Ele faz **not** não importa se o perfil é apenas o Evento de experiência ou se ele contém apenas atributos de perfil.
- Esta limpeza fará **only** ocorrem em Perfil. O Serviço de identidade pode continuar a mostrar as identidades excluídas no gráfico após a limpeza nos casos em que o perfil tem duas ou mais identidades pseudônimas associadas (como `AAID` e `ECID`). Essa discrepância será solucionada em breve.

### Como a expiração dos dados do Perfil pseudônimo difere da expiração dos dados do Evento de experiência atual?

A expiração de dados de perfil pseudônimo e a expiração de dados de evento de experiência são recursos complementares.

#### Granularidade

A expiração de dados do Evento de experiência funciona em um **conjunto de dados** nível. Como resultado, cada conjunto de dados pode ter uma configuração de expiração de dados diferente.

A expiração de dados do perfil pseudônimo funciona em um **sandbox** nível. Como resultado, a expiração dos dados afetará todos os perfis na sandbox.

#### Tipos de identidade

A expiração de dados do Evento de experiência remove eventos **only** com base no carimbo de data e hora do registro de eventos. Os namespaces de identidade incluídos são **ignored** para fins de expiração.

Expiração de dados do perfil pseudônimo **only** O considera perfis com gráficos de identidade que contêm namespaces de identidade que foram selecionados pelo cliente, como `ECID`, `AAID`ou outros tipos de cookies. Se o perfil contiver **any** namespace de identidade adicional que era **not** na lista selecionada do cliente, o perfil **not** ser eliminado.

#### Itens removidos

Expiração de dados do evento de experiência **only** remove eventos e faz **not** remover dados de classe de perfil. Os dados da classe de perfil só são removidos quando todos os dados são removidos **all** conjuntos de dados e há **não** registros de classe de perfil restantes para o perfil.

A expiração de dados de perfil pseudônimo remove **both** registros de evento e perfil. Como resultado, os dados da classe de perfil também serão removidos.

### Como a expiração de dados do Perfil Pseudônimo pode ser usada juntamente com a expiração de dados do Evento de Experiência?

A expiração de dados do Perfil pseudônimo e a expiração de dados do Evento de Experiência podem ser usadas para complementar um ao outro.

Você deveria **always** configure a expiração dos dados do Evento de experiência em seus conjuntos de dados, com base nas suas necessidades de retenção de dados sobre seus clientes conhecidos. Depois que os dados do Evento de experiência expirarem, você poderá usar a expiração de dados do Perfil pseudônimo para remover automaticamente os Perfis pseudônimos. Normalmente, o período de expiração dos dados para Perfis pseudônimos é menor que o período de expiração dos dados para Eventos de experiência.

Para um caso de uso típico, você pode definir sua expiração de dados do Evento de experiência com base nos valores de seus dados de usuário conhecidos e pode definir sua expiração de dados do Perfil pseudônimo em um período muito menor para limitar o impacto dos perfis pseudônimos na conformidade com a licença da plataforma.
