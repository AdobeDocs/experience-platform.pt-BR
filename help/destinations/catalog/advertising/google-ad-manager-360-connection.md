---
title: (Beta) [!DNL Google Ad Manager 360] conexão
description: O Google Ad Manager 360 é uma plataforma de veiculação de anúncios da Google que fornece aos editores os meios de gerenciar a exibição de anúncios em seus sites, por meio de vídeo e em aplicativos móveis.
exl-id: 3251145a-3e4d-40aa-b120-d79c8c9c7cae
source-git-commit: 21b76877e8b36d6b844d9c0726a2347b1fab170e
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 4%

---

# (Beta) [!DNL Google Ad Manager 360] conexão

>[!IMPORTANT]
>
> A Google está lançando alterações na [API do Google Ads](https://developers.google.com/google-ads/api/docs/start), na [Correspondência do Cliente](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) e na [API de Exibição e Vídeo 360](https://developers.google.com/display-video/api/guides/getting-started/overview) para oferecer suporte aos requisitos de conformidade e consentimento definidos na [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) da União Europeia ([Política de Consentimento do Usuário](https://www.google.com/about/company/user-consent-policy/) da UE). A aplicação dessas alterações aos requisitos de consentimento estará em vigor a partir de 6 de março de 2024.
><br/>
>Para aderir à política de consentimento do usuário da UE e continuar criando listas de públicos-alvo para usuários no Espaço Econômico Europeu (EEE), anunciantes e parceiros devem garantir que eles transmitem o consentimento do usuário final ao fazer upload dos dados de público-alvo. Como Parceiro da Google, o Adobe fornece as ferramentas necessárias para cumprir esses requisitos de consentimento de acordo com a DMA na União Europeia.
><br/>
>Os clientes que compraram o Adobe Privacy &amp; Security Shield e configuraram uma [política de consentimento](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para filtrar perfis não consentidos não precisam tomar nenhuma ação.
><br/>
>Os clientes que não compraram o Adobe Privacy &amp; Security Shield devem usar os recursos de [definição de segmento](../../../segmentation/home.md#segment-definitions) no [Construtor de segmentos](../../../segmentation/ui/segment-builder.md) para filtrar perfis não consentidos, a fim de continuar usando os Destinos Real-Time CDP Google existentes sem interrupção.

A conexão [!DNL Google Ad Manager 360] habilita o carregamento em lote de [!DNL publisher provided identifiers] (PPID) em [!DNL Google Ad Manager 360], via [!DNL Google Cloud Storage].

Para obter mais detalhes sobre como os identificadores fornecidos pelo editor funcionam no Google Ad Manager 360, consulte a [documentação oficial do Google](https://support.google.com/admanager/answer/2880055?hl=en).

>[!IMPORTANT]
>
>Atualmente, esse destino está no Beta e só está disponível para um número limitado de clientes. Para solicitar acesso à conexão [!DNL Google Ad Manager 360], contate o representante da Adobe e forneça seu [!DNL organization ID].

O destino [!DNL Google Ad Manager 360] exporta arquivos [!DNL CSV] para o bucket [!DNL Google Cloud Storage]. Após exportar os arquivos do [!DNL CSV], você deve importá-los para sua conta do [!DNL Google Ad Manager 360].

## Especificações do destino {#specifics}

Observe os detalhes a seguir que são específicos para destinos [!DNL Google Ad Manager 360].

* No momento, este destino não oferece suporte ao recurso [exportar arquivos por demanda](../../ui/export-file-now.md).
* Os públicos ativados são criados programaticamente na plataforma do Google e preenchidos no arquivo CSV.

## Identidades suportadas {#supported-identities}

[!DNL This integration] dá suporte à ativação das identidades descritas na tabela abaixo.

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | Selecione esta identidade de destino para enviar audiências para [!DNL Google Ad Manager 360] |

{style="table-layout:auto"}

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos gerados por meio do [Serviço de segmentação](../../../segmentation/home.md) do Experience Platform. |
| Uploads personalizados | ✓ | Públicos [importados](../../../segmentation/ui/audience-portal.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, juntamente com os campos de esquema aplicáveis (por exemplo, seu PPID), conforme escolhido na tela selecionar atributos de perfil do [fluxo de trabalho de ativação de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Lote]** | Os destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos com base em arquivo de lote](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Pré-requisitos {#prerequisites}

### Incluir na lista de permissões {#allow-listing}

A inclusão na lista de permissões é obrigatória antes de configurar seu primeiro destino do [!DNL Google Ad Manager 360] na Platform. Conclua o processo de inclusão na lista de permissões descrito abaixo antes de criar seu destino.

>[!NOTE]
>
>A exceção a esta regra é para clientes [Audience Manager](https://docs.adobe.com/content/help/pt-BR/experience-cloud/user-guides/home.translate.html) existentes. Se você já tiver criado uma conexão com esse destino Google no Audience Manager, não será necessário passar pelo processo de inclusão na lista de permissões novamente e você poderá prosseguir para as próximas etapas.

1. Siga as etapas descritas na [documentação do Google Ad Manager](https://support.google.com/admanager/answer/3289669?hl=en) para adicionar o Adobe como uma Plataforma de Gerenciamento de Dados vinculada (DMP).
2. Na interface [!DNL Google Ad Manager], vá para **[!UICONTROL Admin]** > **[!UICONTROL Configurações Globais]** > **[!UICONTROL Configurações de Rede]** e habilite o controle deslizante **[!UICONTROL Acesso à API]**.


## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa de **[!UICONTROL Exibir Destinos]** e **[!UICONTROL Gerenciar Destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). No workflow da configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Conectar ao destino]**.

* **[!UICONTROL ID da chave de acesso]**: uma sequência de 61 caracteres alfanuméricos usada para autenticar sua conta do [!DNL Google Cloud Storage] na Platform.
* **[!UICONTROL Chave de acesso secreta]**: uma cadeia de 40 caracteres codificada em base64 usada para autenticar sua conta do [!DNL Google Cloud Storage] na Platform.

Para obter mais informações sobre esses valores, consulte o guia [Chaves HMAC do Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Para obter etapas sobre como gerar sua própria ID da chave de acesso e chave de acesso secreta, consulte a [[!DNL Google Cloud Storage] visão geral da origem](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Preencher detalhes do destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam360_appendSegmentID"
>title="Anexar ID de público-alvo ao nome do público-alvo"
>abstract="Selecione essa opção para que o nome do público-alvo nesse destino inclua a ID do público-alvo da Experience Platform, da seguinte maneira: `Audience Name (Audience ID)`"

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: preencha o nome preferencial para este destino.
* **[!UICONTROL Descrição]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Caminho da pasta]**: insira o caminho para a pasta de destino que hospedará os arquivos exportados.
* **[!UICONTROL Nome do bucket]**: insira o nome do bucket [!DNL Google Cloud Storage] a ser usado por este destino.
* **[!UICONTROL ID da conta]**: digite o [!DNL Audience Link ID] da conta [!DNL Google]. Este é um identificador específico associado à rede do [!DNL Google Ad Manager] (não ao [!DNL Network code]). Você pode encontrar isso em **[!UICONTROL Admin > Configurações globais]** na interface [!DNL Google Ad Manager].
* **[!UICONTROL Tipo de Conta]**: Selecione uma opção, dependendo da sua conta [!DNL Google]:
   * Usar `AdX buyer` para [!DNL Google AdX]
   * Usar `DFP by Google` para [!DNL DoubleClick] para editores
* **[!UICONTROL Anexar a ID de público-alvo ao nome de público-alvo]**: selecione esta opção para que o nome de público-alvo no Google Ad Manager 360 inclua a ID de público-alvo do Experience Platform, desta forma: `Audience Name (Audience ID)`.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Avançar]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa de **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Ativar Destinos]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL permissão Exibir Gráfico de Identidade]** [controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

Na etapa Mapeamento de identidade, você pode ver os seguintes mapeamentos pré-preenchidos:

| Mapeamento preenchido | Descrição |
|---------|----------|
| `ECID` -> `ppid` | Este é o único mapeamento pré-preenchido editável pelo usuário. Você pode selecionar qualquer um dos seus atributos ou namespaces de identidade da Platform e mapeá-los para `ppid`. |
| `metadata.segment.alias` -> `list_id` | Mapeia nomes de público-alvo do Experience Platform para IDs de público-alvo na plataforma do Google. |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | Informa à plataforma Google quando remover usuários desqualificados de segmentos. |

Esses mapeamentos são exigidos pelo [!DNL Google Ad Manager 360] e são criados automaticamente pela Adobe Experience Platform para todas as conexões [!DNL Google Ad Manager 360].

![Imagem da interface do usuário mostrando a etapa de mapeamento do Google Ad Manager 360.](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## Dados exportados {#exported-data}

Para verificar se os dados foram exportados com êxito, verifique o bucket [!DNL Google Cloud Storage] e se os arquivos exportados contêm as populações de perfis esperadas.

## Solução de problemas {#troubleshooting}

Caso encontre erros ao usar esse destino e precise entrar em contato com o Adobe ou o Google, mantenha as seguintes IDs à mão.

Estas são as IDs de conta do Adobe Google:

* **[!UICONTROL ID da conta]**: 87933855
* **[!UICONTROL ID do cliente]**: 89690775