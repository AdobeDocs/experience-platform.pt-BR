---
title: Visão geral da extensão do Splunk
description: Saiba mais sobre a extensão Splunk para encaminhamento de eventos no Adobe Experience Platform.
source-git-commit: e6f0bdcdb11630730834e353064abb960d3d0ea1
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 1%

---

# Visão geral da extensão do Splunk

[Splunk](https://www.splunk.com) é uma plataforma de observabilidade que fornece pesquisa, análise e visualização para obter insights acionáveis sobre seus dados. O Splunk [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) a extensão utiliza o [API REST do coletor de eventos HTTP de partes plunk](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/HECRESTendpoints) para enviar eventos da rede de borda do Adobe Experience Platform para a [Coletor de eventos HTTP Splunk](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector).

O Splunk usa os tokens do portador como mecanismo de autenticação para se comunicar com a API do coletor de eventos do Splunk.

## Casos de uso {#use-cases}

As equipes de marketing podem usar a extensão para os seguintes casos de uso:

| Caso de uso | Descrição |
| --- | --- |
| Análise de comportamento do cliente | As organizações podem capturar dados de eventos de interação do cliente de seu site e encaminhar eventos relevantes para o Splunk. As equipes de marketing e análise podem então realizar análises subsequentes na plataforma Splunk para entender as principais interações e comportamentos do usuário. A plataforma Splunk pode ser usada para gerar gráficos, painéis ou outras visualizações e informar as partes interessadas da empresa. |
| Pesquisa dimensionável em conjuntos de dados grandes | As organizações podem capturar entradas transacionais ou conversacionais como dados de evento do site e encaminhar eventos para o Splunk. As equipes do Analytics podem aproveitar as habilidades de indexação escaláveis do Splunk para filtrar e processar grandes conjuntos de dados para derivar quaisquer insights de negócios e tomar decisões informadas. |

{style=&quot;table-layout:auto&quot;}

## Pré-requisitos {#prerequisites}

Você deve ter uma conta do Splunk para usar essa extensão. Você pode se registrar para uma conta Splunk no [Página inicial do Splunk](https://www.splunk.com/page/sign_up).

>[!NOTE]
>
> A extensão Splunk é compatível com as instâncias corporativas da Splunk Cloud e do Splunk. Este guia documenta a implementação usando [Nuvem Splunk](https://www.splunk.com/en_us/products/splunk-cloud-platform.html) como referência. O processo de configuração para [Splunk Enterprise](https://www.splunk.com/en_us/products/splunk-enterprise.html) é semelhante, mas requer orientação específica do administrador do Splunk Enterprise.

Você também deve ter os seguintes valores técnicos para configurar a extensão:

* Um [Token do Coletor de Eventos](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector#Create_an_Event_Collector_token_on_Splunk_Cloud_Platform). Os tokens normalmente são o formato UUIDv4, como o seguinte: `12345678-1234-1234-1234-1234567890AB`.
* O endereço e a porta da instância da plataforma Splunk para sua organização. Um endereço e uma porta de instância da plataforma normalmente terão o seguinte formato: `mysplunkserver.example.com:443`.
   >[!IMPORTANT]
   >
   > Os pontos de extremidade de plunk referenciados no encaminhamento de eventos devem usar somente a porta `443`. No momento, portas não padrão não são compatíveis em implementações de encaminhamento de eventos.

## Instalar a extensão Splunk {#install}

Para instalar a extensão Splunk Event Collector na interface do usuário, navegue até **Encaminhamento de evento** e selecione uma propriedade para adicionar a extensão ou crie uma nova propriedade.

Depois de selecionar ou criar a propriedade desejada, navegue até **Extensões** > **Catálogo**. Pesquisar por &quot;[!DNL Splunk]&quot; e, em seguida, selecione **[!DNL Install]** na Extensão Splunk.

![Botão Instalar para a extensão Splunk que está sendo selecionada na interface do usuário](../../../images/extensions/splunk/install.png)

## Configurar a extensão Splunk {#configure_extension}

>[!IMPORTANT]
>
>Dependendo das necessidades de implementação, talvez seja necessário criar um esquema, elementos de dados e um conjunto de dados antes de configurar a extensão. Revise todas as etapas de configuração antes de começar para determinar quais entidades você precisa configurar para o caso de uso.

Selecionar **Extensões** no painel de navegação esquerdo. Em **Instalado**, selecione **Configurar** na extensão Splunk.

![Botão Configurar para a extensão do Splunk que está sendo selecionada na interface do usuário](../../../images/extensions/splunk/configure.png)

Para **[!UICONTROL URL do Coletor de Eventos HTTP]**, digite o endereço e a porta da instância da plataforma Splunk. Em **[!UICONTROL Token de acesso]**, insira [!DNL Event Collector Token] valor. Quando terminar, selecione **[!UICONTROL Salvar]**.

![Opções de configuração preenchidas na interface do usuário](../../../images/extensions/splunk/input.png)

## Configurar uma regra de encaminhamento de eventos {#config_rule}

Comece a criar uma nova regra de encaminhamento de eventos [regra](../../../ui/managing-resources/rules.md) e configure as condições conforme desejado. Ao selecionar as ações para a regra, selecione o [!UICONTROL Splunk] e selecione a [!UICONTROL Criar evento] tipo de ação. Controles adicionais são exibidos para configurar ainda mais o Evento Splunk.

![Definir Configuração de Ação](../../../images/extensions/splunk/action-configurations.png)

A próxima etapa é mapear as propriedades do evento Splunk para elementos de dados criados anteriormente. Os mapeamentos opcionais suportados com base nos dados de evento de entrada que podem ser configurados são fornecidos abaixo. Consulte a [Documentação do Splunk](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/FormateventsforHTTPEventCollector#Event_metadata) para obter mais detalhes.

| Nome do campo | Descrição |
| --- | --- |
| [!UICONTROL Evento ]<br><br>**(OBRIGATÓRIO)** | Indique como você deseja fornecer os dados do evento. Os dados do evento podem ser atribuídos à variável `event` no objeto JSON na solicitação HTTP ou pode ser texto bruto. O `event` A chave está no mesmo nível no pacote de eventos JSON que as chaves de metadados. No `event` chaves de valor, os dados podem estar em qualquer forma necessária (como uma string, um número, outro objeto JSON e assim por diante). |
| [!UICONTROL Host] | O nome do host do cliente do qual você está enviando dados. |
| [!UICONTROL Tipo de origem] | O tipo de origem a ser atribuído aos dados do evento. |
| [!UICONTROL Fonte] | O valor de origem a ser atribuído aos dados do evento. Por exemplo, se estiver enviando dados de um aplicativo em desenvolvimento, defina essa chave como o nome do aplicativo. |
| [!UICONTROL Índice] | O nome do índice dos dados do evento. O índice especificado aqui deve estar dentro da lista de índices permitidos se o token tiver o parâmetro de índices definido. |
| [!UICONTROL Hora] | A hora do evento. O formato de hora padrão é horário UNIX (no formato `<sec>.<ms>`) e depende do fuso horário local. Por exemplo, `1433188255.500` indica 1433188255 segundos e 500 milissegundos após a época ou segunda-feira, 1° de junho de 2015, em 7:50:17:00 GMT |
| [!UICONTROL Campos] | Especifique um objeto JSON bruto ou um conjunto de pares de valores chave que contenham campos personalizados explícitos a serem definidos no momento do índice.  O `fields` A chave não se aplica aos dados brutos.<br><br>Solicitações que contêm `fields` deve ser enviada para o `/collector/event` endpoint ou não serão indexados. Para obter mais informações, consulte a documentação do Splunk em [extrações de campo indexadas](http://docs.splunk.com/Documentation/Splunk/8.2.5/Data/IFXandHEC). |

### Validar dados no Splunk {#validate}

Depois de criar e executar a regra de encaminhamento de eventos, valide se o evento enviado para a API do Splunk é exibido conforme esperado na interface do usuário do Splunk. Se a coleção de eventos e a integração do Experience Platform tiverem sido bem-sucedidas, você verá os eventos no console do Splunk da seguinte maneira:

![Dados do evento que aparecem na interface do usuário do Splunk durante a validação](../../../images/extensions/splunk/splunk-data.png)

## Próximas etapas

Este documento cobriu como instalar e configurar a extensão de encaminhamento de eventos do Splunk na interface do usuário. Para obter mais informações sobre como coletar dados do evento no Splunk, consulte a documentação oficial:

* [Configurar e usar o Coletor de Eventos HTTP na Web Splunk ](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector)
* [Configurar autenticação com tokens](https://docs.splunk.com/Documentation/Splunk/8.2.5/Security/Setupauthenticationwithtokens#Prerequisites_for_activating_tokens)
* [Solucionar problemas do coletor de eventos HTTP](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/TroubleshootHTTPEventCollector) (também lista um compêndio de [possíveis códigos de erro](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/TroubleshootHTTPEventCollector#Possible_error_codes))
