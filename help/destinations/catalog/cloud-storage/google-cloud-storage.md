---
title: Conexão do Google Cloud Storage
description: Saiba como se conectar ao Google Cloud Storage e ativar públicos ou exportar conjuntos de dados.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: ab274270-ae8c-4264-ba64-700b118e6435
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 2%

---

# [!DNL Google Cloud Storage] conexão

## Visão geral {#overview}

Crie uma conexão de saída ativa com o [!DNL Google Cloud Storage] para exportar arquivos de dados do Adobe Experience Platform periodicamente para seus próprios buckets.

## Conectar-se ao armazenamento do [!DNL Google Cloud Storage] por meio da API ou da interface {#connect-api-or-ui}

* Para se conectar ao local de armazenamento do [!DNL Google Cloud Storage] usando a interface do usuário do Experience Platform, leia as seções [Conectar-se ao destino](#connect) e [Ativar públicos-alvo para este destino](#activate) abaixo.
* Para se conectar ao local de armazenamento do [!DNL Google Cloud Storage] de forma programática, leia o [Tutorial da API do Serviço de Fluxo](../../api/activate-segments-file-based-destinations.md) para ativar públicos-alvo para destinos baseados em arquivo.

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo [Serviço de Segmentação](../../../segmentation/home.md) da Experience Platform. |
| Uploads personalizados | ✓ | Públicos [importados](../../../segmentation/ui/audience-portal.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Profile-based]** | Você está exportando todos os membros de um segmento, juntamente com os campos de esquema aplicáveis, conforme escolhido na tela selecionar atributos de perfil do [fluxo de trabalho de ativação de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Batch]** | Os destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos com base em arquivo de lote](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Exportar conjuntos de dados {#export-datasets}

Esse destino suporta exportações de conjunto de dados. Para obter informações completas sobre como configurar exportações de conjunto de dados, leia os tutoriais:

* Como [exportar conjuntos de dados usando a interface do usuário do Experience Platform](/help/destinations/ui/export-datasets.md).
* Como [exportar conjuntos de dados de forma programática usando a API de Serviço de Fluxo](/help/destinations/api/export-datasets.md).

## Formato de arquivo dos dados exportados {#file-format}

Ao exportar *dados de público-alvo*, o Experience Platform cria um arquivo `.csv`, `parquet` ou `.json` no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte a seção [formatos de arquivo compatíveis com a exportação](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) no tutorial de ativação de público-alvo.

Ao exportar *conjuntos de dados*, o Experience Platform cria um arquivo `.parquet` ou `.json` no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte a seção [verificar exportação bem-sucedida do conjunto de dados](../../ui/export-datasets.md#verify) no tutorial exportar conjuntos de dados.

## Pré-requisito de configuração para conectar sua conta do [!DNL Google Cloud Storage] {#prerequisites}

Para conectar o Experience Platform ao [!DNL Google Cloud Storage], primeiro você deve habilitar a interoperabilidade para sua conta [!DNL Google Cloud Storage]. Para acessar a configuração de interoperabilidade, abra o [!DNL Google Cloud Platform] e selecione **[!UICONTROL Settings]** na opção **[!UICONTROL Cloud Storage]** no painel de navegação.

![Painel da Google Cloud Platform com Armazenamento na Nuvem e Configurações realçados.](../../../sources/images/tutorials/create/google-cloud-storage/nav.png)

A página **[!UICONTROL Settings]** é exibida. Aqui, você pode ver informações sobre sua ID de projeto do [!DNL Google] e detalhes sobre sua conta do [!DNL Google Cloud Storage]. Para acessar as configurações de interoperabilidade, selecione **[!UICONTROL Interoperability]** no cabeçalho superior.

![A guia Interoperabilidade destacada no painel da Google Cloud Platform.](../../../sources/images/tutorials/create/google-cloud-storage/project-access.png)

A página **[!UICONTROL Interoperability]** contém informações sobre autenticação, chaves de acesso e o projeto padrão associado à sua conta de serviço. Para gerar uma nova ID de chave de acesso e uma chave de acesso secreta para sua conta de serviço, selecione **[!UICONTROL Create a Key for a Service Account]**.

![A opção Criar uma chave para um controle de conta de serviço realçado no painel da Google Cloud Platform.](../../../sources/images/tutorials/create/google-cloud-storage/interoperability.png)

Você pode usar a ID da chave de acesso recém-gerada e a chave de acesso secreta para conectar sua conta do [!DNL Google Cloud Storage] à Experience Platform.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa das **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](/help/destinations/ui/connect-destination.md). No workflow da configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Connect to destination]**.

* **[!UICONTROL Access key ID]**: uma sequência de 61 caracteres alfanuméricos usada para autenticar sua conta do [!DNL Google Cloud Storage] no Experience Platform. Para obter informações sobre como obter este valor, leia a seção [pré-requisitos](#prerequisites) acima.
* **[!UICONTROL Secret access key]**: uma cadeia de caracteres de 40 caracteres codificada em base64 usada para autenticar sua conta do [!DNL Google Cloud Storage] no Experience Platform. Para obter informações sobre como obter este valor, leia a seção [pré-requisitos](#prerequisites) acima.
* **[!UICONTROL Encryption key]**: Opcionalmente, você pode anexar sua chave pública formatada em RSA para adicionar criptografia aos seus arquivos exportados. Veja um exemplo de uma chave de criptografia formatada corretamente na imagem abaixo.

  ![Imagem mostrando um exemplo de uma chave PGP formatada corretamente na interface](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

Para obter mais informações sobre esses valores, leia o [guia de chaves HMAC do Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Para obter etapas sobre como gerar sua própria ID da chave de acesso e chave de acesso secreta, consulte a [[!DNL Google Cloud Storage] visão geral da origem](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Name]**: Preencha o nome preferencial para este destino.
* **[!UICONTROL Description]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Bucket name]**: insira o nome do bucket [!DNL Google Cloud Storage] a ser usado por este destino.
* **[!UICONTROL Folder path]**: Insira o caminho para a pasta de destino que hospedará os arquivos exportados.
* **[!UICONTROL File type]**: Selecione o formato que o Experience Platform deve usar para os arquivos exportados. Ao selecionar a opção [!UICONTROL CSV], você também pode [configurar as opções de formatação de arquivo](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Compression format]**: Selecione o tipo de compactação que o Experience Platform deve usar para os arquivos exportados.
* **[!UICONTROL Include manifest file]**: ative esta opção se desejar que as exportações incluam um arquivo JSON de manifesto que contenha informações sobre o local de exportação, tamanho da exportação e muito mais. O manifesto é nomeado usando o formato `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Exibir um [arquivo de manifesto de exemplo](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). O arquivo de manifesto inclui os seguintes campos:
   * `flowRunId`: A [execução do fluxo de dados](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) que gerou o arquivo exportado.
   * `scheduledTime`: A hora em UTC quando o arquivo foi exportado.
   * `exportResults.sinkPath`: O caminho no local de armazenamento onde o arquivo exportado está depositado.
   * `exportResults.name`: O nome do arquivo exportado.
   * `size`: O tamanho do arquivo exportado, em bytes.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

### [!DNL Google Cloud Storage] permissões necessárias {#required-google-cloud-storage-permission}

Para conectar e exportar dados com êxito para o local de armazenamento do [!DNL Google Cloud Storage], você precisa das seguintes [!DNL Google Cloud Storage] permissões para seus buckets:

* `orgpolicy.policy.get`
* `resourcemanager.projects.get`
* `resourcemanager.projects.list`
* `storage.managedFolders.create`
* `storage.multipartUploads.abort`
* `storage.multipartUploads.create`
* `storage.multipartUploads.listParts`
* `storage.objects.create`
* `storage.objects.list`

Leia mais sobre [controle de acesso e permissões](https://cloud.google.com/storage/docs/access-control/iam-permissions) em [!DNL Google Cloud Storage].

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL View Identity Graph]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

### Agendamento

Na etapa **[!UICONTROL Scheduling]**, você pode [configurar o agendamento de exportação](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) para o seu destino [!DNL Google Cloud Storage] e também [configurar o nome dos seus arquivos exportados](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Mapear atributos e identidades {#map}

Na etapa **[!UICONTROL Mapping]**, você pode selecionar quais campos de atributo e identidade serão exportados para seus perfis. Você também pode optar por alterar os cabeçalhos no arquivo exportado para qualquer nome amigável. Para obter mais informações, exiba a [etapa de mapeamento](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) no tutorial de ativação da interface de destinos em lote.

## Validar exportação de dados bem-sucedida {#exported-data}

Para verificar se os dados foram exportados com êxito, verifique o bucket [!DNL Google Cloud Storage] e se os arquivos exportados contêm as populações de perfis esperadas.

## INCLUO NA LISTA DE PERMISSÕES de endereços IP {#ip-address-allow-list}

Consulte o artigo [incluo na lista de permissões de endereços IP](ip-address-allow-list.md) se precisar adicionar IPs do Adobe a um incluo na lista de permissões.