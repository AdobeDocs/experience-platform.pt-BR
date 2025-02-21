---
solution: Experience Platform
title: Cumprimento do consentimento nas definições de segmento
description: Saiba como respeitar as preferências de consentimento do cliente para a coleta e o compartilhamento de dados pessoais em operações de segmentação.
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: bf0e5065e771b748ee9d6ae3c431e76f08552983
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---

# Cumprimento do consentimento nas definições de segmento

>[!NOTE]
>
>Este guia explica como aceitar consentimentos em **definições de segmento**.

As regulamentações legais de privacidade, como a [!DNL California Consumer Privacy Act] (CCPA), fornecem aos consumidores o direito de optar pela coleta ou compartilhamento de seus dados pessoais com terceiros. O Adobe Experience Platform fornece componentes padrão do Experience Data Model (XDM) destinados a capturar essas preferências de consentimento do cliente em dados de perfil do cliente em tempo real.

Se um cliente tiver retirado ou retido o consentimento para o compartilhamento de seus dados pessoais, é importante que sua organização honre essa preferência ao gerar públicos-alvo para atividades de marketing. Este documento descreve como integrar os valores de consentimento do cliente nas definições de segmento usando a interface do usuário do Experience Platform.

## Introdução

O cumprimento dos valores de consentimento do cliente requer uma compreensão dos vários serviços do [!DNL Adobe Experience Platform] envolvidos. Antes de iniciar este tutorial, verifique se você está familiarizado com os seguintes serviços:

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): a estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.
* [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): permite que você compile públicos a partir de dados de [!DNL Real-Time Customer Profile].

## Campos de esquema de consentimento

Para honrar os consentimentos e as preferências do cliente, um dos esquemas que faz parte do esquema de união do [!UICONTROL Perfil individual XDM] deve conter o grupo de campos padrão **[!UICONTROL Consentimentos e Preferências]**.

Para obter detalhes sobre a estrutura e o caso de uso pretendido de cada um dos atributos fornecidos pelo grupo de campos, consulte o [guia de referência de consentimentos e preferências](../../xdm/field-groups/profile/consents.md). Para obter instruções passo a passo sobre como adicionar um grupo de campos a um esquema, consulte o [Guia da interface do usuário do XDM](../../xdm/ui/resources/schemas.md#add-field-groups).

Depois que o grupo de campos for adicionado a um [esquema habilitado para perfil](../../xdm/ui/resources/schemas.md#profile) e seus campos forem usados para assimilar dados de consentimento do aplicativo de experiência, você poderá usar os atributos de consentimento coletados nas regras de segmento.

## Lidar com o consentimento na segmentação

Para garantir que perfis de recusa de participação não sejam incluídos nas definições de segmento, campos especiais devem ser adicionados às definições de segmento existentes e incluídos ao criar novas definições de segmento.

As etapas abaixo demonstram como adicionar os campos apropriados para dois tipos de sinalizadores de recusa:

1. [!UICONTROL Coleta de dados]
1. [!UICONTROL Compartilhar Dados]

>[!NOTE]
>
>Embora este guia se concentre nos dois sinalizadores de recusa acima, você também pode configurar as definições de segmento para incorporar sinais de consentimento adicionais. O [guia de referência de consentimentos e preferências](../../xdm/field-groups/profile/consents.md) fornece mais informações sobre cada uma dessas opções e seus casos de uso pretendidos.

Ao criar uma definição de segmento na interface, em **[!UICONTROL Atributos]**, navegue até **[!UICONTROL Perfil Individual XDM]** e selecione **[!UICONTROL Consentimentos e Preferências]**, seguido de **[!UICONTROL Específico de ID]**. Aqui, você pode ver as opções para **[!UICONTROL Coleção de Dados]** e **[!UICONTROL Compartilhar Dados]**.

![](../images/tutorials/opt-outs/consents.png)

Comece selecionando a categoria **[!UICONTROL Coleção de dados]** e arraste **[!UICONTROL Valor de opção]** para o construtor de segmentos. Ao adicionar o atributo à definição do segmento, você pode especificar os [valores de consentimento](../../xdm/field-groups/profile/consents.md#choice-values) que devem ser incluídos ou excluídos.

![](../images/tutorials/opt-outs/consent-values.png)

Uma abordagem é excluir todos os clientes que optaram por não ter seus dados coletados. Para fazer isso, defina o operador como **[!UICONTROL não é igual a]** e escolha os seguintes valores:

* **[!UICONTROL Não (recusar)]**
* **[!UICONTROL Padrão de Não (recusar)]**
* **[!UICONTROL Desconhecido]** (se o consentimento for presumido como retido caso seja desconhecido)

![](../images/tutorials/opt-outs/collect.png)

Em **[!UICONTROL Atributos]** no painel esquerdo, navegue de volta para a seção **[!UICONTROL Consentimentos e Preferências]** e selecione **[!UICONTROL Compartilhar Dados]**. Arraste seu **[!UICONTROL Valor de Escolha]** correspondente para a tela e selecione os mesmos valores que os da opção de valor [!UICONTROL Coleção de Dados]. Verifique se uma relação **[!UICONTROL Or]** está estabelecida entre os dois atributos.

![](../images/tutorials/opt-outs/share.png)

Com os valores de consentimento **[!UICONTROL Coleta de dados]** e **[!UICONTROL Compartilhar dados]** adicionados à definição de segmento, todos os clientes que optaram por não ter seus dados usados serão excluídos do público resultante. Aqui, você pode continuar personalizando a definição do segmento antes de selecionar **[!UICONTROL Salvar]** para concluir o processo.

## Próximas etapas

Seguindo este tutorial, você deve ter um melhor entendimento de como honrar os consentimentos e as preferências do cliente ao criar definições de segmento no Experience Platform.

Para obter mais informações sobre como gerenciar o consentimento na Platform, consulte a seguinte documentação:

* [Processamento de consentimento usando o padrão Adobe](../../landing/governance-privacy-security/consent/adobe/overview.md)
* [Processamento de consentimento usando o padrão IAB TCF 2.0](../../landing/governance-privacy-security/consent/iab/overview.md)