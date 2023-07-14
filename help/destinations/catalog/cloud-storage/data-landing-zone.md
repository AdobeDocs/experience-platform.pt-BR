---
title: Destino da Data Landing Zone
description: Saiba como se conectar à Data Landing Zone para ativar públicos e exportar conjuntos de dados.
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: 4b9e7c22282a5531f2f25f3d225249e4eb0e178e
workflow-type: tm+mt
source-wordcount: '1434'
ht-degree: 1%

---

# (Beta) Destino da zona de aterrissagem de dados

>[!IMPORTANT]
>
>* No momento, esse destino está na versão beta e só está disponível para um número limitado de clientes. Para solicitar acesso à [!DNL Data Landing Zone] conexão, entre em contato com o representante da Adobe e forneça [!DNL Organization ID].
>* Esta página de documentação se refere ao [!DNL Data Landing Zone] *destino*. Existe também uma [!DNL Data Landing Zone] *origem* no catálogo de origens. Para obter mais informações, leia a [[!DNL Data Landing Zone] origem](/help/sources/connectors/cloud-storage/data-landing-zone.md) documentação.


## Visão geral {#overview}

[!DNL Data Landing Zone] é um [!DNL Azure Blob] interface de armazenamento de dados provisionada pela Adobe Experience Platform, que concede acesso a um recurso seguro de armazenamento de arquivos baseado em nuvem para exportar arquivos da plataforma. Você tem acesso a um [!DNL Data Landing Zone] por sandbox, e o volume total de dados em todos os containers é limitado ao total de dados fornecido com sua licença de Produtos e Serviços da Platform. Todos os clientes da Platform e seus serviços de aplicativos, como [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services], e [!DNL Real-Time Customer Data Platform] são provisionados com um [!DNL Data Landing Zone] contêiner por sandbox. Você pode ler e gravar arquivos no seu contêiner por meio de [!DNL Azure Storage Explorer] ou na interface de linha de comando.

[!DNL Data Landing Zone] oferece suporte à autenticação baseada em SAS e seus dados estão protegidos com o padrão [!DNL Azure Blob] mecanismos de segurança de armazenamento em repouso e em trânsito. A autenticação baseada em SAS permite que você acesse com segurança seus [!DNL Data Landing Zone] contêiner por meio de uma conexão pública com a internet. Não são necessárias alterações na rede para que você acesse seu [!DNL Data Landing Zone] contêiner, o que significa que você não precisa definir nenhuma configuração de lista de permissões ou entre regiões para sua rede.

A Platform impõe um TTL (time-to-live) rigoroso de sete dias em todos os arquivos carregados em um [!DNL Data Landing Zone] recipiente. Todos os arquivos são excluídos após sete dias.

## Conecte-se ao seu [!UICONTROL Data Landing Zone] armazenamento por meio da API ou da interface {#connect-api-or-ui}

