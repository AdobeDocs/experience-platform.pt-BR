---
title: Visão geral das regras de vinculação do gráfico de identidade
description: Saiba mais sobre as regras de vinculação do gráfico de identidade no Serviço de identidade.
badge: Beta
exl-id: 317df52a-d3ae-4c21-bcac-802dceed4e53
source-git-commit: 67b08acaecb4adf4d30d6d4aa7b8c24b30dfac2e
workflow-type: tm+mt
source-wordcount: '1114'
ht-degree: 1%

---

# Visão geral das regras de vinculação do gráfico de identidade

>[!AVAILABILITY]
>
>Esse recurso ainda não está disponível; o programa beta para regras de vinculação de gráficos de identidade deve começar em julho nas sandboxes de desenvolvimento. Entre em contato com a equipe de conta do Adobe para obter informações sobre os critérios de participação.

## Índice 

* [Visão geral](./overview.md)
* [Algoritmo de otimização de identidade](./identity-optimization-algorithm.md)
* [Exemplos de cenários](./example-scenarios.md)

Com o Serviço de identidade da Adobe Experience Platform e o Perfil do cliente em tempo real, é fácil supor que seus dados são assimilados perfeitamente e que todos os perfis mesclados representam uma única pessoa por meio de um identificador de pessoa, como uma ID de CRM. No entanto, há possíveis cenários em que determinados dados podem tentar mesclar vários perfis diferentes em um único perfil (&quot;colapso de gráfico&quot;). Para evitar essas mesclagens indesejadas, é possível usar as configurações fornecidas por meio das regras de vinculação do gráfico de identidade e permitir a personalização precisa para seus usuários.

## Exemplos de cenários em que o colapso de gráficos pode ocorrer

* **Dispositivo compartilhado**: Dispositivo compartilhado refere-se aos dispositivos usados por mais de um indivíduo. Exemplos de dispositivos compartilhados incluem tablets, computadores de biblioteca e quiosques.
* **Email e números de telefone incorretos**: emails e números de telefone incorretos se referem a usuários finais que registram informações de contato inválidas, como &quot;test&quot;<span>@test.com&quot; para email e &quot;+1-111-111-1111&quot; para número de telefone.
* **Valores de identidade incorretos ou incorretos**: valores de identidade errados ou inválidos se referem a valores de identidade não exclusivos que podem mesclar IDs de CRM. Por exemplo, embora os IDFAs devam ter 36 caracteres (32 caracteres alfanuméricos e quatro hifens), há cenários em que um IDFA com um valor de identidade de &quot;user_null&quot; pode ser assimilado. Da mesma forma, os números de telefone suportam apenas caracteres numéricos, mas um namespace de telefone com um valor de identidade &quot;não especificado&quot; pode ser assimilado.

Para obter mais informações sobre cenários de caso de uso para regras de vinculação de gráficos de identidade, leia o documento sobre [exemplos de cenários](./example-scenarios.md).

## Regras de vinculação do gráfico de identidade {#identity-graph-linking-rules}

Com as regras de vinculação do gráfico de identidade, você pode:

* Crie um único gráfico de identidade/perfil mesclado para cada usuário configurando namespaces exclusivos, o que impedirá que dois identificadores de pessoa diferentes sejam mesclados em um gráfico de identidade.
* Associar eventos online e autenticados à pessoa, configurando prioridades

### Terminologia {#terminology}

| Terminologia | Descrição |
| --- | --- |
| Namespace exclusivo | Um namespace exclusivo é um namespace de identidade que foi configurado para ser distinto no contexto de um gráfico de identidade. Você pode configurar um namespace para ser exclusivo usando a interface do usuário. Depois que um namespace é definido como exclusivo, um gráfico só pode ter uma identidade que contenha esse namespace. |
| Prioridade de namespace | A prioridade de namespace refere-se à importância relativa dos namespaces em comparação uns com os outros. A prioridade de namespace pode ser configurada por meio da interface do usuário. Você pode classificar namespaces em um determinado gráfico de identidade. Depois de ativada, a prioridade de nomes será usada em vários cenários, como entrada para o algoritmo de otimização de identidade e determinação da identidade principal para fragmentos de evento de experiência. |
| Algoritmo de otimização de identidade | O algoritmo de otimização de identidade garante que as diretrizes criadas pela configuração de um namespace exclusivo e de prioridades de namespace sejam aplicadas em um determinado gráfico de identidade. |

### Namespace exclusivo {#unique-namespace}

