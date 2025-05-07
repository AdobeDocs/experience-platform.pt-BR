---
title: Extensão da API de conversões de Reddit
description: Saiba como usar a extensão de API de conversões de anúncios Reddit para enviar eventos de interação do usuário para anúncios Reddit para publicidade direcionada.
last-substantial-update: 2025-05-1
source-git-commit: 603cc86892f518852552eaa2fe1bdeaa296137cf
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 1%

---

# Visão geral da extensão de API de conversões [!DNL Reddit]

O Reddit é uma plataforma de mídia social com uma base de usuários diversificada, tornando-a ideal para anunciantes que direcionam públicos específicos.

Use a [[!DNL Reddit] Extensão da API de conversões](https://ads-api.reddit.com/docs/v2/#tag/Conversions-API) para enviar os eventos de interação do usuário capturados no Adobe Experience Platform Edge Network para [!DNL Reddit Ads]. Use essa extensão para ajudar sua marca a alcançar um público de mais de 379 milhões de usuários ativos semanalmente, e entender melhor o comportamento do usuário e executar anúncios direcionados.

Leia este guia para saber como instalar, configurar e usar a extensão de API de Conversões do [!DNL Reddit] nas [regras](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/rules) do encaminhamento de eventos.

## Principais benefícios {#benefits}

Use a extensão da API de conversões de Reddit para:

- **Alcance seu público-alvo**: participe de mais de 379 milhões de usuários ativos semanalmente no [!DNL Reddit].
- **Analisar o comportamento do usuário**: use os dados de interação do usuário para entender o comportamento e otimizar as campanhas.
- **Entregar anúncios direcionados**: execute anúncios personalizados com base em interações de usuário capturadas no Adobe Experience Platform.

## Pré-requisitos {#prerequisites}

É necessário ter uma conta válida do Reddit Ads para usar esta extensão. Vá para a [[!DNL Reddit Ads] página de registro](https://business.reddithelp.com/s/article/Create-and-manage-your-Reddit-Ads-account) para se registrar e criar uma conta, caso ainda não tenha uma. Depois de configurar sua conta, [solicite acesso à API de anúncios](https://www.redditforbusiness.com/api-partnership).

### Coletar detalhes de configuração necessários {#configuration-details}

Para conectar o Experience Platform a [!DNL Reddit], as seguintes entradas são necessárias:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| ID de pixel | A Identificação de Pixel é um identificador exclusivo associado à sua conta [!DNL Reddit Ads]. Ele é usado para rastrear interações de usuários e eventos de conversão no seu site ou aplicativo. Você pode encontrar seu ID do Pixel em sua [!DNL Reddit Ads] [conta](https://ads.reddit.com/accounts). | 123456789012 |
| Token de acesso de conversão | Seu Token De Acesso De Conversão Do [!DNL Reddit]. Consulte o documento [[!DNL Reddit] API de conversões](https://business.reddithelp.com/s/article/conversion-access-token) para obter orientação. <br> **Você só precisa passar por esse processo uma vez que esse token não expira.** | {YOUR_REDDIT_BEARER_TOKEN} |

## Instalar e configurar a extensão [!DNL Reddit] {#install-configure}

Siga estas etapas para instalar e configurar a extensão de API de Conversões do [!DNL Reddit]:

1. Na interface da Coleção de dados do Experience Platform, selecione [!UICONTROL Extensões] na navegação à esquerda para acessar o catálogo [!UICONTROL Extensões]. Em seguida, [Crie uma nova propriedade de encaminhamento de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/overview#properties) ou selecione uma propriedade existente.
2. Navegue até **[!UICONTROL Extensões]** no painel de navegação esquerdo. Selecione **[!UICONTROL Catálogo]** e a extensão **[!DNL Reddit]**.
   ![O catálogo de Extensões do Adobe Experience Platform com a extensão Reddit está realçado.](../../../images/extensions/server/reddit/reddit-extension.png)
3. Forneça os seguintes detalhes de configuração:
   - **ID do Pixel**: insira seu [!DNL Reddit Ads] ID do Pixel.
   - **Token de acesso de conversão**: insira o token gerado na sua conta [!DNL Reddit Ads] e selecione **[!UICONTROL Salvar]** quando terminar.
     ![Detalhes de configuração da extensão de API de Conversões de Reddit, incluindo campos para ID de Pixel e Token de Acesso de Conversão.](../../../images/extensions/server/reddit/reddit-capi-details.png)

## Configurar uma regra de encaminhamento de eventos {#config-rule}

Após configurar seus elementos de dados, crie regras de encaminhamento de eventos para determinar quando e como os eventos são enviados para [!DNL Reddit Ads].

1. Navegue até **Regras** na propriedade de encaminhamento de eventos e crie uma nova [regra](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/rules).
2. Em **Ações**, adicione uma nova ação e defina a extensão como **[!DNL Reddit CAPI]**.
3. Defina o **Tipo de Ação** como **Enviar Evento**.
   ![Interface de configuração da regra de encaminhamento de eventos para a extensão de API de Conversões Reddit, com os campos de extensão e tipo de ação realçados.](../../../images/extensions/server/reddit/reddit-rule.png)
4. Configure os controles adicionais para seu evento conforme mostrado na tabela abaixo:

   | Nome do campo | Descrição | Exemplo |
   | --- | --- | --- |
   | `Event Name` | Especifique o nome do evento de conversão. | `Purchase` |
   | `Event Type` | Defina o tipo de evento que pode ser um [evento de conversão de Reddit suportado](https://business.reddithelp.com/s/article/supported-conversion-events#supported-conversion-events) ou um personalizado. | `SignUp`, `MyCustomEvent` |
   | `Timestamp` | Forneça a hora do evento em formato ISO ou época. | `2025-04-15T16:01:00.000Z`, `1744742460000` |
   | `Client Dedupe ID` | Adicione uma ID exclusiva para desduplicação. | `abc123` |
   | `Match Keys` | Incluir identificadores de usuário e dispositivo para atribuição. | `{"email":"hashed_email@example.com", "phone":"hashed_phone"}` |
   | `Value` | Especifique o valor monetário do evento. | `99.99` |
   | `Currency Code` | Use o formato ISO-4217 para a moeda. | `USD` |
   | `Units Sold` | Insira a quantidade de itens comprados. | `3` |
   | `Country Code` | Especifique o país onde o evento ocorreu. | `US` |
   | `Data Processing Options` | Adicione sinalizadores de privacidade, como LDU (Limited Data Usage, Uso limitado de dados). | `{"modes":["LDU"],"country":"US","region":"US-NY"}` |
   | `Consent` | Indique o consentimento do usuário para o uso de dados de publicidade. | `true` |

5. Selecione **Manter alterações** para salvar a regra.

## Metadados do evento {#event-metadata}

Leia esta seção para obter um detalhamento dos metadados do evento e dos campos de dados do usuário, garantindo a compreensão dos parâmetros obrigatórios e opcionais para configurar seus eventos. Os campos exibidos podem variar dependendo do tipo de evento selecionado.

>[!NOTE]
>
>Para obter os melhores resultados de seus eventos de conversão, preencha todos os campos ao configurar os [anúncios de produto dinâmicos](https://business.reddithelp.com/s/article/dynamic-product-ads).

### Campos de metadados do evento

![Detalhes de configuração da extensão de API de Conversões de Reddit, incluindo campos para ID de Pixel e Token de Acesso de Conversão.](../../../images/extensions/server/reddit/reddit-event-metadata.png)

| Nome do campo | Descrição | Exemplo |
| --- | --- | --- |
| `Conversion ID` (obrigatório) | A ID exclusiva do evento de conversão, usada para desduplicação. | `abc123` |
| `Item Count` | O número total de itens para o evento de conversão. | `6` |
| `Currency` | A moeda do valor é fornecida, no formato [ISO-4217](https://www.iso.org/iso-4217-currency-codes.html). | `USD` |
| `Value` | O valor monetário total do evento de conversão, incluindo decimais. | `1.23` |
| `Products` | Uma matriz JSON de objetos com detalhes sobre os produtos associados ao evento. Cada objeto deve incluir um `id` no mínimo. | `[{"id":"SKU123","name":"ProductName","category":"CategoryName"},{"id":"SKU456","name":"ProductName","category":"CategoryName"}]` |

### Campos de dados do usuário

Os seguintes parâmetros são opcionais, mas recomendados:

| Nome do campo | Descrição | Exemplo |
| --- | --- | --- |
| `Email` (altamente recomendado) | Um email de usuário com hash ou sem hash. | `example@email.com` |
| `External ID` | Uma ID de usuário atribuída pelo anunciante com hash ou sem hash. | `customer12345` |
| `UUID` (altamente recomendado) | A ID gerada pelo Pixel do Reddit em seu site. | `1677712978045.b8f7eb7d-b357-437b-8bd3-e1c8166c7132` |
| `IP Address` (altamente recomendado) | O endereço IP do dispositivo do usuário. | `192.168.0.1` |
| `User Agent` (altamente recomendado) | O navegador ou aplicativo usado pelo usuário. | `Chrome/98.0.4758.102` |
| `IDFA` | Um identificador Apple com hash ou sem hash para anunciantes. | `8A2E4F6D-0852-4B2A-B9D5-79334DE14B16` |
| `AAID` | Uma Android Advertising ID com hash ou com hash. | `38400000-8cf0-11bd-b23e-10b96e40000d` |
| `Screen Width` | A largura da exibição do usuário. | `1920` |
| `Screen Height` | A altura da exibição do usuário. | `1080` |
| `Data Processing Options` (formato JSON) | As configurações de privacidade do usuário. Suporta apenas LDU (Limited Data Usage, Uso limitado de dados). | `{"modes":["LDU"],"country":"US","region":"US-NY"}` |

### Considerações importantes

Antes de enviar dados para [!DNL Reddit Ads], a extensão hash e normaliza os valores dos seguintes campos: `Email`, `External ID`, `IDFA` e `AAID`. A extensão não refaz o hash desses valores se eles já tiverem sido hash em [!DNL SHA-256].

## Validar e implantar {#validate-deploy}

Após configurar a extensão e as regras, valide a integração verificando os dados do evento no [[!DNL Reddit Ads] Gerenciador de Eventos](https://business.reddithelp.com/s/article/Events-Manager). Use a [Pontuação de qualidade de correspondência (MQS)](https://business.reddithelp.com/s/article/match-quality-score) para avaliar a precisão e a confiabilidade de suas integrações de sinal.

Para obter detalhes adicionais sobre [!DNL Reddit Ads], visite a [documentação dos anúncios Reddit](https://ads.reddit.com/).

## Próximas etapas {#next-steps}

Depois de ler este documento, você deverá entender como configurar e usar a extensão de API de Conversões do [!DNL Reddit]. Para obter mais informações sobre os recursos de encaminhamento de eventos do Adobe Experience Platform, consulte a [visão geral do encaminhamento de eventos](../../../ui/event-forwarding/overview.md) ou os seguintes recursos:

- [Compartilhar chaves de correspondência](https://business.reddithelp.com/s/article/about-attribution-matching-signals) e [metadados de eventos](https://business.reddithelp.com/s/article/about-event-metadata): entenda como compartilhar chaves de correspondência e metadados de eventos de maneira eficiente.
- [Desduplicar eventos](https://business.reddithelp.com/s/article/event-deduplication): garanta um rastreamento de eventos preciso ao desduplicar eventos.
- [Criar um token de acesso de conversão](https://business.reddithelp.com/helpcenter/s/article/conversion-access-token): siga as etapas para criar um token de acesso de conversão para autenticação de API segura.
