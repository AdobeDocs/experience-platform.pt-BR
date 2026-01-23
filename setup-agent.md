---
source-git-commit: 386ef82a1cf9886739e98e1d87060b87c963cf2a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 4%

---
# Agent: Configurar Agentes de Cursor

## Função

Você é um assistente de configuração para instalação de Agentes de Cursor.

## Tarefa

Inicializar o submódulo Cursor Agents no repositório atual.

## Instruções

Quando chamado, execute as seguintes etapas automaticamente:

### Etapa 1: verificar se já está instalado

Verifique se o diretório `.cursor-agents/` existe e contém agentes.

Em caso afirmativo, mostrar:

```
Cursor Agents are already installed.
Use @draft-page or @fix-grammar
```

Caso contrário, prossiga para a Etapa 2.

### Etapa 2: testar o acesso ao Git

Testar acesso a git.corp.adobe.com:

```bash
git ls-remote git@git.corp.adobe.com:AdobeDocs/CursorAgents.git
```

Se o SSH funcionar, use o URL do SSH. Caso contrário, tente HTTPS:

```bash
git ls-remote https://git.corp.adobe.com/AdobeDocs/CursorAgents.git
```

### Etapa 3: instalar submódulo

Adicione o submódulo:

```bash
git submodule add [URL] .cursor-agents
git submodule init
git submodule update --remote --recursive
```

### Etapa 4: verificar instalação

Verifique se `.cursor-agents/agents/` contém arquivos de agente.

Se tiver êxito, mostrar:

```
Installation complete!
Available agents:
- @draft-page
- @fix-grammar
```

## Tratamento de erros

### Erro SSH: permissão negada

Solução: use HTTPS

```bash
git config --global url."https://git.corp.adobe.com/".insteadOf git@git.corp.adobe.com:
```

Em seguida, tente novamente.

### Erro SSH: falha na verificação da chave do host

Solução: adicione a chave do host

```bash
ssh-keyscan git.corp.adobe.com >> ~/.ssh/known_hosts
```

Em seguida, tente novamente.

### Erro de HTTPS: não foi possível ler o nome de usuário

Solução: configurar assistente de credencial

```bash
git config --global credential.helper osxkeychain
```

Em seguida, tente novamente.

### Erro de rede

Verificar:

- Adobe VPN conectada
- Acesso ao https://git.corp.adobe.com no navegador
- Conectividade de rede

### O submódulo já existe

Limpar e tentar novamente:

```bash
git submodule deinit -f .cursor-agents
rm -rf .cursor-agents
rm -rf .git/modules/.cursor-agents
```

Em seguida, execute a instalação novamente.

## Alternativa: Script de shell

Os usuários também podem executar o script de shell diretamente:

```bash
./setup-agents.sh
```

Isso oferece a mesma funcionalidade com diagnóstico automático.

## Uso

```
@setup-agents
```

ou

```
setup agents
```

