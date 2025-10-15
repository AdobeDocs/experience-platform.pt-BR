---
title: Comportamento de exportação de perfil
description: Saiba como o comportamento de exportação de perfil varia entre os diferentes padrões de integração compatíveis com destinos do Experience Platform.
exl-id: 2be62843-0644-41fa-a860-ccd65472562e
source-git-commit: 7502810ff329a31f2fdaf6797bc7672118555e6a
workflow-type: tm+mt
source-wordcount: '2935'
ht-degree: 0%

---

# Comportamento de exportação de perfil para diferentes tipos de destino

Há vários tipos de destino no Experience Platform, conforme mostrado no diagrama abaixo. Esses destinos têm padrões de exportação ligeiramente diferentes no que diz respeito ao que desencadeia uma exportação de destino e ao que está incluído numa exportação, tal como descrito nas seções mais adiante.

>[!IMPORTANT]
>
>Esta página de documentação descreve apenas o comportamento de exportação do perfil das conexões destacadas na parte inferior do diagrama.

<!--
>* Note the export behavior change introduced in September 2025 for [enterprise destinations](#enterprise-behavior)
>* This documentation page only describes the profile export behavior for the connections highlighted at the bottom of the diagram.
-->

![Diagrama de tipos de destinos](/help/destinations/assets/how-destinations-work/types-of-destinations-v4.png)

## Agregação de mensagens em destinos de streaming

Antes de mergulhar em informações específicas por tipo de destino, é importante entender o conceito de agregação de mensagens para *destinos de streaming*.

Os destinos do Experience Platform exportam dados para integrações baseadas em API, como chamadas HTTPS. Assim que o serviço de destinos for notificado por outros serviços upstream de que os perfis foram atualizados como resultado da assimilação em lote, assimilação por streaming, segmentação em lote, segmentação por streaming ou alterações no gráfico de identidade, os dados serão exportados e enviados para destinos de streaming.

Os perfis são agregados em mensagens HTTPS antes de serem despachados para endpoints da API de destino.

Pegue o [destino do Facebook](/help/destinations/catalog/social/facebook.md) com uma política de *[agregação configurável](../destination-sdk/functionality/destination-configuration/aggregation-policy.md)* como exemplo - os dados são enviados de forma agregada, em que o serviço de destinos pega todos os dados recebidos do serviço de perfil upstream e os agrega por um dos seguintes, antes de despachá-los para o Facebook:

* Número de registros (máximo de 10.000) ou
* Intervalo da janela de tempo (300 segundos)

Qualquer que seja o limite acima atingido primeiro aciona uma exportação para o Facebook. Portanto, no painel [!DNL Facebook Custom Audiences], você pode ver públicos-alvo vindos do Experience Platform em incrementos de 10.000 registros. Você pode estar vendo 10.000 registros a cada 2-3 minutos porque os dados são processados e agregados mais rapidamente do que o intervalo de exportação de 300 segundos e são enviados mais rapidamente, portanto, aproximadamente a cada 2-3 minutos até que todos os registros tenham sido processados. Se não houver registros suficientes para compor um lote de 10.000, o número atual de registros será enviado como está quando o limite da janela de tempo for atingido, portanto, você também pode ver lotes menores enviados para o Facebook.

Como outro exemplo, considere o [destino da API HTTP](/help/destinations/catalog/streaming/http-destination.md), que tem uma política de *[agregação de melhor esforço](../destination-sdk/functionality/destination-configuration/aggregation-policy.md)*, com `maxUsersPerRequest: 10`. Isso significa que no máximo dez perfis serão agregados antes que uma chamada HTTP seja disparada para esse destino, mas o Experience Platform tenta despachar perfis para o destino assim que o serviço de destinos receber informações de reavaliação atualizadas de um serviço upstream.

A política de agregação é configurável e os desenvolvedores de destino podem decidir como configurar a política de agregação para melhor atender às limitações de taxa dos endpoints da API downstream. Leia mais sobre [política de agregação](../destination-sdk/functionality/destination-configuration/aggregation-policy.md) na documentação do Destination SDK.

## Destinos de exportação (corporativos) de perfil de transmissão {#streaming-profile-destinations}

>[!IMPORTANT]
>
> Os destinos corporativos estão disponíveis somente para clientes do [Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/br/legal/product-descriptions/real-time-customer-data-platform.html?lang=pt-BR).

Os [destinos corporativos](/help/destinations/destination-types.md#advanced-enterprise-destinations) no Experience Platform são Amazon Kinesis, Hubs de Eventos do Azure e API HTTP.

O Experience Platform otimiza o comportamento de exportação de perfis para o destino da sua empresa, a fim de exportar dados somente para o endpoint da API quando atualizações relevantes para um perfil tiverem ocorrido após a qualificação de público-alvo ou outros eventos significativos. Os perfis são exportados para seu destino nas seguintes situações:

* A atualização do perfil foi determinada por uma alteração na [associação de público](/help/xdm/field-groups/profile/segmentation.md) para pelo menos um dos públicos mapeados para o destino. Por exemplo, o perfil se qualificou para um dos públicos mapeados para o destino ou saiu de um dos públicos mapeados para o destino.
* A atualização do perfil foi determinada por uma alteração no [mapa de identidade](/help/xdm/field-groups/profile/identitymap.md). Por exemplo, um perfil que já se qualificou para um dos públicos-alvo mapeados para o destino recebeu uma nova identidade no atributo de mapa de identidade.
* A atualização do perfil foi determinada por uma alteração nos atributos de pelo menos um dos atributos mapeados para o destino. Por exemplo, um dos atributos mapeados para o destino na etapa de mapeamento é adicionado a um perfil.

Em todos os casos descritos acima, somente os perfis em que ocorreram atualizações relevantes são exportados para o seu destino. Por exemplo, se um público-alvo mapeado para o fluxo de destino tiver cem membros e cinco novos perfis se qualificarem para o segmento, a exportação para o destino será incremental e incluirá apenas os cinco novos perfis.

Observe que todos os atributos mapeados são exportados para um perfil, independentemente de onde estejam as alterações. Portanto, no exemplo acima, todos os atributos mapeados para esses cinco novos perfis serão exportados mesmo se os atributos em si não tiverem sido alterados.

### O que determina uma exportação de dados e o que está incluído na exportação {#enterprise-behavior}

Com relação aos dados exportados para um determinado perfil, é importante entender os dois conceitos diferentes de *o que determina uma exportação de dados para o destino da sua empresa* e *quais dados são incluídos na exportação*.

| O que determina uma exportação de destino | O que está incluído na exportação de destino |
|---------|----------|
| <ul><li>Atributos e segmentos mapeados servem como dica para uma exportação de destino. Isso significa que se o status `segmentMembership` de um perfil for alterado para `realized` ou `exiting` ou qualquer atributo mapeado for atualizado, uma exportação de destino será iniciada.</li><li>Como as identidades não podem ser mapeadas para destinos corporativos no momento, as alterações em qualquer identidade em um determinado perfil também determinam as exportações de destino.</li><li>Uma alteração em um atributo é definida como qualquer atualização no atributo, seja ou não o mesmo valor. Isso significa que uma substituição em um atributo é considerada uma alteração, mesmo que o valor em si não tenha sido alterado.</li></ul> | <ul><li>O objeto `segmentMembership` inclui o segmento mapeado no fluxo de dados de ativação, para o qual o status do perfil foi alterado após um evento de qualificação ou saída de segmento. Observe que outros segmentos não mapeados para os quais o perfil se qualificou podem fazer parte da exportação de destino, se esses segmentos pertencerem à mesma [política de mesclagem](/help/profile/merge-policies/overview.md) que o segmento mapeado no fluxo de dados de ativação. </li><li>Todas as identidades no objeto `identityMap` também estão incluídas (no momento, o Experience Platform não oferece suporte ao mapeamento de identidades no destino da empresa).</li><li>Somente os atributos mapeados são incluídos na exportação de destino.</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>Destinos corporativos transmitem dados de preenchimento retroativo ao ativar perfis para um destino. Isso significa que a primeira exportação de dados após a configuração de um fluxo de trabalho de ativação para um destino incluirá perfis que se qualificaram para o público-alvo ativado antes que o público-alvo seja mapeado para o destino.

>[!BEGINSHADEBOX]

Por exemplo, considere esse fluxo de dados para um destino HTTP, onde três públicos-alvo são selecionados no fluxo de dados e quatro atributos são mapeados para o destino.

![fluxo de dados de destino da empresa](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Uma exportação de perfil para o destino pode ser determinada por um perfil qualificado para ou saindo dos *três segmentos mapeados*. No entanto, na exportação de dados, no objeto `segmentMembership`, outros públicos não mapeados poderão aparecer se esse perfil específico for membro deles e se eles compartilharem a mesma política de mesclagem que o público-alvo que acionou a exportação. Se um perfil se qualificar para o público-alvo **Customer with DeLosands Cars**, mas também for membro dos **segmentos assistidos de &quot;Back to the Future&quot;** e **Fãs de ficção científica**, esses dois outros públicos-alvo também estarão presentes no objeto `segmentMembership` da exportação de dados, mesmo que não estejam mapeados no fluxo de dados, se compartilharem a mesma política de mesclagem com o segmento **Customer with DeLosands Cars**.

Do ponto de vista dos atributos de perfil, qualquer alteração nos quatro atributos mapeados acima determinará uma exportação de destino e qualquer um dos quatro atributos mapeados presentes no perfil estará presente na exportação de dados.

>[!ENDSHADEBOX]

>[!TIP]
>
> Você pode ver exemplos de dados exportados para vários destinos da empresa nas páginas de documentação de destino do [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md#exported-data), [Hubs de Eventos do Azure](/help/destinations/catalog/cloud-storage/azure-event-hubs.md#exported-data) e [API HTTP](/help/destinations/catalog/streaming/http-destination.md#exported-data).

## Destinos baseados em API de streaming {#streaming-api-based-destinations}

O comportamento de exportação de perfil para destinos de transmissão, como Facebook, Trade Desk e outras integrações baseadas em API, é muito semelhante ao comportamento descrito acima para destinos corporativos.

Exemplos de destinos de transmissão são os destinos pertencentes às [categorias sociais e de publicidade](/help/destinations/destination-types.md#categories) no catálogo.

O Experience Platform otimiza o comportamento de exportação de perfil para seu destino de streaming, a fim de exportar dados somente para destinos baseados em API de streaming quando atualizações relevantes para um perfil tiverem ocorrido após a qualificação de público-alvo ou outros eventos significativos. Os perfis são exportados para seu destino nas seguintes situações:

* A atualização do perfil foi determinada por uma alteração na [associação de público](/help/xdm/field-groups/profile/segmentation.md) para pelo menos um dos públicos mapeados para o destino. Por exemplo, o perfil se qualificou para um dos públicos mapeados para o destino ou saiu de um dos públicos mapeados para o destino.
* A atualização do perfil foi determinada por uma alteração no [mapa de identidade](/help/xdm/field-groups/profile/identitymap.md) para um namespace de identidade que está marcado para exportação para esta instância de destino. Por exemplo, um perfil que já se qualificou para um dos públicos-alvo mapeados para o destino recebeu uma nova identidade no atributo de mapa de identidade.
* A atualização do perfil foi determinada por uma alteração nos atributos de pelo menos um dos atributos mapeados para o destino. Por exemplo, um dos atributos mapeados para o destino na etapa de mapeamento é adicionado a um perfil.
* O consentimento é alterado para um perfil quando a imposição de consentimento automatizada é configurada e um perfil é recusado. A aplicação automática de consentimento enviará um evento de saída de público-alvo para o destino para que o perfil não seja incluído em nenhum direcionamento no destino.

Em todos os casos descritos acima, somente os perfis em que ocorreram atualizações relevantes são exportados para o seu destino. Por exemplo, se um público-alvo mapeado para o fluxo de destino tiver cem membros e cinco novos perfis se qualificarem para o segmento, a exportação para o destino será incremental e incluirá apenas os cinco novos perfis.

Observe que todos os atributos mapeados são exportados para um perfil, independentemente de onde estejam as alterações. Portanto, no exemplo acima, todos os atributos mapeados para esses cinco novos perfis serão exportados mesmo se os atributos em si não tiverem sido alterados.

### O que determina uma exportação de dados e o que está incluído na exportação {#streaming-behavior}

Em relação aos dados exportados para um determinado perfil, é importante entender os dois conceitos diferentes do que determina uma exportação de dados para o destino da API de streaming e quais dados são incluídos na exportação.

| O que determina uma exportação de destino | O que está incluído na exportação de destino |
|---------|----------|
| <ul><li>Atributos e segmentos mapeados servem como dica para uma exportação de destino. Isso significa que se o status `segmentMembership` de um perfil for alterado para `realized` ou `exiting` ou qualquer atributo mapeado for atualizado, uma exportação de destino será iniciada.</li><li>Uma alteração no mapa de identidade é definida como uma identidade adicionada/removida para o [gráfico de identidade](/help/identity-service/features/identity-graph-viewer.md) do perfil, para namespaces de identidade mapeados para exportação.</li><li>Uma alteração em um atributo é definida como qualquer atualização no atributo, para atributos que são mapeados para o destino.</li></ul> | <ul><li>Os segmentos mapeados para o destino e alterados serão incluídos no objeto `segmentMembership`. Em alguns cenários, eles podem ser exportados usando várias chamadas. Além disso, em alguns cenários, alguns segmentos que não foram alterados também podem ser incluídos na chamada do. Em qualquer caso, somente os segmentos mapeados serão exportados.</li><li>Todas as identidades dos namespaces que estão mapeadas para o destino no objeto `identityMap` também estão incluídas.</li><li>Somente os atributos mapeados são incluídos na exportação de destino.</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>Os destinos da API de transmissão transmitem dados de preenchimento retroativo ao ativar perfis para um destino. Isso significa que a primeira exportação de dados após a configuração de um fluxo de trabalho de ativação para um destino incluirá perfis que se qualificaram para o público-alvo ativado antes que o público-alvo seja mapeado para o destino.

>[!BEGINSHADEBOX]

Por exemplo, considere esse fluxo de dados para um destino de transmissão em que três públicos-alvo são selecionados no fluxo de dados.

![fluxo de dados de destino de streaming](/help/destinations/assets/how-destinations-work/streaming-destination-example-dataflow.png)

Uma exportação de perfil para o destino pode ser determinada por um perfil qualificado para um ou saindo dos três segmentos mapeados. Se um perfil for qualificado para o segmento **Cliente com carros DeLoree**, uma exportação será acionada. Os outros públicos-alvo (**Cidade - Dallas** e **Site Básico Ativo**) também poderão ser exportados caso o perfil tenha esse público-alvo presente com um dos status possíveis (`realized` ou `exited`). Públicos não mapeados (como **fãs de ficção científica**) não serão exportados.

Do ponto de vista dos atributos de perfil, qualquer alteração nos três atributos mapeados acima determinará uma exportação de destino.

>[!ENDSHADEBOX]

## Destinos em lote (baseados em arquivo) {#file-based-destinations}

Ao exportar perfis para [destinos baseados em arquivo](/help/destinations/destination-types.md#file-based) no Experience Platform, há três tipos de agendamentos (listados abaixo) e duas opções de exportação de arquivos (arquivos completos ou incrementais) que você pode usar. Todas essas configurações são definidas em nível de público-alvo, mesmo quando vários públicos-alvo são mapeados para um único fluxo de dados de destino.

* Exportações programadas: configure um destino, adicione um ou mais segmentos, selecione se deseja exportar arquivos completos ou incrementais e selecione um horário definido a cada dia ou várias vezes por dia quando os arquivos devem ser exportados. Por exemplo, um horário de exportação de 17h significa que os perfis qualificados para o público serão exportados às 17h.
* Após a avaliação do segmento: a exportação é acionada imediatamente após a execução diária do trabalho de avaliação do público-alvo. Isso significa que os números de perfil exportados no arquivo estão o mais próximo possível da população avaliada mais recentemente do segmento.
* Exportações por demanda ([exportar arquivo agora](/help/destinations/ui/export-file-now.md)): com base no trabalho de avaliação de público-alvo mais recente, um arquivo completo é exportado uma vez, além das exportações agendadas regularmente.

Em qualquer uma das situações de exportação acima, os arquivos exportados incluem os perfis qualificados para a exportação, junto com as colunas selecionadas como atributos XDM para exportação.

>[!TIP]
>
>Quando um público-alvo de transmissão é mapeado para um destino em lote, há uma maior probabilidade de que o número de perfis no arquivo exportado esteja mais próximo do número de usuários no segmento. Isso ocorre porque há uma maior chance de a última avaliação de público-alvo ter sido executada mais perto do tempo de exportação.

### Exportações incrementais de arquivos {#incremental-file-exports}

Nem todas as atualizações em um perfil qualificam um perfil para ser incluído em exportações de arquivos incrementais. Por exemplo, se um atributo foi adicionado ou removido de um perfil, isso não inclui o perfil na exportação.

No entanto, quando o atributo `segmentMembership` em um perfil for alterado, o perfil será incluído nos arquivos exportados. Em outras palavras, se o perfil se tornar parte do público-alvo ou for removido do público-alvo, ele será incluído nas exportações de arquivos incrementais.

Da mesma forma, se uma nova identidade (novo endereço de email, número de telefone, ECID etc.) for adicionada a um perfil no [gráfico de identidade](/help/identity-service/features/identity-graph-viewer.md), isso fará com que o perfil seja incluído em uma nova exportação de arquivo incremental.

Se um novo público-alvo for adicionado a um mapeamento de destino, as qualificações e exportações de outro segmento não serão afetadas. Os agendamentos de exportação são configurados individualmente por público-alvo e os arquivos são exportados separadamente para cada segmento, mesmo que os públicos-alvo tenham sido adicionados ao mesmo fluxo de dados de destino.

>[!BEGINSHADEBOX]

Por exemplo, na configuração de exportação ilustrada abaixo, em que um público-alvo está exportando atualizações de arquivos incrementais, observe as seguintes circunstâncias em que um perfil é incluído ou não em uma exportação de arquivo incremental:

![Exportar configuração com vários atributos selecionados.](/help/destinations/assets/how-destinations-work/export-selection-batch-destination.png)

* Um perfil *é* incluído em uma exportação de arquivo incremental quando ele se qualifica ou desqualifica para o segmento.
* Um perfil *é* incluído em uma exportação de arquivo incremental quando um novo número de telefone é adicionado ao gráfico de identidade.
* Um perfil *não é* incluído em uma exportação de arquivo incremental quando o valor de qualquer um dos campos XDM mapeados, como `xdm: loyalty.points`, `xdm: loyalty.tier`, `xdm: personalEmail.address`, é atualizado em um perfil.
* Sempre que o campo XDM `segmentMembership.status` é mapeado no fluxo de trabalho de ativação de destino, os perfis que saem do público *também são incluídos* em arquivos incrementais exportados, com status `exited`.

>[!ENDSHADEBOX]

### O que determina uma exportação de dados e o que está incluído na exportação

Com base nas informações na seção acima, o comportamento de exportação do perfil para destinos baseados em arquivo pode ser resumido conforme descrito abaixo:

**Exportações de arquivos completas**

A população ativa completa do público-alvo é exportada todos os dias.

| O que determina uma exportação de destino | O que está incluído no arquivo exportado |
|---------|----------|
| <ul><li>O agendamento de exportação definido na interface ou na API e a ação do usuário (selecionar [Exportar arquivo agora](/help/destinations/ui/export-file-now.md) na interface ou usar a [API de ativação ad-hoc](/help/destinations/api/ad-hoc-activation-api.md)) determinam o início de uma exportação de destino.</li></ul> | Em exportações de arquivos completas, toda a população do perfil ativo de um segmento, com base na última avaliação do público-alvo, é incluída em cada exportação de arquivo. Os valores mais recentes para cada atributo XDM selecionado para exportação também são incluídos como colunas em cada arquivo. Observe que os perfis no status &quot;fechado&quot; não são incluídos na exportação de arquivos. |

{style="table-layout:fixed"}

**Exportações incrementais de arquivos**

Na primeira exportação de arquivo após a configuração do fluxo de trabalho de ativação, toda a população do público-alvo é exportada. Nas exportações subsequentes, somente os perfis modificados serão exportados.

| O que determina uma exportação de destino | O que está incluído no arquivo exportado |
|---------|----------|
| <ul><li>O cronograma de exportação definido na interface ou na API determina o início de uma exportação de destino.</li><li>Quaisquer alterações na associação de público-alvo de um perfil, seja ele qualificado ou desqualificado do segmento, ou alterações em mapas de identidade, qualificam um perfil para ser incluído em exportações incrementais. As alterações nos atributos de um perfil *não* qualificam um perfil para ser incluído em exportações incrementais.</li></ul> | <p>Os perfis para os quais a associação de público-alvo foi alterada, juntamente com as informações mais recentes para cada atributo XDM selecionado para exportação.</p><p>Perfis com o status de saída são incluídos em exportações de destino se o campo XDM `segmentMembership.status` for selecionado na etapa de mapeamento.</p> |

{style="table-layout:fixed"}

>[!TIP]
>
>Como lembrete, as alterações nos mapas de identidade de um perfil o qualificam para ser incluído em uma exportação de arquivo incremental. As alterações nos valores de atributo *não* qualificam-no para ser incluído em uma exportação de arquivo incremental.

## Próximas etapas {#next-steps}

Depois de ler este documento, agora você sabe o que esperar das exportações de perfil para destinos de transmissão, corporativos e baseados em arquivo.

Em seguida, você pode ler sobre como [as identidades são tratadas](/help/destinations/how-destinations-work/identity-handling.md) no fluxo de trabalho de ativação.
