---
title: (Beta) Conexão Gen2 do Armazenamento Azure Data Lake
description: Saiba como se conectar ao Armazenamento Azure Data Lake Gen2 para ativar segmentos e exportar conjuntos de dados.
exl-id: d265a02d-c901-4b39-8714-fe9ecdbb5bb1
source-git-commit: a07557ec398631ece0c8af6ec7b32e0e8593e24b
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 1%

---

# (Beta) [!DNL Azure Data Lake Storage Gen2] conexão

>[!IMPORTANT]
>
>No momento, esse destino está na versão Beta e só está disponível para um número limitado de clientes. Para solicitar acesso à [!DNL Azure Data Lake Storage Gen2] entre em contato com o representante do Adobe e forneça [!DNL Organization ID].

## Visão geral {#overview}

Leia esta página para saber como criar uma conexão de saída em tempo real com seu [[!DNL Azure Data Lake Storage Gen2]](https://learn.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) ([!DNL ADLS Gen2]) data lake para exportar periodicamente arquivos de dados do Experience Platform.

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, juntamente com os campos de esquema aplicáveis (por exemplo, seu PPID), conforme escolhido na tela selecionar atributos de perfil do [fluxo de trabalho de ativação de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Em lote]** | Destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos com base em arquivo em lote](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Pré-requisitos {#prerequisites}

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](/help/destinations/ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para destino {#authenticate}

Para autenticar para o destino, preencha os campos obrigatórios e selecione **[!UICONTROL Ligar ao destino]**.

* **[!UICONTROL URL]**: O terminal para [!DNL Azure Data Lake Storage Gen2]. O padrão de ponto de extremidade é: `https://<accountname>.dfs.core.windows.net`.
* **[!UICONTROL Tenant]**: As informações do locatário que contêm seu aplicativo.
* **[!UICONTROL ID da entidade de serviço]**: A ID de cliente do aplicativo.
* **[!UICONTROL Chave de entidade de serviço]**: A chave do aplicativo.
* **[!UICONTROL Chave de criptografia]**: Opcionalmente, é possível anexar sua chave pública formatada em RSA para adicionar criptografia aos arquivos exportados. Exiba um exemplo de uma chave de criptografia corretamente formatada na imagem abaixo.

   ![Imagem que mostra um exemplo de uma chave PGP formatada corretamente na interface do usuário](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Preencha os detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: Preencha o nome preferencial para esse destino.
* **[!UICONTROL Descrição]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Caminho da pasta]**: Insira o caminho para a pasta de destino que hospedará os arquivos exportados.
* **[!UICONTROL Tipo de arquivo]**: selecione o Experience Platform format que deve ser usado para os arquivos exportados. Ao selecionar o [!UICONTROL CSV] , você também pode [configurar as opções de formatação de arquivo](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Formato de compactação]**: selecione o tipo de compactação que o Experience Platform deve usar para os arquivos exportados.

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o guia sobre [inscrever-se em alertas de destinos usando a interface do usuário](../../ui/alerts.md).

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

### Programação {#scheduling}

No **[!UICONTROL Agendamento]** , você pode [configurar o cronograma de exportação](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) para seu [!DNL Azure Data Lake Storage Gen2] e você também pode [configurar o nome dos arquivos exportados](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Mapear atributos e identidades {#map}

No **[!UICONTROL Mapeamento]** , é possível selecionar quais campos de atributo e identidade serão exportados para seus perfis. Você também pode optar por alterar os cabeçalhos no arquivo exportado para qualquer nome amigável que desejar. Para obter mais informações, visualize o [etapa de mapeamento](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) no tutorial ativar interface do usuário de destinos em lote.

## (Beta) Exportar conjuntos de dados {#export-datasets}

Esse destino é compatível com exportações de conjunto de dados. Para obter informações completas sobre como configurar exportações de conjunto de dados, leia a [tutorial exportar conjuntos de dados](/help/destinations/ui/export-datasets.md).

## Validar exportação de dados bem-sucedida {#exported-data}

Para verificar se os dados foram exportados com êxito, verifique seu [!DNL Azure Data Lake Storage Gen2] armazene e verifique se os arquivos exportados contêm as populações de perfis esperadas.
