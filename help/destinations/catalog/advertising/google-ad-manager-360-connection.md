---
title: (Beta) [!DNL Google Ad Manager 360] conexão
description: O Google Ad Manager 360 é uma plataforma de veiculação de anúncios da Google que fornece aos editores os meios de gerenciar a exibição de anúncios em seus sites, por meio de vídeo e em aplicativos móveis.
exl-id: 3251145a-3e4d-40aa-b120-d79c8c9c7cae
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 1%

---

# (Beta) [!DNL Google Ad Manager 360] conexão

## Visão geral {#overview}

A variável [!DNL Google Ad Manager 360] conexão permite o upload em lote para [!DNL publisher provided identifiers] (PPID) em [!DNL Google Ad Manager 360], via [!DNL Google Cloud Storage].

Para obter mais detalhes sobre como os identificadores fornecidos pelo editor funcionam no Google Ad Manager 360, consulte [documentação oficial do Google](https://support.google.com/admanager/answer/2880055?hl=en).

>[!IMPORTANT]
>
>No momento, esse destino está na versão beta e só está disponível para um número limitado de clientes. Para solicitar acesso à [!DNL Google Ad Manager 360] conexão, entre em contato com o representante da Adobe e forneça [!DNL organization ID].

A variável [!DNL Google Ad Manager 360] exportações de destino [!DNL CSV] arquivos para seu [!DNL Google Cloud Storage] balde. Depois de exportar o [!DNL CSV] arquivos, você deve importá-los para o [!DNL Google Ad Manager 360] conta.

## Especificações do destino {#specifics}

Observe os seguintes detalhes, específicos do [!DNL Google Ad Manager 360] destinos.

* Os públicos ativados são criados programaticamente na plataforma do Google e preenchidos no arquivo CSV.

## Identidades suportadas {#supported-identities}

[!DNL This integration] O oferece suporte à ativação das identidades descritas na tabela abaixo.

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | Selecione esta identidade de público alvo para a qual enviar públicos [!DNL Google Ad Manager 360] |

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
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, juntamente com os campos de esquema aplicáveis (por exemplo, o PPID), conforme escolhido na tela Selecionar atributos de perfil da [workflow de ativação de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Lote]** | Os destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos baseados em arquivo em lote](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Pré-requisitos {#prerequisites}

### Incluir na lista de permissões {#allow-listing}

A inclusão na lista de permissões é obrigatória antes de configurar o primeiro [!DNL Google Ad Manager 360] destino na Platform. Conclua o processo de inclusão na lista de permissões descrito abaixo antes de criar seu destino.

>[!NOTE]
>
>A exceção a esta regra é para [Audience Manager](https://docs.adobe.com/content/help/pt-BR/experience-cloud/user-guides/home.translate.html) clientes. Se você já tiver criado uma conexão com esse destino Google no Audience Manager, não será necessário passar pelo processo de inclusão na lista de permissões novamente e você poderá prosseguir para as próximas etapas.

1. Siga as etapas descritas na seção [Documentação do Google Ad Manager](https://support.google.com/admanager/answer/3289669?hl=en) para adicionar o Adobe como uma Plataforma de gerenciamento de dados (DMP) vinculada.
2. No [!DNL Google Ad Manager] , vá para **[!UICONTROL Admin]** > **[!UICONTROL Configurações globais]** > **[!UICONTROL Configurações de rede]** e habilite o **[!UICONTROL Acesso à API]** controle deslizante.


## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). No workflow da configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Conectar ao destino]**.

* **[!UICONTROL ID da chave de acesso]**: uma sequência de 61 caracteres alfanuméricos usada para autenticar seu [!DNL Google Cloud Storage] para a Platform.
* **[!UICONTROL Chave de acesso secreta]**: uma sequência de 40 caracteres codificada em base64 usada para autenticar seu [!DNL Google Cloud Storage] para a Platform.

Para obter mais informações sobre esses valores, consulte [Chaves HMAC do Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guia. Para obter etapas sobre como gerar sua própria ID da chave de acesso e chave de acesso secreta, consulte o [[!DNL Google Cloud Storage] visão geral da origem](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Preencher detalhes do destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam360_appendSegmentID"
>title="Anexar ID de público-alvo ao nome do público-alvo"
>abstract="Selecione esta opção para que o nome do público-alvo no Google Ad Manager 360 inclua a ID do público-alvo do Experience Platform, desta forma: `Audience Name (Audience ID)`"

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: Preencha o nome preferencial para este destino.
* **[!UICONTROL Descrição]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Caminho da pasta]**: insira o caminho para a pasta de destino que hospedará os arquivos exportados.
* **[!UICONTROL Nome do bloco]**: Insira o nome do [!DNL Google Cloud Storage] bucket a ser usado por esse destino.
* **[!UICONTROL ID da conta]**: Insira seu [!DNL Audience Link ID] do seu [!DNL Google] conta. Esse é um identificador específico associado à [!DNL Google Ad Manager] rede (não a sua [!DNL Network code]). Você pode encontrar isso em **[!UICONTROL Administração > Configurações globais]** no [!DNL Google Ad Manager] interface.
* **[!UICONTROL Tipo de conta]**: selecione uma opção, dependendo da sua [!DNL Google] conta:
   * Uso `AdX buyer` para [!DNL Google AdX]
   * Uso `DFP by Google` para [!DNL DoubleClick] para editores
* **[!UICONTROL Anexar ID de público-alvo ao nome do público-alvo]**: selecione esta opção para ter o nome do público-alvo no Google Ad Manager 360 incluindo a ID do público-alvo do Experience Platform, desta forma: `Audience Name (Audience ID)`.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

Na etapa Mapeamento de identidade, você pode ver os seguintes mapeamentos pré-preenchidos:

| Mapeamento preenchido | Descrição |
|---------|----------|
| `ECID` -> `ppid` | Este é o único mapeamento pré-preenchido editável pelo usuário. Você pode selecionar qualquer um dos atributos ou namespaces de identidade da Platform e mapeá-los para `ppid`. |
| `metadata.segment.alias` -> `list_id` | Mapeia nomes de público-alvo do Experience Platform para IDs de público-alvo na plataforma do Google. |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | Informa à plataforma Google quando remover usuários desqualificados de segmentos. |

Esses mapeamentos são exigidos pelo [!DNL Google Ad Manager 360] e são criados automaticamente pela Adobe Experience Platform para todos [!DNL Google Ad Manager 360] conexões.

![Imagem da interface mostrando a etapa de mapeamento do Google Ad Manager 360.](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## Dados exportados {#exported-data}

Para verificar se os dados foram exportados com êxito, verifique [!DNL Google Cloud Storage] e verifique se os arquivos exportados contêm as populações de perfis esperadas.

## Solução de problemas {#troubleshooting}

Caso encontre erros ao usar esse destino e precise entrar em contato com o Adobe ou o Google, mantenha as seguintes IDs à mão.

Estas são as IDs de conta do Adobe Google:

* **[!UICONTROL ID da conta]**: 87933855
* **[!UICONTROL ID do cliente]**: 89690775