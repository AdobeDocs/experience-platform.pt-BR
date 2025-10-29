---
title: Lançar uma extensão
description: Saiba como lançar de forma privada ou pública uma extensão de tag na Adobe Experience Platform.
exl-id: a5eb6902-4b0f-4717-a431-a290c50fb5a6
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 64%

---

# Lançar uma extensão

>[!NOTE]
>
>O Adobe Experience Platform Launch foi reformulado como um conjunto de tecnologias de coleta de dados na Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Quando os testes e a documentação estiverem concluídos, a extensão estará pronta para ser lançada. Atualmente, existem dois tipos de lançamentos que podem ser executados:

- **Lançamento privado**: a extensão concluída está disponível para todas as propriedades na sua empresa, mas não está disponível para outras empresas no Adobe Experience Platform.
- **Lançamento público**: a extensão concluída está disponível no marketplace público para todos os usuários da Adobe Experience Platform.

>[!NOTE]
>
>Depois de lançar sua extensão, você não poderá mais fazer alterações nela e não poderá cancelar o lançamento.  Depois de lançada, as correções de erros e as adições de recursos são realizadas `POST`adicionando uma nova versão do pacote de extensão e seguindo as etapas de teste e versão acima nessa nova versão.

Primeiro, você deve lançar sua extensão como uma extensão privada antes que ela possa ser lançada publicamente.

## Lançamento privado

A maneira mais fácil de lançar sua extensão com disponibilidade privada é usar o [lançador de extensão de tag](https://www.npmjs.com/package/@adobe/reactor-releaser).

```bash
npx @adobe/reactor-releaser
```

`npx` permite baixar e executar um pacote npm sem instalá-lo na sua máquina. Essa é a maneira mais simples de executar o lançador.

>[!NOTE]
> Por padrão, o lançador espera as credenciais do Adobe I/O para um fluxo Oauth de servidor para servidor. As credenciais `jwt-auth` herdadas
> > O pode ser usado executando o `npx @adobe/reactor-releaser@v3.1.3` até a desativação em 1º de janeiro de 2025. Os parâmetros necessários
> > para executar a versão `jwt-auth` pode ser encontrado [aqui](https://github.com/adobe/reactor-releaser/tree/9ea66aa2c683fe7da0cca50ff5c9b9372f183bb5).

O lançador requer que você insira apenas algumas informações. Os `clientId` e `clientSecret` podem ser recuperados do console do Adobe I/O. Navegue até a [página Integrações](https://console.adobe.io/integrations) no console do I/O. Selecione a organização correta na lista suspensa, localize a integração apropriada e selecione **[!UICONTROL View]**.

- Qual é o seu `clientId`? Copie e cole isso do Console do I/O.
- Qual é o seu `clientSecret`? Copie e cole isso do Console do I/O.

O lançador lerá os campos `name` e `platform` do manifesto da extensão e consultará a API para obter um pacote de extensão correspondente na disponibilidade de desenvolvimento.
O lançador solicitará que você confirme se encontrou o pacote de extensão correto que deseja liberar para disponibilidade privada.

Se quiser lançar sua extensão com disponibilidade privada usando a API diretamente, veja o exemplo de chamada para [lançar de forma privada um pacote de extensão](/help/tags/api/endpoints/extension-packages.md#private-release) na documentação da API para obter mais detalhes.

## Lançamento público

Depois de concluir o lançamento privado, peça à Adobe para lançá-lo publicamente. Isso tornará sua extensão disponível no catálogo público. Qualquer usuário da coleção de dados pode instalar sua extensão em qualquer propriedade.

Preencha o [formulário de solicitação de lançamento público](https://www.feedbackprogram.adobe.com/c/r/DCExtensionReleaseRequest) para iniciar o processo de lançamento.
