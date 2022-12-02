---
keywords: Experience Platform, interface do usuário, interface do usuário, painéis, painel, perfis, segmentos, destinos, uso de licença
title: Editar esquema para criar widgets de painel personalizados
description: Este guia fornece instruções passo a passo para selecionar atributos e configurar o esquema da sua organização para criar widgets personalizados para painéis do Adobe Experience Platform.
exl-id: a744eb24-5ba7-4971-9183-3f891e807863
source-git-commit: 9b89effa6f90fb513fac9d0b826722ab05020036
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# Editar esquema para criar widgets personalizados

Para criar widgets personalizados para painéis do Adobe Experience Platform, primeiro você deve identificar os atributos de Perfil do cliente em tempo real nos quais os widgets serão baseados.

Este guia fornece instruções passo a passo para editar o esquema da organização selecionando atributos para criar widgets de painel personalizados.

Depois que os atributos tiverem sido selecionados e o esquema tiver sido configurado, você poderá prosseguir com as etapas para [criação de widgets personalizados para seus painéis](custom-widgets.md).

>[!NOTE]
>
>Os usuários devem receber a permissão &quot;Gerenciar painéis padrão&quot; para poder editar o esquema. Para obter etapas sobre a concessão de permissões de acesso para painéis, consulte [guia de permissões do painel](../permissions.md).

## Biblioteca de widgets {#widget-library}

Este guia requer acesso ao [!UICONTROL Biblioteca de widgets] no Experience Platform. Para saber mais sobre a biblioteca de widgets e como acessá-la na interface do usuário, comece lendo o [visão geral da biblioteca de widgets](widget-library.md).

## Editar esquema

Na biblioteca de widgets, a variável **[!UICONTROL Personalizado]** A guia permite criar widgets e compartilhá-los com outros usuários em sua organização para personalizar a aparência dos painéis.

Antes de criar widgets personalizados, os atributos de Perfil do cliente em tempo real devem ser selecionados para garantir que os dados sejam incluídos como parte do instantâneo diário.

>[!IMPORTANT]
>
>Sua organização pode selecionar no máximo 20 atributos.

Se sua organização não selecionou atributos de perfil, comece selecionando **[!UICONTROL Configurar]** no centro da tela.

![A guia Personalizado do espaço de trabalho da biblioteca de widgets com Configurar , realçada.](../images/customization/configure-schema.png)

Quando pelo menos um atributo personalizado tiver sido criado, selecione **[!UICONTROL Editar esquema]** para exibir os atributos selecionados e adicionar mais.

![A guia Personalizado do espaço de trabalho da biblioteca de widgets com o esquema Editar é realçada.](../images/customization/edit-schema.png)

## Selecionar um atributo

Para selecionar um atributo na função **[!UICONTROL Selecionar campo de esquema de união]** , navegue até o atributo no esquema de união (ou use pesquisa) e marque a caixa de seleção ao lado do atributo. A seleção da caixa de seleção também adiciona o atributo ao **[!UICONTROL Atributos selecionados]** no lado direito da caixa de diálogo.

>[!NOTE]
>
>Para que um atributo fique visível para seleção, ele deve ser um dos seguintes: Sequência, Data, Data-Hora, Booleano, Curto, Longo, Número Inteiro ou Byte. Os tipos de dados Mapear e Duplicar não são suportados e ficam esmaecidos para que não possam ser selecionados.

Depois de escolher os atributos que deseja adicionar, selecione **[!UICONTROL Salvar]** para salvar seus atributos e retornar à guia widgets personalizados.

>[!WARNING]
>Os atributos recém-selecionados ficam disponíveis após o próximo instantâneo diário quando os dados são atualizados.

![A caixa de diálogo para selecionar atributos de esquema com atributos e Salvar realçado.](../images/customization/select-attribute.png)

## Próximas etapas

Após a leitura deste guia, você pode navegar até a biblioteca de widgets e selecionar Atributos de perfil do cliente em tempo real para configurar seu esquema. Com os atributos de perfil selecionados, você pode começar [criação de widgets personalizados para seus painéis](custom-widgets.md).
