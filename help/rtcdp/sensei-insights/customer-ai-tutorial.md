---
title: Prever pontuações de propensão do cliente usando a IA do cliente (alfa)
seo-title: Prever pontuações de propensão do cliente usando a IA do cliente (alfa)
description: Este tutorial fornece instruções sobre como usar a API do cliente (alfa)
seo-description: Este tutorial fornece instruções sobre como usar a API do cliente (alfa)
index: false
translation-type: tm+mt
source-git-commit: e0d11adb7f0ece9344efb118b4199ecb1fc37bb3

---


# Prever pontuações de propensão do cliente usando a IA do cliente (alfa)

>[!NOTE]
>A funcionalidade de IA do cliente descrita neste documento está em alfa. A documentação e a funcionalidade estão sujeitas a alterações.

Construído e capacitado pelo Adobe Sensei, a API do cliente na Adobe Experience Platform permite que você gere pontuações de propensão personalizadas sem precisar se preocupar com os aspectos de aprendizado da máquina.

Este tutorial aborda as etapas para trabalhar com a API do cliente usando a interface do usuário da plataforma de experiência. As etapas são fornecidas para os seguintes tópicos:

* [Configurar uma instância](#configure-an-instance)
* [Criar segmentos de clientes com pontuações previstas](#create-customer-segments-with-predicted-scores)

## Introdução

Este guia exige uma compreensão de trabalho dos vários serviços da plataforma envolvidos no uso da API do cliente. Antes de iniciar este tutorial, reveja os seguintes documentos:

* [Visão geral do Perfil do cliente em tempo real](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)
* [Visão geral do Serviço de segmentação](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/segmentation/segmentation-overview.md)
* [Guia do usuário do Construtor de segmentos](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/segmentation/segment-builder-guide.md)

## Configurar uma instância

A plataforma Experience fornece a IA do cliente como um serviço simples de uso do Adobe Sensei que pode ser configurado para diferentes casos de uso. As seções a seguir fornecem etapas para configurar uma instância da API do cliente.

### Configurar sua instância

Na interface do usuário da plataforma, clique em **Serviços** no painel de navegação esquerdo. O navegador **Serviços** é exibido e exibe todos os serviços disponíveis à sua disposição. No container para API do cliente, clique em **Abrir**.

![](./images/service.png)

A tela *Customer AI* (AI do cliente) exibe todas as instâncias existentes do Customer AI. Clique em **Criar instância**.

![](./images/customer_ai.png)

O fluxo de trabalho de criação da instância é exibido, começando na etapa *Configuração* .

Abaixo estão informações importantes sobre valores para os quais você deve fornecer à instância:

* O nome da instância será usado em todos os locais onde a pontuação da AI do cliente for exibida. Assim, os nomes devem descrever o que as pontuações de previsão representam, por exemplo, &quot;Probabilidade de cancelar a subscrição de revistas&quot;.

* O tipo de propensão determina a intenção da pontuação e da polaridade da métrica. Você pode escolher **Churn** ou **Conversion**.

* A fonte de dados se refere ao conjunto de dados de entrada que será usado para prever pontuações. Por padrão, a IA do cliente usa os dados do Evento da experiência do consumidor para calcular as pontuações de propensão. Ao selecionar um conjunto de dados no seletor suspenso, somente os que são compatíveis com a IA do cliente serão listados.

* Por padrão, as pontuações de propensão são geradas para todos os perfis, a menos que uma população qualificada seja especificada. Você pode especificar uma população qualificada definindo condições para incluir ou excluir perfis com base em eventos.

Forneça os valores necessários e clique em **Avançar**.

![](./images/setup.png)

### Definir uma meta

A etapa *Definir meta* é exibida e fornece um ambiente interativo para que você defina visualmente uma meta. Uma meta é composta de um ou mais eventos, nos quais cada ocorrência de evento é baseada na condição que contém. O objetivo de uma instância da API do cliente é determinar a probabilidade de atingir sua meta dentro de um determinado intervalo de tempo.

Clique em **Inserir nome** do campo e selecione um campo na lista suspensa. Clique na segunda entrada e selecione uma cláusula para a condição do evento, em seguida, forneça o valor do público alvo para concluir o evento. eventos adicionais podem ser configurados clicando em **Adicionar evento**. Por fim, conclua a meta aplicando um período de previsão em número de dias e clique em **Avançar**.

![](./images/goal.png)

### Configurar um agendamento *(opcional)*

A etapa *avançada* é exibida. Esta etapa opcional permite configurar uma programação para automatizar execuções de previsão, definir exclusões de previsão para filtrar determinados eventos ou clicar em **Concluir** se nada for necessário.

Configure um agendamento de pontuação configurando a Frequência *de* Pontuação. As execuções de previsão automatizadas podem ser programadas para serem executadas semanalmente ou mensalmente.

![](./images/schedule.png)

Abaixo da configuração da programação, você pode definir exclusões de previsão para impedir que eventos que atendem a determinadas condições sejam avaliados ao gerar pontuações. Este recurso pode ser usado para filtrar entradas de dados irrelevantes.

Para excluir determinados eventos, clique em **Adicionar exclusão** e defina o evento da mesma forma que a meta é definida. Para remover uma exclusão, clique nas elipses (**...**) na parte superior direita do container do evento e clique em **Remover Container**.

![](./images/exclusion.png)

Exclua eventos conforme necessário e clique em **Concluir** para criar a instância.

![](./images/advanced.png)

Se a instância for criada com êxito, uma execução de previsão será acionada imediatamente e as subsequentes serão executadas de acordo com sua programação definida.

>[!NOTE] Dependendo do tamanho dos dados de entrada, as execuções de previsão podem levar até 24 horas para serem concluídas.

Ao seguir esta seção, você configurou uma instância do AI do cliente e uma execução de previsão foi executada. Quando a execução for concluída com êxito, insights pontuados automaticamente hidratarão Perfis com pontuações previstas. Aguarde 24 horas antes de continuar com a próxima seção deste tutorial.

## Criar segmentos de clientes com pontuações previstas

Quando uma execução de previsão é concluída, as pontuações de propensão previstas são automaticamente consumidas pelos Perfis. O enriquecimento de Perfis com pontuações de AI do cliente permite a criação de segmentos de clientes com base em pontuações de propensão. Esta seção fornece etapas para a criação de segmentos usando o Construtor de segmentos. Para obter um tutorial mais robusto sobre a criação de segmentos, consulte o guia [do usuário do Construtor de](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/segmentation/segment-builder-guide.md)segmentos.

Na interface do usuário da plataforma, clique em **Segmentos** no painel de navegação esquerdo e clique em **Criar segmento**.

![](./images/segments.png)

O Construtor *de segmentos* é exibido. Na coluna *Campos* à esquerda e na guia *Atributos* , clique na pasta chamada Perfil **individual** XDM e clique na pasta com a namespace de sua organização. A pasta chamada AI **do** cliente contém os resultados de execuções de previsão e são nomeados após a instância à qual as pontuações pertencem. Clique e acesse os resultados da instância desejada.

![](./images/results.png)

Localizado no centro do Construtor de segmentos, arraste e solte o atributo **Pontuação** na tela *do construtor de* regras para definir uma regra.

Na coluna de propriedades *do* segmento à direita, selecione uma política *de* mesclagem e forneça um nome para o segmento. Em seguida, clique em **Salvar** para criar o segmento.

![](./images/properties.png)

## Próximas etapas

Ao seguir este tutorial, você configurou com êxito uma instância da AI do cliente, gerou pontuações de propensão e criou um segmento imposto pelas pontuações de propensão usando o Construtor de segmentos. Seu segmento de cliente agora pode ser usado por destinos ativados para público alvo de suas audiências. Consulte a visão geral [de](../destinations/destinations-overview.md) Destinos para obter mais informações.
