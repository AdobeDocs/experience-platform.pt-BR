---
title: Conectar a zona de aterrissagem de dados à plataforma usando a interface do
description: Saiba como criar um conector de origem da Zona de aterrissagem de dados usando a interface do usuário da Platform.
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: cdcce07a5adf08bf9d5e6a08d6bc965d37458a5d
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---

# Conectar [!DNL Data Landing Zone] à Plataforma usando a interface

>[!IMPORTANT]
>
>Esta página é específica para o conector de [!DNL Data Landing Zone] *origem* no Experience Platform. Para obter informações sobre como se conectar ao conector de [!DNL Data Landing Zone] *destino*, consulte a [[!DNL Data Landing Zone] página de documentação de destino](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

O [!DNL Data Landing Zone] é um recurso de armazenamento de arquivos seguro e baseado em nuvem para trazer arquivos para a Adobe Experience Platform. Os dados são excluídos automaticamente do [!DNL Data Landing Zone] após sete dias.

Este tutorial fornece etapas para a criação de uma conexão de origem [!DNL Data Landing Zone] usando a interface do usuário da Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Trazer seus arquivos do [!DNL Data Landing Zone] para a Platform

>[!IMPORTANT]
>
> Para se conectar à origem, você precisa das **[!UICONTROL Exibir Fontes]** e **[!UICONTROL Gerenciar Fontes]** permissões de controle de acesso. Leia a [visão geral do controle de acesso](../../../../../access-control/home.md) ou contate o administrador do produto para obter as permissões necessárias.

Na interface da Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

Na categoria [!UICONTROL armazenamento na nuvem], selecione [!DNL Data Landing Zone] e **[!UICONTROL Adicionar dados]**.

![O catálogo de fontes com a Zona de Aterrissagem de Dados selecionada.](../../../../images/tutorials/create/dlz/catalog.png)

A etapa [!UICONTROL Adicionar dados] é exibida, fornecendo uma interface para selecionar e visualizar os dados que você deseja trazer para a Platform.

* A parte esquerda da interface é um navegador de pastas, que fornece uma lista de arquivos do container que você pode trazer para a Platform.
* A parte direita da interface permite visualizar até 100 linhas de dados de um arquivo compatível.

Selecione o arquivo que deseja trazer para o Experience Platform e aguarde alguns momentos para que a interface correta seja atualizada em uma tela de visualização.

![A interface de adição de dados do espaço de trabalho de fontes.](../../../../images/tutorials/create/dlz/add-data.png)

>[!TIP]
>
>A Platform detecta automaticamente as informações de propriedade do arquivo selecionado, incluindo informações sobre o formato de dados do arquivo, delimitador de coluna designado e tipo de compactação.

A interface de visualização permite inspecionar o conteúdo e a estrutura de um arquivo. Por padrão, a interface de visualização exibe o primeiro arquivo na pasta selecionada.

Para visualizar um arquivo diferente, selecione o ícone de visualização ao lado do nome do arquivo que deseja inspecionar.

Quando terminar, selecione **[!UICONTROL Próximo]**.

![A página de visualização de dados do espaço de trabalho de fontes.](../../../../images/tutorials/create/dlz/file-detection.png)

Para obter um guia passo a passo detalhado sobre como criar um fluxo de dados para uma fonte de armazenamento na nuvem, consulte o tutorial sobre [criação de um fluxo de dados de armazenamento na nuvem para trazer dados para a Platform](../../dataflow/batch/cloud-storage.md).

## Recupere suas credenciais do [!DNL Data Landing Zone]

[!DNL Data Landing Zone] é uma fonte que vem com sua licença de Fontes do Adobe Experience Platform. [!DNL Data Landing Zone] usa uma autenticação baseada em token SAS e URI SAS. Você pode recuperar suas credenciais de autenticação da página [!UICONTROL Catálogo de fontes].

Para recuperar suas credenciais, selecione o cartão **[!UICONTROL Zona de Aterrissagem de Dados]** e copie suas credenciais do painel direito exibido.

![Uma lista de opções de exibição para a Zona de Aterrissagem de Dados.](../../../../images/tutorials/create/dlz/view-credentials.png)

Um pop-over é exibido, exibindo o nome do container, o token SAS, o nome da conta de armazenamento, o URI SAS e a data de expiração.

## Atualize suas credenciais do [!DNL Data Landing Zone]

Suas credenciais do [!DNL Data Landing Zone] estão definidas para expirar automaticamente após 90 dias, e você deve usar novas credenciais para se reconectar ao [!DNL Data Landing Zone] após a expiração. Seus fluxos de dados no Experience Platform não são afetados pelas credenciais de expiração e você ainda pode continuar trabalhando com fluxos de dados novos e existentes com suas novas credenciais.

Há duas maneiras de atualizar suas credenciais do [!DNL Data Landing Zone]:

>[!BEGINTABS]

>[!TAB Usar o cartão de origem]

Para atualizar suas credenciais da página de catálogo de origens, selecione as reticências (**`...`**) no cartão [!DNL Data Landing Zone] e selecione **[!UICONTROL Atualizar credenciais]**.

![Atualizar credenciais usando o cartão de origem.](../../../../images/tutorials/create/dlz/refresh-with-card.png)

Uma janela pop-up é exibida, solicitando sua confirmação antes de você poder continuar. Quando estiver pronto, selecione **[!UICONTROL Atualizar credenciais]**.

![A janela de confirmação de atualização de credenciais.](../../../../images/tutorials/create/dlz/confirm.png)

>[!TAB Usar o painel direito]

Para atualizar suas credenciais usando o painel direito, selecione o cartão de origem **[!UICONTROL Zona de Aterrissagem de Dados]** e selecione **[!UICONTROL Mais ações]**. Em seguida, selecione **[!UICONTROL Atualizar credenciais]** e confirme usando a janela pop-up exibida.

![Atualize as credenciais usando o painel direito.](../../../../images/tutorials/create/dlz/refresh-with-right-rail.png)

>[!ENDTABS]

## Próximas etapas

Seguindo este tutorial, você acessou seu contêiner do [!DNL Data Landing Zone] e aprendeu a recuperar e atualizar suas credenciais. Agora você pode prosseguir para o próximo tutorial em [criando um fluxo de dados para trazer dados de um armazenamento em nuvem para a Platform](../../dataflow/batch/cloud-storage.md).
