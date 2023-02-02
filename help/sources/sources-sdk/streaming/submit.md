---
title: Teste E Envie Sua Fonte
description: O documento a seguir fornece etapas sobre como testar e verificar uma nova fonte usando a API do Serviço de Fluxo e integrar uma nova fonte por meio de Fontes de Autosserviço (SDK de Streaming).
hide: true
hidefromtoc: true
source-git-commit: 7744fef9751212a40f8f20df52812d38130c42fc
workflow-type: tm+mt
source-wordcount: '1249'
ht-degree: 0%

---

# Testar e enviar sua fonte

As etapas finais para integrar sua nova fonte ao Adobe Experience Platform usando o SDK de Fontes de autoatendimento (Streaming SDK) são testar e enviar sua nova fonte. Depois de concluir sua especificação de conexão e atualizar a especificação do fluxo de transmissão, você pode começar a testar a funcionalidade da fonte por meio da API ou da interface do usuário. Após ser bem-sucedido, é possível enviar sua nova fonte entrando em contato com o representante do Adobe.

O documento a seguir fornece etapas sobre como testar e depurar sua fonte usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

* Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../landing/api-guide.md).
* Para obter informações sobre como gerar suas credenciais para APIs da plataforma, consulte o tutorial em [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md).
* Para obter informações sobre como configurar [!DNL Postman] para APIs da plataforma, consulte o tutorial em [configurar o console do desenvolvedor e [!DNL Postman]](../../../landing/postman.md).
* Para ajudar no processo de teste e depuração, baixe a variável [Coleta e ambiente de verificação de Fontes de Autoatendimento aqui](../assets/sdk-verification.zip) e siga as etapas descritas abaixo.

## Teste sua fonte usando a API

Para testar sua fonte usando a API do , execute o [Coleta e ambiente de verificação de Fontes de Autoatendimento](../assets/sdk-verification.zip) on [!DNL Postman] ao mesmo tempo em que fornece as variáveis de ambiente apropriadas que pertencem à sua fonte.

Para iniciar os testes, primeiro configure a coleção e o ambiente em [!DNL Postman]. Em seguida, especifique a ID da especificação de conexão que deseja testar.

>[!NOTE]
>
>Todas as variáveis de exemplo abaixo são valores de espaço reservado que devem ser atualizados, exceto para `flowSpecificationId` e `targetConnectionSpecId`, que são valores fixos.

