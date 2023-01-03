---
keywords: Experience Platform, home, tópicos populares, recusar, segmentação, serviço de segmentação, serviço de segmentação, opções de honra, recusas, rejeitar, recusar, consentimento, compartilhar, coletar;
solution: Experience Platform
title: Respeito do consentimento em segmentos
topic-legacy: overview
description: Saiba como honrar as preferências de consentimento do cliente para coleta de dados pessoais e compartilhamento em operações do segmento.
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Respeito do consentimento em segmentos

Regulamentos legais de privacidade, como o [!DNL California Consumer Privacy Act] (CCPA) confere aos consumidores o direito de optarem por não terem os seus dados pessoais recolhidos ou partilhados com terceiros. A Adobe Experience Platform fornece componentes padrão do Experience Data Model (XDM), destinados a capturar essas preferências de consentimento do cliente em dados do Perfil do cliente em tempo real.

Se um cliente tiver retirado ou retido o consentimento de ter seus dados pessoais compartilhados, é importante que sua organização respeite essa preferência ao gerar públicos-alvo para atividades de marketing. Este documento descreve como integrar valores de consentimento do cliente em suas definições de segmento usando a interface do usuário do Experience Platform.

## Introdução

O cumprimento dos valores de consentimento do cliente requer uma compreensão das várias [!DNL Adobe Experience Platform] serviços envolvidos. Antes de iniciar este tutorial, verifique se você está familiarizado com os seguintes serviços:

* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): A estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.
* [[!DNL Real-Time Customer Profile]](../profile/home.md): Fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Permite criar segmentos de público-alvo a partir de [!DNL Real-Time Customer Profile] dados.

## Campos de esquema de consentimento

Para honrar os consentimentos e as preferências do cliente, um dos esquemas que faz parte de [!UICONTROL Perfil individual XDM] o schema de união deve conter o grupo de campos padrão **[!UICONTROL Consentimentos e preferências]**.

Para obter detalhes sobre a estrutura e o caso de uso pretendido de cada atributo fornecido pelo grupo de campos, consulte o [guia de referência de consentimentos e preferências](../xdm/field-groups/profile/consents.md). Para obter instruções passo a passo sobre como adicionar um grupo de campos a um schema, consulte o [Guia da interface do usuário do XDM](../xdm/ui/resources/schemas.md#add-field-groups).

Depois que o grupo de campos é adicionado a um [Esquema habilitado para perfil](../xdm/ui/resources/schemas.md#profile) e seus campos tiverem sido usados para assimilar dados de consentimento do aplicativo de experiência, você poderá usar os atributos de consentimento coletados nas regras do segmento.

## Manuseio de consentimento na segmentação

Para garantir que os perfis rejeitados não sejam incluídos em segmentos, campos especiais devem ser adicionados a segmentos existentes e incluídos ao criar novos segmentos.

As etapas abaixo demonstram como adicionar os campos apropriados para dois tipos de sinalizadores de opt out:

1. [!UICONTROL Coleta de dados]
1. [!UICONTROL Compartilhar dados]

>[!NOTE]
>
>Embora este guia se concentre nos dois sinalizadores de opt-out acima, você pode configurar seus segmentos para incorporar também sinais de consentimento adicionais. O [guia de referência de consentimentos e preferências](../xdm/field-groups/profile/consents.md) O fornece mais informações sobre cada uma dessas opções e seus casos de uso planejados.

Ao criar um segmento na interface do usuário, em **[!UICONTROL Atributos]**, navegue até **[!UICONTROL Perfil individual XDM]**, em seguida selecione **[!UICONTROL Consentimentos e preferências]**. Aqui, você pode ver as opções de **[!UICONTROL Coleta de dados]** e **[!UICONTROL Compartilhar dados]**.

![](./images/opt-outs/consents.png)

Comece selecionando o **[!UICONTROL Coleta de dados]** categoria e arraste **[!UICONTROL Valor da escolha]** no construtor de segmentos. Ao adicionar o atributo ao segmento, você pode especificar a variável [valores de consentimento](../xdm/field-groups/profile/consents.md#choice-values) que devem ser incluídas ou excluídas.

![](./images/opt-outs/consent-values.png)

Uma abordagem é excluir todos os clientes que optaram por não ter seus dados coletados. Para fazer isso, defina o operador como **[!UICONTROL não é igual]** e escolha os seguintes valores:

* **[!UICONTROL Não (opt-out)]**
* **[!UICONTROL Padrão de Não (opt out)]**
* **[!UICONTROL Desconhecido]** (se o consentimento for presumido como retido, caso contrário desconhecido)

![](./images/opt-outs/collect.png)

Em **[!UICONTROL Atributos]** no painel à esquerda, navegue de volta para a **[!UICONTROL Consentimentos e preferências]** e selecione **[!UICONTROL Compartilhar dados]**. Arraste o correspondente **[!UICONTROL Valor da escolha]** na tela e selecione os mesmos valores para a [!UICONTROL Coleta de dados] valor de escolha. Certifique-se de que **[!UICONTROL Ou]** é estabelecida entre os dois atributos.

![](./images/opt-outs/share.png)

Com ambas as variáveis **[!UICONTROL Coleta de dados]** e **[!UICONTROL Compartilhar dados]** valores de consentimento adicionados ao segmento, quaisquer clientes que optaram por não ter seus dados usados serão excluídos do público resultante. A partir daqui, você pode continuar personalizando a definição do segmento antes de selecionar **[!UICONTROL Salvar]** para concluir o processo.

## Próximas etapas

Ao seguir este tutorial, você deve conhecer melhor como honrar os consentimentos e as preferências do cliente ao criar segmentos no Experience Platform.

Para obter mais informações sobre como gerenciar o consentimento no Platform, consulte a seguinte documentação:

* [Processamento de consentimento usando o padrão Adobe](../landing/governance-privacy-security/consent/adobe/overview.md)
* [Processamento de consentimento usando o padrão TCF do IAB 2.0](../landing/governance-privacy-security/consent/iab/overview.md)