---
title: (Beta) Públicos-Alvo Do Experience Cloud
description: Saiba como compartilhar segmentos do Experience Platform para várias soluções de Experience Platform.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: 2bdbcda3-2efb-4a4e-9702-4fd9991e9461
source-git-commit: 017c8bbc19845c0f60040ba2995b5dd2b0299a8b
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 2%

---

# (Beta) [!UICONTROL Públicos do Experience Cloud] conexão

Esse destino permite compartilhar segmentos do Experience Platform com várias soluções de Experience Cloud, como Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target ou Marketo.

![O destino do Experience Cloud Audiences, destacado no catálogo de destinos.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

>[!IMPORTANT]
>
>* Esse destino substitui o [integração de compartilhamento de segmento herdado](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-in-aam) de Experience Platform para várias soluções de Experience Cloud.
>* Este destino está atualmente na versão beta. A documentação e a funcionalidade estão sujeitas a alterações.


## Casos de uso e benefícios {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o [!UICONTROL Públicos do Experience Cloud] destino, aqui estão exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Habilitar casos de uso da Plataforma de Gerenciamento de Dados {#dmp-use-cases}

No Audience Manager, você pode usar segmentos de Experience Platform para casos de uso da Plataforma de gerenciamento de dados, como:

* Adicionar [dados de terceiros](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html?lang=en#third-party-data) aos seus segmentos;
* [Modelagem algorítmica](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html?lang=en);
* Ative seus segmentos para destinos baseados em cookies que ainda não são compatíveis com o catálogo de destinos Experience Platform.

### Controle granular de segmentos exportados {#segments-control}

Use a nova integração de compartilhamento de segmento de autoatendimento por meio do destino Experience Cloud Audiences para selecionar quais segmentos serão exportados para Audience Manager e além. Isso permite determinar quais segmentos você deseja compartilhar com outras soluções de Experience Cloud e quais segmentos você deseja manter exclusivamente no Experience Platform.

A integração de compartilhamento de segmento herdado não permitiu um controle granular de quais segmentos devem ser exportados para Audience Manager e além.

### Compartilhar segmentos de Experience Platform com outras soluções de Experience Cloud {#share-segments-with-other-solutions}

Além de compartilhar segmentos com o Audience Manager, o cartão de destino do Experience Platform Audiences permite compartilhar segmentos com qualquer outra solução Experience Cloud provisionada para você, incluindo:

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
> * Este destino está disponível para [Adobe Real-time Customer Data Platform Prime e Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) clientes.
> * Você precisa de uma licença de Audience Manager para ativar o [Casos de uso da Plataforma de gerenciamento de dados](#dmp-use-cases) acima referidos.
> * Você *não precisam* uma licença de Audience Manager para compartilhar segmentos de Experience Platform com Adobe Advertising Cloud, Adobe Target, Marketo e outras soluções de Experience Cloud, mencionadas na [seção acima](#share-segments-with-other-solutions).


### Para clientes que estão usando a solução de compartilhamento de segmentos herdada

Se você já estiver compartilhando segmentos de Experience Platform para Audience Manager e outras soluções de Experience Cloud através da [integração de compartilhamento de segmento herdado](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam), entre em contato com o Atendimento ao cliente ou com a equipe de conta do Adobe para desativar a integração herdada. As equipes de atendimento ao cliente e de conta Adobe devem registrar um ticket Jira (consulte ticket de modelo AAM-52354) para desativar a integração.

O tempo de resposta para resolver o tíquete de desprovisionamento para clientes beta é de seis dias úteis ou menos. Depois que a integração herdada existente for desativada, você poderá prosseguir para [criação de uma conexão](#connect) por meio do cartão de destino de autoatendimento.

>[!IMPORTANT]
>
>A exportação de segmentos do Experience Platform para outras soluções será interrompida no tempo entre a resolução do tíquete Jira e o momento em que uma nova conexão é estabelecida por meio do cartão de destino. Você pode minimizar esse tempo de inatividade criando a conexão através do cartão de destino assim que o tíquete Jira for fechado.

## Limitações e chamadas de retorno conhecidas {#known-limitations}

Observe as seguintes limitações conhecidas e chamadas importantes na versão beta do cartão Experience Cloud Audiences:

* [Monitoramento de fluxos de dados](/help/dataflows/ui/monitor-destinations.md) não é compatível.
* Ao se conectar ao destino, você pode ver uma opção para [ativar alertas de fluxo de dados](#enable-alerts). Embora visível na interface do usuário, a variável **a opção ativar alertas não é suportada** na versão beta.
* **Preenchimentos retroativos não são suportados**. A primeira exportação para Audience Manager ou outras soluções de Experience Cloud não inclui uma população histórica dos segmentos.
* Na versão beta, é possível criar **uma única conexão de destino com o destino do Experience Cloud Audiences**, em todas as sandboxes pertencentes à sua organização do Experience Platform.

### Latência ao ativar públicos {#audience-activation-latency}

Há uma latência de quatro horas entre o momento em que os públicos-alvo são ativados pela primeira vez no Experience Platform e o momento em que estão prontos para serem usados no Audience Manager e em outras soluções de Experience Cloud para determinados casos de uso.

Pode levar até 24 horas para que os públicos-alvo estejam totalmente disponíveis em Audience Manager para todos os casos de uso e até 48 horas para que os públicos-alvo dos públicos-alvo de Experience Cloud apareçam nos relatórios de Audience Manager.

Os metadados, como nomes de segmentos, estão disponíveis no Audience Manager em minutos após a configuração da exportação para o destino do Experience Cloud Audiences.

## Identidades suportadas {#supported-identities}

Os perfis exportados para o [!UICONTROL Públicos do Experience Cloud] destino são mapeados de acordo com as identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| ECID | Experience Cloud ID | Um namespace que representa a ECID. Esse namespace também pode ser referenciado pelos seguintes aliases: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte o seguinte documento em [ECID](/help/identity-service/ecid.md) para obter mais informações. |
| GAID | ID de publicidade do Google | Os perfis assimilados no Experience Platform com uma identidade principal da Google Advertising ID (GAID) podem ser exportados para esse destino. |
| IDFA | Apple ID para anunciantes | Os perfis assimilados no Experience Platform com uma identidade principal da Apple ID para anunciantes (IDFA) podem ser exportados para esse destino. |
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | Os perfis assimilados no Experience Platform com uma identidade principal de endereço de email com hash podem ser exportados para esse destino. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportar segmento]** | Você está exportando todos os membros de um segmento (público-alvo) com as identidades listadas na seção acima. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

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


## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de exportação de segmento de transmissão](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para esse destino. Observe que nenhuma [etapa de mapeamento](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) é obrigatório e não [etapa de agendamento](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) O está disponível para este destino.

## Validar exportação de dados {#exported-data}

Para validar uma exportação de dados bem-sucedida, você pode verificar se os segmentos conseguiram chegar à solução de Experience Cloud desejada.

### Validar dados no Audience Manager

Seus segmentos de Experience Platform aparecem no Audience Manager como [sinais](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-signals), [características](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-traits), e [segmentos](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-segments). Você pode verificar no Audience Manager se os dados foram exibidos conforme descrito nos links de documentação acima.

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia o [Visão geral da governança de dados](/help/data-governance/home.md).

A governança de dados no Experience Platform é aplicada por ambos [rótulos de uso de dados](/help/data-governance/labels/reference.md) e de marketing.
Os rótulos de uso de dados serão transferidos para os aplicativos, mas as ações de marketing não. Isso significa que uma vez aterrissados na Audience Manager, os segmentos da Experience Platform podem ser exportados para qualquer destino disponível. No Audience Manager, é possível usar [controles de exportação de dados](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=en) para bloquear segmentos de exportação para determinados destinos.

### Gerenciamento de permissões no Audience Manager

Segmentos e características no Audience Manager estão sujeitos a [Controles de acesso com base em função](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=pt-BR) (RBAC).

Segmentos exportados do Experience Platform são atribuídos a uma fonte de dados específica no Audience Manager, chamada **[!UICONTROL Segmentos Experience Platform]**.

Para permitir que apenas determinados usuários acessem os segmentos, você pode aplicar controles de acesso aos segmentos pertencentes à origem de dados. Você deve definir novas permissões de controle de acesso no Audience Manager para esses segmentos e características criadas a partir de segmentos Experience Platform.
