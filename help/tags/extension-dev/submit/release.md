---
title: Lançar uma extensão
description: Saiba como lançar de forma privada ou pública uma extensão de tag no Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 58%

---

# Lançar uma extensão

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Quando os testes e a documentação estiverem concluídos, a extensão estará pronta para ser lançada. Atualmente, existem dois tipos de lançamentos que podem ser executados:

- **Lançamento privado**: a extensão concluída está disponível para todas as propriedades na sua empresa, mas não está disponível para outras empresas no Adobe Experience Platform.
- **Versão** pública: A extensão concluída está disponível no mercado público para todos os usuários do Adobe Experience Platform.

>[!NOTE]
>
>Depois de liberar sua extensão, não é mais possível fazer alterações nela e não é possível cancelar a liberação.  Depois de lançada, as correções de erros e as adições de recursos são realizadas `POST` adicionando uma nova versão do pacote de extensão e seguindo as etapas de teste e versão acima nessa nova versão.

Você deve lançar sua extensão como uma extensão privada antes de lançá-la publicamente.

## Lançamento privado

A maneira mais fácil de liberar sua extensão com disponibilidade privada é usar o [liberador de extensão de tag](https://www.npmjs.com/package/@adobe/reactor-releaser). Mais instruções estão disponíveis na documentação.

Se quiser liberar sua extensão com disponibilidade privada usando a API diretamente, consulte o exemplo de chamada para [liberar privadamente um pacote de extensão](https://developer.adobelaunch.com/api/reference/1.0/extension_packages/release_private/) nos documentos da API para obter mais detalhes.

## Lançamento público

Depois de concluir o lançamento privado, peça à Adobe para lançá-lo publicamente. Isso tornará sua extensão disponível no catálogo público. Qualquer usuário da coleta de dados pode instalar sua extensão em qualquer propriedade.

Preencha o [formulário de solicitação de lançamento público](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=7DRB5U) para iniciar o processo de lançamento.
