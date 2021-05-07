---
keywords: Experience Platform, introdução, ai de atribuição, tópicos populares
solution: Experience Platform, Intelligent Services
title: Introdução ao Attribution AI
topic-legacy: Getting started
description: Os guias a seguir exigem uma compreensão dos vários serviços da Adobe Experience Platform envolvidos com o uso do Attribution AI. Antes de iniciar os tutoriais, revise os seguintes documentos.
exl-id: ab269c24-97ac-4da9-9b6c-7d2dde61f0dc
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# Introdução ao Attribution AI

Os guias a seguir exigem uma compreensão dos vários serviços [!DNL Adobe Experience Platform] envolvidos com o uso do Attribution AI. Antes de iniciar os tutoriais, revise os seguintes documentos:

- [Visão geral](../../xdm/home.md) do sistema do Experience Data Model (XDM): O XDM é a estrutura fundamental que permite,  [!DNL Adobe Experience Cloud]viabilizada pelo Experience Platform, enviar a mensagem certa para a pessoa certa, no canal certo, no momento certo. A metodologia na qual o Experience Platform é criado, o Sistema XDM, opera esquemas do Experience Data Model para uso pelos serviços da plataforma.
- [Noções básicas da composição](../../xdm/schema/composition.md) do schema: Este documento fornece uma introdução aos esquemas do Experience Data Model (XDM) e aos blocos de construção, princípios e práticas recomendadas para a composição de schemas a serem usados no  [!DNL Adobe Experience Platform].
- [Criação de schemas](../../xdm/tutorials/create-schema-ui.md): Este tutorial aborda as etapas para criar um esquema usando o Editor de esquemas no Experience Platform.

O Attribution AI requer que os conjuntos de dados estejam em conformidade com o esquema Eventos de experiência do consumidor (CEE), que é um grupo de campos de esquema [Experience Data Model (XDM)](../../xdm/home.md). Entre em contato com o suporte ao Adobe em attributionai-support@adobe.com para implementar ou fazer alterações nesses dados. Se os dados de gasto de mídia estiverem presentes, você poderá fazer mais análises, como receita incremental e ROI. Se os dados do perfil do cliente estiverem disponíveis, você poderá atribuir mais créditos ao nível do perfil do cliente.

## Terminologia

- **Evento de conversão:** qualquer evento digital ou interação digital que os clientes fazem para indicar um marco em direção a uma meta, como registros de conferência. Exemplos adicionais incluem conversões pagas, inscrições em conta gratuita ou qualificação para uma característica.

- **Ponto de contato:** qualquer evento digital ou interação digital que os clientes fazem no caminho para uma meta. Os exemplos incluem esforços de marketing relacionados ao antes da compra, impressões de exibição de anúncios visualizadas e cliques de pesquisa paga.

## Download de pontuações do Attribution AI

>[!NOTE]
>
>Se não precisar baixar pontuações brutas, ignore esta etapa e prossiga para as [próximas etapas](#next-steps).

O download das pontuações do Attribution AI é feito por meio de uma combinação de chamadas de API. Para fazer chamadas para APIs da plataforma, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API do Experience Platform, conforme mostrado abaixo:

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

## Próximas etapas {#next-steps}

Quando estiver pronto e tiver todas as suas credenciais e esquemas em vigor, comece seguindo o [guia de interface do usuário do Attribution AI](./user-guide.md). Este guia o orienta a criar uma instância e enviá-la para treinamento e pontuação.
