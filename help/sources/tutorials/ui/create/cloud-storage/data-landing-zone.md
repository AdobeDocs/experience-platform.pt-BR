---
keywords: Experience Platform, home, tópicos populares, Zona de aterrissagem de dados, zona de aterrissagem de dados
solution: Experience Platform
title: Conectar a zona de aterrissagem de dados à plataforma usando a interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar um conector de origem de zona de aterrissagem de dados usando a interface do usuário da plataforma.
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: b007cdf92811b453df5b5d005456a05cd845b769
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# Connect [!DNL Data Landing Zone] para Plataforma usando a interface do usuário

[!DNL Data Landing Zone] é um recurso de armazenamento de dados baseado em nuvem para armazenamento temporário de arquivos provisionado com o Adobe Experience Platform. Os dados são excluídos automaticamente do [!DNL Data Landing Zone] após sete dias.

Este tutorial fornece etapas para criar um [!DNL Data Landing Zone] conexão de origem usando a interface do usuário da plataforma.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Traga seus arquivos de [!DNL Data Landing Zone] para a plataforma

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

Em [!UICONTROL armazenamento na nuvem] categoria , selecione [!DNL Data Landing Zone] e depois selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/dlz/catalog.png)

O [!UICONTROL Adicionar dados] é exibida, fornecendo uma interface para selecionar e visualizar os dados que deseja trazer para a plataforma.

![add-data](../../../../images/tutorials/create/dlz/add-data.png)

Para obter um guia detalhado e passo a passo sobre como criar um fluxo de dados para uma fonte de armazenamento em nuvem, consulte o tutorial em [criação de um fluxo de dados de armazenamento em nuvem para trazer dados para o Platform](../../dataflow/batch/cloud-storage.md).

## Recupere e atualize seu [!DNL Data Landing Zone] credenciais

[!DNL Data Landing Zone] O é uma fonte pronta para uso que vem com a licença das Fontes do Adobe Experience Platform. [!DNL Data Landing Zone] O usa uma autenticação baseada em SAS URI e SAS Token. Você pode recuperar e atualizar suas credenciais de autenticação do [!UICONTROL Catálogo de origens] página.

No [!UICONTROL Catálogo de origens]nos termos do [!UICONTROL armazenamento na nuvem] selecione as reticências (**...**) do **[!UICONTROL Zona de aterrissagem de dados]** cartão. No menu suspenso exibido, selecione **[!UICONTROL Exibir credenciais]**.

![opções](../../../../images/tutorials/create/dlz/options.png)

Um provedor é exibido, exibindo o nome do contêiner, o token SAS, o nome da conta de armazenamento e o URI SAS.

Selecionar **[!UICONTROL Atualizar credenciais]** e aguarde alguns segundos para que suas credenciais atualizadas sejam processadas.

>[!TIP]
>
>Seu [!DNL Data Landing Zone] as credenciais são definidas para expirar automaticamente após 90 dias e você deve usar novas credenciais para se reconectar ao [!DNL Data Landing Zone] após a expiração. Seus fluxos de dados na Platform não são afetados pelas credenciais que estão expirando e você ainda pode continuar trabalhando com fluxos de dados novos e existentes com suas novas credenciais.

![view-credentials](../../../../images/tutorials/create/dlz/credentials.png)

## Próximas etapas

Ao seguir este tutorial, você acessou seu [!DNL Data Landing Zone] e aprendeu a recuperar e atualizar suas credenciais. Agora você pode prosseguir para o próximo tutorial em [criação de um fluxo de dados para trazer dados de um armazenamento em nuvem para a plataforma](../../dataflow/batch/cloud-storage.md).
