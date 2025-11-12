---
title: Visão geral do conector SFTP Source
description: Saiba como conectar um servidor SFTP ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: d5bced3d-cd33-40ea-bce0-32c76ecd2790
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '1205'
ht-degree: 2%

---

# Conector SFTP

A Adobe Experience Platform permite a assimilação de dados de fontes externas, além de permitir estruturar, rotular e aprimorar os dados recebidos por meio dos serviços da Experience Platform. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

Leia este documento para obter as etapas de pré-requisito que você precisa concluir para conectar com êxito sua conta do [!DNL SFTP] ao Experience Platform.

>[!TIP]
>
>É necessário desativar a Autenticação interativa de teclado na configuração do servidor SFTP antes de se conectar. Desativar a configuração permitirá que as senhas sejam inseridas manualmente, em vez de serem inseridas por meio de um serviço ou programa.

## Pré-requisitos {#prerequisites}

Leia esta seção para obter as etapas de pré-requisito que você deve concluir para conectar com êxito a origem do [!DNL SFTP] ao Experience Platform.

### INCLUO NA LISTA DE PERMISSÕES de endereços IP

Você deve adicionar endereços IP específicos da região ao incluo na lista de permissões antes de conectar suas fontes à Experience Platform. Para obter mais informações, leia o guia sobre [como ler os endereços IP de incluir na lista de permissões para se conectar ao Experience Platform](../../ip-address-allow-list.md) para obter mais informações.

### Restrições de nomenclatura para arquivos e diretórios

Veja a seguir uma lista de restrições que você deve considerar ao nomear seu arquivo ou diretório de armazenamento em nuvem.

