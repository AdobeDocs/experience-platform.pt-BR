---
title: Usar o atributo XDM do último horário de qualificação nos novos destinos de armazenamento na nuvem beta
description: Saiba como usar o atributo XDM do último tempo de qualificação nos novos destinos de armazenamento na nuvem beta
hidefromtoc: y
hide: y
source-git-commit: 03031dcaad82932f92e76177adf3b55447c3c153
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# Usar o atributo XDM do último horário de qualificação nos novos destinos de armazenamento na nuvem beta {#last-qualification-time}

>[!IMPORTANT]
> 
>Esta página descreve a funcionalidade que está na versão beta. A funcionalidade e a documentação estão sujeitas a alterações. Entre em contato com o representante da Adobe ou com o Atendimento ao cliente se desejar obter acesso a esse programa beta.

## Pré-requisitos {#prerequisites}

Para usar o último horário de qualificação (`lastQualificationTime`), você deve estar inscrito no [programa beta](/help/release-notes/2022/october-2022.md#destinations) para usar a funcionalidade aprimorada de exportação de arquivos e exportar dados para um dos seis [destinos de armazenamento na nuvem beta](/help/release-notes/2022/october-2022.md#destinations) ([[!DNL ADLS Gen 2]](/help/destinations/catalog/cloud-storage/adls-gen2.md), [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md), [[!DNL Azure Blob]](/help/destinations/catalog/cloud-storage/azure-blob.md), [[!DNL Data Landing Zon]e](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [[!DNL Google Cloud Storage]](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)). Você está inscrito se puder ver os novos cartões beta para os destinos de armazenamento em nuvem no catálogo, conforme mostrado abaixo para [!DNL Amazon S3].

![Imagem mostrando a nova placa beta do Amazon S3](/help/destinations/assets/ui/activate-destinations/new-amazon-s3-beta-card.png)

## Como usar o atributo XDM do último tempo de qualificação {#how-to-use}

Se você estiver usando um dos seis novos conectores beta do Cloud Storage, poderá usar o atributo XDM do último tempo de qualificação na [etapa de mapeamento](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) do fluxo de trabalho de ativação para criar uma coluna no arquivo exportado com o carimbo de data e hora mais recente de quando um perfil se qualificou para um segmento. Isso pode ajudá-lo com determinados casos de uso de medição ou análise, bem como fornecer uma ideia melhor de quando ativar determinados públicos-alvo.

Observe que, para adicionar `lastQualificationTime` às exportações de arquivo, é necessário inserir manualmente o valor `xdm: segmentMembership.ups.seg_id.lastQualificationTime` no campo de origem, conforme mostrado abaixo. Também é possível editar o campo de destino para `lastQualificationTime` ou qualquer outro valor que você queira nomear para essa coluna. Observe que, como essa é uma funcionalidade beta, a sintaxe do `xdm: segmentMembership.ups.seg_id.lastQualificationTime` valor pode mudar no futuro.

![Gravação de tela mostrando o atributo XDM do último horário de qualificação colado na etapa de mapeamento](/help/destinations/ui/last-qualification-time.gif)

## Mais informações {#more-information}

Para obter informações abrangentes sobre como ativar dados para destinos baseados em arquivo, incluindo todas as etapas do fluxo de trabalho e as permissões necessárias, leia as [tutorial ativar destinos baseados em arquivo](/help/destinations/ui/activate-batch-profile-destinations.md).