---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem do Azure Blob ou Amazon S3 na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: 9fd00ec198f61843bb9a395103215e5441b23745
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 2%

---


# Criar um conector de origem do Azure Blob ou Amazon S3 na interface do usuário

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem do Azure Blob (a seguir denominado &quot;Blob&quot;) ou do Amazon S3 (a seguir denominado &quot;S3&quot;) usando a interface do usuário da plataforma.

## Introdução

Este tutorial requer uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

- [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual a plataforma Experience organiza os dados da experiência do cliente.
   - [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
- [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão básica Blob ou S3, poderá ignorar o restante desse documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Formatos de arquivo não suportados

A plataforma Experience suporta os seguintes formatos de arquivo para serem assimilados de armazenamentos externos:

- Valores separados por delimitador (DSV): Atualmente, o suporte para arquivos de dados formatados em DSV está limitado a valores separados por vírgulas. O valor dos cabeçalhos de campo nos arquivos formatados em DSV deve consistir apenas em caracteres alfanuméricos e sublinhados. O suporte para arquivos DSV gerais será fornecido no futuro.
- JSON (JavaScript Object Notation): Os arquivos de dados formatados JSON devem ser compatíveis com XDM.
- Parqueta Apache: Os arquivos de dados formatados do parâmetro devem ser compatíveis com XDM.

### Reunir credenciais obrigatórias

Para acessar seu armazenamento Blob na plataforma, é necessário fornecer um valor válido para a seguinte credencial:

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | A string de conexão necessária para acessar dados no armazenamento Blob. O padrão da string de conexão Blob é: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

Para obter mais informações sobre a introdução, visite [este documento](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string)Blob do Azure.

Da mesma forma, acessar seu bucket S3 na plataforma exige que você forneça seus valores válidos para as seguintes credenciais:

| Credencial | Descrição |
| ---------- | ----------- |
| `s3AccessKey` | A ID da chave de acesso para seu armazenamento S3. |
| `s3SecretKey` | A ID da chave secreta para seu armazenamento S3. |

Para obter mais informações sobre como começar, visite [este documento](https://aws.amazon.com/blogs/security/wheres-my-secret-access-key/)AWS.

## Conecte sua conta Blob ou S3

Depois de reunir as credenciais necessárias, siga as etapas abaixo para criar uma nova conta Blob ou S3 para se conectar à Plataforma.

Faça logon na [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho *[!UICONTROL Fontes]* . A tela *[!UICONTROL Catálogo]* exibe várias fontes nas quais você pode criar uma conta de entrada e cada fonte mostra o número de contas e fluxos de dados existentes associados a elas.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria *[!UICONTROL Bancos]* de Dados, selecione **[!UICONTROL Azure Blob Armazenamento]** ou **[!UICONTROL Amazon S3]** , clique **no ícone + (+)** para criar um novo conector Blob ou S3.

![catálogo](../../../../images/tutorials/create/blob/catalog.png)

A página *[!UICONTROL Conectar-se ao Armazenamento]* Blob do Azure é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça à conexão um nome, uma descrição opcional e suas credenciais do Blob ou S3. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conta ser estabelecida.

![connect](../../../../images/tutorials/create/blob/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta Blob ou S3 com a qual deseja se conectar e, em seguida, selecione **[!UICONTROL Avançar]** para continuar.

![existente](../../../../images/tutorials/create/blob/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta Blob ou S3. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados do seu armazenamento em nuvem para a Plataforma](../../dataflow/batch/cloud-storage.md).