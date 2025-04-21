---
title: Extensão da API de conversões do Adobe Amazon
description: Essa API de eventos da Web do Adobe Experience Platform permite compartilhar interações do site diretamente com o Amazon.
last-substantial-update: 2025-04-17T00:00:00Z
source-git-commit: 65a3eb20dc3de62319f73be49197dacb8fc1778b
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 1%

---

# Visão geral da extensão de API de eventos da Web do [!DNL Amazon]

A extensão de API de conversões [!DNL Amazon] cria uma conexão direta entre os dados de marketing do servidor de um anunciante e [!DNL Amazon]. Isso permite que os anunciantes avaliem a eficácia da campanha independentemente do local de conversão e otimizem as campanhas de acordo. A extensão fornece atribuição mais completa, maior confiabilidade dos dados e entrega mais otimizada.

## [!DNL Amazon] pré-requisitos {#prerequisites}

Antes de instalar e configurar a extensão de API de conversões do [!DNL Amazon], é necessário concluir várias etapas de pré-requisito para garantir a autenticação e o acesso aos dados adequados.

### Criar um segredo e um elemento de dados {#secret}

A autenticação com [!DNL Amazon] requer um token seguro que deve ser armazenado e referenciado corretamente:

1. Crie um novo segredo de encaminhamento de eventos [!DNL Amazon] com um nome exclusivo para autenticação.
2. Crie um elemento de dados usando a extensão **Core** com um tipo de elemento de dados **Secret** para fazer referência ao seu segredo [!DNL Amazon].

Esse processo garante que suas credenciais de autenticação permaneçam seguras enquanto ainda estejam acessíveis para a extensão quando necessário.

## Instalar e configurar a extensão [!DNL Amazon]

A instalação da extensão requer acesso à propriedade de encaminhamento de eventos no Experience Platform:

- Crie ou edite uma propriedade de encaminhamento de eventos.
- Selecione **Extensões** na navegação à esquerda e, em seguida, selecione a extensão [!DNL Amazon] na guia Catálogo.
- Selecione **Instalar**.

![[!DNL Amazon] extensão selecionada no catálogo de extensões junto com o botão de instalação.](../../../images/extensions/server/amazon/amazon-extension.png)

- Configurar o com:

- **Token de acesso**: seu segredo do elemento de dados que contém o token OAuth 2

![Configurações individuais para inserir o segredo do elemento de dados destacado.](../../../images/extensions/server/amazon/2.png)

- **Id de entidade**: sua Id de entidade (encontrada na URL do portal do Campaign Manager com o prefixo &quot;entity&quot;)

![O portal do gerenciador de campanhas na navegação à esquerda.](../../../images/extensions/server/amazon/3.png)

- Selecione **Salvar**.

Esses valores de configuração estabelecem a conexão entre a Platform e sua conta do [!DNL Amazon].

### [!DNL Amazon] OAuth 2 {#oauth}

Para criar um segredo OAuth 2 do [!DNL Amazon]:

- Selecione [!DNL Amazon] OAuth 2 na lista suspensa **Tipo** e selecione **Criar Segredo**.

![Amazon OAuth 2 no menu suspenso.](../../../images/extensions/server/amazon/Oauth.png)

- Selecione **Criar e autorizar segredo com o Amazon** no popover para autorizar manualmente o segredo e continuar.

![Criar e autorizar segredo com o Amazon selecionado.](../../../images/extensions/server/amazon/Oauth.1.png)

- Insira suas credenciais do [!DNL Amazon] na caixa de diálogo exibida. Siga as instruções para conceder acesso ao encaminhamento de eventos para seus dados.

Após a conclusão, você verá seu segredo com seu status e data de expiração na guia **Segredos**.

![Segredo criado na guia de segredos.](../../../images/extensions/server/amazon/Oauth.2.png)

## Configurar uma regra de encaminhamento de eventos {#config-rule}

Depois que todos os elementos de dados forem configurados, você poderá criar regras de encaminhamento de eventos que determinam quando e como seus eventos serão enviados para a Amazon.

- Navegue até **Regras** e crie uma nova regra de encaminhamento de eventos.
- Em **Ações**, selecione **Extensão da API de Conversões do Amazon**.
- Defina o **Tipo de ação** como **Importar eventos de conversão**.

![Opções de configuração de ação realçadas.](../../../images/extensions/server/amazon/4.png)

- Configure as propriedades do evento conforme descrito abaixo:

| Entrada | Descrição |
| --- | --- |
| **Nome do Evento** | O nome do evento de conversão. |
| **Tipo de evento** | Define o tipo de evento rastreado (por exemplo, compras, adições ao carrinho). |
| **Carimbo de data/hora** | Hora do evento em formato ISO. |
| **ID de Eliminação de Duplicação de Cliente** | Uma ID exclusiva para desduplicação. |
| **Chaves de correspondência** | Identificadores de usuário e dispositivo para atribuição. |
| **Valor** | Valor monetário do evento. |
| **Código de moeda** | Moeda no formato ISO-4217. |
| **Unidades Vendidas** | Quantidade de itens comprados. |
| **Código do país** | País onde o evento ocorreu. |
| **Opções de Processamento de Dados** | Sinalizadores para uso limitado de dados. |
| **Consentimento** | Indica o consentimento do usuário para o uso de dados de publicidade. |

- Selecione **Manter alterações** para salvar a regra.

![Parâmetros de evento na configuração de ação destacados junto com o botão manter alterações.](../../../images/extensions/server/amazon/5.png)

![Parâmetros de evento adicionais na configuração de ação destacados junto com o botão manter alterações.](../../../images/extensions/server/amazon/6.png)

## Desduplicação de eventos {#deduplication}

Se você usar a AAT (Advertising Tag) [!DNL Amazon] e a extensão de API de conversões [!DNL Amazon] para os mesmos eventos, será necessária a configuração da desduplicação. Inclua `clientDedupeId` em cada evento compartilhado para garantir a desduplicação adequada.
A desduplicação não é necessária se os eventos do cliente e do servidor não se sobrepuserem.

A desduplicação adequada impede contagens de conversão infladas e garante que seus dados de otimização permaneçam precisos.

Consulte o [Guia de Eliminação de Duplicação de Eventos da Amazon](https://advertising.amazon.com/) para obter mais detalhes.

## Próximas etapas

Este guia aborda como configurar e enviar eventos de conversão para o [!DNL Amazon] usando a extensão de API de Conversões do [!DNL Amazon]. Para obter mais informações sobre os recursos de encaminhamento de eventos do [!DNL Adobe Experience Platform], consulte a [visão geral do encaminhamento de eventos](../../../ui/event-forwarding/overview.md)

Para obter mais detalhes sobre como depurar sua implementação usando o Depurador da Experience Platform e a ferramenta de Monitoramento de encaminhamento de eventos, leia a [Visão geral da Adobe Experience Platform Debugger](https://experienceleague.adobe.com/en/docs/experience-platform/debugger/home) e as [Atividades do monitor](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/monitoring) no encaminhamento de eventos.