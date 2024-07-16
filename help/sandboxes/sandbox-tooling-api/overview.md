---
title: Guia da API de ferramentas de sandbox
description: As ferramentas de sandbox no Adobe Experience Platform permitem exportar e importar um instantâneo das configurações de sandbox entre as sandboxes.
exl-id: 4bcc095b-5db1-4824-8b7c-c2ea5a393b98
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 3%

---

# Guia da API de ferramentas do [!DNL Sandbox]

A API de ferramentas do [!DNL Sandbox] fornece vários endpoints que permitem exportar e importar instantâneos entre sandboxes disponíveis para você em sua organização. Todas as interações ocorrem por meio de endpoints HTTP. A sandbox de origem é verificada em busca de artefatos, que são os objetos contidos em um pacote, antes de exportar um instantâneo. Quando uma solicitação de importação é feita, um instantâneo [!DNL Azure Blob] é obtido e utilizado como modelo para produzir artefatos quase semelhantes para a sandbox de destino. Consulte a documentação [ferramenta de sandbox](../ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling) para obter uma lista de objetos e limitações compatíveis.

Esses endpoints são descritos abaixo. Visite os manuais de endpoint individuais para obter detalhes e consulte o [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, como ler chamadas de API de exemplo e muito mais.

## Pacotes {#packages}

O endpoint dos pacotes de ferramentas de sandbox permite gerenciar pacotes. O pacote de ferramentas da sandbox é uma coleção de definições de artefatos, incluindo a ID do pacote, o nome, a descrição, a ID da organização e a ID do criador. Consulte o [manual de endpoint de pacotes](./packages.md) para obter mais informações sobre como trabalhar com pacotes na API.

## Ferramentas {#tools}

O ponto de extremidade das ferramentas de ferramentas de sandbox permite buscar independentemente os dados JSON do trabalho. Consulte o [manual de endpoint de ferramentas](./tools.md) para obter mais informações sobre como recuperar dados JSON do trabalho na API.

## Próximas etapas {#next-steps}

Para começar a fazer chamadas usando a API de ferramentas de sandbox, leia o [guia de introdução](./getting-started.md) e selecione um dos manuais de endpoint para saber como usar endpoints específicos.
