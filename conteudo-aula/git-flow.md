# Git Flow

## O que é Git Flow?

Git Flow é um modelo de organização de branches do Git. Ele define como o código deve ser desenvolvido, revisado, preparado para publicação e corrigido em produção.

O objetivo é separar o desenvolvimento de novas funcionalidades das versões estáveis da aplicação. Dessa forma, a equipe consegue trabalhar em várias tarefas ao mesmo tempo, mantendo a branch de produção protegida.

> Git Flow é um modelo de trabalho. Ele não é um comando específico do Git e não substitui a revisão de código, os testes ou a integração contínua.

## Branches principais

### `main`

Contém o código pronto para produção. Cada alteração incorporada nessa branch deve representar uma versão estável e utilizável do sistema.

### `develop`

É a branch de integração do desenvolvimento. As novas funcionalidades são reunidas nela antes de serem preparadas para uma versão de produção.

Em equipes que preferem um fluxo mais simples, `main` pode ser a única branch permanente. Nesse caso, o Git Flow tradicional é adaptado para o uso de branches curtas de funcionalidade e pull requests.

## Branches auxiliares

### `feature/*`

Usadas para desenvolver uma nova funcionalidade. São criadas a partir de `develop` e, quando concluídas, retornam para `develop` por meio de merge ou pull request.

Exemplo: `feature/tela-login`

### `release/*`

Usadas para preparar uma nova versão. Nessa etapa podem ser feitos ajustes finais, como correções de bugs, atualização da documentação e alteração do número da versão.

São criadas a partir de `develop` e normalmente incorporadas tanto em `main` quanto em `develop`.

Exemplo: `release/1.2.0`

### `hotfix/*`

Usadas para corrigir problemas urgentes encontrados em produção. São criadas a partir de `main` e, depois da correção, incorporadas em `main` e `develop` para que o ajuste não seja perdido no próximo ciclo de desenvolvimento.

Exemplo: `hotfix/corrige-erro-pagamento`

## Fluxo de trabalho

O fluxo tradicional pode ser representado assim:

```text
main     o---------o-------------------o---------o
			 \       /                     \       /
develop    o-----o-------o------o--------o-----o
						\     /        \
feature             o---o          release
```

Na prática, o processo costuma seguir estas etapas:

1. Atualizar a branch de origem:

   ```bash
   git switch develop
   git pull origin develop
   ```

2. Criar uma branch para a funcionalidade:

   ```bash
   git switch -c feature/tela-login
   ```

3. Implementar a funcionalidade e registrar os commits:

   ```bash
   git add .
   git commit -m "Adiciona tela de login"
   ```

4. Publicar a branch no repositório remoto:

   ```bash
   git push -u origin feature/tela-login
   ```

5. Abrir um pull request de `feature/tela-login` para `develop`. Depois da revisão e da aprovação dos testes, a branch pode ser incorporada.

6. Quando houver funcionalidades suficientes para uma versão, criar uma branch de release:

   ```bash
   git switch develop
   git pull origin develop
   git switch -c release/1.0.0
   ```

7. Após a validação, incorporar a release em `main`, criar uma tag e atualizar `develop`:

   ```bash
   git switch main
   git merge --no-ff release/1.0.0
   git tag -a v1.0.0 -m "Versão 1.0.0"
   git push origin main --tags

   git switch develop
   git merge --no-ff release/1.0.0
   git push origin develop
   ```

8. Para uma correção urgente em produção, criar uma branch de hotfix a partir de `main`:

   ```bash
   git switch main
   git pull origin main
   git switch -c hotfix/corrige-erro-pagamento
   ```

   Depois da correção e dos testes, incorporar o hotfix em `main` e em `develop`.

## Convenções recomendadas

- Use nomes objetivos para as branches, como `feature/cadastro-usuario` e `fix/validacao-email`.
- Faça commits pequenos e com mensagens que expliquem a alteração.
- Atualize a branch antes de começar uma tarefa para reduzir conflitos.
- Execute os testes antes de abrir um pull request.
- Evite fazer commits diretamente em `main` e `develop` sem revisão.
- Remova branches auxiliares depois que forem incorporadas, quando não houver motivo para mantê-las.
- Use tags para identificar versões publicadas, como `v1.0.0`.

## Vantagens e limitações

### Vantagens

- Define responsabilidades para cada tipo de branch.
- Isola funcionalidades em desenvolvimento do código de produção.
- Facilita o planejamento e a preparação de versões.
- Permite tratar correções urgentes sem interromper todo o desenvolvimento.

### Limitações

- Pode criar muitas branches e aumentar a complexidade do processo.
- Merges frequentes são necessários para evitar que as branches fiquem desatualizadas.
- Pode ser excessivo para equipes pequenas ou projetos com deploy contínuo.

Por isso, o Git Flow deve ser adaptado ao contexto do projeto que está sendo desenvolvido. Para produtos que publicam alterações várias vezes ao dia, um fluxo baseado em `main`, branches curtas e integração contínua pode ser mais adequado.
