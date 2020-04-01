---
keywords: Experience Platform;getting started;attribution ai;popular topics
solution: Experience Platform
title: Introdução ao AI de atribuição
topic: Getting started
translation-type: tm+mt
source-git-commit: 14d47f99f1edd7734245b25b7c39f3a71e7aac50

---


# Introdução ao AI de atribuição

Os guias a seguir exigem uma compreensão dos vários serviços da plataforma Adobe Experience envolvidos com o uso da API de atribuição. Antes de iniciar os tutoriais, reveja as seguintes documentos:

- [Visão geral](../../xdm/home.md)do sistema do Experience Data Model (XDM): O XDM é a estrutura fundamental que permite à Adobe Experience Cloud, capacitada pela Experience Platform, fornecer a mensagem certa à pessoa certa, no canal certo, no momento certo. A metodologia na qual a plataforma de experiência é criada, o sistema XDM, opera schemas do modelo de dados de experiência para uso pelos serviços da plataforma.
- [Noções básicas da composição](../../xdm/schema/composition.md)do schema: Este documento fornece uma introdução aos schemas do Experience Data Model (XDM) e aos blocos de construção, princípios e práticas recomendadas para a composição de schemas a serem usados na Adobe Experience Platform.
- [Construção de schemas](../../xdm/tutorials/create-schema-ui.md): Este tutorial aborda as etapas para a criação de um schema usando o Editor de Schemas na Plataforma de experiência.

A Atribuição AI exige que os conjuntos de dados estejam em conformidade com o schema Consumer Experience Eventos (CEE), que é uma combinação no Modelo [de Dados de](../../xdm/home.md) Experiência (XDM). Entre em contato com o suporte da Adobe em attributionai-support@adobe.com para implementar ou fazer alterações nesses dados. Se os dados de gastos de mídia estiverem presentes, você poderá fazer mais análises, como receita incremental e ROI. Se os dados do perfil do cliente estiverem disponíveis, você poderá atribuir créditos adicionais ao nível do perfil do cliente.

## Terminologia

- **evento de conversão:** Qualquer evento digital ou interação digital que os clientes façam para indicar um marco em direção a uma meta, como registros de conferência. Exemplos adicionais incluem conversões pagas, inscrições em conta gratuita ou qualificação para uma característica.

- **Ponto de contato:** Qualquer evento digital ou interação digital que os clientes fazem no caminho para uma meta. Os exemplos incluem esforços de marketing relacionados à compra, impressões de exibição de anúncios visualizadas e cliques de pesquisa pagos.

## Acessar e consultar pontuações

>[!NOTE] Se você não precisar query ou acessar as pontuações brutas, ignore essa etapa e vá para o guia [da interface do](./user-guide.md)usuário.

O acesso e a consulta de pontuações para a Atribuição AI são feitos por meio do Floco de neve. Atualmente, você precisa enviar um email para o suporte da Adobe em attributionai-support@adobe.com para configurar e receber as credenciais para sua conta de leitor do Floco de neve ou exportar dados brutos em massa.

Depois que o suporte da Adobe tiver processado sua solicitação, você receberá um URL para a conta do leitor para Snowflake e as credenciais correspondentes abaixo:

- URL do floco de neve
- Nome do usuário
- Password

## Próximas etapas

Quando estiver pronto e tiver todas as suas credenciais e schemas no lugar, start seguindo o guia [da interface do usuário do](./user-guide.md)AI de atribuição. Este guia aborda a criação de uma instância e o envio para treinamento e pontuação.