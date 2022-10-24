---
keywords: Experience Platform, introdução, atendimento ao cliente, tópicos populares
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Introdução ao Customer AI
topic-legacy: Getting started
description: Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente.
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 1%

---

# Introdução ao Customer AI

Os guias da API do cliente exigem uma compreensão funcional dos vários serviços da plataforma envolvidos no uso da API do cliente. Antes de começar, reveja os seguintes documentos:

- [Visão geral do sistema do Experience Data Model (XDM)](../../xdm/home.md): O XDM é a estrutura básica que permite [!DNL Adobe Experience Cloud], viabilizada por Experience Platform, para enviar a mensagem certa à pessoa certa, no canal certo, no momento certo. A metodologia na qual o Experience Platform é criado, o Sistema XDM, opera esquemas do Experience Data Model para uso pelos serviços da plataforma.
- [Noções básicas da composição do schema](../../xdm/schema/composition.md): Este documento fornece uma introdução aos esquemas do Experience Data Model (XDM) e aos blocos de construção, princípios e práticas recomendadas para a composição de schemas a serem usados em [!DNL Adobe Experience Platform].
- [Criação de schemas](../../xdm/tutorials/create-schema-ui.md): Este tutorial aborda as etapas para criar um esquema usando o Editor de esquemas no Experience Platform.
- [Visão geral do perfil do cliente em tempo real](../../rtcdp/overview.md): Criado em [!DNL Adobe Experience Platform], o Adobe Real-time Customer Data Platform (Real-Time CDP) ajuda as empresas a unir dados conhecidos e desconhecidos para ativar perfis do cliente com decisões inteligentes na jornada do cliente. O Real-Time CDP combina várias fontes de dados corporativas para criar perfis unificados em tempo real, que podem ser usados para fornecer experiências personalizadas de clientes individuais em todos os canais e dispositivos.
- [Visão geral do serviço de segmentação](../../segmentation/home.md): A segmentação é o processo de definir atributos ou comportamentos específicos compartilhados por um subconjunto de perfis do seu armazenamento de perfil para distinguir um grupo comercializável de pessoas da base de clientes. Por exemplo, em uma campanha de email chamada &quot;Você se esqueceu de comprar seus tênis?&quot;, talvez você queira um público-alvo de todos os usuários que procuraram por tênis de corrida nos últimos 30 dias, mas que não concluíram uma compra. Usando segmentos diferentes, você pode se concentrar em vários públicos-alvo, proporcionando uma experiência de marketing mais personalizada.
- [Guia do usuário do Construtor de segmentos](../../segmentation/tutorials/create-a-segment.md): A Platform permite criar e acessar segmentos com facilidade, bem como usar diferentes blocos de construção para caracterizar ainda mais seus segmentos.

## Download das pontuações do Customer AI

>[!NOTE]
>
>Se não precisar baixar pontuações brutas, ignore esta etapa e prossiga para a [guia de configuração](./user-guide/configure.md).

O download das pontuações do Customer AI é feito por meio de uma combinação de chamadas de API. Para fazer chamadas para APIs da plataforma, primeiro conclua o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API do Experience Platform, conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos os recursos no Experience Platform são isolados para sandboxes virtuais específicas. Todas as solicitações para APIs da plataforma exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes na Platform, consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

### Lendo exemplos de chamadas de API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../landing/troubleshooting.md) no guia de solução de problemas do Experience Platform.

## Controle de acesso {#access-control}

Ao usar o controle de acesso, a variável **Exibir AI do cliente** e **Gerenciar o Customer AI** concede acesso a diferentes funcionalidades da API do cliente. O **Gerenciar o Customer AI** permissão permite **criar**,**atualizar**, **excluir**, **habilitar** ou **disable** uma instância ao **Exibir AI do cliente** permite que você leia ou visualize. O **criar**, **atualizar** e **excluir** ações são registradas por logs de auditoria.

Consulte a documentação para saber mais [atribuição de permissões para controle de acesso](../../../help/access-control/home.md) ou como [usar logs de auditoria para monitorar o acesso e a atividade](../../../help/landing/governance-privacy-security/audit-logs/overview.md).

## Próximas etapas

Depois de concluir as etapas descritas no documento acima, visite o [Entrada e saída](./input-output.md) documentação. Este documento fornece uma breve visão geral de quais tipos de dados são usados e produzidos no Customer AI.
