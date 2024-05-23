---
title: Solicitação de carimbo de data e hora do cliente
description: Saiba como adicionar a ordem de carimbo de data e hora do cliente aos seus conjuntos de dados para garantir a consistência nos dados do perfil.
badgePrivateBeta: label="Beta privado" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: c5789b872be49c3bd4a1ca61a2d44392ebd4a746
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---


# Solicitação de carimbo de data e hora do cliente

No Adobe Experience Platform, a ordem dos dados não é garantida automaticamente ao assimilar dados por meio da assimilação de streaming na loja de perfis. Com a solicitação de carimbo de data e hora do cliente, você pode garantir que a mensagem mais recente, de acordo com o carimbo de data e hora fornecido pelo cliente, será retida na loja de perfis. Como resultado, permite que os dados de perfil sejam consistentes e permite que os dados de perfil permaneçam sincronizados com os sistemas de origem.

Para habilitar a solicitação do carimbo de data e hora do cliente, é necessário usar o `lastUpdatedDate` campo dentro do [Tipo de dados Atributos de auditoria do sistema de origem externa](../xdm/data-types/external-source-system-audit-attributes.md) e entre em contato com o Gerente técnico de conta do Adobe ou com o Atendimento ao cliente do Adobe com suas informações de sandbox e conjunto de dados.

## Restrições

Durante esse beta privado, as seguintes restrições se aplicam ao usar a solicitação de carimbo de data e hora do cliente:

- Você só pode usar a solicitação de carimbo de data e hora do cliente com **atributos de perfil** assimilado com **assimilação por transmissão**.
- Você só pode usar a solicitação de carimbo de data e hora do cliente em **não produção** sandboxes.
- Você só pode aplicar a solicitação de carimbo de data e hora do cliente a **5** conjuntos de dados por sandbox.
- A variável `lastUpdatedDate` o campo deve estar na [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) formato.
- Todas as linhas de dados assimiladas **deve** contém o `lastUpdatedDate` campo. Se esse campo estiver ausente ou em um formato incorreto, a assimilação falhará.
- Qualquer conjunto de dados habilitado para a solicitação de carimbo de data e hora do cliente **deve** ser um novo conjunto de dados sem dados assimilados anteriormente.
- Para qualquer fragmento de perfil específico, somente as linhas que contêm um `lastUpdatedDate` serão assimilados. Se a linha não contiver um atributo mais recente `lastUpdatedDate`, a linha será descartada.

## Recomendações

Ao implementar a solicitação de carimbo de data e hora do cliente, lembre-se das seguintes considerações:

- Você é responsável por sincronizar os relógios em todos os sistemas internos que enviam dados para o armazenamento de perfil.
- Você deve ter precisão de nível de milissegundo em seus carimbos de data e hora formatados em ISO 8061.
- O uso do Preparo de dados em coordenação com a solicitação de carimbo de data e hora do cliente é **altamente recomendado**, o cria uma cópia de todas as linhas assimiladas junto com seus carimbos de data e hora, o que permite uma melhor depuração caso surjam problemas.
