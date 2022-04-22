---
title: Práticas recomendadas de criação
description: Saiba quais regras e dicas você deve seguir ao criar a página de documentação de destino, para garantir que ela atenda aos padrões de qualidade da documentação do Adobe Experience Platform.
source-git-commit: 35e5c388e9572a3b27ec4bce55e766725936eda4
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# Práticas recomendadas de criação

## Visão geral {#overview}

Esta página descreve as regras que devem ser seguidas quando [criação da documentação de destino](./documentation-instructions.md) para garantir que atenda aos padrões de qualidade da documentação do Adobe Experience Platform.

## Orientação geral {#general-guidance}

* Ao preencher o [modelo](./self-service-template.md) para obter a documentação de destino, consulte o guia do colaborador do Adobe para obter informações sobre [vinculação](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en), [tabelas](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#tables), o [sintaxe de marcação suportada](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en), [orientação escrita](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en)e muito mais.
* Não inclua observações e estimativas na documentação do produto.
* Na documentação do Experience Platform, os Adobe-escritores usam **formatação em negrito** para se referir aos controles da interface do usuário, desta forma:
   * Ir para **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]** e selecione o **[!UICONTROL Catálogo]** guia . Veja um exemplo de como os controles da interface do usuário são documentados em um [tutorial de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#select-destination).

## Vinculação {#linking}

Siga o modelo de documentação fornecido e não edite os links existentes no modelo. Ao incluir novos links, leia [usando links na documentação](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en) no guia do colaborador.

## Diretrizes de marca {#branding}

* O AEP não é um termo aprovado aberto ao público. Use o Adobe Experience Platform na primeira utilização, depois o Experience Platform e, em seguida, a Plataforma.
   * **Não use**: Antes de exportar dados do AEP para o seu destino, leia e conclua esses pré-requisitos.
   * **Use**: Antes de exportar dados do Adobe Experience Platform para o seu destino, leia e conclua esses pré-requisitos.

## Imagens e capturas de tela {#images-and-screenshots}

* Para obter informações sobre [como vincular a imagens](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#images), consulte o guia do colaborador.
* Ao usar capturas de tela, certifique-se de que a captura de tela capture a tela inteira da interface do usuário da plataforma.
* Ao marcar imagens para realçar um determinado controle ou rótulo na página, tente seguir o estilo de marcação usado pela equipe de documentação do Experience Platform. Observe como a função Baseada em perfil é realçada em [esta captura de tela](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency).
* Use `png` formatar imagens.
* Não use capturas de tela numeradas como nomes de arquivo. Os nomes de arquivo da imagem devem ser descritivos.
   * **Não use**: `1.png`, `2.png`, `3.png`
   * **Utilização**: `yourdestination-authentication-details.png`, `yourdestination-destination-details.png`
* Use o texto alternativo para as imagens que você adicionar à documentação e use a gramática correta no texto alternativo.
   * **Não use**: Detalhes da conexão de destino
   * **Use**: Imagem da interface do usuário da plataforma, mostrando os detalhes da conexão de destino preenchidos.

## Processo {#process}

* O [modelo de documentação](./self-service-template.md) é atualizado com pouca frequência, com base no feedback do parceiro. Antes de começar a criar a documentação para o seu destino, baixe o [versão mais recente do modelo](/help/destinations/destination-sdk/docs-framework/assets/yourdestination-template.zip).
* Crie a documentação e crie a solicitação de extração de documentação (PR) a partir de uma ramificação em sua bifurcação *que não a sucursal principal*. Consulte a seção Enviar destino para revisão ao criar no [Interface do GitHub](./use-github-interface-to-create-documentation.md#submit-review) ou [seu ambiente local](./work-in-local-environment.md#submit-review).