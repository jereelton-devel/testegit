
# CONFIGURAR GIT NO WINDOWS VIA TERMINAL (GITBASH) USANDO MAIS DE UMA CHAVE SSH

>NOTA:
>- O GitHuub também pode ser instalado o GitHub for Windows, com o 
qual é possível fazer login na conta do git apenas com 
usuário e senha, sem a necessidade de gerar chaves
>- Pode ser necessário remover as credencias criadas anteriormente no Windows para acesso ao GitHub.

#1 - Instalar Git Bash

https://git-scm.com/

#2 - Configurar Git Local
<pre>
git config --global user.name "Nome Sobrenome" //Como esta no github
git config --global user.email "seu@email.com" //Como esta no github
</pre>

#3 - Gerar as chaves SSH

ssh-keygen -t rsa -C "seu@email.com"

* Configurar o nome da chave, ex:
[PROMPT CMD]<br />
Enter file in which to save the key (/c/Users/Jereelton Teixeira/.ssh/id_rsa):/c/Users/Jereelton Teixeira/.ssh/id_rsa_chave1_desktop_devel<br />
* Criar uma senha para o arquivo e pronto.

* Obter a chave gerada
<pre>
cd ~/.ssh/<br />
cat ~/.ssh/id_rsa_chave1_desktop_devel.pub<br />
ssh-rsa 9A6AB3NzaC1yc2EAAAADAQABAAABgQDbK5YvLmvzufc7kUZqHxDZdjVW0S/mKuRECtjj9J5bOz71ACX+txdEWPv2tF0BCm82xXYuOZIvFLAM/OL+R8KHGzan1zYIQ1xObf31AOf01B0CNjvZ2Bt5efsOzR6CDuT7L0a5gC2e4KaizDhXECXTv34y9vU6vTrzyxNvA/xFWafzUy7JqVeazHHwASD6k6FhESKayEn7hVaYlYE6v9S/4wFvPXbnAAQsogqk2yubuOxzwZvVu5NLwLw0Ln0QVR1mtlpNEg13+9SOa/keoi/AI7zP/r9zA236pHFb6T50UzKig3rkpz+9OBKn6weffTkzar6SuIG+SegLF9xJHA7M4UCzYuQcSdslm2A+GnLQgRmccVViZJvnglfsSL/6VVBJRzYNPqQvnw8BXlVc6IsuOT+lg7PUQ1kkXlySTIKEnGSOnNVYE6bx/zsnMJjUANegdFy8NLJBfHNl0VMMPGggBK6EUbaKTy1yUjC7OCrmnRktpjrGn5T2c864mp88bdk= seu@email.com
</pre>

#4 - Configurar sua conta no GitHub
>Settings>SSH and GPG Keys>New SSH key>Add Key
!Colar todo o conteudo da chave gerada no input de entrada [Key]

#5 - Criar e Configurar arquivo "config" na pasta .ssh

<pre>
Host chave1_desktop_devel.github.com (Chave personalizada)<br />
    HostName github.com<br />
    PreferredAuthentications publickey<br />
    IdentityFile ~/.ssh/id_rsa_chave1_desktop_devel<br />

Host github.com (Essa é a configuração padrão)<br />
    HostName github.com<br />
    PreferredAuthentications publickey<br />
    IdentityFile ~/.ssh/id_rsa<br />
</pre>

#6 - Autenticação no git
<pre>
ssh -T git@chave1_desktop_devel.github.com
</pre>
>Informar a senha criada na etapa 3

#7 - Clonar um projeto do seu git, ou iniciar um git e criar um novo projeto no git

<pre>
git init (opcional)
git clone https://github.com/jereelton-devel/testegit.git
</pre>

#8 - Para os casos de "fatal: remote origin already exists" usar o seguinte comando
<pre>
git remote set-url origin git@chave1_desktop_devel.github.com:conta_no_git/projeto_no_git.git
</pre>

#9 - Testar as configurações
<pre>
git status
git add --all
git commit -m 'Comentario'
git push
</pre>

A senha criada na etapa 3 devera ser informada durante o commit

Feito !



