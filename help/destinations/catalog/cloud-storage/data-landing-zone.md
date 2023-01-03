---
title: Destino da zona de aterrissagem de dados
description: Saiba como se conectar à Zona de aterrissagem de dados para ativar segmentos e exportar conjuntos de dados.
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# (Beta) Destino da zona de aterrissagem de dados

>[!IMPORTANT]
>
>No momento, esse destino está na versão Beta e só está disponível para um número limitado de clientes. Para solicitar acesso à [!DNL Data Landing Zone] entre em contato com o representante do Adobe e forneça [!DNL Organization ID].


## Visão geral {#overview}

[!DNL Data Landing Zone] é um [!DNL Azure Blob] interface de armazenamento provisionada pela Adobe Experience Platform, que concede acesso a um recurso de armazenamento de arquivos seguro e baseado em nuvem para exportar arquivos da Platform. Você tem acesso a um [!DNL Data Landing Zone] por sandbox, e o volume total de dados em todos os contêineres está limitado aos dados totais fornecidos com sua licença de Produtos e Serviços da plataforma . Todos os clientes da Platform e seus serviços de aplicativos, como [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services]e [!DNL Real-Time Customer Data Platform] são provisionados com um [!DNL Data Landing Zone] contêiner por sandbox. Você pode ler e gravar arquivos no contêiner por meio de [!DNL Azure Storage Explorer] ou sua interface de linha de comando.

[!DNL Data Landing Zone] O suporta autenticação baseada em SAS e seus dados estão protegidos com o padrão [!DNL Azure Blob] mecanismos de segurança de armazenamento em repouso e em trânsito. A autenticação baseada em SAS permite que você acesse com segurança sua [!DNL Data Landing Zone] por meio de uma conexão pública com a Internet. Não são necessárias alterações de rede para que você acesse seu [!DNL Data Landing Zone] , o que significa que não é necessário configurar nenhuma configuração lista de permissões ou entre regiões para sua rede.

A Platform impõe um TTL (time-to-live) estrito de sete dias em todos os arquivos carregados em um [!DNL Data Landing Zone] contêiner. Todos os arquivos são excluídos após sete dias.

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, juntamente com os campos de esquema aplicáveis (por exemplo, seu PPID), conforme escolhido na tela selecionar atributos de perfil do [fluxo de trabalho de ativação de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Lote]** | Destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos com base em arquivo em lote](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Gerencie o conteúdo de seu [!DNL Data Landing Zone]

Você pode usar [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/features/storage-explorer/) para gerenciar o conteúdo de sua [!DNL Data Landing Zone] contêiner.

No [!DNL Azure Storage Explorer] Na interface do usuário, selecione o ícone de conexão na barra de navegação esquerda. O **Selecionar recurso** for exibida, fornecendo opções para conexão. Selecionar **[!DNL Blob container]** para se conectar ao seu [!DNL Data Landing Zone] armazenamento.

![select-resource](/help/sources/images/tutorials/create/dlz/select-resource.png)

Em seguida, selecione **URL de assinatura de acesso compartilhado (SAS)** como seu método de conexão e selecione **Próximo**.

![select-connection-method](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

Após selecionar o método de conexão, você deve fornecer um **nome de exibição** e **[!DNL Blob]URL SAS do contêiner** que corresponde ao seu [!DNL Data Landing Zone] contêiner.

>[!IMPORTANT]
>
>Você deve usar as APIs da plataforma para recuperar as credenciais da Zona de aterrissagem de dados. Para obter informações completas, consulte [Recuperar credenciais da Zona de aterrissagem de dados](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/create/cloud-storage/data-landing-zone.html?lang=en#retrieve-data-landing-zone-credentials).
>
> Para recuperar as credenciais e acessar os arquivos exportados, você deve substituir o parâmetro de consulta `type=user_drop_zone` com `type=dlz_destination` em qualquer chamada HTTP descrita na página acima.

Forneça sua [!DNL Data Landing Zone] URL SAS e selecione **Próximo**.

![enter-connection-info](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

O **Resumo** for exibida, fornecendo uma visão geral de suas configurações, incluindo informações sobre [!DNL Blob] endpoint e permissões. Quando estiver pronto, selecione **Connect**.

![resumo](/help/sources/images/tutorials/create/dlz/summary.png)

Uma conexão bem-sucedida atualiza sua [!DNL Azure Storage Explorer] Interface do usuário com seu [!DNL Data Landing Zone] contêiner.

![dlz-user-container](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

Com seu [!DNL Data Landing Zone] contêiner conectado a [!DNL Azure Storage Explorer], agora você pode começar a exportar arquivos do Experience Platform para seu [!DNL Data Landing Zone] contêiner. Para exportar arquivos, é necessário estabelecer uma conexão com o [!DNL Data Landing Zone] na interface do usuário do Experience Platform, conforme descrito na seção abaixo.

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para destino {#authenticate}

Porque [!DNL Data Landing Zone] for um armazenamento provisionado pelo Adobe, não é necessário executar etapas para autenticar para o destino.

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

### Programação

No **[!UICONTROL Agendamento]** , você pode [configurar o cronograma de exportação](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) para seu [!DNL Data Landing Zone] e você também pode [configurar o nome dos arquivos exportados](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Mapear atributos e identidades {#map}

No **[!UICONTROL Mapeamento]** , é possível selecionar quais campos de atributo e identidade serão exportados para seus perfis. Você também pode optar por alterar os cabeçalhos no arquivo exportado para qualquer nome amigável que desejar. Para obter mais informações, visualize o [etapa de mapeamento](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) no tutorial ativar interface do usuário de destinos em lote.

## (Beta) Exportar conjuntos de dados {#export-datasets}

Esse destino é compatível com exportações de conjunto de dados. Para obter informações completas sobre como configurar exportações de conjunto de dados, leia a [tutorial exportar conjuntos de dados](/help/destinations/ui/export-datasets.md).

## Validar exportação de dados bem-sucedida {#exported-data}

Para verificar se os dados foram exportados com êxito, verifique seu [!DNL Data Landing Zone] armazene e verifique se os arquivos exportados contêm as populações de perfis esperadas.
