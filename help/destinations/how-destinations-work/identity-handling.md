---
title: Manuseio de identidade no workflow de ativação de destinos
description: Saiba como a exportação de identidade é tratada no fluxo de trabalho de ativação, dependendo do tipo de destino
exl-id: f4894a08-c7a9-4d57-a6d3-660c49206d6a
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 2%

---

# Manuseio de identidade no workflow de ativação de destinos

Esta página descreve as particularidades de como as identidades são exportadas para diferentes tipos de destino e ensina como encontrar quais identidades estão disponíveis para exportação, dependendo do destino.

>[!TIP]
>
> Para obter informações abrangentes sobre identidades, namespaces de identidade e definições de termos relacionados à identidade, leia o [visão geral do serviço de identidade](/help/identity-service/home.md).

Cada destino no [catálogo](/help/destinations/catalog/overview.md) O é um pouco diferente, portanto, não há uma configuração única para todos os destinos. No entanto, há alguns padrões que orientam a configuração de destinos e seus requisitos de identidade, conforme descrito nas seções abaixo.

## Destinos baseados em arquivo {#file-based}

Para [destinos baseados em arquivo](/help/destinations/destination-types.md#file-based) (por exemplo [!DNL Amazon S3], SFTP, a maioria dos destinos de marketing por email, como [!DNL Adobe Campaign], [!DNL Oracle Eloqua], [!DNL Salesforce Marketing Cloud]), a configuração de identidade na maioria desses destinos está aberta, o que significa que você não precisa selecionar nenhuma identidade na [Selecionar atributos](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) etapa do fluxo de trabalho de ativação em lote.

Se você optar por adicionar identidades às exportações de arquivo, observe que apenas uma única identidade da [namespace de identidade](/help/identity-service/ui/identity-graph-viewer.md#access-identity-graph-viewer) podem ser selecionados em uma exportação. Quando você seleciona uma identidade para exportação, ela é automaticamente selecionada como [atributo obrigatório](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes) e [chave de desduplicação](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys).

![Uma identidade selecionada como atributo obrigatório e chave de desduplicação.](/help/destinations/assets/how-destinations-work/selected-identity.png)

Como solução alternativa, você pode adicionar mais identidades à exportação se elas tiverem sido assimiladas no Experience Platform como atributos. Veja abaixo um exemplo em que o endereço de email do atributo XDM foi selecionado para exportação, além do namespace de identidade `Phone_E.164`.

![Exemplo de atributo de endereço de email selecionado para exportação.](/help/destinations/assets/how-destinations-work/email-selected.png)

## Exportação de uma identidade de um mapa de identidade em vez da exportação de uma identidade como um atributo XDM - as diferenças {#identity-map-or-attribute}

O número de registros exportados pode ser diferente dependendo se você seleciona para exportar identidades do mapa de identidades ou de identidades que foram assimiladas como atributos no Experience Platform. [Políticas de mesclagem](/help/profile/merge-policies/overview.md) também desempenham uma função importante no número de registros que são exportados quando você seleciona identidades no mapa de identidades.

Por exemplo, considere que, a partir de dois conjuntos de dados diferentes, você tem os seguintes fragmentos de perfil que serão mesclados em um único perfil de cliente:

**Fragmento do perfil um**

| Mapa de identidade | Primeiro nome | Sobrenome | Atributo de email |
|---------|----------|---------|--------|
| email1, ID de fidelidade1 | John | Doe | email 1 |


**Fragmento de perfil dois**

| Mapa de identidade | Primeiro nome | Sobrenome | Atributo de email |
|---------|----------|---------|--------|
| email2, ID de fidelidade1 | John | Doe | email 2 |

O perfil mesclado seria semelhante ao abaixo:

| Mapa de identidade | Primeiro nome | Sobrenome | Atributo de email |
|---------|----------|---------|--------|
| email 1, email2, ID de fidelidade1 | John | Doe | email 2 |

O comportamento de exportação é diferente conforme você seleciona `IdentityMap: Email` ou `xdm: personalEmail.address` para exportação.

Se um cliente ativar `IdentityMap: Email`, haverá dois registros no arquivo exportado, um para email1 e outro para email2.

No entanto, se um cliente ativar `xdm: personalEmail.address`, somente email2 estará presente no registro, já que o campo de atributo de email inclui apenas email2. Essas situações podem abordar diferentes casos de uso nos quais você pode desejar ativar todos os endereços de email que você tem em arquivo para um cliente ou apenas o endereço de email mais recente que você tem em arquivo para o cliente.

O argumento é que o número de registros exportados depende das políticas de mesclagem escolhidas e se você seleciona identidades ou atributos na exportação.

## Destinos de transmissão baseados em API {#streaming-destinations}

[Destinos de transmissão baseados em API](/help/destinations/destination-types.md#streaming-destination) criado com [Destination SDK](/help/destinations/destination-sdk/overview.md) (por exemplo [!DNL Facebook], [!DNL Google Customer Match], [!DNL Pinterest], [!DNL Braze]e outros) suportam apenas IDs específicas para exportação. Para obter informações detalhadas sobre as identidades específicas que podem ser exportadas para cada destino, leia o *identidades suportadas* em cada página da documentação de destino (por exemplo, consulte a [seção identidades suportadas](/help/destinations/catalog/advertising/pinterest.md) no [!DNL Pinterest] página de destino).

Observe, no entanto, que você tem a flexibilidade de usar dados do [gráficos privados](/help/profile/merge-policies/overview.md#id-stitching) ou de atributos como identidades. Isso significa que é possível mapear atributos XDM para o campo de identidade exigido pelo destino. Veja abaixo um exemplo do [!DNL Pinterest] destino, onde o atributo XDM `personalEmail.address` é mapeado para o [!DNL Pinterest] identidade `pinterest_audience`.

>[!TIP]
>
>Quando o campo de origem contiver atributos sem hash, verifique a **[!UICONTROL Aplicar transformação]** para que o Experience Platform coloque automaticamente os dados em hash na ativação. Leia mais sobre o **[!UICONTROL Aplicar transformação]** opção no [tutorial de ativação de destinos de transmissão](/help/destinations/ui/activate-segment-streaming-destinations.md#apply-transformation).

![Exemplo de atributo de endereço de email mapeado para o campo de identidade do destino do Pinterest.](/help/destinations/assets/how-destinations-work/email-mapped-to-identity.png)

### Destinos de publicidade que dependem de integrações de cookies de terceiros {#third-party-cookie-destinations}

Destinos de publicidade que dependem de cookies de terceiros (por exemplo: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google DV360], [!DNL Bing], [!DNL The Trade Desk]) não exigem que os clientes selecionem IDs no fluxo de trabalho de ativação. Para esses destinos, ao configurar um workflow de ativação, o Experience Platform procura automaticamente a tabela de correspondência de identidades criada pelo [[!UICONTROL Serviço de ID do Experience Cloud]](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=pt-BR) O e o exportam todas as identidades disponíveis para um perfil e suportadas pelo destino.

Esses destinos exigem uma sincronização de ID para ocorrer por meio de [!UICONTROL Serviço de ID do Experience Cloud] ou por meio de [!UICONTROL Experience Platform Web SDK].

Se você estiver usando [!UICONTROL Experience Platform Web SDK] e o legado [!UICONTROL Serviço de ID do Experience Cloud] não estiver implementado na página, será necessário garantir que a sequência de dados do site em questão esteja ativada para permitir a sincronização de ID de terceiros, conforme descrito na seção [configurar documentação de sequência de dados](/help/datastreams/configure.md#create).

Ao configurar um fluxo de dados conforme descrito na documentação vinculada acima, você precisa garantir que o **[!UICONTROL Sincronização de ID de terceiros]** o controle deslizante está ativado. A maioria dos clientes deixaria o `container_id` campo em branco (o padrão será 0). Você só precisará alterar esse valor se sua implementação de Audience Manager herdada usar uma ID de contêiner específica (observe, no entanto, que essa seria a grande minoria de clientes).

>[!NOTE]
>
>A maioria desses destinos de publicidade são suportados em Audience Manager (esses tipos de destino são conhecidos em Audience Manager como destinos baseados em dispositivos). Consulte uma [lista de todos os destinos com base em dispositivo compatíveis no Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/device-based/device-based-destinations-list.html?lang=en)). Apenas alguns estão listados no Experience Platform. Para obter informações sobre o compartilhamento de dados entre Experience Platform e Audience Manager, leia a seção sobre [ativação do compartilhamento de dados do Experience Platform para o Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#enable-aep-to-aam-data). Atualmente, não há nenhum plano para oferecer suporte a mais destinos de cookies de terceiros.

## Destinos corporativos {#enterprise-destinations}

[Destinos corporativos](/help/destinations/destination-types.md#streaming-profile-export) ([!DNL Amazon Kinesis], [!DNL Azure Event Hubs], HTTP API) não exigem IDs específicas na exportação de dados, pois foram projetadas para casos de uso de integração corporativa. No entanto, você pode exportar identidades como atributos XDM ou do mapa de identidade, se desejar. Exibir um [exemplo de dados exportados para o destino HTTP](/help/destinations/catalog/streaming/http-destination.md#exported-data), que inclui os `personalEmail.address` Atributo XDM e as identidades `ECID` e `email_lc_sha256` (endereço de email com hash) no mapa de identidade.

## Destinos de personalização {#personalization-destinations}

[Destinos de personalização (ou borda)](/help/destinations/destination-types.md#edge-personalization-destinations) (por exemplo: Adobe Target, [!DNL Custom Personalization]) não exigem nenhuma seleção de identidade no fluxo de trabalho de ativação, pois a integração é uma pesquisa de perfil. O cliente ([!DNL Target], [!DNL Web SDK], ou outros) consulta o [[!UICONTROL Edge]](/help/collection/home.md#edge) O e o obtêm as informações de perfil necessárias para a personalização no site.

<!--
![Table with all supported identities](/help/destinations/assets/how-destinations-work/identities-table.png)

-->

## Próximas etapas {#next-steps}

Depois de ler este documento, agora você sabe como descobrir quais identidades são compatíveis ou necessárias para destinos individuais. Agora você também sabe como a seleção de identidade funciona para cada tipo de destino.

Em seguida, você pode ler sobre qual [configurações de exportação](/help/destinations/how-destinations-work/destinations-configurations.md) os destinos são comuns entre tipos de destino, que podem ser configurados em um nível de destino individual pelos desenvolvedores e quais configurações podem ser editadas pelos usuários no fluxo de trabalho de ativação.

Você também pode conferir todos os destinos disponíveis na [catálogo](/help/destinations/catalog/overview.md).
