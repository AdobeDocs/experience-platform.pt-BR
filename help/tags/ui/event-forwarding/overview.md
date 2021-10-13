---
title: Visão geral do encaminhamento de eventos
description: Saiba mais sobre o encaminhamento de eventos da Adobe Experience Platform, que permite usar a Platform Edge Network para executar tarefas sem alterar a sua implementação de tag.
feature: Event Forwarding
exl-id: 18e76b9c-4fdd-4eff-a515-a681bc78d37b
source-git-commit: 5218e6cf82b74efbbbcf30495395a4fe2ad9fe14
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 96%

---

# Visão geral do encaminhamento de eventos

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

O encaminhamento de eventos da Adobe Experience Platform diminui o peso da página da Web e do aplicativo usando a Adobe Experience Platform Edge Network para executar tarefas normalmente realizadas no cliente. As regras de encaminhamento de eventos podem transformar e enviar dados para novos destinos sem alterar as implementações do lado do cliente.

O encaminhamento de eventos, combinado a SDKs da Web e móveis da Adobe Experience Platform, torna possível:

* Fazer uma chamada única da página que contém uma carga de dados. Os dados são então federados do lado do servidor para reduzir o tráfego de rede do lado do cliente e fornecer uma experiência mais rápida.
* Diminuir o tempo de carregamento das páginas da Web para que seu site esteja em conformidade com as práticas recomendadas do setor em relação ao desempenho.
* Aumentar a transparência e o controle sobre quais tipos de dados são enviados e para onde, em todas as propriedades de tag.
* Criar uma regra de encaminhamento de eventos para enviar dados rastreados anteriormente para um novo destino.

## Desempenho aprimorado

Em um ambiente cada vez mais competitivo, as empresas devem priorizar o desempenho para manter e expandir a participação no mercado. O encaminhamento de eventos melhora o desempenho do site e do aplicativo em dispositivos móveis, IoT e OTT. As taxas de conversão do site podem aumentar devido aos tempos de carregamento mais rápidos, os aplicativos móveis não consomem as baterias tão rapidamente e os aplicativos OTT são tão responsivos quanto os mesmos aplicativos executados em dispositivos móveis. À medida que o desempenho aumenta, também é comum que as taxas de conversão aumentem.

## Melhor governança de dados

À medida que a pilha de tecnologia cresce e os dados são enviados para mais e mais destinos, o desafio de controlar quais dados são enviados torna-se mais difícil. A normalização de regulamentos como o GDPR e o CCPA forçam as empresas a exercer mais controle sobre um problema de dados que está se tornando cada vez mais difícil.

O encaminhamento de eventos ajuda as equipes de marketing a expandir os negócios enquanto controlam os dados. Ele diminui o número de tecnologias do lado do cliente que os profissionais de marketing precisam usar para chegar ao mercado alvo e enviar dados a destinos que não são da Adobe. Isso torna mais fácil para as equipes de implementação gerenciarem os dados que fluem do cliente para vários destinos

## Diferenças entre o encaminhamento de eventos e as tags

É importante observar as seguintes diferenças entre o encaminhamento de eventos e as tags:

* Tokenização do elemento de dados

   * Tags: em uma regra, os elementos de dados são tokenizados com um `%` no início e no fim do nome do elemento de dados. Por exemplo, `%viewportHeight%`.

   * Encaminhamento de eventos: em uma regra, os elementos de dados são tokenizados com um `{{` no início e `}}` no fim do nome do elemento de dados. Por exemplo, `{{viewportHeight}}`.

* Como os dados são referenciados

   Para referenciar dados da rede de borda, o caminho do elemento de dados deve ser `arc.event._<element>_`.

   `arc` significa Contexto de resposta da Adobe.

   Por exemplo: `arc.event.xdm.web.webPageDetails.URL`

   >[!IMPORTANT]
   >
   >Se esse caminho for especificado incorretamente, os dados não serão coletados.


* Sequência de ações de regras

   Na seção Ação de uma regra, as regras do encaminhamento de eventos são sempre executadas sequencialmente. Certifique-se de que a ordem das ações esteja correta ao salvar uma regra. Essa sequência de execução não pode ser escolhida como acontece com as tags.

* Versões JavaScript de código personalizado

   As tags usam a versão es5 do JavaScript. O encaminhamento de eventos usa a versão es6.

<!--doc Adobe Cloud Connector extension, get from Jon-->
