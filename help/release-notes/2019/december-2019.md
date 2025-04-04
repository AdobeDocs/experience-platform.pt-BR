---
title: Notas de versão da Adobe Experience Platform de dezembro de 2019
description: As notas de versão de dezembro de 2019 para Adobe Experience Platform.
doc-type: release notes
last-update: December 12, 2019
author: ens71067
exl-id: 98d50b90-38ed-4cc2-ad48-78b712b453f7
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 15%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 11 de dezembro de 2019**

Atualizações dos recursos já existentes na Adobe Experience Platform:

* [[!DNL Segmentation Service]](#segmentation)
* [[!DNL Decisioning Service]](#decisioning)
* [[!DNL Sources]](#sources)
* [[!DNL Experience Data Model (XDM) System]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

O Serviço de Segmentação da Adobe Experience Platform fornece uma interface de usuário e uma API RESTful que permite criar segmentos e gerar públicos a partir dos dados do [!DNL Real-Time Customer Profile]. Esses segmentos são configurados e mantidos centralmente no [!DNL Experience Platform], tornando-os prontamente acessíveis por qualquer aplicativo do Adobe.

O [!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo de pessoas na sua base de clientes que pode ser direcionado por campanhas de marketing. Os segmentos podem ser baseados em dados de registro (como informações demográficas) ou em eventos de séries temporais que representam interações de clientes com sua marca.

**Novos recursos**

| Recurso | Descrição |
|--- | ---|
| Guia Públicos mesclados em [!DNL Segment Builder] | As guias [!UICONTROL Segmentos] e [!UICONTROL Públicos-alvo] na [!DNL Segment Builder] foram combinadas em uma única guia [!UICONTROL Públicos-alvo]. Essa guia permite procurar e pesquisar públicos-alvo existentes, que você pode arrastar e soltar na tela do construtor de regras para criar uma nova definição de segmento. Fazer referência a um público-alvo pode adicionar um dos seguintes conjuntos de lógicas de regra à nova definição de segmento: Associação de público-alvo como uma regra, o conjunto completo de lógicas de regra que definiu o público-alvo referenciado. |
| Novo local para o seletor de política de mesclagem | O local do seletor de política de mesclagem em [!DNL Segment Builder] foi alterado. Para selecionar uma política de mesclagem para uma definição de segmento, selecione o ícone de engrenagem na guia **[!UICONTROL Campos]** e use o menu suspenso **[!UICONTROL Política de mesclagem]** para selecionar a política de mesclagem que deseja usar. |

**Problemas conhecidos**

* None

Para obter mais informações, consulte a [visão geral do Serviço de segmentação](../../segmentation/home.md).

## [!DNL Decisioning Service] {#decisioning}

O Adobe Experience Platform [!DNL Decisioning Service] permite selecionar de forma programática e inteligente a &quot;Próxima Melhor Experiência&quot; de um conjunto de opções disponíveis para um determinado indivíduo, entregá-las a qualquer canal ou aplicativo e executar relatórios e análises.

**Novos recursos**

| Recurso | Descrição |
| -----------| ---------- |
| Funções de classificação | A ordem das ofertas para perfis agora é derivada por meio de uma função de classificação, em vez de um conjunto fixo de ofertas em todos os perfis. |

**Problemas conhecidos**

* Nenhum.

## [!DNL Sources] {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir que você estruture, rotule e aprimore esses dados usando os serviços do [!DNL Experience Platform]. Você pode assimilar dados de várias fontes, como Soluções da Adobe, armazenamento na nuvem, software de terceiros e seu sistema de CRM.

O [!DNL Experience Platform] fornece uma API RESTful e uma interface do usuário interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem que você faça autenticação em seus sistemas de armazenamento e serviços CRM, defina tempos para execuções de assimilação e gerencie a taxa de transferência de assimilação de dados.

**Novos recursos**

| Recurso | Descrição |
| ---------- | ------------ |
| Conexão de transmissão | A assimilação de streaming permite enviar dados de dispositivos no lado do cliente e do servidor para o [!DNL Experience Platform] em tempo real. A versão inclui uma nova interface de usuário de conexão de streaming. |
| Suporte ao conector para [!DNL Google Cloud Store] | Suporte para coletar dados de [!DNL Google Cloud Store]. |

**Problemas conhecidos**

* Nenhum.

Para obter mais informações sobre origens, consulte a [visão geral das origens](../../sources/home.md).

## Sistema de [!DNL Experience Data Model] (XDM) {#xdm}

A padronização e a interoperabilidade são os principais conceitos por trás do [!DNL Experience Platform]. O [!DNL Experience Data Model] (XDM), orientado pela Adobe, é um esforço para padronizar os dados de experiência do cliente e definir esquemas para o gerenciamento da experiência do cliente.

O XDM é uma especificação documentada publicamente projetada para melhorar o potencial das experiências digitais. Ele fornece estruturas e definições comuns para que qualquer aplicativo se comunique com os serviços na Adobe Experience Platform. Seguindo os padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum, fornecendo insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

**Novos recursos**

| Recurso | Descrição |
|--- | ---|
| Validação de esquema aprimorada | Novas verificações para garantir que as referências sejam resolvidas em campos adicionais, conforme esperado. Adição de verificações adicionais em campos definidos como uma matriz de objetos para garantir que os objetos estejam totalmente definidos. Mensagens de erro aprimoradas para ajudar a identificar e corrigir problemas. |

**Correções de erros**

* Manutenção e melhorias relacionadas ao controle de acesso e sandboxes.
* Suporte para `eTag` para o ponto de extremidade `/descriptors` na API [!DNL Schema Registry].

**Problemas conhecidos**

* None

Para saber mais sobre como trabalhar com XDM usando a API [!DNL Schema Registry] e a interface de usuário [!DNL Schema Editor], leia a [documentação do Sistema XDM](../../xdm/home.md).
