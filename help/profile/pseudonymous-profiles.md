---
keywords: Experience Platform;página inicial;tópicos populares;conjunto de dados;conjunto de dados;tempo de vida;ttl;tempo de vida;pseudônimo;perfis pseudônimos;expiração de dados;expiração;
solution: Experience Platform
title: Expiração de dados do perfil pseudônimo
description: Este documento fornece orientação geral sobre como configurar a expiração de dados para Perfis pseudônimos no Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: 3f776255ca858a86f501fd587c44fe176c45e103
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 0%

---


# Expiração de dados de perfis pseudônimos [!BADGE Versão limitada]

No Adobe Experience Platform, um perfil é considerado para expiração de dados pseudônimos se atender às seguintes condições:

- Os tipos de identidade do perfil compilado correspondem ao que o cliente especificou como um tipo de identidade pseudônimo ou desconhecido.
   - Por exemplo, se o tipo de identidade do perfil for `ECID`, `GAID`ou `AAID`. O perfil compilado não tem IDs de nenhum outro tipo de identidade. Neste exemplo, um perfil compilado faz **não** têm uma identidade de email ou CRM.
- Nenhuma atividade ocorreu em um período definido pelo usuário. A atividade é definida por qualquer evento de experiência que esteja sendo assimilado ou por atualizações iniciadas pelo cliente nos atributos do perfil.
   - Por exemplo, um novo evento de exibição de página ou atualização de atributo de página é considerado uma atividade. No entanto, uma atualização de associação de segmento iniciada por não usuários é **não** como uma atividade. Atualmente, para calcular a expiração dos dados, o rastreamento em um nível de perfil se baseia no momento da assimilação.

## Access {#access}

A expiração de dados do perfil de pseudônimo não pode ser configurada por meio da interface do usuário da plataforma ou de APIs. Em vez disso, entre em contato com o suporte para ativar esse recurso. Ao entrar em contato com o suporte, inclua as seguintes informações:

- Os tipos de identidade a serem considerados para exclusões de perfil pseudônimo.
   - Por exemplo: `ECID` somente, `AAID` ou uma combinação de `ECID` e `AAID`.
- O tempo de espera antes da exclusão de um perfil com pseudônimo. A recomendação padrão para clientes é de 30 dias. No entanto, esse valor pode ser diferente com base no seu caso de uso.
- A contagem de perfis atual em comparação à contagem de perfis de licenças.

## Perguntas frequentes {#faq}

A seção a seguir lista as perguntas frequentes sobre a expiração dos dados de perfis pseudônimos:

### Quais usuários devem usar a expiração de dados de perfis pseudônimos?

- Se estiver usando um conector que envia dados diretamente da origem para a Platform.
- Se você tiver um site que atende clientes não autenticados em massa.
- Se você tiver contagens excessivas de perfis em seus conjuntos de dados e tiver confirmado que essa contagem excessiva de perfis se deve ao tipo de identidade anônima baseada em cookies.
   - Para determinar isso, você deve usar o relatório de sobreposição do tipo de identidade. Mais informações sobre este relatório podem ser encontradas em LINK

### Quais são alguns avisos que você deve estar ciente antes de usar a expiração de dados de perfis pseudônimos?

- A expiração de dados de perfis pseudônimos será executada no **produção** sandbox.
- Depois de ativar esse recurso, a exclusão de perfis é **permanente**. Há **não** forma de reverter ou restaurar os perfis excluídos.
- Isso é **não** um trabalho de limpeza único. A expiração de dados de perfil pseudônimo será executada continuamente uma vez por dia e excluirá os perfis que correspondem à entrada do cliente.
- **Todos** Os perfis definidos como perfis pseudônimos serão afetados pela expiração dos dados do perfil pseudônimo. Ele faz **não** importante se o perfil for somente Evento de experiência ou se contiver apenas atributos de perfil.
- Essa limpeza **somente** ocorrer no Perfil. O Serviço de identidade pode continuar mostrando as identidades excluídas no gráfico após a limpeza nos casos em que o perfil tem duas ou mais identidades com pseudônimos associadas (como `AAID` e `ECID`). Esta discrepância será abordada num futuro próximo.

### Como a expiração de dados do Perfil de pseudônimo difere da expiração de dados existente do Evento de experiência?

A expiração de dados do Perfil de pseudônimo e a expiração de dados do Evento de experiência são recursos complementares.

#### Granularidade

A expiração de dados do evento de experiência funciona em um **conjunto de dados** nível. Como resultado, cada conjunto de dados pode ter uma configuração de expiração de dados diferente.

A expiração de dados do perfil de pseudônimo funciona em um **sandbox** nível. Como resultado, a expiração dos dados afetará todos os perfis na sandbox.

#### Tipos de identidade

A expiração dos dados do evento de experiência remove os eventos **somente** com base no carimbo de data e hora do registro do evento. Os tipos de identidade incluídos são **ignorado** para fins de expiração.

Expiração de dados do perfil pseudônimo **somente** O considera perfis que têm gráficos de identidade que contêm tipos de identidade selecionados pelo cliente, como `ECID`, `AAID`ou outros tipos de cookies. Se o perfil contiver **qualquer** tipo de identidade adicional que foi **não** na lista selecionada pelo cliente, o perfil **não** ser excluídos.

#### Itens Removidos

Expiração de dados do evento de experiência **somente** remove eventos e faz **não** remover dados da classe de perfil. Os dados da classe de perfil só são removidos quando todos os dados são removidos **all** conjuntos de dados e há **não** registros de classe de perfil restantes para o perfil.

A expiração de dados do perfil de pseudônimo remove **ambos** registros de eventos e perfis. Como resultado, os dados da classe de perfil também serão removidos.

### Como a expiração de dados do Perfil de pseudônimo pode ser usada juntamente com a expiração de dados do Evento de experiência?

A expiração de dados do perfil de pseudônimo e a expiração de dados do evento de experiência podem ser usadas para se complementar.

Você deve **sempre** Configure a expiração de dados do Evento de experiência em seus conjuntos de dados com base nas necessidades de retenção de dados sobre clientes conhecidos. Depois que a expiração de dados do evento de experiência for configurada, você poderá usar a expiração de dados do perfil de pseudônimo para remover automaticamente os perfis de pseudônimo. Normalmente, o período de expiração dos dados para perfis pseudônimos é menor que o período de expiração dos dados para eventos de experiência.

Para um caso de uso típico, você pode definir a expiração de dados do evento de experiência com base nos valores dos dados do usuário conhecidos e definir a expiração de dados do perfil pseudônimo para uma duração muito mais curta para limitar o impacto dos perfis pseudônimos na conformidade de licença da plataforma.
