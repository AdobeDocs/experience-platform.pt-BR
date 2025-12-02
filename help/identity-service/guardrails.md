---
keywords: Experience Platform;identidade;serviço de identidade;solução de problemas;medidas de proteção;diretrizes;limite;
title: Medidas de proteção do serviço de identidade
description: Este documento fornece informações sobre limites de uso e taxa para dados do Serviço de identidade para ajudar você a otimizar o uso do gráfico de identidade.
exl-id: bd86d8bf-53fd-4d76-ad01-da473a1999ab
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 1%

---

# Medidas de proteção para dados do [!DNL Identity Service]

Este documento fornece informações sobre limites de uso e taxa para dados do [!DNL Identity Service] para ajudar você a otimizar o uso do gráfico de identidade. Ao revisar as medidas de proteção a seguir, presume-se que você tenha modelado os dados corretamente. Em caso de dúvidas sobre como modelar os dados, entre em contato com o representante do Atendimento ao cliente.

>[!IMPORTANT]
>
>Verifique os direitos de licença em seu Pedido de Venda e a [Descrição do Produto](https://helpx.adobe.com/legal/product-descriptions.html?lang=pt-BR) correspondente sobre os limites de uso reais, além desta página de medidas de proteção.

## Introdução

Os seguintes serviços da Experience Platform estão envolvidos na modelagem de dados de identidade:

* [Identidades](home.md): identidades Bridge de fontes de dados diferentes conforme são assimiladas na Experience Platform.
* [[!DNL Real-Time Customer Profile]](../profile/home.md): Criar perfis de consumidor unificados usando dados de várias fontes.

## Limites do modelo de dados

As tabelas abaixo fornecem orientação sobre medidas de proteção para limites estáticos, bem como regras de validação a serem consideradas para namespaces de identidade.

### Limites estáticos

A tabela a seguir descreve os limites estáticos aplicados aos dados de identidade.

| Grade de Proteção | Limite | Notas |
| --- | --- | --- |
| Número de identidades em um gráfico | 50 | Quando um gráfico com 50 identidades vinculadas é atualizado, o Serviço de Identidade aplica um mecanismo de &quot;primeiro a entrar, primeiro a sair&quot; e exclui a identidade mais antiga para abrir espaço para a identidade mais recente desse gráfico (**Observação**: o Perfil do cliente em tempo real não é afetado). A exclusão se baseia no tipo de identidade e no carimbo de data e hora. O limite é aplicado no nível da sandbox. Para obter mais informações, leia a seção sobre [noções básicas sobre a lógica de exclusão](#deletion-logic). |
| Número de links para uma identidade para uma única assimilação em lote | 50 | Um único lote pode conter identidades anômalas que causam mesclagens de gráficos indesejadas. Para evitar que isso aconteça, o Serviço de identidade não assimilará identidades que já estejam vinculadas a 50 ou mais identidades. |
| Número de identidades em um registro XDM | 20 | O número mínimo de registros XDM necessários é dois. |
| Número de namespaces personalizados | None | Não há limites para o número de namespaces personalizados que você pode criar. |
| Número de caracteres para um nome para exibição de namespace ou símbolo de identidade | None | Não há limites para o número de caracteres de um nome para exibição de namespace ou símbolo de identidade. |

{style="table-layout:auto"}

### Validação do valor de identidade

A tabela a seguir descreve as regras existentes que devem ser seguidas para garantir uma validação bem-sucedida do valor de identidade.

| Namespace | Regra de validação | Comportamento do sistema quando a regra é violada |
| --- | --- | --- |
| ECID | <ul><li>O valor de identidade de uma ECID deve ter exatamente 38 caracteres.</li><li>O valor de identidade de uma ECID deve consistir apenas em números.</li></ul> | <ul><li>Se o valor de identidade da ECID não tiver exatamente 38 caracteres, o registro será ignorado.</li><li>Se o valor de identidade da ECID contiver caracteres não numéricos, o registro será ignorado.</li></ul> |
| Não ECID | <ul><li>O valor de identidade não pode exceder 1024 caracteres.</li><li>Os valores de identidade não podem ser &quot;null&quot;, &quot;anonymous&quot;, &quot;invalid&quot; ou ser uma cadeia de caracteres vazia (por exemplo: &quot; &quot;, &quot;&quot;, &quot; &quot;).</li></ul> | <ul><li>Se o valor de identidade exceder 1024 caracteres, o registro será ignorado.</li><li>A assimilação da identidade será bloqueada.</li></ul> |

{style="table-layout:auto"}

### Assimilação do namespace de identidade

A partir de 31 de março de 2023, o Serviço de identidade bloqueará a assimilação da Adobe Analytics ID (AAID) para novos clientes. Normalmente, esta identidade é assimilada por meio da [origem do Adobe Analytics](../sources/connectors/adobe-applications/analytics.md) e da [origem do Adobe Audience Manager](../sources//connectors/adobe-applications/audience-manager.md) e é redundante porque a ECID representa o mesmo navegador da Web. Se quiser alterar essa configuração padrão, entre em contato com a equipe de conta da Adobe.

## Medidas de proteção de desempenho {#performance-guardrails}

O Serviço de identidade monitora continuamente os dados recebidos para garantir alto desempenho e confiabilidade em escala. No entanto, um fluxo de dados de eventos de experiência em um curto período pode levar à degradação do desempenho e à latência. A Adobe não é responsável por essa degradação de desempenho.

## Noções básicas sobre a lógica de exclusão quando um gráfico de identidade na capacidade é atualizado {#deletion-logic}

Quando um gráfico de identidade completo é atualizado, o Serviço de identidade exclui a identidade mais antiga no gráfico antes de adicionar a identidade mais recente. Isso é para manter a precisão e a relevância dos dados de identidade. Esse processo de exclusão segue duas regras principais:

### A exclusão da regra #1 é priorizada com base no tipo de identidade de um namespace

A prioridade de exclusão é a seguinte:

1. ID do cookie
2. ID do dispositivo
3. ID entre dispositivos, email e telefone

### A exclusão da regra #2 é baseada no carimbo de data e hora armazenado na identidade

Cada identidade vinculada em um gráfico tem seu próprio carimbo de data e hora correspondente. Quando um gráfico completo é atualizado, o Serviço de identidade exclui a identidade com o carimbo de data e hora mais antigo.

Quando um gráfico completo é atualizado com uma nova identidade, essas duas regras funcionam em conjunto para designar qual identidade mais antiga será excluída. O Serviço de identidade exclui primeiro a ID de cookie mais antiga, em seguida a ID de dispositivo mais antiga e, por fim, a ID/email/telefone entre dispositivos mais antiga.

>[!NOTE]
>
>Se a identidade designada para ser excluída estiver vinculada a várias outras identidades no gráfico, os links que conectam essa identidade também serão excluídos.

### Implicações na implementação

As seções a seguir descrevem as implicações que a lógica de exclusão tem para o Serviço de identidade, o Perfil do cliente em tempo real e o WebSDK.

#### Serviço de identidade: alterações no tipo de identidade do namespace personalizado

Entre em contato com a equipe de conta da Adobe para solicitar uma alteração no tipo de identidade se a sandbox de produção contiver:

* Um namespace personalizado em que os identificadores de pessoa (como CRMIDs) são configurados como tipo de identidade de cookie/dispositivo.
* Um namespace personalizado em que os identificadores de cookie/dispositivo são configurados como tipo de identidade entre dispositivos.

Quando esse recurso estiver disponível, os gráficos que excederem o limite de 50 identidades serão reduzidos para até 50 identidades. Para o Real-Time CDP B2C Edition, isso pode resultar em um aumento mínimo no número de perfis qualificados para um público-alvo, pois esses perfis foram ignorados da Segmentação e Ativação anteriormente.

#### Perfil do cliente em tempo real: impacto nos públicos endereçáveis

A exclusão acontece somente com os dados no Serviço de identidade, não com o Perfil do cliente em tempo real.

* Esse comportamento poderia, consequentemente, criar mais perfis com uma única ECID, pois a ECID não faz mais parte do gráfico de identidade.
* Para que você fique dentro de seus números de direito de público endereçável, é recomendável habilitar a [expiração de dados de perfil pseudônimo](../profile/pseudonymous-profiles.md) para excluir seus perfis antigos.

#### Perfil do cliente em tempo real e WebSDK: exclusão de identidade principal

Se você quiser preservar os eventos autenticados no CRMID, é recomendável alterar as IDs primárias de ECID para CRMID. Leia os seguintes documentos para obter as etapas sobre como implementar essa alteração:

* [Configurar mapa de identidade para marcas Experience Platform](../tags/extensions/client/web-sdk/data-element-types.md#identity-map).
* [Dados de identidade no Experience Platform Web SDK](/help/collection/use-cases/identity/id-overview.md)

### Exemplos de cenários

#### Exemplo um: gráfico grande típico

*Anotações do diagrama:*

* `t` = carimbo de data/hora.
* O valor de um carimbo de data e hora corresponde à recenticidade de uma determinada identidade. Por exemplo, `t1` representa a primeira identidade vinculada (mais antiga) e `t51` representaria a identidade vinculada mais recente.

Neste exemplo, antes que o gráfico à esquerda possa ser atualizado com uma nova identidade, o Serviço de identidade primeiro exclui a identidade existente com o carimbo de data e hora mais antigo. No entanto, como a identidade mais antiga é uma ID de dispositivo, o Serviço de identidade ignora essa identidade até que chegue ao namespace com um tipo que esteja mais alto na lista de prioridade de exclusão, que neste caso é `ecid-3`. Depois que a identidade mais antiga com um tipo de prioridade de exclusão mais alta é removida, o gráfico é atualizado com um novo link, `ecid-51`.

* No raro caso de haver duas identidades com o mesmo carimbo de data e hora e tipo de identidade, o Serviço de Identidade classificará as IDs com base em [XID](./api/list-native-id.md) e fará a exclusão.

![Um exemplo da identidade mais antiga sendo excluída para acomodar a identidade mais recente](./images/graph-limits-v3.png)

#### Exemplo dois: &quot;divisão de gráfico&quot;

>[!BEGINTABS]

>[!TAB Evento de entrada]

*Anotações do diagrama:*

* O diagrama a seguir presume que em `timestamp=50`, existem 50 identidades no gráfico de identidade.
* `(...)` significa as outras identidades que já estão vinculadas dentro do gráfico.

Neste exemplo, ECID:32110 é assimilada e vinculada a um gráfico grande em `timestamp=51`, excedendo o limite de 50 identidades.

![](./images/guardrails/before-split.png)

>[!TAB Processo de exclusão]

Como resultado, o Serviço de identidade exclui a identidade mais antiga com base no carimbo de data e hora e no tipo de identidade. Nesse caso, a ECID:35577 é excluída somente do gráfico de identidade.

![](./images/guardrails/during-split.png)

>[!TAB Saída de gráfico]

Como resultado da exclusão da ECID:35577, as bordas que vincularam a CRMID:60013 e a CRMID:25212 à ECID excluída agora:35577 também são excluídas. Esse processo de exclusão faz com que o gráfico seja dividido em dois gráficos menores.

![](./images/guardrails/after-split.png)

>[!ENDTABS]

#### Exemplo três: &quot;hub-and-spoke&quot;

>[!BEGINTABS]

>[!TAB Evento de entrada]

*Anotações do diagrama:*

* O diagrama a seguir presume que em `timestamp=50`, existem 50 identidades no gráfico de identidade.
* `(...)` significa as outras identidades que já estão vinculadas dentro do gráfico.

Devido à lógica de exclusão, algumas identidades de &quot;hub&quot; também podem ser excluídas. Essas identidades de hub se referem a nós vinculados a várias identidades individuais que, de outra forma, seriam desvinculadas.

No exemplo abaixo, ECID:21011 é assimilada e vinculada ao gráfico em `timestamp=51`, excedendo assim o limite de 50 identidades.

![](./images/guardrails/hub-and-spoke-start.png)

>[!TAB Processo de exclusão]

Como resultado, o Serviço de Identidade exclui a identidade mais antiga somente do gráfico de identidade, que neste caso é ECID:35577. A exclusão de ECID:35577 também resulta na exclusão do seguinte:

* O vínculo entre CRMID: 60013 e a ECID :35577 excluída, resultando em um cenário de divisão de gráfico.
* IDFA: 32110, IDFA: 02383 e as identidades restantes representadas por `(...)`. Essas identidades são excluídas porque, individualmente, não estão vinculadas a outras identidades e, portanto, não podem ser representadas em um gráfico.

![](./images/guardrails/hub-and-spoke-process.png)

>[!TAB Saída de gráfico]

Finalmente, o processo de exclusão produz dois gráficos menores.

![](./images/guardrails/hub-and-spoke-result.png)

>[!ENDTABS]

## Próximas etapas

Consulte a documentação a seguir para obter mais informações sobre [!DNL Identity Service]:

* [Visão geral do [!DNL Identity Service]](home.md)
* [Visualizador de gráficos de identidade](features/identity-graph-viewer.md)

Consulte a documentação a seguir para obter mais informações sobre outras medidas de proteção dos serviços da Experience Platform, informações de latência de ponta a ponta e informações de licenciamento dos documentos Descrição do produto da Real-Time CDP:

* [Medidas de proteção do Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagramas de latência de ponta a ponta](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) para vários serviços da Experience Platform.
* [Real-Time Customer Data Platform (B2C Edition - Pacotes do Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Pacotes do Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Pacotes do Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
