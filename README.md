# Tutorial: instalando o MiKTeX

O MiKTeX é uma distribuição LaTeX para Linux e Windows. Este guia mostra como instalá-lo nos dois sistemas e, ao final, como atualizar sua branch com as mudanças do repositório remoto.

## Linux

Os passos abaixo valem para Ubuntu e Debian. O MiKTeX não faz parte dos repositórios oficiais dessas distribuições, então é preciso adicionar o repositório dele.

### 1. Adicione a chave e o repositório do MiKTeX

Descubra o codinome da sua versão com `lsb_release -cs` (por exemplo, `jammy` no Ubuntu 22.04 ou `noble` no Ubuntu 24.04). Depois execute:

```bash
sudo apt update
sudo apt install -y curl gnupg ca-certificates
curl -fsSL https://miktex.org/download/key | sudo tee /usr/share/keyrings/miktex-keyring.asc > /dev/null
echo "deb [signed-by=/usr/share/keyrings/miktex-keyring.asc] https://miktex.org/download/ubuntu $(lsb_release -cs) universe" | sudo tee /etc/apt/sources.list.d/miktex.list
```

No Debian, troque `ubuntu` por `debian` na linha do `echo`.

### 2. Instale o pacote

```bash
sudo apt update
sudo apt install miktex
```

### 3. Configure a instalação automática de pacotes

Assim o MiKTeX baixa sozinho os pacotes que forem necessários durante a compilação:

```bash
initexmf --set-config-value=[MPM]AutoInstall=1
```

### 4. Verifique a instalação

```bash
pdflatex --version
```

Se o comando exibir a versão instalada, o MiKTeX está configurado corretamente.

---

## Windows

### 1. Baixe o instalador

Acesse [miktex.org/download](https://miktex.org/download) e baixe o **Basic MiKTeX Installer** (64 bits).

### 2. Execute o instalador

- Escolha a instalação para o seu usuário ou para todos os usuários do computador.
- Mantenha marcada a opção de adicionar o MiKTeX ao `PATH`, se ela aparecer.
- Na opção de instalação de pacotes sob demanda (*Install missing packages on-the-fly*), deixe a instalação automática ativada, para que o MiKTeX baixe os pacotes que faltarem na primeira compilação.

### 3. Verifique a instalação

Abra o **PowerShell** ou o **Prompt de Comando** e execute:

```powershell
pdflatex --version
```

Se a versão for exibida, a instalação está funcionando. Caso o comando não seja reconhecido, feche e abra o terminal novamente para que o `PATH` seja atualizado.

---

## Atualizando sua branch com o repositório remoto

Os comandos abaixo baixam as atualizações da branch remota e as aplicam na sua branch local. Substitua `<sua-branch>` pelo nome da sua branch (por exemplo, `luri`).

### 1. Guarde alterações locais não commitadas (se houver)

```bash
git status
git stash
```

### 2. Baixe as atualizações do remoto

O `fetch` apenas traz as informações do remoto e não altera a sua branch:

```bash
git fetch origin
```

### 3. Aplique as atualizações

Escolha **uma** das opções:

**Opção A: rebase** (mantém o histórico linear, reaplicando seus commits sobre a versão remota):

```bash
git rebase origin/<sua-branch>
```

**Opção B: merge** (cria um commit de integração com as mudanças remotas):

```bash
git merge origin/<sua-branch>
```

Use o rebase apenas em commits que ainda não foram enviados ao remoto ou que você é a única pessoa usando a branch. Se já tiver enviado os commits e outras pessoas trabalharem na mesma branch, prefira o merge.

Se houver conflitos, resolva os arquivos indicados, marque-os com `git add <arquivo>` e continue com:

```bash
git rebase --continue   # no caso do rebase
git commit              # no caso do merge
```

Para desfazer um rebase em andamento, use `git rebase --abort`.

### 4. Restaure as alterações guardadas (se usou o stash)

```bash
git stash pop
```
