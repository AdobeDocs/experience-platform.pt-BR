---
keywords: Experience Platform, home, tópicos populares, api do serviço de identidade, guia do desenvolvedor do serviço de identidade, região
solution: Experience Platform
title: Guia da API do Serviço de identidade
topic-legacy: API guide
description: A API do Serviço de identidade permite que os desenvolvedores gerenciem a identificação entre dispositivos, entre canais e quase em tempo real dos clientes usando gráficos de identidade no Adobe Experience Platform. Siga este manual para saber como executar operações importantes usando a API.
exl-id: d612af38-4648-4c3e-8cfd-3f306c9370e1
source-git-commit: f269a7b1584a6e4a0e1820a0c587a647c0c8f7b5
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 3%

---

# [!DNL Identity Service] Manual da API

O Adobe Experience Platform [!DNL Identity Service] gerencia a identificação entre dispositivos, entre canais e quase em tempo real dos clientes no que é conhecido como um gráfico de identidade no Adobe Experience Platform.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Identity Service]](../home.md): Resolve o desafio fundamental colocado pela fragmentação dos dados de perfil do cliente. Ele faz isso através da conexão de identidades entre dispositivos e sistemas, onde os clientes interagem com a sua marca.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Platform] organiza os dados de experiência do cliente.

As seções a seguir fornecem informações adicionais que você precisará saber ou ter em mãos para fazer chamadas com êxito para a API [!DNL Identity Service].

### Lendo exemplos de chamadas de API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

### Roteamento baseado na região

A API [!DNL Identity Service] emprega endpoints específicos da região que exigem a inclusão de um `{REGION}` como parte do caminho da solicitação. Durante o provisionamento da organização IMS, uma região é determinada e armazenada no perfil da Organização IMS. Usar a região correta com cada endpoint garante que todas as solicitações feitas usando a API [!DNL Identity Service] sejam roteadas para a região apropriada.

Há duas regiões atualmente compatíveis com [!DNL Identity Service] APIs: VA7 e NLD2.

A tabela abaixo mostra exemplos de caminhos usando regiões:

| Serviço de | Região: VA7 | Região: NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe.</span>io/data/core/namespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/namespace{ENDPOINT} |

>[!NOTE]
>
>As solicitações feitas sem especificar uma região podem resultar no roteamento de chamadas para a região incorreta ou causar falha inesperada de chamadas.

Se você não conseguir localizar a região no seu perfil da Organização IMS, entre em contato com o administrador do sistema para obter suporte.

## Uso da API [!DNL Identity Service]

Os parâmetros de identidade utilizados nestes serviços podem ser expressos de uma das duas formas seguintes: composto ou XID.

Identidades compostas são construções que incluem o valor da ID e o namespace. Ao usar identidades compostas, o namespace pode ser fornecido pelo nome (`namespace.code`) ou ID (`namespace.id`).

Quando uma identidade é persistente, [!DNL Identity Service] gera e atribui uma ID a essa identidade, chamada de ID nativa ou XID. Todas as variações de APIs de Cluster e Mapeamento são compatíveis com identidades compostas e XID em suas solicitações e resposta. Um dos parâmetros é necessário - `xid` ou combinação de [`ns` ou `nsid`] e `id` para usar essas APIs.

Para limitar a carga nas respostas, as APIs adaptam suas respostas ao tipo de construção de identidade usada. Ou seja, se você passar o XID, suas respostas terão XIDs, se você passar identidades compostas, a resposta seguirá a estrutura usada na solicitação.

Os exemplos neste documento não cobrem a funcionalidade completa da API [!DNL Identity Service]. Para obter a API completa, consulte a [Referência da API Swagger](https://www.adobe.io/experience-platform-apis/references/identity-service).

>[!NOTE]
>
>Todas as identidades retornadas estarão no formulário XID nativo quando o XID nativo for usado na solicitação. É recomendável usar o formulário ID/namespace. Para obter mais informações, consulte a seção sobre [obter o XID para uma identidade](./create-custom-namespace.md).

## Próximas etapas

Agora que você coletou as credenciais necessárias, pode continuar a ler o resto do guia do desenvolvedor. Cada seção fornece informações importantes sobre seus endpoints e demonstra chamadas de API de exemplo para executar operações CRUD. Cada chamada inclui o formato da API geral, uma solicitação de amostra que mostra os cabeçalhos necessários e as cargas corretamente formatadas e uma resposta de amostra para uma chamada bem-sucedida.
