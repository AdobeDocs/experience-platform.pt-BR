---
title: Manuseio de identidade no fluxo de trabalho de ativação de destinos
description: Saiba como a exportação de identidade é tratada no workflow de ativação, dependendo do tipo de destino
source-git-commit: 6ccf26cbdbbe675d0d731f59cee589d63ca6f8ad
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 2%

---

# Manuseio de identidade no fluxo de trabalho de ativação de destinos

Esta página descreve as particularidades de como as identidades são exportadas para diferentes tipos de destino e ensina como descobrir quais identidades estão disponíveis para exportação, dependendo do destino.

>[!TIP]
>
> Para obter informações extensas sobre identidades, namespaces de identidade e definições de termos relacionados à identidade, leia o [visão geral do serviço de identidade](/help/identity-service/home.md).

Cada destino no [catálogo](/help/destinations/catalog/overview.md) O é um pouco diferente, portanto, não há configuração de tamanho único para todos os destinos. No entanto, existem alguns padrões que orientam a configuração de destinos e seus requisitos de identidade, conforme descrito nas seções abaixo.

## Destinos baseados em arquivo {#file-based}

Para [destinos com base em arquivo](/help/destinations/destination-types.md#file-based) (por exemplo, [!DNL Amazon S3], SFTP, a maioria dos destinos de marketing por email, como [!DNL Adobe Campaign], [!DNL Oracle Eloqua], [!DNL Salesforce Marketing Cloud]), a configuração de identidade na maioria desses destinos está aberta, o que significa que você não é obrigado a selecionar nenhuma identidade na variável [Selecionar atributos](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) etapa do fluxo de trabalho de ativação em lote.

Se você optar por adicionar identidades às exportações do arquivo, observe que apenas uma única identidade do [namespace de identidade](/help/identity-service/ui/identity-graph-viewer.md#access-identity-graph-viewer) pode ser selecionado em uma exportação. Ao selecionar uma identidade para exportação, ela é selecionada automaticamente como uma [atributo obrigatório](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes) e [chave de desduplicação](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys).

![Uma identidade selecionada como atributo obrigatório e chave de desduplicação.](/help/destinations/assets/how-destinations-work/selected-identity.png)

Como solução alternativa, você pode adicionar mais identidades à exportação se elas tiverem sido assimiladas no Experience Platform como atributos. Veja abaixo um exemplo onde o endereço de email do atributo XDM foi selecionado para exportação, além do namespace de identidade `Phone_E.164`.

![Exemplo de atributo de endereço de email selecionado para exportação.](/help/destinations/assets/how-destinations-work/email-selected.png)

## Exportar uma identidade de um mapa de identidade versus exportar uma identidade como um atributo XDM - as diferenças {#identity-map-or-attribute}

O número de registros exportados pode ser diferente, com base na seleção de identidades de exportação no mapa de identidade ou identidades que foram assimiladas como atributos no Experience Platform. [Mesclar políticas](/help/profile/merge-policies/overview.md) também desempenha uma função importante no número de registros que são exportados ao selecionar identidades no mapa de identidade.

Por exemplo, considere que de dois conjuntos de dados diferentes, você tem os seguintes fragmentos de perfil que serão mesclados em um único perfil de cliente:

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

O comportamento de exportação é diferente com base na seleção `IdentityMap: Email` ou `xdm: personalEmail.address` para exportação.

Se um cliente ativar `IdentityMap: Email`, haverá dois registros no arquivo exportado, um para email1 e outro para email2.

No entanto, se um cliente ativar `xdm: personalEmail.address`, somente email2 estará presente no registro, já que o campo de atributo de email inclui somente email2. Essas situações podem atender a casos de uso diferentes, onde você pode ativar para todos os endereços de email que você possui em um arquivo para um cliente ou apenas para o endereço de email mais recente que você possui em um arquivo para o cliente.

A conclusão é que o número de registros que você exporta depende das políticas de mesclagem escolhidas e se você seleciona identidades ou atributos na exportação.

## Destinos de transmissão com base em API {#streaming-destinations}

[Destinos de transmissão com base em API](/help/destinations/destination-types.md#streaming-destination) criado com [Destination SDK](/help/destinations/destination-sdk/overview.md) (por exemplo, [!DNL Facebook], [!DNL Google Customer Match], [!DNL Pinterest], [!DNL Braze]e outros) oferecem suporte somente a IDs específicas para exportação. Para obter informações detalhadas sobre as identidades específicas que podem ser exportadas para cada destino, leia o *identidades suportadas* em cada página de documentação de destino (por exemplo, consulte a seção [seção identidades suportadas](/help/destinations/catalog/advertising/pinterest.md) no [!DNL Pinterest] página de destino).

Observe, no entanto, que você tem a flexibilidade de usar os dados de [gráficos privados](/help/profile/merge-policies/overview.md#id-stitching) ou de atributos como identidades. Isso significa que você pode mapear atributos XDM para o campo de identidade exigido pelo destino. Veja abaixo um exemplo para a variável [!DNL Pinterest] destino, onde o atributo XDM `personalEmail.address` está mapeado para o [!DNL Pinterest] identidade `pinterest_audience`.

>[!TIP]
>
>Quando o campo de origem contém atributos com hash, verifique a **[!UICONTROL Aplicar transformação]** para que o Experience Platform faça o hash automático dos dados na ativação. Leia mais sobre o **[!UICONTROL Aplicar transformação]** na [tutorial de ativação de destinos de transmissão](/help/destinations/ui/activate-segment-streaming-destinations.md#apply-transformation).

![Exemplo de atributo de endereço de email mapeado para campo de identidade para destino Pinterest.](/help/destinations/assets/how-destinations-work/email-mapped-to-identity.png)

### Destinos de publicidade que dependem de integrações de cookies de terceiros {#third-party-cookie-destinations}

Destinos de publicidade que dependem de cookies de terceiros (por exemplo: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google DV360], [!DNL Bing], [!DNL The Trade Desk]) não exige que os clientes selecionem IDs no fluxo de trabalho de ativação. Para esses destinos, ao configurar um workflow de ativação, o Experience Platform procura automaticamente a tabela de correspondência de identidade construída pela variável [[!UICONTROL Serviço de Experience Cloud ID]](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=pt-BR) O e exporta todas as identidades disponíveis para um perfil e suportadas pelo destino.

Esses destinos exigem uma sincronização de ID por meio da variável [!UICONTROL Serviço de Experience Cloud ID] ou [!UICONTROL Experience Platform Web SDK].

Se estiver usando [!UICONTROL Experience Platform Web SDK] e o legado [!UICONTROL Serviço de Experience Cloud ID] não estiver implementado na página, você precisará garantir que o conjunto de dados do site em questão esteja habilitado para permitir a sincronização de IDs de terceiros, conforme descrito no [configurar documentação do datastream](/help/edge/datastreams/configure.md#create).

Ao configurar um armazenamento de dados conforme descrito na documentação vinculada acima, você precisa garantir que a variável **[!UICONTROL Sincronização de ID de terceiros]** está ativado. A maioria dos clientes deixaria o `container_id` em branco (o padrão será 0). Você só precisará alterar esse valor se a implementação Audience Manager herdada usar uma ID de contêiner específica (observe, no entanto, que essa seria a grande minoria de clientes).

>[!NOTE]
>
>A maioria desses destinos de publicidade são suportados no Audience Manager (esses tipos de destino são conhecidos no Audience Manager como destinos com base em dispositivo. Consulte um [lista de todos os destinos com base em dispositivos compatíveis no Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/device-based/device-based-destinations-list.html?lang=en)). Apenas alguns estão listados no Experience Platform. Para obter informações sobre o compartilhamento de dados entre o Experience Platform e o Audience Manager, leia a seção em [habilitar o compartilhamento de dados do Experience Platform para o Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#enable-aep-to-aam-data). No momento, não há plano para suportar mais destinos de cookies de terceiros.

## Destinos corporativos {#enterprise-destinations}

[Destinos corporativos](/help/destinations/destination-types.md#streaming-profile-export) ([!DNL Amazon Kinesis], [!DNL Azure Event Hubs], HTTP (API) não exigem IDs específicas na exportação de dados, pois foram projetadas para casos de uso da integração corporativa. No entanto, você pode exportar identidades como atributos XDM ou do mapa de identidade, se desejar. Exibir um [exemplo de dados exportados para o destino HTTP](/help/destinations/catalog/streaming/http-destination.md#exported-data), que inclui a variável `personalEmail.address` atributo XDM e as identidades `ECID` e `email_lc_sha256` (endereço de email com hash) do mapa de identidade.

## Destinos de personalização {#personalization-destinations}

[Destinos de personalização (ou borda)](/help/destinations/destination-types.md#edge-personalization-destinations) (por exemplo: Adobe Target, [!DNL Custom Personalization]) não exigem nenhuma seleção de identidade no fluxo de trabalho de ativação, pois a integração é uma pesquisa de perfil. O cliente ([!DNL Target], [!DNL Web SDK]ou outros) consulta a [[!UICONTROL Edge]](/help/collection/home.md#edge) e extrai as informações de perfil necessárias para a personalização no site.

<!--
![Table with all supported identities](/help/destinations/assets/how-destinations-work/identities-table.png)

-->

## Próximas etapas {#next-steps}

Depois de ler este documento, você agora sabe como descobrir quais identidades são suportadas ou necessárias para destinos individuais. Agora você também sabe como a seleção de identidade funciona para cada tipo de destino.

Em seguida, você pode ler sobre qual [exportar configurações](/help/destinations/how-destinations-work/destinations-configurations.md) os destinos são comuns em tipos de destino, que podem ser configurados em um nível de destino individual por desenvolvedores e quais configurações podem ser editadas pelos usuários no fluxo de trabalho de ativação.