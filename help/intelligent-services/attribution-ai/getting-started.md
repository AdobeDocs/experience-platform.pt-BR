---
keywords: Experience Platform;introdução;ia de atribuição;tópicos populares;;getting started;attribution ai;popular topics
feature: Attribution AI
title: Introdução à IA de atribuição
description: Os guias a seguir exigem uma compreensão dos vários serviços da Adobe Experience Platform envolvidos no uso da IA de atribuição. Antes de iniciar os tutoriais, revise os documentos a seguir.
exl-id: ab269c24-97ac-4da9-9b6c-7d2dde61f0dc
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 6%

---

# Introdução à IA de atribuição

Os guias a seguir exigem uma compreensão dos vários serviços do [!DNL Adobe Experience Platform] envolvidos no uso da IA de atribuição. Antes de iniciar os tutoriais, revise os seguintes documentos:

- [Visão geral do Sistema do Experience Data Model (XDM)](../../xdm/home.md): o XDM é a estrutura fundamental que permite ao [!DNL Adobe Experience Cloud], viabilizado pelo Experience Platform, enviar a mensagem certa à pessoa certa, no canal direito, no momento exato. A metodologia na qual o Experience Platform é criado, o Sistema XDM, operacionaliza esquemas do Modelo de dados de experiência para uso pelos serviços da Experience Platform.
- [Noções básicas sobre a composição de esquemas](../../xdm/schema/composition.md): este documento fornece uma introdução aos esquemas do Experience Data Model (XDM) e aos elementos, princípios e práticas recomendadas para a composição de esquemas a serem usados em [!DNL Adobe Experience Platform].
- [Criação de esquemas](../../xdm/tutorials/create-schema-ui.md): este tutorial aborda as etapas para a criação de um esquema usando o Editor de esquemas no Experience Platform.

A IA de atribuição exige que os conjuntos de dados estejam em conformidade com o esquema Consumer Experience Events (CEE), que é um grupo de campos de esquema do [Experience Data Model (XDM)](../../xdm/home.md). Entre em contato com o suporte da Adobe em attributionai-support@adobe.com para implementar ou fazer alterações nesses dados. Se os dados de gastos de mídia estiverem presentes, você poderá fazer mais análises, como receita incremental e ROI. Se os dados do perfil do cliente estiverem disponíveis, você poderá atribuir mais créditos ao nível do perfil do cliente.

## Terminologia

- **Evento de conversão**: qualquer evento digital ou interação digital que os clientes façam para indicar um marco rumo a uma meta, como inscrições em conferências. Outros exemplos incluem conversões pagas, inscrições em contas gratuitas ou qualificação para uma característica.

- **Ponto de contato:** Qualquer evento ou interação digital que os clientes façam no caminho para uma meta. Os exemplos incluem esforços de marketing relacionados a compras, impressões de publicidade exibidas e cliques de pesquisa pagos.

## Baixar pontuações da IA de atribuição

>[!NOTE]
>
>Se não precisar baixar pontuações brutas, ignore esta etapa e vá para as [próximas etapas](#next-steps).

O download das pontuações da IA de atribuição é feito por meio de uma combinação de chamadas de API. Para fazer chamadas para APIs do Experience Platform, primeiro conclua o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores de cada um dos cabeçalhos necessários em todas as chamadas de API do Experience Platform, conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id `{ORG_ID}`

Todos os recursos no Experience Platform são isolados em sandboxes virtuais específicas. Todas as solicitações para APIs do Experience Platform exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes na Experience Platform, consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

### Leitura de chamadas de API de amostra

Este manual fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md) no guia de solução de problemas do Experience Platform.

## Controle de acesso {#access-control}

Ao usar o controle de acesso baseado em função, os privilégios **Exibir IA de atribuição** e **Gerenciar IA de atribuição** concedem acesso a diferentes funcionalidades da IA de atribuição. A **IA de Gerenciar Atribuição** permite **criar**, **clonar**, **editar**, **excluir**, **habilitar** ou **desabilitar** uma instância, enquanto a **IA de Atribuição** permite **ler** ou **exibir**. As ações **criar**, **editar** e **excluir** são registradas por logs de auditoria.

Consulte a documentação para saber [atribuir permissões para controle de acesso](../../../help/access-control/home.md) ou como [usar logs de auditoria para monitorar acesso e atividade](../../../help/landing/governance-privacy-security/audit-logs/overview.md).

## Próximas etapas {#next-steps}

Quando estiver pronto e tiver todas as credenciais e esquemas em vigor, comece seguindo o [guia da interface do usuário da IA de atribuição](./user-guide.md). Este guia orienta você na criação de uma instância e no envio para treinamento e pontuação.
