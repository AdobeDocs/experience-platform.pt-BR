---
title: Comportamento de exportação de perfil
description: Saiba como o comportamento de exportação de perfil varia entre os diferentes padrões de integração compatíveis com destinos de Experience Platform.
source-git-commit: 4d1f9fa19bd35095e3ccbd8d83bcc33dcd4c45a8
workflow-type: tm+mt
source-wordcount: '2933'
ht-degree: 0%

---

# Comportamento de exportação de perfil para diferentes tipos de destino

Há vários tipos de destino no Experience Platform, conforme mostrado no diagrama abaixo. Estes destinos têm padrões de exportação ligeiramente diferentes no que respeita ao que desencadeia uma exportação de destino e ao que está incluído numa exportação, tal como descrito nas seções seguintes.

>[!IMPORTANT]
>
>Esta página de documentação descreve somente o comportamento de exportação do perfil para as conexões destacadas na parte inferior do diagrama.

![Tipos de diagrama de destinos](/help/destinations/assets/how-destinations-work/types-of-destinations-v4.png)

## Política de microlotes e agregação

Antes de mergulhar em informações específicas por tipo de destino, é importante entender os conceitos de microlote e política de agregação para *destinos de transmissão*.

Os destinos do Experience Platform exportam dados para integrações baseadas em API como chamadas HTTPS. Quando o serviço de destinos for notificado por outros serviços upstream, os perfis terão sido atualizados como resultado da assimilação em lote, da assimilação em fluxo, da segmentação em lote, da segmentação em fluxo ou das alterações no gráfico de identidade, os dados serão exportados e enviados para destinos de transmissão.

O processo pelo qual os perfis são agregados em mensagens HTTPS antes de serem enviados para pontos de extremidade da API de destino é chamado *microlotes*.

