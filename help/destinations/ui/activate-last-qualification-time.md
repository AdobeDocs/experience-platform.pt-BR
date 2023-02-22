---
title: Use o atributo XDM do último tempo de qualificação nos novos destinos de armazenamento da nuvem beta
description: Saiba como usar o atributo XDM do último tempo de qualificação nos novos destinos de armazenamento da nuvem beta
hidefromtoc: y
hide: y
source-git-commit: 03031dcaad82932f92e76177adf3b55447c3c153
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# Use o atributo XDM do último tempo de qualificação nos novos destinos de armazenamento da nuvem beta {#last-qualification-time}

>[!IMPORTANT]
> 
>Esta página descreve a funcionalidade que está em beta. A funcionalidade e a documentação estão sujeitas a alterações. Entre em contato com o representante do Adobe ou com o Atendimento ao cliente se desejar acessar esse programa beta.

## Pré-requisitos {#prerequisites}

Para usar o tempo da última qualificação (`lastQualificationTime`) atributo XDM, você deve ser inscrito no [programa beta](/help/release-notes/2022/october-2022.md#destinations) para usar a funcionalidade aprimorada de exportação de arquivos e exportar dados para um dos seis [destinos de armazenamento na nuvem beta](/help/release-notes/2022/october-2022.md#destinations) ([[!DNL ADLS Gen 2]](/help/destinations/catalog/cloud-storage/adls-gen2.md), [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md), [[!DNL Azure Blob]](/help/destinations/catalog/cloud-storage/azure-blob.md), [[!DNL Data Landing Zon]e](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [[!DNL Google Cloud Storage]](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)). Você estará inscrito se puder ver os novos cartões beta para os destinos de armazenamento em nuvem no catálogo, conforme mostrado abaixo para [!DNL Amazon S3].

![Imagem que mostra a nova placa beta Amazon S3](/help/destinations/assets/ui/activate-destinations/new-amazon-s3-beta-card.png)

## Como usar o último atributo XDM de tempo de qualificação {#how-to-use}

Se estiver usando um dos seis novos conectores beta de armazenamento em nuvem, você pode usar o atributo XDM do último tempo de qualificação no [etapa de mapeamento](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) do fluxo de trabalho de ativação para criar uma coluna no arquivo exportado com o registro de data e hora mais recente de quando um perfil se qualificou para um segmento. Isso pode ajudá-lo com determinados casos de uso de medição ou análise, bem como fornecer uma ideia melhor de quando ativar certos públicos-alvo.

Observe que para adicionar `lastQualificationTime` para suas exportações de arquivo, atualmente é necessário inserir manualmente o valor `xdm: segmentMembership.ups.seg_id.lastQualificationTime` no campo de origem, conforme mostrado abaixo. Também é possível editar o campo de destino para `lastQualificationTime` ou qualquer outro valor que você queira nomear essa coluna. Observe que, como essa é uma funcionalidade beta, a sintaxe da variável `xdm: segmentMembership.ups.seg_id.lastQualificationTime` pode mudar no futuro.

![Gravação de tela mostrando o último tempo de qualificação Atributo XDM colado na etapa de mapeamento](/help/destinations/ui/last-qualification-time.gif)

## Mais informações {#more-information}

Para obter informações extensas sobre como ativar dados em destinos baseados em arquivos, incluindo todas as etapas no fluxo de trabalho e as permissões necessárias, leia a [tutorial ativar destinos com base em arquivo](/help/destinations/ui/activate-batch-profile-destinations.md).