---
title: Visão Geral Do Salesforce Marketing Cloud (V2) Source
description: Saiba como conectar o Salesforce Marketing Cloud (V2) ao Adobe Experience Platform usando APIs ou a interface do usuário.
source-git-commit: 3c200ff1a29c3462a5d4fef554f6a410cfcbdde8
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 0%

---

# Visão geral da origem de [!DNL Salesforce Marketing Cloud] (V2)

>[!IMPORTANT]
>
>A origem [[!DNL Salesforce Marketing Cloud] (V1)](salesforce-marketing-cloud.md) original foi descontinuada em janeiro de 2026. Não há migrações disponíveis para esta fonte obsoleta e você deve reimplementar seus dados usando a nova fonte [!DNL Salesforce Marketing Cloud] (V2).

A integração entre o Adobe [Real-Time CDP](../../../rtcdp/overview.md) e o [!DNL Salesforce Marketing Cloud] foi projetada para aproveitar as Extensões de Dados devido à flexibilidade e ao controle que elas oferecem. Diferentemente das Tabelas de sistema padrão (Visualizações de dados e Objetos integrados), que são limitadas a campos predefinidos e servem principalmente ao rastreamento no nível do sistema, você pode usar Extensões de dados para definir campos personalizados, organizar uma grande variedade de dados específicos de negócios e adaptar suas estruturas de dados para atender a requisitos exclusivos.

Devido a esse nível de personalização e escalabilidade, a integração entre o Real-Time CDP e o [!DNL Salesforce Marketing Cloud] depende de Extensões de Dados em vez de Tabelas de Sistema Padrão. Essa abordagem oferece uma base mais flexível, escalável e integrada para gerenciar dados, garantindo que se alinhe às suas metas de negócios

Você pode usar a origem [!DNL Salesforce Marketing Cloud] para conectar sua conta do [!DNL Salesforce Marketing Cloud] à Real-Time CDP e à Adobe Experience Platform. Leia a documentação abaixo para saber como começar.

## Exemplos de caso de uso {#use-case-examples}

### Personalizar campanhas de email com dados de contato

Uma marca de varejo deseja personalizar campanhas de email com base nos estágios do ciclo de vida do cliente (por exemplo, novo cliente, comprador recorrente, cliente fiel). Para fazer isso, eles criam uma Extensão de dados de contato para armazenar as principais informações do cliente, incluindo nome, email, estágio do ciclo de vida e comportamento de compra. Esses dados são assimilados no Experience Platform para segmentação e direcionamento mais profundos.

Ao assimilar os dados da Extensão de dados de contato na Experience Platform, a marca pode segmentar os clientes com base no estágio do ciclo de vida e no comportamento de compra. Por exemplo, eles podem enviar uma oferta de boas-vindas para novos clientes, uma recompensa de fidelidade para compradores recorrentes ou até mesmo reengajar clientes inativos com ofertas direcionadas. Essa abordagem garante uma comunicação personalizada e permite um engajamento do cliente mais relevante e eficaz.

### Assimilar dados do Campaign para segmentação personalizada

Uma equipe de marketing deseja otimizar suas campanhas de email direcionando os clientes com base no engajamento com campanhas anteriores. Para fazer isso, eles criam uma Extensão de Dados do Campaign no [!DNL Salesforce Marketing Cloud] para armazenar dados de participação do cliente, como aberturas de email, cliques e respostas da campanha. Esses dados são assimilados no Experience Platform para segmentação e personalização adicionais.

Ao assimilar esses dados da Extensão de dados do Campaign no Experience Platform, a equipe de marketing pode segmentar os clientes com base no engajamento anterior, como aqueles que clicaram nas ofertas do produto ou responderam positivamente. Os clientes que se envolveram podem receber promoções direcionadas em emails futuros, enquanto aqueles que responderam negativamente podem receber acompanhamento do atendimento ao cliente. Essa integração com o Experience Platform garante que a equipe de marketing possa fornecer conteúdo mais personalizado e relevante com base no comportamento do cliente.

### Direcionamento de dados de clientes com base em atividades

Uma equipe de marketing deseja direcionar os clientes com base em suas atividades, como visitas a sites, envios de formulários ou interações com campanhas de email anteriores. Para isso, eles criam uma Extensão de dados de atividades para armazenar informações sobre as atividades de engajamento de cada cliente. Esses dados são assimilados no Experience Platform para segmentação adicional e direcionamento personalizado de campanha.

Ao assimilar os dados da Extensão de dados de atividades no Experience Platform, a equipe de marketing pode segmentar os clientes com base em seu histórico de engajamento. Por exemplo, os clientes que visitaram o site recentemente, mas não concluíram uma compra, podem receber emails de lembrete com ofertas especiais. Da mesma forma, os clientes que preencheram um formulário podem receber comunicações de acompanhamento personalizadas. Essa abordagem garante que cada cliente receba conteúdo relevante com base em suas atividades mais recentes, melhorando as taxas de engajamento e conversão.

