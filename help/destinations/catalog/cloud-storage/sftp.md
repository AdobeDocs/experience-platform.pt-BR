---
title: Conexão SFTP
description: Crie uma conexão de saída ativa com o servidor SFTP para exportar arquivos de dados delimitados da Adobe Experience Platform periodicamente.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1182'
ht-degree: 8%

---

# Conexão SFTP

## Log de alterações de destino {#changelog}

Com a versão de julho de 2023 do Experience Platform, o destino SFTP fornece novas funcionalidades, conforme listado abaixo:

* [Suporte à exportação de conjuntos de dados](/help/destinations/ui/export-datasets.md).
* [Opções de nomenclatura de arquivo](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) adicionais.
* Capacidade de definir cabeçalhos de arquivos personalizados em seus arquivos exportados por meio da [etapa de mapeamento aprimorado](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Capacidade de personalizar a formatação de arquivos de dados CSV exportados](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Visão geral {#overview}

Crie uma conexão de saída ativa com o servidor SFTP para exportar arquivos de dados delimitados da Adobe Experience Platform periodicamente.

>[!IMPORTANT]
>
> Embora a Experience Platform ofereça suporte a exportações de dados para servidores SFTP, os locais de armazenamento na nuvem recomendados para a exportação de dados são [!DNL Amazon S3] e [!DNL Azure Blob].

## Conectar-se ao SFTP por meio da API ou da interface {#connect-api-or-ui}

* Para se conectar ao local de armazenamento SFTP usando a interface do usuário do Experience Platform, leia as seções [Conectar-se ao destino](#connect) e [Ativar públicos-alvo para este destino](#activate) abaixo.
* Para se conectar ao local de armazenamento SFTP de forma programática, leia o [Tutorial da API de Serviço de Fluxo](../../api/activate-segments-file-based-destinations.md) para ativar públicos-alvo para destinos baseados em arquivo.

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
| Tipo de exportação | **[!UICONTROL Profile-based]** | Você está exportando todos os membros de um segmento, juntamente com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos de perfil do [fluxo de trabalho de ativação de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Batch]** | Os destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos com base em arquivo de lote](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![Tipo de exportação baseado em perfil SFTP realçado no catálogo de destinos.](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Exportar conjuntos de dados {#export-datasets}

Esse destino suporta exportações de conjunto de dados. Para obter informações completas sobre como configurar exportações de conjunto de dados, leia os tutoriais:

* Como [exportar conjuntos de dados usando a interface do usuário do Experience Platform](/help/destinations/ui/export-datasets.md).
* Como [exportar conjuntos de dados de forma programática usando a API de Serviço de Fluxo](/help/destinations/api/export-datasets.md).

## Formato de arquivo dos dados exportados {#file-format}

Ao exportar *dados de público-alvo*, o Experience Platform cria um arquivo `.csv`, `parquet` ou `.json` no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte a seção [formatos de arquivo compatíveis com a exportação](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) no tutorial de ativação de público-alvo.

Ao exportar *conjuntos de dados*, o Experience Platform cria um arquivo `.parquet` ou `.json` no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte a seção [verificar exportação bem-sucedida do conjunto de dados](../../ui/export-datasets.md#verify) no tutorial exportar conjuntos de dados.

## Requisitos de conexão do servidor SFTP {#sftp-connection-requirements}

Para garantir exportações de dados bem-sucedidas, você deve configurar o servidor SFTP de destino para permitir um número suficiente de conexões simultâneas. Se o servidor SFTP limitar o número de conexões simultâneas, você poderá enfrentar falhas no trabalho de exportação, especialmente ao exportar vários públicos ou conjuntos de dados ao mesmo tempo.

**Recomendação**
Para um desempenho ideal, o servidor SFTP deve permitir pelo menos uma conexão simultânea para cada público ou conjunto de dados que está sendo exportado. No mínimo, o servidor deve oferecer suporte a pelo menos 30% do número total de públicos-alvo ou conjuntos de dados agendados para exportação ao mesmo tempo.

**Exemplo**\
Se você agendar exportações para 100 públicos-alvo ou conjuntos de dados simultaneamente, o servidor SFTP deverá permitir pelo menos 30 conexões simultâneas.

A configuração correta dos limites de conexão do servidor SFTP ajuda a impedir exportações com falha e garante a entrega confiável de dados pelo Adobe Experience Platform.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa das **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Informações de autenticação {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="Chave pública RSA"
>abstract="Opcionalmente, é possível anexar sua chave pública formatada em RSA para adicionar criptografia aos arquivos exportados. Veja um exemplo de uma chave corretamente formatada no link da documentação abaixo."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="Chave SSH privada"
>abstract="A chave SSH privada precisa ser uma string formatada em RSA e codificada em Base64 e não pode estar protegida por senha."

Se você selecionar o tipo de autenticação **[!UICONTROL SFTP with password]** para se conectar ao seu local SFTP:

![Autenticação básica de destino SFTP com senha.](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Domain]**: o endereço do local de armazenamento SFTP;
* **[!UICONTROL Username]**: o nome de usuário para fazer logon no local de armazenamento SFTP;
* **[!UICONTROL Port]**: a porta usada pelo local de armazenamento SFTP;
* **[!UICONTROL Password]**: a senha para fazer logon no local de armazenamento SFTP.
* **[!UICONTROL Encryption key]**: Opcionalmente, você pode anexar sua chave pública formatada em RSA para adicionar criptografia aos seus arquivos exportados. Veja um exemplo de uma chave de criptografia formatada corretamente na imagem abaixo.

  ![Imagem mostrando um exemplo de uma chave PGP formatada corretamente na interface.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)


Se você selecionar o tipo de autenticação **[!UICONTROL SFTP with SSH key]** para se conectar ao seu local SFTP:

![Autenticação de chave SSH de destino SFTP.](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Domain]**: Preencha o endereço IP ou o nome de domínio da sua conta SFTP
* **[!UICONTROL Port]**: a porta usada pelo local de armazenamento SFTP;
* **[!UICONTROL Username]**: o nome de usuário para fazer logon no local de armazenamento SFTP;
* **[!UICONTROL SSH Key]**: a chave SSH privada usada para fazer logon no local de armazenamento SFTP. A chave privada deve ser uma string com formato RSA e codificação Base64, e não deve ser protegida por senha.
* **[!UICONTROL Encryption key]**: Opcionalmente, você pode anexar sua chave pública formatada em RSA para adicionar criptografia aos seus arquivos exportados. Veja um exemplo de uma chave de criptografia formatada corretamente na imagem abaixo.

  ![Imagem mostrando um exemplo de uma chave PGP formatada corretamente na interface.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Detalhes do destino {#destination-details}

Depois de estabelecer a conexão de autenticação com o local SFTP, forneça as seguintes informações para o destino:

![Campos de detalhes do destino SFTP.](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Name]**: insira um nome que ajude a identificar esse destino na interface do usuário do Experience Platform;
* **[!UICONTROL Description]**: Insira uma descrição para este destino;
* **[!UICONTROL Folder path]**: Digite o caminho para a pasta no local SFTP para onde os arquivos serão exportados.
* **[!UICONTROL File type]**: Selecione o formato que o Experience Platform deve usar para os arquivos exportados. Ao selecionar a opção [!UICONTROL CSV], você também pode [configurar as opções de formatação de arquivo](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Compression format]**: Selecione o tipo de compactação que o Experience Platform deve usar para os arquivos exportados.
* **[!UICONTROL Include manifest file]**: ative esta opção se desejar que as exportações incluam um arquivo JSON de manifesto que contenha informações sobre o local de exportação, tamanho da exportação e muito mais. O manifesto é nomeado usando o formato `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Exibir um [arquivo de manifesto de exemplo](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). O arquivo de manifesto inclui os seguintes campos:
   * `flowRunId`: A [execução do fluxo de dados](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) que gerou o arquivo exportado.
   * `scheduledTime`: A hora em UTC quando o arquivo foi exportado.
   * `exportResults.sinkPath`: O caminho no local de armazenamento onde o arquivo exportado está depositado.
   * `exportResults.name`: O nome do arquivo exportado.
   * `size`: O tamanho do arquivo exportado, em bytes.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL View Identity Graph]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

## Validar exportação de dados bem-sucedida {#exported-data}

Para verificar se os dados foram exportados com êxito, verifique o armazenamento SFTP e se os arquivos exportados contêm as populações de perfis esperadas.

## INCLUO NA LISTA DE PERMISSÕES de endereços IP {#ip-address-allow-list}

Consulte o artigo [incluo na lista de permissões de endereços IP](ip-address-allow-list.md) se precisar adicionar IPs do Adobe a um incluo na lista de permissões.
