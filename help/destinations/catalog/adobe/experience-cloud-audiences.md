---
title: (Beta) Públicos-Alvo Do Experience Cloud
description: Saiba como compartilhar públicos do Experience Platform com várias soluções de Experience Platform.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: 2bdbcda3-2efb-4a4e-9702-4fd9991e9461
source-git-commit: 1c9725c108d55aea5d46b086fbe010ab4ba6cf45
workflow-type: tm+mt
source-wordcount: '1631'
ht-degree: 2%

---

# (Beta) [!UICONTROL Públicos do Experience Cloud] conexão

Esse destino permite compartilhar públicos-alvo do Experience Platform com várias soluções de Experience Cloud, como Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target ou Marketo.

![O destino do Experience Cloud Audiences, destacado no catálogo de destinos.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

>[!IMPORTANT]
>
>* Esse destino substitui o [integração de compartilhamento de público herdado](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-in-aam) de Experience Platform para várias soluções de Experience Cloud.
>* Este destino está atualmente na versão beta. A documentação e a funcionalidade estão sujeitas a alterações.

## Casos de uso e benefícios {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o [!UICONTROL Públicos do Experience Cloud] destino, aqui estão exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Habilitar casos de uso da Plataforma de Gerenciamento de Dados {#dmp-use-cases}

No Audience Manager, você pode usar públicos-alvo do Experience Platform para casos de uso da Plataforma de gerenciamento de dados, como:

* Adicionar [dados de terceiros](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html?lang=en#third-party-data) aos seus segmentos;
* [Modelagem algorítmica](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html?lang=en);
* Ative seus públicos para destinos baseados em cookies que ainda não são compatíveis com o catálogo de destinos Experience Platform.

### Controle granular de públicos exportados {#segments-control}

Use a nova integração de compartilhamento de público-alvo de autoatendimento por meio do destino Experience Cloud Audiences para selecionar quais públicos-alvo serão exportados para Audience Manager e além. Isso permite determinar quais públicos-alvo você deseja compartilhar com outras soluções Experience Cloud e quais públicos-alvo você deseja manter exclusivamente no Experience Platform.

A integração de compartilhamento de público-alvo herdada não permitiu um controle granular de quais públicos-alvo devem ser exportados para Audience Manager e além.

### Compartilhar públicos-alvo do Experience Platform com outras soluções de Experience Cloud {#share-segments-with-other-solutions}

Além de compartilhar públicos-alvo com o Audience Manager, o cartão de destino do Experience Platform Audiences permite compartilhar públicos-alvo com qualquer outra solução Experience Cloud que você tenha provisionado para, incluindo:

* Adobe Campaign
* Adobe Target
* Advertising Cloud
* Analytics
* Marketo

<!--

Note: briefly talk about when to share audiences to these destinations using the existing destination cards and when to share using the new Experience Cloud Audiences destination. 

-->

## Pré-requisitos {#prerequisites}

>[!IMPORTANT]
>
> * Este destino está disponível para [Adobe Real-time Customer Data Platform Prime e Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) clientes.
> * Você precisa de uma licença de Audience Manager para ativar o [Casos de uso da Plataforma de gerenciamento de dados](#dmp-use-cases) acima referidos.
> * Você *não precisam* uma licença de Audience Manager para compartilhar públicos-alvo do Experience Platform com a Adobe Advertising Cloud, Adobe Target, Marketo e outras soluções de Experience Cloud, mencionadas na [seção acima](#share-segments-with-other-solutions).

### Para clientes que estão usando a solução de compartilhamento de público-alvo herdada

Se você já estiver compartilhando públicos-alvo do Experience Platform para o Audience Manager e outras soluções de Experience Cloud pelo [integração de compartilhamento de público herdado](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam), entre em contato com o Atendimento ao cliente ou com a equipe de conta do Adobe para desativar a integração herdada. As equipes de atendimento ao cliente e de conta Adobe devem registrar um ticket Jira (consulte ticket de modelo AAM-52354) para desativar a integração.

O tempo de resposta para resolver o tíquete de desprovisionamento para clientes beta é de seis dias úteis ou menos. Depois que a integração herdada existente for desativada, você poderá prosseguir para [criação de uma conexão](#connect) por meio do cartão de destino de autoatendimento.

>[!IMPORTANT]
>
>A exportação de público do Experience Platform para outras soluções será interrompida no tempo entre a resolução do tíquete Jira e o momento em que uma nova conexão é estabelecida por meio do cartão de destino. Você pode minimizar esse tempo de inatividade criando a conexão através do cartão de destino assim que o tíquete Jira for fechado.

## Limitações e chamadas de retorno conhecidas {#known-limitations}

Observe as seguintes limitações conhecidas e chamadas importantes na versão beta do cartão Experience Cloud Audiences:

* [Monitoramento de fluxos de dados](/help/dataflows/ui/monitor-destinations.md) não é compatível.
* Ao se conectar ao destino, você pode ver uma opção para [ativar alertas de fluxo de dados](#enable-alerts). Embora visível na interface do usuário, a variável **a opção ativar alertas não é suportada** na versão beta.
* **Preenchimentos retroativos não são suportados**. A primeira exportação para Audience Manager ou outras soluções de Experience Cloud não inclui uma população histórica dos públicos-alvo.
* Na versão beta, é possível criar **uma única conexão de destino com o destino do Experience Cloud Audiences**, em todas as sandboxes pertencentes à sua organização do Experience Platform.

### Latência ao ativar públicos {#audience-activation-latency}

Há uma latência de quatro horas entre o momento em que os públicos-alvo são ativados pela primeira vez no Experience Platform e o momento em que estão prontos para serem usados no Audience Manager e em outras soluções de Experience Cloud para determinados casos de uso.

Pode levar até 24 horas para que os públicos-alvo estejam totalmente disponíveis em Audience Manager para todos os casos de uso e até 48 horas para que os públicos-alvo dos públicos-alvo de Experience Cloud apareçam nos relatórios de Audience Manager.

Os metadados, como nomes de público-alvo, estão disponíveis no Audience Manager em minutos após a configuração da exportação para o destino do Experience Cloud Audiences.

## Identidades suportadas {#supported-identities}

Os perfis exportados para o [!UICONTROL Públicos do Experience Cloud] destino são mapeados de acordo com as identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| ECID | Experience Cloud ID | Um namespace que representa a ECID. Esse namespace também pode ser referenciado pelos seguintes aliases: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte o seguinte documento em [ECID](/help/identity-service/ecid.md) para obter mais informações. |
| GAID | ID de publicidade do Google | Os perfis assimilados no Experience Platform com uma identidade principal da Google Advertising ID (GAID) podem ser exportados para esse destino. |
| IDFA | Apple ID para anunciantes | Os perfis assimilados no Experience Platform com uma identidade principal da Apple ID para anunciantes (IDFA) podem ser exportados para esse destino. |
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | Os perfis assimilados no Experience Platform com uma identidade principal de endereço de email com hash podem ser exportados para esse destino. |

{style="table-layout:auto"}

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve todos os públicos-alvo que você pode exportar para esse destino.

Todos os destinos oferecem suporte à ativação de públicos-alvo gerados pelo Experience Platform [Serviço de segmentação](../../../segmentation/home.md).

Além disso, esse destino também suporta a ativação dos públicos-alvo descritos na tabela abaixo.

| Tipo de público | Descrição |
---------|----------|
| Uploads personalizados | Públicos-alvo assimilados em Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportação de público]** | Você está exportando todos os membros de um público-alvo com as identidades listadas na seção acima. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

>[!IMPORTANT]
> 
>Na versão beta, você pode criar uma única conexão de destino para o destino do Experience Cloud Audiences, em todas as sandboxes que pertencem à sua organização Experience Platform.

### Autenticar para destino {#authenticate}

Para autenticar no destino, selecione **[!UICONTROL Configurar]** na exibição cartão de destino no catálogo e selecione **[!UICONTROL Conectar ao destino]**.

![Exibição da opção Conectar ao destino para o destino do Experience Cloud Audiences.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Tela Configurar novo destino mostrando as configurações obrigatórias e opcionais para se conectar ao destino do Experience Cloud Audiences.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esse destino no futuro.

<!--

Commenting this part out for the duration of the beta program

### Enable alerts {#enable-alerts}

You can enable alerts to receive notifications on the status of the dataflow to your destination. Select an alert from the list to subscribe to receive notifications on the status of your dataflow. For more information on alerts, see the guide on [subscribing to destinations alerts using the UI](../../ui/alerts.md).
-->

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.


## Ativar públicos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e públicos para destinos de exportação de público de transmissão](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino. Observe que nenhuma [etapa de mapeamento](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) é obrigatório e não [etapa de agendamento](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) O está disponível para este destino.

## Validar exportação de dados {#exported-data}

Para validar uma exportação de dados bem-sucedida, você pode verificar se os públicos-alvo conseguiram chegar à solução de Experience Cloud desejada.

### Validar dados no Audience Manager

Os públicos-alvo do Experience Platform aparecem no Audience Manager como [sinais](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-signals), [características](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-traits), e [segmentos](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-segments). Você pode verificar no Audience Manager se os dados foram exibidos conforme descrito nos links de documentação acima.

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia o [Visão geral da governança de dados](/help/data-governance/home.md).

A governança de dados no Experience Platform é aplicada por ambos [rótulos de uso de dados](/help/data-governance/labels/reference.md) e de marketing.
Os rótulos de uso de dados serão transferidos para os aplicativos, mas as ações de marketing não. Isso significa que uma vez direcionados ao Audience Manager, os públicos-alvo do Experience Platform podem ser exportados para qualquer destino disponível. No Audience Manager, é possível usar [controles de exportação de dados](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=en) para bloquear a exportação de públicos para determinados destinos.

### Gerenciamento de permissões no Audience Manager

Os públicos-alvo e características no Audience Manager estão sujeitos a [Controles de acesso com base em função](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=pt-BR) (RBAC).

Os públicos exportados do Experience Platform são atribuídos a uma fonte de dados específica no Audience Manager, chamada **[!UICONTROL Segmentos Experience Platform]**.

Para permitir que apenas determinados usuários acessem os públicos-alvo, você pode aplicar controles de acesso aos públicos-alvo pertencentes à fonte de dados. Você deve definir novas permissões de controle de acesso no Audience Manager para esses públicos-alvo e características criadas a partir de segmentos de Experience Platform.
