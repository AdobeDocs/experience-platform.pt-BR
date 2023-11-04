---
title: Conexão com o Amazon S3
description: Crie uma conexão de saída ativa com seu armazenamento Amazon Web Services (AWS) S3 para exportar arquivos de dados CSV da Adobe Experience Platform periodicamente para seus próprios buckets do S3.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: a1b3e59e0d5b1312b7bc22885ee679775c2a4d78
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 17%

---

# Conexão com o [!DNL Amazon S3] {#s3-connection}

## Log de alterações de destino {#changelog}

Com a versão de julho de 2023 do Experience Platform, a [!DNL Amazon S3] O destino fornece novas funcionalidades, conforme listado abaixo:

* [Suporte à exportação de conjuntos de dados](/help/destinations/ui/export-datasets.md).
* [Opções de nomenclatura de arquivo](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) adicionais.
* Capacidade de definir cabeçalhos de arquivos personalizados em seus arquivos exportados por meio da [etapa de mapeamento aprimorado](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Capacidade de personalizar a formatação de arquivos de dados CSV exportados](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Conecte-se ao seu [!DNL Amazon S3] armazenamento por meio da API ou da interface {#connect-api-or-ui}

* Para se conectar ao seu [!DNL Amazon S3] local de armazenamento usando a interface do usuário da Platform, leia as seções [Conectar ao destino](#connect) e [Ativar públicos para este destino](#activate) abaixo.
* Para se conectar ao seu [!DNL Amazon S3] local de armazenamento de dados de forma programática, leia as [Ative públicos para destinos baseados em arquivo usando o tutorial da API do Serviço de fluxo](../../api/activate-segments-file-based-destinations.md).

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve que tipo de público-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo Experience Platform [Serviço de segmentação](../../../segmentation/home.md). |
| Uploads personalizados | ✓ | Públicos-alvo [importado](../../../segmentation/ui/overview.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, juntamente com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos de perfil da [workflow de ativação de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Lote]** | Os destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos baseados em arquivo em lote](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![Tipo de exportação baseada em perfil do Amazon S3](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow da configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="Chave pública RSA"
>abstract="Opcionalmente, é possível anexar sua chave pública formatada em RSA para adicionar criptografia aos arquivos exportados. Veja um exemplo de uma chave corretamente formatada no link da documentação abaixo."

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Conectar ao destino]**.

* **[!DNL Amazon S3]chave de acesso** e **[!DNL Amazon S3]chave secreta**: Em [!DNL Amazon S3], gerar um `access key - secret access key` emparelhe para conceder acesso à Platform ao seu [!DNL Amazon S3] conta. Saiba mais na [Documentação do Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Chave de criptografia]**: como opção, você pode anexar sua chave pública formatada em RSA para adicionar criptografia aos arquivos exportados. Veja um exemplo de uma chave de criptografia formatada corretamente na imagem abaixo.

  ![Imagem que mostra um exemplo de uma chave PGP formatada corretamente na interface](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Preencher detalhes do destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="Nome do bucket"
>abstract="Deve ter entre 3 e 63 caracteres. Deve começar e terminar com uma letra ou número. Deve conter somente letras minúsculas, números ou hifens ( - ). Não deve ser formatado como um endereço IP (por exemplo, 192.100.1.1)."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="Caminho da pasta"
>abstract="Deve conter somente caracteres A-Z, a-z, 0-9 e pode incluir os seguintes caracteres especiais: `/!-_.'()"^[]+$%.*"`. Para criar uma pasta por arquivo de público-alvo, insira a macro `/%SEGMENT_NAME%` ou `/%SEGMENT_ID%` ou `/%SEGMENT_NAME%/%SEGMENT_ID%` no campo de texto. Macros só podem ser inseridas no final do caminho da pasta. Veja exemplos de macro na documentação."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html#use-macros" text="Use macros para criar uma pasta no seu local de armazenamento"

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: digite um nome que ajudará a identificar esse destino.
* **[!UICONTROL Descrição]**: digite uma descrição desse destino.
* **[!UICONTROL Nome do bloco]**: Insira o nome do [!DNL Amazon S3] bucket a ser usado por esse destino.
* **[!UICONTROL Caminho da pasta]**: insira o caminho para a pasta de destino que hospedará os arquivos exportados.
* **[!UICONTROL Tipo de arquivo]**: selecione o formato que o Experience Platform deve usar para os arquivos exportados. Ao selecionar a variável [!UICONTROL CSV] , você também pode [configurar as opções de formatação de arquivo](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Formato de compactação]**: selecione o tipo de compactação que o Experience Platform deve usar para os arquivos exportados.
* **[!UICONTROL Incluir arquivo de manifesto]**: ative essa opção se desejar que as exportações incluam um arquivo JSON de manifesto que contenha informações sobre o local de exportação, o tamanho da exportação e muito mais. O manifesto é nomeado usando o formato `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Exibir um [exemplo de arquivo de manifesto](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). O arquivo de manifesto inclui os seguintes campos:
   * `flowRunId`: A variável [execução do fluxo de dados](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) que gerou o arquivo exportado.
   * `scheduledTime`: a hora em UTC quando o arquivo foi exportado.
   * `exportResults.sinkPath`: O caminho no local de armazenamento em que o arquivo exportado está depositado.
   * `exportResults.name`: o nome do arquivo exportado.
   * `size`: o tamanho do arquivo exportado, em bytes.

>[!TIP]
>
>No workflow de destino de conexão, é possível criar uma pasta personalizada no armazenamento Amazon S3 por arquivo de público exportado. Ler [Usar macros para criar uma pasta no local de armazenamento](overview.md#use-macros) para obter instruções.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

### Obrigatório [!DNL Amazon S3] permissões {#required-s3-permission}

Para conectar e exportar dados para o seu [!DNL Amazon S3] local de armazenamento, crie um usuário do Identity and Access Management (IAM) para [!DNL Platform] in [!DNL Amazon S3] e atribuir permissões para as seguintes ações:

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`

<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisará do **[!UICONTROL Exibir gráfico de identidade]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos."){width="100" zoomable="yes"}

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

## (Beta) Exportar conjuntos de dados {#export-datasets}

Esse destino suporta exportações de conjunto de dados. Para obter informações completas sobre como configurar exportações de conjunto de dados, leia os tutoriais:

* Como [exportar conjuntos de dados usando a interface do usuário da Platform](/help/destinations/ui/export-datasets.md).
* Como [exportar conjuntos de dados de forma programática usando a API do Serviço de fluxo](/help/destinations/api/export-datasets.md).

## Dados exportados {#exported-data}

Para [!DNL Amazon S3] destinos, [!DNL Platform] cria um arquivo de dados no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) no tutorial de ativação de público-alvo.
