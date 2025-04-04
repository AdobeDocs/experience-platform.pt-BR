---
title: Criar uma conexão do Google Cloud Storage Source na interface
description: Saiba como criar uma conexão de origem do Google Cloud Storage usando a interface do Adobe Experience Platform.
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 3%

---

# Criar uma conexão de origem [!DNL Google Cloud Storage] na interface

Este tutorial fornece etapas para criar uma conexão de origem [!DNL Google Cloud Storage] usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão [!DNL Google Cloud Storage] válida, ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Formatos de arquivo compatíveis

[!DNL Experience Platform] dá suporte aos seguintes formatos de arquivo a serem assimilados de armazenamentos externos:

* Valores separados por delimitadores (DSV): qualquer valor com um único caractere pode ser usado como delimitador para arquivos de dados formatados em DSV.
* Notação de objeto do JavaScript (JSON): os arquivos de dados formatados em JSON devem ser compatíveis com XDM.
* Apache Parquet: os arquivos de dados formatados com Parquet devem ser compatíveis com XDM.

### Coletar credenciais necessárias

Para acessar os dados do [!DNL Google Cloud Storage] no Experience Platform, você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| ID da chave de acesso | Uma sequência de 61 caracteres alfanuméricos usada para autenticar sua conta do [!DNL Google Cloud Storage] no Experience Platform. |
| Chave de acesso secreta | Uma cadeia de 40 caracteres com codificação de base 64 usada para autenticar sua conta do [!DNL Google Cloud Storage] no Experience Platform. |
| Nome do bucket | O nome do seu bucket [!DNL Google Cloud Storage]. Você deve especificar um nome de bucket se quiser fornecer acesso a uma subpasta específica no armazenamento na nuvem. |
| Caminho da pasta | O caminho para a pasta à qual você deseja fornecer acesso. |

Para obter mais informações sobre esses valores, consulte o guia [Chaves HMAC do Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Para obter etapas sobre como gerar sua própria ID da chave de acesso e chave de acesso secreta, consulte a [[!DNL Google Cloud Storage] visão geral](../../../../connectors/cloud-storage/google-cloud-storage.md).

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular sua conta do [!DNL Google Cloud Storage] à Experience Platform.

## Conectar sua conta do [!DNL Google Cloud Storage]

Na interface do usuário do Experience Platform, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria [!UICONTROL Armazenamento na nuvem], selecione **[!UICONTROL Armazenamento na nuvem do Google]** e **[!UICONTROL Adicionar dados]**.

![A tela da interface do usuário do Experience Platform exibindo a página do catálogo de fontes.](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

A página **[!UICONTROL Conectar-se ao Google Cloud Storage]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL Google Cloud Storage] com a qual deseja se conectar e clique em **[!UICONTROL Avançar]** para continuar.

![A tela da interface do usuário do Experience Platform exibindo a página da conta existente para uma fonte do Google Cloud Storage](../../../../images/tutorials/create/google-cloud-storage/existing.png)

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que aparece, forneça um nome, uma descrição opcional e suas credenciais do [!DNL Google Cloud Storage]. Durante essa etapa, também é possível designar as subpastas às quais sua conta terá acesso definindo o nome do caminho para a subpasta.

Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![A tela da interface do usuário do Experience Platform exibindo a nova página da conta para uma fonte do Google Cloud Storage.](../../../../images/tutorials/create/google-cloud-storage/new.png)


## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua conta do [!DNL Google Cloud Storage]. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados do seu armazenamento em nuvem para o Experience Platform](../../dataflow/batch/cloud-storage.md).
