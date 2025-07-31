---
title: Usar o atributo XDM do último horário de qualificação nos novos destinos de armazenamento na nuvem beta
description: Saiba como usar o atributo XDM do último tempo de qualificação nos novos destinos de armazenamento na nuvem beta
badgeBeta: label="Beta" type="Informative"
exl-id: d077ea10-5ff2-4acc-8ee6-78ea6cd752d1
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 1%

---

# Usar o atributo XDM do último horário de qualificação nos novos destinos de armazenamento na nuvem beta {#last-qualification-time}

>[!IMPORTANT]
> 
>Esta página descreve a funcionalidade que está na versão beta. A funcionalidade e a documentação estão sujeitas a alterações. Entre em contato com seu representante da Adobe ou com o Atendimento ao cliente se desejar ter acesso a esse programa beta.

## Pré-requisitos {#prerequisites}

Para usar o atributo XDM do último horário de qualificação (`lastQualificationTime`), você deve exportar dados para um dos seis destinos de armazenamento na nuvem listados abaixo:

* [[!DNL ADLS Gen 2]](/help/destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md)
* [[!DNL Azure Blob]](/help/destinations/catalog/cloud-storage/azure-blob.md)
* [[!DNL Data Landing Zone]](/help/destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](/help/destinations/catalog/cloud-storage/google-cloud-storage.md)
* [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)

## Como usar o atributo XDM do último tempo de qualificação {#how-to-use}

Se você estiver usando um dos seis conectores de armazenamento na nuvem listados acima, poderá usar o atributo XDM do último horário de qualificação na [etapa de mapeamento](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) do fluxo de trabalho de ativação para criar uma coluna no arquivo exportado com o carimbo de data e hora mais recente de quando um perfil se qualificou para um segmento. Isso pode ajudá-lo com determinados casos de uso de medição ou análise, bem como fornecer uma ideia melhor de quando ativar determinados públicos-alvo.

Observe que, para adicionar `lastQualificationTime` às suas exportações de arquivo, é necessário inserir manualmente o valor `xdm: segmentMembership.ups.seg_id.lastQualificationTime` no campo de origem, conforme mostrado abaixo. Você também pode editar o campo de destino como `lastQualificationTime` ou qualquer outro valor que queira nomear para essa coluna. Observe que, como essa é uma funcionalidade beta, a sintaxe do valor `xdm: segmentMembership.ups.seg_id.lastQualificationTime` poderá ser alterada no futuro.

![Gravação de tela mostrando o atributo XDM do último horário de qualificação colado na etapa de mapeamento](/help/destinations/ui/last-qualification-time.gif)

## Mais informações {#more-information}

Para obter informações detalhadas sobre como ativar dados para destinos baseados em arquivo, incluindo todas as etapas no fluxo de trabalho e as permissões necessárias, leia o [tutorial sobre ativação de destinos baseados em arquivo](/help/destinations/ui/activate-batch-profile-destinations.md).
