---
title: Solicitação de carimbo de data e hora do cliente
description: Saiba como adicionar a ordem de carimbo de data e hora do cliente aos seus conjuntos de dados para garantir a consistência nos dados do perfil.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 1cd9f0b5-6334-4815-860a-78596a9cea1a
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Solicitação de carimbo de data e hora do cliente

No Adobe Experience Platform, a ordem dos dados não é garantida por padrão ao assimilar dados por meio da assimilação de streaming na loja de perfis. Com a solicitação de carimbo de data e hora do cliente, você pode garantir que a mensagem mais recente, de acordo com o carimbo de data e hora fornecido pelo cliente, será retida na loja de perfis. Todas as mensagens obsoletas serão descartadas e **não** estarão disponíveis para uso em serviços downstream que usam dados de perfil, como segmentação e destinos. Como resultado, permite que os dados de perfil sejam consistentes e permite que os dados de perfil permaneçam sincronizados com os sistemas de origem.

Para habilitar a solicitação do carimbo de data e hora do cliente, use o campo `extSourceSystemAudit.lastUpdatedDate` no [grupo de campos Atributos de Auditoria do Sistema Externo da Source](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.md) e entre em contato com o Gerente Técnico de Conta do Adobe ou com o Atendimento ao Cliente do Adobe com as informações da sandbox e do conjunto de dados.

## Restrições

Durante esse beta privado, as seguintes restrições se aplicam ao usar a solicitação de carimbo de data e hora do cliente:

- Você só pode usar a ordenação do carimbo de data e hora do cliente com **atributos de perfil** assimilados com **assimilação por transmissão** no armazenamento de perfil.
   - Há **não** garantias de pedidos fornecidas para dados no data lake ou no Serviço de identidade.
- Você só pode usar a solicitação de carimbo de data e hora do cliente em **sandboxes de não produção**.
- Você só pode aplicar a solicitação de carimbo de data e hora do cliente a **5** conjuntos de dados por sandbox.
- Você **não pode** usar upserts de transmissão para enviar atualizações parciais de linhas em um conjunto de dados que tenha a ordenação de carimbo de data/hora do cliente habilitada.
- O campo `extSourceSystemAudit.lastUpdatedDate` **deve** estar no formato [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html). Ao usar o formato ISO 8601, ele **deve** ser um datetime completo no formato `yyyy-MM-ddTHH:mm:ss.sssZ` (por exemplo, `2028-11-13T15:06:49.001Z`).
- Todas as linhas de dados assimilados **devem** conter o campo `extSourceSystemAudit.lastUpdatedDate` como um grupo de campos de nível superior. Isso significa que este campo **deve** não deve ser aninhado dentro do esquema XDM. Se este campo estiver ausente ou em um formato incorreto, o registro malformado **não** será assimilado e uma mensagem de erro correspondente será enviada.
- Qualquer conjunto de dados habilitado para ordenação de carimbo de data/hora do cliente **deve** ser um novo conjunto de dados sem dados assimilados anteriormente.
- Para qualquer fragmento de perfil fornecido, somente as linhas que contêm um `extSourceSystemAudit.lastUpdatedDate` mais recente serão assimiladas. As linhas que contêm um `extSourceSystemAudit.lastUpdatedDate` mais antigo ou com a mesma idade serão descartadas.

## Recomendações

Ao implementar a solicitação de carimbo de data e hora do cliente, lembre-se das seguintes considerações:

- Você é responsável por sincronizar os relógios em todos os sistemas internos que enviam dados para o armazenamento de Perfil.
- Você deve ter precisão de nível de milissegundo em seus carimbos de data e hora formatados em ISO 8061.
