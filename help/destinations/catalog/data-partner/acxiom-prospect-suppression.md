---
title: Acxiom Prospect-Suppression
description: Exporte seus públicos-alvo primários para o destino da Acxiom, para permitir que a Acxiom suprima clientes conhecidos ou convertidos. Em seguida, use o conector de origem da Acxiom para assimilar e ativar listas de clientes potenciais da Acxiom, com seus clientes conhecidos ou convertidos removidos.
last-substantial-update: 2024-03-14T00:00:00Z
badge: Beta
source-git-commit: c35eec2b83f92a7fb165bad13213ec50a6c9863e
workflow-type: tm+mt
source-wordcount: '1466'
ht-degree: 2%

---

# [!DNL Acxiom Prospect-Suppression] conexão de destino

>[!NOTE]
>
>A variável [!DNL Acxiom Prospect-Suppression] o destino está na versão beta. Esse conector de destino e a página de documentação são criados e mantidos pela equipe da Acxiom. Para quaisquer consultas ou solicitações de atualização, entre em contato diretamente em acxiom-adobe-help@acxiom.com.

## Visão geral {#overview}

Uso [!DNL Acxiom Prospect-Suppression] para fornecer os públicos-alvo mais produtivos possíveis. Esse conector exporta com segurança os dados primários do Real-time Customer Data Platform e os executa por meio de uma resolução premiada de higiene e identidade que produz um arquivo de dados para ser usado como uma lista de supressão. Isso será comparado com o [!DNL Acxiom Global] banco de dados que permite que as listas de clientes potenciais sejam personalizadas para importação. Em seguida, use o [[!DNL Acxiom Prospecting Data Import]](/help/sources/connectors/data-partners/acxiom-prospecting-data-import.md) conector de origem para listas de clientes potenciais da Acxiom de volta para a Real-Time CDP, com seus clientes conhecidos ou convertidos removidos.

![Diagrama de marketing para exportar dados primários para a Acxiom e, em seguida, importar dados de clientes potenciais de volta para o Real-Time CDP](/help/destinations/assets/catalog/data-partner/acxiom/marketing-workflow.png)

A Acxiom oferece os públicos-alvo de melhor desempenho do setor, com o maior catálogo de mais de 12.000 atributos de dados globais, concentrados especificamente no fornecimento de experiências personalizadas. Aproveite combinações ilimitadas de dados de alta qualidade para criar e distribuir públicos para atender às necessidades específicas da campanha.

Este tutorial fornece etapas para criar um [!DNL Acxiom Prospect-Suppression] conexão de destino e fluxo de dados usando a interface do usuário do Adobe Experience Platform. Esse conector é usado para fornecer dados ao serviço de prospecto da Acxiom usando o Amazon S3 como um ponto de partida. Entre em contato com o representante de conta da Acxiom depois de começar a exportar arquivos para o ponto de depósito do Amazon S3.

![O catálogo de destino com o destino Acxiom selecionado.](../../assets/catalog/data-partner/acxiom/image-destination-catalog.png)

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o [!DNL Acxiom Prospect-Suppression] destino, aqui estão exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Criar uma lista de supressão para conjuntos de dados de prospecção {#create-suppression-list}

Profissionais de marketing que visam melhorar a eficácia de suas estratégias de alcance geralmente empregam a criação de uma lista de supressão. Essa lista inclui clientes existentes e segmentos específicos, garantindo sua exclusão das atividades de prospecção durante campanhas direcionadas. Essa abordagem estratégica ajuda a refinar o público-alvo, evita comunicação redundante e contribui para um esforço de marketing mais focado e eficiente.

Por exemplo, como profissional de marketing, talvez você queira ampliar o alcance da campanha adicionando perfis de prospecto direcionados às suas campanhas com base nos critérios de segmentação e supressão fornecidos.

O caso de uso é executado por meio de uma combinação de conectores de destino e de origem.

Inicialmente, você começaria exportando seus perfis de clientes existentes usando esse conector de destino para ser usado como um arquivo de supressão. Isso garante que nenhum registro de cliente existente seja incluído.

O serviço da Acxiom pesquisaria o arquivo, recuperaria-o e o usaria junto com outros critérios de seleção e geraria um arquivo de prospecto. Em seguida, você usaria a variável correspondente [[!DNL Acxiom Prospecting Data Import]](/help/sources/connectors/data-partners/acxiom-prospecting-data-import.md) conector de origem para assimilar os perfis de cliente potencial no Adobe Real-Time CDP.

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
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Exibir destinos]** e **[!UICONTROL Gerenciar destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

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

Contas já definidas usando o [!DNL Acxiom Prospect Suppression] destino aparecem em um pop-up de lista. Quando selecionada, você poderá ver os detalhes da conta no painel direito. Veja o exemplo da interface do usuário ao navegar para **[!UICONTROL Destinos]** > **[!UICONTROL Contas]**:

![Conta existente](../../assets/catalog/data-partner/acxiom/image-destination-account.png)

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

O processamento requer elementos de nome e endereço, enquanto nem todos os elementos são necessários, fornecendo o máximo possível para ajudar na correspondência bem-sucedida.  As sugestões de mapeamento são fornecidas na tabela abaixo, listando os atributos no seu lado de destino que são usados pelo processamento da Acxiom para os quais os clientes podem mapear atributos de perfil.  Isso deve ser tratado como sugestões, pois nem todos os elementos são necessários e os valores de origem dependerão das necessidades da conta.

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

{style="table-layout:auto"}

>[!NOTE]
>
>Campos adicionais não listados acima serão incluídos na exportação, mas serão ignorados pelo processamento da Acxiom.

## Revisar seu fluxo de dados

Use a página de revisão para obter um resumo do seu fluxo de dados antes do envio

![Consulte a seção](../../assets/catalog/data-partner/acxiom/image-destination-review.png)

## Validar exportação de dados {#exported-data}

Para verificar se os dados foram exportados com êxito, verifique [!DNL Amazon S3 Storage] e verifique se os arquivos exportados contêm as populações de perfis esperadas.

## Próximas etapas

Ao seguir este tutorial, você criou com sucesso um fluxo de dados para exportar dados em lote do Experience Platform para o seu [!DNL Acxiom] local do S3 gerenciado. Você precisaria entrar em contato com o representante da Acxiom com o nome da conta, nome do arquivo e caminho do bucket para que o processamento possa ser configurado.

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia o [Visão geral da governança de dados](/help/data-governance/home.md).

## Recursos adicionais {#additional-resources}

*Distribuição e dados de público-alvo da Acxiom:* https://www.acxiom.com/customer-data/audience-data-distribution/
