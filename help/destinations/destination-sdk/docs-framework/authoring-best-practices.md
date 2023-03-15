---
title: Práticas recomendadas de criação
description: Saiba quais regras e dicas você deve seguir ao criar sua página de documentação de destino para garantir que ela atenda aos padrões de qualidade da documentação do Adobe Experience Platform.
exl-id: b12059f1-6635-41cd-acc5-6ff471111164
source-git-commit: 0b9b724c2530e43ce681011d12fc1341148ddbf5
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Práticas recomendadas de criação

## Visão geral {#overview}

Esta página descreve as regras que você deve seguir ao [criação da documentação de destino](./documentation-instructions.md) para garantir que atenda aos padrões de qualidade da documentação do Adobe Experience Platform.

## Orientações gerais {#general-guidance}

* Ao preencher o [modelo](./self-service-template.md) para obter a documentação de destino, consulte o guia do colaborador de Adobe para obter informações sobre [vinculação](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en), [tabelas](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#tables), o [sintaxe de markdown compatível](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en), [orientação de escrita](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en)e muito mais.
* Não inclua observações e estimativas na documentação do produto.
* Na documentação do Experience Platform, os gravadores de Adobe usam **bold formatação** para consultar os controles da interface do usuário, desta forma:
   * Ir para **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]** e selecione a variável **[!UICONTROL Catálogo]** guia. Exibir um exemplo de como os controles da interface do usuário são documentados em um [tutorial de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#select-destination).

## Estilo de escrita

>[!IMPORTANT]
>
>Ler [Orientação de escrita para a documentação do Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en) antes de começar a criar a página de documentação de destino.

* Mantenha suas frases curtas e vá direto ao ponto. Se a sua frase contiver mais de 20 palavras ou usar várias vírgulas, considere dividi-la em frases separadas. Frases com mais de 20 palavras podem ser especialmente desafiadoras para os leitores.
* Não seja excessivamente educado. Evite usar &quot;favor&quot; ou &quot;gentilmente faça ...&quot; na documentação técnica.

## Vinculação {#linking}

Siga o modelo de documentação fornecido e não edite os links existentes no modelo. Ao incluir novos links, leia [uso de links na documentação](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en) no guia do colaborador.

## Diretrizes de marca {#branding}

* AEP não é um termo aprovado voltado para o público. Use o Adobe Experience Platform na primeira utilização, depois o Experience Platform e, por fim, a Platform.
   * **Não usar**: antes de exportar dados do AEP para o seu destino, leia e conclua esses pré-requisitos.
   * **Uso**: antes de exportar dados do Adobe Experience Platform para o seu destino, leia e conclua esses pré-requisitos.

## Imagens e capturas de tela {#images-and-screenshots}

* Para obter informações sobre [como vincular a imagens](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#images), consulte o guia do colaborador.
* Ao usar capturas de tela, certifique-se de que sua captura de tela capture toda a tela da interface do usuário da plataforma.
* Ao marcar as imagens para destacar um determinado controle ou rótulo na página, tente seguir o estilo de marcação usado pela equipe de documentação do Experience Platform. Observe como a dimensão Baseado em perfil é destacada no [esta captura de tela](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency).
* Use `png` formatar imagens.
* Não use capturas de tela numeradas como nomes de arquivo. Os nomes de arquivo de imagem devem ser descritivos.
   * **Não usar**: `1.png`, `2.png`, `3.png`
   * **Utilização**: `yourdestination-authentication-details.png`, `yourdestination-destination-details.png`
* Use o texto alternativo para quaisquer imagens adicionadas à documentação e use a gramática apropriada no texto alternativo.
   * **Não usar**: Detalhes da conexão de destino
   * **Uso**: imagem da interface da Platform, mostrando os detalhes da conexão de destino preenchidos.

## Processo {#process}

* A variável [modelo de documentação](./self-service-template.md) O é atualizado com pouca frequência, com base nos comentários dos parceiros. Antes de começar a criar a documentação para o seu destino, verifique se você baixou o [versão mais recente do modelo](/help/destinations/destination-sdk/docs-framework/assets/yourdestination-template.zip).
* Crie a documentação e crie a solicitação de pull (PR) de documentação a partir de uma ramificação na sua bifurcação *que não seja a ramificação principal*. Consulte a seção destino de envio para revisão ao criar na [Interface do GitHub](./use-github-interface-to-create-documentation.md#submit-review) ou em [seu ambiente local](./work-in-local-environment.md#submit-review).
