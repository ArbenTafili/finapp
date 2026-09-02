# Gestão do repositório no GitHub

**Responsável:** Arben (Configuração)

Este documento define um fluxo leve para seis pessoas trabalharem em paralelo durante as iterações Scrum.

## Branches

### Permanentes

| Branch | Finalidade | Entrada permitida |
|---|---|---|
| `main` | Versões estáveis, apresentadas ou entregues | Pull Request de `develop` ou `hotfix/*` |
| `develop` | Integração da iteração atual | Pull Request de uma branch curta |

### Branches curtas

| Prefixo | Uso | Origem | Destino normal |
|---|---|---|---|
| `feature/` | História ou funcionalidade | `develop` | `develop` |
| `fix/` | Correção durante a iteração | `develop` | `develop` |
| `docs/` | Documentação ou slides | `develop` | `develop` |
| `chore/` | Configuração e manutenção | `develop` | `develop` |
| `hotfix/` | Falha urgente na versão estável | `main` | `main` e depois `develop` |

Formato: `<prefixo>/<numero-da-issue>-<resumo-em-kebab-case>`.

Exemplos: `feature/12-cadastro-transacao`, `docs/27-atualizar-riscos` e
`fix/31-validar-valor-negativo`.

Regras do time:

1. Toda branch de trabalho deve estar vinculada a uma Issue.
2. Não fazer push direto em `main` ou `develop`.
3. Manter Pull Requests pequenos e com um único objetivo.
4. Exigir o CI verde e uma aprovação de alguém que não seja o autor.
5. Preferir **squash merge** e excluir a branch após o merge.
6. Levar todo `hotfix/*` integrado em `main` também para `develop`.

Ao fim de cada iteração, abrir um Pull Request de `develop` para `main`, validar a demonstração e criar a
tag correspondente: `v0.1.0`, `v0.2.0` ou `v1.0.0`.

## Proteção de branches

Em **Settings → Branches**, criar regras para `main` e `develop` com:

- Pull Request obrigatório antes do merge;
- uma aprovação obrigatória;
- aprovação invalidada após novos commits;
- check `test` obrigatório;
- conversas resolvidas antes do merge;
- push direto e force push bloqueados.

## Issues

Os formulários em `.github/ISSUE_TEMPLATE/` cobrem os três tipos básicos:

- **História:** entrega valor observável ao usuário e possui critérios de aceite;
- **Tarefa:** trabalho técnico, documental, de gestão ou apresentação;
- **Bug:** comportamento observado diferente do esperado.

Cada Issue deve caber, de preferência, em um a três dias. Uma história estimada em 13 pontos ou mais deve
ser dividida antes de entrar na iteração.

### Labels sugeridos

Criar os labels abaixo em **Issues → Labels**:

| Grupo | Labels |
|---|---|
| Tipo | `tipo: história`, `tipo: bug`, `tipo: tarefa`, `tipo: documentação`, `tipo: gestão` |
| Prioridade | `prioridade: alta`, `prioridade: média`, `prioridade: baixa` |
| Estimativa | `pontos: 1`, `pontos: 2`, `pontos: 3`, `pontos: 5`, `pontos: 8`, `pontos: 13` |
| Apoio | `impedimento`, `precisa decisão`, `boa primeira issue` |

O status deve ficar no GitHub Project; não é necessário duplicá-lo em labels.

### Definition of Ready

Uma Issue pode entrar na iteração quando objetivo e valor estão claros, critérios de aceite são
verificáveis, dependências estão registradas, estimativa foi acordada e responsável e Milestone foram
definidos.

### Definition of Done

Uma Issue pode ser encerrada quando os critérios foram atendidos, os testes aplicáveis passam, o resultado
foi revisado por Pull Request, a documentação afetada foi atualizada e o item está demonstrável em
`develop`.

## Milestones por iteração

Criar em **Issues → Milestones → New milestone**, usando as datas reais da disciplina.

| Milestone | Objetivo | Entregas sugeridas |
|---|---|---|
| `Iteração 1 — Planejamento e MVP` | Validar visão, escopo e primeiro fluxo vertical | Artefatos da Rodada 1, base técnica, CRUD inicial e demo v1 |
| `Iteração 2 — Evolução e qualidade` | Ampliar o produto e consolidar a qualidade | Funcionalidades priorizadas, testes, riscos atualizados e demo v2 |
| `Iteração 3 — Entrega final` | Estabilizar, documentar e apresentar | Correções, documentação final, apresentação e demo v3 |

O Product Owner associa ao Milestone atual apenas Issues prontas e priorizadas. Itens não concluídos voltam
ao Product Backlog e são replanejados explicitamente.

## Quadro Scrum no GitHub Project

Criar um Project do tipo Board com os status:

1. `Backlog`
2. `Pronto para a iteração`
3. `Em andamento`
4. `Em revisão`
5. `Concluído`

Campos úteis: `Milestone`, `Prioridade`, `Story points`, `Responsável`, `Data de início` e `Data de término`.
Manter, sempre que possível, apenas uma Issue principal em andamento por integrante.

## Commits e Pull Requests

Usar mensagens curtas e objetivas:

```text
feat: adiciona cadastro de transação (#12)
fix: valida valor de receita (#31)
docs: atualiza análise de riscos (#27)
```

No corpo do Pull Request, usar `Closes #12` para vincular e encerrar a Issue após o merge.
