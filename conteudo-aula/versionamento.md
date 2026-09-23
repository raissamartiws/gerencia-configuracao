# O que é Versionamento no Git?

O **Git** é um sistema de controle de versão distribuído. Ele serve para registrar todas as alterações feitas em um conjunto de arquivos ao longo do tempo, permitindo que você volte para versões anteriores, trabalhe em equipe sem sobrescrever o código dos outros e organize o desenvolvimento em paralelo.

## Principais Conceitos

1. **Repositório (Repo):** A pasta do seu projeto que o Git monitora.
2. **Commit:** O "salvamento" oficial. Cada commit tira uma "foto" do seu código naquele momento, acompanhada de uma mensagem explicando o que mudou.
3. **Branch (Ramificação):** Uma linha de desenvolvimento independente. Permite criar novos recursos ou testar ideias sem mexer no código principal (`main` ou `master`).
4. **Merge:** O ato de juntar as alterações de uma branch de volta à branch principal.

## Comandos Essenciais

* `git init`: Cria um novo repositório Git na pasta atual.
* `git add .`: Prepara os arquivos modificados para o próximo commit.
* `git commit -m "mensagem"`: Salva as alterações preparadas com uma mensagem descritiva.
* `git status`: Mostra o estado atual dos arquivos (modificados, prontos para commit, etc.).
* `git push`: Envia seus commits locais para um repositório remoto (como o GitHub).
* `git pull`: Baixa e atualiza seu código local com as novidades do repositório remoto.