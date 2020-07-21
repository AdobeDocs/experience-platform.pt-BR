---
title: 'Notas de versão do Adobe Experience Platform '
description: Notas de versão de Experience Platform 11 de dezembro de 2019
doc-type: release notes
last-update: December 12, 2019
author: ens71067
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 5%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 11 de dezembro de 2019**

Atualizações dos recursos existentes no Adobe Experience Platform:

* [!DNL Segmentation Service](#segmentation)
* [!DNL Decisioning Service](#decisioning)
* [!DNL Sources](#sources)
* [!DNL Experience Data Model (XDM) System](#xdm)

## [!DNL Segmentation Service] {#segmentation}

O Serviço de segmentação de Adobe Experience Platform fornece uma interface de usuário e uma RESTful API que permite criar segmentos e gerar audiências a partir de seus [!DNL Real-time Customer Profile] dados. Esses segmentos são configurados e mantidos centralmente [!DNL Platform], tornando-os facilmente acessíveis por qualquer aplicativo da Adobe.

[!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo comercializável de pessoas dentro da sua base de clientes. Os segmentos podem se basear em dados de registro (como informações demográficas) ou em eventos de séries cronológicas que representem as interações do cliente com sua marca.

**Novos recursos**

| Recurso | Descrição |
|--- | ---|
| Guia Audiências mescladas em [!DNL Segment Builder] | As guias [!UICONTROL _Segmentos _]e[!UICONTROL _Audiências_] no [!DNL Segment Builder] foram combinadas em uma única guia [!UICONTROL _Audiência _]. Essa guia permite que você procure e procure audiências existentes, que podem ser arrastadas e soltas na tela do construtor de regras para criar uma nova definição de segmento. A referência a uma audiência pode adicionar um dos seguintes conjuntos de lógica de regra à nova definição de segmento: associação de Audiência como uma regra, o conjunto completo de lógicas de regra que definiram a audiência referenciada. |
| Novo local para o seletor de política de mesclagem | O local do seletor de política de mesclagem no [!DNL Segment Builder] foi alterado. Para selecionar uma política de mesclagem para uma definição de segmento, clique no ícone de engrenagem na guia [!UICONTROL _Campos _]e use o menu suspenso Política_[!UICONTROL  de]_ mesclagem para selecionar a política de mesclagem que deseja usar. |

**Problemas conhecidos**

* None

Para obter mais informações, consulte a visão geral [do Serviço de](../../segmentation/home.md)segmentação.

## [!DNL Decisioning Service] {#decisioning}

O Adobe Experience Platform [!DNL Decisioning Service] oferece a capacidade de selecionar de forma programática e inteligente a &quot;Próxima melhor experiência&quot; a partir de um conjunto de opções disponíveis para um determinado indivíduo, entregá-las a qualquer canal ou aplicativo e executar relatórios e análise.

**Novos recursos**

| Recurso | Descrição |
| -----------| ---------- |
| Funções de classificação | A ordem das ofertas para perfis agora é derivada por meio de uma função de classificação, em vez de um conjunto fixo de ofertas em todos os perfis. |

**Problemas conhecidos**

* None.

Consulte a visão geral [do serviço de](../../decisioning-service/home.md) decisão para obter uma introdução completa ao serviço.

## [!DNL Sources] {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas, permitindo que você estruture, rotule e aprimore esses dados usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como Adobe Solutions, armazenamento baseado em nuvem, software de terceiros e sistema CRM.

[!DNL Experience Platform] fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem que você se autentique em seus sistemas de armazenamentos e serviços CRM, defina horários para execuções de ingestão e gerencie a throughput de ingestão de dados.

**Novos recursos**

| Recurso | Descrição |
| ---------- | ------------ |
| Conexão de transmissão | A ingestão de streaming permite enviar dados de dispositivos do cliente e do servidor para [!DNL Experience Platform] em tempo real. A versão inclui uma nova interface de usuário de conexão de streaming. |
| Suporte de conector para [!DNL Google Cloud Store] | Suporte para a coleta de dados do [!DNL Google Cloud Store]. |

**Problemas conhecidos**

* None.

Para obter mais informações sobre fontes, consulte a visão geral [das](../../sources/home.md)fontes.

## [!DNL Experience Data Model] Sistema (XDM) {#xdm}

A normalização e a interoperabilidade são conceitos fundamentais subjacentes [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), desenvolvido pela Adobe, é um esforço para padronizar os dados de experiência do cliente e definir schemas para o gerenciamento da experiência do cliente.

A XDM é uma especificação publicamente documentada projetada para melhorar o poder das experiências digitais. Fornece estruturas e definições comuns para qualquer aplicativo que se comunique com os serviços no Adobe Experience Platform. Ao aderir aos padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum, fornecendo insights de forma mais rápida e integrada. Você pode obter informações importantes das ações do cliente, definir audiências do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Novos recursos**

| Recurso | Descrição |
|--- | ---|
| Validação de schemas aprimorada | Novas verificações para garantir que as referências sejam resolvidas em campos adicionais, conforme esperado. Adicionadas verificações adicionais aos campos definidos como uma matriz de objetos para garantir que os objetos estejam totalmente definidos. Mensagens de erro aprimoradas para ajudar a identificar e corrigir problemas. |

**Correções de erros**

* Manutenção e melhorias relacionadas ao controle de acesso e às caixas de proteção.
* Suporte para `eTag` o `/descriptors` endpoint na [!DNL Schema Registry] API.

**Problemas conhecidos**

* None

Para saber mais sobre como trabalhar com o XDM usando a [!DNL Schema Registry] API e a interface do [!DNL Schema Editor] usuário, leia a documentação [do Sistema](../../xdm/home.md)XDM.