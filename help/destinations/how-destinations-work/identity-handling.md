---
title: Manuseio de identidade no workflow de ativação de destinos
description: Saiba como a exportação de identidade é tratada no fluxo de trabalho de ativação, dependendo do tipo de destino
exl-id: f4894a08-c7a9-4d57-a6d3-660c49206d6a
source-git-commit: 322510055bd8b8803292a2b4af9df9e1dbee7ffb
workflow-type: tm+mt
source-wordcount: '1163'
ht-degree: 1%

---

# Manuseio de identidade no workflow de ativação de destinos

Esta página descreve as particularidades de como as identidades são exportadas para diferentes tipos de destino e ensina como encontrar quais identidades estão disponíveis para exportação, dependendo do destino.

>[!TIP]
>
> Para obter informações abrangentes sobre identidades, namespaces de identidade e definições de termos relacionados à identidade, leia a [visão geral do serviço de identidade](/help/identity-service/home.md).

Cada destino no [catálogo](/help/destinations/catalog/overview.md) é um pouco diferente, portanto não há uma configuração única para todos os destinos. No entanto, há alguns padrões que orientam a configuração de destinos e seus requisitos de identidade, conforme descrito nas seções abaixo.

## Destinos baseados em arquivo {#file-based}

Para [destinos baseados em arquivo](/help/destinations/destination-types.md#file-based) (por exemplo, [!DNL Amazon S3], SFTP, a maioria dos destinos de marketing por email, como [!DNL Adobe Campaign], [!DNL Oracle Eloqua], [!DNL Salesforce Marketing Cloud]), a configuração de identidade na maioria desses destinos está aberta, o que significa que você não precisa selecionar nenhuma identidade na etapa [Selecionar atributos](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) do fluxo de trabalho de ativação em lote.

Se você optar por adicionar identidades às suas exportações de arquivo, observe que apenas uma única identidade do [namespace de identidade](/help/identity-service/features/identity-graph-viewer.md#access-identity-graph-viewer) pode ser selecionada em uma exportação. Ao selecionar uma identidade para exportação, ela é automaticamente selecionada como um [atributo obrigatório](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes) e [chave de desduplicação](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys).

![Uma identidade selecionada como atributo obrigatório e chave de desduplicação.](/help/destinations/assets/how-destinations-work/selected-identity.png)

Como solução alternativa, você pode adicionar mais identidades à exportação se elas tiverem sido assimiladas no Experience Platform como atributos. Veja abaixo um exemplo em que o endereço de email do atributo XDM foi selecionado para exportação, além do namespace de identidade `Phone_E.164`.

![Exemplo de atributo de endereço de email selecionado para exportação.](/help/destinations/assets/how-destinations-work/email-selected.png)

## Exportação de uma identidade de um mapa de identidade em vez da exportação de uma identidade como um atributo XDM - as diferenças {#identity-map-or-attribute}

O número de registros exportados pode ser diferente dependendo se você seleciona para exportar identidades do mapa de identidades ou de identidades que foram assimiladas como atributos no Experience Platform. As [políticas de mesclagem](/help/profile/merge-policies/overview.md) também desempenham uma função importante no número de registros que são exportados quando você seleciona identidades no mapa de identidades.

Por exemplo, considere que, a partir de dois conjuntos de dados diferentes, você tem os seguintes fragmentos de perfil que serão mesclados em um único perfil de cliente:

**Fragmento de perfil um**

| Mapa de identidade | Nome | Sobrenome | Atributo de email |
|---------|----------|---------|--------|
| email1, ID de fidelidade1 | John | Doe | email 1 |


**Fragmento de perfil dois**

| Mapa de identidade | Nome | Sobrenome | Atributo de email |
|---------|----------|---------|--------|
| email2, ID de fidelidade1 | John | Doe | email 2 |

O perfil mesclado seria semelhante ao abaixo:

| Mapa de identidade | Nome | Sobrenome | Atributo de email |
|---------|----------|---------|--------|
| email 1, email2, ID de fidelidade1 | John | Doe | email 2 |

O comportamento de exportação é diferente se você selecionar `IdentityMap: Email` ou `xdm: personalEmail.address` para exportação.

Se um cliente ativar o `IdentityMap: Email`, haverá dois registros no arquivo exportado, um para o email1 e outro para o email2.

No entanto, se um cliente ativar o `xdm: personalEmail.address`, somente o email2 estará presente no registro, já que o campo de atributo de email inclui apenas email2. Essas situações podem abordar diferentes casos de uso nos quais você pode desejar ativar todos os endereços de email que você tem em arquivo para um cliente ou apenas o endereço de email mais recente que você tem em arquivo para o cliente.

O argumento é que o número de registros exportados depende das políticas de mesclagem escolhidas e se você seleciona identidades ou atributos na exportação.

## Destinos de transmissão baseados em API {#streaming-destinations}

[Destinos de streaming baseados em API](/help/destinations/destination-types.md#streaming-destination) criados com [Destination SDK](/help/destinations/destination-sdk/overview.md) (por exemplo, [!DNL Facebook], [!DNL Google Customer Match], [!DNL Pinterest], [!DNL Braze] e outros) oferecem suporte apenas a IDs específicas para exportação. Para obter informações detalhadas sobre as identidades específicas que podem ser exportadas para cada destino, leia a seção *identidades com suporte* em cada página de documentação de destino (por exemplo, consulte a [seção identidades com suporte](/help/destinations/catalog/advertising/pinterest.md) na página de destino [!DNL Pinterest]).

Observe, no entanto, que você tem a flexibilidade de usar dados de [gráficos privados](/help/profile/merge-policies/overview.md#id-stitching) ou de atributos como identidades. Isso significa que é possível mapear atributos XDM para o campo de identidade exigido pelo destino. Veja abaixo um exemplo do destino [!DNL Pinterest], onde o atributo XDM `personalEmail.address` está mapeado para a identidade [!DNL Pinterest] necessária `pinterest_audience`.

>[!TIP]
>
>Quando o campo de origem contiver atributos sem hash, marque a opção **[!UICONTROL Aplicar transformação]** para fazer com que o Experience Platform coloque os dados em hash automaticamente durante a ativação. Leia mais sobre a opção **[!UICONTROL Aplicar transformação]** no [tutorial de ativação de destinos de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md#apply-transformation).

![Exemplo de atributo de endereço de email mapeado para o campo de identidade do destino do Pinterest.](/help/destinations/assets/how-destinations-work/email-mapped-to-identity.png)

### Destinos do Advertising que dependem de integrações de cookies de terceiros {#third-party-cookie-destinations}

Os destinos do Advertising que dependem de cookies de terceiros (por exemplo: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google DV360], [!DNL Bing], [!DNL The Trade Desk]) não exigem que os clientes selecionem IDs no fluxo de trabalho de ativação. Para esses destinos, ao configurar um fluxo de trabalho de ativação, o Experience Platform procura automaticamente a tabela de correspondência de identidades criada pelo [[!UICONTROL serviço de ID do Experience Cloud]](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=pt-BR) e exporta todas as identidades disponíveis para um perfil e com suporte do destino.

Estes destinos exigem uma sincronização de ID para ocorrer por meio do [!UICONTROL serviço de ID do Experience Cloud] ou do [!UICONTROL SDK da Web do Experience Platform].

Se você estiver usando o [!UICONTROL SDK da Web do Experience Platform] e o [!UICONTROL serviço de ID do Experience Cloud] herdado não estiver implementado na página, será necessário garantir que a sequência de dados do site em questão esteja habilitada para permitir a sincronização de ID de terceiros, conforme descrito na [documentação de configuração da sequência de dados](/help/datastreams/configure.md#create).

Ao configurar uma sequência de dados conforme descrito na documentação vinculada acima, você precisa garantir que o controle deslizante da **[!UICONTROL Sincronização de ID de terceiros]** esteja habilitado. A maioria dos clientes deixaria o campo `container_id` em branco (o padrão será 0). Você só precisará alterar esse valor se sua implementação de Audience Manager herdada usar uma ID de contêiner específica (observe, no entanto, que essa seria a grande minoria de clientes).

>[!NOTE]
>
>A maioria desses destinos de publicidade são suportados em Audience Manager (esses tipos de destino são conhecidos em Audience Manager como destinos baseados em dispositivos). Consulte uma [lista de todos os destinos com base em dispositivo com suporte no Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/device-based/device-based-destinations-list.html)). Apenas alguns estão listados no Experience Platform. Para obter informações sobre como compartilhar dados entre Experience Platform e Audience Manager, leia a seção sobre [como habilitar o compartilhamento de dados de Experience Platform para Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#enable-aep-to-aam-data). Atualmente, não há nenhum plano para oferecer suporte a mais destinos de cookies de terceiros.

## Destinos corporativos {#enterprise-destinations}

[Destinos de empresa](/help/destinations/destination-types.md#advanced-enterprise-destinations) ([!DNL Amazon Kinesis], [!DNL Azure Event Hubs], API HTTP) não exigem IDs específicas na exportação de dados, pois eles foram projetados para casos de uso de integração de empresa. No entanto, você pode exportar identidades como atributos XDM ou do mapa de identidade, se desejar. Exiba um [exemplo de dados exportados para o destino HTTP](/help/destinations/catalog/streaming/http-destination.md#exported-data), que inclui o atributo XDM `personalEmail.address` e as identidades `ECID` e `email_lc_sha256` (endereço de email com hash) do mapa de identidade.

## Destinos do Personalization {#personalization-destinations}

[Os destinos do Personalization (ou borda)](/help/destinations/destination-types.md#edge-personalization-destinations) (por exemplo: Adobe Target, [!DNL Custom Personalization]) não exigem nenhuma seleção de identidade no fluxo de trabalho de ativação, pois a integração é uma pesquisa de perfil. O cliente ([!DNL Target], [!DNL Web SDK] ou outros) consulta o [[!UICONTROL Edge]](/help/collection/home.md#edge) e extrai as informações de perfil necessárias para personalização no site.

<!--
![Table with all supported identities](/help/destinations/assets/how-destinations-work/identities-table.png)

-->

## Próximas etapas {#next-steps}

Depois de ler este documento, agora você sabe como descobrir quais identidades são compatíveis ou necessárias para destinos individuais. Agora você também sabe como a seleção de identidade funciona para cada tipo de destino.

Em seguida, você pode ler sobre quais [configurações de exportação](/help/destinations/how-destinations-work/destinations-configurations.md) para destinos são comuns entre tipos de destino, quais podem ser definidas em um nível de destino individual por desenvolvedores e quais configurações podem ser editadas pelos usuários no fluxo de trabalho de ativação.

Você também pode conferir todos os destinos disponíveis no [catálogo](/help/destinations/catalog/overview.md).
