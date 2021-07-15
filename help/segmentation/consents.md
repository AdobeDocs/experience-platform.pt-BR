---
keywords: Experience Platform, home, tópicos populares, recusar, segmentação, serviço de segmentação, serviço de segmentação, opções de honra, recusas, rejeitar, recusar, consentimento, compartilhar, coletar;
solution: Experience Platform
title: Respeito do consentimento em segmentos
topic-legacy: overview
description: Saiba como honrar as preferências de consentimento do cliente para coleta de dados pessoais e compartilhamento em operações do segmento.
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: bd312024a1a3fb6da840a38d6e9d19fcbd6eab5a
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Respeito do consentimento em segmentos

Regulamentações legais de privacidade como a [!DNL California Consumer Privacy Act] (CCPA) oferecem aos consumidores o direito de optar por não coletar ou compartilhar seus dados pessoais com terceiros. A Adobe Experience Platform fornece componentes padrão do Experience Data Model (XDM), destinados a capturar essas preferências de consentimento do cliente em dados do Perfil do cliente em tempo real.

Se um cliente tiver retirado ou retido o consentimento de ter seus dados pessoais compartilhados, é importante que sua organização respeite essa preferência ao gerar públicos-alvo para atividades de marketing. Este documento descreve como integrar valores de consentimento do cliente em suas definições de segmento usando a interface do usuário do Experience Platform.

## Introdução

O cumprimento dos valores de consentimento do cliente requer uma compreensão dos vários serviços [!DNL Adobe Experience Platform] envolvidos. Antes de iniciar este tutorial, verifique se você está familiarizado com os seguintes serviços:

* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): A estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.
* [[!DNL Real-time Customer Profile]](../profile/home.md): Fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Permite criar segmentos de público-alvo a partir de  [!DNL Real-time Customer Profile] dados.

## Campos de esquema de consentimento

Para honrar os consentimentos e preferências do cliente, um dos esquemas que faz parte do esquema de união [!UICONTROL Perfil individual XDM] deve conter o grupo de campos padrão **[!UICONTROL Consentimentos e Preferências]**.

Para obter detalhes sobre a estrutura e o caso de uso pretendido de cada atributo fornecido pelo grupo de campos, consulte o [guia de referência de consentimentos e preferências](../xdm/field-groups/profile/consents.md). Para obter instruções passo a passo sobre como adicionar um grupo de campos a um esquema, consulte o [Guia da interface do usuário XDM](../xdm/ui/resources/schemas.md#add-field-groups).

Depois que o grupo de campos tiver sido adicionado a um [Esquema habilitado para perfil](../xdm/ui/resources/schemas.md#profile) e seus campos tiverem sido usados para assimilar dados de consentimento do seu aplicativo de experiência, você poderá usar os atributos de consentimento coletados nas regras do segmento.

## Manuseio de consentimento na segmentação

Para garantir que os perfis rejeitados não sejam incluídos em segmentos, campos especiais devem ser adicionados a segmentos existentes e incluídos ao criar novos segmentos.

As etapas abaixo demonstram como adicionar os campos apropriados para dois tipos de sinalizadores de opt out:

1. [!UICONTROL Coleta de dados]
1. [!UICONTROL Compartilhar dados]

>[!NOTE]
>
>Embora este guia se concentre nos dois sinalizadores de opt-out acima, você pode configurar seus segmentos para incorporar também sinais de consentimento adicionais. O [guia de referência de consentimento e preferências](../xdm/field-groups/profile/consents.md) fornece mais informações sobre cada uma dessas opções e seus casos de uso planejados.

Ao criar um segmento na interface do usuário, em **[!UICONTROL Atributos]**, navegue até **[!UICONTROL Perfil individual XDM]** e selecione **[!UICONTROL Consentimentos e Preferências]**. Aqui, você pode ver as opções para **[!UICONTROL Coleta de dados]** e **[!UICONTROL Compartilhar dados]**.

![](./images/opt-outs/consents.png)

Comece selecionando a categoria **[!UICONTROL Coleta de dados]** e arraste **[!UICONTROL Valor de escolha]** para o construtor de segmentos. Ao adicionar o atributo ao segmento, você pode especificar os [valores de consentimento](../xdm/field-groups/profile/consents.md#choice-values) que devem ser incluídos ou excluídos.

![](./images/opt-outs/consent-values.png)

Uma abordagem é excluir todos os clientes que optaram por não ter seus dados coletados. Para fazer isso, defina o operador como **[!UICONTROL não é igual a]** e escolha os seguintes valores:

* **[!UICONTROL Não (opt-out)]**
* **[!UICONTROL Padrão de Não (opt out)]**
* **[!UICONTROL Desconhecido]**  (se o consentimento for presumido como retido, caso contrário desconhecido)

![](./images/opt-outs/collect.png)

Em **[!UICONTROL Atributos]** no painel à esquerda, navegue de volta para a seção **[!UICONTROL Consentimentos e Preferências]** e selecione **[!UICONTROL Compartilhar dados]**. Arraste seu **[!UICONTROL Valor de escolha]** correspondente para a tela e selecione os mesmos valores que aqueles para o valor de escolha [!UICONTROL Coleta de dados]. Certifique-se de que uma relação **[!UICONTROL Or]** seja estabelecida entre os dois atributos.

![](./images/opt-outs/share.png)

Com os valores de consentimento **[!UICONTROL Data Collection]** e **[!UICONTROL Share Data]** adicionados ao segmento, todos os clientes que optaram por não ter seus dados usados serão excluídos do público resultante. A partir daqui, você pode continuar personalizando a definição do segmento antes de selecionar **[!UICONTROL Salvar]** para concluir o processo.

## Próximas etapas

Ao seguir este tutorial, você deve conhecer melhor como honrar os consentimentos e as preferências do cliente ao criar segmentos no Experience Platform.

Para obter mais informações sobre como gerenciar o consentimento no Platform, consulte a seguinte documentação:

* [Processamento de consentimento usando o padrão Adobe](../landing/governance-privacy-security/consent/adobe/overview.md)
* [Processamento de consentimento usando o padrão TCF do IAB 2.0](../landing/governance-privacy-security/consent/iab/overview.md)