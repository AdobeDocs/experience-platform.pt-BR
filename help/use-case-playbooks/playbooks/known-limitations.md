---
solution: Experience Platform
title: Limitações conhecidas dos manuais de reprodução
description: Saiba mais sobre os problemas conhecidos e os problemas comuns com os manuais e como solucioná-los
role: User, Developer, Admin
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: e24334bb4ac788770abe20ec2324efa1e64bc0e8
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 1%

---


# Limitações conhecidas {#known-limitations}

Saiba como solucionar erros ao trabalhar com manuais de casos de uso e entender as limitações conhecidas da versão de disponibilidade geral.

## Limitações conhecidas

Algumas limitações conhecidas são exibidas ao criar uma instância de um manual e gerar ativos.

* Para esquemas gerados, se um esquema for gerado em uma instância de um manual e você editá-lo, outro esquema *não* será gerado se você habilitar outra instância do manual. Em vez disso, continue a usar o schema editado na instância também.

* Ao usar a [funcionalidade de reconhecimento de dados](/help/use-case-playbooks/playbooks/data-awareness.md) para promover o esquema da sandbox inspiradora para a sandbox de desenvolvimento, você poderá ver alguns erros semelhantes aos abaixo:

![Erros exibidos no fluxo de trabalho de mapeamento de esquema.](/help/use-case-playbooks/assets/playbooks/troubleshooting/schema-errors.png){width="1000" zoomable="yes"}

Isso ocorre porque alguns campos gerados a partir do esquema não estão presentes no esquema na sandbox de desenvolvimento para a qual você está copiando. Procure o que são esses campos. Em seguida, volte para a sandbox de desenvolvimento, onde é possível:

* Crie um novo grupo de campos que inclua esses campos ou
* Inclua no esquema um grupo de campos padrão e predefinido que inclua os campos ausentes.

Depois de incluir esses campos no esquema na sandbox de desenvolvimento, volte para o fluxo de trabalho para copiar os campos do esquema da sandbox inspiradora para a sandbox de desenvolvimento. Os erros desapareceram agora.

Para obter mais informações, assista ao vídeo abaixo para criar grupos de campos de esquema.

>[!VIDEO](https://video.tv.adobe.com/v/27013/?learn=on)
