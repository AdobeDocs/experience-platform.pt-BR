---
description: Saiba como criar um conector de origem do Adobe Analytics na interface do usuário para trazer dados de classificações para o Adobe Experience Platform.
title: Criar uma conexão do Adobe Analytics Source para dados de classificações na interface
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# Criar uma conexão de origem do Adobe Analytics para dados de classificações na interface

>[!TIP]
>
>Por padrão, os dados de classificações do Adobe Analytics são atualizados semanalmente. A assimilação de dados para seus dados de classificações será processada sete dias após a configuração inicial do fluxo de dados. A primeira carga assimila os dados inteiros e a assimilação semanal subsequente executa dados incrementais.

Leia este tutorial para obter etapas sobre como assimilar dados de classificações da Adobe Analytics na Adobe Experience Platform por meio da interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

O conector de origem de classificações do Analytics exige que os dados tenham sido migrados para a nova infraestrutura de classificações do Adobe Analytics antes do uso. Para confirmar o status de migração dos dados, entre em contato com a equipe de conta da Adobe.

## Selecione suas classificações

Na interface do Experience Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria *aplicativos do Adobe*, selecione **[!UICONTROL Adobe Analytics]** e **[!UICONTROL Configurar]**.

>[!TIP]
>
>As origens no catálogo de origens exibem a opção **[!UICONTROL Configurar]** se não houver uma conta autenticada. Após a autenticação da conta, a opção muda para **[!UICONTROL Adicionar dados]**.

![O catálogo de origens na interface do usuário do Experience Platform com a origem do Adobe Analytics selecionada.](../../../../images/tutorials/create/classifications/catalog.png)

Em seguida, selecione [!UICONTROL Classificações] e selecione os conjuntos de dados de classificações que você deseja assimilar na Experience Platform.

É possível selecionar até 30 conjuntos de dados de classificações diferentes para trazer para a Experience Platform. Todos os conjuntos de dados selecionados serão exibidos no painel direito. Quando terminar, selecione [!UICONTROL Avançar] para continuar.

![A página de classificações com vários conjuntos de dados de classificações selecionados.](../../../../images/tutorials/create/classifications/select.png)

## Revise suas classificações

A etapa **[!UICONTROL Revisão]** é exibida, permitindo que você revise os conjuntos de dados de classificações selecionados antes de criá-los. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: mostra a plataforma de origem e o status da conexão.
* **[!UICONTROL Tipo de dados]**: mostra o número de classificações selecionadas.
* **[!UICONTROL Agendamento]**: mostra a frequência de sincronização para os dados de classificações. **Observação**: os dados de classificações são atualizados semanalmente.

Depois de revisar o fluxo de dados, clique em **[!UICONTROL Concluir]** e aguarde algum tempo para que o fluxo de dados seja criado.

![A página de revisão dos dados de classificações do Adobe Analytics.](../../../../images/tutorials/create/classifications/review.png)

## Próximas etapas

Seguindo este tutorial, você criou um conector sata de classificações do Analytics que traz dados de classificações para a Experience Platform. Consulte os seguintes documentos para obter mais informações sobre [!DNL Analytics] e dados de classificações:

* [Visão geral do conector de origem do Adobe Analytics](../../../../connectors/adobe-applications/analytics.md)
* [Criar uma conexão de origem do Analytics para dados do conjunto de relatórios na interface](./analytics.md)
* [Sobre as classificações](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)
