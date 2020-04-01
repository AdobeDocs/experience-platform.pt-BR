---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Amostra de transformações de ETL
topic: overview
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3

---


# Amostra de transformações de ETL

Este artigo demonstra as seguintes transformações de exemplo que um desenvolvedor de extração, transformação, carregamento (ETL) pode encontrar.

## CSV plano para hierarquia

### Arquivos de exemplo

Arquivos CSV e JSON de amostra estão disponíveis no acordo GitHub de referência ETL público mantido pela Adobe:

- [CRM_perfis.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_perfis.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)

### CSV de exemplo

Os seguintes dados do CRM foram exportados como `CRM_profiles.csv`:

```shell
TITLE   F_NAME  L_NAME  GENDER  DOB EMAIL   CRMID   ECID    LOYALTYID   ECID2   PHONE   STREET  CITY    STATE   COUNTRY ZIP LAT LONG
Mr  Ewart   Bennedsen   M   2004-09-25  ebennedsenex@jiathis.com    71a16013-d805-7ece-9ac4-8f2cd66e8eaa    87098882279810196101440938110216748923  2e33192000007456-0365c00000000000   55019962992006103186215643814973128178  256-284-7231    72 Buhler Crossing  Anniston    Alabama US  36205   33.708276   -85.7922905
Dr  Novelia Ansteys F   1987-10-31  nansteysdk@spotify.com  2eeb6532-82e1-0d58-8955-bf97de66a6f5    50829196174854544323574004005273946998  2e3319208000765b-3811c00000000001   65233136134594262632703695260919939885  704-181-6371    79 Northfield Hill  Charlotte   North Carolina  US  28299   35.2188655  -80.8108885
Mr  Ulises  Mochan  M   1996-03-20  umochanco@gnu.org   6f393075-addb-bdd6-73f8-31c393b700f5    70086119428645095847094710218289660855  2e33192080003023-26b2000000000002   82011353387947708954389153068944017636  720-837-4159    00671 Mifflin Trail Lacolle Qu√©bec CA  E5A 45.08338    -73.36585
Mrs Friederike  Durrell F   1979-01-3   fdurrellbj@utexas.edu   33d018ec-5fed-f1a3-56aa-079370a9511b    50164729868919217963697788808932473456  2e33192080006dfc-0cdf400000000003   64452712468609735658703639722261004071  798-528-3458    47 Fremont Hill Independencia   Veracruz Llave  MX  91891   19.3803931  -99.1476905
Rev Evita   Bingall F   1974-02-28  ebingallod@mac.com  8c93db88-f328-8efb-dc73-d5654d371cbe    74973364195185450328832136951985519627  2e331920800038db-0559e00000000004   58945501950285346322834356669253860483  397-178-5897    56 Crescent Oaks Court  Buenavista  Oaxaca  MX  71730   19.4458447  -99.1497665
Mr  Eugenie Bechley F   1969-05-19  ebechley9r@telegraph.co.uk  b0c76a3f-6526-0ad0-e050-48143b687d18    67119779213799783658184754966135750376  2e331920800001a4-24b2800000000005   59715249079109455676103900762283358508  718-374-7456    5760 Southridge Junction    Staten Island   New York    US  10310   40.6307451  -74.1181235
Dr  Cammi   Haslen  F   1973-12-17  chaslenqv@ehow.com  56059cd5-5006-ce5f-2f5f-15b4d856a204    61747117963243728095047674165570746095  2e33192080007c25-2ec0600000000006   86268258269066295956223980330791223320  865-538-8291    83 Veith Street Knoxville   Tennessee   US  37995   35.95   -84.05
```

### Mapeamento

Os requisitos de mapeamento para os dados do CRM são descritos na tabela a seguir e incluem as seguintes transformações:
- Colunas de identidade para `identityMap` propriedades
- Data de nascimento (DOB) ao Ano e ao Mês
- Strings para Duplos ou números inteiros curtos.

