---
title: Configurar a extensão de tag do SDK da Web
description: Saiba como configurar a extensão de tag do SDK da Web do Experience Platform na interface do usuário de tags.
exl-id: 22425daa-10bd-4f06-92de-dff9f48ef16e
source-git-commit: dea75b92847320284e1dc1b939f3ae11a12077a8
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 6%

---

# Configurar a extensão de tag do SDK da Web

A variável [!DNL Web SDK] A extensão de tag envia dados para a Adobe Experience Cloud a partir das propriedades da Web por meio da Rede de borda do Experience Platform.

A extensão permite transmitir dados para a Platform, sincronizar identidades, processar sinais de consentimento do cliente e coletar automaticamente dados de contexto.

Este documento explica como configurar a extensão de tag na interface do usuário de tags.

## Instalar a extensão de tag do SDK da Web {#install}

A extensão de tag do SDK da Web precisa de uma propriedade para ser instalada. Se ainda não tiver feito isso, consulte a documentação em [criação de uma propriedade de tag](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html?lang=pt-BR).

Após criar uma propriedade, abra a propriedade e selecione a variável **[!UICONTROL Extensões]** na barra lateral esquerda.

Selecione o **[!UICONTROL Catálogo]** guia. Na lista de extensões disponíveis, localize o [!DNL Web SDK] e selecione **[!UICONTROL Instalar]**.

![Imagem mostrando a interface do usuário de tags com a extensão SDK da Web selecionada](assets/web-sdk-install.png)

Depois de selecionar **[!UICONTROL Instalar]**, você deve configurar a extensão de tag do SDK da Web e salvar a configuração.

>[!NOTE]
>
>A extensão de tag só é instalada depois de salvar a configuração. Consulte as próximas seções para saber como configurar a extensão de tag.

## Definir configurações de instância {#general}

As opções de configuração na parte superior da página informam à Adobe Experience Platform para onde rotear os dados e quais configurações usar no servidor.

![Imagem que mostra as configurações gerais da extensão de tag do SDK da Web na interface do usuário de tags](assets/web-sdk-ext-general.png)

* **[!UICONTROL Nome]**: a extensão SDK da Web do Adobe Experience Platform oferece suporte a várias instâncias na página. O nome é usado para enviar dados para várias organizações com uma configuração de tag. O nome da instância é padronizado como `alloy`. No entanto, é possível alterar o nome da instância para qualquer nome de objeto JavaScript válido.
* **[!UICONTROL IMS organization ID]**: a ID da organização para a qual você deseja que os dados sejam enviados no Adobe. Na maioria das vezes, use o valor padrão preenchido automaticamente. Quando houver várias instâncias na página, preencha esse campo com o valor da segunda organização para a qual deseja enviar dados.
* **[!UICONTROL Domínio de borda]**: o domínio do qual a extensão envia e recebe dados. O Adobe recomenda usar um domínio próprio (CNAME) para essa extensão. O domínio padrão de terceiros funciona em ambientes de desenvolvimento, mas não é adequado para ambientes de produção. As instruções sobre como configurar um CNAME primário estão listadas [aqui](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=pt-BR).

## Definir configurações de sequência de dados {#datastreams}

Essa seção permite selecionar os fluxos de dados que devem ser usados para cada um dos três ambientes disponíveis (produção, preparo e desenvolvimento).

Quando uma solicitação é enviada para a Rede de borda, uma ID de fluxo de dados é usada para fazer referência à configuração do lado do servidor. Você pode atualizar a configuração sem precisar fazer alterações de código no site.

Consulte o guia sobre [sequências de dados](../../../../datastreams/overview.md) para saber como configurar um fluxo de dados.

Você pode escolher um fluxo de dados nos menus suspensos disponíveis ou selecionar **[!UICONTROL Inserir valores]** e insira uma ID de fluxo de dados personalizada para cada ambiente.

![Imagem que mostra as configurações de sequência de dados da extensão de tag do SDK da Web na interface do usuário de tags](assets/web-sdk-ext-datastreams.png)

## Definir configurações de privacidade {#privacy}

Esta seção permite configurar como o SDK da Web lida com sinais de consentimento do usuário do seu site. Especificamente, ela permite selecionar o nível padrão de consentimento assumido de um usuário se nenhuma outra preferência de consentimento explícito tiver sido fornecida.

