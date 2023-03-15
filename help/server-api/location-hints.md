---
title: Dicas de localização
description: Este artigo explica como as dicas de localização funcionam na API do servidor da rede de borda, para que as solicitações do usuário final possam sempre ser roteadas para o mesmo servidor.
exl-id: 8cd2f8e2-2065-4b7e-8d35-4ed1a716f1b3
source-git-commit: 80c527ab3c82e01fe19e5003e224d63e79b23bdc
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# Dicas de localização

## Visão geral {#overview}

A variável [!DNL Adobe Experience Platform Edge Network] O usa vários servidores distribuídos globalmente para garantir tempos de resposta rápidos, independentemente da localização do usuário final. Ele também usa roteamento baseado em DNS para garantir que as solicitações sejam sempre roteadas para o local da rede de borda mais próximo dos usuários finais.

Se os usuários finais se conectarem a uma VPN ou alternarem tipos de rede em seus dispositivos móveis durante uma sessão, as solicitações de Rede de borda geralmente poderão ser roteadas para um local diferente. O roteamento de meia sessão entre servidores pode ser problemático, pois as soluções da Adobe Experience Platform e da Adobe Experience Cloud armazenam informações de perfil do usuário final na rede de borda.

É aqui que as dicas de localização são exibidas.

Para garantir que os usuários finais sempre interajam com o servidor regional da Rede de borda que contém seus dados de perfil atuais, a funcionalidade de dicas de localização garante que todas as solicitações para a Rede de borda sejam enviadas para o mesmo servidor em que a primeira solicitação de sessão foi feita. Isso ajuda os usuários a ter uma experiência consistente, independentemente das alterações de rede que possam ocorrer durante uma sessão.

## Uso de dicas de localização

As dicas de localização são incluídas na resposta da solicitação inicial da Rede de borda e em todas as solicitações subsequentes, como mostrado no exemplo abaixo:

```json
{
   "payload":[
      {
         "scope":"EdgeNetwork",
         "hint":"or2",
         "ttlSeconds":1800
      }
   ],
   "type":"locationHint:result"
}
```

A variável `EdgeNetwork` O escopo contém todas as informações relevantes de que a rede de borda precisa para rotear as solicitações subsequentes de acordo. Na resposta da solicitação inicial e de cada solicitação subsequente à rede de borda, haverá uma seção no identificador com um tipo de `locationHint:result`.

A dica associada à variável `EdgeNetwork` o escopo pode conter um dos seguintes valores:

* `or2`
* `va6`
* `irl1`
* `ind1`
* `jpn3`
* `sgp3`
* `aus3`

**Formato da API**

Para garantir que as solicitações subsequentes sejam roteadas corretamente, insira a dica de local no caminho do URL das chamadas de API subsequentes entre o caminho base, normalmente `ee`, e `v2` Versão da API.

```http
POST 'https://edge.adobedc.net/ee/{LOCATION_HINT}/v2/interact?dataStreamId={DataStream_ID}'
```

## Armazenamento de dicas de localização em cookies {#storing-hints-in-cookies}

Para garantir que a dica de local retornada pela Rede de borda persista pela duração da sessão, você pode armazenar o valor da dica de local em um cookie, juntamente com o tempo de vida do cookie, contido na variável `ttlSeconds` (normalmente 1800 segundos).

Assim como na maioria dos cookies, você deve estender o tempo de vida desse cookie sempre que houver uma resposta da Rede de borda. Para garantir a compatibilidade máxima com o SDK da Web, use o nome do cookie `kndctr_{IMSORG}_AdobeOrg_cluster`. As IDs organizacionais IMS normalmente terminam com `@AdobeOrg`. A variável `@` O valor deve ser convertido em sublinhado para garantir que o cookie esteja no formato correto.
