---
keywords: Experience Platform;getting started;attribution ai;popular topics
solution: Experience Platform
title: Introdução ao Attribution AI
topic: Getting started
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---


# Introdução ao Attribution AI

Os guias a seguir exigem uma compreensão dos vários [!DNL Adobe Experience Platform] serviços envolvidos com o uso do Attribution AI. Antes de iniciar os tutoriais, reveja as seguintes documentos:

- [Visão geral](../../xdm/home.md)do sistema do Experience Data Model (XDM): O XDM é a estrutura fundamental que permite, [!DNL Adobe Experience Cloud]acionado pelo Experience Platform, entregar a mensagem certa para a pessoa certa, no canal certo, no momento exato. A metodologia na qual o Experience Platform é criado, o sistema XDM, opera schemas do Experience Data Model para uso pelos serviços da Platform.
- [Noções básicas da composição](../../xdm/schema/composition.md)do schema: Este documento fornece uma introdução aos schemas do Experience Data Model (XDM) e aos blocos de construção, princípios e práticas recomendadas para a composição de schemas a serem usados em [!DNL Adobe Experience Platform].
- [Construção de schemas](../../xdm/tutorials/create-schema-ui.md): Este tutorial aborda as etapas para a criação de um schema usando o Editor de Schemas no Experience Platform.

O Attribution AI exige que os conjuntos de dados estejam em conformidade com o schema Consumer Experience Evento (CEE), que é uma combinação no [Experience Data Model](../../xdm/home.md) (XDM). Entre em contato com o suporte ao Adobe em attributionai-support@adobe.com para implementar ou fazer alterações nesses dados. Se os dados de gastos de mídia estiverem presentes, você poderá fazer mais análises, como receita incremental e ROI. Se os dados do perfil do cliente estiverem disponíveis, você poderá atribuir créditos adicionais ao nível do perfil do cliente.

## Terminologia

- **evento de conversão:** Qualquer evento digital ou interação digital que os clientes façam para indicar um marco em direção a uma meta, como registros de conferência. Exemplos adicionais incluem conversões pagas, inscrições em conta gratuita ou qualificação para uma característica.

- **Ponto de contato:** Qualquer evento digital ou interação digital que os clientes fazem no caminho para uma meta. Os exemplos incluem esforços de marketing relacionados à compra, impressões de exibição de anúncios visualizadas e cliques de pesquisa pagos.

## Download de pontuações de Attribution AI

>[!NOTE]
>
>Se não precisar baixar pontuações brutas, ignore essa etapa e prossiga para as [próximas etapas](#next-steps).

O download das pontuações do Attribution AI é feito por meio de uma combinação de chamadas de API. Para fazer chamadas para as APIs da Platform, você deve primeiro concluir o tutorial [de](../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API de Experience Platform, como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos no Experience Platform são isolados para caixas de proteção virtuais específicas. Todas as solicitações às APIs do Platform exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção no Platform, consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

### Lendo chamadas de exemplo da API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md) de API de exemplo no guia de solução de problemas do Experience Platform.

## Próximas etapas {#next-steps}

Quando estiver pronto e tiver todas as suas credenciais e schemas no lugar, start seguindo o guia [da interface do usuário do](./user-guide.md)Attribution AI. Este guia aborda a criação de uma instância e o envio para treinamento e pontuação.