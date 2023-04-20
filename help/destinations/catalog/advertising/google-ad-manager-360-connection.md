---
title: (Beta) [!DNL Google Ad Manager 360] conexão
description: O Google Ad Manager 360 é uma plataforma de veiculação de anúncios da Google que oferece aos editores meios de gerenciar a exibição de anúncios em seus sites, por meio de vídeos e aplicativos móveis.
exl-id: 3251145a-3e4d-40aa-b120-d79c8c9c7cae
source-git-commit: ea480854c6058d84615b66a7df2d7c8fbd619bab
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 1%

---

# (Beta) [!DNL Google Ad Manager 360] conexão

## Visão geral {#overview}

O [!DNL Google Ad Manager 360] a conexão habilita o upload em lote para [!DNL publisher provided identifiers] (PPID) em [!DNL Google Ad Manager 360], via [!DNL Google Cloud Storage].

Para obter mais detalhes sobre como os identificadores fornecidos pelo editor funcionam no Google Ad Manager 360, consulte o [documentação oficial do Google](https://support.google.com/admanager/answer/2880055?hl=en).

>[!IMPORTANT]
>
>No momento, esse destino está na versão Beta e só está disponível para um número limitado de clientes. Para solicitar acesso à [!DNL Google Ad Manager 360] entre em contato com o representante do Adobe e forneça [!DNL organization ID].

O [!DNL Google Ad Manager 360] exportações de destino [!DNL CSV] arquivos para [!DNL Google Cloud Storage] balde. Depois de exportar o [!DNL CSV] arquivos, você deve importá-los para o [!DNL Google Ad Manager 360] conta.

## Especificações do destino {#specifics}

Observe os detalhes a seguir que são específicos para [!DNL Google Ad Manager 360] destinos.

* Públicos ativados são criados de forma programática na plataforma Google e preenchidos no arquivo CSV.

## Identidades suportadas {#supported-identities}

[!DNL This integration] O suporta a ativação de identidades descritas na tabela abaixo.

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | Selecione essa identidade de destino para enviar públicos para o [!DNL Google Ad Manager 360] |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, juntamente com os campos de esquema aplicáveis (por exemplo, seu PPID), conforme escolhido na tela selecionar atributos de perfil do [fluxo de trabalho de ativação de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Lote]** | Destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos com base em arquivo em lote](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Pré-requisitos {#prerequisites}

### Lista de permissões {#allow-listing}

A lista de permissões é obrigatória antes da configuração da primeira [!DNL Google Ad Manager 360] no Platform. Conclua o processo de lista de permissões descrito abaixo, antes de criar seu destino.

>[!NOTE]
>
>A exceção a esta regra é para os [Audience Manager](https://docs.adobe.com/content/help/pt-BR/experience-cloud/user-guides/home.translate.html) clientes. Se você já criou uma conexão com esse destino Google no Audience Manager, não é necessário passar pelo processo de lista de permissões novamente e prosseguir para as próximas etapas.

1. Siga as etapas descritas em [Documentação do Google Ad Manager](https://support.google.com/admanager/answer/3289669?hl=en) para adicionar o Adobe como uma Plataforma de gerenciamento de dados vinculada (DMP).
2. No [!DNL Google Ad Manager] interface, vá para **[!UICONTROL Administrador]** > **[!UICONTROL Configurações globais]** > **[!UICONTROL Configurações de rede]** e ative a **[!UICONTROL Acesso à API]** controle deslizante.


## Conecte-se ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para destino {#authenticate}

Para autenticar para o destino, preencha os campos obrigatórios e selecione **[!UICONTROL Ligar ao destino]**.

* **[!UICONTROL ID da chave de acesso]**: Uma sequência de 61 caracteres alfanuméricos usada para autenticar o [!DNL Google Cloud Storage] para a Platform.
* **[!UICONTROL Chave de acesso secreta]**: Uma string codificada em base64, de 40 caracteres, usada para autenticar seu [!DNL Google Cloud Storage] para a Platform.

Para obter mais informações sobre esses valores, consulte o [Chaves HMAC do Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guia. Para obter etapas sobre como gerar sua própria ID de chave de acesso e chave de acesso secreta, consulte [[!DNL Google Cloud Storage] visão geral da fonte](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Preencha os detalhes do destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam360_appendSegmentID"
>title="Anexar ID de segmento ao nome do segmento"
>abstract="Selecione essa opção para que o nome do segmento no Google Ad Manager 360 inclua a ID do segmento no Experience Platform, assim: `Segment Name (Segment ID)`"

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: Preencha o nome preferencial para esse destino.
* **[!UICONTROL Descrição]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Caminho da pasta]**: Insira o caminho para a pasta de destino que hospedará os arquivos exportados.
* **[!UICONTROL Nome do bucket]**: Insira o nome do [!DNL Google Cloud Storage] bucket a ser usado por este destino.
* **[!UICONTROL ID da conta]**: Insira seu [!DNL Audience Link ID] do [!DNL Google] conta. Esse é um identificador específico associado ao [!DNL Google Ad Manager] rede (não sua [!DNL Network code]). Você pode encontrar isso em **[!UICONTROL Administração > Configurações globais]** no [!DNL Google Ad Manager] interface.
* **[!UICONTROL Tipo de conta]**: Selecione uma opção, dependendo do [!DNL Google] conta:
   * Use `AdX buyer` para [!DNL Google AdX]
   * Use `DFP by Google` para [!DNL DoubleClick] para editores

<!--

*  **[!UICONTROL Append segment ID to segment name]**: Select this option to have the segment name in Google Ad Manager 360 include the segment ID from Experience Platform, like this: `Segment Name (Segment ID)`

-->

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o guia sobre [inscrever-se em alertas de destinos usando a interface do usuário](../../ui/alerts.md).

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

Na etapa Mapeamento de identidade, você pode ver os seguintes mapeamentos pré-preenchidos:

| Mapeamento pré-preenchido | Descrição |
|---------|----------|
| `ECID` -> `ppid` | Este é o único mapeamento pré-preenchido editável pelo usuário. Você pode selecionar qualquer um dos atributos ou namespaces de identidade da Platform e mapeá-los para `ppid`. |
| `metadata.segment.alias` -> `list_id` | Mapeia nomes de segmentos de Experience Platform para IDs de segmento na plataforma Google. |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | Informa à plataforma Google quando remover usuários desqualificados dos segmentos. |

Esses mapeamentos são exigidos por [!DNL Google Ad Manager 360] e são criadas automaticamente pela Adobe Experience Platform para todos [!DNL Google Ad Manager 360] conexões.

![Imagem da interface do usuário que mostra a etapa de mapeamento do Google Ad Manager 360.](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## Dados exportados {#exported-data}

Para verificar se os dados foram exportados com êxito, verifique seu [!DNL Google Cloud Storage] e verifique se os arquivos exportados contêm as populações de perfis esperadas.

## Solução de problemas {#troubleshooting}

Caso encontre erros ao usar esse destino e precise entrar em contato com o Adobe ou Google, mantenha as seguintes IDs em mãos.

Estas são IDs de conta Google do Adobe:

* **[!UICONTROL ID da conta]**: 87933855
* **[!UICONTROL Customer ID]**: 89690775