* Os nomes dos componentes de diretório e arquivo não podem exceder 255 caracteres.
* Nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
* Os seguintes caracteres de URL reservados devem ter um escape adequado: `! ' ( ) ; @ & = + $ , % # [ ]`
* Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
* Caracteres de caminho de URL inválidos não permitidos. Pontos de código como `\uE000`, embora válidos em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode, como caracteres de controle (0x00 a 0x1F, \u0081 etc.), também não são permitidos. Para regras que regem cadeias de caracteres Unicode em HTTP/1.1, consulte [RFC 2616, Seção 2.2: Regras Básicas](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
* Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (.) e dois caracteres de ponto (..).

### Configurar uma chave privada OpenSSH codificada na Base64 para [!DNL SFTP]

A origem [!DNL SFTP] dá suporte à autenticação usando a chave privada OpenSSH codificada em [!DNL Base64]. Consulte as etapas abaixo para obter informações sobre como gerar sua chave privada OpenSSH codificada na Base64 e conectar o [!DNL SFTP] ao Experience Platform.

>[!BEGINTABS]

>[!TAB Janelas]

### [!DNL Windows] usuários

Se você estiver usando uma máquina [!DNL Windows], abra o menu **Iniciar** e selecione **Configurações**.

![configurações](../../images/tutorials/create/sftp/settings.png)

No menu **Configurações** exibido, selecione **Aplicativos**.

![aplicativos](../../images/tutorials/create/sftp/apps.png)

Em seguida, selecione **Recursos opcionais**.

![recursos-opcionais](../../images/tutorials/create/sftp/optional-features.png)

Uma lista de recursos opcionais é exibida. Se o **OpenSSH Client** já estiver pré-instalado no computador, ele será incluído na lista **Recursos instalados** em **Recursos opcionais**.

![open-ssh](../../images/tutorials/create/sftp/open-ssh.png)

Se não estiver instalado, selecione **Instalar**, abra **[!DNL Powershell]** e execute o seguinte comando para gerar sua chave privada:

```shell
PS C:\Users\lucy> ssh-keygen -t rsa -m pem
Generating public/private rsa key pair.
Enter file in which to save the key (C:\Users\lucy/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in C:\Users\lucy/.ssh/id_rsa.
Your public key has been saved in C:\Users\lucy/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:osJ6Lg0TqK8nekNQyZGMoYwfyxNc+Wh0hYBtBylXuGk lucy@LAPTOP-FUJT1JEC
The key's randomart image is:
+---[RSA 3072]----+
|.=.*+B.o.        |
|=.O.O +          |
|+o+= B           |
|+o +E .          |
|.o=o  . S        |
|+... . .         |
| *o .            |
|o.B.             |
|=O..             |
+----[SHA256]-----+
```

Em seguida, execute o seguinte comando ao fornecer o caminho de arquivo da chave privada, para codificar sua chave privada em [!DNL Base64]:

```shell
C:\Users\lucy> [convert]::ToBase64String((Get-Content -path "C:\Users\lucy\.ssh\id_rsa" -Encoding byte)) > C:\Users\lucy\.ssh\id_rsa_base64
```

O comando acima salva a chave privada codificada em [!DNL Base64] no caminho de arquivo designado. Em seguida, você pode usar essa chave privada para se autenticar no [!DNL SFTP] e se conectar ao Experience Platform.

>[!TAB Mac]

### [!DNL Mac] usuários

Se você estiver usando um [!DNL Mac], abra o **Terminal** e execute o seguinte comando para gerar a chave privada (nesse caso, a chave privada será salva em `/Documents/id_rsa`):

```shell
ssh-keygen -t rsa -m pem -f ~/Documents/id_rsa
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/vrana/Documents/id_rsa.
Your public key has been saved in /Users/vrana/Documents/id_rsa.pub.
The key fingerprint is:
SHA256:s49PCaO4a0Ee8I7OOeSyhQAGc+pSUQnRii9+5S7pp1M vrana@vrana-macOS
The key's randomart image is:
+---[RSA 2048]----+
|o ==..           |
|.+..o            |
|oo.+             |
|=.. +            |
|oo = .  S        |
|+.+ +E . = .     |
|o*..*.. . o      |
|.o*=.+   +       |
|.oo=Oo  ..o      |
+----[SHA256]-----+
```

Em seguida, execute o seguinte comando para codificar a chave privada em [!DNL Base64]:

```shell
base64 ~/Documents/id_rsa > ~/Documents/id_rsa_base64
 
 
# Print Content of base64 encoded file
cat ~/Documents/id_rsa_base64
LS0tLS1CRUdJTiBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0KYjNCbGJuTnphQzFyWlhrdGRqRUFBQUFBQkc1dmJtVUFBQUFFYm05dVpRQUFBQUFBQUFBQkFBQUJGd0FBQUFkemMyZ3RjbgpOaEFBQUFBd0VBQVFBQUFRRUF0cWFYczlXOUF1ZmtWazUwSXpwNXNLTDlOMU9VYklaYXVxbVM0Q0ZaenI1NjNxUGFuN244CmFxZWdvQTlCZnVnWDJsTVpGSFl5elEzbnp6NXdXMkdZa1hkdjFjakd0elVyNyt1NnBUeWRneGxrOGRXZWZsSzBpUlpYWW4KVFRwS0E5c2xXaHhjTXg3R2x5ejdGeDhWSzI3MmdNSzNqY1d1Q0VIU3lLSFR5SFFwekw0MEVKbGZJY1RGR1h1dW1LQjI5SwpEakhwT1grSDdGcG5Gd1pabTA4Uzc2UHJveTVaMndFalcyd1lYcTlyUDFhL0E4ejFoM1ZLdllzcG53c2tCcHFQSkQ1V3haCjczZ3M2OG9sVllIdnhWajNjS3ZsRlFqQlVFNWRNUnB2M0I5QWZ0SWlrYmNJeUNDaXV3UnJmbHk5eVNPQ2VlSEc0Z2tUcGwKL3V4YXNOT0h1d0FBQThqNnF6R1YrcXN4bFFBQUFBZHpjMmd0Y25OaEFBQUJBUUMycHBlejFiMEM1K1JXVG5Rak9ubXdvdgowM1U1UnNobHE2cVpMZ0lWbk92bnJlbzlxZnVmeHFwNkNnRDBGKzZCZmFVeGtVZGpMTkRlZlBQbkJiWVppUmQyL1Z5TWEzCk5TdnY2N3FsUEoyREdXVHgxWjUrVXJTSkZsZGlkTk9rb0QyeVZhSEZ3ekhzYVhMUHNYSHhVcmJ2YUF3cmVOeGE0SVFkTEkKb2RQSWRDbk12alFRbVY4aHhNVVplNjZZb0hiMG9PTWVrNWY0ZnNXbWNYQmxtYlR4THZvK3VqTGxuYkFTTmJiQmhlcjJzLwpWcjhEelBXSGRVcTlpeW1mQ3lRR21vOGtQbGJGbnZlQ3pyeWlWVmdlL0ZXUGR3cStVVkNNRlFUbDB4R20vY0gwQiswaUtSCnR3aklJS0s3Qkd0K1hMM0pJNEo1NGNiaUNST21YKzdGcXcwNGU3QUFBQUF3RUFBUUFBQVFBcGs0WllzMENSRnNRTk9WS0sKYWxjazlCVDdzUlRLRjFNenhrSGVydmpJYk9kL0lvRXpkcHlVa28rbm41RmpGK1hHRnNCUXZnOFdTaUlJTk1oU3BNYWI1agpvWXlka2gvd0ovWElOaDlZaE5QVXlURi9NNkFnMkNYd21KS2RxN1VKWjZyNjloV3V0VVN6U05QbkVYWTZLc29GeVUwTEFvCko0OHJMT1pMZldtMHFhWDBLNUgzNmJPaHFXSWJwMDNoZk94eno5M0MrSDM5MFJkRkp4bzJVZ0FVY3UvdHREb0REVldBdmEKVkVyMWEzak9LenVHbThrK21WeXpPZERjVFY4ckZIT0pwRnRBU3l6Q24yVld1MjV0TWtrcGRPRjNKcVdMZHdOY3loeG1URApXZGVDNWh4V0Fiano0WDZ5WXpHcFcwTmptVkFoWUVVZGNBSVlXWWM3OGEvQkFBQUFnRm8wakl4aGhwZkJ6QjF6b09FMDJBClpjTC9hcUNuYysrdmJ1a2V0aFg5Zzhlb0xQMTQyeUgzdlpLczl3c1RtbVVsZ0prZURaN2hUcklwOGY2eEwzdDRlMXByY1kKb2ZLd0gwckNGOTFyaldPbGZOUmxEempoR1NTTEVMczZoNlNzMEdBQXE2Z0ZQTVF2dTB4TDlQUTlGQ21YZVVKazJpRm1MWgpEWWJGc0NyVUxEQUFBQWdRRGF0a1pMamJaSTBFM0ZuY2dTOVF5Y3lVWmtkZ1dVNjBQcG9ud3BMQXdUdHRpOG1EQXE5cHYwClEvUlk1WE9UeGF3VXNHa0tYMjNtV1BYR0grdUlBSzhrelVVM2dGM1dRWGVkTWw4NHVCVFZCTEtUdStvVVAvZmIvMEE0dE0KSE9BSythbXZPMkZuYzFiSmVwd05USTE2cjZXWk9sZWV2ZklJQVpXcEgxVVpIdkVRQUFBSUVBMWNwcStDNUVXSFJwbnVPZQpiNHE4T0tKTlJhSUxIRUN6U0twWlFpZDFhRmJYWlVKUXpIQU85YzhINVZMcjBNUjFkcW1ORkNja2ZsZzI2Y3BEUEl3TjBYCm5HMFBxcmhKbXp0U3ZQZ3NGdkNPallncXF6U0RYUjkxd1JQTEN5cU8zcGMyM2kzZnp2WkhtMGhIdWdoNVJqV0loUlFZVkwKZUpDWHRqM08vY3p1SWdzQUFBQVJkbkpoYm1GQWRuSmhibUV0YldGalQxTUJBZz09Ci0tLS0tRU5EIE9QRU5TU0ggUFJJVkFURSBLRVktLS0tLQo=
```

Depois que a chave privada codificada em [!DNL Base64] for salva na pasta designada, você deverá adicionar o conteúdo do arquivo de chave pública a uma nova linha nas chaves autorizadas do host [!DNL SFTP]. Execute o seguinte comando na linha de comando:

```shell
cat ~/id_rsa.pub >> ~/.ssh/authorized_keys
```

Para confirmar se a chave pública foi adicionada corretamente, execute o seguinte na linha de comando:

```shell
more ~/.ssh/authorized_keys
```

>[!ENDTABS]

### Coletar credenciais necessárias {#credentials}

Você deve fornecer valores para as credenciais a seguir para conectar seu servidor [!DNL SFTP] ao Experience Platform.

>[!BEGINTABS]

>[!TAB Autenticação básica]

Forneça os valores apropriados para as credenciais a seguir para autenticar o servidor [!DNL SFTP] usando a autenticação básica.

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O nome ou endereço IP associado ao servidor [!DNL SFTP]. |
| `port` | A porta do servidor [!DNL SFTP] à qual você está se conectando. Se não for fornecido, o valor padrão será `22`. |
| `username` | O nome de usuário com acesso ao servidor [!DNL SFTP]. |
| `password` | A senha do servidor [!DNL SFTP]. |
| `maxConcurrentConnections` | Esse parâmetro permite especificar um limite máximo para o número de conexões simultâneas que a Experience Platform criará ao se conectar ao servidor SFTP. Você deve definir esse valor como menor que o limite definido pelo SFTP. **Observação**: quando esta configuração é habilitada para uma conta SFTP existente, ela afeta apenas os fluxos de dados futuros, não os existentes. |
| `folderPath` | O caminho para a pasta à qual você deseja fornecer acesso. [!DNL SFTP] origem, você pode fornecer o caminho da pasta para especificar o acesso do usuário à subpasta de sua escolha. |
| `disableChunking` | Durante a assimilação de dados, a origem [!DNL SFTP] pode recuperar o comprimento do arquivo primeiro, dividir o arquivo em várias partes e lê-los simultaneamente. Você pode habilitar ou desabilitar esse valor para especificar se o servidor [!DNL SFTP] pode recuperar comprimentos de arquivo ou ler dados de um deslocamento específico. |
| `connectionSpec.id` | (Somente API) A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL SFTP] é: `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

>[!TAB Autenticação de chave pública SSH]

Forneça os valores apropriados para as credenciais a seguir para autenticar o servidor [!DNL SFTP] usando a autenticação de chave pública SSH.

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O nome ou endereço IP associado ao servidor [!DNL SFTP]. |
| `port` | A porta do servidor [!DNL SFTP] à qual você está se conectando. Se não for fornecido, o valor padrão será `22`. |
| `username` | O nome de usuário com acesso ao servidor [!DNL SFTP]. |
| `password` | A senha do servidor [!DNL SFTP]. |
| `privateKeyContent` | O conteúdo da chave privada SSH codificada na Base64. Os tipos de chave OpenSSH com suporte são `ed25519`, `RSA` e `DSA`. |
| `passPhrase` | A senha para descriptografar a chave privada se o arquivo de chave ou o conteúdo da chave estiver protegido por uma senha. Se PrivateKeyContent estiver protegida por senha, esse parâmetro precisará ser usado com a senha de PrivateKeyContent como valor. |
| `maxConcurrentConnections` | Esse parâmetro permite especificar um limite máximo para o número de conexões simultâneas que a Experience Platform criará ao se conectar ao servidor SFTP. Você deve definir esse valor como menor que o limite definido pelo SFTP. **Observação**: quando esta configuração é habilitada para uma conta SFTP existente, ela afeta apenas os fluxos de dados futuros, não os existentes. |
| `folderPath` | O caminho para a pasta à qual você deseja fornecer acesso. [!DNL SFTP] origem, você pode fornecer o caminho da pasta para especificar o acesso do usuário à subpasta de sua escolha. |
| `disableChunking` | Durante a assimilação de dados, a origem [!DNL SFTP] pode recuperar o comprimento do arquivo primeiro, dividir o arquivo em várias partes e lê-los simultaneamente. Você pode habilitar ou desabilitar esse valor para especificar se o servidor [!DNL SFTP] pode recuperar comprimentos de arquivo ou ler dados de um deslocamento específico. |
| `connectionSpec.id` | (Somente API) A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL SFTP] é: `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

>[!ENDTABS]

## Conectar SFTP à Experience Platform

A documentação abaixo fornece informações sobre como conectar um servidor SFTP ao Experience Platform usando APIs ou a interface do usuário:

### Uso das APIs

* [Criar uma conexão básica SFTP usando a API do serviço de fluxo](../../tutorials/api/create/cloud-storage/sftp.md)
* [Explore a estrutura de dados e o conteúdo de uma fonte de armazenamento na nuvem usando a API do serviço de fluxo](../../tutorials/api/explore/cloud-storage.md)
* [Criar um fluxo de dados para uma fonte de armazenamento na nuvem usando a API do Serviço de fluxo](../../tutorials/api/collect/cloud-storage.md)

### Uso da interface

* [Criar uma conexão de origem SFTP na interface](../../tutorials/ui/create/cloud-storage/sftp.md)
* [Criar um fluxo de dados para uma conexão de armazenamento na nuvem na interface](../../tutorials/ui/dataflow/batch/cloud-storage.md)
