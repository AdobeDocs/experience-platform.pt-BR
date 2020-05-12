---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem do Azure Blob ou Amazon S3 na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: 799445eca080175e2bffc49c6714f0c812b9bbea
workflow-type: tm+mt
source-wordcount: '558'
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

Para acessar seu armazenamento Blob na plataforma, você deve fornecer uma string **de conexão válida do Armazenamento** Azure. Você pode saber mais sobre sequências de conexão, incluindo maneiras de obtê-las por meio <a href="https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string" target="_blank">deste documento</a>do Microsoft Azure.

Da mesma forma, acessar seu bucket S3 na plataforma requer que você forneça sua chave **de acesso** S3 e chave **secreta** S3. For more information, refer to <a href="https://aws.amazon.com/blogs/security/wheres-my-secret-access-key/" target="_blank">this AWS document</a>.

## Conecte sua conta Blob ou S3

Com suas credenciais de armazenamento em nuvem prontas, você pode seguir as etapas abaixo para criar uma nova conexão básica de entrada para vincular sua conta Blob ou S3 à Plataforma.

Faça logon na <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> e selecione **Fontes** na barra de navegação esquerda para acessar a área de trabalho de fontes. A tela *Catálogo* exibe várias fontes com as quais você pode criar conexões base de entrada e cada fonte mostra o número de conexões base existentes associadas a elas.

Na categoria do Armazenamento *da* Cloud, selecione o Armazenamento **Blob do** Azure ou o **Amazon S3** para exibir uma barra de informações no lado direito da tela. A barra de informações fornece uma breve descrição para a fonte selecionada, bem como opções para visualização de sua documentação ou para conexão com a fonte. Para criar uma nova conexão básica de entrada, clique em **Conectar fonte**.

![](../../../../images/tutorials/create/s3/s3_sources_catalog.png)

No formulário de entrada, forneça um nome, uma descrição opcional e suas credenciais do Blob ou S3. Por fim, clique em **Conectar** e aguarde algum tempo para que a nova conexão básica seja estabelecida.

![](../../../../images/tutorials/create/s3/s3_credentials.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão básica para sua conta do Azure Blob ou Amazon S3. Agora você pode continuar com o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Plataforma](../../dataflow/batch/cloud-storage.md).