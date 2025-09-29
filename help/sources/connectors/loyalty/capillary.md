---
title: Visão geral dos eventos de transmissão capilares
description: Saiba como transmitir dados do Capilary para o Experience Platform.
badge: Beta
exl-id: 3b8eb2f6-3b4a-4b91-89d4-b6d9027c6ab4
source-git-commit: bd5611b23740f16e41048f3bc65f62312593a075
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 4%

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

Antes de conectar o [!DNL Capillary] ao Adobe Experience Platform, verifique se você tem:

* Uma **ID de organização da Adobe** válida e acesso a uma sandbox da Experience Platform habilitada.
* **[!DNL Capillary]credenciais de origem** (ID do Cliente e Segredo do Cliente).
* As permissões necessárias no Adobe Admin Console para criar fontes e fluxos de dados.

### Coletar credenciais necessárias

Você deve fornecer valores para as seguintes credenciais para conectar sua conta do [!DNL Capillary] à Experience Platform:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| ID de cliente | O identificador de cliente para a origem [!DNL Capillary]. | `321c8a8fee0d4a06838d46f9d3109e8a` |
| Segredo do cliente | A frase secreta do cliente emitida com a ID do cliente | `xxxxxxxxxxxxxxxxxx` |
| ID da organização | Sua ID da organização da Adobe | `0A7D42FC5DB9D3360A495FD3@AdobeOrg` |

Para obter mais informações sobre a geração de tokens de acesso, leia o [guia de autenticação do Adobe](https://developer.adobe.com/developer-console/docs/guides/authentication/).

### Gerar um token de acesso

Em seguida, use a ID do cliente e o Segredo do cliente para gerar um token de acesso do Adobe.

**Solicitação**

```shell
curl -X POST 'https://ims-na1.adobelogin.com/ims/token' \
  -d 'client_id={CLIENT_ID}' \
  -d 'client_secret={CLIENT_SECRET}' \
  -d 'grant_type=client_credentials' \
  -d 'scope=openid AdobeID read_organizations additional_info.projectedProductContext session'
```

**Resposta**

```json
{
  "access_token": "eyJhbGciOi...",
  "token_type": "bearer",
  "expires_in": 86399994
}
```

## Próximas etapas

Depois de concluir a configuração de pré-requisito para [!DNL Capillary], leia a documentação a seguir para saber como você pode conectar sua conta e iniciar a transmissão de dados do [!DNL Capillary] para a Experience Platform.

* [Conectar  [!DNL Capillary Streaming Events]  ao Experience Platform usando a API](../../tutorials/api/create/loyalty/capillary.md)
* [Conectar [!DNL Capillary Streaming Events] ao Experience Platform usando a interface](../../tutorials/ui/create/loyalty/capillary.md)
