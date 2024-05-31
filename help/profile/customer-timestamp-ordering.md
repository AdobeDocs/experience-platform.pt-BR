---
title: Solicitação de carimbo de data e hora do cliente
description: Saiba como adicionar a ordem de carimbo de data e hora do cliente aos seus conjuntos de dados para garantir a consistência nos dados do perfil.
badgePrivateBeta: label="Beta privado" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: dffbdafc3f063906c8c8fb648ace59b2f1aedab8
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---


# Solicitação de carimbo de data e hora do cliente

No Adobe Experience Platform, a ordem dos dados não é garantida por padrão ao assimilar dados por meio da assimilação de streaming na loja de perfis. Com a solicitação de carimbo de data e hora do cliente, você pode garantir que a mensagem mais recente, de acordo com o carimbo de data e hora fornecido pelo cliente, será retida na loja de perfis. Todas as mensagens obsoletas serão descartadas e **não** estar disponíveis para uso em serviços downstream que usam dados de perfil como segmentação e destinos. Como resultado, permite que os dados de perfil sejam consistentes e permite que os dados de perfil permaneçam sincronizados com os sistemas de origem.

Para habilitar a solicitação de carimbo de data e hora do cliente, use o `extSourceSystemAudit.lastUpdatedDate` campo dentro do [Grupo de campos Atributos de Auditoria do Sistema de Origem Externa](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.md) e entre em contato com o Gerente técnico de conta do Adobe ou com o Atendimento ao cliente do Adobe com suas informações de sandbox e conjunto de dados.

## Restrições

Durante esse beta privado, as seguintes restrições se aplicam ao usar a solicitação de carimbo de data e hora do cliente:

- Você só pode usar a solicitação de carimbo de data e hora do cliente com **atributos de perfil** assimilado com **assimilação por transmissão** na loja de Perfis.
   - Há **não** solicitar garantias fornecidas para dados no data lake ou no Serviço de identidade.
- Você só pode usar a solicitação de carimbo de data e hora do cliente em **não produção** sandboxes.
- Você só pode aplicar a solicitação de carimbo de data e hora do cliente a **5** conjuntos de dados por sandbox.
- Você **não é possível** use upserts de transmissão para enviar atualizações parciais de linha em um conjunto de dados que tenha a ordem de carimbo de data e hora do cliente ativada.
- A variável `extSourceSystemAudit.lastUpdatedDate` campo **deve** estar no [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) formato. Ao usar o formato ISO 8601, ele **deve** ser como um datetime completo no formato `yyyy-MM-ddTHH:mm:ss.sssZ` (por exemplo, `2028-11-13T15:06:49.001Z`).
- Todas as linhas de dados assimiladas **deve** contém o `extSourceSystemAudit.lastUpdatedDate` como um grupo de campos de nível superior. Isso significa que esse campo **deve** não podem ser aninhados no esquema XDM. Se esse campo estiver ausente ou em um formato incorreto, o registro malformado **não** será assimilado e uma mensagem de erro correspondente será enviada.
- Qualquer conjunto de dados habilitado para a solicitação de carimbo de data e hora do cliente **deve** ser um novo conjunto de dados sem dados assimilados anteriormente.
- Para qualquer fragmento de perfil específico, somente as linhas que contêm um `extSourceSystemAudit.lastUpdatedDate` serão assimilados. Linhas que contêm um `extSourceSystemAudit.lastUpdatedDate` que seja mais velho ou da mesma idade será descartada.

## Recomendações

Ao implementar a solicitação de carimbo de data e hora do cliente, lembre-se das seguintes considerações:

- Você é responsável por sincronizar os relógios em todos os sistemas internos que enviam dados para o armazenamento de Perfil.
- Você deve ter precisão de nível de milissegundo em seus carimbos de data e hora formatados em ISO 8061.
