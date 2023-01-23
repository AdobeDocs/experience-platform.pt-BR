---
title: Conector de perfil Pega
description: Use o Pega Profile Connector for Amazon S3 no Adobe Experience Platform para exportar dados completos ou incrementais, ou ambos, do perfil para o armazenamento em nuvem Amazon S3. No Hub de decisão do cliente da Pega, os trabalhos de dados podem ser agendados no Designer de perfil do cliente para importar dados de perfil periodicamente do armazenamento Amazon S3.
source-git-commit: bdc6ef162e9684065b60a13670848dac64be21fd
workflow-type: tm+mt
source-wordcount: '1086'
ht-degree: 1%

---


# Conector de perfil Pega

## Visão geral {#overview}

Use o [!DNL Pega Profile Connector] no Adobe Experience Platform para criar uma conexão de saída ao vivo com seu [!DNL Amazon Web Services] (AWS) Armazenamento S3 para exportar periodicamente dados de perfil para arquivos CSV do Adobe Experience Platform em seus próprios buckets do S3. Em [!DNL Pega Customer Decision Hub], você pode agendar trabalhos de dados para importar esses dados de perfil do armazenamento S3 para atualizar o [!DNL Pega Customer Decision Hub] perfil.

Esse conector ajuda a configurar a exportação inicial de dados de perfil e também ajuda a sincronizar novos perfis periodicamente em [!DNL Pega Customer Decision Hub].  Ter dados atualizados no Customer Decision Hub fornece uma visualização melhor e atualizada da base de clientes para a próxima melhor tomada de decisão.

>[!IMPORTANT]
>
>Esta página de documentação foi criada pelo Pegasystems. Para quaisquer consultas ou pedidos de atualização, contacte diretamente Pega [here](mailto:support@pega.com).

## Casos de uso

Para ajudá-lo a entender melhor como e quando você deve usar a variável [!DNL Pega Profile Connector] destino, aqui estão casos de uso de exemplo que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso 1

Um profissional de marketing deseja configurar inicialmente [!DNL Pega Customer Decision Hub] com dados de perfil carregados do Adobe Experience Platform. Trata-se de uma carga total inicial seguida de cargas delta programadas.

### Caso de uso 2

Um profissional de marketing deseja obter dados de perfil atualizados da Adobe Experience Platform disponíveis em [!DNL Pega Customer Decision Hub] que aprimora continuamente os insights do Pega sobre os perfis do cliente.

## Pré-requisitos {#prerequisites}

Antes de usar esse destino para exportar dados do Adobe Experience Platform e importar perfis para o [!DNL Pega Customer Decision Hub], certifique-se de concluir os seguintes pré-requisitos:

* Configurar [!DNL Amazon S3] e o caminho da pasta a ser usado para exportação e importação de arquivos de dados.
* Configure o [!DNL Amazon S3] chave de acesso e [!DNL Amazon S3] chave secreta: Em [!DNL Amazon S3]gerar um `access key - secret access key` par para conceder acesso à plataforma [!DNL Amazon S3] conta.
* Para se conectar e exportar dados com êxito para seu [!DNL Amazon S3] local de armazenamento, criar um usuário do Gerenciamento de identidade e acesso (IAM) para [!DNL Platform] em [!DNL Amazon S3] e atribuir permissões como `s3:DeleteObject`, `s3:GetBucketLocation`, `s3:GetObject`, `s3:ListBucket`, `s3:PutObject`, `s3:ListMultipartUploadParts`
* Certifique-se de que [!DNL Pega Customer Decision Hub] A instância é atualizada para a versão 8.8 ou superior.

## Identidades suportadas {#supported-identities}

[!DNL Pega Customer Decision Hub] O suporta a ativação de IDs de usuário personalizadas descritas na tabela abaixo. Para obter mais detalhes, consulte [identidades](/help/identity-service/namespaces.md).

