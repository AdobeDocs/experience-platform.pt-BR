---
title: Conexão com o Amazon S3
description: Crie uma conexão de saída ativa com seu armazenamento Amazon Web Services (AWS) S3 para exportar arquivos de dados CSV da Adobe Experience Platform periodicamente para seus próprios buckets do S3.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1773'
ht-degree: 14%

---

# [!DNL Amazon S3] conexão {#s3-connection}

## Log de alterações de destino {#changelog}

+++ Exibir changelog


| Mês de lançamento | Tipo de atualização | Descrição |
|---|---|---|
| Janeiro de 2024 | Atualização de funcionalidade e documentação | O conector de destino do Amazon S3 agora oferece suporte a um novo tipo de autenticação de função presumida. Leia mais sobre isso na [seção de autenticação](#assumed-role-authentication). |
| Julho de 2023 | Atualização de funcionalidade e documentação | Com a versão de julho de 2023 do Experience Platform, o destino [!DNL Amazon S3] fornece novas funcionalidades, conforme listado abaixo: <br><ul><li>[Suporte à exportação do conjunto de dados](/help/destinations/ui/export-datasets.md)</li><li>[Opções de nomenclatura de arquivo](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) adicionais.</li><li>Capacidade de definir cabeçalhos de arquivos personalizados em seus arquivos exportados por meio da [etapa de mapeamento aprimorado](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[Capacidade de personalizar a formatação de arquivos de dados CSV exportados](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> |

{style="table-layout:auto"}

+++

## Conectar-se ao armazenamento do [!DNL Amazon S3] por meio da API ou da interface {#connect-api-or-ui}

* Para se conectar ao local de armazenamento do [!DNL Amazon S3] usando a interface do usuário do Experience Platform, leia as seções [Conectar-se ao destino](#connect) e [Ativar públicos-alvo para este destino](#activate) abaixo.
* Para se conectar ao local de armazenamento do [!DNL Amazon S3] de forma programática, leia o guia sobre como [ativar públicos-alvo para destinos baseados em arquivo usando o tutorial da API de Serviço de Fluxo](../../api/activate-segments-file-based-destinations.md).

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

![Tipo de exportação baseado em perfil do Amazon S3 realçado na UU.](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Exportar conjuntos de dados {#export-datasets}

Esse destino suporta exportações de conjunto de dados. Para obter informações completas sobre como configurar exportações de conjunto de dados, leia os tutoriais:

* Como [exportar conjuntos de dados usando a interface do usuário do Experience Platform](/help/destinations/ui/export-datasets.md).
* Como [exportar conjuntos de dados de forma programática usando a API de Serviço de Fluxo](/help/destinations/api/export-datasets.md).

## Formato de arquivo dos dados exportados {#file-format}

Ao exportar *dados de público-alvo*, o Experience Platform cria um arquivo `.csv`, `parquet` ou `.json` no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte a seção [formatos de arquivo compatíveis com a exportação](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) no tutorial de ativação de público-alvo.

Ao exportar *conjuntos de dados*, o Experience Platform cria um arquivo `.parquet` ou `.json` no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte a seção [verificar exportação bem-sucedida do conjunto de dados](../../ui/export-datasets.md#verify) no tutorial exportar conjuntos de dados.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa das **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow da configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="Chave pública RSA"
>abstract="Opcionalmente, é possível anexar sua chave pública formatada em RSA para adicionar criptografia aos arquivos exportados. Veja um exemplo de uma chave corretamente formatada no link da documentação abaixo."

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Connect to destination]**. O destino do Amazon S3 é compatível com dois métodos de autenticação:

* Autenticação da chave de acesso e da chave secreta
* Autenticação de função presumida

#### Autenticação com chave de acesso S3 e chave secreta

Use esse método de autenticação quando quiser inserir sua chave de acesso e chave secreta do Amazon S3 para permitir que o Experience Platform exporte dados para suas propriedades do Amazon S3.

![Imagem dos campos obrigatórios ao selecionar a autenticação da chave de acesso e da chave secreta.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/access-key-secret-key-authentication.png)

* **[!DNL Amazon S3]chave de acesso** e **[!DNL Amazon S3]chave secreta**: em [!DNL Amazon S3], gere um par de `access key - secret access key` para conceder ao Experience Platform acesso à sua conta do [!DNL Amazon S3]. Saiba mais na [documentação do Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Encryption key]**: Opcionalmente, você pode anexar sua chave pública formatada em RSA para adicionar criptografia aos seus arquivos exportados. Veja um exemplo de uma chave de criptografia formatada corretamente na imagem abaixo.

  ![Imagem mostrando um exemplo de uma chave PGP formatada corretamente na interface.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

#### Autenticação com função S3 assumida {#assumed-role-authentication}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_assumed_role"
>title="Autenticação de função presumida"
>abstract="Use esse tipo de autenticação se preferir não compartilhar chaves de conta e chaves secretas com a Adobe. Em vez disso, a Experience Platform se conecta ao local do Amazon S3 usando acesso com base em função. Cole o ARN da função que você criou no AWS para o usuário da Adobe. O padrão é semelhante a `arn:aws:iam::800873819705:role/destinations-role-customer` "

Use esse tipo de autenticação se preferir não compartilhar chaves de conta e chaves secretas com a Adobe. Em vez disso, o Experience Platform se conecta ao local do Amazon S3 usando acesso com base em função.

![Imagem dos campos obrigatórios ao selecionar a autenticação de função presumida.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/assumed-role-authentication.png)

* **[!DNL Role]**: Cole o ARN da função que você criou no AWS para o usuário do Adobe. O padrão é semelhante a `arn:aws:iam::800873819705:role/destinations-role-customer`. Consulte as etapas abaixo para obter orientações detalhadas sobre como configurar o acesso S3 corretamente.
* **[!UICONTROL Encryption key]**: Opcionalmente, você pode anexar sua chave pública formatada em RSA para adicionar criptografia aos seus arquivos exportados. Veja um exemplo de uma chave de criptografia formatada corretamente na imagem abaixo.

Para fazer isso, você precisa criar no console do AWS uma função assumida para o Adobe com as [permissões certas necessárias](#minimum-permissions-iam-user) para gravar em seus buckets do Amazon S3.

**Criar uma política com as permissões necessárias**

1. Abra o Console do AWS e acesse IAM > Políticas > Criar política
2. Selecione Editor de políticas > JSON e adicione as permissões abaixo.

   ```json
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Sid": "VisualEditor0",
               "Effect": "Allow",
               "Action": [
                   "s3:PutObject",
                   "s3:GetObject",
                   "s3:DeleteObject",
                   "s3:GetBucketLocation",
                   "s3:ListMultipartUploadParts"
               ],
               "Resource": "arn:aws:s3:::bucket/folder/*"
           },
           {
               "Sid": "VisualEditor1",
               "Effect": "Allow",
               "Action": [
                   "s3:ListBucket"
               ],
               "Resource": "arn:aws:s3:::bucket"
           }
       ]
   }
   ```

3. Na próxima página, digite um nome para a política e salve-a para referência. Você precisará desse nome de política ao criar a função na próxima etapa.

**Criar função de usuário em sua conta de cliente S3**

1. Abra o Console do AWS e acesse IAM > Funções > Criar nova função
2. Selecione **Tipo de entidade confiável** > **Conta da AWS**
3. Selecione **Uma conta do AWS** > **Outra conta do AWS** e insira a ID da conta do Adobe: `670664943635`
4. Adicionar permissões usando a política criada anteriormente
5. Insira um nome de função (por exemplo, `destinations-role-customer`). O nome da função deve ser tratado como confidencial, semelhante a uma senha. Ele pode ter até 64 caracteres e pode conter caracteres alfanuméricos e os seguintes caracteres especiais: `+=,.@-_`. Em seguida, verifique se:
   * A ID da conta da Adobe `670664943635` está presente na seção **[!UICONTROL Select trusted entities]**
   * A política criada anteriormente está presente em **[!UICONTROL Permissions policy summary]**

**Forneça a função a ser assumida pela Adobe**

Depois de criar a função no AWS, é necessário fornecer a função ARN para o Adobe. O ARN segue este padrão: `arn:aws:iam::800873819705:role/destinations-role-customer`

Você pode encontrar o ARN na página principal depois de criar a função no console do AWS. Você usará este ARN ao criar o destino.

**Verificar permissões de função e relações de confiança**

Certifique-se de que sua função tenha a seguinte configuração:

* **Permissões**: a função deve ter permissões para acessar S3 (acesso total ou as permissões mínimas fornecidas na etapa **Criar uma política com as permissões necessárias** acima)
* **Relações de confiança**: a função deve ter a conta raiz Adobe (`670664943635`) em suas relações de confiança

**Alternativa: Restringir a um usuário específico do Adobe (Opcional)**

Se preferir não permitir toda a conta do Adobe, é possível restringir o acesso somente ao usuário específico do Adobe. Para fazer isso, edite a diretiva de confiança com a seguinte configuração:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::670664943635:user/destinations-adobe-user"
            },
            "Action": "sts:AssumeRole",
            "Condition": {}
        }
    ]
}
```

Para obter mais informações, consulte a [documentação do AWS sobre criação de funções](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html).



### Preencher detalhes do destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="Nome do bucket"
>abstract="Deve ter entre 3 e 63 caracteres. Deve começar e terminar com uma letra ou número. Deve conter somente letras minúsculas, números ou hifens ( - ). Não deve ser formatado como um endereço IP (por exemplo, 192.100.1.1)."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="Caminho da pasta"
>abstract="Deve conter somente caracteres A-Z, a-z, 0-9 e pode incluir os seguintes caracteres especiais: `/!-_.'()"^[]+$%.*"`. Para criar uma pasta por arquivo de público-alvo, insira a macro `/%SEGMENT_NAME%` ou `/%SEGMENT_ID%` ou `/%SEGMENT_NAME%/%SEGMENT_ID%` no campo de texto. Macros só podem ser inseridas no final do caminho da pasta. Veja exemplos de macro na documentação."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=pt-BR#use-macros" text="Use macros para criar uma pasta no seu local de armazenamento"

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Name]**: Digite um nome que o ajudará a identificar este destino.
* **[!UICONTROL Description]**: Insira uma descrição deste destino.
* **[!UICONTROL Bucket name]**: insira o nome do bucket [!DNL Amazon S3] a ser usado por este destino.
* **[!UICONTROL Folder path]**: Insira o caminho para a pasta de destino que hospedará os arquivos exportados.
* **[!UICONTROL File type]**: Selecione o formato que o Experience Platform deve usar para os arquivos exportados. Ao selecionar a opção [!UICONTROL CSV], você também pode [configurar as opções de formatação de arquivo](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Compression format]**: Selecione o tipo de compactação que o Experience Platform deve usar para os arquivos exportados.
* **[!UICONTROL Include manifest file]**: ative esta opção se desejar que as exportações incluam um arquivo JSON de manifesto que contenha informações sobre o local de exportação, tamanho da exportação e muito mais. O manifesto é nomeado usando o formato `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Exibir um [arquivo de manifesto de exemplo](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). O arquivo de manifesto inclui os seguintes campos:
   * `flowRunId`: A [execução do fluxo de dados](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) que gerou o arquivo exportado.
   * `scheduledTime`: A hora em UTC quando o arquivo foi exportado.
   * `exportResults.sinkPath`: O caminho no local de armazenamento onde o arquivo exportado está depositado.
   * `exportResults.name`: O nome do arquivo exportado.
   * `size`: O tamanho do arquivo exportado, em bytes.

>[!TIP]
>
>No workflow de destino de conexão, é possível criar uma pasta personalizada no armazenamento Amazon S3 por arquivo de público exportado. Leia [Usar macros para criar uma pasta no local de armazenamento](overview.md#use-macros) para obter instruções.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

### [!DNL Amazon S3] permissões necessárias {#required-s3-permission}

Para conectar e exportar dados com êxito para o local de armazenamento do [!DNL Amazon S3], crie um usuário do Gerenciamento de Identidade e Acesso (IAM) para [!DNL Experience Platform] no [!DNL Amazon S3] e atribua permissões para as seguintes ações:

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`

#### Permissões mínimas necessárias para autenticação de função assumida pelo IAM {#minimum-permissions-iam-user}

Ao configurar a função IAM como cliente, verifique se a política de permissão associada à função inclui as ações necessárias para a pasta de destino no bucket e a ação `s3:ListBucket` para a raiz do bucket. Veja abaixo um exemplo da política de permissões mínimas para este tipo de autenticação:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:DeleteObject",
                "s3:GetBucketLocation",
                "s3:ListMultipartUploadParts"
            ],
            "Resource": "arn:aws:s3:::bucket/folder/*"
        },
        {
            "Sid": "VisualEditor1",
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket"
            ],
            "Resource": "arn:aws:s3:::bucket"
        }
    ]
}  
```

<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Experience Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL View Identity Graph]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

## Validar exportação de dados bem-sucedida {#exported-data}

Para verificar se os dados foram exportados com êxito, verifique o armazenamento do [!DNL Amazon S3] e se os arquivos exportados contêm as populações de perfis esperadas.

## INCLUO NA LISTA DE PERMISSÕES de endereços IP {#ip-address-allow-list}

Consulte o artigo [incluo na lista de permissões de endereços IP](ip-address-allow-list.md) se precisar adicionar IPs do Adobe a um incluo na lista de permissões.