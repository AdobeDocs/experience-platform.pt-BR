---
title: Suporte à identidade unificada na coleção de dados
description: Saiba como o suporte à identidade unificada reúne a persistência própria e a ativação de terceiros compatíveis na coleção de dados da Web.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 32c2565d31eed4eda28195afaf82aac6f04a6f8a
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 3%

---

# Suporte à identidade unificada na coleção de dados

>[!AVAILABILITY]
>
>No momento, esse recurso está na versão beta. Disponibilidade, comportamento e documentação podem mudar.

O suporte à identidade unificada permite que o Edge Network funcione em contextos de identidade próprios e de terceiros. Ele reúne a identificação própria durável em suas propriedades com fluxos de trabalho de ativação de terceiros em navegadores que oferecem suporte a cookies de terceiros. Para obter informações sobre como o Web SDK lida com ECIDs, FPIDs e outros sinais de identidade, consulte [Identidade na Coleção de Dados](./overview.md).

Com o suporte unificado à identidade, você pode:

* **Maximizar o alcance do público-alvo**: ative os públicos-alvo da Experience Platform em destinos de terceiros (DSPs, SSPs e redes de anúncios) para obter um compartilhamento maior do seu tráfego.
* **Manter a precisão da medição**: mantenha a identificação consistente do visitante em todas as suas propriedades e plataformas de publicidade.
* **Sua implementação à prova de obsolescência**: use IDs de dispositivo primário como base, mantendo a compatibilidade com fluxos de trabalho de ativação de terceiros.

Quando um visitante chega ao seu site, o Edge Network avalia os sinais de identidade disponíveis, vinculando contextos próprios e de terceiros automaticamente quando as condições permitem. Os navegadores que bloqueiam cookies de terceiros continuam a operar no modo próprio, sem interrupção da implementação.

## Como funciona

O Edge Network gera ECIDs avaliando os sinais de identidade disponíveis na seguinte ordem de prioridade:

| Prioridade | Fonte | Contexto | Comportamento |
| --- | --- | --- | --- |
| 1 | **ID do Demdex** | Terceiros | Se uma ID Demdex estiver presente, a ECID será propagada a partir dela. Essa propagação produz uma ECID consistente em domínios que compartilham o mesmo cookie de terceiros. |
| 2 | **FPID** | Primários | Se nenhuma ID Demdex estiver presente, mas um FPID existir, a ECID será propagada do FPID e uma ID Demdex será derivada dele. |
| 3 | **Random** | Primários | Se nenhuma ID Demdex ou FPID estiver disponível, uma nova ECID aleatória será gerada e uma ID Demdex será derivada dela. |

ECIDs e IDs Demdex são vinculadas criptograficamente por meio de um algoritmo determinístico, o que significa que uma pode ser derivada da outra. Essa relação é o que permite que o Edge Network traduza contextos de identidade próprios e de terceiros sem exigir lógica de manipulação de visitante separada na implementação.

Como a relação é determinística, os públicos-alvo criados em ECIDs primárias podem ser ativados por meio de infraestrutura de terceiros quando a ID Demdex correspondente estiver disponível.

Para visitantes que já têm uma ECID derivada do FPID, o Edge Network pode vincular automaticamente sua identidade própria ao contexto de identidade de terceiros. Isso acontece de forma transparente quando o navegador aceita cookies de terceiros e não requer alterações na implementação. Quando ocorre a vinculação automática:

1. O Edge Network detecta que a ECID do visitante não foi derivada de uma ID Demdex.
1. Se o navegador do visitante suportar cookies de terceiros, uma sincronização de identidade leve será acionada.
1. O sistema cria um link entre a ECID primária do visitante e sua identidade de terceiros.
1. O link é armazenado no armazenamento de identidade, permitindo a ativação do público-alvo em destinos de terceiros.

A vinculação automática preserva ECIDs existentes e impede o cliffing de visitantes. Com o tempo, mais do seu público-alvo se torna gradualmente qualificado para ativação de terceiros, à medida que os visitantes retornam e a vinculação ocorre.

A ativação de público-alvo de terceiros depende da sincronização de ID (sincronização de ID). Quando o Edge Network estabelece ou atualiza uma identidade de terceiros, ele retorna instruções de sincronização de ID na resposta. Essas instruções direcionam o navegador para sincronizar a identidade do visitante com domínios de parceiros (DSPs, redes de anúncios e outras plataformas de ativação), para que os públicos-alvo da Experience Platform possam ser correspondidos e entregues nessas plataformas.

## Pré-requisitos

O suporte à identidade unificada exige todos os itens a seguir:

