---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem de Armazenamento do Google Cloud na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# Criar um conector de origem de Armazenamento do Google Cloud na interface do usuário

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem do Armazenamento do Google Cloud (a seguir denominado &quot;GCS&quot;) usando a interface do usuário da plataforma.

## Introdução

Este tutorial requer uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual a plataforma Experience organiza os dados da experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão básica GCS, poderá ignorar o restante deste documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/cloud-storage.md).

### Formatos de arquivo não suportados

A plataforma Experience suporta os seguintes formatos de arquivo para serem assimilados de armazenamentos externos:

* Valores separados por delimitador (DSV): Atualmente, o suporte para arquivos de dados formatados em DSV está limitado a valores separados por vírgulas. O valor dos cabeçalhos de campo nos arquivos formatados em DSV deve consistir apenas em caracteres alfanuméricos e sublinhados. O suporte para arquivos DSV gerais será fornecido no futuro.
* JSON (JavaScript Object Notation): Os arquivos de dados formatados JSON devem ser compatíveis com XDM.
* Parqueta Apache: Os arquivos de dados formatados do parâmetro devem ser compatíveis com XDM.

### Reunir credenciais obrigatórias

Para acessar seus dados GCS na Plataforma, é necessário fornecer uma ID **de chave de** acesso GCS e um **segredo** válidos. Você pode saber mais sobre como obter esses valores lendo o guia <a href="https://cloud.google.com/docs/authentication/production" target="_blank">de autenticação</a> servidor a servidor do Google Cloud.

## Conectar sua conta GCS

Depois de reunir as credenciais necessárias, siga as etapas abaixo para criar uma nova conexão básica de entrada para vincular sua conta GCS à Plataforma.

Faça logon na <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> e selecione **Fontes** na barra de navegação esquerda para acessar a área de trabalho *Fontes* . A tela *Catálogo* exibe várias fontes com as quais você pode criar conexões base de entrada e cada fonte mostra o número de conexões base existentes associadas a elas.

Na categoria do Armazenamento *da* Cloud, selecione Armazenamento **da** Google Cloud para exibir uma barra de informações no lado direito da tela. A barra de informações fornece uma breve descrição para a fonte selecionada, bem como opções para se conectar com a visualização de origem em sua documentação ou para se conectar com a fonte. Para criar uma nova conexão básica de entrada, clique em **Conectar fonte**.

![](../../../../images/tutorials/create/google-cloud-storage/sources-catalog.png)

A caixa de diálogo _Conectar-se ao Armazenamento_ do Google Cloud é exibida. No formulário de entrada, forneça um nome à conexão básica, uma descrição opcional e suas credenciais GCS. Quando terminar, clique em **Conectar** e aguarde algum tempo para que a nova conexão básica seja estabelecida.

![](../../../../images/tutorials/create/google-cloud-storage/gcs-credentials.png)

Depois que uma conexão básica for estabelecida, você poderá continuar até a próxima seção e configurar um fluxo de dados para trazer dados para a Plataforma.

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão básica com sua conta GCS. Agora você pode continuar com o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Plataforma](../../dataflow/cloud-storage.md).