## Pré-requisitos {#prerequisites}

Leia as seções abaixo para obter a configuração de pré-requisitos que você deve concluir antes de poder conectar sua origem ao Experience Platform.

### Configurar aplicativo para autenticação {#set-up-application-for-authentication}

Ao criar uma integração com [!DNL Salesforce Marketing Cloud], uma das primeiras etapas é criar um **Pacote Instalado** em [!DNL Salesforce Marketing Cloud]. O pacote instalado gera as credenciais do cliente necessárias para autenticar chamadas de API, define o tipo de integração e os escopos de permissão associados. Além disso, o pacote instalado fornece os endpoints de API corretos para o locatário. Ele também serve como um contêiner gerenciado para administrar, monitorar e revogar o acesso, garantindo que todas as integrações sejam seguras, auditáveis e alinhadas com o modelo de autenticação recomendado pela Salesforce.

Para criar um pacote instalado, use a interface do usuário do [!DNL Salesforce Marketing Cloud] e navegue até **[!DNL Setup]** > **[!DNL Apps]** > **[!DNL Installed Packages]** e selecione **[!DNL New]**. Use a interface [!DNL New Package Details] para fornecer um nome e informações para o pacote. Quando terminar, selecione **[!DNL Save]**.

![A nova interface de pacote da interface do Salesforce Marketing Cloud.](../../images/tutorials/create/sfmc/new-package.png)

Após criar o novo pacote, selecione **[!DNL Add Component]**.

![A interface Adicionar Componente da Interface do Usuário do Salesforce Marketing Cloud.](../../images/tutorials/create/sfmc/add-component.png)

Selecione **[!DNL API Integration]** como seu tipo de componente.

![A janela de seleção de componentes com a opção &quot;Integração de API&quot; selecionada.](../../images/tutorials/create/sfmc/api-integration.png)

Selecione **[!DNL Server-to-Server]** como seu tipo de integração.

![A janela de seleção do tipo de integração](../../images/tutorials/create/sfmc/server-to-server.png)

Finalmente, navegue até **[!DNL Scope]** > **[!DNL Data]**. Em **[!DNL Data Extensions]**, selecione **[!DNL Read]**.

![A seção de extensões de dados do Escopo no Salesforce Marketing](../../images/tutorials/create/sfmc/data-extensions.png)

Selecione **[!DNL Save]** e copie e salve o **segredo do cliente**. Quando terminar, selecione **[!DNL Finish]**.

![A janela do Salesforce Marketing Cloud para gerar um segredo de cliente.](../../images/tutorials/create/sfmc/generate-secret.png)

Antes de sair da interface do usuário do [!DNL Salesforce Marketing Cloud], copie a **ID do cliente** e o **prefixo do URI de base exclusivo**, pois você usará ambos os valores para criar uma conexão com o Experience Platform. Para o URI da Base de Autenticação, remova tudo depois de `.auth.marketingcloudapis.com/`

![A interface dos componentes do Salesforce Marketing Cloud na qual a ID do cliente e o URI de base exclusiva podem ser recuperados.](../../images/tutorials/create/sfmc/client-id-and-uri.png)

Para obter etapas detalhadas sobre como criar um pacote instalado, leia a [[!DNL Salesforce] documentação](https://trailhead.salesforce.com/content/learn/modules/marketing-cloud-developer-basics/set-up-your-developer-environment).

### Coletar credenciais necessárias {#gather-required-credentials}

Você deve fornecer valores para as credenciais a seguir para conectar [!DNL Salesforce Marketing Cloud] ao Experience Platform.

| Credencial | Descrição |
| --- | --- |
| ID de cliente | O identificador exposto publicamente usado por [!DNL Salesforce Marketing Cloud] para identificar sua conta ao autorizar a Experience Platform. A ID do cliente pode ser recuperada do painel Componentes da interface do usuário do [!DNL Salesforce Marketing Cloud]. |
| Segredo do cliente | A chave confidencial conhecida apenas pelo aplicativo cliente e pelo servidor de autorização. Você pode gerar o segredo do cliente seguindo as etapas de configuração do aplicativo [ descritas acima](#set-up-application-for-authentication). |
| Endpoint base | O prefixo do URI da base de autenticação para [!DNL Salesforce Marketing Cloud]. |

{style="table-layout:auto"}

## Conectar [!DNL Salesforce Marketing Cloud] ao Experience Platform

Continue a configurar sua conexão de origem do [!DNL Salesforce Marketing Cloud] no Experience Platform. Para obter um guia passo a passo sobre como configurar a conexão através da interface do usuário, consulte o [tutorial aqui](../../tutorials/ui/create/marketing-automation/sfmc.md). Leia este tutorial para saber mais sobre como conectar sua conta do [!DNL Salesforce Marketing Cloud], selecionar dados, mapear campos, agendar assimilações e monitorar seus fluxos de dados.
