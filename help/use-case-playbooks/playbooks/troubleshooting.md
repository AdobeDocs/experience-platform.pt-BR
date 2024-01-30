---
solution: Experience Platform
title: Limitações conhecidas e solução de problemas com os manuais
description: Saiba mais sobre os problemas conhecidos e os problemas comuns com os manuais e como solucioná-los
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: d6be5d3e21ea924ff98c400b972709b1f60c25eb
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 2%

---


# Solução de problemas e limitações conhecidas {#troubleshooting-known-limitations}

## Solução de problemas {#troubleshooting}

### Superfícies do Adobe Journey Optimizer não configuradas

Ao criar uma instância de um manual, você pode ver a mensagem abaixo exibida.

![Solução de problemas](/help/use-case-playbooks/assets/playbooks/troubleshooting/troubleshooting-ajo.png)

Isso ocorre porque os manuais do Journey Optimizer criam mensagens para canais de email, push e SMS. Leia o [introdução](/help/use-case-playbooks/playbooks/get-started.md#configure-sandbox-and-channel-surfaces-in-journey-optimizer) guia para configurar as diferentes superfícies.

### Status *falhou* ao criar uma nova instância

Se você vir uma mensagem de falha ao tentar criar uma instância, talvez o administrador não tenha concedido as permissões de usuário necessárias. Um manual contém muitos ativos diferentes e seu usuário precisa de permissões para criar esses ativos e poder criar a instância do manual com êxito. Consulte a [permissões](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) seção deste guia sobre como configurar permissões.

## Limitações conhecidas

Algumas limitações conhecidas são exibidas ao criar uma instância de um manual e gerar ativos.

* Para esquemas gerados, se um esquema for gerado em uma instância de um manual e você editá-lo, outro esquema *não* será gerado se você habilitar outra instância do manual. Em vez disso, continue a usar o schema editado na instância também.

* Ao usar o [funcionalidade de reconhecimento de dados](/help/use-case-playbooks/playbooks/data-awareness.md) para promover o esquema da sandbox inspiradora para a sandbox de desenvolvimento, você pode ver alguns erros semelhantes aos abaixo:

![schema-errors](/help/use-case-playbooks/assets/playbooks/troubleshooting/schema-errors.png)

Isso ocorre porque alguns campos gerados a partir do esquema não estão presentes no esquema na sandbox de desenvolvimento para a qual você está copiando. Procure o que são esses campos. Em seguida, volte para a sandbox de desenvolvimento, onde é possível:

* Crie um novo grupo de campos que inclua esses campos ou
* Inclua no esquema um grupo de campos padrão e predefinido que inclua os campos ausentes.

Depois de incluir esses campos no esquema na sandbox de desenvolvimento, volte para o fluxo de trabalho para copiar os campos do esquema da sandbox inspiradora para a sandbox de desenvolvimento. Os erros desapareceram agora.

Para obter mais informações, assista ao vídeo abaixo para criar grupos de campos de esquema.

>[!VIDEO](https://video.tv.adobe.com/v/27013/?learn=on)
