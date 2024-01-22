---
title: Conector do perfil Pega
description: Use o Conector de perfil Pega para Amazon S3 no Adobe Experience Platform para exportar dados de perfil completos ou incrementais, ou ambos, para o armazenamento em nuvem do Amazon S3. No Pega Customer Decision Hub, os trabalhos de dados podem ser agendados no Customer Profile Designer para importar dados do perfil periodicamente do armazenamento do Amazon S3.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: f422f21b-174a-4b93-b05d-084b42623314
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '1115'
ht-degree: 3%

---

# Conector do perfil Pega

## Visão geral {#overview}

Use o [!DNL Pega Profile Connector] no Adobe Experience Platform para criar uma conexão de saída ativa com o seu [!DNL Amazon Web Services] (AWS) Armazenamento S3 para exportar periodicamente dados de perfil para arquivos CSV do Adobe Experience Platform em seus próprios buckets S3. No [!DNL Pega Customer Decision Hub], você pode agendar processos para importar esses dados de perfil do armazenamento S3 para atualizar o perfil do [!DNL Pega Customer Decision Hub].

Esse conector ajuda a configurar a exportação inicial de dados de perfil e também ajuda a sincronizar novos perfis periodicamente no [!DNL Pega Customer Decision Hub].  Ter dados atualizados no Hub de decisão do cliente fornece uma visualização melhor e atualizada da base de clientes para a tomada de decisões de próxima ação.

>[!IMPORTANT]
>
>Esse conector de destino e a página de documentação são criados e mantidos pela Pegasystems. Para qualquer consulta ou pedido de atualização, entre em contato diretamente com Pega [aqui](mailto:support@pega.com).

## Casos de uso

Para ajudá-lo a entender melhor como e quando você deve usar o [!DNL Pega Profile Connector] destino, aqui estão exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso 1

Um profissional de marketing deseja configurar inicialmente [!DNL Pega Customer Decision Hub] com dados de perfil carregados do Adobe Experience Platform. Essa é uma carga total inicial seguida por cargas delta programadas.

### Caso de uso 2

Um profissional de marketing quer dados de perfil atualizados do Adobe Experience Platform disponíveis em [!DNL Pega Customer Decision Hub] que aprimora os insights de Pega sobre perfis de clientes de forma contínua.

## Pré-requisitos {#prerequisites}

Antes de usar esse destino para exportar dados do Adobe Experience Platform e importar perfis para o [!DNL Pega Customer Decision Hub], conclua os seguintes pré-requisitos:

* Configurar [!DNL Amazon S3] e o caminho da pasta a ser usada para exportação e importação de arquivos de dados.
* Configure o [!DNL Amazon S3] chave de acesso e [!DNL Amazon S3] chave secreta: Em [!DNL Amazon S3], gerar um `access key - secret access key` emparelhe para conceder acesso à Platform ao seu [!DNL Amazon S3] conta.
* Para conectar e exportar dados para o seu [!DNL Amazon S3] local de armazenamento, crie um usuário do Identity and Access Management (IAM) para [!DNL Platform] in [!DNL Amazon S3] e atribuir permissões, como `s3:DeleteObject`, `s3:GetBucketLocation`, `s3:GetObject`, `s3:ListBucket`, `s3:PutObject`, `s3:ListMultipartUploadParts`
* Verifique se o [!DNL Pega Customer Decision Hub] A instância foi atualizada para a versão 8.8 ou superior.

## Identidades suportadas {#supported-identities}

[!DNL Pega Customer Decision Hub] O é compatível com a ativação de IDs de usuário personalizadas descritas na tabela abaixo. Para obter mais detalhes, consulte [identidades](/help/identity-service/namespaces.md).

| Identidade de destino | Descrição |
|---|---|
| *CustomerID* | Identificador de usuário comum que identifica exclusivamente um perfil no [!DNL Pega Customer Decision Hub] e ADOBE EXPERIENCE PLATFORM |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, juntamente com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos de perfil da [workflow de ativação de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Lote]** | Os destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos baseados em arquivo em lote](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Exibir destinos]** e **[!UICONTROL Gerenciar destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow da configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Conectar ao destino]**.

