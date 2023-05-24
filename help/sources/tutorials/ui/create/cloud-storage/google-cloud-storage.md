---
title: Criar uma conexão de origem de armazenamento na nuvem do Google na interface
description: Saiba como criar uma conexão de origem do Google Cloud Storage usando a interface do Adobe Experience Platform.
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: 7181cb92dd44d8005fe1054020ffeb36c309b42e
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 1%

---

# Criar um [!DNL Google Cloud Storage] conexão de origem na interface

Este tutorial fornece etapas para a criação de um [!DNL Google Cloud Storage] conexão de origem usando a interface do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL Google Cloud Storage] conexão, você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Formatos de arquivo não compatíveis

[!DNL Experience Platform] O suporta os seguintes formatos de arquivo para serem assimilados de armazenamentos externos:

* Valores separados por delimitadores (DSV): qualquer valor com um único caractere pode ser usado como delimitador para arquivos de dados formatados em DSV.
* Anotação de objeto JavaScript (JSON): os arquivos de dados formatados em JSON devem ser compatíveis com XDM.
* Apache Parquet: os arquivos de dados formatados com Parquet devem ser compatíveis com XDM.

### Coletar credenciais necessárias

Para acessar seu [!DNL Google Cloud Storage] dados na Platform, você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| ID da chave de acesso | Uma sequência de 61 caracteres alfanuméricos usada para autenticar seu [!DNL Google Cloud Storage] para a Platform. |
| Chave de acesso secreta | Uma string de 40 caracteres codificada em base 64 usada para autenticar seu [!DNL Google Cloud Storage] para a Platform. |
| Nome do bucket | O nome do seu [!DNL Google Cloud Storage] balde. Você deve especificar um nome de bucket se quiser fornecer acesso a uma subpasta específica no armazenamento na nuvem. |
| Caminho da pasta | O caminho para a pasta à qual você deseja fornecer acesso. |

Para obter mais informações sobre esses valores, consulte [Chaves HMAC do Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guia. Para obter etapas sobre como gerar sua própria ID da chave de acesso e chave de acesso secreta, consulte o [[!DNL Google Cloud Storage] visão geral](../../../../connectors/cloud-storage/google-cloud-storage.md).

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular [!DNL Google Cloud Storage] para a Platform.

## Conecte seu [!DNL Google Cloud Storage] account

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na barra de navegação esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No [!UICONTROL armazenamento na nuvem] categoria, selecione **[!UICONTROL Armazenamento em nuvem Google]** e selecione **[!UICONTROL Adicionar dados]**.

![A tela Interface do usuário da Platform exibindo a página do catálogo de origens.](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

A variável **[!UICONTROL Conectar-se ao Google Cloud Storage]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Google Cloud Storage] conta à qual deseja se conectar e selecione **[!UICONTROL Próxima]** para continuar.

![A tela da interface do usuário da Platform que exibe a página da conta existente de uma fonte de armazenamento na nuvem da Google](../../../../images/tutorials/create/google-cloud-storage/existing.png)

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que aparece, forneça um nome, uma descrição opcional e [!DNL Google Cloud Storage] credenciais. Durante essa etapa, também é possível designar as subpastas às quais sua conta terá acesso definindo o nome do caminho para a subpasta.

Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para estabelecer a nova conexão.

![A tela da interface do usuário da Platform que exibe a nova página da conta para uma fonte de armazenamento na nuvem da Google.](../../../../images/tutorials/create/google-cloud-storage/new.png)


## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com o seu [!DNL Google Cloud Storage] conta. Agora você pode seguir para o próximo tutorial e [configure um fluxo de dados para trazer dados do armazenamento em nuvem para a Platform](../../dataflow/batch/cloud-storage.md).
