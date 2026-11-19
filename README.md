# NVM 2.0 NO WINDOWS 11 — NODE.JS AUTOMÁTICO POR PROJETO

Guia rápido para instalar o **NVM for Windows 2.x** com **Winget**, gerenciar versões do Node.js e selecionar automaticamente a versão correta para cada projeto usando um arquivo `.nvmrc`.

## Requisitos

- Windows 11
- PowerShell
- Winget disponível (`winget --version`)

> Também funciona ao executar `node`, `npm` e outros comandos no terminal Git Bash integrado ao VS Code, desde que o NVM esteja disponível no `PATH`.

## 1. Instalar o NVM pelo PowerShell

Abra o **PowerShell** e execute:

```powershell
winget install nvm-windows
```

Depois, abra um novo terminal e confirme a instalação:

```powershell
nvm version
```

> Se o comando não for encontrado imediatamente, feche e reabra o PowerShell ou o VS Code para atualizar as variáveis de ambiente.

## 2. Verificar a configuração automática

No NVM 2.x, o modo `shim` e a configuração `auto_use=true` já vêm habilitados por padrão. Portanto, **normalmente não é necessário configurar nada**.

Para conferir:

```powershell
nvm config get mode auto_use
```

Se precisar ativar explicitamente, execute:

```powershell
nvm config set mode=shim
nvm config set auto_use=true
```

O modo `shim` permite que o NVM selecione a versão do Node.js de acordo com a configuração do projeto, sem trocar a versão global a cada mudança de pasta.

## 3. Instalar versões do Node.js

Instale as versões necessárias para seus projetos (exemplos):

```powershell
nvm install 18
nvm install 20
nvm install 22
```

Consulte as versões instaladas:

```powershell
nvm list
```

## 4. Criar o arquivo `.nvmrc` em cada projeto

Na **raiz de cada projeto**, crie um arquivo chamado **`.nvmrc`** (sem extensão adicional). Dentro dele, coloque somente a versão desejada do Node.js.

Exemplo de organização:

```text
projetos/
├── projeto-angular/
│   └── .nvmrc   # conteúdo: 18
├── projeto-react/
│   └── .nvmrc   # conteúdo: 20
└── projeto-api/
    └── .nvmrc   # conteúdo: 22
```

Para criar o arquivo pelo PowerShell, dentro da pasta do projeto:

```powershell
'22' | Set-Content .nvmrc
```

Você também pode informar uma versão completa, como `22.15.0`, desde que esteja instalada.

**Recomendação:** adicione o `.nvmrc` ao Git para que outras pessoas do projeto saibam qual versão do Node.js utilizar.

## 5. Testar a seleção automática

Execute o comando `node -v` dentro de cada projeto:

```powershell
cd C:\projetos\projeto-angular
node -v

cd C:\projetos\projeto-react
node -v

cd C:\projetos\projeto-api
node -v
```

O NVM 2.x identificará o `.nvmrc` da pasta e usará a versão correspondente ao executar o Node.js. **Não é necessário executar `nvm use` toda vez que mudar de projeto.**

> Se uma versão indicada pelo `.nvmrc` não estiver instalada, instale-a usando `nvm install <versão>`. A instalação automática de versões ausentes é uma configuração separada e não vem ativada por padrão.

## Comandos úteis

| Comando | Finalidade |
| --- | --- |
| `nvm version` | Exibe a versão do NVM |
| `nvm list` | Lista versões instaladas do Node.js |
| `nvm install 22` | Instala uma versão do Node.js |
| `nvm config get mode auto_use` | Consulta as opções de seleção automática |
| `nvm config set mode=shim` | Ativa o modo de resolução por projeto |
| `nvm config set auto_use=true` | Habilita o uso automático da versão detectada |
| `node -v` | Exibe a versão do Node.js usada no diretório atual |

## Referências

- [Documentação oficial — instalação do NVM for Windows](https://docs.nvm-windows.com/install/installers/)
- [Documentação oficial — configurações](https://docs.nvm-windows.com/cfg/core/)
- [Documentação oficial — modos de operação](https://docs.nvm-windows.com/features/modes/)
- [Repositório oficial do NVM for Windows](https://github.com/nvm-windows/nvm)
