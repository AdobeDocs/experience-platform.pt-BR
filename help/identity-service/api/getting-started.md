---
keywords: Experience Platform;página inicial;tópicos populares;api do serviço de identidade;guia do desenvolvedor do serviço de identidade;região
solution: Experience Platform
title: Guia da API do Serviço de identidade
description: A API do serviço de identidade permite que os desenvolvedores gerenciem a identificação entre dispositivos, canais e quase em tempo real dos clientes usando gráficos de identidade no Adobe Experience Platform. Siga este manual para saber como executar operações importantes usando a API.
role: Developer
exl-id: d612af38-4648-4c3e-8cfd-3f306c9370e1
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 14%

---

# [!DNL Identity Service] Manual da API

O Adobe Experience Platform [!DNL Identity Service] gerencia a identificação entre dispositivos, canais e quase em tempo real dos clientes no que é conhecido como um gráfico de identidade no Adobe Experience Platform.

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

- [[!DNL Identity Service]](../home.md): resolve o desafio fundamental colocado pela fragmentação dos dados de perfil do cliente. Ele faz isso unindo identidades em dispositivos e sistemas nos quais os clientes interagem com sua marca.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de múltiplas fontes.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Platform] organiza os dados de experiência do cliente.

As seções a seguir fornecem informações adicionais que você precisará saber ou ter disponíveis para fazer chamadas com êxito para a API [!DNL Identity Service].

### Leitura de chamadas de API de amostra

Este manual fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para APIs do [!DNL Platform], primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API da [!DNL Experience Platform], conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] estão isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm um conteúdo (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

### Roteamento baseado em região

A API [!DNL Identity Service] emprega pontos de extremidade específicos da região que exigem a inclusão de um `{REGION}` como parte do caminho da solicitação. Durante o provisionamento da organização, uma região é determinada e armazenada no perfil da organização. Usar a região correta com cada ponto de extremidade garante que todas as solicitações feitas usando a API [!DNL Identity Service] sejam roteadas para a região apropriada.

Atualmente, há duas regiões compatíveis com APIs do [!DNL Identity Service]: VA7 e NLD2.

A tabela abaixo mostra caminhos de exemplo usando regiões:

| Serviço | Região: VA7 | Região: NLD2 |
| ------ | -------- |--------- |
| API [!DNL Identity Service] | https://</span>platform-va7.adobe.</span>io/dados/núcleo/identidade/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/dados/núcleo/identidade/{ENDPOINT} |
| API [!DNL Identity Namespace] | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>As solicitações feitas sem especificar uma região podem resultar no roteamento de chamadas para a região incorreta ou fazer com que as chamadas falhem inesperadamente.

Se não conseguir localizar a região no perfil da organização, entre em contato com o administrador do sistema para obter suporte.

## Usando a API [!DNL Identity Service]

Os parâmetros de identidade usados nesses serviços podem ser expressos de uma das duas formas: composta ou XID.

Identidades compostas são construções que incluem o valor de ID e o namespace. Ao usar identidades compostas, o namespace pode ser fornecido por nome (`namespace.code`) ou ID (`namespace.id`).

Quando uma identidade é persistente, o [!DNL Identity Service] gera e atribui uma ID a essa identidade, chamada de ID nativa ou XID. Todas as variações de APIs de cluster e mapeamento oferecem suporte a identidades compostas e XID em suas solicitações e respostas. Um dos parâmetros é necessário - `xid` ou combinação de [`ns` ou `nsid`] e `id` para usar essas APIs.

Para limitar o conteúdo nas respostas, as APIs adaptam suas respostas ao tipo de construção de identidade usada. Ou seja, se você passar XID, suas respostas terão XIDs. Se você passar identidades compostas, a resposta seguirá a estrutura usada na solicitação.

Os exemplos neste documento não abrangem a funcionalidade completa da API [!DNL Identity Service]. Para obter a API completa, consulte a [Referência da API do Swagger](https://www.adobe.io/experience-platform-apis/references/identity-service).

>[!NOTE]
>
>Todas as identidades retornadas estarão no formato XID nativo quando o XID nativo for usado na solicitação. É recomendado usar o formulário de ID/namespace. Para obter mais informações, consulte a seção sobre [obtenção de XID para uma identidade](./create-custom-namespace.md).

## Próximas etapas

Agora que você reuniu as credenciais necessárias, pode continuar lendo o restante do guia do desenvolvedor. Cada seção fornece informações importantes sobre seus endpoints e demonstra exemplos de chamadas de API para executar operações CRUD. Cada chamada inclui o formato da API geral, uma solicitação de amostra mostrando os cabeçalhos necessários e cargas úteis formatadas corretamente e uma resposta de amostra para uma chamada bem-sucedida.
