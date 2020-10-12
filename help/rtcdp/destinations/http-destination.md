---
keywords: streaming;
title: O destino HTTP é um destino Adobe Real-Time Customer Data Platform que ajuda a enviar dados de perfis para pontos de extremidade HTTP de terceiros.
seo-title: O destino HTTP é um destino Adobe Real-Time Customer Data Platform que ajuda a enviar dados de perfis para pontos de extremidade HTTP de terceiros.
description: O destino HTTP é um destino Adobe Real-Time Customer Data Platform que ajuda a enviar dados de perfis para pontos de extremidade HTTP de terceiros.
seo-description: O destino HTTP é um destino Adobe Real-Time Customer Data Platform que ajuda a enviar dados de perfis para pontos de extremidade HTTP de terceiros.
translation-type: tm+mt
source-git-commit: cf100e8df225a665eade5ee6ddab071707e93f8b
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 2%

---


# (Alfa) [!DNL HTTP] Destino

>[!IMPORTANT]
>
>O [!DNL HTTP] destino no CDP em tempo real do Adobe está atualmente em alfa. A documentação e a funcionalidade estão sujeitas a alterações.

## Visão geral {#overview}

O [!DNL HTTP] destino é um destino de [!DNL Adobe Real-Time Customer Data Platform] streaming que ajuda a enviar dados do perfil para [!DNL HTTP] pontos de extremidade de terceiros.

Para enviar dados de perfil para [!DNL HTTP] pontos de extremidade, primeiro você deve se conectar ao destino no [!DNL Adobe Real-Time Customer Data Platform](#connect-destination).

## Casos de uso {#use-cases}

O [!DNL HTTP] destino é direcionado para clientes que precisam exportar dados de perfil XDM e segmentos de audiência para [!DNL HTTP] pontos de extremidade genéricos.

[!DNL HTTP] os pontos de extremidade podem ser sistemas próprios do cliente ou soluções de terceiros.

## Conectar ao destino {#connect-destination}

1. Em **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]**, selecione [!DNL  HTTP API]e selecione **[!UICONTROL Configurar]**.

   ![Ativar destino HTTP](assets/activate-http-destination.png)

   >[!NOTE]
   >
   >Se já existir uma conexão com esse destino, você poderá ver um botão **[!UICONTROL Ativar]** no cartão de destino. Para obter mais informações sobre a diferença entre **[!UICONTROL Ativar]** e **[!UICONTROL Configurar]**, consulte a seção [Catálogo](../destinations/destinations-workspace.md#catalog) da documentação da área de trabalho de destino.
   ![Ativar destino HTTP](assets/connect-http-destination.png)

2. Na etapa [!UICONTROL Conta] , é necessário definir os detalhes da conexão do terminal HTTP. Selecione **[!UICONTROL Nova conta]** e insira os detalhes da conexão do terminal HTTP ao qual você deseja se conectar.
   * **[!UICONTROL httpEndpoint]**: a conclusão [!DNL URL] do endpoint HTTP para o qual você deseja enviar os dados do perfil.
      * Como opção, você pode adicionar parâmetros de query ao [!UICONTROL httpEndpoint] [!DNL URL].
   * **[!UICONTROL authEndpoint]**: a conclusão [!DNL URL] do endpoint HTTP usado para [!DNL OAuth2] autenticação.
   * **[!UICONTROL ID]** do cliente: o [!DNL clientID] parâmetro usado nas credenciais [!DNL OAuth2] do cliente.
   * **[!UICONTROL Segredo]** do cliente: o [!DNL clientSecret] parâmetro usado nas credenciais [!DNL OAuth2] do cliente.

   >[!NOTE]
   >
   >Atualmente, apenas [!DNL OAuth2] as credenciais do cliente são suportadas.

   ![Conexão de ponto de extremidade HTTP](assets/connect-http-endpoint.png)
3. Clique em **[!UICONTROL Conectar-se ao destino]**.
4. Depois que a conexão for bem-sucedida, clique em **[!UICONTROL Avançar]**.
5. Na etapa [!UICONTROL Autenticação] , digite as credenciais de autenticação da conta:
   * **[!UICONTROL Nome]**: insira um nome pelo qual você reconhecerá esse destino no futuro.
   * **[!UICONTROL Descrição]**: insira uma descrição que o ajudará a identificar esse destino no futuro.
   * **[!UICONTROL Cabeçalhos]** personalizados: insira os cabeçalhos personalizados que você deseja incluir nas chamadas de destino, seguindo este formato: `header1:value1,header2:value2,...headerN:valueN`.

      >[!IMPORTANT]
      >
      >A implementação atual requer pelo menos um cabeçalho personalizado. Essa limitação será resolvida em uma atualização futura.
   ![Autenticação HTTP](assets/authentication-http-connection.png)

6. **[!UICONTROL Caso]** de uso de marketing: Os casos de uso de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar de casos de uso de marketing definidos pelo Adobe ou criar seu próprio caso de uso de marketing. Para obter mais informações sobre casos de uso de marketing, consulte a página [Data Governance em CDP](../privacy/data-governance-overview.md#destinations) em tempo real. Para obter informações sobre casos individuais de uso de marketing definidos pelo Adobe, consulte a visão geral [das políticas de uso de](../../data-governance/policies/overview.md#core-actions)dados.
7. Clique em **[!UICONTROL Criar destino]**.

## Ativar segmentos

Consulte [Ativar perfis e segmentos em um destino](activate-destinations.md#select-attributes) para obter informações sobre o fluxo de trabalho da ativação de segmentos.

## Atributos de destino

Durante a etapa [[!UICONTROL Selecionar atributos]](activate-destinations.md#select-attributes) , ao [ativar segmentos](activate-destinations.md) em um [!DNL HTTP] destino, recomendamos que você selecione um identificador exclusivo do seu schema [de](../../profile/home.md#profile-fragments-and-union-schemas)união. Selecione o identificador exclusivo e quaisquer outros campos XDM que você deseja exportar para o destino.

## Dados exportados {#exported-data}

Seus [!DNL Experience Platform] dados exportados chegam ao seu [!DNL HTTP] destino no formato JSON. Por exemplo, o evento abaixo contém o atributo de perfil de endereço de email de uma audiência que se qualificou para um determinado segmento e saiu de outro. As identidades para este prospecto são [!DNL ECID] e-mail.

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
