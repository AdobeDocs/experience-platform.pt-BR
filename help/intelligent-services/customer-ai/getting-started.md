---
keywords: Experience Platform;introdução;ia do cliente;tópicos populares;getting started;customer ai;popular topics
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Introdução à IA do cliente
description: Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente.
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
source-git-commit: 07a110f6d293abff38804b939014e28f308e3b30
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---

# Introdução à IA do cliente

Os guias da IA do cliente exigem uma compreensão funcional dos vários serviços da plataforma envolvidos no uso da IA do cliente. Antes de começar, revise os seguintes documentos:

- [Visão geral do sistema do Experience Data Model (XDM)](../../xdm/home.md): o XDM é a estrutura fundamental que permite [!DNL Adobe Experience Cloud], habilitado por Experience Platform, para enviar a mensagem certa à pessoa certa, no canal direito, no momento exato. A metodologia na qual o Experience Platform é criado, o Sistema XDM, operacionaliza esquemas do Modelo de dados de experiência para uso pelos serviços da plataforma.
- [Noções básicas da composição do esquema](../../xdm/schema/composition.md): este documento fornece uma introdução aos esquemas do Experience Data Model (XDM) e aos elementos, princípios e práticas recomendadas para a composição de esquemas a serem usados no [!DNL Adobe Experience Platform].
- [Criação de esquemas](../../xdm/tutorials/create-schema-ui.md): Este tutorial aborda as etapas para a criação de um esquema usando o Editor de esquemas no Experience Platform.
- [Visão geral do Perfil do cliente em tempo real](../../rtcdp/overview.md): Criado em [!DNL Adobe Experience Platform], o Adobe Real-time Customer Data Platform (Real-Time CDP) ajuda as empresas a unirem dados conhecidos e desconhecidos para ativar perfis de clientes com decisões inteligentes em toda a jornada do cliente. A Real-Time CDP combina várias fontes de dados corporativas para criar perfis unificados em tempo real, que podem ser usados para fornecer experiências personalizadas individuais do cliente em todos os canais e dispositivos.
- [Visão geral do serviço de segmentação](../../segmentation/home.md): a segmentação é o processo de definir atributos ou comportamentos específicos compartilhados por um subconjunto de perfis da sua loja de perfis para distinguir um grupo comercializável de pessoas da sua base de clientes. Por exemplo, em uma campanha de email chamada &quot;Você se esqueceu de comprar seu tênis?&quot;, você pode querer um público de todos os usuários que procuraram tênis de corrida nos últimos 30 dias, mas que não concluíram uma compra. Usando segmentos diferentes, você pode se concentrar em seus vários públicos, fornecendo uma experiência de marketing mais personalizada.
- [Guia do usuário do Construtor de segmentos](../../segmentation/tutorials/create-a-segment.md): O Platform permite que você crie e acesse segmentos facilmente, bem como use diferentes blocos de construção para caracterizar ainda mais seus segmentos.

## Download das pontuações da IA do cliente

>[!NOTE]
>
>Se não precisar baixar pontuações brutas, ignore esta etapa e prossiga para a [guia de configuração](./user-guide/configure.md).

O download das pontuações da IA do cliente é feito por meio de uma combinação de chamadas de API. Para fazer chamadas para APIs da Platform, primeiro conclua o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API de Experience Platform, conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos os recursos no Experience Platform são isolados em sandboxes virtuais específicas. Todas as solicitações para APIs da Platform exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes na Platform, consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

### Leitura de chamadas de API de amostra

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O exemplo de JSON retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md) no guia de solução de problemas de Experience Platform.

## Próximas etapas

Depois de concluir as etapas descritas no documento acima, visite o [Entrada e Saída](./data-requirements.md) documentação. Este documento fornece uma breve visão geral de quais tipos de dados são usados e produzidos na IA do cliente.
