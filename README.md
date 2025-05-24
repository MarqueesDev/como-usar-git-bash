# Como usar Git simples

<h2>Fluxo de trabalho</h2>

<p>Seus repositórios locais consistem em três "árvores" mantidas pelo Git. A primeira delas é seu <code>Working Directory</code>, que contém os arquivos do seu projeto. A segunda é o <code>Index</code> (também chamado de <code>Staging Area</code>), que funciona como uma área temporária onde os arquivos ficam preparados antes de serem confirmados. E por fim, o <code>HEAD</code>, que aponta para o último commit (confirmação) que você fez.</p>

---

## Após a instalação do Git

<h2>Configurando o Git</h2>

<p>Configure seu e-mail de acordo com a conta que você vai usar no Git:</p>

```bash
git config --global user.email "seuemail@gmail.com"
```

<p>Configure também seu nome de usuário, que aparecerá nos commits:</p>

```bash
git config --global user.name "seunome"
```

<h3>Configurar qual editor usar no Git</h3>

<p>Por padrão, o Git utiliza o editor de texto padrão do sistema (que em muitos casos é o <code>vi</code>) para editar mensagens de commits. Para usar outro editor (como o Atom, VS Code, Notepad++ etc.), utilize a configuração <code>core.editor</code>. Exemplo:</p>

```bash
git config --global core.editor atom
```

<p>Agora, o Git vai utilizar o Atom como editor padrão para editar mensagens de commit e outras operações como rebase interativo.</p>

---

## Criando um novo repositório

<h2>Iniciando um repositório local</h2>

<p>Crie uma nova pasta, abra-a e execute o comando:</p>

```bash
git init
```

<p>Esse comando cria um novo repositório Git vazio na pasta.</p>

---

## Adicionando um repositório remoto

<p>Para conectar seu repositório local a um repositório remoto (como o do GitHub), use o comando:</p>

```bash
git remote add origin https://github.com/seuusuario/seurepositorio.git
```

<p>Esse comando adiciona um "controle remoto" chamado <code>origin</code>, que aponta para o endereço do repositório remoto.</p>

<p>⚠️ No entanto, pode acontecer de o Git não saber automaticamente que o <code>main</code> local deve ser vinculado ao <code>main</code> remoto. Isso pode causar erro ao usar <code>git pull</code> ou <code>git push</code>.</p>

<p>Nesse caso, use:</p>

```bash
git branch --set-upstream-to=origin/main main
```

<p>Ou simplesmente use:</p>

```bash
git push -u origin main
```

<p>O parâmetro <code>-u</code> configura o <code>upstream</code> da sua branch local para o remoto. Assim, nas próximas vezes, você pode usar apenas:</p>

```bash
git push
```

<p>Se quiser desvincular uma branch do repositório remoto, use:</p>

```bash
git branch --unset-upstream
```

<p>Se os históricos do repositório local e remoto forem diferentes, o Git pode bloquear o push. Para forçar a sobreposição (atenção: isso apaga o conteúdo remoto!), use:</p>

```bash
git push origin main --force
```

<p>Se quiser combinar os dois históricos (local e remoto), use o comando:</p>

```bash
git pull origin main --allow-unrelated-histories
```

---

## Clonando um repositório existente

<h2>Copiando um projeto remoto para sua máquina</h2>

<p>Para clonar um repositório e criar uma cópia local completa com histórico, branches e arquivos:</p>

```bash
git clone https://github.com/seuusuario/seurepositorio.git
```

---

## Apagando arquivos do repositório local

<p>Para remover arquivos da pasta local (sem afetar o repositório remoto):</p>

```bash
rm -r nome-do-arquivo
```

<p>Para apagar vários arquivos de uma vez:</p>

```bash
rm -r arquivo1.txt arquivo2.txt arquivo3.txt
```

<p>Ou para apagar tudo:</p>

```bash
rm -r .
```

⚠️ Use com cuidado!

---

## Trabalhando com branches

<p>Trocar de branch existente:</p>

```bash
git checkout nome-da-branch
```

<p>Criar e já trocar para uma nova branch:</p>

```bash
git checkout -b nova-branch
```

<p>Criar uma nova branch (sem trocar):</p>

```bash
git branch nova-branch
```

<p>Excluir uma branch local:</p>

