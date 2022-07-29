---
title: Hosts SFTP
description: Saiba como configurar tags na Adobe Experience Platform para fornecer builds de biblioteca a um servidor SFTP seguro e auto-hospedado.
exl-id: 3c1dc43b-291c-4df4-94f7-a03b25dbb44c
source-git-commit: a0f22bad4a18936ba7c59d3747f8dd34f3de5ca4
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 38%

---

# Hosts SFTP

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

O Adobe Experience Platform permite fornecer builds de biblioteca de tags para um servidor SFTP seguro que você hospeda, fornecendo maior controle sobre como as builds são armazenadas e gerenciadas. Este guia aborda como configurar um host SFTP para uma propriedade de tag na interface do usuário da coleta de dados.

>[!NOTE]
>
>Você também pode optar por usar um host gerenciado pelo Adobe. Consulte o guia sobre [Hosts gerenciados pelo Adobe](./managed-by-adobe-host.md) para obter mais informações.
>
>Para obter informações sobre os benefícios e limitações das bibliotecas de auto-hospedagem, consulte o [guia de auto-hospedagem](./self-hosting-libraries.md).

## Configurar uma chave de acesso para o servidor {#access-key}

O Platform se conecta com seu site SFTP usando uma chave criptografada. Há algumas etapas para configurar isso corretamente:

### Criar um par de chaves públicas/privadas

Você deve ter um par de chaves pública/privada instalado no servidor SFTP. Você pode gerar essas chaves no servidor ou em outro lugar e instalá-las no servidor. Consulte a documentação do GitHub sobre [como gerar chaves SSH](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key) para obter mais informações.

### Criptografar suas chaves

A chave privada é usada para criptografar a chave pública. Será necessário fornecer a chave privada durante o processo de criação do host SFTP. Consulte a seção sobre [como criptografar valores](../../../api/guides/encrypting-values.md) no guia API Reator para obter instruções sobre como criptografar chaves públicas. Use a chave GPG do ambiente de produção, a menos que você saiba que precisa de uma específica. Por fim, você pode criptografar sua chave privada de qualquer computador e não precisa instalar o GPG no servidor para concluir essa etapa.

### lista de permissões endereços IP da plataforma

Talvez seja necessário aprovar um conjunto de endereços IP a serem usados no firewall da empresa para permitir que a Platform alcance seu servidor SFTP e se conecte a ele. Esses endereços IP são:

* `184.72.239.68`
* `23.20.85.113`
* `54.226.193.184`

>[!NOTE]
>
>A estrutura das builds de tag mudou com o tempo. Eles usam links simbólicos (symlinks) internamente para manter a compatibilidade com versões anteriores, para que os códigos incorporados anteriores continuem a funcionar com a estrutura de build mais recente. O servidor SFTP deve aceitar o uso de symlinks a fim de servir como destino válido para builds de tag.

Para obter informações mais detalhadas, consulte o artigo a seguir do Medium sobre [como configurar servidores SFTP para fornecer um build](https://medium.com/launch-by-adobe/configuring-an-sftp-server-for-use-with-adobe-launch-bc626027e5a6).

## Criar um host SFTP {#create}

Na interface do usuário da coleta de dados, selecione **[!UICONTROL Hosts]** no painel de navegação esquerdo, seguido de **[!UICONTROL Adicionar host]**.

![Imagem que mostra o botão Adicionar host selecionado na interface do usuário](../../../images/ui/publishing/sftp-hosts/add-host-button.png)

A caixa de diálogo de criação do host é exibida. Forneça um nome para o host e em **[!UICONTROL Tipo]**, selecione **[!UICONTROL SFTP]**.

![Imagem que mostra a opção de hospedagem SFTP selecionada](../../../images/ui/publishing/sftp-hosts/select-sftp.png)

### Configurar o host SFTP {#configure}

A caixa de diálogo é expandida para incluir opções de configuração adicionais para o host SFTP. Elas são explicadas abaixo.

![Imagem mostrando os detalhes necessários para uma conexão de host SFTP](../../../images/ui/publishing/sftp-hosts/host-details.png)

| Campo Configuração | Descrição |
| --- | --- |
| [!UICONTROL Não Usar Symlinks] | Por padrão, todos os hosts SFTP usam links simbólicos (symlinks) para fazer referência à biblioteca [builds](../builds.md) que são salvas no servidor. No entanto, nem todos os servidores suportam o uso de links simbólicos. Quando essa opção é selecionada, o host usa uma operação de cópia para atualizar os ativos de criação diretamente, em vez de usar links simbólicos. |
| [!UICONTROL URL do servidor SFTP] | O caminho base do URL do seu servidor. |
| [!UICONTROL Path] | O caminho a ser anexado ao URL do servidor base para esse host. |
| [!UICONTROL Porta ] | A porta deve ser uma das seguintes:<ul><li>`21`</li><li>`22`</li><li>`80`</li><li>`200-299`</li><li>`443`</li><li>`2000-2999`</li><li>`4343`</li><li>`8080`</li><li>`8888`</li></ul>Como prática recomendada de segurança, a Adobe limita o número de portas que podem ser usadas para tráfego de saída. As portas selecionadas geralmente são permitidas por meio de firewalls corporativos e incluem alguns intervalos para oferecer flexibilidade. |
| [!UICONTROL Nome de usuário] | O nome de usuário a ser usado ao acessar o servidor. |
| [!UICONTROL Chave privada criptografada] | A chave privada criptografada que você criou em um [etapa anterior](#access-key). |

Selecionar **[!UICONTROL Salvar]** para criar o host com a configuração selecionada.

![Imagem que mostra o host SFTP sendo salvo](../../../images/ui/publishing/sftp-hosts/save-host.png)

Quando você seleciona **[!UICONTROL Salvar]**, a conexão e a capacidade de entregar os arquivos ao servidor SFTP são testadas. A Platform cria uma pasta, grava um arquivo nessa pasta, verifica se o arquivo está lá e depois faz a limpeza. Se a conta de usuário no servidor SFTP (aquele anexado ao certificado seguro fornecido para a Platform) não tiver as permissões necessárias para executar essa ação, o host entrará em um status &quot;Falha&quot;.

## Próximas etapas

Este guia cobriu como configurar um servidor SFTP auto-hospedado para uso em tags. Depois que o host tiver sido estabelecido, você poderá associá-lo a um ou mais de seus [ambientes](../environments.md) para publicar bibliotecas de tags. Para obter mais informações sobre o processo de alto nível de ativação das funcionalidades de tags em suas propriedades da Web ou móveis, consulte o [visão geral da publicação](../overview.md).
