---
title: 'Notas de versão do Adobe Experience Platform '
description: Notas de versão da Experience Platform em 11 de dezembro de 2019
doc-type: release notes
last-update: December 12, 2019
author: ens71067
translation-type: tm+mt
source-git-commit: 2f0f155beacbc6a4ba2892ae211a9c0305e969ac

---


# Notas de versão da Adobe Experience Platform

## Data de lançamento: 11 de dezembro de 2019

## Serviço de segmentação

O Adobe Experience Platform Segmentation Service fornece uma interface de usuário e uma RESTful API que permite criar segmentos e gerar audiências a partir dos dados do Perfil do cliente em tempo real. Esses segmentos são configurados e mantidos centralmente na Plataforma, tornando-os facilmente acessíveis por qualquer aplicativo da Adobe.

O Serviço de segmentação define um subconjunto específico de perfis ao descrever os critérios que distinguem um grupo comercializável de pessoas dentro da sua base de clientes. Os segmentos podem se basear em dados de registro (como informações demográficas) ou em eventos de séries cronológicas que representem as interações do cliente com sua marca.

### Novos recursos

| Recurso | Descrição |
|--- | ---|
| Guia Audiências mescladas no Construtor de segmentos | As guias _Segmentos_ e _Audiências_ no Construtor de segmentos foram combinadas em uma única guia _Audiência_ . Essa guia permite que você procure e procure audiências existentes, que podem ser arrastadas e soltas na tela do construtor de regras para criar uma nova definição de segmento. A referência a uma audiência pode adicionar um dos seguintes conjuntos de lógica de regra à nova definição de segmento: associação de Audiência como uma regra, o conjunto completo de lógicas de regra que definiram a audiência referenciada. |
| Novo local para o seletor de política de mesclagem | O local do seletor de política de mesclagem no Construtor de segmentos foi alterado. Para selecionar uma política de mesclagem para uma definição de segmento, clique no ícone de engrenagem na guia _Campos_ e use o menu suspenso Política _de_ mesclagem para selecionar a política de mesclagem que deseja usar. |

### Problemas conhecidos

* Nenhum

Para obter mais informações, consulte a visão geral [do Serviço de](../../segmentation/home.md)segmentação.

## Serviço de tomada de decisão

O Adobe Experience Platform Decisioning Service fornece a capacidade de selecionar de forma programática e inteligente a &quot;Próxima melhor experiência&quot; de um conjunto de opções disponíveis para um determinado indivíduo, entregá-las a qualquer canal ou aplicativo e executar relatórios e análise.

### Novos recursos

| Recurso | Descrição |
| -----------| ---------- |
| Funções de classificação | A ordem das ofertas para perfis agora é derivada por meio de uma função de classificação, em vez de um conjunto fixo de ofertas em todos os perfis. |

### Problemas conhecidos

* Nenhum.

Consulte a visão geral [do serviço de](../../decisioning-service/home.md) decisão para obter uma introdução completa ao serviço.

## Fontes

A plataforma Adobe Experience pode assimilar dados de fontes externas, permitindo que você estruture, rotule e aprimore esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como Adobe Solutions, armazenamento baseado em nuvem, software de terceiros e sistema CRM.

A plataforma Experience fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem que você se autentique em seus sistemas de armazenamentos e serviços CRM, defina horários para execuções de ingestão e gerencie a throughput de ingestão de dados.

### Novos recursos

| Recurso | Descrição |
| ---------- | ------------ |
| Conexão de transmissão | A assimilação de streaming permite enviar dados de dispositivos do cliente e do servidor para a plataforma Experience em tempo real. A versão inclui uma nova interface de usuário de conexão de streaming. |
| Suporte a conector para Google Cloud Store | Suporte para coletar dados da Google Cloud Store. |

### Problemas conhecidos

* Nenhum.

Para obter mais informações sobre fontes, consulte a visão geral [das](../../sources/home.md)fontes.

## Sistema do Experience Data Model (XDM)

A normalização e a interoperabilidade são conceitos-chave por trás da plataforma da experiência. O Experience Data Model (XDM), desenvolvido pela Adobe, é um esforço para padronizar os dados de experiência do cliente e definir schemas para o gerenciamento da experiência do cliente.

A XDM é uma especificação publicamente documentada projetada para melhorar o poder das experiências digitais. Fornece estruturas e definições comuns para qualquer aplicativo que se comunique com os serviços na Adobe Experience Platform. Ao aderir aos padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum, fornecendo insights de forma mais rápida e integrada. Você pode obter informações importantes das ações do cliente, definir audiências do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

### Novos recursos

| Recurso | Descrição |
|--- | ---|
| Validação de schemas aprimorada | Novas verificações para garantir que as referências sejam resolvidas em campos adicionais, conforme esperado. Adicionadas verificações adicionais aos campos definidos como uma matriz de objetos para garantir que os objetos estejam totalmente definidos. Mensagens de erro aprimoradas para ajudar a identificar e corrigir problemas. |

### Correções de erros

* Manutenção e melhorias relacionadas ao controle de acesso e às caixas de proteção.
* Suporte para `eTag` o `/descriptors` endpoint na API do Registro do Schema.

### Problemas conhecidos

* Nenhum

Para saber mais sobre como trabalhar com o XDM usando a API do Registro do Schema e a interface do usuário do Editor de Schemas, leia a documentação [do Sistema](../../xdm/home.md)XDM.