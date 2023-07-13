---
solution: Experience Platform
title: Cumprir o consentimento em segmentos
description: Saiba como respeitar as preferências de consentimento do cliente para a coleta e o compartilhamento de dados pessoais em operações de segmento.
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---

# Cumprimento do consentimento nos segmentos

>[!NOTE]
>
>Este guia explica como honrar os consentimentos no **definições de segmento**.

Regulamentos legais de privacidade, como o [!DNL California Consumer Privacy Act] (CCPA) proporcionam aos consumidores o direito de optar por não ter seus dados pessoais coletados ou compartilhados com terceiros. O Adobe Experience Platform fornece componentes padrão do Experience Data Model (XDM) destinados a capturar essas preferências de consentimento do cliente em dados de perfil do cliente em tempo real.

Se um cliente tiver retirado ou retido o consentimento para o compartilhamento de seus dados pessoais, é importante que sua organização honre essa preferência ao gerar públicos-alvo para atividades de marketing. Este documento descreve como integrar os valores de consentimento do cliente nas definições de segmento usando a interface do usuário do Experience Platform.

## Introdução

O respeito dos valores de consentimento do cliente exige a compreensão dos vários [!DNL Adobe Experience Platform] serviços envolvidos. Antes de iniciar este tutorial, verifique se você está familiarizado com os seguintes serviços:

* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): a estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.
* [[!DNL Real-Time Customer Profile]](../profile/home.md): fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): permite criar públicos-alvo a partir do [!DNL Real-Time Customer Profile] dados.

## Campos de esquema de consentimento

Para honrar os consentimentos e preferências do cliente, um dos esquemas que fazem parte do [!UICONTROL Perfil individual XDM] o esquema de união deve conter o grupo de campos padrão **[!UICONTROL Consentimentos e preferências]**.

Para obter detalhes sobre a estrutura e o caso de uso pretendido de cada um dos atributos fornecidos pelo grupo de campos, consulte o [guia de referência de consentimentos e preferências](../xdm/field-groups/profile/consents.md). Para obter instruções passo a passo sobre como adicionar um grupo de campos a um schema, consulte o [Guia da interface do XDM](../xdm/ui/resources/schemas.md#add-field-groups).

Depois que o grupo de campos for adicionado a um [Esquema ativado por perfil](../xdm/ui/resources/schemas.md#profile) e seus campos foram usados para assimilar dados de consentimento do aplicativo de experiência, você pode usar os atributos de consentimento coletados nas regras de segmento.

## Lidar com o consentimento na segmentação

Para garantir que perfis de recusa de participação não sejam incluídos nas definições de segmento, campos especiais devem ser adicionados às definições de segmento existentes e incluídos ao criar novas definições de segmento.

As etapas abaixo demonstram como adicionar os campos apropriados para dois tipos de sinalizadores de recusa:

1. [!UICONTROL Coleta de dados]
1. [!UICONTROL Compartilhar dados]

>[!NOTE]
>
>Embora este guia se concentre nos dois sinalizadores de recusa acima, você também pode configurar as definições de segmento para incorporar sinais de consentimento adicionais. A variável [guia de referência de consentimentos e preferências](../xdm/field-groups/profile/consents.md) O fornece mais informações sobre cada uma dessas opções e seus casos de uso pretendidos.

Ao criar uma definição de segmento na interface do usuário, em **[!UICONTROL Atributos]**, navegue até **[!UICONTROL Perfil individual XDM]** e selecione **[!UICONTROL Consentimentos e preferências]**. Aqui, você pode ver as opções para **[!UICONTROL Coleta de dados]** e **[!UICONTROL Compartilhar dados]**.

![](./images/opt-outs/consents.png)

Comece selecionando o **[!UICONTROL Coleta de dados]** categoria e, em seguida, arraste **[!UICONTROL Valor de escolha]** no construtor de segmentos. Ao adicionar o atributo à definição do segmento, é possível especificar o [valores de consentimento](../xdm/field-groups/profile/consents.md#choice-values) que devem ser incluídos ou excluídos.

![](./images/opt-outs/consent-values.png)

Uma abordagem é excluir todos os clientes que optaram por não ter seus dados coletados. Para fazer isso, defina o operador como **[!UICONTROL não é igual a]** e escolha os seguintes valores:

* **[!UICONTROL Não (recusar)]**
* **[!UICONTROL Padrão de Não (recusar)]**
* **[!UICONTROL Desconhecido]** (se o consentimento for presumido como retido caso seja desconhecido)

![](./images/opt-outs/collect.png)

Em **[!UICONTROL Atributos]** no painel à esquerda, navegue de volta para a **[!UICONTROL Consentimentos e preferências]** e selecione **[!UICONTROL Compartilhar dados]**. Arraste o correspondente **[!UICONTROL Valor de escolha]** na tela e selecione os mesmos valores para a variável [!UICONTROL Coleta de dados] valor de escolha. Assegure que uma **[!UICONTROL Ou]** A relação é estabelecida entre os dois atributos.

![](./images/opt-outs/share.png)

Com ambos os **[!UICONTROL Coleta de dados]** e **[!UICONTROL Compartilhar dados]** valores de consentimento adicionados à definição de segmento, todos os clientes que optaram por não ter seus dados usados serão excluídos do público-alvo resultante. Aqui, é possível continuar personalizando a definição do segmento antes de selecionar **[!UICONTROL Salvar]** para concluir o processo.

## Próximas etapas

Seguindo este tutorial, você deve ter um melhor entendimento de como honrar os consentimentos e preferências do cliente ao criar definições de segmento no Experience Platform.

Para obter mais informações sobre como gerenciar o consentimento na Platform, consulte a seguinte documentação:

* [Processamento de consentimento usando o padrão Adobe](../landing/governance-privacy-security/consent/adobe/overview.md)
* [Processamento de consentimento usando o padrão IAB TCF 2.0](../landing/governance-privacy-security/consent/iab/overview.md)