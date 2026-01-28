---
title: Editar destinos
type: Tutorial
description: Saiba como editar e atualizar contas de destinos existentes na interface do usuário do Adobe Experience Platform
exl-id: f3298836-668b-43fb-b4f3-85a650766f05
source-git-commit: f91551c460c7d6fd4f98111210f29cf16ec5b565
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Editar destinos

Saiba como editar vários componentes de uma conexão de destino existente, incluindo como atualizar credenciais de autenticação, exportar local e muito mais usando a interface do usuário do Experience Platform.

>[!NOTE]
>
> As operações de edição descritas neste tutorial também são compatíveis por meio de operações de API. Leia o tutorial sobre como [editar destinos na API](/help/destinations/api/edit-destination.md) para obter mais informações.

## Pré-requisitos {#prerequisites}

Para editar conexões de destino, você precisa da **[!UICONTROL Manage Destinations]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

## Editar conexões de destino {#edit}

Para editar vários componentes de uma conexão de destino existente:

1. Navegue até **[!UICONTROL Destinations]** > **[!UICONTROL Browse]**.
2. Selecione o destino desejado que deseja editar.
3. Selecione as reticências (`...`) na coluna [!UICONTROL Name] e use o controle ![Editar controle de destino ](/help/images/icons/edit.png)**[!UICONTROL Edit destination]**para editar conexões de destino existentes.
4. Na janela modal, edite as configurações desejadas. Selecione **[!UICONTROL Save]** quando terminar.

Na janela de edição do destino, é possível atualizar quaisquer configurações definidas ao se conectar inicialmente ao destino. Essas configurações são diferentes com base na plataforma de destino que você está atualizando.

Dependendo de como o destino foi configurado, alguns campos podem ser somente leitura e não podem ser editados. Para alterar o valor de campos somente leitura, você deve [criar uma nova conexão de destino](../ui/connect-destination.md) com os novos valores de campo.

![Captura de tela mostrando um campo somente leitura.](../assets/ui/edit-destinations/read-only.png)

Abaixo estão alguns exemplos das configurações que você pode atualizar para os destinos do [Amazon S3](../catalog/cloud-storage/amazon-s3.md), [Azure Event Hubs](../catalog/cloud-storage/azure-event-hubs.md) e [Google Ads](../catalog/advertising/google-ads-destination.md).

<div style="display: flex; gap: 12px; justify-content: flex-start; align-items: flex-start;">
  <img class="modal-image" src="../assets/ui/edit-destinations/edit-amazon-s3-connection.png" alt="Tela Editar destino do Amazon S3." style="max-width: 200px; height: auto; border: 1px solid #ccc;">
  <img class="modal-image" src="../assets/ui/edit-destinations/edit-eventhubs-connection.png" alt="Editar tela de destino para o destino do Azure EventHubs." style="max-width: 200px; height: auto; border: 1px solid #ccc;">
  <img class="modal-image" src="../assets/ui/edit-destinations/edit-google-ads-connection.png" alt="Tela Editar destino para o destino do Google Ads." style="max-width: 200px; height: auto; border: 1px solid #ccc;">
</div>

>[!SUCCESS]
>
>As configurações de conexão de destino foram atualizadas.

## Outras opções de edição

Ao usar a interface do usuário do Experience Platform ou a API do Serviço de fluxo, é possível editar várias configurações de destino, conforme detalhado nos links abaixo:

| Uso da interface do Experience Platform | Uso da API do Serviço de fluxo |
|---------|----------|
| Editar conexões de destino (esta página) | [Editar componentes de conexão de destino (local de armazenamento e outros componentes)](/help/destinations/api/edit-destination.md#patch-target-connection) |
| [Editar contas](/help/destinations/ui/update-accounts.md) | [Editar componentes de conexão base (parâmetros de autenticação e outros componentes)](/help/destinations/api/edit-destination.md#patch-base-connection) |
| [Editar fluxos de dados de ativação](/help/destinations/ui/edit-activation.md) | [Atualizar fluxos de dados de destino](/help/destinations/api/update-destination-dataflows.md) |

## Próximas etapas

Ao seguir este tutorial, você usou com êxito o espaço de trabalho **[!UICONTROL destinations]** para atualizar as conexões de destino existentes.

Para obter mais informações sobre destinos, consulte a [visão geral sobre destinos](../catalog/overview.md).
