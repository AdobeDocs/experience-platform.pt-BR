---
title: (Beta) [!DNL Google Ad Manager 360] conexão
description: O Google Ad Manager 360 é uma plataforma de veiculação de anúncios da Google que oferece aos editores meios de gerenciar a exibição de anúncios em seus sites, por meio de vídeos e aplicativos móveis.
source-git-commit: 60ae86ed6e741bd7739086105bfe70952841d454
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 2%

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
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, junto com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos de perfil do [fluxo de trabalho de ativação de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Em lote]** | Destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos com base em arquivo em lote](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Pré-requisitos {#prerequisites}

### Lista de permissões {#allow-listing}

>[!NOTE]
>
>A lista de permissões é obrigatória antes de configurar a primeira [!DNL Google Ad Manager] no Platform. Verifique se o processo de lista de permissões descrito abaixo foi concluído por [!DNL Google] antes de criar um destino.

Antes de criar a [!DNL Google Ad Manager 360] no Platform, você deve entrar em contato com [!DNL Google] para que o Adobe seja colocado na lista de provedores de dados permitidos e para que sua conta seja adicionada à lista de permissões. Contato [!DNL Google] e fornecer as seguintes informações:

* **ID da conta**: ID da conta do Adobe com Google. ID da conta: 87933855.
* **Customer ID**: ID da conta do cliente do Adobe com Google. ID do cliente: 89690775.
* **ID de rede**: esta é a sua conta com [!DNL Google Ad Manager]
* **ID do link de público-alvo**: esta é a sua conta com [!DNL Google Ad Manager]
* Seu tipo de conta. DFP por Google ou comprador AdX.

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configuração](../../ui/connect-destination.md) nesse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: Preencha o nome preferencial para esse destino.
* **[!UICONTROL Descrição]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Nome do bucket]**: digite o nome do [!DNL Google Cloud Storage] bucket a ser usado por este destino.
* **[!UICONTROL Caminho da pasta]**: insira o caminho para a pasta de destino que hospedará os arquivos exportados.

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
