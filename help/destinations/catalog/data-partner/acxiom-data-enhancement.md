---
title: Aprimoramento de dados da Acxiom
description: Use esse conector para ativar perfis de Adobe primários no Real-Time CDP para Acxiom para enriquecimento de dados e usar em canais de marketing. Em seguida, você pode usar a origem Acxiom para importar os perfis com dados aprimorados e trabalhar com eles no Real-Time CDP.
last-substantial-update: 2024-03-14T00:00:00Z
badge: Beta
source-git-commit: c35eec2b83f92a7fb165bad13213ec50a6c9863e
workflow-type: tm+mt
source-wordcount: '1346'
ht-degree: 2%

---

# [!DNL Acxiom Data Enhancement] conexão de destino

>[!NOTE]
>
>A variável [!DNL Acxiom Data Enhancement] o destino está na versão beta.  Esse conector de destino e a página de documentação são criados e mantidos pela equipe da Acxiom. Para quaisquer consultas ou solicitações de atualização, entre em contato diretamente em acxiom-adobe-help@acxiom.com.

## Visão geral {#overview}

Use o [!DNL Acxiom Data Enhancement] conector para fornecer dados descritivos adicionais aos perfis do cliente, para uso em aplicativos de análise, segmentação e direcionamento. Com centenas de elementos disponíveis, você pode segmentar e modelar melhor os dados, resultando em direcionamento mais preciso e modelagem preditiva.

![Diagrama de marketing para exportar dados primários para a Acxiom e, em seguida, importar dados enriquecidos de volta para o Real-Time CDP](/help/destinations/assets/catalog/data-partner/acxiom/marketing-workflow-data-enhancement.png)

Este tutorial fornece etapas para criar um [!DNL Acxiom Data Enhancement] conexão de destino e fluxo de dados usando a interface do usuário do Adobe Experience Platform. Esse conector é usado para fornecer dados ao serviço de aprimoramento da Acxiom usando o Amazon S3 como ponto de queda.

![O catálogo de destino com o destino Acxiom selecionado.](../../assets/catalog/data-partner/acxiom/image-destination-enhancement-catalog.png)

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o [!DNL Acxiom Data Enhancement] destino, aqui estão exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Aprimorar os dados do cliente {#enhance-customer-data}

Esse conector deve ser usado por profissionais de marketing que visem melhorar a eficácia de suas estratégias de alcance, anexando elementos descritivos selecionados aos perfis dos clientes e usando-os para direcionar melhor as campanhas.

Por exemplo, como profissional de marketing, você pode querer aprofundar sua compreensão dos públicos-alvo existentes enriquecendo os perfis com dados adicionais. Isso melhorará sua segmentação e estratégias de direcionamento, resultando em um aumento na personalização e conversão da campanha.

O caso de uso é executado por meio de uma combinação de conectores de destino e de origem.

Você pode começar exportando seus registros de clientes existentes para enriquecimento usando esse conector de destino. O serviço da Acxiom pesquisaria o arquivo, recuperaria-o, enriqueceria-o com os dados da Acxiom e geraria um arquivo.

Em seguida, o cliente utilizaria o [Assimilação de dados da Acxiom](/help/sources/connectors/data-partners/acxiom-data-ingestion.md) cartão-fonte para assimilar os perfis hidratados do cliente de volta na Adobe Real-Time CDP.

## Pré-requisitos {#prerequisites}

>[!IMPORTANT]
>
>* Para se conectar ao destino, você precisa da variável **[!UICONTROL Exibir destinos]** e **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisará do **[!UICONTROL Exibir gráfico de identidade]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos."){width="100" zoomable="yes"}

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve que tipo de público-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
|-----------------------------|-----------|---------------------------------------------------------------------------------------------------------------------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo Experience Platform [Serviço de segmentação](../../../segmentation/home.md). |
| Uploads personalizados | x | Públicos-alvo [importado](../../../segmentation/ui/overview.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}


## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|------------------|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, juntamente com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos de perfil da [workflow de ativação de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Lote]** | Os destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos baseados em arquivo em lote](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
>
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Exibir destinos]** e **[!UICONTROL Gerenciar e ativar destinos do conjunto de dados]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow da configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Conectar ao destino]**.

Para acessar seu bucket no Experience Platform, é necessário fornecer valores válidos para as seguintes credenciais:

| Credencial | Descrição |
|---------------|----------------------------------------------------------------------------------------------------------|
| Chave de acesso S3 | A ID da chave de acesso do seu bucket. Você pode recuperar esse valor da variável [!DNL Acxiom] equipe. |
| Chave secreta S3 | A ID da chave secreta para o seu bucket. Você pode recuperar esse valor da variável [!DNL Acxiom] equipe. |
| Nome do bucket | Esse é o seu bucket onde os arquivos serão compartilhados. Você pode recuperar esse valor da variável [!DNL Acxiom] equipe. |