| Identidade do Target | Descrição |
|---|---|
| *CustomerID* | Identificador de usuário comum que identifica exclusivamente um perfil no [!DNL Pega Customer Decision Hub] e Adobe Experience Platform |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, junto com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos de perfil do [fluxo de trabalho de ativação de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Lote]** | Destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos com base em arquivo em lote](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para destino {#authenticate}

Para autenticar para o destino, preencha os campos obrigatórios e selecione **[!UICONTROL Ligar ao destino]**.

* **[!DNL Amazon S3]chave de acesso** e **[!DNL Amazon S3]chave secreta**: Em [!DNL Amazon S3]gerar um `access key - secret access key` par para conceder acesso à Adobe Experience Platform [!DNL Amazon S3] conta. Saiba mais na [Documentação do Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Preencha os detalhes do destino {#destination-details}

Depois de estabelecer a conexão de autenticação com o [!DNL Amazon S3], fornecer as seguintes informações para o destino:

![Imagem da tela da interface do usuário que mostra os campos preenchidos para os detalhes de destino do Conector de perfil de página](../../assets/catalog/personalization/pega-profile/pega-profile-connect-destination.png)

Para configurar detalhes para o destino, preencha os campos obrigatórios e selecione **[!UICONTROL Próximo]**. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: insira um nome que ajudará a identificar esse destino.
* **[!UICONTROL Descrição]**: insira uma descrição deste destino.
* **[!UICONTROL Nome do bucket]**: digite o nome do [!DNL Amazon S3] bucket a ser usado por este destino.
* **[!UICONTROL Caminho da pasta]**: insira o caminho para a pasta de destino que hospedará os arquivos exportados.
* **[!UICONTROL Tipo de compactação]**: Selecione o tipo de compactação como GZIP ou NONE.

>[!TIP]
>
>No workflow de destino de conexão, você pode criar uma pasta personalizada no armazenamento Amazon S3 por arquivo de segmento exportado. Ler [Use macros para criar uma pasta no seu local de armazenamento](/help/destinations/catalog/cloud-storage/overview.md#use-macros) para obter instruções.

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o guia sobre [inscrever-se em alertas de destinos usando a interface do usuário](../../ui/alerts.md).

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

### Mapear atributos e identidades {#map}

No **[!UICONTROL Mapeamento]** , é possível selecionar quais campos de atributo e identidade serão exportados para seus perfis. Você também pode optar por alterar os cabeçalhos no arquivo exportado para qualquer nome amigável que desejar. Para obter mais informações, visualize o [etapa de mapeamento](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) no tutorial ativar interface do usuário de destinos em lote.

## Validar exportação de dados {#exported-data}

Para [!DNL Pega Profile Connector] destinos, [!DNL Platform] cria um `.csv` no local de armazenamento do Amazon S3 fornecido. Para obter mais informações sobre os arquivos, consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) no tutorial de ativação de segmento.

Uma importação bem-sucedida de dados de perfil do S3 insere dados no [!DNL Pega Customer] armazenamento de dados de perfil. Os dados de perfil do cliente importados podem ser validados em [!DNL Pega Customer Profile Designer] , como mostrado na figura a seguir.
![Imagem da tela da interface do usuário, onde é possível validar os dados do perfil do Adobe no Designer de perfil do cliente](../../assets/catalog/personalization/pega-profile/pega-profile-data.png)

Em [!DNL Pega Customer Decision Hub], os administradores de dados podem configurar tarefas de dados no [!DNL Customer Profile Designer] para importar dados de perfil periodicamente do S3, conforme mostrado na figura a seguir. Consulte a [recursos adicionais](#additional-resources) para obter mais informações sobre como configurar trabalhos de dados para importar dados de perfil do [!DNL Amazon S3].
![Imagem da tela da interface do usuário para configurar trabalhos de dados no Designer de perfil do cliente](../../assets/catalog/personalization/pega-profile/pega-profile-screen-image1.png)

## Recursos adicionais {#additional-resources}

Consulte [Importar trabalhos de dados](https://academy.pega.com/topic/import-data-jobs/v1) em [!DNL Pega Customer Decision Hub].

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [Visão geral da governança de dados](/help/data-governance/home.md).



