---
keywords: Experience Platform, introdução, atendimento ao cliente, tópicos populares
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Introdução ao Customer AI
topic-legacy: Getting started
description: Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente.
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# Introdução ao Customer AI

Os guias da API do cliente exigem uma compreensão funcional dos vários serviços da plataforma envolvidos no uso da API do cliente. Antes de começar, reveja os seguintes documentos:

- [Visão geral](../../xdm/home.md) do sistema do Experience Data Model (XDM): O XDM é a estrutura fundamental que permite,  [!DNL Adobe Experience Cloud]viabilizada pelo Experience Platform, enviar a mensagem certa para a pessoa certa, no canal certo, no momento certo. A metodologia na qual o Experience Platform é criado, o Sistema XDM, opera esquemas do Experience Data Model para uso pelos serviços da plataforma.
- [Noções básicas da composição](../../xdm/schema/composition.md) do schema: Este documento fornece uma introdução aos esquemas do Experience Data Model (XDM) e aos blocos de construção, princípios e práticas recomendadas para a composição de schemas a serem usados no  [!DNL Adobe Experience Platform].
- [Criação de schemas](../../xdm/tutorials/create-schema-ui.md): Este tutorial aborda as etapas para criar um esquema usando o Editor de esquemas no Experience Platform.
- [Visão geral](../../rtcdp/overview.md) do Perfil do cliente em tempo real: Criada com a  [!DNL Adobe Experience Platform]Real-time Customer Data Platform (CDP em tempo real), ajuda as empresas a unir dados conhecidos e desconhecidos para ativar perfis do cliente com decisões inteligentes em toda a jornada do cliente. A CDP em tempo real combina várias fontes de dados corporativas para criar perfis unificados em tempo real, que podem ser usados para fornecer experiências personalizadas individuais do cliente em todos os canais e dispositivos.
- [Visão geral](../../segmentation/home.md) do Serviço de segmentação: A segmentação é o processo de definir atributos ou comportamentos específicos compartilhados por um subconjunto de perfis do seu armazenamento de perfil para distinguir um grupo comercializável de pessoas da base de clientes. Por exemplo, em uma campanha de email chamada &quot;Você se esqueceu de comprar seus tênis?&quot;, talvez você queira um público-alvo de todos os usuários que procuraram por tênis de corrida nos últimos 30 dias, mas que não concluíram uma compra. Usando segmentos diferentes, você pode se concentrar em vários públicos-alvo, proporcionando uma experiência de marketing mais personalizada.
- [Guia](../../segmentation/tutorials/create-a-segment.md) do usuário do Construtor de segmentos: A Platform permite criar e acessar segmentos com facilidade, bem como usar diferentes blocos de construção para caracterizar ainda mais seus segmentos.

## Download das pontuações do Customer AI

>[!NOTE]
>
>Se não precisar baixar pontuações brutas, ignore esta etapa e prossiga para o [guia de configuração](./user-guide/configure.md).

O download das pontuações do Customer AI é feito por meio de uma combinação de chamadas de API. Para fazer chamadas para APIs da plataforma, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API do Experience Platform, conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos no Experience Platform são isolados para sandboxes virtuais específicas. Todas as solicitações para APIs da plataforma exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes na Platform, consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

### Lendo exemplos de chamadas de API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md) no guia de solução de problemas do Experience Platform.

## Próximas etapas

Depois de concluir as etapas descritas no documento acima, visite a documentação [Entrada e Saída](./input-output.md). Este documento fornece uma breve visão geral de quais tipos de dados são usados e produzidos no Customer AI.
