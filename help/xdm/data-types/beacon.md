---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;beacon;detalhes de interação;datatype;data-type;data type;Schema;home;popular topics;;social;social;social;topics;data-type;data type;data type;
solution: Experience Platform
title: Tipo de dados do beacon
topic: overview
description: Este documento fornece uma visão geral da classe de Perfil individual XDM.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 3%

---


# [!UICONTROL Tipo ] Beacondata

[!UICONTROL O ] Beaconis é um tipo de dados XDM padrão que descreve o dispositivo sem fio que comunica informações de identidade para aplicativos móveis quando dispositivos móveis estão dentro da faixa de alcance.

<img src="../images/data-types/beacon.png" width="450" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `beaconMajor` | Duplo | Os valores principais identificam e distinguem um grupo e valores inteiros não assinados entre 1 e 65.535. |
| `beaconMinor` | Duplo | Valores menores identificam e distinguem valores inteiros individuais e não assinados entre 1 e 65.535. |
| `proximity` | String | Distância estimada do sinal. Consulte o [apêndice](#proximity) para obter os valores e as definições aceitos. |
| `proximityUUID` | String | Um UUID de proximidade (Universally Unique Identifier) é um tipo especial de identificador usado para diferenciar os beacons em sua rede de todos os outros beacons em redes fora do seu controle. A UUID de proximidade é configurada em um beacon, para ser transmitida a dispositivos móveis no intervalo para identificar os beacons de uma organização. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.schema.json)

## Apêndice

A seção a seguir contém informações adicionais sobre o tipo de dados [!UICONTROL Beacon].

## Valores aceitos para proximidade {#proximity}

A tabela a seguir descreve os valores aceitos para `proximity` e seus significados associados:

| Valor | Descrição |
| --- | --- |
| `immediate` | Dentro de alguns centímetros. |
| `near` | A menos de 10 metros de distância. |
| `far` | A mais de 10 metros de distância. |
| `unknown` | A distância não pôde ser determinada, provavelmente devido a um sinal fraco. |