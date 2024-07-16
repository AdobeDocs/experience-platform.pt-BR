---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;beacon;detalhes de interação;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de dados do sinal
description: Saiba mais sobre a classe Perfil individual XDM.
exl-id: a3767c8d-a009-49b4-81a4-b084b6e5101a
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 17%

---

# Tipo de dados [!UICONTROL Sinal]

[!UICONTROL Beacon] é um tipo de dados XDM padrão que descreve o dispositivo sem fio que comunica informações de identidade para aplicativos móveis à medida que os dispositivos móveis ficam ao alcance.

<img src="../images/data-types/beacon.png" width="450" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `beaconMajor` | Duplo | Os valores maiores identificam e distinguem um grupo e valores inteiros sem sinal entre 1 e 65.535. |
| `beaconMinor` | Duplo | Os valores menores identificam e distinguem valores inteiros individuais e sem sinal entre 1 e 65.535. |
| `proximity` | String | Distância estimada do sinal. Consulte o [apêndice](#proximity) para obter os valores e as definições aceitos. |
| `proximityUUID` | String | Um UUID (Identificador universal exclusivo) de proximidade é um tipo especial de identificador usado para distinguir beacons em sua rede de todos os outros beacons em redes fora do seu controle. A UUID de proximidade é configurada em um beacon, a ser transmitido para dispositivos móveis ao alcance para identificar os beacons de uma organização. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.schema.json)

## Apêndice

A seção a seguir contém informações adicionais sobre o tipo de dados [!UICONTROL Beacon].

## Valores aceitos para proximidade {#proximity}

A tabela a seguir descreve os valores aceitos para `proximity` e seus significados associados:

| Valor | Descrição |
| --- | --- |
| `immediate` | Dentro de alguns centímetros. |
| `near` | A menos de 10 metros. |
| `far` | A mais de 10 metros. |
| `unknown` | A distância não pôde ser determinada, provavelmente devido a um sinal fraco. |
