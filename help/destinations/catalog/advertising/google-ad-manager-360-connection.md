---
title: (Beta) [!DNL Google Ad Manager 360] conexão
description: O Google Ad Manager 360 é uma plataforma de veiculação de anúncios da Google que oferece aos editores meios de gerenciar a exibição de anúncios em seus sites, por meio de vídeos e aplicativos móveis.
exl-id: 3251145a-3e4d-40aa-b120-d79c8c9c7cae
source-git-commit: 4f57574bc17f43406df800358c7320372eb197d0
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 1%

---

# (Beta) [!DNL Google Ad Manager 360] conexão

## Visão geral {#overview}

O [!DNL Google Ad Manager 360] a conexão habilita o upload em lote para [!DNL publisher provided identifiers] (PPID) em [!DNL Google Ad Manager 360], via [!DNL Google Cloud Storage].

Para obter mais detalhes sobre como os identificadores fornecidos pelo editor funcionam no Google Ad Manager 360, consulte o [documentação oficial do Google](https://support.google.com/admanager/answer/2880055?hl=en).

>[!IMPORTANT]
>
>No momento, esse destino está na versão Beta e só está disponível para um número limitado de clientes. Para solicitar acesso à [!DNL Google Ad Manager 360] entre em contato com o representante do Adobe e forneça [!DNL IMS Organization ID].

O [!DNL Google Ad Manager 360] exportações de destino [!DNL CSV] arquivos para [!DNL Google Cloud Storage] balde. Depois de exportar o [!DNL CSV] arquivos, você deve importá-los para o [!DNL Google Ad Manager 360] conta.

## Especificações do destino {#specifics}

Observe os detalhes a seguir que são específicos para [!DNL Google Ad Manager 360] destinos.

* Públicos ativados são criados de forma programática na plataforma Google e preenchidos no arquivo CSV.

## Identidades suportadas {#supported-identities}

[!DNL This integration] O suporta a ativação de identidades descritas na tabela abaixo.

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | Selecione essa identidade de destino para enviar públicos para o [!DNL Google Ad Manager 360] |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, juntamente com os campos de esquema aplicáveis (por exemplo, seu PPID), conforme escolhido na tela selecionar atributos de perfil do [fluxo de trabalho de ativação de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Em lote]** | Destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos com base em arquivo em lote](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Pré-requisitos {#prerequisites}

### Lista de permissões {#allow-listing}

>[!NOTE]
>
>A lista de permissões é obrigatória antes de configurar a primeira [!DNL Google Ad Manager] no Platform. Verifique se o processo de lista de permissões descrito abaixo foi concluído por [!DNL Google] antes de criar um destino.

>[!IMPORTANT]
>
>A Google simplificou o processo para conectar plataformas externas de gerenciamento de público-alvo ao Google Ad Manager 360. Agora você pode passar pelo processo de vinculação ao Google Ad Manager 360 de maneira automatizada. Ler [Segmentos de plataformas de gerenciamento de dados](https://support.google.com/admanager/answer/3289669?hl=en) na documentação do Google. Você deve ter as IDs listadas abaixo à mão.

* **ID da conta**: ID da conta do Adobe com Google. ID da conta: 87933855.
* **Customer ID**: ID da conta do cliente do Adobe com Google. ID do cliente: 89690775.
* **Código de rede**: Este é o seu [!DNL Google Ad Manager] identificador de rede, encontrado em **[!UICONTROL Administração > Configurações globais]** na interface do Google, bem como no URL.
* **ID do link de público-alvo**: Esse é um identificador específico associado ao [!DNL Google Ad Manager] rede (não sua [!DNL Network code]), também encontrado em **[!UICONTROL Administração > Configurações globais]** na interface do Google.
* Seu tipo de conta. DFP por Google ou comprador AdX.

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para destino {#authenticate}

Para autenticar para o destino, preencha os campos obrigatórios e selecione **[!UICONTROL Ligar ao destino]**.

* **[!UICONTROL ID da chave de acesso]**: Uma sequência de 61 caracteres alfanuméricos usada para autenticar o [!DNL Google Cloud Storage] para a Platform.
* **[!UICONTROL Chave de acesso secreta]**: Uma string codificada em 40 caracteres, base e 64, usada para autenticar seu [!DNL Google Cloud Storage] para a Platform.

Para obter mais informações sobre esses valores, consulte o [Chaves HMAC do Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guia. Para obter etapas sobre como gerar sua própria ID de chave de acesso e chave de acesso secreta, consulte [[!DNL Google Cloud Storage] visão geral da fonte](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Preencha os detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: Preencha o nome preferencial para esse destino.
* **[!UICONTROL Descrição]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Nome do bucket]**: Insira o nome do [!DNL Google Cloud Storage] bucket a ser usado por este destino.
* **[!UICONTROL Caminho da pasta]**: Insira o caminho para a pasta de destino que hospedará os arquivos exportados.

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