* Seu site usa a coleta de dados primários em um domínio que você controla.
* Sua implementação usa FPIDs ou outra estratégia de persistência primária como base.
* Cookies de terceiros são ativados na configuração do Web SDK.
* A sincronização de ID de terceiros está habilitada para a sequência de dados.
* O visitante usa um navegador que permite cookies de terceiros (consulte [Compatibilidade do navegador](#browser-compatibility) abaixo).

## Configuração

1. **Habilitar cookies de terceiros no Web SDK**: habilitar a configuração **Usar cookies de terceiros** na implementação do Web SDK. Se estiver usando a extensão de marca, habilite **[!UICONTROL Use third-party cookies]** em [Configurações de identidade](/help/tags/extensions/client/web-sdk/configure/identity.md#use-third-party-cookies). Se estiver usando a biblioteca JavaScript, defina [`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md) como `true`.

1. **Habilitar sincronização de ID de terceiros na sequência de dados**: habilite a opção **[!UICONTROL Third-Party ID Sync]** nas configurações avançadas da sequência de dados. Consulte [Criar e configurar sequências de dados](/help/datastreams/configure.md#advanced-options).

1. **Verifique se a persistência própria está em vigor**: confirme se sua estratégia de persistência própria (como FPIDs) já está implantada em seu próprio domínio. Consulte [IDs de dispositivo próprio na Coleção de dados](fpid.md).

## Validação

Para verificar se o suporte à identidade unificada está funcionando:

1. Abra as ferramentas de desenvolvedor do seu navegador e navegue até a guia **Rede**.
1. Limpe as solicitações existentes e acione um evento do Web SDK (carregamento de página ou evento personalizado) em uma sessão nova ou incógnita.
1. Encontre a resposta do Edge Network (procure chamadas para `adobedc.demdex.net` e seu ponto de extremidade de coleção próprio).
1. Inspecione o conteúdo da resposta para obter instruções de sincronização de ID.

Quando as instruções de sincronização de ID estão presentes, a resposta inclui um identificador `identity:exchange` semelhante ao seguinte:

```json
{
  "handle": [
    {
      "type": "identity:exchange",
      "payload": [
        {
          "type": "url",
          "id": 411,
          "spec": {
            "url": "https://example.com/...",
            "hideReferrer": false,
            "ttlMinutes": 10080
          }
        },
        {
          "type": "url",
          "id": 89,
          "spec": {
            "url": "https://example.org/...",
            "hideReferrer": true,
            "ttlMinutes": 10080
          }
        }
      ]
    }
  ]
}
```

| Elemento | Descrição |
| --- | --- |
| `type: "identity:exchange"` | Indica que as instruções de sincronização de ID estão presentes. |
| Matriz `payload` | Lista de URLs de sincronização de ID de parceiro. |
| `url` valores | Redirecionar URLs para domínios parceiros para sincronização de ID. |
| `id` valores | Identificadores de parceiro. |

>[!TIP]
>
>Se você não vir o identificador `identity:exchange` na resposta:
>
>* Verifique se você está testando com uma sessão de navegador nova ou incógnita. As identidades existentes não acionam novas sincronizações.
>* Verifique se as configurações do datastream e do Web SDK estão configuradas corretamente.
>* Confirme se você está usando um navegador compatível com cookies de terceiros (consulte a tabela abaixo).

Depois de confirmar a atividade de sincronização de ID, valide se:

* A identidade própria persiste conforme esperado em carregamentos de página em seu domínio.
* Os fluxos de ativação e de relatórios se comportam conforme esperado nos ambientes compatíveis.

## Compatibilidade do navegador {#browser-compatibility}

Os recursos de identidade de terceiros dependem do suporte do navegador para cookies de terceiros. A tabela a seguir resume o comportamento esperado:

| Navegador | Suporte a cookies de terceiros | Demdex disponível | Comportamento de identidade |
| --- | --- | --- | --- |
| Google Chrome | Suportado | Sim | Demdex → ECID (consistente entre domínios) |
| Microsoft Edge | Compatível por padrão | Sim | Demdex → ECID (consistente entre domínios) |
| Mozilla Firefox | Bloqueado por padrão (ETP) | Não (por padrão) | FPID → ECID (por domínio) |
| Apple Safari | Bloqueado (ITP) | Não | FPID → ECID (por domínio) |

Para navegadores que bloqueiam cookies de terceiros, a identificação própria continua a funcionar normalmente. Os recursos de ativação de terceiros só estão disponíveis onde o navegador permite cookies de terceiros.

## Limitações

* O comportamento da identidade de terceiros depende totalmente do navegador do visitante, que permite cookies de terceiros. Não há fallback para ativação de terceiros em navegadores que os bloqueiam.
* A vinculação automática exige que o visitante retorne ao site. A parte do seu público elegível para ativação de terceiros aumenta gradualmente ao longo do tempo.
