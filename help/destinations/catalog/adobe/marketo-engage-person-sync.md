---
title: Sincronização de pessoas do Marketo Engage
description: Use o conector de sincronização de pessoas do Marketo Engage para transmitir atualizações do público-alvo de uma pessoa para os registros correspondentes no seu Marketo Engage.
last-substantial-update: 2025-01-14T00:00:00Z
badgeBeta: label="Beta" type="Informative"
exl-id: 2c909633-b169-4ec8-9f58-276395cb8df2
source-git-commit: 7d9f06f77f2265f3ae62542fd7fc1bd09d34d078
workflow-type: tm+mt
source-wordcount: '1127'
ht-degree: 3%

---

# Conexão de Sincronização da Pessoa do Marketo Engage {#marketo-engage-person-sync}

>[!IMPORTANT]
>
>Este conector de destino está na versão beta e só está disponível para clientes selecionados. Para solicitar acesso, entre em contato com o representante da Adobe.

>[!IMPORTANT]
>
>O cartão de destino da **[!UICONTROL Sincronização de pessoa do Marketo Engage]** será descontinuado em **outubro de 2025**.
>
>Para garantir uma transição suave para o novo destino do **[[!UICONTROL Marketo Engage]](marketo-engage-connection.md)**, analise os seguintes pontos principais e ações necessárias:
>
>* Todos os usuários devem **parar de usar o destino da Sincronização de Pessoas do Marketo Engage** e migrar para o novo destino do **[[!UICONTROL Marketo Engage]](marketo-engage-connection.md)** até outubro de 2025.
>* **Os fluxos de dados existentes não serão migrados automaticamente.** Você deve [configurar uma nova conexão](marketo-engage-connection.md#connect-to-the-destination) com o novo destino **[!UICONTROL Marketo Engage]** e ativar seus públicos lá.


## Visão geral {#overview}

Use o conector de sincronização de pessoas do Marketo Engage para transmitir atualizações dos públicos-alvo de pessoas para os registros correspondentes na sua instância do Marketo Engage.

>[!IMPORTANT]
> 
>O [Conector de sincronização de público-alvo do Marketo V2](/help/destinations/catalog/adobe/marketo-engage.md) não deve ser usado no modo de criação juntamente com o Conector de sincronização de atualização de perfil

## Identidades e atributos compatíveis {#support-identities-and-attributes}

### Identidades suportadas {#supported-identities}

| Identidade de destino | Descrição |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Email | Um namespace que representa um endereço de email. Esse tipo de namespace é frequentemente associado a uma única pessoa e, portanto, pode ser usado para identificá-la em diferentes canais. |

{style="table-layout:auto"}

### Atributos suportados {#supported-attributes}

Você pode mapear atributos do Experience Platform para qualquer um dos atributos aos quais sua organização tem acesso no Marketo. No Marketo, você pode usar a solicitação [Descrever API](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_6) para recuperar os campos de atributo aos quais sua organização tem acesso.

## Públicos-alvo suportados {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
| -------------------- | :-------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Serviço de segmentação | ✓ | Públicos-alvo gerados pelo [Serviço de Segmentação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/home) da Experience Platform. |
| Uploads personalizados | ✓ | Públicos importados para o Experience Platform de arquivos CSV. |

## Tipo e frequência de exportação {#export-type-and-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
| ---------------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Frequência de exportação | Transmissão | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil for atualizado no Experience Platform com base na avaliação do público-alvo, o conector enviará a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Configurar destino {#set-up-destination}

>[!IMPORTANT]
>
>* Para se conectar ao destino, você precisa de **[!UICONTROL Exibir Destinos]** e **[!UICONTROL Gerenciar Destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions).

Se sua empresa tiver acesso a várias organizações, certifique-se de usar a mesma organização na Marketo Engage e no Real-Time CDP, onde você está configurando o conector de destino para o Marketo.  Se você já tiver configurado um destino, poderá selecionar uma conta existente do Marketo para usar com sua nova configuração.  Caso contrário, clique no prompt Conector para destino, que permitirá definir o nome, a descrição e a Marketo Munchkin ID do destino desejado.  A Munchkin ID da sua instância do Marketo pode ser encontrada no menu Admin->Munchkin.

>[!IMPORTANT]
>
>O usuário que configura o destino deve ter a permissão [Editar Pessoa](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/descriptions-of-role-permissions#access-database) na instância e partição do Marketo.

![Conectar ao Destino](../../assets/catalog/adobe/marketo-engage-person-sync/connect-to-destination.png)

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar este destino no futuro.
* **[!UICONTROL Munchkin ID]**: a Munchkin ID é o identificador exclusivo de uma instância específica do Marketo.
* **[!UICONTROL Partição]**: um conceito no Marketo Engage usado para separar registros de cliente potencial por preocupação comercial
* **[!UICONTROL Primeiro campo pesquisável]**: campo no qual desduplicar. O campo deve estar presente em cada registro de cliente potencial da entrada. O padrão é email
* **[!UICONTROL Primeiro campo pesquisável]**: um campo secundário para desduplicar. O campo deve estar presente em cada registro de cliente potencial da entrada. Opcional

Depois de selecionar a instância, também será necessário selecionar a Partição de lead à qual deseja que a configuração se integre. Uma [Partição de Cliente Potencial](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/workspaces-and-person-partitions/understanding-workspaces-and-person-partitions) é um conceito no Marketo Engage usado para separar registros de cliente potencial por preocupação comercial, como uma marca ou uma região de vendas. Se sua assinatura do Marketo não tiver o recurso Espaços de trabalho e partições ou se nenhuma partição adicional tiver sido criada em sua assinatura, somente a partição Padrão estará disponível. Uma única configuração só pode atualizar registros de cliente potencial que existam em sua partição configurada.

>[!IMPORTANT]
> 
>Depois que um público-alvo é ativado para o destino do Marketo pela primeira vez, o preenchimento retroativo de perfis que já existiam no público-alvo antes da ativação do destino do Marketo pode levar *até 24 horas*. A partir de agora, sempre que perfis forem adicionados ao público, eles serão adicionados ao Marketo imediatamente.

### Campos de desduplicação {#deduplication-fields}

Ao enviar atualizações para o envolvimento do Marketo, os registros são selecionados com base na partição selecionada e em um ou dois campos selecionados pelo usuário. Se o destino estiver configurado com a partição da América do Norte e tiver Endereço de email e Nome da empresa configurados como campos de desduplicação, todos os três campos deverão corresponder para aplicar alterações a um registro existente. Por exemplo:

* O destino está configurado com a partição da América do Norte
* Pessoa com Email <test@example.com> e Nome da empresa Example Inc. no Experience Platform corresponde ao público de destino
* A menos que um registro com esses valores já exista na partição da América do Norte no Marketo, um novo registro de cliente potencial será criado

Se nenhum registro de cliente potencial correspondente for encontrado, um novo registro será criado.

![Detalhes do destino](../../assets/catalog/adobe/marketo-engage-person-sync/destination-details.png)

## Ativar públicos-alvo {#activate-audiences}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa de **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Ativar Destinos]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Leia [Ativar perfis e segmentos para destinos de exportação de segmento de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público para este destino.

Na etapa Ativar públicos-alvo, você poderá selecionar entre qualquer público-alvo de pessoa que esteja visível para você.

![Ativar públicos-alvo](../../assets/catalog/adobe/marketo-engage-person-sync/activate-audiences.png)

## Mapeamento de campos {#field-mapping}

Para que as alterações em um atributo de pessoa específico sejam enviadas para o Marketo Engage, o campo deve ser mapeado de um campo do Real-Time CDP para o campo do Marketo.

![Mapeamento de campos](../../assets/catalog/adobe/marketo-engage-person-sync/field-mapping.png)

Os tipos de dados do Experience Platform e do Marketo podem ser mapeados das seguintes maneiras:

| Tipo de dados do Experience Platform | Tipo de dados do Marketo |
| ----------------------------- | ------------------------------------ |
| String | String, Área De Texto, Url, Telefone, Email |
| Enumeração | String |
| Data | Data |
| Data e hora | Data e hora |
| Número inteiro | Número inteiro |
| Curto | Número inteiro |
| Longo | Ponto flutuante |
| Duplo | Moeda, Flutuante, Porcentagem |
| Booleano | Booleano |
| Matriz | Incompatível |
| Objeto | Incompatível |
| Mapa | Incompatível |
| Byte | Incompatível |

{style="table-layout:auto"}

Em alguns casos, é desejável permitir integrações para definir o valor de um campo, se não houver nenhum, enquanto impede que integrações façam atualizações em campos que já têm um valor.  Se você precisar impedir que o conector de destino substitua valores existentes na instância do Marketo Engage, poderá configurar campos para bloquear atualizações na seção Admin->Gerenciamento de campo da instância do Marketo e alternar o tipo de origem do Adobe Experience Platform.

![Bloquear Atualizações de Campo](../../assets/catalog/adobe/marketo-engage-person-sync/block-field-updates.png)

![Bloquear Atualizações de Campo](../../assets/catalog/adobe/marketo-engage-person-sync/block-field-updates-2.png)

## Uso e governança de dados {#data-usage-and-governance}

Todos os destinos do Adobe Experience Platform estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como a Adobe Experience Platform impõe a governança de dados, consulte a [visão geral da governança de dados](/help/data-governance/home.md).
