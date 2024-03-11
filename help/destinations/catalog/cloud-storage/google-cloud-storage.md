---
title: Conexão do Google Cloud Storage
description: Saiba como se conectar ao Google Cloud Storage e ativar públicos ou exportar conjuntos de dados.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: ab274270-ae8c-4264-ba64-700b118e6435
source-git-commit: 8771aa0df001e8ef81d4ad712f4d1f9661b405b2
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 2%

---

# [!DNL Google Cloud Storage] conexão

## Visão geral {#overview}

Criar uma conexão de saída ativa com o [!DNL Google Cloud Storage] para exportar arquivos de dados do Adobe Experience Platform periodicamente para seus próprios buckets.

## Conecte-se ao seu [!DNL Google Cloud Storage] armazenamento por meio da API ou da interface {#connect-api-or-ui}

* Para se conectar ao seu [!DNL Google Cloud Storage] local de armazenamento usando a interface do usuário da Platform, leia as seções [Conectar ao destino](#connect) e [Ativar públicos para este destino](#activate) abaixo.
* Para se conectar ao seu [!DNL Google Cloud Storage] local de armazenamento de dados de forma programática, leia as [Ative públicos para destinos baseados em arquivo usando o tutorial da API do Serviço de fluxo](../../api/activate-segments-file-based-destinations.md).

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo Experience Platform [Serviço de segmentação](../../../segmentation/home.md). |
| Uploads personalizados | ✓ | Públicos-alvo [importado](../../../segmentation/ui/overview.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, juntamente com os campos de esquema aplicáveis, conforme escolhido na tela Selecionar atributos de perfil da [workflow de ativação de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Lote]** | Os destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos baseados em arquivo em lote](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Exportar conjuntos de dados {#export-datasets}

Esse destino suporta exportações de conjunto de dados. Para obter informações completas sobre como configurar exportações de conjunto de dados, leia os tutoriais:

* Como [exportar conjuntos de dados usando a interface do usuário da Platform](/help/destinations/ui/export-datasets.md).
* Como [exportar conjuntos de dados de forma programática usando a API do Serviço de fluxo](/help/destinations/api/export-datasets.md).

## Formato de arquivo dos dados exportados {#file-format}

Ao exportar *dados de público*, a Platform cria um `.csv`, `parquet`ou `.json` no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte [formatos de arquivo compatíveis com a exportação](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) no tutorial de ativação de público-alvo.

Ao exportar *conjuntos de dados*, a Platform cria um `.parquet` ou `.json` no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte [verificar exportação bem-sucedida do conjunto de dados](../../ui/export-datasets.md#verify) no tutorial exportar conjuntos de dados.

## Pré-requisito de configuração para a conexão com o [!DNL Google Cloud Storage] account {#prerequisites}

Para conectar a Platform a [!DNL Google Cloud Storage], você deve primeiro habilitar a interoperabilidade para o seu [!DNL Google Cloud Storage] conta. Para acessar a configuração de interoperabilidade, abra [!DNL Google Cloud Platform] e selecione **[!UICONTROL Configurações]** do **[!UICONTROL Armazenamento na nuvem]** no painel de navegação.

![Painel da Google Cloud Platform com Armazenamento na nuvem e configurações destacados.](../../../sources/images/tutorials/create/google-cloud-storage/nav.png)

A variável **[!UICONTROL Configurações]** é exibida. Aqui, você pode ver informações sobre o seu [!DNL Google] ID do projeto e detalhes sobre o [!DNL Google Cloud Storage] conta. Para acessar as configurações de interoperabilidade, selecione **[!UICONTROL Interoperabilidade]** no cabeçalho superior.

![A guia Interoperabilidade é realçada no painel da Google Cloud Platform.](../../../sources/images/tutorials/create/google-cloud-storage/project-access.png)

A variável **[!UICONTROL Interoperabilidade]** Esta página contém informações sobre autenticação, chaves de acesso e o projeto padrão associado à sua conta de serviço. Para gerar uma nova ID de chave de acesso e uma chave de acesso secreta para sua conta de serviço, selecione **[!UICONTROL Criar uma Chave para uma Conta de Serviço]**.

![A opção Create a key for a service account control destacada no painel da Google Cloud Platform.](../../../sources/images/tutorials/create/google-cloud-storage/interoperability.png)

Você pode usar a ID da chave de acesso recém-gerada e a chave de acesso secreta para conectar [!DNL Google Cloud Storage] para a Platform.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Exibir destinos]** e **[!UICONTROL Gerenciar destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](/help/destinations/ui/connect-destination.md). No workflow da configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Conectar ao destino]**.

* **[!UICONTROL ID da chave de acesso]**: uma sequência de 61 caracteres alfanuméricos usada para autenticar seu [!DNL Google Cloud Storage] para a Platform. Para obter informações sobre como obter esse valor, leia a [pré-requisitos](#prerequisites) acima.
* **[!UICONTROL Chave de acesso secreta]**: uma sequência de 40 caracteres codificada em base64 usada para autenticar seu [!DNL Google Cloud Storage] para a Platform. Para obter informações sobre como obter esse valor, leia a [pré-requisitos](#prerequisites) acima.
* **[!UICONTROL Chave de criptografia]**: como opção, você pode anexar sua chave pública formatada em RSA para adicionar criptografia aos arquivos exportados. Veja um exemplo de uma chave de criptografia formatada corretamente na imagem abaixo.

  ![Imagem que mostra um exemplo de uma chave PGP formatada corretamente na interface](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

Para obter mais informações sobre esses valores, leia a [Chaves HMAC do Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guia. Para obter etapas sobre como gerar sua própria ID da chave de acesso e chave de acesso secreta, consulte o [[!DNL Google Cloud Storage] visão geral da origem](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: Preencha o nome preferencial para este destino.
* **[!UICONTROL Descrição]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Nome do bloco]**: Insira o nome do [!DNL Google Cloud Storage] bucket a ser usado por esse destino.
* **[!UICONTROL Caminho da pasta]**: insira o caminho para a pasta de destino que hospedará os arquivos exportados.
* **[!UICONTROL Tipo de arquivo]**: selecione o formato que o Experience Platform deve usar para os arquivos exportados. Ao selecionar a variável [!UICONTROL CSV] , você também pode [configurar as opções de formatação de arquivo](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Formato de compactação]**: selecione o tipo de compactação que o Experience Platform deve usar para os arquivos exportados.
* **[!UICONTROL Incluir arquivo de manifesto]**: ative essa opção se desejar que as exportações incluam um arquivo JSON de manifesto que contenha informações sobre o local de exportação, o tamanho da exportação e muito mais. O manifesto é nomeado usando o formato `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Exibir um [exemplo de arquivo de manifesto](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). O arquivo de manifesto inclui os seguintes campos:
   * `flowRunId`: A variável [execução do fluxo de dados](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) que gerou o arquivo exportado.
   * `scheduledTime`: a hora em UTC quando o arquivo foi exportado.
   * `exportResults.sinkPath`: O caminho no local de armazenamento em que o arquivo exportado está depositado.
   * `exportResults.name`: o nome do arquivo exportado.
   * `size`: o tamanho do arquivo exportado, em bytes.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar os dados, é necessário **[!UICONTROL Exibir destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisará do **[!UICONTROL Exibir gráfico de identidade]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos."){width="100" zoomable="yes"}

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

### Agendamento

No **[!UICONTROL Agendamento]** etapa, você pode [configurar o cronograma de exportação](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) para seu [!DNL Google Cloud Storage] destino e você também pode [configurar o nome dos arquivos exportados](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Mapear atributos e identidades {#map}

No **[!UICONTROL Mapeamento]** etapa, você pode selecionar quais campos de atributo e identidade serão exportados para seus perfis. Você também pode optar por alterar os cabeçalhos no arquivo exportado para qualquer nome amigável. Para obter mais informações, consulte [etapa de mapeamento](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) no tutorial ativar interface do usuário de destinos em lote.

## Validar exportação de dados bem-sucedida {#exported-data}

Para verificar se os dados foram exportados com êxito, verifique [!DNL Google Cloud Storage] e verifique se os arquivos exportados contêm as populações de perfis esperadas.

## INCLUIR NA LISTA DE PERMISSÕES endereço IP {#ip-address-allow-list}

Consulte a [INCLUIR NA LISTA DE PERMISSÕES endereço IP](ip-address-allow-list.md) consulte este artigo se precisar adicionar IPs de Adobe a um incluo na lista de permissões.