---
title: Notas de versão da extensão do Adobe Content Analytics
description: As notas de versão mais recentes da extensão de tag da Content Analytics na Adobe Experience Platform.
source-git-commit: 24ff17af89bc882f08ec0f331ebae53b61f35d78
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 1%

---

# Notas de versão da extensão do Adobe Content Analytics

Veja a seguir uma lista das notas de versão da extensão de tag do Content Analytics.

| Versão | Data | Correções |
|---|---|---|
| <p>1.0.47</p> | <p>23 de julho de 2025</p> | <ul><li>Correção do bug encontrado por um cliente quando as experiências não estavam ativadas e a verificação de expressão regular para experiências estava falhando. Isso faz com que os dados do Content Analytics não sejam coletados.</li><li>Corrige o bug do idioma padrão que impedia a exibição da interface do usuário de tags para alguns usuários se eles não tivessem o idioma padrão principal definido na Experience Cloud.</li></ul> |
| <p>1.0.46</p> | <p>18 de junho de 2025</p> | <ul><li>Adiciona uma notificação em caixa de informações se uma sequência de dados de produção não estiver presente ao tentar salvar a configuração da extensão.</li><li>Corrige temporariamente a visibilidade da carga do Content Analytics, mas coloca o conteúdo restrito da carga do Content Analytics no console.</li><li>Adiciona localização à interface de usuário da extensão.</li><li>Correção parcial de um problema de CSS com preenchimento extra ao redor do conteúdo da interface do usuário de extensão.</li></ul> |
| <p>1.0.45</p> | <p>14 de abril de 2025</p> | <ul><li>Soluciona alguns bugs nas definições de configuração do ao reter eventos do Content Analytics ao aguardar eventos de exibição de página. Agora, o Content Analytics aguardará por padrão acionar eventos até que o PRIMEIRO evento de exibição de página ocorra.</li></ul> |
| <p>1.0.44</p> | <p>31 de março de 2025</p> | <ul><li>Primeira iteração da integração do AppMeasurement.</li><li>Esta versão não é compatível com a filtragem de solicitações específicas (por exemplo, exibições de página), mas pode ser adicionada em uma data posterior.  Também é usada a primeira instância do AppMeasurement encontrada na página.</li></ul> |
| <p>1.0.43</p> | <p>10 de março de 2025</p> | <ul><li>Versão inicial da extensão.</li></ul> |

