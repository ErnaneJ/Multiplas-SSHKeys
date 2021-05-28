# Múltiplas chaves SSH para GitHub e GitLab

## 1. Gerar Chaves SSH

``` bash
ssh-keygen -t rsa -C "user@email.com" -b 4096 -f ~/.ssh/id_rsa_github
ssh-keygen -t rsa -C "user@email.com" -b 4096 -f ~/.ssh/id_rsa_gitlab
```

## 2. Copiar chaves para GitHub e GitLab

``` bash
# Copiar chave pública para o GitHub
pbcopy < ~/.ssh/id_rsa_github.pub
# Em seguida colar no painel do GitHub

# Copiar chave pública para o GitLab
pbcopy < ~/.ssh/id_rsa_gitlab.pub
# Em seguida colar no painel do GitLab
```

## 3. Adicionar as chaves ao SSH-Agent

``` bash
ssh-add ~/.ssh/id_rsa_github
ssh-add ~/.ssh/id_rsa_gitlab
```

## 4. Arquivo de configuração

``` bash
touch ~/.ssh/config
nano ~/.ssh/config
```

**Arquivo** `config`

```
# Conta do GitHub
Host github.com
  HostName github.com
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/id_rsa_github

# Conta do GitLab
Host gitlab.com
  HostName gitlab.com
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/id_rsa_gitlab
```

## 5. Testando as conexões

``` bash
ssh -T git@github.com
yes
# Hi UserName! You've successfully authenticated, but GitHub does not provide shell access.

ssh -T git@gitlab.com
yes
# Welcome to GitLab, @UserName!
```