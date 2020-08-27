---
keywords: Experience Platform;getting started;customer ai;popular topics
solution: Experience Platform
title: Introdução à IA do cliente
topic: Getting started
description: Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente.
translation-type: tm+mt
source-git-commit: c30bbaead775e68f869b080e24e18d4a23cda973
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 0%

---


# Introdução à IA do cliente

Os guias da API do cliente exigem uma compreensão funcional dos vários serviços da plataforma envolvidos no uso da IA do cliente. Antes do start, reveja os seguintes documentos:

- [Visão geral](../../xdm/home.md)do sistema do Experience Data Model (XDM): O XDM é a estrutura fundamental que permite, [!DNL Adobe Experience Cloud]acionado pelo Experience Platform, entregar a mensagem certa para a pessoa certa, no canal certo, no momento exato. A metodologia na qual o Experience Platform é criado, o Sistema XDM, opera schemas do Modelo de Dados da Experiência para uso pelos serviços da plataforma.
- [Noções básicas da composição](../../xdm/schema/composition.md)do schema: Este documento fornece uma introdução aos schemas do Experience Data Model (XDM) e aos blocos de construção, princípios e práticas recomendadas para a composição de schemas a serem usados em [!DNL Adobe Experience Platform].
- [Construção de schemas](../../xdm/tutorials/create-schema-ui.md): Este tutorial aborda as etapas para a criação de um schema usando o Editor de Schemas no Experience Platform.
- [Visão geral](../../rtcdp/overview.md)do Perfil do cliente em tempo real: Criada [!DNL Adobe Experience Platform], [!DNL Adobe Real-time Customer Data Platform] (CDP em tempo real) ajuda as empresas a unir dados conhecidos e desconhecidos para ativar perfis de clientes com decisões inteligentes durante toda a jornada do cliente. A CDP em tempo real combina várias fontes de dados corporativos para criar perfis unificados em tempo real que podem ser usados para fornecer experiências personalizadas individuais do cliente em todos os canais e dispositivos.
- [Visão geral](../../segmentation/home.md)do Serviço de segmentação: A segmentação é o processo de definição de atributos ou comportamentos específicos compartilhados por um subconjunto de perfis da sua loja de perfis para diferenciar um grupo comercializável de pessoas da sua base de clientes. Por exemplo, em uma campanha de email chamada &quot;Você esqueceu de comprar seus tênis?&quot;, você pode querer uma audiência de todos os usuários que procuraram tênis de corrida nos últimos 30 dias, mas que não concluíram uma compra. Usando diferentes segmentos, você pode se concentrar em suas várias audiências, oferecendo uma experiência de marketing mais personalizada.
- [Guia](../../segmentation/tutorials/create-a-segment.md)do usuário do Construtor de segmentos: A plataforma permite que você crie e acesse segmentos com facilidade, além de usar diferentes blocos de construção para caracterizar ainda mais seus segmentos.

## Download das pontuações da AI do cliente

>[!NOTE]
>
>Se não precisar baixar pontuações brutas, ignore essa etapa e vá para o guia [de](./user-guide/configure.md)configuração.

O download das pontuações da AI do cliente é feito por meio de uma combinação de chamadas de API. Para fazer chamadas para APIs de plataforma, você deve primeiro concluir o tutorial [de](../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API de Experience Platform, como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos no Experience Platform são isolados para caixas de proteção virtuais específicas. Todas as solicitações para APIs de plataforma exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção na Plataforma, consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

### Lendo chamadas de exemplo da API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md) de API de exemplo no guia de solução de problemas do Experience Platform.

## Próximas etapas

Depois de concluir as etapas descritas no documento acima, visite a documentação [Entrada e Saída](./input-output.md) . Este documento fornece uma breve visão geral dos tipos de dados usados e produzidos na IA do cliente.