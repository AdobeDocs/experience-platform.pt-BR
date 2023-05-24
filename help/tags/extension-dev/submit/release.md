---
title: Lançar uma extensão
description: Saiba como lançar de forma privada ou pública uma extensão de tag na Adobe Experience Platform.
exl-id: a5eb6902-4b0f-4717-a431-a290c50fb5a6
source-git-commit: 60d88be5d710314cdc6900f4b63643c740b91fa6
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 92%

---

# Lançar uma extensão

>[!NOTE]
>
>O Adobe Experience Platform Launch foi reformulado como um conjunto de tecnologias de coleção de dados na Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Quando os testes e a documentação estiverem concluídos, a extensão estará pronta para ser lançada. Atualmente, existem dois tipos de lançamentos que podem ser executados:

- **Lançamento privado**: a extensão concluída está disponível para todas as propriedades na sua empresa, mas não está disponível para outras empresas no Adobe Experience Platform.
- **Lançamento público**: a extensão concluída está disponível no marketplace público para todos os usuários da Adobe Experience Platform.

>[!NOTE]
>
>Depois de lançar sua extensão, você não poderá mais fazer alterações nela e não poderá cancelar o lançamento.  Depois de lançada, as correções de erros e as adições de recursos são realizadas `POST`adicionando uma nova versão do pacote de extensão e seguindo as etapas de teste e versão acima nessa nova versão.

Você deve lançar sua extensão como uma extensão privada antes de lançá-la publicamente.

## Lançamento privado

A maneira mais fácil de lançar sua extensão com disponibilidade privada é usar o [lançador de extensão de tag](https://www.npmjs.com/package/@adobe/reactor-releaser). Mais instruções estão disponíveis na documentação.

Se quiser lançar sua extensão com disponibilidade privada usando a API diretamente, veja o exemplo de chamada para [lançar de forma privada um pacote de extensão](../../api/endpoints/extension-packages.md/#private-release) na documentação da API para obter mais detalhes.

## Lançamento público

Depois de concluir o lançamento privado, peça à Adobe para lançá-lo publicamente. Isso tornará sua extensão disponível no catálogo público. Qualquer usuário da coleção de dados pode instalar sua extensão em qualquer propriedade.

Preencha o [formulário de solicitação de lançamento público](https://www.feedbackprogram.adobe.com/c/r/DCExtensionReleaseRequest) para iniciar o processo de lançamento.
