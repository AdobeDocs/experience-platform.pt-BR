---
title: Práticas recomendadas de criação
description: Saiba quais regras e dicas você deve seguir ao criar sua página de documentação de destino para garantir que ela atenda aos padrões de qualidade da documentação do Adobe Experience Platform.
exl-id: b12059f1-6635-41cd-acc5-6ff471111164
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Práticas recomendadas de criação

## Visão geral {#overview}

Esta página descreve as regras que você deve seguir ao [criar sua documentação de destino](./documentation-instructions.md) para garantir que ela atenda aos padrões de qualidade da documentação do Adobe Experience Platform.

## Orientações gerais {#general-guidance}

* Ao preencher o [modelo](./self-service-template.md) da documentação de destino, consulte o guia do colaborador do Adobe para obter informações sobre [vinculação](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html), [tabelas](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#tables), a [sintaxe de marcação com suporte](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html), [orientação de escrita](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html) e muito mais.
* Não inclua observações e estimativas na documentação do produto.
* Na documentação do Experience Platform, os escritores do Adobe usam a **formatação em negrito** para se referir aos controles da interface do usuário, desta forma:
   * Vá para **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]** e selecione a guia **[!UICONTROL Catálogo]**. Veja um exemplo de como os controles da interface do usuário são documentados em um [tutorial de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#select-destination).

## Estilo de escrita

>[!IMPORTANT]
>
>Leia [Orientação de escrita para a documentação do Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html) antes de começar a criar a página de documentação de destino.

* Mantenha suas frases curtas e vá direto ao ponto. Se a sua frase contiver mais de 20 palavras ou usar várias vírgulas, considere dividi-la em frases separadas. Frases com mais de 20 palavras podem ser especialmente desafiadoras para os leitores.
* Não seja excessivamente educado. Evite usar &quot;favor&quot; ou &quot;gentilmente faça ...&quot; na documentação técnica.

## Vinculação {#linking}

Siga o modelo de documentação fornecido e não edite os links existentes no modelo. Ao incluir novos links, leia [usando links na documentação](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html) no guia do colaborador.

## Diretrizes de marca {#branding}

* AEP não é um termo aprovado voltado para o público. Use o Adobe Experience Platform na primeira utilização, depois o Experience Platform e, em seguida, o Experience Platform.
   * **Não usar**: antes de exportar dados do AEP para o seu destino, leia e conclua esses pré-requisitos.
   * **Uso**: antes de exportar dados do Adobe Experience Platform para o Seu Destino, leia e conclua esses pré-requisitos.

## Imagens e capturas de tela {#images-and-screenshots}

* Para obter informações sobre [como vincular a imagens](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#images), consulte o guia do colaborador.
* Ao usar capturas de tela, certifique-se de que sua captura de tela capture toda a tela da interface do usuário do Experience Platform.
* Ao marcar imagens para destacar um determinado controle ou rótulo na página, tente seguir o estilo de marcação usado pela equipe de documentação do Experience Platform. Observe como Baseado em perfil é realçado em [esta captura de tela](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency).
* Use imagens no formato `png`.
* Não use capturas de tela numeradas como nomes de arquivo. Os nomes de arquivo de imagem devem ser descritivos.
   * **Não usar**: `1.png`, `2.png`, `3.png`
   * **Uso**: `yourdestination-authentication-details.png`, `yourdestination-destination-details.png`
* Use o texto alternativo para quaisquer imagens adicionadas à documentação e use a gramática apropriada no texto alternativo.
   * **Não usar**: detalhes da conexão de destino
   * **Uso**: imagem da interface do Experience Platform, mostrando os detalhes de conexão de destino preenchidos.

## Processo {#process}

* O [modelo de documentação](./self-service-template.md) é atualizado com pouca frequência, com base no feedback do parceiro. Antes de começar a criar a documentação para o seu destino, baixe a [última versão do modelo](../assets/docs-framework/yourdestination-template.zip).
* Crie a documentação e crie a solicitação de pull (PR) de documentação de uma ramificação na sua bifurcação *diferente da ramificação principal*. Consulte a seção destino de envio para revisão ao criar na [interface do GitHub](./use-github-interface-to-create-documentation.md#submit-review) ou em [seu ambiente local](./work-in-local-environment.md#submit-review).
