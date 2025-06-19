---
title: Configurar alertas e inclui na lista de permissões de IP para o CMK do Azure
description: Saiba como incluir na lista de permissões o endereço IP estático da Adobe no Cofre de Chaves do Azure e entender como os alertas da Experience Platform ajudam a detectar e resolver problemas de acesso de Chave gerenciada pelo cliente.
source-git-commit: 719273798954b70460c77711ef5eda5f9d22cdb0
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 1%

---

# Configurar alertas e inclui na lista de permissões de IP para [!DNL Azure] CMK

Para melhorar a transparência, o Adobe fornece um [serviço de monitoramento](../../../../observability/alerts/ui.md){target="_blank"} que verifica o status de acesso do cofre de chaves e aciona alertas em caso de problemas. Esses alertas ajudam você a responder rapidamente e evitar interrupções do serviço. Para ativar esse serviço, execute a inclui na lista de permissões do endereço IP estático da Adobe.

>[!IMPORTANT]
>
>Se você tiver desabilitado o acesso à rede pública ou configurado o Cofre da Chave do [!DNL Azure] para permitir somente redes selecionadas, será necessário adicionar o endereço IP estático da Adobe ao seu arquivo de inclui na lista de permissões. Sem ele, você pode não ser notificado de problemas de acesso que poderiam afetar sua instância do Experience Platform.

## Incluir na lista de permissões IP estático da Adobe no Cofre de Chaves [!DNL Azure] {#add-adobe-static-ip}

Para habilitar esses alertas enquanto mantém as restrições de rede, navegue até **[!DNL Azure Key Vault]** > **[!DNL Networking settings]**. Na guia **[!DNL Firewalls and virtual networks]**, selecione **[!DNL Allow public access from specific virtual networks and IP addresses]**.

A tela de configurações de Rede do Cofre de Chaves ![[!DNL Azure] mostrando onde adicionar o endereço IP estático da Adobe e com a opção Permitir acesso de realçada.](../../../images/governance-privacy-security/customer-managed-keys/key-vault-networking-settings.png)

### Endereço IP estático da Adobe

>[!IMPORTANT]
>
>O endereço IP estático fornecido pela Adobe é: `20.88.123.53`.

Em seguida, na seção **[!DNL Firewall]**, selecione **[!DNL Add your current IP address]** e substitua-o pelo endereço IP estático do Adobe. Incluir na lista de permissões Todas as conexões de saída são tratadas como ambientes de produção, portanto, esse endereço IP estático deve ser para garantir acesso ininterrupto ao cofre de chaves em configurações de rede restritas.

>[!NOTE]
>
>Depois de adicionar ou atualizar o endereço IP estático nas configurações do Cofre de Chaves do [!DNL Azure], aguarde até 10 minutos para que a alteração entre em vigor. Depois que o IP for adicionado, o aplicativo CMK acessará o cofre de chaves para verificar as permissões.

Depois de ➡ incluir na lista de permissões o IP estático da Adobe, o Experience Platform pode monitorar o acesso ao seu cofre de chaves e acionar alertas se surgirem problemas. Esses alertas fornecem avisos antecipados para que você possa agir antes que o serviço seja afetado. A próxima seção detalha os tipos de alertas que você pode receber e como responder.

## Monitorar alertas {#monitor-alerts}

Os alertas da plataforma notificam você sobre problemas que podem interromper o acesso à chave, como **[!UICONTROL falha de acesso à chave]** ou **[!UICONTROL desativação de chave]**. Esses alertas ajudam a identificar problemas rapidamente, como IP estático removido ou firewall mal configurado. Para restaurar o acesso, revise as configurações do firewall do [!DNL Azure] e adicione novamente o endereço IP necessário.

<!-- For a complete list of alert types and recommended resolutions, see the [CMK alert resolution reference](../alert-resolution-reference.md). -->

Assine as notificações de eventos do Adobe I/O para receber alertas em tempo real nas ferramentas de monitoramento. Para obter instruções de instalação, consulte [Assinar notificações de eventos Adobe I/O](../../../../observability/alerts/subscribe.md). Você também pode consultar o [guia da interface do usuário de alertas](../../../../observability/alerts/ui.md) para saber como visualizar e gerenciar alertas no Experience Platform.

## Próximas etapas

Incluir na lista de permissões Agora você configurou o monitoramento de IP e de alertas para o Cofre de Chaves do [!DNL Azure]. Para concluir a configuração das Chaves gerenciadas pelo cliente no [!DNL Azure], siga estes guias de configuração.

- [Configurar um [!DNL Azure] Cofre de Chaves](./azure-key-vault-config.md)
- [Usar a API para configurar o CMK](./api-set-up.md)
- [Use a interface do usuário para configurar o CMK](./ui-set-up.md)
