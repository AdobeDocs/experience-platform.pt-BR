---
title: Testar E Enviar Seu Source
description: O documento a seguir fornece etapas sobre como testar e verificar uma nova fonte usando a API do Serviço de fluxo e integrar uma nova fonte por meio de Fontes de autoatendimento (Streaming SDK).
exl-id: 2ae0c3ad-1501-42ab-aaaa-319acea94ec2
badge: Beta
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 0%

---

# Testar e enviar sua origem

>[!NOTE]
>
>Fontes de autoatendimento A transmissão de SDK está na versão beta. Leia a [visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

As etapas finais para integrar sua nova fonte à Adobe Experience Platform usando Fontes de autoatendimento (SDK de transmissão) são testar e enviar sua nova fonte. Depois de concluir a especificação de conexão e atualizar a especificação do fluxo de transmissão, você pode começar a testar a funcionalidade da fonte por meio da API ou da interface do usuário. Depois de obter sucesso, você pode enviar sua nova fonte entrando em contato com o representante da Adobe.

O documento a seguir fornece etapas sobre como testar e depurar sua origem usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

* Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../landing/api-guide.md).
* Para obter informações sobre como gerar suas credenciais para as APIs do Experience Platform, consulte o tutorial sobre [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md).
* Para obter informações sobre como configurar o [!DNL Postman] para APIs do Experience Platform, consulte o tutorial em [configuração do console do desenvolvedor e [!DNL Postman]](../../../landing/postman.md).
* Para ajudar no processo de teste e depuração, baixe a [coleção e o ambiente de verificação de Fontes de Autoatendimento aqui](../assets/sdk-verification.zip) e siga as etapas descritas abaixo.

## Testar sua fonte usando a API

Para testar sua fonte usando a API, você deve executar a [coleção e o ambiente de verificação de Fontes de Autoatendimento](../assets/sdk-verification.zip) em [!DNL Postman] enquanto fornece as variáveis de ambiente apropriadas que pertencem à sua fonte.

Para iniciar o teste, primeiro você deve configurar a coleção e o ambiente em [!DNL Postman]. Em seguida, especifique a ID de especificação de conexão que deseja testar.

>[!NOTE]
>
>Todas as variáveis de exemplo abaixo são valores de espaço reservado que você deve atualizar, exceto para `flowSpecificationId` e `targetConnectionSpecId`, que são valores fixos.

