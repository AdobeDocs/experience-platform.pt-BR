---
keywords: transmissão contínua;
title: Conexão HTTP
description: O destino HTTP no Adobe Experience Platform permite enviar dados de perfil para pontos de extremidade HTTP de terceiros.
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 2%

---


# (Alfa) [!DNL HTTP] conexão

>[!IMPORTANT]
>
>O destino [!DNL HTTP] na Plataforma está atualmente em alfa. A documentação e a funcionalidade estão sujeitas a alterações.

O destino [!DNL HTTP] é um [!DNL Adobe Experience Platform] destino de transmissão que ajuda a enviar dados de perfil para pontos de extremidade [!DNL HTTP] de terceiros.

Para enviar dados de perfil para [!DNL HTTP] pontos de extremidade, primeiro conecte-se ao destino em [[!DNL Adobe Experience Platform]](#connect-destination).

## Casos de uso {#use-cases}

O destino [!DNL HTTP] é direcionado para clientes que precisam exportar dados de perfil XDM e segmentos de audiência para pontos de extremidade genéricos [!DNL HTTP].

[!DNL HTTP] os pontos de extremidade podem ser sistemas próprios do cliente ou soluções de terceiros.

## Conectar ao destino {#connect-destination}

Em **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]**, selecione [!DNL HTTP API] e **[!UICONTROL Configurar]**.

![Ativar destino HTTP](../assets/catalog/http/activate.png)

>[!NOTE]
>
>Se já existir uma conexão com esse destino, você poderá ver um botão **[!UICONTROL Ativar]** no cartão de destino. Para obter mais informações sobre a diferença entre **[!UICONTROL Ativate]** e **[!UICONTROL Configure]**, consulte a seção [Catalog](../ui/destinations-workspace.md#catalog) da documentação da área de trabalho de destino.
>
>![Ativar destino HTTP](../assets/catalog/http/connect.png)

Na etapa [!UICONTROL Account], é necessário definir os detalhes da conexão do terminal HTTP. Selecione **[!UICONTROL Nova conta]** e insira os detalhes da conexão do terminal HTTP ao qual você deseja se conectar.
- **[!UICONTROL httpEndpoint]**: a conclusão  [!DNL URL] do endpoint HTTP para o qual você deseja enviar os dados do perfil.
   - Como opção, você pode adicionar parâmetros de query ao [!UICONTROL httpEndpoint] [!DNL URL].
- **[!UICONTROL authEndpoint]**: a conclusão  [!DNL URL] do terminal HTTP usado para  [!DNL OAuth2] autenticação.
- **[!UICONTROL ID]** do cliente: o  [!DNL clientID] parâmetro usado nas credenciais  [!DNL OAuth2] do cliente.
- **[!UICONTROL Segredo]** do cliente: o  [!DNL clientSecret] parâmetro usado nas credenciais  [!DNL OAuth2] do cliente.

>[!NOTE]
>
>No momento, há suporte apenas para [!DNL OAuth2] credenciais de cliente.

![Conexão de ponto de extremidade HTTP](../assets/catalog/http/connect.png)

Clique em **[!UICONTROL Ligar ao destino]**. Depois que a conexão tiver êxito, clique em **[!UICONTROL Next]**.

Na etapa [!UICONTROL Authentication], digite as credenciais de autenticação da conta:
- **[!UICONTROL Nome]**: insira um nome pelo qual você reconhecerá esse destino no futuro.
- **[!UICONTROL Descrição]**: insira uma descrição que o ajudará a identificar esse destino no futuro.
- **[!UICONTROL Cabeçalhos]** personalizados: insira os cabeçalhos personalizados que você deseja incluir nas chamadas de destino, seguindo este formato:  `header1:value1,header2:value2,...headerN:valueN`.

>[!IMPORTANT]
>
>A implementação atual requer pelo menos um cabeçalho personalizado. Essa limitação será resolvida em uma atualização futura.

![Autenticação HTTP](../assets/catalog/http/authenticate.png)

**[!UICONTROL Caso]** de uso de marketing: Os casos de uso de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar de casos de uso de marketing definidos pelo Adobe ou criar seu próprio caso de uso de marketing. Para obter mais informações sobre casos de uso de marketing, consulte [Visão geral das políticas de uso de dados](../../data-governance/policies/overview.md).

Clique em **[!UICONTROL Criar destino]**.

## Ativar segmentos

Consulte [Ativar perfis e segmentos em um destino](../ui/activate-destinations.md#select-attributes) para obter informações sobre o fluxo de trabalho da ativação de segmentos.

## Atributos de destino

Durante a etapa [[!UICONTROL Selecionar atributos]](../ui/activate-destinations.md#select-attributes), ao [ativar segmentos](../ui/activate-destinations.md) para um destino [!DNL HTTP], recomendamos que você selecione um identificador exclusivo do seu schema [união](../../profile/home.md#profile-fragments-and-union-schemas). Selecione o identificador exclusivo e quaisquer outros campos XDM que você deseja exportar para o destino.

## Dados exportados {#exported-data}

Seus dados exportados [!DNL Experience Platform] chegam em seu destino [!DNL HTTP] no formato JSON. Por exemplo, o evento abaixo contém o atributo de perfil de endereço de email de uma audiência que se qualificou para um determinado segmento e saiu de outro. As identidades para este prospecto são [!DNL ECID] e por email.

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```
