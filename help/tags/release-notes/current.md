---
title: Notas de versão
description: As notas de versão mais recentes para tags no Adobe Experience Platform.
source-git-commit: 7a6bec77895458cf1735bc7a00d16b78df9776a5
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 67%

---

# Notas de versão

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

## 17 de maio de 2021

**Melhor tratamento das alterações não salvas** — sempre que você saía de uma exibição de configurações (extensões, elementos de dados e componentes de regras), recebia um aviso sobre se queria descartar as alterações. Porém, a lógica para determinar isso não era boa. Então, na maioria das vezes, você era solicitado a salvar mudanças, mesmo que não houvesse nenhuma. Isso foi corrigido. A partir de agora, você só deverá ver esse aviso quando tiver feito realmente alterações.

## 10 de maio de 2021

**Publicação simplificada** — a criação no ambiente de preparo não é mais necessária. Se você tiver os direitos apropriados, ignore totalmente o estado Enviado e publique diretamente do Desenvolvimento, desde que tenha tido uma criação bem-sucedida e não haja outras bibliotecas upstream

## 22 de abril de 2021

**Coleta de dados no Adobe Experience Platform**  - O envio de dados para o Adobe não é apenas sobre a implantação de tags no site ou a configuração no aplicativo.  O uso dos SDKs do Experience Platform e da Edge Network requer acesso a outros recursos da plataforma. Isso costumava exigir o logon em algumas ferramentas diferentes, mas agora elas estão reunidas em um único lugar.

A Coleta de dados na plataforma consiste em seis recursos, e a navegação recém-simplificada conterá apenas os itens aos quais sua empresa e conta de usuário têm acesso.  Alguns dos recursos também foram atualizados para corresponder aos padrões de nomenclatura do Experience Platform.

* Cliente (acessado anteriormente como lado do cliente)
* Datastreams (acessados anteriormente como configurações de borda)
* Servidor (acessado anteriormente como lado do servidor)
* Configurações do aplicativo
* Esquemas
* Identidades

Aguarde mais atualizações à medida que o Experience Platform e a Coleção de dados continuarem a evoluir.

## 18 de fevereiro de 2021

* Atualização da interface do usuário da coleta de dados para o espectro de reação v3
* Placas de extensão atualizadas para os padrões mais recentes do Spectrum
* Aumento do tamanho dos campos de nome em todo o aplicativo

## 13 de janeiro de 2021

**Disponibilidade geral: Encaminhamento** de eventosEnvie dados a nível de evento para o Adobe Experience Platform Edge, em seguida, use o encaminhamento de eventos para transformar, enriquecer e enviar esses dados para um endpoint que não seja o Adobe usando servidores Adobe Network, não o cliente, com baixa latência.

Consulte a [visão geral do encaminhamento de eventos](../ui/event-forwarding/overview.md) e o [guia de introdução](../ui/event-forwarding/getting-started.md) para obter mais informações.
