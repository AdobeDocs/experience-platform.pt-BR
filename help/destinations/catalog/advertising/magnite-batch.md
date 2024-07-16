---
title: Destino em lote de transmissão Magnite
description: Use esse destino para fornecer públicos-alvo da CDP do Adobe para a plataforma de transmissão Magnite em lote.
badgeBeta: label="Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1685'
ht-degree: 1%

---


# Magnite Streaming: conexão em lote {#magnite-streaming-batch}

## Visão geral {#overview}

Este documento descreve o destino Magnite Streaming: Batch e fornece exemplos de casos de uso para ajudá-lo a entender melhor como ativar e exportar públicos para ele.

Os públicos-alvo da Adobe Real-Time CDP podem ser fornecidos para a Magnite: plataforma de streaming de duas maneiras: uma por dia ou em tempo real:

1. Se você quiser e/ou precisar fornecer públicos-alvo apenas uma vez por dia, poderá usar o destino Magnite: Lote de transmissão, que fornece públicos-alvo para Magnite: transmissão por meio de uma entrega diária de arquivo em lote S3. Esses públicos-alvo do Batch são armazenados indefinidamente em nossa plataforma, ao contrário dos públicos-alvo em tempo real, que são armazenados apenas por alguns dias.

2. No entanto, se você quiser e/ou precisar fornecer públicos-alvo em tempo real, será necessário usar o destino Magnite: Streaming em tempo real. Ao usar o destino em tempo real, o Magnite: streaming receberá públicos em tempo real, mas só poderemos armazenar públicos em tempo real temporariamente em nossa plataforma, e eles serão removidos do nosso sistema em alguns dias. Por isso, se você quiser usar o destino Magnite: Streaming em tempo real, também precisará usar o destino Magnite: Streaming Batch - cada público-alvo ativado para o destino em tempo real, também precisará ativar para o destino Batch.

Para recapitular: se você quiser fornecer públicos-alvo da Adobe Real-Time CDP apenas uma vez por dia, use o destino Magnite: lote de streaming e os públicos-alvo serão entregues uma vez por dia. Se quiser fornecer públicos-alvo da Adobe Real-Time CDP em tempo real, você usará AMBOS, Magnite: destino de lote de streaming e Magnite: destino de streaming em tempo real. Para obter mais informações, entre em contato com Magnite: Streaming.


Continue lendo abaixo para obter mais informações sobre o destino Magnite: Lote de streaming, como se conectar a ele e como ativar públicos do Adobe Real-Time CDP para ele.
Para obter mais informações sobre o destino em Tempo real, consulte [este documento](magnite-streaming.md).

>[!IMPORTANT]
>
>Este conector de destino está na versão beta e só está disponível para clientes selecionados. Para solicitar acesso, entre em contato com o representante da Adobe.
>
>O conector de destino e a página de documentação são criados e mantidos pela equipe [!DNL Magnite]. Para qualquer consulta ou solicitação de atualização, contate-os diretamente em `adobe-tech@magnite.com`.

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o destino Magnite Streaming: Batch, aqui estão exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso #1 {#use-case-1}

Você ativou um público-alvo no destino Magnite Streaming: Tempo real.

Qualquer público ativado por meio da transmissão Magnite: o destino em tempo real também deve usar a transmissão Magnite: destino Batch, pois os dados da entrega em lote devem substituir/persistir os dados da entrega em tempo real na plataforma de transmissão Magnite.

### Caso de uso #2 {#use-case-2}

Você deseja ativar um público-alvo somente em um lote/cadência diária para a plataforma Magnite Streaming.

Qualquer público ativado por meio da transmissão Magnite: o destino do lote será entregue em um lote/cadência diária e poderá ser direcionado na plataforma de transmissão Magnite.

## Pré-requisitos {#prerequisites}

