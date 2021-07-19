---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, campos, esquemas, esquemas, beacon, detalhes de interação, tipo de dados, tipo de dados, tipo de dados;
solution: Experience Platform
title: Tipo de dados do sinal
topic-legacy: overview
description: Este documento fornece uma visão geral da classe Perfil individual XDM.
exl-id: a3767c8d-a009-49b4-81a4-b084b6e5101a
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 4%

---

#  Tipo de dados Beacondata

 Beaconis é um tipo de dados XDM padrão que descreve o dispositivo sem fio que comunica informações de identidade a aplicativos móveis, à medida que os dispositivos móveis estão dentro da faixa.

<img src="../images/data-types/beacon.png" width="450" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `beaconMajor` | Duplo | Os valores principais identificam e distinguem um grupo e valores inteiros não assinados entre 1 e 65.535. |
| `beaconMinor` | Duplo | Valores menores identificam e distinguem valores inteiros individuais e não assinados entre 1 e 65.535. |
| `proximity` | String | Distância estimada do sinal. Consulte o [apêndice](#proximity) para obter os valores e as definições aceitos. |
| `proximityUUID` | String | Um UUID de proximidade (Identificador universal exclusivo) é um tipo especial de identificador usado para distinguir beacons em sua rede de todos os outros beacons em redes fora de seu controle. A UUID de proximidade é configurada em um beacon, para ser transmitida a dispositivos móveis no intervalo para identificar os beacons de uma organização. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.schema.json)

## Apêndice

A seção a seguir contém informações adicionais sobre o tipo de dados [!UICONTROL Beacon].

## Valores aceitos para proximidade {#proximity}

A tabela a seguir descreve os valores aceitos para `proximity` e seus significados associados:

| Valor | Descrição |
| --- | --- |
| `immediate` | Dentro de alguns centímetros. |
| `near` | A menos de 10 metros de distância. |
| `far` | Mais de 10 metros de distância. |
| `unknown` | A distância não pôde ser determinada, provavelmente devido a um sinal fraco. |
