---
keywords: transmissão contínua;
title: Conexão HTTP
description: O destino HTTP no Adobe Experience Platform permite enviar dados do perfil para pontos de extremidade HTTP de terceiros.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 802b1844bec1e577e978da5d5a69de87278c04b9
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 3%

---

# (Alfa) [!DNL HTTP] conexão

>[!IMPORTANT]
>
>O destino [!DNL HTTP] na Plataforma está atualmente em alfa. A documentação e a funcionalidade estão sujeitas a alterações.

## Visão geral {#overview}

O destino [!DNL HTTP] é um [!DNL Adobe Experience Platform] destino de transmissão que ajuda a enviar dados de perfil para pontos de extremidade [!DNL HTTP] de terceiros.

Para enviar dados de perfil para [!DNL HTTP] endpoints, primeiro você deve se conectar ao destino em [[!DNL Adobe Experience Platform]](#connect-destination).

## Casos de uso {#use-cases}

O destino [!DNL HTTP] é direcionado para clientes que precisam exportar dados de perfil XDM e segmentos de público-alvo para endpoints genéricos [!DNL HTTP].

[!DNL HTTP] os endpoints podem ser sistemas próprios do cliente ou soluções de terceiros.

## Conecte-se ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Enquanto [configurar](../ui/connect-destination.md) esse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL httpEndpoint]**: o  [!DNL URL] do ponto de extremidade HTTP para o qual você deseja enviar os dados do perfil.
   * Como opção, você pode adicionar parâmetros de consulta ao [!UICONTROL httpEndpoint] [!DNL URL].
* **[!UICONTROL authEndpoint]**: o  [!DNL URL] do endpoint HTTP usado para  [!DNL OAuth2] autenticação.
* **[!UICONTROL ID]** do cliente: o  [!DNL clientID] parâmetro usado nas credenciais do  [!DNL OAuth2] cliente.
* **[!UICONTROL Segredo]** do cliente: o  [!DNL clientSecret] parâmetro usado nas credenciais do  [!DNL OAuth2] cliente.

   >[!NOTE]
   >
   >No momento, há suporte somente para [!DNL OAuth2] credenciais de cliente.

* **[!UICONTROL Nome]**: insira um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: insira uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL Cabeçalhos]** personalizados: insira quaisquer cabeçalhos personalizados que você deseja incluir nas chamadas de destino, seguindo este formato:  `header1:value1,header2:value2,...headerN:valueN`.

   >[!IMPORTANT]
   >
   >A implementação atual requer pelo menos um cabeçalho personalizado. Essa limitação será resolvida em uma atualização futura.

## Ativar segmentos para este destino {#activate}

Consulte [Ativar perfis e segmentos para um destino](../ui/activate-destinations.md#select-attributes) para obter instruções sobre como ativar segmentos de público-alvo para destinos.

## Atributos de destino {#attributes}

Na etapa [[!UICONTROL Selecionar atributos]](../ui/activate-destinations.md#select-attributes), quando [ativar segmentos](../ui/activate-destinations.md) para um destino [!DNL HTTP], o Adobe recomenda selecionar um identificador exclusivo do [esquema de união](../../profile/home.md#profile-fragments-and-union-schemas). Selecione o identificador exclusivo e quaisquer outros campos XDM que deseja exportar para o destino.

## Dados exportados {#exported-data}

Seus dados [!DNL Experience Platform] exportados chegam ao seu destino [!DNL HTTP] no formato JSON. Por exemplo, o evento abaixo contém o atributo de perfil de endereço de email de um público que se qualificou para um determinado segmento e saiu de outro. As identidades desse prospecto são [!DNL ECID] e email.

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
