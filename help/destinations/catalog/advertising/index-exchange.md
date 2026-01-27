---
title: Index Exchange
description: Conecte-se ao Index Exchange (Index) e ative os dados para que os segmentos de público-alvo possam ser direcionados por ofertas criadas na interface do usuário de índice.
source-git-commit: 4ecd3b60a6b45a94285785049fd4dee99d7c9bdf
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 2%

---


# [!DNL Index Exchange] {#index-exchange}

## Visão geral {#overview}

[!DNL Index] é uma plataforma global de fornecimento de publicidade que ajuda os proprietários de mídia a maximizar o valor de seu conteúdo em todas as telas. Com mais de 20 anos de liderança no setor, o [!DNL Index] conecta as maiores marcas do mundo com criadores de experiências premium para fornecer experiências de alta qualidade ao consumidor.

Use este conector de destino para exportar segmentos de público do Adobe Experience Platform diretamente para a plataforma de publicidade programática do [!DNL Index Exchange].

Depois de exportados, esses segmentos de público-alvo podem ser usados para direcionar ofertas por proprietários de mídia, parceiros de marketplace ou compartilhados com editores e curadores por fornecedores de marketplace.

>[!IMPORTANT]
>
>O conector de destino e a página de documentação são criados e mantidos pela equipe [!DNL Index]. Para perguntas ou solicitações de atualização, contate-os diretamente em [technical_am_marketplace@indexexchange.com](mailto:technical_am_marketplace@indexexchange.com).

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o destino [!DNL Index Exchange], veja a seguir exemplos de casos de uso que os clientes da Experience Platform podem resolver usando esse destino.

### Direcionamento de usuários em plataformas móveis, da Web e de CTV {#targeting-users}

Proprietários de mídia, parceiros de marketplace ou fornecedores de marketplace que desejam enviar públicos do Experience Platform para o [!DNL Index] para usuários de destino em plataformas móveis, da Web e de CTV, usando um grande intervalo de identificadores.

### Direcionamento de conteúdo específico em plataformas móveis, da Web e de CTV {#targeting-content}

Proprietários de mídia, parceiros de marketplace ou fornecedores de marketplace que desejam enviar públicos do Experience Platform para o [!DNL Index] para usuários de destino que visualizam conteúdo específico em plataformas móveis, da Web e de CTV usando URLs, pacotes de aplicativos ou IDs de conteúdo específicos.

## Pré-requisitos {#prerequisites}

Os segmentos de público-alvo devem ser registrados com [!DNL Index] por meio de um processo adicional ao usar este destino antes de serem exibidos na sua conta. Entre em contato com o representante de conta do [!DNL Index Exchange] para obter assistência com esse processo.

## Identidades suportadas {#supported-identities}

[!DNL Index] dá suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

