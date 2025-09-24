---
title: Suporte a link privado para origens na interface do usuário
description: Saiba como usar os Links privados do Azure para origens na interface do usuário do Experience Platform.
exl-id: 2882729e-2d46-48dc-9227-51dda5bf7dfb
source-git-commit: 4d82b0a7f5ae9e0a7607fe7cb75261e4d3489eff
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 0%

---

# Suporte a link privado para fontes na interface do usuário

>[!AVAILABILITY]
>
>Esse recurso é compatível com as seguintes fontes:
>
>* [[!DNL Azure Blob Storage]](../../connectors/cloud-storage/blob.md)
>* [[!DNL ADLS Gen2]](../../connectors/cloud-storage/adls-gen2.md)
>* [[!DNL Azure File Storage]](../../connectors/cloud-storage/azure-file-storage.md)
>
>No momento, o Suporte a links privados está disponível apenas para organizações que compraram o Adobe Healthcare Shield ou o Adobe Privacy &amp; Security Shield.

Você pode usar o recurso Links privados para criar endpoints privados para que suas fontes da Adobe Experience Platform se conectem ao. Conecte com segurança suas fontes a uma rede virtual usando endereços IP privados, eliminando a necessidade de IPs públicos e reduzindo sua superfície de ataque. Simplifique a configuração da rede, eliminando a necessidade de configurações complexas de firewall ou tradução de endereço de rede, garantindo que o tráfego de dados atinja apenas os serviços aprovados.

Leia este guia para saber como você pode usar o espaço de trabalho de origens na interface do usuário do Experience Platform para criar e usar um endpoint privado.

>[!BEGINSHADEBOX]

## Direito de uso de licença para suporte a link privado

As métricas de direito de uso de licença para suporte a links privados nas origens são as seguintes:

* Os clientes têm direito a até 2 TB por ano de transferência de dados por meio de fontes compatíveis ([!DNL Azure Blob Storage], [!DNL ADLS Gen2] e [!DNL Azure File Storage]), em todas as sandboxes e organizações.
* Cada organização pode ter no máximo 10 endpoints para todas as sandboxes de produção.
* Cada organização pode ter no máximo um terminal para todas as sandboxes de desenvolvimento.

>[!ENDSHADEBOX]

## Criar um ponto de extremidade privado

Para começar a usar Links Privados, navegue até o catálogo *[!UICONTROL Fontes]* da interface do usuário do Experience Platform e selecione **[!UICONTROL Pontos de extremidade privados]** no menu de guias no espaço de trabalho de fontes.

![O catálogo de fontes com &quot;Pontos de extremidade particulares&quot;.](../../images/tutorials/private-links/catalog.png)

Use a interface para exibir informações sobre pontos de extremidade privados existentes, como ID, fonte associada e status atual. Para criar um novo ponto de extremidade privado, selecione **[!UICONTROL Criar ponto de extremidade privado]**.

![A interface de pontos de extremidade Privados com &quot;Criar ponto de extremidade privado&quot; foi selecionada.](../../images/tutorials/private-links/private-endpoints.png)

