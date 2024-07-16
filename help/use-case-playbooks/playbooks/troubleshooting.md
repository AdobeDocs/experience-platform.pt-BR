---
solution: Experience Platform
title: Limitações conhecidas e solução de problemas com os manuais
description: Saiba mais sobre os problemas conhecidos e os problemas comuns com os manuais e como solucioná-los
role: User, Developer, Admin
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: 0faf3187c0b32e0be70033e501939412ade37d7e
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Solução de problemas {#troubleshooting}

Exibir sugestões de solução de problemas para erros comuns ao trabalhar com manuais de casos de uso

## Superfícies do Adobe Journey Optimizer não configuradas {#surfaces-not-configured}

Ao criar uma instância de um manual, você pode ver a mensagem abaixo exibida.

![Solução de problemas](/help/use-case-playbooks/assets/playbooks/troubleshooting/troubleshooting-ajo.png)

Isso ocorre porque os manuais do Journey Optimizer criam mensagens para canais de email, push e SMS. Leia o guia de [introdução](/help/use-case-playbooks/playbooks/get-started.md#configure-sandbox-and-channel-surfaces-in-journey-optimizer) para configurar as diferentes superfícies.

## Falha no status *ao criar uma nova instância* {#status-failed}

Se você vir uma mensagem de falha ao tentar criar uma instância, talvez o administrador não tenha concedido as permissões de usuário necessárias. Um manual contém muitos ativos diferentes e seu usuário precisa de permissões para criar esses ativos e poder criar a instância do manual com êxito. Consulte a seção [permissões](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) deste guia sobre como configurar permissões.

## Falha na importação {#import-failure}

Os clientes operam em diferentes ambientes de teste e, ocasionalmente, ao importar uma instância de seu ambiente para a sandbox Adobe, pode ocorrer uma falha. Para visualizar o status dessas importações, selecione Sandbox na navegação à esquerda e, em seguida, selecione Jobs. Aqui é possível exibir todos os detalhes dos arquivos importados. Selecione um arquivo com um status de falha e, em seguida, selecione Exibir detalhes do trabalho. Uma modal é exibida. Selecione Exibir arquivo JSON, role para baixo e copie a mensagem de erro que aparece em &quot;mensagens&quot;. É bem possível que várias mensagens de erro sejam exibidas, portanto, copie todas elas. Envie-os para a equipe de Adobe ao tentar registrar um tíquete de erro. Isso agiliza o processo de resolução e oferece à sua equipe mais contexto sobre o que está acontecendo.
