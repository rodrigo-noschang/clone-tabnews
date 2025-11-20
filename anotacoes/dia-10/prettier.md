O `editorconfig` ajuda a escrever o código no formato correto, mas ele não formata código que já foi escrito no formato errado. Pra preencher esse vazio, vamos usar o prettier, que é do car***o!

Pra tornar isso um pouco mais escalável e "distribuível" (outros colaboradores do projeto também se beneficiarem e seguirem as regras dele, vamos fazer uma instalação dele como um pacote dentro da aplicação: npm install prettier --save-dev).

Vamos criar um script pra fazer o prettier conferir o projeto todo, e se sua escrita segue o padrão dele.