| Coluna CSV | Caminho XDM | Formatação de dados |
| ---------- | -------- | --------------- |
| TÍTULO | people.name.courtesyTitle | Copiar como string |
| F_NAME | people.name.firstName | Copiar como string |
| L_NAME | people.name.lastName | Copiar como string |
| GÊNERO | pessoa.gênero | Transformar gênero como valor de enumeração pessoal correspondente.gênero |
| DOB | people.bornDayAndMonth: &quot;MM-DD&quot;<br/>people.bornData: &quot;AAAA-MM-DD&quot;<br/>pessoa.nascimentoAno: YYYY | Transforme bornDayAndMonth como<br/>stringTransform bornDate como<br/>stringTransform bornYear como short int |
| EMAIL | personalEmail.address | Copiar como string |
| CRMID | identityMap.CRMID[{&quot;id&quot;:x, primário:false}] | Copiar como string para a matriz CRMID no identityMap e definir Primary como false |
| ECID | identityMap.ECID[{&quot;id&quot;:x, principal: false}] | Copiar como string para a primeira entrada na matriz ECID no identityMap e definir Primary como false |
| LOYALTYID | identityMap.LOYALTYID[{&quot;id&quot;:x, primário:true}] | Copiar como string para a matriz LOYALTYID no identityMap e definir Primary como true |
| ECID2 | identityMap.ECID[{&quot;id&quot;:x, primário:false}] | Copiar como sequência para segunda entrada na matriz ECID no identityMap e definir Primary como false |
| TELEFONE | homePhone.number | Copiar como string |
| RUA | homeAddress.street1 | Copiar como string |
| CIDADE | homeAddress.city | Copiar como string |
| ESTADO | homeAddress.stateProvince | Copiar como string |
| PAÍS | homeAddress.country | Copiar como string |
| ZIP | homeAddress.postalCode | Copiar como string |
| LADO | homeAddress.latitude | Converter em duplo |
| LONGO | homeAddress.longitude | Converter em duplo |


### Saída XDM

A amostra a seguir mostra as duas primeiras linhas do CSV transformadas em XDM, conforme mostrado em `CRM_profiles.json`:

```json
{
   "person": {
      "name": {
         "courtesyTitle": "Mr",
         "firstName": "Ewart",
         "lastName": "Bennedsen"
      },
      "gender": "male",
      "birthDayAndMonth": "09-25",
      "birthDate": "2004-09-25",
      "birthYear": 2004
   },
   "identityMap": {
      "CRMID": [{
         "id": "71a16013-d805-7ece-9ac4-8f2cd66e8eaa",
         "primary": false
      }],
      "ECID": [{
         "id": "87098882279810196101440938110216748923",
         "primary": false
      },
      {
         "id": "55019962992006103186215643814973128178",
         "primary": false
      }],
      "LOYALTYID": [{
         "id": "2e33192000007456-0365c00000000000",
         "primary": true
      }]
   },
   "homePhone": {
      "number": "256-284-7231"
   },
   "personalEmail": {
      "address": "ebennedsenex@jiathis.com"
   },
   "homeAddress": {
      "street1": "72 Buhler Crossing",
      "city": "Anniston",
      "stateProvince": "Alabama",
      "country": "US",
      "postalCode": "36205",
      "_schema": {
         "latitude": 33.708276,
         "longitude": -85.7922905
      }
   }
},{
   "person": {
      "name": {
         "courtesyTitle": "Dr",
         "firstName": "Novelia",
         "lastName": "Ansteys"
      },
      "gender": "female",
      "birthDayAndMonth": "10-31",
      "birthDate": "1987-10-31",
      "birthYear": 1987
   },
   "identityMap": {
      "CRMID": [{
         "id": "2eeb6532-82e1-0d58-8955-bf97de66a6f5",
         "primary": false
      }],
      "ECID": [{
         "id": "50829196174854544323574004005273946998",
         "primary": false
      },
      {
         "id": "65233136134594262632703695260919939885",
         "primary": false
      }],
      "LOYALTYID": [{
         "id": "2e3319208000765b-3811c00000000001",
         "primary": true
      }]
   },
   "homePhone": {
      "number": "704-181-6371"
   },
   "personalEmail": {
      "address": "nansteysdk@spotify.com"
   },
   "homeAddress": {
      "street1": "79 Northfield Hill",
      "city": "Charlotte",
      "stateProvince": "North Carolina",
      "country": "US",
      "postalCode": "28299",
      "_schema": {
         "latitude": 35.2188655,
         "longitude": -80.8108888
      }
   }
}
```

