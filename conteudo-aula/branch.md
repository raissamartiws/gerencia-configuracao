### O que é uma Branch? 🌿

Uma **branch** é uma linha de desenvolvimento independente dentro de um repositório Git. Ela permite que você trabalhe em uma funcionalidade, correção ou alteração **sem modificar diretamente a branch principal** do projeto.

Imagine o projeto como uma árvore:

```text
                    main
                     │
          ┌──────────┴──────────┐
          │                     │
    feature/login         feature/cadastro
          │                     │
      alterações            alterações
          │                     │
          └──────────┬──────────┘
                     │
                  Pull Request
                     ↓
                    main
```

### Para que serve?

A branch permite **separar diferentes tarefas** do projeto.

Por exemplo, em vez de fazer uma alteração diretamente na `main`:

```bash
git checkout main
# começa a desenvolver...
```

Você cria uma branch específica:

```bash
git checkout -b feature/login
```

Agora você pode desenvolver o **login** sem afetar a `main`.

Quando terminar:

```text
feature/login
      ↓
   commits
      ↓
Pull Request
      ↓
    revisão
      ↓
     main
```

### Exemplos de branches

Cada branch deve representar uma tarefa específica:

```text
main
├── feature/login
├── feature/cadastro-usuario
├── feature/tela-produtos
├── fix/correcao-validacao
└── docs/documentacao
```

Uma convenção comum é usar:

* `feature/` → nova funcionalidade
* `fix/` → correção de problema
* `docs/` → documentação
* `refactor/` → reorganização do código sem mudar a funcionalidade
* `test/` → criação ou alteração de testes

### Exemplo prático

Suponha que você recebeu a tarefa:

> Criar a tela de cadastro de usuários.

Você cria:

```bash
git checkout -b feature/cadastro-usuario
```

Faz as alterações e depois registra:

```bash
git add .
git commit -m "✨ feat: adiciona tela de cadastro de usuário"
```

Depois envia a branch para o GitHub:

```bash
git push origin feature/cadastro-usuario
```

E então pode abrir um **Pull Request** para que outra pessoa revise antes de entrar na `main`.

### Resumo:

> **Branch é uma ramificação do projeto usada para desenvolver uma tarefa isoladamente, permitindo trabalhar com segurança sem alterar diretamente a versão principal do código.**