Observe que os destinos [!DNL Index Exchange] oferecem suporte a apenas um tipo de identidade por upload. Especifique o tipo de identificador apropriado ao configurar os detalhes de destino (consulte a seção [&quot;Preencher detalhes de destino&quot;](#destination-details) abaixo).

Para carregar vários tipos de identidade, crie instâncias separadas do destino [!DNL Index Exchange] para cada tipo de identidade.

| Identidade de destino | Descrição | Considerações |
| --- | --- | --- |
| GAID | GOOGLE ADVERTISING ID | Se a identidade de origem for um namespace GAID, selecione GAID como a identidade de destino. |
| IDFA | Apple ID para anunciantes | Se a identidade de origem for um namespace IDFA, selecione a identidade de destino do IDFA. |
| Windows AID | Windows Advertising ID | Se a identidade de origem for um namespace do Windows AID, selecione a identidade de destino do Windows AID. |
| extern_id | IDs de usuário personalizadas | Se a identidade de origem for um namespace personalizado, selecione essa identidade de destino. |

{style="table-layout:auto"}

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção explica quais tipos de público-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
| --------- | ---------- | ---------- |
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo [Serviço de Segmentação](../../../segmentation/home.md) da Experience Platform. |
| Uploads personalizados | ✓ | Públicos [importados](../../../segmentation/ui/overview.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
| --------- | ---------- | --------- | 
| Tipo de exportação | **[!UICONTROL Segment export]** | Exporta todos os membros de um segmento (público) com os identificadores (IDFA, GAID ou outros) usados no destino [!DNL Index Exchange]. |
| Frequência de exportação | **[!UICONTROL Batch]** | Exporta arquivos para plataformas downstream em intervalos de 3, 6, 8, 12 ou 24 horas. Leia mais sobre [destinos com base em arquivo de lote](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da **[!UICONTROL View Destinations]** e da **[!UICONTROL Manage Destinations]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Detalhes do destino](../../assets/catalog/advertising/index-exchange/destination-details.png)

* [!UICONTROL Name]: Digite um nome para ajudá-lo a reconhecer este destino mais tarde.
* [!UICONTROL Description]: insira uma descrição para ajudá-lo a identificar este destino mais tarde.
* [!UICONTROL Identifier Type]: Selecione o tipo de identificador fornecido pelo índice que corresponda ao identificador que você está enviando para [!DNL Index]. Consulte a tabela de tipos de identificadores compatíveis abaixo. Se não tiver certeza de qual tipo de identificador usar, contate o representante do [!DNL Index]. Para enviar vários tipos de identificadores, crie instâncias separadas desse destino.
* [!UICONTROL Account ID]: Digite sua ID de conta do [!DNL Index]. Não é o mesmo que a ID do editor. Se não tiver certeza sobre qual ID usar, contate o representante do [!DNL Index].

#### Tipos de identificador suportados

| Tipo de identificador | Descrição |
|------------------ | ------------- |
| [!DNL appbundle] | Pacote de aplicativos móveis |
| [!DNL contentid] | ID de conteúdo |
| [!DNL deviceid] | ID do dispositivo (por exemplo, IDFA, GAID, WAID etc.) |
| [!DNL ip] | Endereço IP |
| [!DNL postcode] | CEP/Código Postal |
| [!DNL url] | URL do site |
| [!DNL ppid_xxx] | Para obter identificadores PPID, entre em contato com o representante de conta do [!DNL Index Exchange] para obter assistência. |

{style="table-layout:auto"}

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para este destino. Selecione um ou mais alertas da lista para assinar notificações de status para seu fluxo de dados. Para obter mais informações, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).
Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL View Identity Graph]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Leia [Ativar dados de público-alvo para destinos de exportação de perfil em lote](/help/destinations/ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para esse destino.

### Mapear atributos e identidades {#map}

Selecionar campos de origem:

* Selecione um identificador (geralmente namespaces, como IDFA ou um namespace de ID personalizada). Deve corresponder ao Tipo de identificador selecionado ao configurar o destino. Por exemplo, ao usar o identificador do IDFA como um campo de origem, o destino deve ter sido configurado com o Tipo de identificador &quot;deviceid&quot;.

Selecionar campos de destino:

* Os nomes dos campos de destino são ignorados e não são importantes. O destino só se preocupa com o tipo de identificador que está sendo enviado, que é determinado pelo Tipo de identificador selecionado ao configurar o destino.

![Mapear atributos e identidades](../../assets/catalog/advertising/index-exchange/identity-mapping.png)

### Registrar segmentos com [!DNL Index] {#register-segments}

Antes ou depois de ativar os dados no destino, contate o representante do [!DNL Index] para registrar os segmentos que você planeja ativar. Seu representante fornecerá instruções sobre como registrar detalhes de segmento adicionais, incluindo nomes, IDs, descrições e preços, se aplicável.

## Dados exportados / Validar exportação de dados {#exported-data}

Quando o registro for concluído, os segmentos estarão disponíveis para direcionamento na sua conta do [!DNL Index]. Para confirmar se os dados estão sendo recebidos corretamente, contate o representante do [!DNL Index], que pode fornecer detalhes sobre o volume de dados de segmento recebidos.

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do Experience Platform estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como a Experience Platform fiscaliza a governança de dados, leia a [visão geral da Governança de dados](/help/data-governance/home.md).