Para usar os destinos Magnite no Adobe Experience Platform, primeiro é necessário ter uma conta de transmissão Magnite. Se você tiver uma conta [!DNL Magnite Streaming], entre em contato com seu gerente de conta [!DNL Magnite] para receber as credenciais para acessar os destinos [!DNL Magnite's]. Se você não tiver uma conta [!DNL Magnite Streaming], entre em contato com adobe-tech@magnite.com

## Identidades suportadas {#supported-identities}

A Magnite Streaming: o destino do lote pode receber *qualquer* fontes de identidade da CDP do Adobe. Atualmente, esse destino tem três campos de Identidade de destino para você mapear.

>[!NOTE]
>
>*Qualquer* fonte de identidade pode mapear para qualquer uma das Identidades de Destino magnite_deviceId.

| Identidade de destino | Descrição | Considerações |
|:--------------------------- |:------------------------------------------------------------------------------------------------ |:------------------------------------------------------------------------------------- |
| magnite_deviceId_GAID | GOOGLE ADVERTISING ID | Selecione esta Identidade de destino quando sua identidade de origem for um GAID |
| magnite_deviceId_IDFA | Apple ID para anunciantes | Selecione esta identidade de destino quando sua identidade de origem for um IDFA |
| magnite_deviceId_CUSTOM | ID personalizada/definida pelo usuário | Selecione essa identidade de destino quando a identidade de origem não for um GAID ou IDFA, ou se for uma ID personalizada ou definida pelo usuário |

{style="table-layout:auto"}

## Públicos-alvo compatíveis {#supported-audiences}

| Origem do público | Suportado | Descrição |
|-----------------------------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos gerados por meio do [Serviço de segmentação](../../../segmentation/home.md) do Experience Platform. |
| Uploads personalizados | ✓ | Públicos [importados](../../../segmentation/ui/audience-portal.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

| Item | Tipo | Notas |
|-----------------------------|----------|----------|
| Tipo de exportação | Exportação de público | Você está exportando todos os membros de um público-alvo com os identificadores (nome, número de telefone ou outros) usados no destino Magnite Streaming: Batch. |
| Frequência de exportação | Lote | Os destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos baseados em arquivo](/help/destinations/destination-types.md) do lote. |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

Depois que o uso do destino for aprovado e a Magnite Streaming tiver compartilhado suas credenciais, siga as etapas abaixo para autenticar, mapear e compartilhar dados.

### Autenticar para o destino {#authenticate}

Localize o Magnite Streaming: destino do lote no catálogo Adobe Experience. Clique no botão de opções adicionais (\...) e configure a conexão/instância de destino.

Se você já tiver uma conta existente, poderá localizá-la alterando a opção Account type para &quot;Existing account&quot;. Caso contrário, você criará uma conta abaixo:

Para criar uma nova conta e autenticá-la no destino pela primeira vez, preencha os campos obrigatórios &quot;Chave de acesso S3&quot; e &quot;Chave secreta S3&quot; (fornecidos ao seu gerente de conta) e selecione **[!UICONTROL Conectar ao destino]**

![campos de autenticação da configuração de destino não preenchidos](../../assets/catalog/advertising/magnite/destination-batch-config-auth-unfilled.png)

>[!NOTE]
>
>A política de segurança do Magnite Streaming requer uma rotação regular de chaves S3. Você deve esperar atualizar sua conta no futuro com novos direitos de acesso S3 e chaves secretas S3. Você só precisa atualizar a própria conta - os destinos que usam essa conta usarão automaticamente as chaves atualizadas. Se as novas chaves não forem carregadas, os dados não serão enviados para este destino.

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá essa conexão/instância de destino na
futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esta
conexão/instância de destino no futuro.
* **[!UICONTROL Nome do seu parceiro de origem]**: o nome que você gostaria de usar como uma origem na plataforma da Magnite Streaming

![campos de autenticação da configuração de destino preenchidos](../../assets/catalog/advertising/magnite/destination-batch-config-auth-filled.png)

>[!NOTE]
>
>Se você planeja enviar vários tipos de ID (GAID, IDFA etc.) usando o destino Lote, uma nova conexão/instância de destino é necessária para cada um. Entre em contato com seu representante de conta Magnite para obter mais informações.

Você pode continuar selecionando **[!UICONTROL Próximo]**

Na próxima tela, intitulada &quot;Política de governança e ações de aplicação (opcional)&quot;, você pode selecionar qualquer política de governança de dados relevante. A opção &quot;Exportação de dados&quot; geralmente é selecionada para o destino Magnite Streaming Batch.

![Política de governança opcional e ações de imposição](../../assets/catalog/advertising/magnite/destination-batch-config-grouping-policy.png)

Depois de selecionado ou se quiser ignorar esta tela opcional, selecione **[!UICONTROL Criar]**

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Avançar]**.

### Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa de **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Ativar Destinos]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL permissão Exibir Gráfico de Identidade]** [controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Leia [Ativar dados de público-alvo para destinos de exportação de perfil em lote](/help/destinations/ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para esse destino.

### Mapear atributos e identidades {#map}

No **[!UICONTROL campo do Source]**, você pode selecionar qualquer atributo ou identidade para seus dispositivos. Neste exemplo, selecionamos um IdentityMap personalizado chamado &quot;DeviceId&quot;
![mapear os campos de dados desejados para o campo device_id](../../assets/catalog/advertising/magnite/destination-batch-active-audience-field-mapping.png)

No **[!UICONTROL campo de Destino]**:
![selecione a identidade de destino do tipo de dispositivo apropriado](../../assets/catalog/advertising/magnite/destination-batch-active-audience-select-device-type.png) Consulte [Identidades com Suporte](#supported-identities) para obter mais informações.
Neste exemplo, selecionamos o **[!UICONTROL Campo de destino]**: magnite_deviceId_CUSTOM, pois nosso **[!UICONTROL Campo do Source]** foi definido como um IdentityMap personalizado: DeviceID.

>[!NOTE]
>
>Se você planeja enviar/mapear vários tipos de ID (GAID, IDFA etc.) usando o destino Lote, uma nova conexão/instância de destino é necessária para cada um. Entre em contato com seu representante de conta Magnite para obter mais informações.


Na tela &quot;Configurar um nome de arquivo e uma programação de exportação para cada público-alvo&quot;, agora você deve configurar uma Data inicial (obrigatória), uma Data final (opcional) e uma ID de mapeamento (obrigatória) para cada público-alvo.

>[!IMPORTANT]
>
> Uma ID de mapeamento ou &quot;NENHUM&quot; é necessário para este destino.
>
> Uma ID de mapeamento deve ser fornecida quando um público-alvo tiver uma ID de segmento pré-existente conhecida anteriormente pela Magnite Streaming. Caso contrário, &quot;NENHUM&quot; deverá ser usado como a ID do mapeamento.
>
> Ao configurar o nome do arquivo para cada público, inclua a ID de mapeamento por meio do campo &quot;Texto personalizado&quot; para adicionar. A ID do mapeamento será anexada como: `{previous_filename}\_\[MAPPING_ID\].` Se este público-alvo for novo na Magnite Streaming e você não fornecer uma ID do mapeamento, &quot;NENHUM&quot; deverá ser inserido no campo &quot;Texto personalizado&quot;. O novo nome de arquivo neste caso deve ser: `{previous_filename}\_\[NONE\]`.

## Dados exportados / Validar exportação de dados {#exported-data}

Depois que os públicos forem carregados, você poderá validar se os públicos foram criados e carregados corretamente.

* O destino Magnite Streaming Batch fornece arquivos S3 para Magnite Streaming diariamente. Após a entrega e a assimilação, espera-se que os públicos-alvo/segmentos apareçam na Magnite Streaming e possam ser aplicados a uma oferta. Você pode confirmar isso verificando a ID ou o nome do segmento que foi compartilhado durante as etapas de ativação no Adobe Experience Platform.

>[!NOTE]
>
>Os públicos ativados/entregues no destino Magnite Streaming Batch *substituirão* os mesmos públicos que foram ativados/entregues por meio do destino Magnite Streaming Real-Time. Se estiver pesquisando um segmento usando o nome do segmento, talvez você não o encontre em tempo real, até que o lote tenha sido assimilado e processado pela plataforma de Streaming Magnite.

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia a [Visão geral da Governança de Dados](/help/data-governance/home.md).

## Recursos adicionais {#additional-resources}

Para obter a documentação de ajuda adicional, visite a [Magnite Help Center](https://help.magnite.com/help).
