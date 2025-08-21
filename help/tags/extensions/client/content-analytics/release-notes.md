---
title: Notas de versão da extensão do Adobe Content Analytics
description: As notas de versão mais recentes da extensão de tag da Content Analytics na Adobe Experience Platform.
exl-id: 37b34915-655b-40de-b17b-43028c579e37
source-git-commit: 9fad0b092263c08a2744023b08f5f353f2c85422
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 1%

---

# Notas de versão da extensão do Adobe Content Analytics

Veja a seguir uma lista das notas de versão da extensão de tag do Content Analytics.

| Versão | Data | Correções |
|---|---|---|
| 1.0.47 | 23 de julho de 2025 | <ul><li>Correção de um bug que ocorria quando as experiências não estavam ativadas, causando falha na verificação da expressão regular para as experiências. Esse problema impedia que os dados do Content Analytics fossem coletados.</li><li>Correção de um problema com a configuração de idioma padrão que impedia a exibição da interface do usuário de tags para alguns usuários que não tinham o idioma padrão principal definido no Experience Cloud.</li></ul> |
| 1.0.46 | 18 de junho de 2025 | <ul><li>Adição de uma notificação em caixa de informações ao tentar salvar a configuração da extensão, se uma sequência de dados de produção não estiver presente.</li><li>Correção temporária do problema de visibilidade da carga do Content Analytics, colocando o conteúdo de carga restrito no console.</li><li>Adição de suporte à localização na interface do usuário da extensão.</li><li>Correção parcial de um problema de CSS que causava o preenchimento extra ao redor do conteúdo da interface do usuário da extensão.</li></ul> |
| 1.0.45 | 14 de abril de 2025 | <ul><li>Foram solucionados vários bugs nas definições de configuração relacionados à retenção de eventos do Content Analytics enquanto aguardavam eventos de exibição de página. Por padrão, o Content Analytics aguardará para acionar eventos até que o PRIMEIRO evento de exibição de página ocorra.</li></ul> |
| 1.0.44 | 31 de março de 2025 | <ul><li>Primeira iteração da integração do AppMeasurement.</li><li>Esta versão ainda não oferece suporte à filtragem de solicitações específicas (por exemplo, exibições de página), mas essa funcionalidade pode ser adicionada em uma atualização futura. Atualmente, ele usa a primeira instância do AppMeasurement encontrada na página.</li></ul> |
| 1.0.43 | 10 de março de 2025 | <ul><li>Versão inicial da extensão.</li></ul> |
