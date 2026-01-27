---
title: Conexão Kevel
description: Use o destino de transmissão Kevel para ativar públicos diretamente nas APIs de UserDB e Gerenciamento de segmento do Kevel e oferecer suporte ao direcionamento em tempo real no momento da decisão.
source-git-commit: d820485fd81efd08d8626f8476338558c4585c20
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 3%

---


# [!DNL Kevel] conexão {#kevel}

## Visão geral {#overview}

[[!DNL Kevel]](https://www.kevel.com/) fornece a tecnologia habilitada para IA e orientação de especialistas que ajudam líderes comerciais inovadores a lançar, escalar e ter sucesso na mídia de varejo. A Retail Media Cloud do [!DNL Kevel] possibilita formatos de anúncios direcionados, atribuíveis e personalizáveis para publicidade no local e fora do local.

O destino de streaming [!DNL Kevel] para o Adobe Experience Platform permite que os clientes ativem os públicos do Adobe diretamente no UserDB e nas APIs de gerenciamento de segmento do [!DNL Kevel], para oferecer suporte ao direcionamento em tempo real no momento da decisão do anúncio.

>[!IMPORTANT]
> 
>Se você tiver dúvidas ou quiser solicitar uma atualização sobre o destino [!DNL Kevel] ou sua documentação, envie um email para a equipe [!DNL Kevel] em [support@kevel.com](mailto:support@kevel.com).

## Casos de uso {#use-cases}

Você pode ativar públicos-alvo comportamentais primários avançados em suas experiências de mídia de varejo para fornecer anúncios mais relevantes e desempenho mais forte. Na Experience Platform, você constrói públicos-alvo de alto valor e baseados em intenção, como compradores frequentes de categorias ou usuários com interesse recente em produtos, e sincroniza essas associações a [!DNL Kevel] em tempo real. O [!DNL Kevel] disponibiliza imediatamente esses segmentos para decisões de anúncios, permitindo um direcionamento preciso para produtos patrocinados e outros formatos em experiências de pesquisa, navegação e aplicativo. Assim que os usuários forem qualificados, você poderá agir de acordo com esses sinais para gerar impressões mais relevantes, melhor direcionamento e medição e ROAS aprimorados.

## Pré-requisitos {#prerequisites}

Para se preparar para usar o destino [!DNL Kevel], verifique se os seguintes pré-requisitos foram atendidos:

- Você deve ter uma rede **[!DNL Kevel]** ativa e acesso à API.
- Você precisa de uma **[!DNL Kevel]chave de API** com permissões para criar segmentos e atualizar registros do UserDB.
- Você deve configurar namespaces de identidade na Experience Platform que mapeiam para as identidades que seu site ou aplicativo envia durante [!DNL Kevel] solicitações de anúncio (por exemplo, ECID, GAID, IDFA, ID de fidelidade etc.).
- Os clientes do Adobe devem mapear identidades somente que são usadas durante solicitações de anúncios em tempo real, pois cada identidade resultará em um registro UserDB.

## Identidades suportadas {#supported-identities}

O destino [!DNL Kevel] oferece suporte à ativação para qualquer identidade que seu aplicativo possa usar ao enviar solicitações de anúncio para [!DNL Kevel]. Você pode mapear até três namespaces de identidade para gerar registros UserDB correspondentes.

[!DNL Kevel] dá suporte aos seguintes namespaces de identidade da Experience Platform:

| Namespace de identidade | Descrição | Uso típico |
|--------------------|---------------------------------|----------------------------------------------------------------|
| **ECID** | Experience Cloud ID | Usado para personalização no site e identificação entre Adobe. |
| **GAID** | GOOGLE ADVERTISING ID | Usado para tráfego de aplicativo/dispositivo do Android. |
| **IDFA** | APPLE ADVERTISING ID | Usado para tráfego de aplicativo/dispositivo do iOS (sujeito ao consentimento do ATT). |
| **EXTERNAL_ID** | ID externa (identificador personalizado) | Passa IDs proprietárias ou geradas no back-end. |

{style="table-layout:auto"}

### Suporte para namespaces de identidade personalizados

O destino [!DNL Kevel] **também aceita namespaces personalizados**, conforme definido na implementação do Experience Platform.

Isso significa:

- Você pode mapear **namespaces de identidade específicos do cliente** (por exemplo: `loyalty_id`, `gigya_id` ou qualquer identidade personalizada que você tenha definido no Serviço de Identidade).
- Esses namespaces podem ser atribuídos a `kevel_user_key1`, `kevel_user_key2` ou `kevel_user_key3` da mesma forma que os namespaces globais.
- [!DNL Kevel] gerará **um registro UserDB por instância de cada identidade mapeada**, permitindo a correspondência em tempo real em tempo de decisão de anúncio para cada identificador enviado por seus sistemas.

### Comportamento do mapeamento de identidade

- Você pode mapear **até três** namespaces de identidade da Experience Platform para os três slots de identidade de [!DNL Kevel].
- Para cada perfil ativado, [!DNL Kevel] recebe **um registro UserDB por instância de cada identidade mapeada**.
- Os clientes devem mapear apenas as identidades para as quais realmente enviam solicitações de anúncio para [!DNL Kevel] para evitar o armazenamento desnecessário do UserDB.

![Exemplo de mapeamento para Destino Kevel](/help/destinations/assets/catalog/advertising/kevel-destination-mappings.png)

## Públicos-alvo compatíveis {#supported-audiences}

| Origem do público | Suportado | Descrição |
|-----------------------|-----------|---------------------------------------------------------- |
| Serviço de segmentação | Sim | Públicos do perfil do Adobe avaliados pelo mecanismo de segmentação. |
| Uploads personalizados | Não | Não suportado no momento. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

| Item | Tipo | Notas |
|------|------|-------|
| Tipo de exportação | **Exportação de segmentos** | [!DNL Kevel] recebe uma atualização sempre que um perfil se qualifica para ou sai de um público-alvo. |
| Frequência de exportação | **Streaming** | As atualizações são enviadas em tempo real usando a estrutura de transmissão do Destination SDK. |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

Siga o fluxo de trabalho padrão do Experience Platform [conectar um destino](../../ui/connect-destination.md).

>[!IMPORTANT]
> 
>Você deve ter **permissões para Exibir Destinos** e **Gerenciar Destinos**.

### Autenticar para o destino {#authenticate}

Ao conectar-se a [!DNL Kevel], forneça o seguinte campo:

- **Token de portador** — Sua chave de API [!DNL Kevel].

![Opções de autenticação para Destino Kevel](/help/destinations/assets/catalog/advertising/kevel-destination-authentication.png)

### Preencher detalhes do destino {#destination-details}

Após a autenticação, configure:

- **Nome** — Um rótulo para identificar esta instância de destino.
- **Descrição** — Texto opcional para descrever esta instância de destino.
- **[!DNL Kevel]ID de Rede** — Seu [!DNL Kevel] identificador de rede.

![Detalhes do destino do Kevel](/help/destinations/assets/catalog/advertising/kevel-destination-details.png)

## Ativar segmentos para este destino {#activate}

Para enviar públicos-alvo para [!DNL Kevel], siga o fluxo de trabalho em\
[Ative perfis e segmentos para destinos de exportação de segmentos de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Desativação de públicos {#deactivate}

Quando um público-alvo é desativado ou removido do destino [!DNL Kevel] no Experience Platform, a Experience Platform interrompe o envio de mais atualizações de qualificação de perfil para esse público-alvo. Qualquer segmento existente criado em [!DNL Kevel] permanece disponível e não é excluído automaticamente.

Se o segmento [!DNL Kevel] estiver sendo usado atualmente em uma campanha ativa, [!DNL Kevel] impedirá a exclusão para evitar interromper a entrega em tempo real. Nesse caso, a desativação no Experience Platform resulta no seguinte:

- O fluxo de dados do Experience Platform é interrompido
- O segmento [!DNL Kevel] continua a existir e pode permanecer anexado a campanhas até que seja removido manualmente ou a campanha seja atualizada

Para interromper totalmente o direcionamento no [!DNL Kevel], verifique se o segmento foi removido de todas as campanhas ativas no sistema de gerenciamento de campanhas do [!DNL Kevel].

### Mapear atributos e identidades {#map}

[!DNL Kevel] requer:

- **Namespaces de identidade** — Até três namespaces de identidade mapeados para [!DNL Kevel] slots de identidade.
- **Associação de segmento** — Não é necessário mapeamento manual; o Experience Platform passa automaticamente identificadores e aliases de associação de segmento.

Durante a ativação, selecione os namespaces de identidade configurados para [!DNL Kevel]. Cada identidade gerará sua própria chamada de atualização do UserDB.

## Dados exportados / Validar exportação de dados {#exported-data}

Quando um perfil é qualificado para ou sai de um público-alvo, o Experience Platform envia uma atualização de streaming para [!DNL Kevel].

### Carga de exemplo recebida por [!DNL Kevel] UserDB

```json
PUT /udb/{networkId}/segments?userKey=ECID-12345
{
  "segments": [1723, 3344, 9988]
}
```

| Parâmetro | Descrição |
|-----------|-------------|
| **userKey** | Derivado da identidade do Adobe mapeada. |
| **segmentos** | O conjunto de [!DNL Kevel] IDs de segmento correspondentes aos públicos da Adobe para os quais o perfil é realizado no momento. |

{style="table-layout:auto"}

### Exemplo de perfil do Experience Platform usado durante a exportação {#sample-profile}

Ao ativar públicos para o destino [!DNL Kevel], o Experience Platform envia fragmentos de perfil que contêm **qualificações de segmento** e as **identidades mapeadas pelo cliente** para os slots de identidade de [!DNL Kevel].

Veja abaixo um exemplo de um perfil exportado mostrando:

- Vários namespaces de identidade mapeados para `kevel_user_key1`, `kevel_user_key2` e `kevel_user_key3`
- Um único segmento ativado no namespace `ups`

```json
{
  "segmentMembership": {
    "ups": {
      "9d161bbb-c785-474a-965b-7d7bc2adf879": {
        "status": "realized",
        "lastQualificationTime": "2025-12-10T21:43:38.541076Z"
      }
    }
  },
  "identityMap": {
    "kevel_user_key1": [
      {
        "id": "ECID-fN1zo"
      },
      {
        "id": "ECID-9Xr2p"
      }
    ],
    "kevel_user_key2": [
      {
        "id": "GAID-4oic4"
      }
    ],
    "kevel_user_key3": [
      {
        "id": "IDFA-nB5fU"
      }
    ]
  }
}
```

#### Como [!DNL Kevel] interpreta este perfil

Com a configuração de destino [!DNL Kevel], cada identidade mapeada gera um registro UserDB distinto, o que significa que [!DNL Kevel] recebe:

- Uma atualização para `ECID-fN1zo`
- Uma atualização para `ECID-9Xr2p`
- Uma atualização para `GAID-4oic4`
- Uma atualização para `IDFA-nB5fU`

Isso permite que a mesma pessoa seja reconhecida no momento da decisão do anúncio usando qualquer uma de suas identidades disponíveis, com cada identidade carregando um conjunto idêntico de associações de segmento.

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia a [Visão geral da Governança de Dados](/help/data-governance/home.md).

## Recursos adicionais {#additional-resources}

- [[!DNL Kevel] Referência do UserDB](https://dev.kevel.com/reference/userdb)
- [[!DNL Kevel] Segmento de usuário - Direcionamento](https://dev.kevel.com/docs/segment-targeting)