| Parâmetro | Descrição | Exemplo |
| --- | --- | --- |
| `x-api-key` | Um identificador exclusivo usado para autenticar chamadas para APIs do Experience Platform. Consulte o tutorial sobre [autenticação e acesso a APIs do Experience Platform](../../../landing/api-authentication.md) para obter informações sobre como recuperar o `x-api-key`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | Uma entidade corporativa que pode ser proprietária ou licenciar produtos e serviços e permitir acesso a seus membros. Consulte o tutorial em [configuração do console do desenvolvedor e [!DNL Postman]](../../../landing/postman.md) para obter instruções sobre como recuperar as informações de `x-gw-ims-org-id`. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | O token de autorização necessário para concluir chamadas para APIs do Experience Platform. Consulte o tutorial sobre [autenticação e acesso a APIs do Experience Platform](../../../landing/api-authentication.md) para obter informações sobre como recuperar o `authorizationToken`. | `Bearer authorizationToken` |
| `schemaId` | Para que os dados de origem sejam usados no Experience Platform, um esquema de destino deve ser criado para estruturar os dados de origem de acordo com suas necessidades. Para obter etapas detalhadas sobre como criar um esquema XDM de destino, consulte o tutorial sobre [criação de um esquema usando a API](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | A versão exclusiva que corresponde ao esquema. | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | O `meta:altId` que é retornado com o `schemaId` ao criar um novo esquema. | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | Para obter etapas detalhadas sobre como criar um conjunto de dados de destino, consulte o tutorial sobre [criação de um conjunto de dados usando a API](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | Os conjuntos de mapeamento podem ser usados para definir como os dados em um esquema de origem são mapeados para o de um esquema de destino. Para obter etapas detalhadas sobre como criar um mapeamento, consulte o tutorial sobre [criação de um conjunto de mapeamento usando a API](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | O identificador exclusivo que corresponde ao seu conjunto de mapeamento. | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | A ID de especificação de conexão que corresponde à sua origem. Esta é a ID gerada após [criar uma nova especificação de conexão](./create.md). | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | A ID da especificação de fluxo de `GenericStreamingAEP`. **Valor fixo**. | `e77fde5a-22a8-11ed-861d-0242ac120002` |
| `targetConnectionSpecId` | A ID de conexão de destino do data lake onde os dados assimilados chegam. **Valor fixo**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | O intervalo de tempo designado a ser seguido ao verificar a conclusão de uma execução de fluxo. | `40` |
| `startTime` | A hora de início designada para seu fluxo de dados. A hora inicial deve ser formatada em hora unix. | `1597784298` |

Depois de fornecer todas as variáveis de ambiente, você pode começar a executar a coleção usando a interface [!DNL Postman]. Na interface [!DNL Postman], selecione as reticências (**...**) ao lado de [!DNL Sources SSSs Verification Collection] e selecione **Executar coleção**.

![executor](../assets/runner.png)

A interface [!DNL Runner] é exibida, permitindo configurar a ordem de execução do fluxo de dados. Selecione **Executar Coleção de Verificação de SSS** para executar a coleção.

>[!NOTE]
>
>Você pode desabilitar **Excluir Fluxo** da lista de verificação de ordem de execução se preferir usar o painel de monitoramento de fontes na interface do Experience Platform. No entanto, após concluir o teste, é necessário garantir que os fluxos de teste sejam excluídos.

![executar-coleção](../assets/run-collection.png)

## Testar sua fonte usando a interface do

Para testar sua origem na interface do usuário, acesse o catálogo de origens da sandbox da sua organização na interface do usuário do Experience Platform. Aqui, você deve ver sua nova fonte na categoria *Streaming*.

Com a nova fonte agora disponível na sandbox, você deve seguir o fluxo de trabalho de fontes para testar as funcionalidades. Para começar, selecione **[!UICONTROL Configurar]**.

![O catálogo de fontes exibindo a nova fonte de streaming.](../assets/testing/catalog-test.png)

A etapa [!UICONTROL Adicionar dados] é exibida. Para testar se a fonte pode transmitir dados, use o lado esquerdo da interface para carregar [uma amostra de dados JSON](../assets/testing/raw.json.zip). Depois que os dados forem carregados, o lado direito da interface será atualizado para uma pré-visualização da hierarquia de arquivos dos dados. Selecione **[!UICONTROL Avançar]** para continuar.

![A etapa para adicionar dados no fluxo de trabalho de fontes na qual você pode carregar e visualizar os dados antes da assimilação.](../assets/testing/add-data-test.png)

A página [!UICONTROL Detalhes do fluxo de dados] permite selecionar se você deseja usar um conjunto de dados existente ou um novo conjunto de dados. Durante esse processo, você também pode configurar seus dados para serem assimilados no Perfil e habilitar configurações como [!UICONTROL Diagnóstico de erro] e [!UICONTROL Assimilação parcial].

Para testes, selecione **[!UICONTROL Novo conjunto de dados]** e forneça um nome de conjunto de dados de saída. Durante essa etapa, também é possível fornecer uma descrição opcional para adicionar mais informações ao conjunto de dados. Em seguida, selecione um esquema para mapear usando a opção [!UICONTROL Pesquisa avançada] ou rolando pela lista de esquemas existentes no menu suspenso. Depois de selecionar um esquema, forneça um nome e uma descrição para o fluxo de dados.

Quando terminar, selecione **[!UICONTROL Próximo]**.

![A etapa de detalhes do fluxo de dados no fluxo de trabalho de fontes.](../assets/testing/dataflow-details-test.png)

A etapa [!UICONTROL Mapeamento] é exibida, fornecendo uma interface para mapear os campos de origem do esquema de origem para os campos XDM de destino apropriados no esquema de destino.

O Experience Platform fornece recomendações inteligentes para campos mapeados automaticamente com base no esquema ou conjunto de dados de destino selecionado. Você pode ajustar manualmente as regras de mapeamento para atender aos seus casos de uso. Com base nas suas necessidades, você pode optar por mapear campos diretamente ou usar funções de preparação de dados para transformar dados de origem para derivar valores calculados ou calculados. Para obter etapas abrangentes sobre como usar a interface do mapeador e campos calculados, consulte o [guia da interface do Preparo de Dados](../../../data-prep/ui/mapping.md)

Depois que os dados de origem forem mapeados com êxito, selecione **[!UICONTROL Próximo]**.

![A etapa de mapeamento do fluxo de trabalho de origens.](../assets/testing/mapping-test.png)

A etapa **[!UICONTROL Revisão]** é exibida, permitindo que você revise seu novo fluxo de dados antes de ele ser criado. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: exibe o nome da sua conta, o tipo de origem e outras informações diversas específicas para a fonte de armazenamento da nuvem de streaming que você está usando.
* **[!UICONTROL Atribuir conjunto de dados e mapear campos]**: exibe o conjunto de dados e o esquema de destino que você está usando para o fluxo de dados.

Depois de revisar o fluxo de dados, selecione **[!UICONTROL Concluir]** e aguarde algum tempo para que o fluxo de dados seja criado.

![A etapa de revisão do fluxo de trabalho de fontes.](../assets/testing/review-test.png)

Por fim, você deve recuperar o ponto de extremidade de transmissão do fluxo de dados. Esse endpoint será usado para assinar seu webhook, permitindo que a fonte de streaming se comunique com o Experience Platform. Para recuperar o ponto de extremidade de streaming, vá para a página [!UICONTROL Atividade de fluxo de dados] do fluxo de dados que você acabou de criar e copie o ponto de extremidade da parte inferior do painel [!UICONTROL Propriedades].

![A extremidade de streaming na atividade de fluxo de dados.](../assets/testing/endpoint-test.png)

## Enviar sua fonte

Assim que a origem puder concluir todo o fluxo de trabalho, você poderá continuar a entrar em contato com o representante da Adobe e enviar a origem para integração em outras organizações da Experience Platform.
