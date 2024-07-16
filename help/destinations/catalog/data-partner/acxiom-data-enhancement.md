---
title: Aprimoramento de dados da Acxiom
description: Use esse conector para ativar perfis de Adobe primários no Real-Time CDP para Acxiom para enriquecimento de dados e usar em canais de marketing. Em seguida, você pode usar a origem Acxiom para importar os perfis com dados aprimorados e trabalhar com eles no Real-Time CDP.
last-substantial-update: 2024-03-14T00:00:00Z
badge: Beta
exl-id: 59edc43d-ae8e-4c3d-820c-b5be1c4483f9
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1346'
ht-degree: 3%

---

# [!DNL Acxiom Data Enhancement] conexão de destino

>[!NOTE]
>
>O destino [!DNL Acxiom Data Enhancement] está na versão beta.  Esse conector de destino e a página de documentação são criados e mantidos pela equipe da Acxiom. Para quaisquer consultas ou solicitações de atualização, entre em contato diretamente em acxiom-adobe-help@acxiom.com.

## Visão geral {#overview}

Use o conector [!DNL Acxiom Data Enhancement] para fornecer dados descritivos adicionais aos perfis do cliente, para uso em aplicativos de análise, segmentação e direcionamento. Com centenas de elementos disponíveis, você pode segmentar e modelar melhor os dados, resultando em direcionamento mais preciso e modelagem preditiva.

![Diagrama de marketing para exportar dados primários para a Acxiom e, em seguida, importar dados enriquecidos de volta para o Real-Time CDP](/help/destinations/assets/catalog/data-partner/acxiom/marketing-workflow-data-enhancement.png)

Este tutorial fornece etapas para criar uma conexão de destino e um fluxo de dados do [!DNL Acxiom Data Enhancement] usando a interface do usuário do Adobe Experience Platform. Esse conector é usado para fornecer dados ao serviço de aprimoramento da Acxiom usando o Amazon S3 como ponto de queda.

![O catálogo de destino com o destino Acxiom selecionado.](../../assets/catalog/data-partner/acxiom/image-destination-enhancement-catalog.png)

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o destino [!DNL Acxiom Data Enhancement], veja a seguir exemplos de casos de uso que os clientes da Adobe Experience Platform podem resolver usando esse destino.

### Aprimorar os dados do cliente {#enhance-customer-data}

Esse conector deve ser usado por profissionais de marketing que visem melhorar a eficácia de suas estratégias de alcance, anexando elementos descritivos selecionados aos perfis dos clientes e usando-os para direcionar melhor as campanhas.

Por exemplo, como profissional de marketing, você pode querer aprofundar sua compreensão dos públicos-alvo existentes enriquecendo os perfis com dados adicionais. Isso melhorará sua segmentação e estratégias de direcionamento, resultando em um aumento na personalização e conversão da campanha.

O caso de uso é executado por meio de uma combinação de conectores de destino e de origem.

Você pode começar exportando seus registros de clientes existentes para enriquecimento usando esse conector de destino. O serviço da Acxiom pesquisaria o arquivo, recuperaria-o, enriqueceria-o com os dados da Acxiom e geraria um arquivo.

O cliente usaria o cartão de origem [Assimilação de dados da Acxiom](/help/sources/connectors/data-partners/acxiom-data-ingestion.md) correspondente para assimilar os perfis hidratados do cliente de volta na Adobe Real-Time CDP.

## Pré-requisitos {#prerequisites}

>[!IMPORTANT]
>
>* Para se conectar ao destino, você precisa de **[!UICONTROL Exibir Destinos]** e **[!UICONTROL Gerenciar Destinos]**, **[!UICONTROL Ativar Destinos]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL permissão Exibir Gráfico de Identidade]** [controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve que tipo de público-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
|-----------------------------|-----------|---------------------------------------------------------------------------------------------------------------------|
| [!DNL Segmentation Service] | ✓ | Públicos gerados por meio do [Serviço de segmentação](../../../segmentation/home.md) do Experience Platform. |
| Uploads personalizados | x | Públicos [importados](../../../segmentation/ui/audience-portal.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}


## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|------------------|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, juntamente com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos de perfil do [fluxo de trabalho de ativação de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Lote]** | Os destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos com base em arquivo de lote](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
>
>Para se conectar ao destino, você precisa de **[!UICONTROL Exibir Destinos]** e **[!UICONTROL Gerenciar e Ativar Destinos de Conjuntos de Dados]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow da configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Conectar ao destino]**.

Para acessar seu bucket no Experience Platform, é necessário fornecer valores válidos para as seguintes credenciais:

| Credencial | Descrição |
|---------------|----------------------------------------------------------------------------------------------------------|
| Chave de acesso S3 | A ID da chave de acesso do seu bucket. Você pode recuperar esse valor da equipe [!DNL Acxiom]. |
| Chave secreta S3 | A ID da chave secreta para o seu bucket. Você pode recuperar esse valor da equipe [!DNL Acxiom]. |
| Nome do bucket | Esse é o seu bucket onde os arquivos serão compartilhados. Você pode recuperar esse valor da equipe [!DNL Acxiom]. |

### Nova conta

Para definir um novo local do Acxiom Managed S3:

![Nova Conta](../../assets/catalog/data-partner/acxiom/image-destination-new-account.png)

### Conta existente

As contas já definidas usando o destino [!DNL Acxiom Data Enhancement] aparecem em um pop-up de lista. Quando selecionada, você poderá ver os detalhes da conta no painel direito. Veja o exemplo da interface do usuário ao navegar até **[!UICONTROL Destinos]** > **[!UICONTROL Contas]**;

![Conta Existente](../../assets/catalog/data-partner/acxiom/image-destination-enhancement-account.png)

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Detalhes do destino](../../assets/catalog/data-partner/acxiom/image-destination-details.png)

* **Nome (Obrigatório)** - O nome com o qual o destino será salvo
* **Descrição** - Breve explicação da finalidade do destino
* **Nome do bucket (obrigatório)** - Nome do bucket do Amazon S3 configurado no S3
* **Caminho da Pasta (Obrigatório)** - Se os subdiretórios em um compartimento forem usados, um caminho deverá ser definido ou &#39;/&#39; para fazer referência ao caminho raiz.
* **Tipo de arquivo** - Selecione o formato que o Experience Platform deve usar para os arquivos exportados. Atualmente, o único tipo de arquivo que o processamento da Acxiom espera é o CSV

>[!IMPORTANT]
>
>Ao selecionar a opção CSV *Delimitador*, *Aspas*, *Caracteres de Escape*, *Valor Vazio*, *Valor Nulo*, *Formato de compactação* e *Incluir arquivo de manifesto*, as opções serão apresentadas. O documento a seguir explica essas configurações com mais detalhes [configure as opções de formatação](../../ui/batch-destinations-file-formatting-options.md).

![Opções de CSV](../../assets/catalog/data-partner/acxiom/image-destination-csv-options.png)

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Avançar]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
>
>* Para ativar dados, você precisa de **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Ativar Destinos]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL permissão Exibir Gráfico de Identidade]** [controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Leia [Ativar dados de público-alvo para destinos de exportação de perfil em lote](/help/destinations/ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

### Sugestões de mapeamento

O processamento correto de arquivos no lado da Acxiom requer elementos de nome e endereço. Embora nem todos os elementos sejam necessários, fornecer o máximo possível ajudará na correspondência bem-sucedida.

As sugestões de mapeamento são fornecidas na tabela abaixo, listando os atributos no seu lado de destino que são usados pelo processamento da Acxiom para os quais os clientes podem mapear atributos de perfil. Trate esses elementos como sugestões, pois nem todos os elementos são necessários e os valores de origem dependerão das necessidades da conta.

| Campo de público alvo | Descrição do Source |
|--------------|-------------------------------------------------------------|
| name | O valor `person.name.fullName` em Experience Platform. |
| firstName | O valor `person.name.firstName` em Experience Platform. |
| lastName | O valor `person.name.lastName` em Experience Platform. |
| address1 | O valor `mailingAddress.street1` em Experience Platform. |
| address2 | O valor `mailingAddress.street2` em Experience Platform. |
| city | O valor `mailingAddress.city` em Experience Platform. |
| estado | O valor `mailingAddress.state` em Experience Platform. |
| zip | O valor `mailingAddress.postalCode` em Experience Platform. |

>[!NOTE]
>
>Se você mapear campos adicionais não listados acima no fluxo de dados, eles serão incluídos na exportação de dados, mas serão ignorados pelo processamento da Acxiom.

## Validar exportação de dados {#exported-data}

Para verificar se os dados foram exportados com êxito, verifique o bucket [!DNL Amazon S3 Storage] e se os arquivos exportados contêm as populações de perfis esperadas.

## Próximas etapas

Seguindo este tutorial, você criou com êxito um fluxo de dados para exportar dados do perfil do Experience Platform para sua localização do S3 gerenciado pelo [!DNL Acxiom]. Em seguida, entre em contato com o representante da Acxiom com o nome da conta, os nomes dos arquivos e o caminho do bucket para que o processamento possa ser configurado.

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia a [Visão geral da Governança de Dados](/help/data-governance/home.md).

## Recursos adicionais {#additional-resources}

*Acxiom Infobase:* https://www.acxiom.com/wp-content/uploads/2022/02/fs-acxiom-infobase_AC-0268-22.pdf