Pegue o [Destino do facebook](/help/destinations/catalog/social/facebook.md) com um *[agregação configurável](/help/destinations/destination-sdk/destination-configuration.md#configurable-aggregation)* política como exemplo - os dados são enviados de forma agregada, onde o serviço de destinos pega todos os dados recebidos do serviço de perfil upstream e os agrega por um dos seguintes, antes de enviá-los para o Facebook:

* Número de registros (máximo de 10.000) ou
* Intervalo da janela de tempo (30 minutos)

Qualquer um dos limites acima é atingido primeiro e inicia uma exportação para o Facebook. Assim, no [!DNL Facebook Custom Audiences] no painel, você pode ver públicos-alvo vindos do Experience Platform em incrementos de registros 10.000. Você pode estar vendo 10.000 registros a cada 10-15 minutos porque os dados são processados e agregados mais rapidamente do que o intervalo de exportação de 30 minutos, e são enviados mais rápido, aproximadamente a cada 10-15 minutos até que todos os registros tenham sido processados. Se não houver registros suficientes para formar um lote 10.000, o número atual de registros será enviado como está quando o limite da janela de tempo for atingido, portanto, você também poderá ver lotes menores enviados para a Facebook.

Como outro exemplo, considere a variável [Destino da API HTTP](/help/destinations/catalog/streaming/http-destination.md), que tem um *[melhor agregação de esforço](/help/destinations/destination-sdk/destination-configuration.md#best-effort-aggregation)* , com `maxUsersPerRequest: 10`. Isso significa que no máximo dez perfis serão agregados antes que uma chamada HTTP seja acionada para esse destino, mas o Experience Platform tenta despachar perfis para o destino assim que o serviço de destinos recebe informações atualizadas de reavaliação de um serviço upstream.

A política de agregação é configurável e os desenvolvedores de destino podem decidir como configurar a política de agregação para melhor atender às limitações de taxa dos pontos de extremidade da API downstream. Leia mais sobre [política de agregação](/help/destinations/destination-sdk/destination-configuration.md#aggregation) na documentação do Destination SDK.

## Destinos de exportação de perfil de transmissão (enterprise) {#streaming-profile-destinations}

>[!IMPORTANT]
>
> Destinos corporativos estão disponíveis somente para [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) clientes.

O [destinos corporativos](/help/destinations/destination-types.md#streaming-profile-export) no Experience Platform, estão Amazon Kinesis, Hubs de eventos do Azure e API HTTP.

O Experience Platform otimiza o comportamento de exportação do perfil para o destino da empresa, para exportar apenas dados para o terminal de API quando ocorrerem atualizações relevantes em um perfil após a qualificação de segmento ou outros eventos significativos. Os perfis são exportados para o seu destino nas seguintes situações:

* A atualização do perfil foi determinada por uma alteração no [associação a segmentos](/help/xdm/field-groups/profile/segmentation.md) para pelo menos um dos segmentos mapeados para o destino. Por exemplo, o perfil se qualificou para um dos segmentos mapeados para o destino ou saiu de um dos segmentos mapeados para o destino.
* A atualização do perfil foi determinada por uma alteração no [mapa de identidade](/help/xdm/field-groups/profile/identitymap.md). Por exemplo, um perfil que já se qualificou para um dos segmentos mapeados para o destino foi adicionado a uma nova identidade no atributo do mapa de identidade.
* A atualização do perfil foi determinada por uma alteração nos atributos para pelo menos um dos atributos mapeados para o destino. Por exemplo, um dos atributos mapeados para o destino na etapa de mapeamento é adicionado a um perfil.

Em todos os casos descritos acima, somente os perfis onde as atualizações relevantes ocorreram são exportados para o seu destino. Por exemplo, se um segmento mapeado para o fluxo de destino tiver cem membros e cinco novos perfis se qualificarem para o segmento, a exportação para o seu destino será incremental e incluirá apenas os cinco novos perfis.

Observe que todos os atributos mapeados são exportados para um perfil, independentemente de onde as alterações se encontrem. Portanto, no exemplo acima, todos os atributos mapeados para esses cinco novos perfis serão exportados mesmo se os atributos em si não tiverem sido alterados.

### O que determina uma exportação de dados e o que está incluído na exportação

Com relação aos dados exportados para um determinado perfil, é importante entender os dois conceitos diferentes de *o que determina uma exportação de dados para o destino da empresa* e *que dados estão incluídos na exportação*.

| O que determina uma exportação de destino | O que está incluído na exportação de destino |
|---------|----------|
| <ul><li>Atributos e segmentos mapeados servem como a dica para uma exportação de destino. Isso significa que se qualquer segmento mapeado alterar estados (de `null` para `realized` ou de `realized` para `exiting`) ou qualquer atributo mapeado for atualizado, uma exportação de destino será iniciada.</li><li>Como as identidades não podem ser mapeadas para destinos corporativos no momento, as alterações em qualquer identidade em um determinado perfil também determinam as exportações de destino.</li><li>Uma alteração para um atributo é definida como qualquer atualização no atributo, independentemente de ser ou não o mesmo valor. Isso significa que uma substituição em um atributo é considerada uma alteração mesmo que o valor em si não tenha sido alterado.</li></ul> | <ul><li>O `segmentMembership` inclui o segmento mapeado no fluxo de dados de ativação, para o qual o status do perfil foi alterado após um evento de qualificação ou de saída de segmento. Observe que outros segmentos não mapeados para os quais o perfil se qualificou podem fazer parte da exportação de destino, se esses segmentos pertencerem ao mesmo [política de mesclagem](/help/profile/merge-policies/overview.md) como o segmento mapeado no fluxo de dados de ativação. </li><li>Todas as identidades na `identityMap` também são incluídos (no momento, o Experience Platform não suporta mapeamento de identidade no destino corporativo).</li><li>Somente os atributos mapeados são incluídos na exportação de destino.</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>Os destinos empresariais fazem o fluxo de dados de preenchimento retroativo ao ativar perfis em um destino. Isso significa que a primeira exportação de dados após configurar um workflow de ativação para um destino incluirá perfis que se qualificaram para o segmento ativado antes que ele seja mapeado para o destino.

>[!BEGINSHADEBOX]

Por exemplo, considere esse fluxo de dados como um destino HTTP, onde três segmentos são selecionados no fluxo de dados e quatro atributos são mapeados para o destino.

![fluxo de dados de destino empresarial](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Uma exportação de perfil para o destino pode ser determinada por um perfil que se qualifica para ou sai de um dos *três segmentos mapeados*. No entanto, na exportação de dados, no `segmentMembership` , outros segmentos não mapeados podem aparecer, se esse perfil específico for membro deles e se compartilharem a mesma política de mesclagem do segmento que acionou a exportação. Se um perfil se qualificar para a variável **Cliente com Carros da Coreia** , mas também é membro do **Assistiu ao filme &quot;De volta ao futuro&quot;** e **Fãs de ficção científica** , esses outros dois segmentos também estarão presentes na variável `segmentMembership` objeto da exportação de dados, mesmo que não estejam mapeados no fluxo de dados, se eles compartilharem a mesma política de mesclagem com a **Cliente com Carros da Coreia** segmento.

Do ponto de vista dos atributos do perfil, qualquer alteração nos quatro atributos mapeados acima determinará uma exportação de destino e qualquer um dos quatro atributos mapeados presentes no perfil estará presente na exportação de dados.

>[!ENDSHADEBOX]

>[!TIP]
>
> Você pode ver exemplos de dados exportados para vários destinos corporativos na [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md#exported-data), [Hubs de Eventos do Azure](/help/destinations/catalog/cloud-storage/azure-event-hubs.md#exported-data)e [API HTTP](/help/destinations/catalog/streaming/http-destination.md#exported-data) páginas da documentação de destino.

## Streaming de destinos com base em API {#streaming-api-based-destinations}

O comportamento de exportação do perfil para destinos de transmissão, como Facebook, Trade Desk e outras integrações baseadas em API é muito semelhante ao comportamento descrito acima para destinos corporativos.

Exemplos de destinos de transmissão são os destinos pertencentes à variável [categorias sociais e publicitárias](/help/destinations/destination-types.md#categories) no catálogo.

O Experience Platform otimiza o comportamento de exportação do perfil para o seu destino de streaming, para exportar apenas dados para destinos com base em API de streaming quando ocorrerem atualizações relevantes em um perfil após a qualificação de segmento ou outros eventos significativos. Os perfis são exportados para o seu destino nas seguintes situações:

* A atualização do perfil foi determinada por uma alteração no [associação a segmentos](/help/xdm/field-groups/profile/segmentation.md) para pelo menos um dos segmentos mapeados para o destino. Por exemplo, o perfil se qualificou para um dos segmentos mapeados para o destino ou saiu de um dos segmentos mapeados para o destino.
* A atualização do perfil foi determinada por uma alteração no [mapa de identidade](/help/xdm/field-groups/profile/identitymap.md) para um namespace de identidade marcado para exportação para esta instância de destino. Por exemplo, um perfil que já se qualificou para um dos segmentos mapeados para o destino foi adicionado a uma nova identidade no atributo do mapa de identidade.
* A atualização do perfil foi determinada por uma alteração nos atributos para pelo menos um dos atributos mapeados para o destino. Por exemplo, um dos atributos mapeados para o destino na etapa de mapeamento é adicionado a um perfil.
* Alterações de consentimento para um perfil quando a imposição de consentimento automatizada é configurada e um perfil recusa. A aplicação automatizada do consentimento enviará um evento de saída de público-alvo para o destino, para que o perfil não seja incluído em nenhum direcionamento no destino.

Em todos os casos descritos acima, somente os perfis onde as atualizações relevantes ocorreram são exportados para o seu destino. Por exemplo, se um segmento mapeado para o fluxo de destino tiver cem membros e cinco novos perfis se qualificarem para o segmento, a exportação para o seu destino será incremental e incluirá apenas os cinco novos perfis.

Observe que todos os atributos mapeados são exportados para um perfil, independentemente de onde as alterações se encontrem. Portanto, no exemplo acima, todos os atributos mapeados para esses cinco novos perfis serão exportados mesmo se os atributos em si não tiverem sido alterados.

### O que determina uma exportação de dados e o que está incluído na exportação

Com relação aos dados exportados para um determinado perfil, é importante entender os dois conceitos diferentes do que determina uma exportação de dados para o destino da API de fluxo e quais dados são incluídos na exportação.

| O que determina uma exportação de destino | O que está incluído na exportação de destino |
|---------|----------|
| <ul><li>Atributos e segmentos mapeados servem como a dica para uma exportação de destino. Isso significa que se qualquer segmento mapeado alterar estados (de `null` para `realized` ou de `realized` para `exiting`) ou qualquer atributo mapeado for atualizado, uma exportação de destino será iniciada.</li><li>Uma alteração no mapa de identidade é definida como uma identidade que é adicionada/removida para a variável [gráfico de identidade](/help/identity-service/ui/identity-graph-viewer.md) do perfil, para namespaces de identidade que são mapeados para exportação.</li><li>Uma alteração para um atributo é definida como qualquer atualização no atributo, para atributos que são mapeados para o destino.</li></ul> | <ul><li>Os segmentos que são mapeados para o destino e que foram alterados serão incluídos na variável `segmentMembership` objeto. Em alguns cenários, eles podem ser exportados usando várias chamadas . Além disso, em alguns cenários, alguns segmentos que não foram alterados também podem ser incluídos na chamada do . Em qualquer caso, somente os segmentos mapeados serão exportados.</li><li>Todas as identidades dos namespaces que são mapeadas para o destino no `identityMap` também são incluídos .</li><li>Somente os atributos mapeados são incluídos na exportação de destino.</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>Os destinos de API de fluxo fazem stream de dados de preenchimento retroativo ao ativar perfis para um destino. Isso significa que a primeira exportação de dados após configurar um workflow de ativação para um destino incluirá perfis que se qualificaram para o segmento ativado antes que ele seja mapeado para o destino.

>[!BEGINSHADEBOX]

Por exemplo, considere esse fluxo de dados em um destino de transmissão em que três segmentos são selecionados no fluxo de dados.

![fluxo de dados de destino](/help/destinations/assets/how-destinations-work/streaming-destination-example-dataflow.png)

Uma exportação de perfil para o destino pode ser determinada por um perfil qualificado para ou existente um dos três segmentos mapeados. Se um perfil se qualificou para a variável **Cliente com Carros da Coreia** , isso acionará uma exportação. Os outros segmentos (**Cidade - Dallas** e **Site básico ativo**) também pode ser exportado caso o perfil tenha esse segmento presente com um dos status possíveis (`realized` ou `exited`). Segmentos não mapeados (como **Fãs de ficção científica**) não será exportada.

Do ponto de vista dos atributos do perfil, qualquer alteração nos três atributos mapeados acima determinará uma exportação de destino.

>[!ENDSHADEBOX]

## Destinos em lote (com base em arquivo) {#file-based-destinations}

Ao exportar perfis para [destinos com base em arquivo](/help/destinations/destination-types.md#file-based) no Experience Platform, há três tipos de agendamentos (listados abaixo) e duas opções de exportação de arquivo (arquivos completos ou incrementais) que você pode usar. Todas essas configurações são definidas em um nível de segmento, mesmo quando vários segmentos são mapeados para um único fluxo de dados de destino.

* Exportações programadas: Configure um destino, adicione um ou mais segmentos, selecione se deseja exportar arquivos completos ou incrementais e selecione uma hora definida a cada dia ou várias vezes ao dia quando os arquivos devem ser exportados. Por exemplo, um tempo de exportação de 17 horas significa que qualquer perfil qualificado para o segmento será exportado às 17:00 horas.
* Após a avaliação do segmento: A exportação é acionada imediatamente após a execução do trabalho diário de avaliação de segmento. Isso significa que os números de perfil exportados no arquivo estão o mais próximos possível da população avaliada mais recente do segmento.
* Exportações por demanda ([exportar arquivo agora](/help/destinations/ui/export-file-now.md)): Com base no último trabalho de avaliação de segmento, um arquivo completo é exportado uma vez por cima das exportações programadas regularmente.

Em qualquer uma das situações de exportação acima, os arquivos exportados incluem os perfis que se qualificaram para a exportação, junto com as colunas que você selecionou como atributos XDM para exportação.

>[!TIP]
>
>Quando um segmento de transmissão é mapeado para um destino em lote, há uma maior probabilidade de o número de perfis no arquivo exportado estar mais próximo do número de usuários no segmento. Isso ocorre porque há uma maior chance de a avaliação de segmento mais recente estar mais próxima do tempo de exportação.

### Exportações de arquivo incremental {#incremental-file-exports}

Nem todas as atualizações em um perfil qualificam um perfil para ser incluído em exportações de arquivo incremental. Por exemplo, se um atributo foi adicionado ou removido de um perfil, isso não inclui o perfil na exportação. Somente perfis para os quais a variável `segmentMembership` for alterado, será incluído nos arquivos exportados. Em outras palavras, somente se o perfil se tornar parte do segmento ou for removido do segmento, ele será incluído nas exportações de arquivo incremental.

Da mesma forma, se uma nova identidade (novo endereço de email, número de telefone, ECID e assim por diante) for adicionada a um perfil no [gráfico de identidade](/help/identity-service/ui/identity-graph-viewer.md), que não representa um motivo para incluir o perfil em uma nova exportação de arquivo incremental.

Se um novo segmento for adicionado a um mapeamento de destino, isso não afetará as qualificações e exportações de outro segmento. Os agendamentos de exportação são configurados individualmente por segmento e os arquivos são exportados separadamente para cada segmento, mesmo que os segmentos tenham sido adicionados ao mesmo fluxo de dados de destino.

>[!BEGINSHADEBOX]

Por exemplo, na configuração de exportação ilustrada abaixo, em que um segmento exporta atualizações de arquivos incrementais, observe as seguintes circunstâncias em que um perfil é incluído ou não em uma exportação de arquivo incremental:

![Exportar com vários atributos selecionados.](/help/destinations/assets/how-destinations-work/export-selection-batch-destination.png)

* Um perfil é incluído em uma exportação de arquivo incremental quando ele se qualifica ou se desqualifica para o segmento.
* Um perfil é *not* incluído em uma exportação de arquivo incremental quando um novo número de telefone é adicionado ao gráfico de identidade.
* Um perfil é *not* incluído em uma exportação de arquivo incremental quando o valor de qualquer um dos campos XDM mapeados como `xdm: loyalty.points`, `xdm: loyalty.tier`, `xdm: personalEmail.address` é atualizado em um perfil.
* Sempre que a variável `segmentMembership.status` O campo XDM é mapeado no workflow de ativação de destino, os perfis que saem do segmento também são incluídos em arquivos incrementais exportados, com um `exited` status.

>[!ENDSHADEBOX]

### O que determina uma exportação de dados e o que está incluído na exportação

Com base nas informações da seção acima, o comportamento de exportação do perfil para destinos com base em arquivo pode ser resumido conforme descrito abaixo:

**Exportações completas de arquivos**

A população ativa completa do segmento é exportada todos os dias.

| O que determina uma exportação de destino | O que está incluído no arquivo exportado |
|---------|----------|
| <ul><li>O agendamento de exportação definido na interface do usuário ou na API e a ação do usuário (seleção de [Exportar arquivo agora](/help/destinations/ui/export-file-now.md) na interface do usuário ou usando o [API de ativação ad-hoc](/help/destinations/api/ad-hoc-activation-api.md)) determinam o início de uma exportação de destino.</li></ul> | Em exportações completas de arquivos, toda a população de perfil ativo de um segmento, com base na avaliação de segmento mais recente, é incluída em cada exportação de arquivo. Os valores mais recentes para cada atributo XDM selecionado para exportação também são incluídos como colunas em cada arquivo. Observe que os perfis no status de saída não são incluídos na exportação de arquivo. |

{style="table-layout:fixed"}

**Exportações de arquivo incremental**

Na primeira exportação de arquivo após a configuração do workflow de ativação, toda a população do segmento é exportada. Nas exportações subsequentes, somente os perfis modificados são exportados.

| O que determina uma exportação de destino | O que está incluído no arquivo exportado |
|---------|----------|
| <ul><li>O agendamento de exportação definido na interface do usuário ou na API determina o início de uma exportação de destino.</li><li>Qualquer alteração na associação de segmentos de um perfil, seja ela qualificada ou desqualificada do segmento, qualifica um perfil para ser incluído em exportações incrementais. Alterações em atributos ou em mapas de identidade de um perfil *não* qualificar um perfil a ser incluído em exportações incrementais.</li></ul> | <p>Os perfis para os quais a associação de segmento foi alterada, juntamente com as informações mais recentes para cada atributo XDM selecionado para exportação.</p><p>Os perfis com status de saída são incluídos nas exportações de destino, se a variável `segmentMembership.status` O campo XDM é selecionado na etapa de mapeamento.</p> |

{style="table-layout:fixed"}

>[!TIP]
>
>Como lembrete, as alterações nos valores do atributo ou nos mapas de identidade de um perfil não qualificam um perfil para ser incluído em uma exportação de arquivo incremental.

## Próximas etapas {#next-steps}

Após a leitura deste documento, você agora sabe o que esperar ver nas exportações de perfil para streaming, corporativo e destinos baseados em arquivos.

Em seguida, você pode ler sobre como [identidades são tratadas](/help/destinations/how-destinations-work/identity-handling.md) no fluxo de trabalho de ativação.