### Nova conta

Para definir um novo local do Acxiom Managed S3:

![Nova conta](../../assets/catalog/data-partner/acxiom/image-destination-new-account.png)

### Conta existente

Contas já definidas usando o [!DNL Acxiom Data Enhancement] destino aparecem em um pop-up de lista. Quando selecionada, você poderá ver os detalhes da conta no painel direito. Veja o exemplo da interface do usuário ao navegar para **[!UICONTROL Destinos]** > **[!UICONTROL Contas]**;

![Conta existente](../../assets/catalog/data-partner/acxiom/image-destination-enhancement-account.png)

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Detalhe do destino](../../assets/catalog/data-partner/acxiom/image-destination-details.png)

* **Nome (obrigatório)** - O nome em que o destino será salvo
* **Descrição** - Breve explicação da finalidade do destino
* **Nome do Período (Obrigatório)** - Nome do bucket do Amazon S3 configurado no S3
* **Caminho da pasta (obrigatório)** - Se os subdiretórios em um bucket forem usados, um caminho deverá ser definido, ou &#39;/&#39; para fazer referência ao caminho raiz.
* **Tipo de arquivo** - Selecione o formato que o Experience Platform deve usar para os arquivos exportados. Atualmente, o único tipo de arquivo que o processamento da Acxiom espera é o CSV

>[!IMPORTANT]
>
>Ao selecionar a opção CSV, *Delimitador*, *Caractere de citação*, *Caractere de escape*, *Valor vazio*, *Valor nulo*, *Formato de compactação*, e *Incluir arquivo de manifesto* opções serão apresentadas, o documento a seguir explica essas configurações com mais detalhes [configurar as opções de formatação](../../ui/batch-destinations-file-formatting-options.md).

![Opções de CSV](../../assets/catalog/data-partner/acxiom/image-destination-csv-options.png)

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
>
>* Para ativar os dados, é necessário **[!UICONTROL Exibir destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisará do **[!UICONTROL Exibir gráfico de identidade]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos."){width="100" zoomable="yes"}

Ler [Ativar dados do público-alvo para destinos de exportação de perfil em lote](/help/destinations/ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

### Sugestões de mapeamento

O processamento correto de arquivos no lado da Acxiom requer elementos de nome e endereço. Embora nem todos os elementos sejam necessários, fornecer o máximo possível ajudará na correspondência bem-sucedida.

As sugestões de mapeamento são fornecidas na tabela abaixo, listando os atributos no seu lado de destino que são usados pelo processamento da Acxiom para os quais os clientes podem mapear atributos de perfil. Trate esses elementos como sugestões, pois nem todos os elementos são necessários e os valores de origem dependerão das necessidades da conta.

| Campo de destino | Descrição da origem |
|--------------|-------------------------------------------------------------|
| name | A variável `person.name.fullName` valor em Experience Platform. |
| firstName | A variável `person.name.firstName` valor em Experience Platform. |
| lastName | A variável `person.name.lastName` valor em Experience Platform. |
| address1 | A variável `mailingAddress.street1` valor em Experience Platform. |
| address2 | A variável `mailingAddress.street2` valor em Experience Platform. |
| city | A variável `mailingAddress.city` valor em Experience Platform. |
| estado | A variável `mailingAddress.state` valor em Experience Platform. |
| CEP | A variável `mailingAddress.postalCode` valor em Experience Platform. |

>[!NOTE]
>
>Se você mapear campos adicionais não listados acima no fluxo de dados, eles serão incluídos na exportação de dados, mas serão ignorados pelo processamento da Acxiom.

## Validar exportação de dados {#exported-data}

Para verificar se os dados foram exportados com êxito, verifique [!DNL Amazon S3 Storage] e verifique se os arquivos exportados contêm as populações de perfis esperadas.

## Próximas etapas

Ao seguir este tutorial, você criou com sucesso um fluxo de dados para exportar dados do perfil do Experience Platform para sua [!DNL Acxiom] local do S3 gerenciado. Em seguida, entre em contato com o representante da Acxiom com o nome da conta, os nomes dos arquivos e o caminho do bucket para que o processamento possa ser configurado.

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia o [Visão geral da governança de dados](/help/data-governance/home.md).

## Recursos adicionais {#additional-resources}

*Acxiom Infobase:* https://www.acxiom.com/wp-content/uploads/2022/02/fs-acxiom-infobase_AC-0268-22.pdf
