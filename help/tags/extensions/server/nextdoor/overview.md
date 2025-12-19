---
title: Extensão de API de conversão do Nextdoor
description: Saiba como usar a extensão Nextdoor Conversion API para enviar eventos de conversão para rastrear o desempenho de suas campanhas publicitárias.
last-substantial-update: 2025-12-18T00:00:00Z
source-git-commit: 56c69696300dd9de8c0e98ecc71cafc7328f1620
workflow-type: tm+mt
source-wordcount: '1772'
ht-degree: 8%

---


# Extensão de API de conversão do [!DNL Nextdoor] - Guia do usuário

## Visão geral

[!DNL Nextdoor] é um serviço de rede social para bairros que conecta as pessoas às suas comunidades locais. É uma plataforma onde os vizinhos podem se comunicar, compartilhar informações, manter-se atualizados sobre eventos e notícias locais, e comprar e vender itens com outras pessoas em sua área.

Use a [[!DNL Nextdoor] Extensão da API de conversão](https://help.nextdoor.com/s/article/About-the-Nextdoor-Conversion-API) para enviar eventos de conversão diretamente para a API de conversão [!DNL Nextdoor's]. Esta extensão ajuda a rastrear e medir o desempenho de suas campanhas de publicidade do [!DNL Nextdoor] enviando dados de conversão do lado do servidor.

Este guia mostra como instalar, configurar e usar a extensão de API de Conversão [!DNL Nextdoor] nas [regras](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/rules) do encaminhamento de eventos.

## Pré-requisitos {#prerequisites}

Você precisa de uma conta válida do Ads Manager do [!DNL Nextdoor] para usar esta extensão. Se você ainda não tiver uma, vá para a [[!DNL Nextdoor Ads] página de registro](https://ads.nextdoor.com/v2/signup) para registrar e criar sua conta.

### Coletar detalhes de configuração necessários {#configuration-details}

Para conectar o Experience Platform ao [!DNL Nextdoor], você precisará das seguintes informações:

| Credencial | Descrição | Notas de segurança |
| --- | --- | --- |
| ID do Source de dados | Seu identificador de fonte de dados exclusivo do [!DNL Nextdoor], que você pode encontrar na conta do [!DNL Nextdoor Ads Manager] acessando a página Assets > Pixels e gerando um Pixel do lado direito. | É seguro compartilhá-lo em sua organização. |
| Token de acesso | Seu token de acesso de autenticação de API para comunicação segura. Você pode gerar esse token fazendo logon na conta do [!DNL Nextdoor Ads Manager] e acessando as configurações da API. | Mantenha esse token protegido, pois ele fornece acesso à sua conta. |

## Instalar e configurar a extensão [!DNL Nextdoor] {#install}

Para instalar a extensão, selecione **[!UICONTROL Extensions]** na navegação à esquerda. Na guia **[!UICONTROL Catalog]**, selecione o **[!UICONTROL Nextdoor Conversion API Extension]** e selecione **[!UICONTROL Install]**.

![O catálogo de extensões que mostra a instalação do destaque do cartão de extensão [!DNL Nextdoor].](../../../images/extensions/server/nextdoor/install-extension.png)

Na próxima tela, insira os valores de configuração gerados com base em seu [!DNL Nextdoor Ads Manager]:

* **[!UICONTROL Data Source ID]**
* **[!UICONTROL Access Token]**

Quando terminar, selecione **[!UICONTROL Save]**.

Tela de configuração ![[!DNL Nextdoor] para a extensão de API de conversão [!DNL Nextdoor].](../../../images/extensions/server/nextdoor/configure.png)

## Configurar uma regra de encaminhamento de eventos {#config-rule}

Depois que todos os seus elementos de dados forem configurados, você poderá criar regras de encaminhamento de eventos que determinam quando e como seus eventos são enviados para [!DNL Nextdoor].

Crie uma nova [regra](../../../ui/managing-resources/rules.md) na propriedade de encaminhamento de eventos. Em **[!UICONTROL Actions]**, adicione uma nova ação e defina a extensão como **[!UICONTROL Nextdoor Conversion API Extension]**. Para enviar eventos do Edge Network para [!DNL Nextdoor], defina **[!UICONTROL Action Type]** como **[!UICONTROL Report Web Conversions]**.

![O tipo de ação [!UICONTROL Report Web Conversions] que está sendo selecionado para uma regra [!DNL Nextdoor] na interface da Coleção de Dados.](../../../images/extensions/server/nextdoor/select-action.png)

Depois de fazer essa seleção, são exibidos controles adicionais que permitem configurar o evento ainda mais, conforme descrito abaixo. Depois de concluído, selecione **[!UICONTROL Keep Changes]** para salvar a regra.

**Parâmetros do corpo principal**

Esses parâmetros principais definem o evento de conversão:

| Parâmetro | Descrição | Tipo de dados | Obrigatório | Opções/Formato | Exemplo |
| ------------------------------------ | -------------- | -------------- | -------------- | -------------- | -------------- |
| [!UICONTROL Event Name] | Especifica o tipo de evento de conversão que está sendo rastreado. | String (lista suspensa) | Obrigatório | <ul><li>Comprar</li><li>Lead</li><li>Inscrever-se</li><li>Adicionar ao carrinho</li><li>Iniciar check-out</li><li>Exibição da página</li><li>Pesquisa</li><li>Exibir conteúdo</li><li>Adicionar à lista de desejos</li><li>Inscreva-se</li><li>Personalizado</li></li>Conversão 1-10</li></ul> | `Purchase` |
| [!UICONTROL Event ID] | Identificador exclusivo para evitar relatórios de eventos duplicados. Ele será gerado automaticamente se estiver em branco. | String | Opcional | Identificador exclusivo da sequência de caracteres | `order_12345` |
| [!UICONTROL Event Time (Unix Epoch)] | Carimbo de data e hora quando o evento de conversão ocorreu. O padrão é a hora atual, se deixado em branco. | Número inteiro | Opcional | Carimbo de data e hora Unix em segundos | `1703980800` (30 de dezembro de 2023) |
| [!UICONTROL Action Source] | Canal ou plataforma em que a conversão ocorreu. | String (lista suspensa) | Obrigatório | <ul><li>site</li><li>email</li><li>aplicativo</li><li>phone_call</li><li>bate-papo</li><li>physical_store</li><li>system_generated</li><li>outro</li></ul> | `website` |
| [!UICONTROL Data Source ID] | Substitua a ID da fonte de dados global por eventos específicos. Herdará da configuração se deixado em branco. | String | Opcional | Sequência alfanumérica | `12345` |
| [!UICONTROL Action Source URL] | O URL específico onde ocorreu a conversão. | String | Opcional | URL completo, incluindo protocolo | https://example.com/checkout/success |

**Parâmetros de privacidade e conformidade**

Use estes parâmetros para garantir a conformidade com a privacidade:

| Parâmetro | Descrição | Tipo de dados | Obrigatório | Valores/Formato | Exemplo |
| -------------------------------------------- | ---------------------------------------------------  | --------- | -------- | ---------------------------------------------------------- | ---------- |
| [!UICONTROL Restricted Data Usage] | Sinalizador para restringir o uso de dados para conformidade com a privacidade. | Número inteiro | Opcional | <ul><li>0 = Sem restrições</li><li>1 = Restrito</li></ul> | `0` |
| [!UICONTROL Restricted Data Usage (Country)] | Restrições de processamento de dados específicas do país. | Número inteiro | Opcional | 1 = EUA (outros códigos podem ser suportados) | `1` |
| [!UICONTROL Restricted Data Usage (State)] | Restrições específicas de estado para usuários dos EUA. | Número inteiro | Opcional | 1000 = CA, 1001 = CO, etc. | `1000` |
| [!UICONTROL Test Event] | Marca o evento como um teste para desenvolvimento/depuração. | String | Opcional | Qualquer sequência de caracteres não vazia | `test` |

**Parâmetros de informações do cliente**

>[!IMPORTANT]
>
>Você deve fornecer pelo menos um parâmetro de informações do cliente para atribuição e correspondência apropriadas do evento.

| Parâmetro | Descrição | Tipo de dados | Obrigatório | Formato | Exemplo |
| ------------------------------ | ----------------------------------------------- | --------- | ------------------------------------ | ------------------------------------ | -------------------------- |
| [!UICONTROL Email] | Endereço de email do cliente para correspondência de identidade. | String | É necessário pelo menos um campo de cliente | Texto sem formatação ou hash SHA-256 | `user@example.com` |
| [!UICONTROL Phone Number] | Número de telefone do cliente para correspondência de identidade. | String | É necessário pelo menos um campo de cliente | Formato E.164 (com hash SHA-256) | `+15551234567` |
| [!UICONTROL First Name] | Nome do cliente para correspondência aprimorada. | String | É necessário pelo menos um campo de cliente | Texto sem formatação ou hash SHA-256 | `John` |
| [!UICONTROL Last Name] | Sobrenome do cliente para correspondência aprimorada. | String | É necessário pelo menos um campo de cliente | Texto sem formatação ou hash SHA-256 | `Smith` |
| [!UICONTROL Date of Birth] | Data de nascimento do cliente para correspondência demográfica. | String | Opcional | AAAAMMDD (SHA-256 com hash) | `19900115` |
| [!UICONTROL Gender] | Sexo do cliente para direcionamento demográfico. | String | Opcional | M/F/O (SHA-256 com hash) | `M` |
| [!UICONTROL External ID] | O identificador interno do cliente. | String | Opcional | Qualquer sequência exclusiva | `customer_12345` |
| [!UICONTROL Street Address] | Endereço do cliente. | String | Opcional | SHA-256 com hash | `123 Main Street` (com hash) |
| [!UICONTROL City] | Cidade do cliente. | String | Opcional | SHA-256 com hash | `San Francisco` (com hash) |
| [!UICONTROL State] | Estado/província do cliente. | String | Opcional | Código de duas letras (SHA-256 com hash) | `CA` (com hash) |
| [!UICONTROL Zip Code] | CEP do cliente. | String | Opcional | Primeiros 5 dígitos EUA (SHA-256 com hash) | `94102` (com hash) |
| [!UICONTROL Country] | País do cliente. | String | Opcional | ISO-3166-1 alpha-2 (SHA-256 com hash) | `US` (com hash) |
| [!UICONTROL Click ID] | Identificador de clique ao lado para atribuição. | String | Opcional | Capturado do parâmetro de URL `ndclid` | `nd_click_12345abcdef` |
| [!UICONTROL Client IP Address] | Endereço IP do dispositivo do usuário. | String | Opcional | Endereço IPv4 ou IPv6 | `192.168.1.1` |
| [!UICONTROL Client User Agent] | Sequência de agente do usuário do navegador. | String | Opcional | String bruta do agente do usuário do navegador | `Mozilla/5.0 (Windows...)` |

**Parâmetros personalizados**

Esses parâmetros fornecem contexto adicional sobre o evento de conversão:

| Parâmetro | Descrição | Tipo de dados | Obrigatório | Formato | Exemplo |
| ------------------------------ | ---------------------------------------------- | ------------------- | -------------------------------- | --------------------------------------- | ----------------------- |
| [!UICONTROL Order Value] | Valor total da transação de compra. | String | **OBRIGATÓRIO para eventos de compra** | Moeda ISO 4217 + Valor (sem espaços) | `USD123.45` |
| [!UICONTROL Order ID] | Identificador exclusivo da transação ou do pedido. | String | Opcional | Qualquer sequência exclusiva | `order_12345` |
| [!UICONTROL Delivery Category] | Método de entrega de produto/serviço. | String | Opcional | <ul><li>`in_store`</li><li>`curbside`</li><li>`home_delivery`</li></ul> | `home_delivery` |
| [!UICONTROL Product Context] | Informações detalhadas sobre produtos comprados. | String (matriz JSON) | Opcional | Matriz JSON de objetos de produto | `[{"id":"SKU123","content_name":"Widget","item_price":29.99,"quantity":1}]` |

**Parâmetros do aplicativo móvel**

Você deve incluir estes parâmetros quando `Action Source = 'APP'`:

| Parâmetro | Descrição | Tipo de dados | Obrigatório | Formato | Exemplo |
| --------------------------------- | --------------------------------------------- | --------- | --------------------------- | ----------------------------------------- | ----------------- |
| [!UICONTROL App ID*] | Identificador do aplicativo móvel. | String | **OBRIGATÓRIO para eventos de APLICATIVO** | <ul><li>ID do pacote (iOS)</li><li>Nome do pacote (Android)</li></ul> | `com.company.app` |
| [!UICONTROL App Tracking Enabled] | Status de consentimento de Transparência do Rastreamento de aplicativo do iOS. | String | **OBRIGATÓRIO para eventos de APLICATIVO** | String booleana | `true` |
| [!UICONTROL Platform] | Sistema operacional móvel. | String | **OBRIGATÓRIO para eventos de APLICATIVO** | <ul><li>`iOS`</li><li>`Android`</li></ul> | `Android` |
| [!UICONTROL App Version] | Versão do aplicativo móvel. | String | **OBRIGATÓRIO para eventos de APLICATIVO** | Sequência de caracteres da versão conforme definido pelo aplicativo | `2.0.0-beta` |

## Tipos de evento {#event-types}

Os seguintes tipos de evento são compatíveis com diferentes cenários de conversão:

| Nome do evento | Tipo de evento | Descrição | Caso de uso | Campos obrigatórios | Notas |
| ------------------------ | ---------- | -------------------------------------- | --------------------------------------- | -------------------------------------- | ------------------------------------- |
| [!UICONTROL Purchase] | Standard | Transação de compra concluída. | Conversões de comércio eletrônico | <ul><li>Nome do evento</li><li>Valor do pedido</li><li>Informações do cliente</li></ul> | Mais importante para a otimização do ROAS |
| [!UICONTROL Lead] | Standard | Geração ou consulta de lead. | Envio de formulários, solicitações de contato | <ul><li>Nome do evento</li><li>Informações do cliente</li></ul> | Conversão de alto valor para B2B |
| [!UICONTROL Sign Up] | Standard | Registro de usuário ou criação de conta. | Inscrição no informativo, registro de conta | <ul><li>Nome do evento</li><li>Informações do cliente</li></ul> | Rastreamento de conversão Top-funnel |
| [!UICONTROL Add to Cart] | Standard | Produto adicionado ao carrinho de compras. | Rastreamento de funnel de comércio eletrônico | <ul><li>Nome do evento</li><li>Informações do cliente</li></ul> | Sinal de engajamento no mid-funnel |
| [!UICONTROL Initiate Checkout] | Standard | Processo de finalização iniciado. | Rastreamento da intenção de compra | <ul><li>Nome do evento</li><li>Informações do cliente</li></ul> | Indicador de intenção de compra forte |
| [!UICONTROL Page View] | Standard | Página importante visitada. | Engajamento de conteúdo, páginas de destino | <ul><li>Nome do evento</li><li>Informações do cliente</li></ul> | Usar somente para páginas de alto valor |
| [!UICONTROL Search] | Standard | Pesquisa realizada no site. | Descoberta de produto/conteúdo | <ul><li>Nome do evento</li><li>Informações do cliente</li></ul> | Indica o engajamento ativo do usuário |
| [!UICONTROL View Content] | Standard | Conteúdo ou produto exibido. | Exibições de página de produto, envolvimento de conteúdo | <ul><li>Nome do evento</li><li>Informações do cliente</li></ul> | Útil para públicos de remarketing |
| [!UICONTROL Add to Wishlist] | Standard | Produto adicionado à lista de desejos. | Tentativa de compra futura | <ul><li>Nome do evento</li><li>Informações do cliente</li></ul> | Indica forte interesse do produto |
| [!UICONTROL Subscribe] | Standard | Assinatura do serviço/informativo. | Receita recorrente, envolvimento | <ul><li>Nome do evento</li><li>Informações do cliente</li></ul> | Indicador de valor de vida útil alto |
| [!UICONTROL Custom Conversion 1 - 10] | Personalizado | Evento de conversão específico da empresa. | Definir seu próprio tipo de conversão | <ul><li>Nome do evento</li><li>Informações do cliente</li></ul> | Personalizar para ações comerciais exclusivas |

## Integração de elementos de dados {#data-element}

Todos os campos são compatíveis com elementos de dados do encaminhamento de eventos do Adobe. Selecione o ícone do elemento de dados ![elementos de dados](../../../images/extensions/server/nextdoor/data-element-icon.png) ao lado de qualquer campo para:

* **Selecionar Elementos de Dados Existentes**: selecione nos elementos de dados que já foram criados.
* **Adicionar novos elementos de dados**: crie e defina novos elementos de dados conforme necessário.
* **Aplicar valores dinâmicos**: preencha campos com conteúdo dinâmico proveniente do seu site.

## Práticas recomendadas {#best-practices}

Siga estas práticas recomendadas para garantir um rastreamento de conversão preciso, melhorar a qualidade dos dados e cumprir as regulamentações de privacidade. Essas recomendações ajudarão a maximizar a eficácia da integração da API de conversão do [!DNL Nextdoor] e a otimizar o desempenho da sua publicidade.

### Conformidade com a qualidade e a privacidade dos dados

O manuseio adequado de dados é essencial para maximizar a precisão da atribuição de conversão, mantendo a privacidade do usuário e a conformidade regulamentar. Essas práticas ajudam a garantir que os dados do cliente sejam formatados corretamente, processados de forma segura e tratados de acordo com as regulamentações de privacidade.

* **Usar formatação de dados consistente**: Formate emails, números de telefone e outros dados de forma consistente:

   * **Normalização de email**: converta emails em minúsculas, elimine espaços em branco e remova pontos de [!DNL Gmail] endereços.
   * **Padronização de número de telefone**: use o formato E.164 (+1234567890) para compatibilidade internacional.
   * **Normalização de endereço**: padronize as abreviações de rua (St., Ave., Rd.) e remova espaços extras.
   * **Formatação de nome**: converta nomes em minúsculas, remova espaços extras e manipule caracteres especiais consistentemente.

* **Dados sensíveis a hash**: considere hash de dados confidenciais do cliente antes de enviá-los. Sempre normalize seus dados antes do hash para garantir valores de hash consistentes:

   * Use hash SHA-256 para números de telefone, endereços e outros PII.
   * A extensão hash automaticamente emails de texto sem formatação - você pode enviar qualquer formato.
   * Use hash nos dados de forma consistente em todas as implementações de rastreamento.
      * **Exemplo**: Normalizar &quot;John@Example.COM&quot; → &quot;john@example.com&quot; antes do hash.

* **Forneça informações completas**: inclua o máximo possível de informações do cliente para uma melhor correspondência:

   * Inclua vários identificadores (email + telefone ou email + nome + endereço) quando disponível.
   * Use IDs externas do cliente para vincular eventos de conversão aos seus dados de CRM.
   * Fornecer dados demográficos (idade, sexo) quando disponíveis e em conformidade com as leis de privacidade.

* **Gerenciamento de consentimento**: verifique se você tem o consentimento adequado para a coleta de dados:

   * Implemente mecanismos de consentimento adequados antes de coletar dados do cliente.
   * Respeite as preferências de recusa do usuário e as solicitações de exclusão de dados.
   * Use os parâmetros de Uso restrito de dados para usuários que recusaram.
   * **Recursos**:
      * [Guia de Conformidade do GDPR](https://gdpr.eu/compliance/)
      * [Requisitos de privacidade da CCPA](https://oag.ca.gov/privacy/ccpa)

* **Minimização de Dados**: Enviar apenas os dados necessários para o rastreamento de conversão:

   * Colete e envie somente dados essenciais para atribuição e otimização.
   * Revise e faça auditorias regularmente nos campos de dados que você está enviando.
   * Remova informações desnecessárias do cliente para reduzir o risco de privacidade.

* **Usar carimbos de data/hora precisos**: verifique se os carimbos de data/hora do evento são precisos para atribuição adequada.
   * Use a hora real em que a conversão ocorreu, não quando você processou os dados.
   * Verifique se os carimbos de data e hora estão no formato de época Unix (segundos desde 1º de janeiro de 1970).
   * Conta para diferenças de fuso horário nos cálculos de carimbo de data e hora.

### Desduplicação de eventos

Evite eventos de conversão duplicados para garantir uma medição de campanha precisa e evitar métricas de desempenho infladas. Implemente a desduplicação adequada para que cada conversão seja contada apenas uma vez, fornecendo dados confiáveis para suas decisões de otimização.

* **Fornecer identificações de evento exclusivas**: sempre use identificações de evento exclusivas para evitar conversões duplicadas.
* **Usar nomenclatura consistente**: aplique a nomenclatura de evento consistente em sua implementação.

### Limite de taxa

A API de Conversão [!DNL Nextdoor] está sujeita à limitação de taxa. O limite de taxa atual é de **100 solicitações/minuto** por anunciante. Se você ultrapassar o limite de taxa, a API retornará um código de erro `HTTP 429 Too Many Requests`.

## Conclusão {#conclusion}

A Extensão da API de Conversão [!DNL Nextdoor] fornece uma maneira poderosa de rastrear conversões e medir a eficácia de suas campanhas publicitárias [!DNL Nextdoor]. Ao seguir este guia e implementar as práticas recomendadas, você poderá garantir um rastreamento preciso das conversões e otimizar o desempenho da sua publicidade.

Para obter as informações mais atualizadas e recursos adicionais, visite [[!DNL Nextdoor Ads Manager]](https://ads.nextdoor.com).

## Próximas etapas {#next-steps}

Este guia mostrou como enviar dados do evento do lado do servidor para o [!DNL Nextdoor] usando a extensão de API de conversão [!DNL Nextdoor]. Para saber mais sobre os recursos de encaminhamento de eventos do [!DNL Adobe Experience Platform], consulte a [visão geral do encaminhamento de eventos](../../../ui/event-forwarding/overview.md).
