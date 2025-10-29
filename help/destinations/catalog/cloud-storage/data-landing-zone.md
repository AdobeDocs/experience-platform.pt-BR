---
title: Destino da Data Landing Zone
description: Saiba como se conectar à Data Landing Zone para ativar públicos e exportar conjuntos de dados.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1976'
ht-degree: 2%

---

# Destino da Data Landing Zone

>[!IMPORTANT]
>
>Esta página de documentação se refere ao [!DNL Data Landing Zone] *destino*. Também há uma [!DNL Data Landing Zone] *origem* no catálogo de fontes. Para obter mais informações, leia a documentação de [[!DNL Data Landing Zone] origem](/help/sources/connectors/cloud-storage/data-landing-zone.md).


## Visão geral {#overview}

[!DNL Data Landing Zone] é uma interface de armazenamento em nuvem provisionada pela Adobe Experience Platform, que concede a você acesso a um recurso de armazenamento de arquivos seguro e baseado em nuvem para exportar arquivos do Experience Platform. Você tem acesso a um [!DNL Data Landing Zone] contêiner por sandbox, e o volume total de dados em todos os contêineres é limitado ao total de dados fornecidos com sua licença de Produtos e Serviços da Experience Platform. Todos os clientes do Experience Platform e seus aplicativos, como [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services] e [!DNL Real-Time Customer Data Platform], são provisionados com um contêiner [!DNL Data Landing Zone] por sandbox.

O Experience Platform impõe um TTL (time-to-live) rigoroso de sete dias em todos os arquivos carregados em um contêiner [!DNL Data Landing Zone]. Todos os arquivos são excluídos após sete dias.

