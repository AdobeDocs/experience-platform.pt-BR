---
keywords: Experience Platform;home;popular topics;identidade service api;identity service developer guide;region
solution: Experience Platform
title: Introdução
topic: API guide
description: 'O Adobe Experience Platform Identity Service gerencia a identificação de dispositivos cruzados, canais cruzados e quase em tempo real de seus clientes no que é conhecido como um gráfico de identidade no Adobe Experience Platform. '
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 1%

---


# [!DNL Identity Service] Guia do desenvolvedor da API

A Adobe Experience Platform [!DNL Identity Service] gerencia a identificação de dispositivos cruzados, canais cruzados e quase em tempo real de seus clientes no que é conhecido como um gráfico de identidade no Adobe Experience Platform.

## Introdução

Este guia exige uma compreensão prática dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Identity Service]](../home.md): Resolve o desafio fundamental colocado pela fragmentação dos dados do perfil do cliente. Ele faz isso ao fazer a ponte de identidades entre dispositivos e sistemas nos quais os clientes interagem com sua marca.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil unificado e de consumidor em tempo real, com base em dados agregados de várias fontes.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Platform] organiza os dados de experiência do cliente.

As seções a seguir fornecem informações adicionais que você precisará conhecer ou ter em mãos para fazer chamadas com êxito para a API [!DNL Identity Service].

### Lendo chamadas de exemplo da API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção em [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a [documentação de visão geral da caixa de proteção](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

### Roteamento baseado na região

A API [!DNL Identity Service] emprega pontos finais específicos da região que exigem a inclusão de um `{REGION}` como parte do caminho da solicitação. Durante o provisionamento da organização IMS, uma região é determinada e armazenada no perfil de organização IMS. Usar a região correta com cada endpoint garante que todas as solicitações feitas usando a API [!DNL Identity Service] sejam encaminhadas para a região apropriada.

Há duas regiões atualmente suportadas por [!DNL Identity Service] APIs: VA7 e NLD2.

A tabela abaixo mostra os caminhos de exemplo usando regiões:

| Serviço de | Região: VA7 | Região: NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>As solicitações feitas sem especificar uma região podem resultar no roteamento de chamadas para a região incorreta ou causar falhas inesperadas de chamadas.

Se você não conseguir localizar a região dentro do perfil IMS Org, entre em contato com o administrador do sistema para obter suporte.

## Uso da API [!DNL Identity Service]

Os parâmetros de identidade utilizados nestes serviços podem ser expressos de duas formas; composto ou XID.

Identidades compostas são construções que incluem o valor da ID e a namespace. Ao usar identidades compostas, a namespace pode ser fornecida pelo nome (`namespace.code`) ou ID (`namespace.id`).

Quando uma identidade é persistente, [!DNL Identity Service] gera e atribui uma ID a essa identidade, chamada de ID nativa ou XID. Todas as variações das APIs de cluster e mapeamento suportam identidades compostas e XID em suas solicitações e respostas. Um dos parâmetros é necessário - `xid` ou uma combinação de [`ns` ou `nsid`] e `id` para usar essas APIs.

Para limitar a carga em respostas, as APIs adaptam suas respostas ao tipo de construção de identidade usada. Ou seja, se você passar o XID suas respostas terão XIDs, se você passar identidades compostas, a resposta seguirá a estrutura usada na solicitação.

Os exemplos neste documento não abrangem a funcionalidade completa da API [!DNL Identity Service]. Para obter a API completa, consulte [Referência da API do Swagger](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml).

>[!NOTE]
>
>Todas as identidades retornadas estarão no formulário XID nativo quando o XID nativo for usado na solicitação. É recomendável usar o formulário de ID/namespace. Para obter mais informações, consulte a seção sobre [obter o XID para uma identidade](./create-custom-namespace.md).

## Próximas etapas

Agora que você reuniu as credenciais necessárias, pode continuar a ler o restante do guia do desenvolvedor. Cada seção fornece informações importantes sobre seus pontos de extremidade e demonstra exemplos de chamadas de API para executar operações CRUD. Cada chamada inclui o formato de API geral, uma solicitação de amostra mostrando os cabeçalhos necessários e as cargas formatadas corretamente e uma resposta de amostra para uma chamada bem-sucedida.
