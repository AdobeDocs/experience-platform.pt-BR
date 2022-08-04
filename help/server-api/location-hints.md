---
title: Dicas de localização
description: Este artigo explica como as dicas de localização funcionam na API do Servidor de Rede de Borda, para que as solicitações do usuário final possam ser sempre roteadas para o mesmo servidor.
source-git-commit: 7f1d8fba34c5478f0d6e727a5a52af642852c9dd
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---


# Dicas de localização

## Visão geral {#overview}

O [!DNL Adobe Experience Platform Edge Network] O usa vários servidores distribuídos globalmente para garantir tempos de resposta rápidos, independentemente da localização do usuário final. Também usa o roteamento baseado em DNS para garantir que as solicitações sejam sempre roteadas para o local da Rede de Borda mais próximo dos usuários finais.

Se os usuários finais se conectarem a uma VPN ou alternarem os tipos de rede em seus dispositivos móveis ao longo de uma sessão, as solicitações de Rede de Borda geralmente poderão ser roteadas para um local diferente. O roteamento de meia sessão entre servidores pode ser problemático, já que as soluções da Adobe Experience Platform e da Adobe Experience Cloud armazenam informações de perfil do usuário final na Edge Network.

É aqui que as dicas de localização entram em ação.

Para garantir que os usuários finais sempre interajam com o servidor regional da Rede de Borda que contém seus dados de perfil atuais, a funcionalidade de dicas de localização garante que todas as solicitações para a Rede de Borda sejam enviadas para o mesmo servidor em que a primeira solicitação de uma sessão foi feita. Isso ajuda os usuários a ter uma experiência consistente, independentemente das alterações de rede que possam ocorrer ao longo de uma sessão.

## Uso de dicas de localização

As dicas de localização são incluídas na resposta da solicitação inicial da Rede de Borda e em todas as solicitações subsequentes, conforme mostrado no exemplo abaixo:

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

O `EdgeNetwork` O escopo contém todas as informações relevantes que a Rede de Borda precisa para rotear as solicitações subsequentes de acordo. Na resposta da solicitação inicial e de cada solicitação subsequente para a rede do Edge, haverá uma seção no identificador com um tipo de `locationHint:result`.

A dica associada à `EdgeNetwork` o escopo pode conter um dos seguintes valores:

* `or2`
* `va6`
* `irl1`
* `ind1`
* `jpn3`
* `sgp3`
* `aus3`

**Formato da API**

Para garantir que as solicitações subsequentes sejam roteadas corretamente, insira a dica de localização no caminho de URL das chamadas de API subsequentes entre o caminho base, normalmente `ee`e `v2` Versão da API.

```http
POST 'https://edge.adobedc.net/ee/{LOCATION_HINT}/v2/interact?dataStreamId={DataStream_ID}'
```

## Armazenamento de dicas de localização em cookies {#storing-hints-in-cookies}

Para garantir que a dica de localização retornada pela Rede de Borda persista durante a sessão, você pode armazenar o valor da dica de localização em um cookie, juntamente com o tempo de vida do cookie, contido no `ttlSeconds` (normalmente, 1800 segundos).

Como na maioria dos cookies, você deve estender o tempo de vida desse cookie sempre que houver uma resposta da Edge Network. Para garantir compatibilidade máxima com o SDK da Web, use o nome do cookie `kndctr_{IMSORG}_AdobeOrg_cluster`. As IDs de organização IMS normalmente terminam com `@AdobeOrg`. O `@` deve ser convertido em um sublinhado para garantir que o cookie esteja no formato correto.
