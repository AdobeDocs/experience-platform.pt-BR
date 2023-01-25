---
title: Criar uma conexão da fonte de armazenamento da Google Cloud na interface do usuário
description: Saiba como criar uma conexão de origem de armazenamento do Google Cloud usando a interface do usuário do Adobe Experience Platform.
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: 7181cb92dd44d8005fe1054020ffeb36c309b42e
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 1%

---

# Crie um [!DNL Google Cloud Storage] conexão de origem na interface do usuário

Este tutorial fornece etapas para criar um [!DNL Google Cloud Storage] conexão de origem usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL Google Cloud Storage] , você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Formatos de arquivo não compatíveis

[!DNL Experience Platform] O suporta os seguintes formatos de arquivo a serem assimilados de armazenamentos externos:

* Valores separados por delimitador (DSV): Qualquer valor de caractere único pode ser usado como delimitador para arquivos de dados formatados em DSV.
* Notação de objeto JavaScript (JSON): Os arquivos de dados formatados JSON devem ser compatíveis com XDM.
* Parqueta Apache: Os arquivos de dados formatados do parâmetro devem ser compatíveis com XDM.

### Obter credenciais necessárias

Para acessar o [!DNL Google Cloud Storage] no Platform, você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| ID da chave de acesso | Uma sequência de 61 caracteres alfanuméricos usada para autenticar o [!DNL Google Cloud Storage] para a Platform. |
| Chave de acesso secreta | Uma string codificada em 40 caracteres, base e 64, usada para autenticar seu [!DNL Google Cloud Storage] para a Platform. |
| Nome do bucket | O nome da sua [!DNL Google Cloud Storage] balde. Você deve especificar um nome de bucket se quiser fornecer acesso a uma subpasta específica no armazenamento na nuvem. |
| Caminho da pasta | O caminho para a pasta à qual você deseja fornecer acesso. |

Para obter mais informações sobre esses valores, consulte o [Chaves HMAC do Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guia. Para obter etapas sobre como gerar sua própria ID de chave de acesso e chave de acesso secreta, consulte [[!DNL Google Cloud Storage] visão geral](../../../../connectors/cloud-storage/google-cloud-storage.md).

Depois de reunir suas credenciais necessárias, siga as etapas abaixo para vincular seus [!DNL Google Cloud Storage] para a Platform.

## Conecte seu [!DNL Google Cloud Storage] account

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em [!UICONTROL armazenamento na nuvem] categoria , selecione **[!UICONTROL Armazenamento em nuvem Google]** e depois selecione **[!UICONTROL Adicionar dados]**.

![A tela da interface do usuário da plataforma que exibe a página de catálogo de fontes.](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

O **[!UICONTROL Conectar-se ao Google Cloud Storage]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Google Cloud Storage] conta com a qual deseja se conectar e selecione **[!UICONTROL Próximo]** para continuar.

![A tela da interface do usuário da plataforma que exibe a página de conta existente para uma fonte de armazenamento da Google Cloud](../../../../images/tutorials/create/google-cloud-storage/existing.png)

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e [!DNL Google Cloud Storage] credenciais. Durante essa etapa, também é possível designar as subpastas às quais sua conta terá acesso, definindo o nome do caminho para a subpasta.

Quando terminar, selecione **[!UICONTROL Conectar-se à origem]** e, em seguida, permitir que a nova conexão seja estabelecida.

![A tela da interface do usuário da plataforma que exibe a nova página de conta de uma fonte de armazenamento da Google Cloud.](../../../../images/tutorials/create/google-cloud-storage/new.png)


## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com seu [!DNL Google Cloud Storage] conta. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados do armazenamento em nuvem para a Platform](../../dataflow/batch/cloud-storage.md).