Em seguida, escolha a origem desejada e insira valores para as seguintes propriedades:

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome do seu ponto de extremidade privado. |
| `subscriptionId` | A ID associada à sua assinatura do [!DNL Azure]. Para obter mais informações, leia o guia [!DNL Azure] em [recuperando sua assinatura e IDs de locatário de [!DNL Azure Portal]](https://learn.microsoft.com/en-us/azure/azure-portal/get-subscription-tenant-id). |
| `resourceGroupName` | O nome do seu grupo de recursos em [!DNL Azure]. Um grupo de recursos contém recursos relacionados para uma solução [!DNL Azure]. Para obter mais informações, leia o guia [!DNL Azure] em [gerenciando grupos de recursos](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal). |
| `resourceGroup` | O nome do recurso. Em [!DNL Azure], um recurso se refere a instâncias como máquinas virtuais, aplicativos Web e bancos de dados. Para obter mais informações, leia o guia [!DNL Azure] em [noções básicas sobre o [!DNL Azure] gerenciador de recursos](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview). |

{style="table-layout:auto"}

Quando terminar, selecione **[!UICONTROL Enviar]**.

![A janela de autenticação para criar um novo ponto de extremidade privado no espaço de trabalho da interface do usuário de fontes.](../../images/tutorials/private-links/create-private-endpoint.png)

### Aprovar um endpoint privado

Um endpoint recém-criado permanece em um estado pendente até ser aprovado por um administrador.

Para aprovar uma solicitação de ponto de extremidade privado para as fontes [!DNL Azure Blob] e [!DNL Azure Data Lake Gen2], faça logon no [!DNL Azure Portal]. Na navegação à esquerda, selecione **[!DNL Data storage]**, vá para a guia **[!DNL Security + networking]** e escolha **[!DNL Networking]**. Em seguida, selecione **[!DNL Private endpoints]** para ver uma lista de pontos de extremidade privados associados à sua conta e seus estados de conexão atuais. Para aprovar uma solicitação pendente, selecione o ponto de extremidade desejado e clique em **[!DNL Approve]**.

![O portal do Azure com uma lista de pontos de extremidade privados pendentes.](../../images/tutorials/private-links/azure.png)

## Criar uma conta com um ponto de extremidade privado

Navegue até o catálogo de origens e selecione uma origem que ofereça suporte a endpoints privados. Em seguida, crie uma nova conta com sua origem e, durante a autenticação da conta, selecione a opção **[!UICONTROL Ponto de extremidade privado]**. Forneça as credenciais de autenticação da origem e selecione **[!UICONTROL Conectar à origem]** Aguarde alguns minutos para que a conexão seja estabelecida.

>[!NOTE]
>
>Se a opção [!UICONTROL Ponto de extremidade privado] estiver habilitada, o Experience Platform verificará se existe um ponto de extremidade privado aprovado para a origem selecionada. Se nenhum endpoint aprovado for encontrado, você não poderá estabelecer uma conexão.

![A nova etapa de autenticação de conta com pontos de extremidade privados habilitada.](../../images/tutorials/private-links/new-account.png)

Em seguida, navegue até a interface [!UICONTROL Conta existente] da sua origem. Use essa interface para exibir uma lista das contas existentes e os status correspondentes. Você pode selecionar o ícone de filtro ![ícone de filtro](../../../images/icons/filter.png) para exibir apenas as contas que foram habilitadas para conexão com um ponto de extremidade privado.

![A interface de conta existente no fluxo de trabalho de origem exibe somente as contas filtradas que estão habilitadas para conexões de ponto de extremidade privado.](../../images/tutorials/private-links/existing-private-endpoints.png)

Selecione a conta que deseja usar e habilite a **[!UICONTROL Criação Interativa]**. Este botão de alternância ativa a [!UICONTROL Criação Interativa], um recurso [!DNL Azure] que permite testar conexões, procurar listas de pastas e visualizar dados. É necessário habilitar a [!UICONTROL Criação Interativa] para conexões de ponto de extremidade privado. Observe que não é possível desativar esse botão manualmente; ele é desativado automaticamente após 60 minutos.

A [!UICONTROL Criação interativa] leva alguns minutos para ser habilitada. Depois que a configuração estiver habilitada, selecione **[!UICONTROL Avançar]** para prosseguir para a próxima etapa e selecione os dados que deseja assimilar.

![Uma conta existente foi selecionada e a criação interativa está habilitada.](../../images/tutorials/private-links/interactive-authoring.png)

## Próximas etapas

Agora que você criou um endpoint privado com êxito, poderá criar conexões de origem e fluxos de dados e assimilar dados usando endpoints privados. Leia os guias a seguir para obter informações sobre como criar fluxos de dados na interface do usuário do:

* [Criar um fluxo de dados para uma fonte de armazenamento na nuvem](../ui/dataflow/batch/cloud-storage.md)
* [Criar um fluxo de dados para uma origem de banco de dados](../ui/dataflow/databases.md)