O conector de destino [!DNL Data Landing Zone] está disponível para clientes que usam o suporte na nuvem do Azure ou do Amazon Web Service. O mecanismo de autenticação é diferente com base na nuvem em que o destino é provisionado, tudo sobre o destino e seus casos de uso são os mesmos. Leia mais sobre os dois mecanismos de autenticação diferentes nas seções [Autenticar na Zona de Aterrissagem de Dados provisionada no Blob do Azure](#authenticate-dlz-azure) e [Autenticar na Zona de Aterrissagem de Dados provisionada pela AWS](#authenticate-dlz-aws).

![Diagrama que mostra como a implementação do destino da Zona de Aterrissagem de Dados é diferente com base no suporte da nuvem.](/help/destinations/assets/catalog/cloud-storage/data-landing-zone/dlz-workflow-based-on-cloud-implementation.png "Implementação de destino da Zona de Aterrissagem de Dados pelo suporte à nuvem"){zoomable="yes"}

## Conectar-se ao armazenamento do [!UICONTROL Data Landing Zone] por meio da API ou da interface {#connect-api-or-ui}

* Para se conectar ao local de armazenamento do [!UICONTROL Data Landing Zone] usando a interface do usuário do Experience Platform, leia as seções [Conectar-se ao destino](#connect) e [Ativar públicos-alvo para este destino](#activate) abaixo.
* Para se conectar ao local de armazenamento do [!UICONTROL Data Landing Zone] de forma programática, leia o [Tutorial da API do Serviço de Fluxo](../../api/activate-segments-file-based-destinations.md) para ativar públicos-alvo para destinos baseados em arquivo.

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
| Tipo de exportação | **[!UICONTROL Profile-based]** | Você está exportando todos os membros de um segmento, juntamente com os campos de esquema aplicáveis (por exemplo, seu PPID), conforme escolhido na tela selecionar atributos de perfil do [fluxo de trabalho de ativação de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Batch]** | Os destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos com base em arquivo de lote](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Exportar conjuntos de dados {#export-datasets}

Esse destino suporta exportações de conjunto de dados. Para obter informações completas sobre como configurar exportações de conjunto de dados, leia os tutoriais:

* Como [exportar conjuntos de dados usando a interface do usuário do Experience Platform](/help/destinations/ui/export-datasets.md).
* Como [exportar conjuntos de dados de forma programática usando a API de Serviço de Fluxo](/help/destinations/api/export-datasets.md).

## Formato de arquivo dos dados exportados {#file-format}

Ao exportar *dados de público-alvo*, o Experience Platform cria um arquivo `.csv`, `parquet` ou `.json` no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte a seção [formatos de arquivo compatíveis com a exportação](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) no tutorial de ativação de público-alvo.

Ao exportar *conjuntos de dados*, o Experience Platform cria um arquivo `.parquet` ou `.json` no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte a seção [verificar exportação bem-sucedida do conjunto de dados](../../ui/export-datasets.md#verify) no tutorial exportar conjuntos de dados.

## Autenticar para a Zona de aterrissagem de dados provisionada no Blob do Azure {#authenticate-dlz-azure}

>[!AVAILABILITY]
>
>Esta seção se aplica às implementações do Experience Platform em execução no Microsoft Azure. Para saber mais sobre a infraestrutura do Experience Platform compatível, consulte a [visão geral da nuvem múltipla do Experience Platform](https://experienceleague.adobe.com/pt-br/docs/experience-platform/landing/multi-cloud).

Você pode ler e gravar arquivos no seu contêiner por meio do [!DNL Azure Storage Explorer] ou da interface de linha de comando.

O [!DNL Data Landing Zone] oferece suporte à autenticação baseada em SAS e seus dados estão protegidos com mecanismos de segurança de armazenamento [!DNL Azure Blob] padrão em repouso e em trânsito. SAS significa [assinatura de acesso compartilhado](https://learn.microsoft.com/en-us/azure/ai-services/translator/document-translation/how-to-guides/create-sas-tokens?tabs=Containers).

Para proteger seus dados em uma conexão pública com a Internet, use a autenticação baseada em SAS para acessar com segurança o contêiner [!DNL Data Landing Zone]. Não há alterações de rede necessárias para você acessar o contêiner [!DNL Data Landing Zone], o que significa que você não precisa definir nenhuma configuração de lista de permissões ou entre regiões para sua rede.

### Conectar seu contêiner do [!DNL Data Landing Zone] a [!DNL Azure Storage Explorer]

Você pode usar o [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/products/storage/storage-explorer/) para gerenciar o conteúdo do seu contêiner [!DNL Data Landing Zone]. Para começar a usar o [!DNL Data Landing Zone], primeiro você deve recuperar suas credenciais, inseri-las no [!DNL Azure Storage Explorer] e conectar seu contêiner do [!DNL Data Landing Zone] ao [!DNL Azure Storage Explorer].

Na interface do usuário do [!DNL Azure Storage Explorer], selecione o ícone de conexão na barra de navegação esquerda. A janela **Selecionar Recurso** é exibida, fornecendo opções para conexão. Selecione **[!DNL Blob container]** para se conectar ao seu armazenamento [!DNL Data Landing Zone].

![Selecione o recurso realçado na interface do Azure.](/help/sources/images/tutorials/create/dlz/select-resource.png)

Em seguida, selecione **SAS (URL de assinatura de acesso compartilhado)** como seu método de conexão e selecione **Avançar**.

![Selecione o método de conexão realçado na interface do Azure.](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

Após selecionar o método de conexão, você deve fornecer um **nome para exibição** e a URL SAS do contêiner **[!DNL Blob]** que corresponda ao contêiner [!DNL Data Landing Zone].

>[!BEGINSHADEBOX]

### Recupere as credenciais para o seu [!DNL Data Landing Zone] {#retrieve-dlz-credentials}

Você deve usar as APIs do Experience Platform para recuperar suas credenciais do [!DNL Data Landing Zone]. A chamada à API para recuperar suas credenciais é descrita abaixo. Para obter informações sobre como obter os valores necessários para seus cabeçalhos, consulte o guia [Introdução às APIs do Adobe Experience Platform](/help/landing/api-guide.md).

**Formato da API**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination
```

| Parâmetros de consulta | Descrição |
| --- | --- |
| `dlz_destination` | O tipo `dlz_destination` permite que a API diferencie um contêiner de destino de zona de aterrissagem dos outros tipos de contêineres disponíveis para você. |

{style="table-layout:auto"}

**Solicitação**

O exemplo de solicitação a seguir recupera credenciais para uma zona de aterrissagem existente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Resposta**

A resposta a seguir retorna as informações de credencial da sua zona de aterrissagem, incluindo as `SASToken` e `SASUri` atuais, e a `storageAccountName` que corresponde ao seu contêiner de zona de aterrissagem.

```json
{
    "containerName": "dlz-destination",
    "SASToken": "sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3df123",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-destination?sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| Propriedade | Descrição |
| --- | --- |
| `containerName` | O nome da sua zona de destino. |
| `SASToken` | O token de assinatura de acesso compartilhado para sua zona de aterrissagem. Esta cadeia de caracteres contém todas as informações necessárias para autorizar uma solicitação. |
| `SASUri` | O URI de assinatura de acesso compartilhado para sua zona de aterrissagem. Essa string é uma combinação do URI para a zona de aterrissagem para a qual você está sendo autenticado e seu token SAS correspondente, |

{style="table-layout:auto"}

### Atualizar credenciais de [!DNL Data Landing Zone] {#update-dlz-credentials}

Você também pode atualizar suas credenciais quando desejar. Você pode atualizar seu `SASToken` fazendo uma solicitação POST para o ponto de extremidade `/credentials` da API [!DNL Connectors].

**Formato da API**

```http
POST /data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh
```

| Parâmetros de consulta | Descrição |
| --- | --- |
| `dlz_destination` | O tipo `dlz_destination` permite que a API diferencie um contêiner de destino de zona de aterrissagem dos outros tipos de contêineres disponíveis para você. |
| `refresh` | A ação `refresh` permite redefinir suas credenciais de zona de aterrissagem e gerar automaticamente um novo `SASToken`. |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir atualiza suas credenciais de zona de aterrissagem.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Resposta**

A resposta a seguir retorna valores atualizados para o(a) `SASToken` e `SASUri`.

```json
{
    "containerName": "dlz-destination",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-destination?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

>[!ENDSHADEBOX]

Forneça seu nome para exibição (`containerName`) e a URL SAS [!DNL Data Landing Zone], conforme retornado na chamada de API descrita acima, e selecione **Avançar**.

![Insira as informações de conexão destacadas na interface do Azure.](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

A janela **Resumo** é exibida, fornecendo uma visão geral das configurações, incluindo informações sobre o ponto de extremidade e as permissões do [!DNL Blob]. Quando estiver pronto, selecione **Conectar**.

![Resumo das configurações mostradas na interface do Azure.](/help/sources/images/tutorials/create/dlz/summary.png)

Uma conexão bem-sucedida atualiza a interface do usuário [!DNL Azure Storage Explorer] com o contêiner [!DNL Data Landing Zone].

![Resumo do contêiner de usuário DLZ realçado na interface do usuário do Azure.](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

Com o contêiner [!DNL Data Landing Zone] conectado ao [!DNL Azure Storage Explorer], você pode começar a exportar arquivos do Experience Platform para o contêiner [!DNL Data Landing Zone]. Para exportar arquivos, você deve estabelecer uma conexão com o destino [!DNL Data Landing Zone] na interface do usuário do Experience Platform, conforme descrito na seção abaixo.

## Autenticar na zona de aterrissagem de dados provisionada pela AWS {#authenticate-dlz-aws}

>[!AVAILABILITY]
>
>Esta seção se aplica às implementações do Experience Platform em execução no Amazon Web Services (AWS). O Experience Platform em execução no AWS está disponível atualmente para um número limitado de clientes. Para saber mais sobre a infraestrutura do Experience Platform compatível, consulte a [visão geral da nuvem múltipla do Experience Platform](https://experienceleague.adobe.com/pt-br/docs/experience-platform/landing/multi-cloud).

Execute as operações abaixo para obter credenciais para sua instância do [!DNL Data Landing Zone] provisionada no AWS. Em seguida, use um cliente de sua escolha para se conectar à sua instância do [!DNL Data Landing Zone].

>[!BEGINSHADEBOX]

### Recupere as credenciais para o seu [!DNL Data Landing Zone] {#retrieve-dlz-credentials-aws}

Você deve usar as APIs do Experience Platform para recuperar suas credenciais do [!DNL Data Landing Zone]. A chamada à API para recuperar suas credenciais é descrita abaixo. Para obter informações sobre como obter os valores necessários para seus cabeçalhos, consulte o guia [Introdução às APIs do Adobe Experience Platform](/help/landing/api-guide.md).

**Formato da API**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination'
```

| Parâmetros de consulta | Descrição |
| --- | --- |
| `dlz_destination` | Adicione o parâmetro de consulta `dlz_destination` para especificar que você deseja que o tipo de credenciais de contêiner [!DNL Data Landing Zone] *destino* seja recuperado. Para conectar e recuperar credenciais de uma *fonte* da Zona de Aterrissagem de Dados, exiba a [documentação de fontes](/help/sources/connectors/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

**Solicitação**

O exemplo de solicitação a seguir recupera credenciais para uma zona de aterrissagem existente.

```shell
curl --request GET \
  --url 'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination' \
  --header 'Authorization: Bearer ***' \
  --header 'Content-Type: application/json' \
  --header 'x-api-key: your_api_key' \
  --header 'x-gw-ims-org-id: yourorg@AdobeOrg'
```

**Resposta**

A resposta a seguir retorna as informações de credencial da sua zona de aterrissagem, incluindo o `awsAccessKeyId`, `awsSecretAccessKey` e outras informações atuais.

```json
{
    "credentials": {
        "awsAccessKeyId": "ABCDW3MEC6HE2T73ZVKP",
        "awsSecretAccessKey": "A1B2Zdxj6y4xfR0QZGtf/phj/hNMAbOGtzM/JNeE",
        "awsSessionToken": "***"
    },
    "dlzPath": {
        "bucketName": "your-bucket-name",
        "dlzFolder": "dlz-destination"
    },
    "dlzProvider": "Amazon S3",
    "expiryTime": 1734494017
}
```

| Propriedade | Descrição |
| --- | --- |
| `credentials` | Esse objeto inclui o `awsAccessKeyId`, `awsSecretAccessKey` e `awsSessionToken` que a Experience Platform usa para exportar arquivos para o local da Zona de Aterrissagem de Dados provisionada. |
| `dlzPath` | Esse objeto inclui o caminho no local do AWS provisionado pela Adobe onde os arquivos exportados são depositados. |
| `dlzProvider` | Indica que esta é uma Zona de aterrissagem de dados provisionada pelo Amazon S3. |
| `expiryTime` | Indica quando as credenciais no objeto `credentials` irão expirar. Para atualizar as credenciais, execute a solicitação novamente. |

{style="table-layout:auto"}

>[!ENDSHADEBOX]

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa das **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=pt-BR). No workflow da configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Verifique se você conectou o contêiner [!DNL Data Landing Zone] a [!DNL Azure Storage Explorer] conforme descrito na seção [pré-requisitos](#prerequisites). Como [!DNL Data Landing Zone] é um armazenamento provisionado pela Adobe, não é necessário executar outras etapas na interface do usuário do Experience Platform para autenticar no destino.

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Encryption key]**: Opcionalmente, você pode anexar sua chave pública formatada em RSA para adicionar criptografia aos seus arquivos exportados. Veja um exemplo de uma chave de criptografia formatada corretamente na imagem abaixo.
  ![Imagem mostrando um exemplo de uma chave PGP formatada corretamente na interface.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)
* **[!UICONTROL Name]**: Preencha o nome preferencial para este destino.
* **[!UICONTROL Description]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
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

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL View Identity Graph]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

### Agendamento

Na etapa **[!UICONTROL Scheduling]**, você pode [configurar o agendamento de exportação](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) para o seu destino [!DNL Data Landing Zone] e também [configurar o nome dos seus arquivos exportados](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Mapear atributos e identidades {#map}

Na etapa **[!UICONTROL Mapping]**, você pode selecionar quais campos de atributo e identidade serão exportados para seus perfis. Você também pode optar por alterar os cabeçalhos no arquivo exportado para qualquer nome amigável. Para obter mais informações, exiba a [etapa de mapeamento](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) no tutorial de ativação da interface de destinos em lote.

## Validar exportação de dados bem-sucedida {#exported-data}

Para verificar se os dados foram exportados com êxito, verifique o armazenamento do [!DNL Data Landing Zone] e se os arquivos exportados contêm as populações de perfis esperadas.
