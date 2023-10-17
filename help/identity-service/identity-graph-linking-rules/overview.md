---
title: Visão geral das regras de vinculação do gráfico de identidade
description: Saiba mais sobre as regras de vinculação do gráfico de identidade no Serviço de identidade.
hide: true
hidefromtoc: true
badge: Alfa
source-git-commit: a6e4511c41408b78a70a22eb8038bb7a37c41ed5
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 0%

---

# Visão geral das regras de vinculação do gráfico de identidade

>[!IMPORTANT]
>
>As regras de vinculação do gráfico de identidade estão atualmente em Alpha. O recurso e a documentação estão sujeitos a alterações.

## Índice 

* [Visão geral](./overview.md)
* [Exemplos de cenários](./example-scenarios.md)
* [Serviço de identidade e perfil do cliente em tempo real](identity-and-profile.md)
* [Lógica de vinculação de identidade](./identity-linking-logic.md)

Com o Serviço de identidade da Adobe Experience Platform e o Perfil do cliente em tempo real, é fácil supor que seus dados são assimilados perfeitamente e que todos os perfis mesclados representam uma única pessoa por meio de um identificador de pessoa, como uma ID de CRM. No entanto, há possíveis cenários em que determinados dados podem tentar mesclar vários perfis diferentes em um único perfil (&quot;colapso de perfil&quot;). Para evitar essas mesclagens indesejadas, é possível usar as configurações fornecidas por meio das regras de vinculação do gráfico de identidade e permitir a personalização precisa para seus usuários.

## Exemplos de cenários em que o colapso de perfis pode ocorrer

* **Dispositivo compartilhado**: Dispositivo compartilhado refere-se aos dispositivos usados por mais de um indivíduo. Exemplos de dispositivos compartilhados incluem tablets, computadores de biblioteca e quiosques.
* **Email e números de telefone incorretos**: emails e números de telefone incorretos se referem a usuários finais que registram informações de contato inválidas, como &quot;test&quot;<span>@test.com&quot; para email e &quot;+1-111-111-1111&quot; para número de telefone.
* **Valores de identidade incorretos ou incorretos**: valores de identidade errados ou inválidos se referem a valores de identidade não exclusivos que podem mesclar IDs de CRM. Por exemplo, embora os IDFAs devam ter 36 caracteres (32 caracteres alfanuméricos e quatro hifens), há cenários em que um IDFA com um valor de identidade de &quot;user_null&quot; pode ser assimilado. Da mesma forma, os números de telefone suportam apenas caracteres numéricos, mas um namespace de telefone com um valor de identidade &quot;não especificado&quot; pode ser assimilado.

Para obter mais informações sobre cenários de caso de uso para regras de vinculação de gráficos de identidade, leia o documento sobre [exemplos de cenários](./example-scenarios.md).

## Objetivos das regras de vinculação do gráfico de identidade

Com as regras de vinculação do gráfico de identidade, você pode:

* Configure limites para impedir que dois identificadores de pessoa diferentes sejam mesclados em um gráfico de identidade, de modo que um único gráfico de identidade represente apenas uma única pessoa.
   * Os limites configurados são aplicados pelo algoritmo de otimização de identidade.
* Configure as prioridades para associar a um determinado usuário os eventos online conduzidos pelo indivíduo autenticado.

### Limites

Você pode usar limites de namespace para definir o número máximo de identidades que podem existir em um gráfico com base em um determinado namespace. Por exemplo, você pode definir o gráfico para ter no máximo uma identidade com um namespace de ID de CRM, evitando assim a mesclagem de dois identificadores de pessoas diferentes no mesmo gráfico.

* Se um limite não for configurado, isso poderá resultar em mesclagens de gráficos indesejadas, como duas identidades com um namespace de ID do CRM em um gráfico.
* Se um limite não for configurado, o gráfico poderá adicionar quantos namespaces forem necessários, desde que o gráfico esteja dentro das medidas de proteção (50 identidades/gráfico).
* Se um limite for configurado, o algoritmo de otimização de identidade garantirá que o limite seja aplicado.

### Algoritmo de otimização de identidade

O algoritmo de otimização de identidade é uma regra que garante que os limites sejam aplicados. O algoritmo respeita os links mais recentes e remove os links mais antigos para garantir que determinado gráfico permaneça dentro dos limites definidos.

Veja a seguir uma lista das implicações do algoritmo na associação de eventos anônimos a identificadores conhecidos:

* A ECID será associada ao último usuário autenticado se as seguintes condições forem atendidas:
   * Se as IDs do CRM forem mescladas pela ECID (dispositivo compartilhado).
   * Se os limites estiverem configurados para apenas uma ID de CRM.

### Prioridade

>[!IMPORTANT]
>
>No momento, as prioridades de namespace não estão disponíveis para alfa.

Você pode usar a prioridade de namespace para definir quais namespaces são mais importantes do que outros. A hierarquia definida para os namespaces é usada para definir as identidades primárias e armazenar fragmentos de perfil. Se as configurações de prioridade estiverem definidas, a configuração de identidade principal no SDK da Web não será mais usada para determinar quais fragmentos de perfil estão armazenados.

* Os limites e a prioridade são configurações independentes e **não** afetam-se mutuamente:
   * Limites é uma configuração de gráfico de identidade no Serviço de identidade.
   * Priority é uma configuração de fragmento de perfil no Perfil do cliente em tempo real.
   * A prioridade sim **não** afetam as medidas de proteção do sistema de gráficos de identidade.

>[!BEGINSHADEBOX]

**Exemplo de prioridade de namespace**

Suponha que você tenha configurado a seguinte prioridade para seus namespaces:

1. ID do CRM: representa um usuário.
2. IDFA: representa um dispositivo de hardware da Apple, como um iPhone e iPad.
3. GAID: representa um dispositivo de hardware do Google, como o Google Pixel.
4. ECID: representa um navegador da Web, como Firefox, Safari e Chrome.
5. AAID: representa um navegador da Web.
Se a ECID e a AAID forem enviadas simultaneamente, ambas as identidades representarão o mesmo navegador da Web (duplicado).

Se os eventos de experiência a seguir forem assimilados no Experience Platform, os fragmentos de perfil serão armazenados no namespace com a prioridade mais alta.

**Eventos autenticados:**

* Se o mapa de identidade contiver uma ECID, um GAID e uma ID do CRM, as informações do evento serão armazenadas na ID do CRM (identidade principal).
   * O GAID representa um dispositivo de hardware da Google (por exemplo, Google Pixel), a ECID representa um navegador da Web (por exemplo, Google Chrome) e a ID do CRM representa um usuário autenticado.
   * Se o mapa de identidade contiver uma ID do CRM, uma ECID e uma AAID, as informações do evento serão armazenadas em relação à ID do CRM (identidade principal).

**Eventos não autenticados:**

* Se o mapa de identidade contiver uma ECID, IDFA e AAID, as informações do evento serão armazenadas no IDFA (identidade principal).
   * O IDFA representa um dispositivo de hardware da Apple (por exemplo, iPhone), a ECID e a AAID representam um navegador da Web (Safari).

>[!ENDSHADEBOX]

## Próximas etapas

Para obter mais informações sobre regras de vinculação de gráficos de identidade, leia a seguinte documentação:

* [Exemplos de cenários para configurar regras de vinculação de gráficos de identidade](./example-scenarios.md)
* [Serviço de identidade e perfil do cliente em tempo real](identity-and-profile.md)
* [Lógica de vinculação de identidade](./identity-linking-logic.md)