| Parâmetro | Descrição | Exemplo |
| --- | --- | --- |
| `x-api-key` | Um identificador exclusivo usado para autenticar chamadas para APIs do Experience Platform. Veja o tutorial em [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md) para obter informações sobre como recuperar seu `x-api-key`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | Uma entidade corporativa que pode ser proprietária ou licenciar produtos e serviços e permitir o acesso a seus membros. Veja o tutorial em [configurar o console do desenvolvedor e [!DNL Postman]](../../../landing/postman.md) para obter instruções sobre como recuperar seu `x-gw-ims-org-id` informações. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | O token de autorização necessário para concluir chamadas para APIs do Experience Platform. Veja o tutorial em [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md) para obter informações sobre como recuperar seu `authorizationToken`. | `Bearer authorizationToken` |
| `schemaId` | Para que os dados de origem sejam usados na Platform, um schema de target deve ser criado para estruturar os dados de origem de acordo com suas necessidades. Para obter etapas detalhadas sobre como criar um esquema XDM de destino, consulte o tutorial em [criação de um schema usando a API](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | A versão exclusiva que corresponde ao esquema. | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | O `meta:altId` que é retornado junto com o  `schemaId` ao criar um novo schema. | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | Para obter etapas detalhadas sobre como criar um conjunto de dados de destino, consulte o tutorial em [criação de um conjunto de dados usando a API](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | Conjuntos de mapeamento podem ser usados para definir como os dados em um schema de origem mapeiam para o de um schema de destino. Para obter etapas detalhadas sobre como criar um mapeamento, consulte o tutorial em [criação de um conjunto de mapeamento usando a API](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | A ID exclusiva que corresponde ao conjunto de mapeamentos. | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | A ID da especificação de conexão que corresponde à sua origem. Essa é a ID que você gerou depois [criação de uma nova especificação de conexão](./create.md). | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | A ID de especificação de fluxo de `GenericStreamingAEP`. **Este é um valor fixo**. | `e77fde5a-22a8-11ed-861d-0242ac120002` |
| `targetConnectionSpecId` | A ID de conexão de destino do lago de dados onde os dados ingeridos chegam. **Este é um valor fixo**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | O intervalo de tempo designado a ser seguido ao verificar a conclusão de uma execução de fluxo. | `40` |
| `startTime` | A hora de início designada para o fluxo de dados. A hora de início deve ser formatada em horário unix. | `1597784298` |

Depois de fornecer todas as variáveis de ambiente, você pode começar a executar a coleção usando o [!DNL Postman] interface. No [!DNL Postman] selecione as reticências (**...**) ao lado [!DNL Sources SSSs Verification Collection] e depois selecione **Executar coleção**.

![corredor](../assets/runner.png)

O [!DNL Runner] for exibida, permitindo configurar a ordem de execução do fluxo de dados. Selecionar **Executar Coleta de Verificação SSS** para executar a coleção.

>[!NOTE]
>
>Você pode desativar **Excluir fluxo** na lista de verificação da ordem de execução, se preferir usar o painel de monitoramento de fontes na interface do usuário da plataforma. No entanto, uma vez terminado o teste, você deve garantir que os fluxos de teste sejam excluídos.

![run-collection](../assets/run-collection.png)

## Teste sua fonte usando a interface do usuário do

Para testar sua fonte na interface do usuário, vá para o catálogo de fontes da sandbox de sua organização na interface do usuário da plataforma. A partir daqui, você deve ver sua nova fonte aparecer abaixo do *Streaming* categoria .

Com sua nova fonte disponível agora na sandbox, você deve seguir o fluxo de trabalho de fontes para testar as funcionalidades. Para começar, selecione **[!UICONTROL Configurar]**.

![O catálogo de fontes que exibe a nova fonte de transmissão.](../assets/testing/catalog-test.png)

O [!UICONTROL Adicionar dados] será exibida. Para testar se sua fonte pode fazer o stream de dados, use o lado esquerdo da interface para fazer upload [uma amostra de dados JSON](../assets/testing/raw.json.zip). Depois que os dados são carregados, o lado direito da interface é atualizado em uma pré-visualização da hierarquia de arquivos dos dados. Selecionar **[!UICONTROL Próximo]** para continuar.

![A etapa para adicionar dados no fluxo de trabalho das fontes, onde é possível fazer upload e visualizar seus dados antes da assimilação.](../assets/testing/add-data-test.png)

O [!UICONTROL Detalhes do fluxo de dados] permite selecionar se deseja usar um conjunto de dados existente ou um novo conjunto de dados. Durante esse processo, você também pode configurar seus dados para serem assimilados no Perfil e ativar configurações como [!UICONTROL Diagnóstico de erros] e [!UICONTROL Ingestão parcial].

Para teste, selecione **[!UICONTROL Novo conjunto de dados]** e fornecer um nome de conjunto de dados de saída. Durante essa etapa, você também pode fornecer uma descrição opcional para adicionar mais informações ao conjunto de dados. Em seguida, selecione um esquema para mapear usando o [!UICONTROL Pesquisa avançada] ou rolando pela lista de schemas existentes no menu suspenso. Depois de selecionar um esquema, forneça um nome e uma descrição para o seu fluxo de dados.

Quando terminar, selecione **[!UICONTROL Próximo]**.

![A etapa de detalhes do fluxo de dados no fluxo de trabalho de fontes.](../assets/testing/dataflow-details-test.png)

O [!UICONTROL Mapeamento] é exibida, fornecendo uma interface para mapear os campos de origem do esquema de origem para os campos XDM de destino apropriados no esquema de destino.

A Platform fornece recomendações inteligentes para campos mapeados automaticamente com base no esquema de destino ou conjunto de dados selecionado. Você pode ajustar manualmente as regras de mapeamento de acordo com seus casos de uso. Com base em suas necessidades, você pode optar por mapear campos diretamente ou usar funções de preparação de dados para transformar dados de origem em valores calculados ou calculados. Para obter etapas abrangentes sobre o uso da interface do mapeador e dos campos calculados, consulte o [Guia da interface do usuário de preparação de dados](../../../data-prep/ui/mapping.md)

Depois que os dados de origem forem mapeados com êxito, selecione **[!UICONTROL Próximo]**.

![A etapa de mapeamento do fluxo de trabalho de origens.](../assets/testing/mapping-test.png)

O **[!UICONTROL Revisão]** é exibida, permitindo que você revise o novo fluxo de dados antes de criá-lo. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: Exibe o nome da conta, o tipo de origem e outras informações diversas específicas da fonte de armazenamento da nuvem de transmissão que você está usando.
* **[!UICONTROL Atribuir conjunto de dados e mapear campos]**: Exibe o conjunto de dados de destino e o esquema usado para o fluxo de dados.

Depois de revisar o fluxo de dados, selecione **[!UICONTROL Concluir]** e permitir que o fluxo de dados seja criado.

![A etapa de revisão do fluxo de trabalho de fontes.](../assets/testing/review-test.png)

Por fim, você deve recuperar o ponto de extremidade de transmissão do fluxo de dados. Esse terminal será usado para se inscrever no webhook, permitindo que sua fonte de transmissão se comunique com o Experience Platform. Para recuperar o terminal de transmissão, acesse [!UICONTROL Atividade do fluxo de dados] página do fluxo de dados que você acabou de criar e copiar o ponto de extremidade da parte inferior do [!UICONTROL Propriedades] painel.

![O endpoint de transmissão na atividade de fluxo de dados.](../assets/testing/endpoint-test.png)

## Enviar sua fonte

Assim que sua fonte puder concluir o fluxo de trabalho inteiro, você poderá continuar a entrar em contato com o representante do Adobe e enviar sua fonte para integração em outras organizações do Experience Platform.
