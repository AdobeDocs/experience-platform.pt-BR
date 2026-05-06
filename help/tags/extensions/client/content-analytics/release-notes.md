---
title: Notas de versão da extensão do Adobe Content Analytics
description: As notas de versão mais recentes da extensão de tag da Content Analytics na Adobe Experience Platform.
exl-id: 37b34915-655b-40de-b17b-43028c579e37
source-git-commit: 057d1ad8d61ed386a777175026a3f01f21541389
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 2%

---

# Notas de versão da extensão do Adobe Content Analytics

Veja a seguir uma lista das notas de versão da extensão de tag do Content Analytics.

| Versão | Data | Correções |
|---|---|---|
| 1.0.52 | 27 de abril de 2026 | <ul><li>Adição de rastreamento para ativos em que o CSS carrega imagens no fundo de um elemento no DOM.</li><li>Adicionada uma matriz `permanentlyBlockedURLs` embutida em código contendo [maps.googleapis.com](https://maps.googleapis.com) e [mapsresources-pa.googleapis.com](https://mapsresources-pa.googleapis.com). Esses URLs são sempre bloqueados por padrão na biblioteca do Content Analytics.</li><li>Adição dos campos `idSource` e `channel` às solicitações de coleta de dados XDM.</li></ul> |
| 1.0.51 | 13 de março de 2026 | <ul><li>Correção de um pequeno erro que fazia com que `experienceIDs` fosse armazenado em cache ao navegar entre páginas.</li><li>Correção de um problema com a captura de parâmetros da string de consulta da experiência. Os parâmetros de query funcionam da seguinte maneira:<ul><li>O campo Query parameters está vazio: nenhum parâmetro de sequência de consulta é capturado na ID da experiência.</li><li>Os parâmetros de consulta são definidos explicitamente (por exemplo, um, dois, três): somente esses parâmetros e valores de sequência de consulta são capturados na ID da experiência.</li><li>O parâmetro de consulta está definido como curinga (`.*`): a cadeia de caracteres document.location.search inteira está incluída na URL.</li></ul></li></ul> |
| 1.0.49 | 12 de setembro de 2025 | <ul><li>Correção de um pequeno erro que resultava na não carga da interface da extensão de tags se o usuário não tivesse permissões de sequência de dados. A interface agora exibirá um aviso de permissão na opção de sequência de dados **[!UICONTROL Choose from list]** e ainda permitirá que o usuário insira valores manualmente.</li><li>Atualização de um problema de caminho para l10n.</li><li>Correção de um problema em que algumas imagens que eram elementos secundários de pais sem imagem não capturavam corretamente cliques em ativos para esses elementos de imagem secundários.</li><li>Se um usuário tiver o WebSDK configurado em tags com um nome de instância diferente de `alloy`, a biblioteca Content Analytics detectará a primeira instância da biblioteca do WebSDK e a usará para enviar eventos Content Analytics.</li></ul> |
| 1.0.48 | 25 de agosto de 2025 | <ul><li>Adiciona suporte para rastrear ativos nos elementos DOM de raiz-sombra de um documento.</li></ul> |
| 1.0.47 | 23 de julho de 2025 | <ul><li>Correção de um bug que ocorria quando as experiências não estavam ativadas, causando falha na verificação da expressão regular para as experiências. Esse problema impedia que os dados do Content Analytics fossem coletados.</li><li>Correção de um problema com a configuração de idioma padrão que impedia a exibição da interface do usuário de tags para alguns usuários que não tinham o idioma padrão principal definido no Experience Cloud.</li></ul> |
| 1.0.46 | 18 de junho de 2025 | <ul><li>Adição de uma notificação em caixa de informações ao tentar salvar a configuração da extensão, se uma sequência de dados de produção não estiver presente.</li><li>Correção temporária do problema de visibilidade da carga do Content Analytics, colocando o conteúdo de carga restrito no console.</li><li>Adição de suporte à localização na interface do usuário da extensão.</li><li>Correção parcial de um problema de CSS que causava o preenchimento extra ao redor do conteúdo da interface do usuário da extensão.</li></ul> |
| 1.0.45 | 14 de abril de 2025 | <ul><li>Foram solucionados vários bugs nas definições de configuração relacionados à retenção de eventos do Content Analytics enquanto aguardavam eventos de exibição de página. Por padrão, o Content Analytics aguardará para acionar eventos até que o PRIMEIRO evento de exibição de página ocorra.</li></ul> |
| 1.0.44 | 31 de março de 2025 | <ul><li>Primeira iteração da integração do AppMeasurement.</li><li>Esta versão ainda não oferece suporte à filtragem de solicitações específicas (por exemplo, exibições de página), mas essa funcionalidade pode ser adicionada em uma atualização futura. Atualmente, ele usa a primeira instância do AppMeasurement encontrada na página.</li></ul> |
| 1.0.43 | 10 de março de 2025 | <ul><li>Versão inicial da extensão.</li></ul> |
