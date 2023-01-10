---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, campos, esquemas, esquemas, beacon, detalhes de interação, tipo de dados, tipo de dados, tipo de dados;
solution: Experience Platform
title: Tipo de dados do sinal
description: Este documento fornece uma visão geral da classe Perfil individual XDM.
exl-id: a3767c8d-a009-49b4-81a4-b084b6e5101a
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 4%

---

# [!UICONTROL Beacon] tipo de dados

[!UICONTROL Beacon] é um tipo de dados XDM padrão que descreve o dispositivo sem fio que comunica informações de identidade para aplicativos móveis, à medida que os dispositivos móveis estão dentro do alcance.

<img src="../images/data-types/beacon.png" width="450" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `beaconMajor` | Duplo | Os valores principais identificam e distinguem um grupo e valores inteiros não assinados entre 1 e 65.535. |
| `beaconMinor` | Duplo | Valores menores identificam e distinguem valores inteiros individuais e não assinados entre 1 e 65.535. |
| `proximity` | String | Distância estimada do sinal. Consulte a [apêndice](#proximity) para os valores e definições aceites. |
| `proximityUUID` | String | Um UUID de proximidade (Identificador universal exclusivo) é um tipo especial de identificador usado para distinguir beacons em sua rede de todos os outros beacons em redes fora de seu controle. A UUID de proximidade é configurada em um beacon, para ser transmitida a dispositivos móveis no intervalo para identificar os beacons de uma organização. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.schema.json)

## Apêndice

A seção a seguir contém informações adicionais sobre o [!UICONTROL Beacon] tipo de dados.

## Valores aceitos para proximidade {#proximity}

A tabela a seguir descreve os valores aceitos para `proximity` e o significado que lhes está associado:

| Valor | Descrição |
| --- | --- |
| `immediate` | Dentro de alguns centímetros. |
| `near` | A menos de 10 metros de distância. |
| `far` | Mais de 10 metros de distância. |
| `unknown` | A distância não pôde ser determinada, provavelmente devido a um sinal fraco. |
