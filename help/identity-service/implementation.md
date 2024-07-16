---
title: Guia de implementação do Identity Service
description: Saiba como os dados fornecidos ao Adobe Experience Platform são processados antes de serem usados pelo Serviço de identidade para criar gráficos de identidade.
exl-id: c961bbf6-6b46-470f-a671-93ff4173876c
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---

# Guia de implementação do Identity Service

Este documento fornece informações sobre como os dados fornecidos à Adobe Experience Platform são processados antes de serem usados pelo Serviço de identidade para criar um gráfico de identidade para um determinado cliente.

## Decidir sobre campos de identidade

Dependendo da sua estratégia de coleta de dados da empresa, os campos de dados rotulados como identidades determinam quais dados são incluídos no mapa de identidade. Para obter o máximo de benefícios do Experience Platform e as identidades mais abrangentes possíveis do cliente, você deve fazer upload de dados online e offline.

* Dados online são dados que descrevem a presença e o comportamento online, como nomes de usuário e endereços de email.

* Os dados offline se referem a dados que não estão diretamente relacionados à presença online, como IDs de sistemas CRM. Esse tipo de dados torna suas identidades mais robustas e oferece suporte à coesão de dados em seus diferentes sistemas.

## Criar namespaces de identidade adicionais

Embora o Experience Platform ofereça uma variedade de namespaces padrão, talvez seja necessário criar namespaces adicionais para categorizar corretamente suas identidades. Para obter mais informações, leia o manual sobre [criação de namespaces personalizados para sua organização](./features/namespaces.md).

>[!NOTE]
>
>Os namespaces de identidade são um qualificador para identidades. Como resultado, depois que um namespace é criado, ele não pode ser excluído.

## Incluir dados de identidade no Experience Data Model (XDM)

Como estrutura padronizada pela qual o Experience Platform organiza os dados do cliente, o Experience Data Model (XDM) permite que os dados sejam compartilhados e compreendidos no Experience Platform e em outros serviços que interagem com o Experience Platform. Para obter mais informações, leia a [Visão geral do Sistema XDM](../xdm/home.md).

Os esquemas de série de registros e de tempo fornecem os meios para incluir dados de identidade. À medida que os dados são assimilados, o gráfico de identidade criará novos relacionamentos entre fragmentos de dados de namespaces diferentes se eles compartilharem dados de identidade comuns.

## Rotular campos XDM como identidade

Qualquer campo do tipo `string` em esquemas que implementam classes XDM de série de tempo ou registro pode ser rotulado como um campo de identidade. Como resultado, todos os dados assimilados nesse campo seriam considerados dados de identidade.

Os campos de identidade também permitem a vinculação de identidades se compartilharem dados PII comuns.
Por exemplo, ao rotular campos de número de telefone como campos de identidade, o Serviço de identidade cria automaticamente gráficos de relacionamentos com os outros indivíduos que estão usando o mesmo número de telefone.

>[!NOTE]
>
>* Campos de tipo de matriz e mapa não são aceitos e não podem ser marcados e rotulados como campos de identidade.
>* O namespace das identidades resultantes é fornecido no momento em que o campo é rotulado.

Para obter mais informações, leia o guia no guia em [definindo campos de identidade na interface](../xdm/ui/fields/identity.md).

## Configurar um conjunto de dados para o Serviço de identidade

Durante o processo de assimilação por transmissão, o Serviço de identidade extrai automaticamente os dados de identidade dos dados de registro e da série temporal. No entanto, antes que os dados possam ser assimilados, eles devem ser ativados para o Serviço de identidade. Leia o tutorial sobre [configuração de um conjunto de dados para o Perfil do cliente em tempo real e o Serviço de identidade usando APIs](../profile/tutorials/dataset-configuration.md) para obter mais informações.

## Assimilar dados no serviço de identidade

O Serviço de identidade consome dados compatíveis com XDM enviados para o Experience Platform pela [assimilação em lote](../ingestion/batch-ingestion/overview.md) ou pela [assimilação por transmissão](../ingestion/streaming-ingestion/overview.md).

O vídeo a seguir tem como objetivo fornecer suporte à sua compreensão do Serviço de identidade. Este vídeo mostra como rotular campos de dados como identidades, assimilar dados de identidade e, em seguida, verificar se os dados foram para o Gráfico privado do serviço de identidade da Adobe Experience Platform.

>[!WARNING]
>
>A interface do Experience Platform mostrada no vídeo a seguir está desatualizada. Consulte a documentação para obter as capturas de tela e a funcionalidade mais recentes da interface.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)