* Para se conectar ao seu [!UICONTROL Data Landing Zone] local de armazenamento usando a interface do usuário da Platform, leia as seções [Conectar ao destino](#connect) e [Ativar públicos para este destino](#activate) abaixo.
* Para se conectar ao seu [!UICONTROL Data Landing Zone] local de armazenamento de dados de forma programática, leia as [Ative públicos para destinos baseados em arquivo usando o tutorial da API do Serviço de fluxo](../../api/activate-segments-file-based-destinations.md).

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve todos os públicos-alvo que você pode exportar para esse destino.

Todos os destinos oferecem suporte à ativação de públicos-alvo gerados pelo Experience Platform [Serviço de segmentação](../../../segmentation/home.md).

Além disso, esse destino também suporta a ativação dos públicos-alvo descritos na tabela abaixo.

| Tipo de público | Descrição |
---------|----------|
| Uploads personalizados | Públicos-alvo assimilados em Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, juntamente com os campos de esquema aplicáveis (por exemplo, o PPID), conforme escolhido na tela Selecionar atributos de perfil da [workflow de ativação de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Lote]** | Os destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos baseados em arquivo em lote](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Pré-requisitos {#prerequisites}

Observe os seguintes pré-requisitos que devem ser atendidos antes de usar o [!DNL Data Landing Zone] destino.

### Conecte seu [!DNL Data Landing Zone] contêiner para [!DNL Azure Storage Explorer]

Você pode usar [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/products/storage/storage-explorer/) para gerenciar o conteúdo do [!DNL Data Landing Zone] recipiente. Para começar a usar o [!DNL Data Landing Zone], você deve primeiro recuperar suas credenciais e inseri-las em [!DNL Azure Storage Explorer]e conecte seu [!DNL Data Landing Zone] contêiner para [!DNL Azure Storage Explorer].

No [!DNL Azure Storage Explorer] Selecione o ícone de conexão na barra de navegação esquerda. A variável **Selecionar recurso** é exibida, fornecendo opções para conexão. Selecionar **[!DNL Blob container]** para se conectar ao seu [!DNL Data Landing Zone] armazenamento.

![select-resource](/help/sources/images/tutorials/create/dlz/select-resource.png)

Em seguida, selecione **URL de assinatura de acesso compartilhado (SAS)** como seu método de conexão e, em seguida, selecione **Próxima**.

![select-connection-method](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

Depois de selecionar o método de conexão, você deve fornecer um **nome de exibição** e a variável **[!DNL Blob]URL SAS do contêiner** que corresponde ao seu [!DNL Data Landing Zone] recipiente.

>[!BEGINSHADEBOX]

### Recupere as credenciais para o seu [!DNL Data Landing Zone] {#retrieve-dlz-credentials}

Você deve usar as APIs da plataforma para recuperar seus [!DNL Data Landing Zone] credenciais. A chamada à API para recuperar suas credenciais é descrita abaixo. Para obter informações sobre como obter os valores necessários para seus cabeçalhos, consulte [Introdução às APIs do Adobe Experience Platform](/help/landing/api-guide.md) guia.

**Formato da API**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination
```

| Parâmetros de consulta | Descrição |
| --- | --- |
| `dlz_destination` | A variável `dlz_destination` O tipo permite que a API diferencie um contêiner de destino de zona de aterrissagem dos outros tipos de contêineres disponíveis para você. |

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

A resposta a seguir retorna as informações de credencial da sua zona de aterrissagem, incluindo a atual `SASToken` e `SASUri`, e o `storageAccountName` que corresponde ao seu contêiner de zona de aterrissagem.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3df123",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| Propriedade | Descrição |
| --- | --- |
| `containerName` | O nome da sua zona de destino. |
| `SASToken` | O token de assinatura de acesso compartilhado para sua zona de aterrissagem. Esta cadeia de caracteres contém todas as informações necessárias para autorizar uma solicitação. |
| `SASUri` | O URI de assinatura de acesso compartilhado para sua zona de aterrissagem. Essa string é uma combinação do URI para a zona de aterrissagem para a qual você está sendo autenticado e seu token SAS correspondente, |

{style="table-layout:auto"}

### Atualizar [!DNL Data Landing Zone] credenciais {#update-dlz-credentials}

Você também pode atualizar suas credenciais quando desejar. Você pode atualizar seu `SASToken` fazendo uma solicitação POST para o `/credentials` endpoint do [!DNL Connectors] API.

**Formato da API**

```http
POST /data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh
```

| Parâmetros de consulta | Descrição |
| --- | --- |
| `dlz_destination` | A variável `dlz_destination` O tipo permite que a API diferencie um contêiner de destino de zona de aterrissagem dos outros tipos de contêineres disponíveis para você. |
| `refresh` | A variável `refresh` permite redefinir suas credenciais de zona de aterrissagem e gerar automaticamente uma nova `SASToken`. |

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

A resposta a seguir retorna os valores atualizados para o `SASToken` e `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

>[!ENDSHADEBOX]

Forneça seu nome para exibição (`containerName`) e [!DNL Data Landing Zone] URL SAS, conforme retornado na chamada de API descrita acima, e selecione **Próxima**.

![enter-connection-info](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

A variável **Resumo** é exibida, fornecendo uma visão geral de suas configurações, incluindo informações sobre [!DNL Blob] endpoint e permissões. Quando estiver pronto, selecione **Conectar**.

![resumo](/help/sources/images/tutorials/create/dlz/summary.png)

Uma conexão bem-sucedida atualiza seu [!DNL Azure Storage Explorer] Interface com o seu [!DNL Data Landing Zone] recipiente.

![dlz-user-container](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

Com o seu [!DNL Data Landing Zone] contêiner conectado a [!DNL Azure Storage Explorer], agora é possível começar a exportar arquivos do Experience Platform para o seu [!DNL Data Landing Zone] recipiente. Para exportar arquivos, é necessário estabelecer uma conexão com o [!DNL Data Landing Zone] destino na interface do usuário do Experience Platform, conforme descrito na seção abaixo.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). No workflow da configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para destino {#authenticate}

Verifique se você conectou o [!DNL Data Landing Zone] contêiner para [!DNL Azure Storage Explorer] conforme descrito na seção [pré-requisitos](#prerequisites) seção. Porque [!DNL Data Landing Zone] é um armazenamento provisionado por Adobe, não é necessário executar outras etapas na interface do usuário do Experience Platform para autenticar no destino.

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: Preencha o nome preferencial para este destino.
* **[!UICONTROL Descrição]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Caminho da pasta]**: insira o caminho para a pasta de destino que hospedará os arquivos exportados.
* **[!UICONTROL Tipo de arquivo]**: selecione o formato que o Experience Platform deve usar para os arquivos exportados. Ao selecionar a variável [!UICONTROL CSV] , você também pode [configurar as opções de formatação de arquivo](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Formato de compactação]**: selecione o tipo de compactação que o Experience Platform deve usar para os arquivos exportados.
* **[!UICONTROL Incluir arquivo de manifesto]**: ative essa opção se desejar que as exportações incluam um arquivo JSON de manifesto que contenha informações sobre o local de exportação, o tamanho da exportação e muito mais.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

### Programação

No **[!UICONTROL Agendamento]** etapa, você pode [configurar o cronograma de exportação](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) para seu [!DNL Data Landing Zone] destino e você também pode [configurar o nome dos arquivos exportados](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Mapear atributos e identidades {#map}

No **[!UICONTROL Mapeamento]** etapa, você pode selecionar quais campos de atributo e identidade serão exportados para seus perfis. Você também pode optar por alterar os cabeçalhos no arquivo exportado para qualquer nome amigável. Para obter mais informações, consulte [etapa de mapeamento](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) no tutorial ativar interface do usuário de destinos em lote.

## (Beta) Exportar conjuntos de dados {#export-datasets}

Esse destino suporta exportações de conjunto de dados. Para obter informações completas sobre como configurar exportações de conjunto de dados, leia os tutoriais:

* Como [exportar conjuntos de dados usando a interface do usuário da Platform](/help/destinations/ui/export-datasets.md).
* Como [exportar conjuntos de dados de forma programática usando a API do Serviço de fluxo](/help/destinations/api/export-datasets.md).

## Validar exportação de dados bem-sucedida {#exported-data}

Para verificar se os dados foram exportados com êxito, verifique [!DNL Data Landing Zone] armazenamento e verifique se os arquivos exportados contêm as populações de perfis esperadas.
