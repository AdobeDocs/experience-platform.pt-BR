---
title: Notas de versão da Adobe Experience Platform
description: Notas de versão da Experience Platform 11 de dezembro de 2019
doc-type: release notes
last-update: December 12, 2019
author: ens71067
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 7%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 11 de dezembro de 2019**

Atualizações dos recursos existentes na Adobe Experience Platform:

* [[!DNL Segmentation Service]](#segmentation)
* [[!DNL Decisioning Service]](#decisioning)
* [[!DNL Sources]](#sources)
* [[!DNL Experience Data Model (XDM) System]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

O Serviço de segmentação da Adobe Experience Platform fornece uma interface de usuário e uma RESTful API que permite criar segmentos e gerar públicos a partir dos dados [!DNL Real-time Customer Profile]. Esses segmentos são configurados e mantidos centralmente em [!DNL Platform], tornando-os acessíveis a qualquer aplicativo da Adobe.

[!DNL Segmentation Service] O define um subconjunto específico de perfis ao descrever os critérios que distinguem um grupo comercializável de pessoas dentro da base do cliente. Os segmentos podem se basear em dados de registro (como informações demográficas) ou em eventos de séries cronológicas que representem as interações do cliente com sua marca.

**Novos recursos**

| Recurso | Descrição |
|--- | ---|
| Guia Públicos-alvo mesclados em [!DNL Segment Builder] | As guias [!UICONTROL Segmentos] e [!UICONTROL Públicos-alvo] no [!DNL Segment Builder] foram combinadas em uma única guia [!UICONTROL Públicos-alvo]. Essa guia permite procurar e procurar públicos-alvo existentes, que você pode arrastar e soltar na tela do construtor de regras para criar uma nova definição de segmento. Referenciar um público-alvo pode adicionar um dos seguintes conjuntos de lógica de regra à nova definição de segmento: Associação de público-alvo como uma regra, o conjunto completo de lógicas de regra que definiu o público-alvo referenciado. |
| Novo local para o seletor de política de mesclagem | A localização do seletor de política de mesclagem no [!DNL Segment Builder] foi alterada. Para selecionar uma política de mesclagem para uma definição de segmento, selecione o ícone de engrenagem na guia **[!UICONTROL Fields]** e use o menu suspenso **[!UICONTROL Merge Policy]** para selecionar a política de mesclagem que deseja usar. |

**Problemas conhecidos**

* None

Para obter mais informações, consulte a [Visão geral do serviço de segmentação](../../segmentation/home.md).

## [!DNL Decisioning Service] {#decisioning}

A Adobe Experience Platform [!DNL Decisioning Service] fornece a capacidade de selecionar de forma programática e inteligente &quot;Próxima melhor experiência&quot; de um conjunto de opções disponíveis para um determinado indivíduo, entregá-las a qualquer canal ou aplicativo e executar relatórios e análises.

**Novos recursos**

| Recurso | Descrição |
| -----------| ---------- |
| Funções de classificação | A ordem de ofertas para perfis agora é derivada de uma função de classificação, em vez de um conjunto fixo de ofertas em todos os perfis. |

**Problemas conhecidos**

* None.

## [!DNL Sources] {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas, permitindo estruturar, rotular e aprimorar esses dados usando serviços [!DNL Platform]. Você pode assimilar dados de várias fontes, como Soluções da Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

[!DNL Experience Platform] O fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar para seus sistemas de armazenamento e serviços de CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Novos recursos**

| Recurso | Descrição |
| ---------- | ------------ |
| Conexão de transmissão | A assimilação de streaming permite enviar dados de dispositivos cliente e servidor para [!DNL Experience Platform] em tempo real. A versão inclui uma nova interface de usuário de conexão de transmissão. |
| Suporte ao conector para [!DNL Google Cloud Store] | Suporte para coletar dados de [!DNL Google Cloud Store]. |

**Problemas conhecidos**

* Nenhum.

Para obter mais informações sobre fontes, consulte a [visão geral das fontes](../../sources/home.md).

## [!DNL Experience Data Model] Sistema (XDM)  {#xdm}

A normalização e a interoperabilidade são conceitos-chave subjacentes a [!DNL Experience Platform]. [!DNL Experience Data Model] O (XDM), impulsionado pela Adobe, é um esforço para padronizar os dados de experiência do cliente e definir esquemas para o gerenciamento da experiência do cliente.

O XDM é uma especificação publicamente documentada projetada para melhorar o poder das experiências digitais. Fornece estruturas e definições comuns para qualquer aplicativo se comunicar com serviços na Adobe Experience Platform. Ao seguir os padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum, fornecendo insights de forma mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Novos recursos**

| Recurso | Descrição |
|--- | ---|
| Validação de esquema aprimorada | Novas verificações para garantir que as referências sejam resolvidas em campos adicionais, conforme esperado. Adicionadas verificações adicionais a campos definidos como uma matriz de objetos para garantir que os objetos sejam totalmente definidos. Mensagens de erro aprimoradas para ajudar a identificar e corrigir problemas. |

**Correções de erros**

* Manutenção e melhorias relacionadas ao controle de acesso e às sandboxes.
* Suporte para `eTag` para o terminal `/descriptors` na API [!DNL Schema Registry].

**Problemas conhecidos**

* Nenhum

Para saber mais sobre como trabalhar com o XDM usando a API [!DNL Schema Registry] e a interface do usuário [!DNL Schema Editor], leia a [documentação do Sistema XDM](../../xdm/home.md).