Você pode configurar um namespace para ser exclusivo usando o espaço de trabalho da interface do usuário de configurações de identidade. Ao fazer isso, o informa ao algoritmo de otimização de identidade que um determinado gráfico pode ter apenas uma identidade que contenha esse namespace exclusivo. Isso impede a mesclagem de dois identificadores de pessoas diferentes no mesmo gráfico.

Considere o seguinte cenário:

* Scott usa um tablet e abre seu navegador Google Chrome para ir ao Nike<span>.com, onde ele se inscreve e procura por novos sapatos de basquete.
   * Nos bastidores, esse cenário registra as seguintes identidades:
      * Um namespace e valor de ECID para representar o uso do navegador
      * Um namespace e valor de ID do CRM para representar o usuário autenticado (Scott entrou com sua combinação de nome de usuário e senha).
* Seu filho Peter, em seguida, usa o mesmo tablet e também usa Google Chrome para ir ao Nike<span>.com, onde ele se conecta com sua própria conta para procurar por equipamentos de futebol.
   * Nos bastidores, esse cenário registra as seguintes identidades:
      * O mesmo namespace e valor de ECID para representar o navegador.
      * Um novo namespace e valor de ID do CRM para representar o usuário autenticado.

Se a ID do CRM foi configurada como um namespace exclusivo, o algoritmo de otimização de identidade divide as IDs do CRM em dois gráficos de identidade separados, em vez de mesclá-los.

Se você não configurar um namespace exclusivo, poderá ter mesclagens de gráficos indesejadas, como duas identidades com o mesmo namespace de ID do CRM, mas valores de identidade diferentes (cenários como esses geralmente representam duas entidades de pessoa diferentes no mesmo gráfico).

Você deve configurar um namespace exclusivo para informar o algoritmo de otimização de identidade para impor limitações aos dados de identidade que são assimilados em um determinado gráfico de identidade.

### Prioridade de namespace {#namespace-priority}

A prioridade de namespace refere-se à importância relativa dos namespaces em comparação uns com os outros. A prioridade de namespace é configurável por meio da interface do usuário e você pode classificar namespaces em um determinado gráfico de identidade.

Uma maneira pela qual a prioridade do namespace é usada é determinar a identidade principal dos fragmentos de evento de experiência (comportamento do usuário) no Perfil do cliente em tempo real. Se as configurações de prioridade estiverem definidas, a configuração de identidade principal no SDK da Web não será mais usada para determinar quais fragmentos de perfil estão armazenados.

Namespaces exclusivos e prioridades de namespace podem ser configurados no espaço de trabalho da interface do usuário de configurações de identidade. No entanto, os efeitos de suas configurações são diferentes:

| | Serviço de identidade | Perfil do cliente em tempo real |
| --- | --- | --- |
| Namespace exclusivo | No Serviço de identidade, o algoritmo de otimização de identidade se refere a namespaces exclusivos para determinar os dados de identidade que são assimilados em um determinado gráfico de identidade. | Os namespaces exclusivos não afetam o Perfil do cliente em tempo real. |
| Prioridade de namespace | No Identity Service, para gráficos com várias camadas, a prioridade do namespace determinará se os links apropriados foram removidos. | Quando um evento de experiência é assimilado no Perfil, o namespace com a prioridade mais alta se torna a identidade principal do fragmento de perfil. |

* A prioridade de namespace não afeta o comportamento do gráfico quando o limite de 50 identidades por gráfico é atingido.
* **A prioridade do namespace é um valor numérico** atribuído a um namespace indicando sua importância relativa. Esta é uma propriedade de um namespace.
* **A identidade principal é a identidade na qual um fragmento de perfil é armazenado**. Um fragmento de perfil é um registro de dados que armazena informações sobre um determinado usuário: atributos (geralmente assimilados por meio de registros do CRM) ou eventos (geralmente assimilados de eventos de experiência ou dados online).
* A prioridade do namespace determina a identidade principal dos fragmentos de evento de experiência.
   * Para registros de perfil, você pode usar o espaço de trabalho de esquemas na interface do usuário do Experience Platform para definir campos de identidade, incluindo a identidade principal. Leia o guia em [definição de campos de identidade na interface](../../xdm/ui/fields/identity.md) para obter mais informações.

Para obter mais informações, leia o guia em [prioridade de namespace](./namespace-priority.md).

## Próximas etapas

Para obter mais informações sobre regras de vinculação de gráficos de identidade, leia a seguinte documentação:

* [Algoritmo de otimização de identidade](./identity-optimization-algorithm.md).
* [Prioridade de namespace](./namespace-priority.md).
* [Exemplos de cenários para configurar regras de vinculação de gráficos de identidade](./example-scenarios.md).
