---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Fonte da Zona de Aterrissagem de Dados
topic-legacy: overview
description: Saiba como conectar a Zona de aterrissagem de dados ao Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: ecc9bc603bfd7b56f5f232b0d6d91eb65a901510
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

[!DNL Data Landing Zone] é um [!DNL Azure Blob] interface de armazenamento provisionada pela Adobe Experience Platform, permitindo que você acesse um recurso de armazenamento de arquivos seguro e baseado em nuvem para trazer arquivos para a plataforma. Você tem acesso a um [!DNL Data Landing Zone] por sandbox, e o volume total de dados em todos os contêineres está limitado aos dados totais fornecidos com sua licença de Produtos e Serviços da plataforma . Todos os clientes da Platform e seus serviços de aplicativos, como [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services]e [!DNL Real-time Customer Data Platform] são provisionados com um [!DNL Data Landing Zone] contêiner por sandbox. Você pode ler e gravar arquivos no contêiner por meio de [!DNL Azure Storage Explorer] ou sua interface de linha de comando.

[!DNL Data Landing Zone] O suporta autenticação baseada em SAS e seus dados estão protegidos com o padrão [!DNL Azure Blob] mecanismos de segurança de armazenamento em repouso e em trânsito. A autenticação baseada em SAS permite que você acesse com segurança sua [!DNL Data Landing Zone] por meio de uma conexão pública com a Internet. Não são necessárias alterações de rede para que você acesse seu [!DNL Data Landing Zone] , o que significa que não é necessário configurar nenhuma configuração lista de permissões ou entre regiões para sua rede. A Platform impõe um TTL (time-to-live) estrito de sete dias em todos os arquivos carregados em um [!DNL Data Landing Zone] contêiner. Todos os arquivos são excluídos após sete dias.

## Restrições de nomenclatura para arquivos e diretórios

Esta é uma lista de restrições que você deve considerar ao nomear seus arquivos ou diretórios de armazenamento em nuvem.

- Os nomes de componentes de diretório e arquivo não podem exceder 255 caracteres.
- Os nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
- Os seguintes caracteres de URL reservados devem ser evitados corretamente: `! ' ( ) ; @ & = + $ , % # [ ]`
- Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
- Caracteres de caminho de URL inválidos não permitidos. Pontos de código como `\uE000`, embora válidas em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode, como caracteres de controle (como `0x00` para `0x1F`, `\u0081`e assim por diante), também não são permitidas. Para obter as regras que regem as cadeias de caracteres Unicode no HTTP/1.1, consulte [RFC 2616, Seção 2.2: Regras básicas](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (...) e dois caracteres de ponto (.).

## Connect [!DNL Data Landing Zone] para [!DNL Platform]

A documentação abaixo fornece informações sobre como trazer dados de seu [!DNL Data Landing Zone] para o Adobe Experience Platform usando APIs ou a interface do usuário.

### Uso de APIs

- [Crie um [!DNL Data Landing Zone] conexão de origem usando a API do Serviço de Fluxo](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Criar um fluxo de dados para uma fonte de armazenamento em nuvem usando a API do Serviço de Fluxo](../../tutorials/api/collect/cloud-storage.md)

### Uso da interface do usuário

- [Connect [!DNL Data Landing Zone] para Plataforma usando a interface do usuário](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [Criar um fluxo de dados para uma conexão de armazenamento em nuvem na interface do usuário do](../../tutorials/ui/dataflow/batch/cloud-storage.md)