* **[!DNL Amazon S3]chave de acesso** e **[!DNL Amazon S3]chave secreta**: Em [!DNL Amazon S3], gerar um `access key - secret access key` emparelhe para conceder acesso à Adobe Experience Platform ao seu [!DNL Amazon S3] conta. Saiba mais na [Documentação do Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Preencher detalhes do destino {#destination-details}

Depois de estabelecer a conexão de autenticação com o [!DNL Amazon S3], forneça as seguintes informações para o destino:

![Imagem da tela da interface do usuário mostrando campos preenchidos para os detalhes de destino do Conector de perfil Mega](../../assets/catalog/personalization/pega-profile/pega-profile-connect-destination.png)

Para configurar detalhes para o destino, preencha os campos obrigatórios e selecione **[!UICONTROL Próxima]**. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: digite um nome que ajudará a identificar esse destino.
* **[!UICONTROL Descrição]**: digite uma descrição desse destino.
* **[!UICONTROL Nome do bloco]**: digite o nome do [!DNL Amazon S3] bucket a ser usado por esse destino.
* **[!UICONTROL Caminho da pasta]**: digite o caminho para a pasta de destino que hospedará os arquivos exportados.
* **[!UICONTROL Tipo de compactação]**: selecione o tipo de compactação como GZIP ou NONE.

>[!TIP]
>
>No workflow de destino de conexão, é possível criar uma pasta personalizada no armazenamento Amazon S3 por arquivo de público exportado. Ler [Usar macros para criar uma pasta no local de armazenamento](/help/destinations/catalog/cloud-storage/overview.md#use-macros) para obter instruções.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar os dados, é necessário **[!UICONTROL Exibir destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisará do **[!UICONTROL Exibir gráfico de identidade]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos."){width="100" zoomable="yes"}

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

### Mapear atributos e identidades {#map}

No **[!UICONTROL Mapeamento]** etapa, você pode selecionar quais campos de atributo e identidade serão exportados para seus perfis. Você também pode optar por alterar os cabeçalhos no arquivo exportado para qualquer nome amigável. Para obter mais informações, consulte [etapa de mapeamento](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) no tutorial ativar interface do usuário de destinos em lote.

## Validar exportação de dados {#exported-data}

Para [!DNL Pega Profile Connector] destinos, [!DNL Platform] cria um `.csv` arquivo no local de armazenamento do Amazon S3 fornecido. Para obter mais informações sobre os arquivos, consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) no tutorial de ativação de público-alvo.

Uma importação bem-sucedida de dados de perfil do S3 insere dados no [!DNL Pega Customer] armazenamento de dados do perfil. Os dados importados do perfil do cliente podem ser validados no [!DNL Pega Customer Profile Designer] , conforme mostrado na figura a seguir.
![Imagem da tela da interface do usuário na qual você pode validar os dados de perfil do Adobe no Designer de perfil do cliente](../../assets/catalog/personalization/pega-profile/pega-profile-data.png)

Entrada [!DNL Pega Customer Decision Hub], os administradores de dados podem configurar trabalhos de dados no [!DNL Customer Profile Designer] para importar dados de perfil periodicamente do S3, conforme mostrado na figura a seguir. Consulte a [recursos adicionais](#additional-resources) para obter mais informações sobre como configurar trabalhos de dados para importar dados de perfil do [!DNL Amazon S3].
![Imagem da tela da interface do usuário para configurar trabalhos de dados no Designer de perfil do cliente](../../assets/catalog/personalization/pega-profile/pega-profile-screen-image1.png)

## Recursos adicionais {#additional-resources}

Consulte [Importar trabalhos de dados](https://academy.pega.com/topic/import-data-jobs/v1) in [!DNL Pega Customer Decision Hub].

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, consulte o [Visão geral da governança de dados](/help/data-governance/home.md).
