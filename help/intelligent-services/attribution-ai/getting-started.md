---
keywords: Experience Platform;introdução;atribuição ai;tópicos populares;;getting started;attribution ai;popular topics
feature: Attribution AI
title: Introdução ao Attribution AI
description: Os guias a seguir exigem a compreensão dos vários serviços da Adobe Experience Platform envolvidos no uso do Attribution AI. Antes de iniciar os tutoriais, revise os documentos a seguir.
exl-id: ab269c24-97ac-4da9-9b6c-7d2dde61f0dc
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 1%

---

# Introdução ao Attribution AI

Os guias a seguir exigem a compreensão dos vários [!DNL Adobe Experience Platform] serviços envolvidos na utilização do Attribution AI. Antes de iniciar os tutoriais, revise os seguintes documentos:

- [Visão geral do sistema do Experience Data Model (XDM)](../../xdm/home.md): o XDM é a estrutura fundamental que permite [!DNL Adobe Experience Cloud], habilitado por Experience Platform, para enviar a mensagem certa à pessoa certa, no canal direito, no momento exato. A metodologia na qual o Experience Platform é criado, o Sistema XDM, operacionaliza esquemas do Modelo de dados de experiência para uso pelos serviços da plataforma.
- [Noções básicas da composição do esquema](../../xdm/schema/composition.md): este documento fornece uma introdução aos esquemas do Experience Data Model (XDM) e aos elementos, princípios e práticas recomendadas para a composição de esquemas a serem usados no [!DNL Adobe Experience Platform].
- [Criação de esquemas](../../xdm/tutorials/create-schema-ui.md): Este tutorial aborda as etapas para a criação de um esquema usando o Editor de esquemas no Experience Platform.

O Attribution AI exige que os conjuntos de dados estejam em conformidade com o esquema Consumer Experience Events (CEE), que é um [Experience Data Model (XDM)](../../xdm/home.md) grupo de campos de esquema. Entre em contato com o suporte da Adobe em attributionai-support@adobe.com para implementar ou fazer alterações nesses dados. Se os dados de gastos de mídia estiverem presentes, você poderá fazer mais análises, como receita incremental e ROI. Se os dados do perfil do cliente estiverem disponíveis, você poderá atribuir mais créditos ao nível do perfil do cliente.

## Terminologia

- **Evento de conversão:** Qualquer evento digital ou interação digital que os clientes façam para indicar um marco em direção a uma meta, como inscrições em conferências. Outros exemplos incluem conversões pagas, inscrições em contas gratuitas ou qualificação para uma característica.

- **Ponto de contato:** Qualquer evento digital ou interação digital que os clientes façam no caminho em direção a uma meta. Os exemplos incluem esforços de marketing relacionados a compras, impressões de publicidade exibidas e cliques de pesquisa pagos.

## Baixando pontuações do Attribution AI

>[!NOTE]
>
>Se não precisar baixar pontuações brutas, ignore esta etapa e prossiga para a [próximas etapas](#next-steps).

O download das pontuações do Attribution AI é feito por meio de uma combinação de chamadas de API. Para fazer chamadas para APIs da Platform, primeiro conclua o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API de Experience Platform, conforme mostrado abaixo:

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

## Controle de acesso {#access-control}

Ao usar o controle de acesso baseado em função, a variável **Exibir Attribution AI** e **Gerenciar Attribution AI** Os privilégios concedem acesso a diferentes funcionalidades do Attribution AI. A variável **Gerenciar Attribution AI** permite **criar**, **clone**, **editar**, **excluir**, **habilitar** ou **disable** uma instância enquanto **Exibir Attribution AI** permite **ler** ou **exibir** o mesmo. A variável **criar**, **editar** e **excluir** as ações são registradas por logs de auditoria.

Consulte a documentação para saber mais [atribuição de permissões para controle de acesso](../../../help/access-control/home.md) ou como [usar logs de auditoria para monitorar o acesso e a atividade](../../../help/landing/governance-privacy-security/audit-logs/overview.md).

## Próximas etapas {#next-steps}

Quando estiver pronto e tiver todas as credenciais e esquemas em vigor, comece seguindo o [guia da interface do usuário do Attribution AI](./user-guide.md). Este guia orienta você na criação de uma instância e no envio para treinamento e pontuação.
