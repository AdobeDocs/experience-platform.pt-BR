---
title: Melhorias na composição do público-alvo
description: Saiba mais sobre os aprimoramentos feitos na Composição de público-alvo com enriquecimento de público e ativação mais rápida.
hide: true
hidefromtoc: true
source-git-commit: 9c790f0b47161301fa8c02c4afb7edfb925e1499
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# Melhorias na composição do público-alvo

Agora você tem acesso a **dois** aprimoramentos da Composição de Público-Alvo:

- [Enriquecimento de público](#audience-enrichment)
- [Ativação mais rápida](#faster-activation)

## Enriquecimento de público {#audience-enrichment}

O enriquecimento do público-alvo permite produzir a matriz de valores que permite que seus perfis se qualifiquem para o público-alvo criado.

Para adicionar enriquecimentos de público-alvo à sua composição, selecione o bloco **[!UICONTROL Audience]** mais acima na tela. Depois de dar um nome ao público-alvo, selecione **[!UICONTROL Build rule]** para abrir a tela do construtor de regras.

![O bloco Público-alvo está realçado, assim como o botão Criar regra.](/help/segmentation/images/ui/composition-enhancements/select-build-rule.png)

A tela do construtor de regras é exibida. Agora você pode criar um critério de filtro para o enriquecimento do público-alvo. Este critério de filtro **deve** incluir um atributo que esteja dentro de uma matriz. O atributo que é uma matriz depende da estrutura do esquema da sua organização. Depois de criar seus critérios de filtro, selecione **[!UICONTROL Delivery]** no painel direito.

![A tela do construtor de regras mostra um exemplo de público-alvo que pode ter enriquecimentos. O botão Delivery também é destacado.](/help/segmentation/images/ui/composition-enhancements/view-delivery.png)

Escolha a matriz de objetos que deseja usar para enriquecimento na lista do painel esquerdo. Se houver apenas uma matriz no perfil, a matriz será selecionada automaticamente para você. Selecione **[!UICONTROL Save]** para retornar à composição do público-alvo.

<!-- , as well as the fields you want to be used in the enrichment. -->

![A árvore de esquema da árvore de enriquecimento é exibida.](/help/segmentation/images/ui/composition-enhancements/view-schema-tree.png)

Na composição de público-alvo, o bloco [!UICONTROL Audience] agora é do tipo &quot;[!UICONTROL Rule builder with enhancement]&quot;. Selecione **[!UICONTROL Publish]** para ativar seu público-alvo com o próximo lote diário.

![O bloco Público-alvo está realçado, mostrando que um público-alvo com enriquecimento foi adicionado.](/help/segmentation/images/ui/composition-enhancements/rule-builder-with-enrichment.png)

### Detalhes de comportamento e medidas de proteção

Lembre-se dos seguintes detalhes e medidas de proteção ao usar o enriquecimento de público-alvo:

- Você só pode usar o enriquecimento de público-alvo em públicos-alvo criados na Composição de público-alvo
- O primeiro bloco usado na composição **deve** ser uma audiência baseada em regras.
- Você **não pode** usar quaisquer outras operações dentro da composição.
- Depois de publicado, você **não pode** editar a composição no público-alvo baseado em regras.
   - Você *pode* copiar a composição em um rascunho e editar esse rascunho se desejar fazer alterações na composição base ou no público-alvo com base em regras.
- Somente uma matriz de objetos **one** pode ser usada para gerar a carga de enriquecimento em um único público-alvo
   - A matriz de carga pode ser aninhada em um objeto (até sete camadas no esquema de perfil), mas **não pode** estar contido em outra matriz.
   - A matriz de carga **deve** ter 50 linhas ou menos.
   - Todas as colunas de saída na carga **devem** ser de um tipo primitivo.
   - Somente as primeiras **vinte** colunas da matriz são geradas.
- Apenas **dez** composições de público-alvo estão disponíveis para uso no momento

## Ativação mais rápida {#faster-activation}

Ativação mais rápida permite ativar o público-alvo para um destino downstream imediatamente após a avaliação da composição. Como resultado, se o destino estiver definido para ativação após a avaliação do segmento, não será mais necessário aguardar 24 horas para que o trabalho de avaliação seja concluído.

Para obter mais informações, leia o [guia de ativação de públicos-alvo para destinos de perfis em lote](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files).
