---
title: Visão geral dos eventos de transmissão capilares
description: Saiba como transmitir dados do Capilary para o Experience Platform.
badge: Beta
exl-id: 3b8eb2f6-3b4a-4b91-89d4-b6d9027c6ab4
source-git-commit: 428aed259343f56a2bf493b40ff2388340fffb7b
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 1%

---

# [!DNL Capillary Streaming Events]

>[!AVAILABILITY]
>
>A origem [!DNL Capillary Streaming Events] está na versão beta. Leia os [termos e condições](../../home.md#terms-and-conditions) na visão geral das fontes para obter mais informações sobre como usar fontes com rótulo beta.

O [!DNL Capillary Technologies] é uma plataforma líder de fidelidade e engajamento, com a confiança de mais de 300 marcas em todo o mundo. Use a fonte [!DNL Capillary Streaming Events] para habilitar sua empresa a transmitir facilmente perfis de clientes, dados de fidelidade e eventos transacionais do [!DNL Capillary] para a Adobe Experience Platform. Conecte sua origem do [!DNL Capillary] para habilitar a personalização em tempo real, a segmentação avançada de público e a orquestração de campanhas omnicanal.

Ao integrar o [!DNL Capillary] ao Experience Platform, você pode:

* Sincronizar **pontos, camadas e recompensas de fidelidade** em tempo real.
* Enviar **dados transacionais** para o Experience Platform para análise e ativação.
* Aproveite o Real-Time CDP, o Experience Platform e o Adobe Journey Optimizer para segmentação, orquestração de jornadas e personalização.

## Pré-requisitos

Antes de conectar [!DNL Capillary] ao Adobe Experience Platform, verifique se você tem o seguinte:

* Uma **ID de organização da Adobe** válida e acesso a uma sandbox da Experience Platform habilitada.
* Você deve ter as permissões **[!UICONTROL Exibir Fontes]** e **[!UICONTROL Gerenciar Fontes]** habilitadas para sua conta a fim de conectar sua conta do [!DNL Capillary] à Experience Platform. Entre em contato com o administrador do produto para obter as permissões necessárias. Para obter mais informações, leia o [guia da interface do usuário de controle de acesso](../../../access-control/ui/overview.md).

### Criar um esquema

Você deve criar um esquema do Experience Data Model (XDM) para descrever um conjunto de dados que possa armazenar os possíveis campos e tipos de dados que serão enviados de [!DNL Capillary].

1. Faça logon no Adobe Experience Platform e acesse a Experience Platform por meio do logon da sua organização.
2. No painel de navegação esquerdo, selecione **[!UICONTROL Esquemas]** para abrir o espaço de trabalho [!UICONTROL Esquemas].
3. Selecione **[!UICONTROL Criar esquema]** no canto superior direito.
4. Na caixa de diálogo Criar esquema, escolha entre **[!UICONTROL Criação manual]** (Adicione você mesmo campos e grupos de campos) ou **[!UICONTROL Criação assistida por aprendizado de máquina]** (Carregue um arquivo CSV e use o aprendizado de máquina para gerar um esquema recomendado).
5. Escolha uma classe base para o esquema (por exemplo, Perfil individual XDM, XDM ExperienceEvent ou Outro). Se você selecionar **[!UICONTROL Outros]**, será possível selecionar dentre as classes personalizadas ou padrão disponíveis.
6. Insira um nome e uma descrição amigáveis para o esquema.
7. Use o Editor de esquemas para: adicionar grupos de campos (blocos de campos reutilizáveis), definir campos individuais (personalizar nomes, tipos de dados e opções) e, opcionalmente, criar tipos de dados personalizados ou grupos de campos, se os existentes não atenderem às suas necessidades.
8. Revise a estrutura do esquema na tela. Selecione **[!UICONTROL Concluir]** para criar o esquema.
9. (Opcional) Edite campos, adicione descrições e ajuste grupos de campos conforme necessário no Editor de esquemas.

Para obter instruções detalhadas sobre como criar um esquema XDM, leia o manual sobre [criação de um esquema usando o editor de esquemas](../../../xdm/tutorials/create-schema-ui.md).

### Criar um conjunto de dados

Em seguida, você deve criar um conjunto de dados que faça referência ao esquema que acabou de criar.

1. Na interface do Experience Platform, selecione [!UICONTROL Conjuntos de dados] na navegação à esquerda para abrir o espaço de trabalho [!UICONTROL Conjuntos de dados].
2. Selecione **[!UICONTROL Criar conjunto de dados]** na parte superior direita.
3. Nas opções de criação, selecione **[!UICONTROL Criar conjunto de dados do esquema]**.
4. Na lista, procure e selecione o esquema XDM criado anteriormente. Depois de localizar o esquema, selecione **[!UICONTROL Próximo]**.
5. Insira um nome descritivo e exclusivo para o conjunto de dados.
6. Opcionalmente, adicione uma descrição que ajude os futuros usuários a identificar o conjunto de dados.
7. Selecione **[!UICONTROL Concluir]** para criar o conjunto de dados.

Para obter instruções detalhadas sobre como criar um conjunto de dados, leia o [guia da interface do usuário de conjuntos de dados](../../../catalog/datasets/user-guide.md).

## Conectar [!DNL Capillary Streaming Events] ao Experience Platform

Depois de concluir a configuração de pré-requisito para [!DNL Capillary], leia o [[!DNL Capillary Streaming Events] tutorial da interface do usuário](../../tutorials/ui/create/loyalty/capillary.md) para saber como você pode conectar sua conta e transmitir dados do [!DNL Capillary] para a Experience Platform.