```bash
git branch -d nome-da-branch
```

<p>Excluir uma branch remota:</p>

```bash
git push origin --delete nome-da-branch
```

<p>Listar branches locais:</p>

```bash
git branch
```

<p>Listar branches locais e remotas:</p>

```bash
git branch -a
```

---

## Atualizando branches remotas

<p>Para atualizar referências remotas e remover branches deletadas:</p>

```bash
git fetch --prune --all
```

---

## Adicionando arquivos para a staging area (Index)

<p>Adicionar um arquivo específico:</p>

```bash
git add nome-do-arquivo
```

<p>Adicionar todos os arquivos modificados:</p>

```bash
git add .
```

---

## Removendo arquivos da staging area

<p>Se adicionou um arquivo por engano:</p>

```bash
git reset nome-do-arquivo
```

<p>Ou para remover todos da staging area:</p>

```bash
git reset .
```

---

## Fazendo e desfazendo commits

<p>Para registrar suas alterações:</p>

```bash
git commit -m "descrição das mudanças"
```

<h4>Editar a mensagem do último commit</h4>

```bash
git commit --amend -m "Nova mensagem"
```

<h4>Adicionar arquivos ao último commit (sem alterar a mensagem)</h4>

```bash
git add .
git commit --amend --no-edit
```

<h4>Desfazer o último commit (mantendo os arquivos)</h4>

```bash
git reset HEAD~
```

<p>Para remover arquivos apenas da staging area (sem apagar do disco):</p>

```bash
git rm --cached nome-do-arquivo
git rm --cached -r .
```

---

## Usando o comando git pull

<p>Atualize sua branch local com o conteúdo remoto:</p>

```bash
git pull
```

<p>Ou especificamente:</p>

```bash
git pull origin main
```

<p>Para evitar commits de merge desnecessários e manter o histórico limpo:</p>

```bash
git pull origin main --rebase
```

---

## Usando o comando git push

<p>Após commitar suas alterações, envie para o repositório remoto:</p>

```bash
git push origin main
```

<p>Para evitar ter que digitar isso sempre, defina o upstream com:</p>

```bash
git push --set-upstream origin main
```

<p>Depois disso, basta usar:</p>

```bash
git push
```

---

## Comandos complementares

### Git fetch

```bash
git fetch
```

<p>Busca atualizações do repositório remoto sem aplicar no seu código.</p>

### Git merge

```bash
git merge nome-da-branch
```

<p>Mescla uma branch com a atual.</p>

---

## Remoção forçada de arquivos

### Diferença entre `rm -r` e `rm -rf`

- <code>rm -r</code>: remove pastas e arquivos de forma recursiva (pede confirmação em alguns casos).
- <code>rm -rf</code>: remove tudo de forma forçada, sem pedir confirmação.

⚠️ Use com cuidado, pois não há volta.

---

## Gerenciando arquivos grandes com Git LFS

<p>Se você trabalha com arquivos pesados (como vídeos, imagens grandes, projetos de design, etc.), o Git normal não é eficiente para lidar com eles. Para isso, usamos o <strong>Git LFS (Large File Storage)</strong>.</p>

<h3>Instalação do Git LFS</h3>

<p>Acesse <a href="https://git-lfs.github.com/">https://git-lfs.github.com/</a> e instale.</p>

<h3>Configurando no repositório</h3>

```bash
git lfs install
```

<p>Depois, adicione o tipo de arquivo a ser tratado pelo LFS:</p>

```bash
git lfs track "*.psd"
```

<p>Isso cria (ou edita) um arquivo chamado <code>.gitattributes</code>, que registra os arquivos controlados via LFS.</p>

<p>Agora é só adicionar, commitar e fazer push normalmente:</p>

```bash
git add .gitattributes
git add nome-do-arquivo.psd
git commit -m "Adicionando arquivo grande com LFS"
git push origin main
```

---

## Caminhos longos no Windows

<p>Se você estiver usando Windows e tiver erros como:</p>

```
error: could not lock config file C:/Program Files/Git/etc/gitconfig: Permission denied
```

<p>Isso pode acontecer porque o Git no Windows, por padrão, não permite caminhos longos. Para resolver:</p>

```bash
git config --system core.longpaths true
```

<p>⚠️ Execute o terminal como administrador.</p>