O nível de consentimento padrão não é salvo no perfil do usuário.

![Imagem mostrando as configurações de privacidade da extensão de tag do SDK da Web na interface do usuário de tags](assets/web-sdk-ext-privacy.png)

| [!UICONTROL Nível de consentimento padrão] | Descrição |
| --- | --- |
| [!UICONTROL Entrada] | Colete eventos que ocorrem antes de o usuário fornecer preferências de consentimento. |
| [!UICONTROL Saída] | Descartar eventos que ocorrem antes de o usuário fornecer preferências de consentimento. |
| [!UICONTROL Pending] | Enfileirar eventos que ocorrem antes de o usuário fornecer preferências de consentimento. Quando as preferências de consentimento são fornecidas, os eventos são coletados ou descartados, dependendo das preferências fornecidas. |
| [!UICONTROL Fornecido pelo elemento de dados] | O nível de consentimento padrão é determinado por um elemento de dados separado que você define. Ao usar essa opção, você deve especificar o elemento de dados usando o menu suspenso fornecido. |

>[!TIP]
>
>Uso **[!UICONTROL Saída]** ou **[!UICONTROL Pending]** se você precisar de consentimento explícito do usuário para suas operações comerciais.

## Definir configurações de identidade {#identity}

Esta seção permite definir o comportamento do SDK da Web quando se trata de lidar com a identificação do usuário.

![Imagem que mostra as configurações de identidade da extensão de tag do SDK da Web na interface do usuário de tags](assets/web-sdk-ext-identity.png)

* **[!UICONTROL Migrar ECID da VisitorAPI]**: essa opção é ativada por padrão. Quando esse recurso está ativado, o SDK pode ler a variável `AMCV` e `s_ecid` cookies e defina o `AMCV` cookie usado por [!DNL Visitor.js]. Esse recurso é importante ao migrar para o SDK da Web, pois algumas páginas ainda podem estar usando [!DNL Visitor.js]. Essa opção permite que o SDK continue usando a mesma [!DNL ECID] para que os usuários não sejam identificados como dois usuários separados.
* **[!UICONTROL Usar cookies de terceiros]**: quando esta opção é ativada, o SDK da Web tenta armazenar um identificador do usuário em um cookie de terceiros. Se for bem-sucedido, o usuário será identificado como um único usuário durante a navegação em vários domínios, em vez de ser identificado como um usuário separado em cada domínio. Se essa opção estiver ativada, o SDK ainda poderá não ser capaz de armazenar o identificador do usuário em um cookie de terceiros se o navegador não for compatível com cookies de terceiros ou tiver sido configurado pelo usuário para não permitir cookies de terceiros. Nesse caso, o SDK armazena apenas o identificador no domínio próprio.

  >[!IMPORTANT]
  >>Cookies de terceiros não são compatíveis com o [ID do dispositivo primário](../../../../edge/identity/first-party-device-ids.md) no SDK da Web.
Você pode usar IDs de dispositivo primário ou cookies de terceiros, mas não pode usar ambos os recursos simultaneamente.
  >
## Definir configurações de personalização {#personalization}

Esta seção permite configurar como você deseja ocultar determinadas partes de uma página enquanto o conteúdo personalizado é carregado. Isso garante que seus visitantes vejam apenas a página personalizada.

![Imagem que mostra as configurações de personalização da extensão de tag do SDK da Web na interface do usuário de tags](assets/web-sdk-ext-personalization.png)

* **[!UICONTROL Migração do Target da at.js para o SDK da Web]**: use esta opção para ativar [!DNL Web SDK] para ler e gravar o legado `mbox` e `mboxEdgeCluster` cookies usados pela at.js `1.x` ou `2.x` bibliotecas. Isso ajuda a manter o perfil do visitante ao mover de uma página que usa o SDK da Web para uma página que usa at.js `1.x` ou `2.x` bibliotecas e vice-versa.

### Estilo pré-ocultação {#prehiding-style}

O editor de estilo pré-ocultação permite definir regras CSS personalizadas para ocultar seções específicas de uma página. Quando a página é carregada, o SDK da Web usa esse estilo para ocultar as seções que precisam ser personalizadas, recupera a personalização e desoculta as seções de página personalizadas. Dessa forma, seus visitantes visualizam as páginas já personalizadas, sem ver o processo de recuperação da personalização.