## Dataframe para schema XDM

A hierarquia de um dataframe (como um arquivo Parquet) deve corresponder à do schema XDM para o qual está sendo feito o upload.

### Exemplo de dataframe

A estrutura do exemplo de dataframe a seguir foi mapeada para um schema que implementa a classe de Perfil Individual XDM e contém os campos mais comuns associados aos schemas desse tipo.

```python
[
    StructField("person", StructType(
        [
            StructField("name", StructType(
                [
                    StructField("courtesyTitle", StringType()),
                    StructField("firstName", StringType()),
                    StructField("lastName", StringType())
                ]
            )),
            StructField("gender", StringType()),
            StructField("birthDayAndMonth", StringType()),
            StructField("birthDate", StringType()),
            StructField("birthYear", LongType())
        ]
    )),
    StructField("identityMap", MapType(
        StructField("CRMID", ArrayType(
            StructType(
                [
                    StructField("id", StringType()),
                    StructField("primary", BooleanType())
                ]
            )
        )),
        StructField("ECID", ArrayType(
            StructType(
                [
                    StructField("id", StringType()),
                    StructField("primary", BooleanType())
                ]
            )
        )),
        StructField("LOYALTYID", ArrayType(
            StructType(
                [
                    StructField("id", StringType()),
                    StructField("primary", BooleanType())
                ]
            )
        ))
    )),
    StructField("homePhone", StructType(
        [
            StructField("number", StringType())
        ]
    )),
    StructField("personalEmail", StructType(
        [
            StructField("address", StringType())
        ]
    )),
    StructField("homeAddress", StructType(
        [
            StructField("street1", StringType()),
            StructField("city", StringType()),
            StructField("stateProvince", StringType()),
            StructField("country", StringType()),
            StructField("postalCode", StringType()),
            StructField("_schema", StructType(
                [
                    StructField("latitude", DoubleType()),
                    StructField("latitude", DoubleType()),
                ]
            ))
        ]
    ))    
]
```

Ao criar um dataframe para uso na Adobe Experience Platform, é importante garantir que sua estrutura hierárquica corresponda exatamente à de um schema XDM existente para que os campos sejam mapeados corretamente.

## Identidades para mapa de identidade

### Matriz de identidades

```json
[
  {
    "xdm:id": "someone1@example.com",
    "xdm:namespace": {
      "xdm:code": "Email"
    }
  },
  {
    "xdm:id": "2eeb6532-82e1-0d58-8955-bf97de66a6f5",
    "xdm:namespace": {
      "xdm:code": "CRMID"
    }
  },
  {
    "xdm:id": "2e3319208000765b-3811c00000000001",
    "xdm:namespace": {
      "xdm:code": "LOYALTYID"
    }
  }
]
```

### Mapeamento

Os requisitos de mapeamento para a matriz de identidades estão descritos na tabela a seguir:

| Campo de identidade | campo IdentityMap | Tipo de dados |
| -------------- | ----------------- | --------- |
| identities[0].id | [identityMapEmail][{"id"}] | copiar como string |
| identities[1].id | [identityMapCRMID][{"id"}] | copiar como string |
| identities[2].id | [identityMapLOYALTYID][{"id"}] | copiar como string |

### Saída XDM

Abaixo está o conjunto de identidades transformadas em XDM:

```JSON
"identityMap": {
      "Email": [{
         "id": "someone1@example.com"
      }],
      "CRMID": [{
         "id": "2eeb6532-82e1-0d58-8955-bf97de66a6f5"
      }],
      "LOYALTYID": [{
         "id": "2e3319208000765b-3811c00000000001"
      }]
   }
```

