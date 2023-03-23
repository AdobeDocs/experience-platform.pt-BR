---
title: Públicos-alvo do Experience Cloud (Beta)
description: Saiba como compartilhar segmentos do Experience Platform para várias soluções Experience Platform.
last-substantial-update: 2023-01-25T00:00:00Z
source-git-commit: 32222aa1c96537b51cd0db35d9cdabce9210f64a
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 2%

---


# (Beta) [!UICONTROL Públicos-alvo do Experience Cloud] conexão

Esse destino permite que você compartilhe segmentos do Experience Platform para várias soluções do Experience Cloud, como Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target ou Marketo.

![O destino Experience Cloud Audiences , destacado no catálogo de destinos.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

>[!IMPORTANT]
>
>* Esse destino substitui [integração de compartilhamento de segmento herdado](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-in-aam) do Experience Platform para várias soluções Experience Cloud.
>* No momento, esse destino está em beta. A documentação e a funcionalidade estão sujeitas a alterações.


## Casos de uso e benefícios {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar a variável [!UICONTROL Públicos-alvo do Experience Cloud] destino, aqui estão casos de uso de exemplo que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Habilitar casos de uso da Plataforma de gerenciamento de dados {#dmp-use-cases}

No Audience Manager, é possível usar segmentos de Experience Platform para casos de uso da Plataforma de gerenciamento de dados, como:

* Adicionar [dados de terceiros](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html?lang=en#third-party-data) aos seus segmentos;
* [Modelagem algorítmica](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html?lang=en);
* Ative seus segmentos para destinos com base em cookies que ainda não são suportados no catálogo de destinos do Experience Platform.

### Controle granular de segmentos exportados {#segments-control}

Use o novo segmento de autoatendimento que compartilha integração por meio do destino Experience Cloud Audiences para selecionar quais segmentos serão exportados para o Audience Manager e além. Isso permite determinar quais segmentos você deseja compartilhar com outras soluções do Experience Cloud e quais segmentos você deseja manter no Experience Platform exclusivamente.

A integração de compartilhamento de segmento herdado não permitia um controle granular de quais segmentos devem ser exportados para o Audience Manager e outros locais.

### Compartilhe segmentos de Experience Platform com mais soluções de Experience Cloud {#share-segments-with-other-solutions}

Além de compartilhar segmentos com o Audience Manager, a placa de destino Experience Platform Audiences permite compartilhar segmentos com qualquer outra solução de Experience Cloud para a qual você está provisionado, incluindo:

* Adobe Campaign
* Adobe Target
* Advertising Cloud
* Analytics
* Marketo

<!--

Note: briefly talk about when to share segments to these destinations using the existing destination cards and when to share using the new Experience Cloud Audiences destination. 

-->

## Pré-requisitos {#prerequisites}

>[!IMPORTANT]
>
> * Esse destino está disponível para [Adobe Real-time Customer Data Platform Prime e Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) clientes.
> * Você precisa de uma licença do Audience Manager para ativar o [Casos de uso da plataforma de gerenciamento de dados](#dmp-use-cases) acima referido.
> * Você *não precisam* uma licença do Audience Manager para compartilhar segmentos do Experience Platform com Adobe Advertising Cloud, Adobe Target, Marketo e outras soluções do Experience Cloud, mencionadas na [seção acima](#share-segments-with-other-solutions).


### Para clientes que estão usando a solução herdada de compartilhamento de segmentos

Se você já estiver compartilhando segmentos do Experience Platform para o Audience Manager e outras soluções do Experience Cloud por meio do [integração de compartilhamento de segmento herdado](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-in-aam), você deve entrar em contato com o Atendimento ao cliente ou com o Gerente de sucesso do cliente para desativar a integração herdada. As equipes de Atendimento ao cliente e Gerenciamento de suporte ao cliente devem registrar um tíquete Jira (consulte o tíquete do modelo AAM-52354) para desativar a integração.

O tempo de resposta para resolver o tíquete de desprovisionamento para clientes beta é de seis dias úteis ou menos. Depois que a integração herdada existente for desativada, você poderá prosseguir para [criação de uma conexão](#connect) por meio do cartão de destino de autoatendimento.

>[!IMPORTANT]
>
>A exportação de segmentos do Experience Platform para suas outras soluções será interrompida no tempo entre a resolução do tíquete Jira e o momento em que uma nova conexão é estabelecida por meio da placa de destino. Você pode minimizar esse tempo de inatividade criando a conexão através do cartão de destino assim que o tíquete Jira for fechado.

## Limitações e chamadas conhecidas {#known-limitations}

Observe as seguintes limitações conhecidas e chamadas importantes na versão beta da placa Experience Cloud Audiences :

* [Monitoramento de fluxos de dados](/help/dataflows/ui/monitor-destinations.md) não é suportado.
* Ao se conectar ao destino, você pode ver uma opção para [ativar alertas de fluxo de dados](#enable-alerts). Embora visível na interface do usuário, a variável **a opção ativar alertas não é suportada** na versão beta.
* **Os preenchimentos retroativos não são suportados**. A primeira exportação para o Audience Manager ou outras soluções de Experience Cloud não inclui uma população histórica dos segmentos.
* Na versão beta, você pode criar **uma única conexão de destino para o destino Experience Cloud Audiences**, em todas as sandboxes pertencentes à organização do Experience Platform.
* Existe um **latência de quatro horas** entre o momento em que os dados são ativados no Experience Platform e o momento em que os dados estão prontos para serem usados no Audience Manager e em outras soluções do Experience Cloud.

## Identidades suportadas {#supported-identities}

Os perfis exportados para a [!UICONTROL Públicos-alvo do Experience Cloud] são mapeados para as identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| ECID | Experience Cloud ID | Um namespace que representa ECID. Esse namespace também pode ser mencionado pelos seguintes aliases: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte o seguinte documento em [ECID](/help/identity-service/ecid.md) para obter mais informações. |
| GAID | Google Advertising ID | Os perfis assimilados no Experience Platform com uma identidade primária de Google Advertising ID (GAID) podem ser exportados para esse destino. |
| IDFA | Apple ID para anunciantes | Os perfis assimilados no Experience Platform com uma identidade primária da Apple ID para anunciantes (IDFA) podem ser exportados para esse destino. |
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | Os perfis assimilados no Experience Platform com uma identidade primária de endereço de email com hash podem ser exportados para esse destino. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportar segmento]** | Você está exportando todos os membros de um segmento (público-alvo) com as identidades listadas na seção acima. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow para configurar destino , preencha os campos listados nas duas seções abaixo.

>[!IMPORTANT]
> 
>Na versão beta, é possível criar uma única conexão de destino ao destino Públicos-alvo do Experience Cloud, em todas as sandboxes pertencentes à sua organização do Experience Platform.

### Autenticar para destino {#authenticate}

Para autenticar para o destino, selecione **[!UICONTROL Configurar]** na exibição do cartão de destino no catálogo e selecione **[!UICONTROL Ligar ao destino]**.

![Exibição da opção Conectar ao destino para o destino Experience Cloud Audiences .](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### Preencha os detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Configure uma nova tela de destino mostrando as configurações necessárias e opcionais para se conectar ao destino de Públicos-alvo do Experience Cloud.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.

<!--

Commenting this part out for the duration of the beta program

### Enable alerts {#enable-alerts}

You can enable alerts to receive notifications on the status of the dataflow to your destination. Select an alert from the list to subscribe to receive notifications on the status of your dataflow. For more information on alerts, see the guide on [subscribing to destinations alerts using the UI](../../ui/alerts.md).
-->

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.


## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de exportação de segmentos de fluxo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino. Observe que [etapa de mapeamento](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) é obrigatório e não [etapa de programação](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) está disponível para este destino.

## Validar exportação de dados {#exported-data}

Para validar a exportação de dados bem-sucedida, é possível verificar se os segmentos conseguiram chegar à solução de Experience Cloud desejada.

### Validar dados no Audience Manager

Seus segmentos de Experience Platform aparecem no Audience Manager como [sinais](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-signals), [características](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-traits)e [segmentos](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-segments). Você pode verificar no Audience Manager se os dados foram exibidos conforme descrito nos links de documentação acima.

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, leia a [Visão geral da governança de dados](/help/data-governance/home.md).

O controle de dados no Experience Platform é empregado por ambos [rótulos de uso de dados](/help/data-governance/labels/reference.md) e ações de marketing.
Os rótulos de uso de dados serão transferidos para aplicativos, mas as ações de marketing não serão transferidas. Isso significa que, uma vez desembarcados em Audience Manager, os segmentos do Experience Platform podem ser exportados para quaisquer destinos disponíveis. No Audience Manager, você pode usar [controles de exportação de dados](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=en) para impedir que segmentos sejam exportados para determinados destinos.

### Gerenciamento de permissões no Audience Manager

Segmentos e características no Audience Manager estão sujeitos a [Controles de acesso com base em função](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=pt-BR) (RBAC).

Segmentos exportados do Experience Platform são atribuídos a uma fonte de dados específica no Audience Manager chamada **[!UICONTROL Experience Platform Segmentos]**.

Para permitir que somente determinados usuários acessem os segmentos, você pode aplicar controles de acesso aos segmentos pertencentes à fonte de dados. Você deve definir novas permissões de controle de acesso no Audience Manager para esses segmentos e características criadas a partir de segmentos de Experience Platform.