### Pré-ocultação de trecho {#prehiding-snippet}

O trecho pré-ocultação é útil quando a biblioteca do SDK da Web é carregada de forma assíncrona. Nessa situação, para evitar oscilação, recomendamos ocultar o conteúdo antes que a biblioteca do SDK da Web seja carregada.

Para usar o trecho pré-ocultação, copie-o e cole-o dentro do `<head>` elemento da sua página.

>[!IMPORTANT]
>
Ao usar o trecho pré-ocultação, o Adobe recomenda usar o mesmo [!DNL CSS] regra como a usada pelo [estilo pré-ocultação](#prehiding-style).

## Definir configurações da coleção de dados {#data-collection}

![Imagem que mostra as configurações da coleção de dados da extensão de tag do SDK da Web na interface do usuário de tags](assets/web-sdk-ext-collection.png)

* **[!UICONTROL Função de retorno de chamada]**: a função de retorno de chamada fornecida na extensão também é chamada de [`onBeforeEventSend` função](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=pt-BR) na biblioteca. Essa função permite modificar eventos globalmente antes que sejam enviados para a Rede de borda. Informações mais detalhadas sobre como usar esta função podem ser encontradas [aqui](../../../../edge/fundamentals/tracking-events.md#modifying-events-globally).
* **[!UICONTROL Ativar a coleta de dados de cliques]**: o SDK da Web pode coletar automaticamente informações de cliques em links para você. Por padrão, esse recurso está ativado, mas pode ser desativado usando essa opção. Os links também são rotulados como links de download se contiverem uma das expressões de download listadas no [!UICONTROL Baixar qualificador de link] caixa de texto. O Adobe fornece alguns qualificadores padrão de link de download. Você pode editá-los de acordo com suas necessidades.
* **[!UICONTROL Dados de contexto coletados automaticamente]**: por padrão, o SDK da Web coleta determinados dados de contexto relacionados ao dispositivo, Web, ambiente e contexto de local. Se quiser ver uma lista dos Adobe de informações coletados, você pode encontrá-la [aqui](../../../../edge/data-collection/automatic-information.md). Se não quiser que esses dados sejam coletados ou se quiser apenas determinadas categorias de dados, selecione **[!UICONTROL Informações de contexto específicas]** e selecione os dados que deseja coletar.

## Configurar substituições de sequência de dados {#datastream-overrides}

As substituições de sequência de dados permitem definir configurações adicionais para suas sequências de dados, que são transmitidas para a rede de borda por meio do SDK da Web.

Isso ajuda a acionar comportamentos de sequência de dados diferentes dos tradicionais sem criar uma nova sequência de dados ou modificar as configurações existentes.

Criar uma substituição de configuração da sequência de dados é um processo de duas etapas:

1. Primeiro, você deve definir as substituições de configuração da sequência na [página de configuração da sequência de dados](../../../../datastreams/configure.md).
2. Em seguida, você deve enviar as substituições para a Rede de borda por meio de um comando do SDK da Web ou usando a extensão de tag do SDK da Web.

Ver a sequência de dados [documentação de substituições de configuração](../../../../datastreams/overrides.md) para obter instruções detalhadas sobre como substituir configurações de sequência de dados.

Como alternativa à transmissão de sobreposições por meio de um comando do SDK da Web, você pode configurar as sobreposições na tela de extensão de tag mostrada abaixo.

>[!IMPORTANT]
>
As substituições de fluxo de dados devem ser configuradas com base no ambiente. Os ambientes de desenvolvimento, armazenamento temporário e produção têm substituições separadas. Você pode copiar as configurações entre elas usando as opções dedicadas mostradas na tela abaixo.

![Imagem que mostra as sobreposições de configuração da sequência de dados na página de extensão de tag do SDK da Web.](assets/datastream-overrides.png)

## Definir configurações avançadas

Use o **[!UICONTROL Caminho base da borda]** se precisar alterar o caminho base usado para interagir com a rede de borda. Isso não deve exigir atualização, mas no caso de você participar de um beta ou alfa, o Adobe pode solicitar que você altere esse campo.

![Imagem que mostra as configurações avançadas na página de extensão de tag do SDK da Web.](assets/advanced-settings.png)
