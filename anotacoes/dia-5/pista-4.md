# Consertando o commit

Ele fez um commit criando o .gitignore, e colocou o `.next` dentro dele. Mas depois que fez o commit viu que deveria ter incluído também o `node_modules`. Poderia só inlcuir ele no arquivo e fazer um novo commit, mas dá pra fazer melhor, dá pra `remendar` esse commit.

```
git commit --ammend -m 'Nova mensagem de commit'
```

Esse `ammend` faz com que a nova alteração faça parte do "commit anterior" - na verdade é sim um novo commit (um novo HEAD), mas ele reaproveita as alterações do ultimo commit.

## Como fica com 2 commits diferentes

Faz o primeiro commit:
Commit 1 - hash abc123 - 1mensagem: "Adicionei o .next no .gitignore"

Faz o segundo commit:
Commit 2 - hash def456 - mensagem: "Adicionei o node_modules no .gitignore".

Histórico mostra:
Commit 1 - hash abc123 - 1mensagem: "Adicionei o .next no .gitignore"
Commit 2 - hash def456 - mensagem: "Adicionei o node_modules no .gitignore".

## Como fica com o ammend

Faz o primeiro commit
Commit 1 - hash abc123 - 1mensagem: "Adicionei o .next no .gitignore".

Faz o ammend
Commit 2 (ammend) - mensagem: "Adicionei o .next e o node_modules no .gitignore".

Histórico mostra:
Commit 1 - hash ghi789 - mensagem: "Adicionei o .next e o node_modules no .gitignore"

