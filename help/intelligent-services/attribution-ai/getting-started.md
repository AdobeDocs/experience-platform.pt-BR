---
keywords: Experience Platform;getting started;attribution ai;popular topics
solution: Experience Platform
title: Introdução ao AI de atribuição
topic: Getting started
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---


# Introdução ao AI de atribuição

Os guias a seguir exigem uma compreensão dos vários [!DNL Adobe Experience Platform] serviços envolvidos com o uso da API de atribuição. Antes de iniciar os tutoriais, reveja as seguintes documentos:

- [Visão geral](../../xdm/home.md)do sistema do Experience Data Model (XDM): O XDM é a estrutura fundamental que permite, [!DNL Adobe Experience Cloud]acionada pela plataforma Experience, entregar a mensagem certa para a pessoa certa, no canal certo, no momento exato. A metodologia na qual a plataforma de experiência é criada, o sistema XDM, opera schemas do modelo de dados de experiência para uso pelos serviços da plataforma.
- [Noções básicas da composição](../../xdm/schema/composition.md)do schema: Este documento fornece uma introdução aos schemas do Experience Data Model (XDM) e aos blocos de construção, princípios e práticas recomendadas para a composição de schemas a serem usados em [!DNL Adobe Experience Platform].
- [Construção de schemas](../../xdm/tutorials/create-schema-ui.md): Este tutorial aborda as etapas para a criação de um schema usando o Editor de Schemas na Plataforma de experiência.

A Atribuição AI exige que os conjuntos de dados estejam em conformidade com o schema Consumer Experience Eventos (CEE), que é uma combinação no Modelo [de Dados de](../../xdm/home.md) Experiência (XDM). Entre em contato com o suporte da Adobe em attributionai-support@adobe.com para implementar ou fazer alterações nesses dados. Se os dados de gastos de mídia estiverem presentes, você poderá fazer mais análises, como receita incremental e ROI. Se os dados do perfil do cliente estiverem disponíveis, você poderá atribuir créditos adicionais ao nível do perfil do cliente.

## Terminologia

- **evento de conversão:** Qualquer evento digital ou interação digital que os clientes façam para indicar um marco em direção a uma meta, como registros de conferência. Exemplos adicionais incluem conversões pagas, inscrições em conta gratuita ou qualificação para uma característica.

- **Ponto de contato:** Qualquer evento digital ou interação digital que os clientes fazem no caminho para uma meta. Os exemplos incluem esforços de marketing relacionados à compra, impressões de exibição de anúncios visualizadas e cliques de pesquisa pagos.

## Download das pontuações da Atribuição AI

>[!NOTE] Se não precisar baixar pontuações brutas, ignore essa etapa e prossiga para as [próximas etapas](#next-steps).

Baixar as pontuações da Atribuição AI é feito por meio de uma combinação de chamadas de API. Para fazer chamadas para APIs de plataforma, você deve primeiro concluir o tutorial [de](../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas da API da plataforma da experiência, como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos da plataforma Experience são isolados para caixas de proteção virtuais específicas. Todas as solicitações para APIs de plataforma exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Para obter mais informações sobre caixas de proteção na Plataforma, consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

### Lendo chamadas de exemplo da API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md) de API de exemplo no guia de solução de problemas da plataforma Experience.

## Próximas etapas {#next-steps}

Quando estiver pronto e tiver todas as suas credenciais e schemas no lugar, start seguindo o guia [da interface do usuário do](./user-guide.md)AI de atribuição. Este guia aborda a criação de uma instância e o envio para treinamento e pontuação.