# FinApp — Controle Financeiro Pessoal

Aplicativo web para controle de gastos e receitas pessoais, desenvolvido para as disciplinas de
Engenharia de Software (ES - TCC00225) e Gerência de Projeto e Manutenção de Software (GPMS - TCC00363).

## Sobre o projeto

O FinApp permite que o usuário registre transações (receitas e despesas), organize-as em categorias,
acompanhe metas de economia e visualize relatórios de seus gastos.

Veja o Documento de Visão completo em [`docs/rodada1/01-documento-visao.md`](docs/rodada1/01-documento-visao.md).

## Stack técnica

- **Linguagem:** Kotlin (JVM 17)
- **Framework:** Spring Boot 3.3
- **Build:** Gradle com Kotlin DSL
- **Containerização:** Docker / Docker Compose
- **Banco de dados:** H2 em memória para desenvolvimento e demonstração

## Equipe e papéis

| Nome | Papel |
|---|---|
| Filipe | Gerente de Projeto (GP) |
| Sara | Product Owner (PO) |
| Emanuel | Scrum Master / Facilitador |
| Arben | Responsável por Configuração |
| Enzo | Desenvolvedor |
| (Você) | Desenvolvedora |

Detalhamento completo em [`docs/rodada1/03-papeis-responsabilidades.md`](docs/rodada1/03-papeis-responsabilidades.md).

## Estrutura do repositório

```
finapp/
├── .github/                 # Templates de Issues/PRs e integração contínua
├── docs/                    # Documentação de gestão do projeto (Plano de Projeto)
│   ├── gestao-github.md     # Fluxo de branches, Issues e Milestones
│   └── rodada1/             # Artefatos entregues na Rodada 1
├── slides/                  # Slides usados nas apresentações
├── src/                     # Código-fonte da aplicação (Kotlin)
│   ├── main/kotlin/...
│   └── test/kotlin/...
├── build.gradle.kts
├── settings.gradle.kts
├── Dockerfile
├── docker-compose.yml
└── LICENSE
```

## Como rodar o projeto

```bash
# Build e execução via Docker Compose
docker compose up --build
```

A aplicação ficará disponível em `http://localhost:8080`. O console H2 de desenvolvimento fica em
`http://localhost:8080/h2-console`, com JDBC URL `jdbc:h2:mem:finapp`, usuário `sa` e senha em branco.

Para encerrar e remover o contêiner:

```bash
docker compose down
```

## Estratégia de branches

- `main` — versão estável, sempre funcional
- `develop` — integração das features em desenvolvimento
- `feature/<issue>-<resumo>` — funcionalidade ou história criada a partir de `develop`
- `fix/<issue>-<resumo>` — correção comum criada a partir de `develop`
- `docs/<issue>-<resumo>` — documentação criada a partir de `develop`
- `hotfix/<issue>-<resumo>` — correção urgente criada a partir de `main`

Exemplo: `feature/12-cadastro-transacao`.

Todo trabalho começa em uma Issue. O merge em `develop` é feito por Pull Request, com CI verde e ao menos
uma aprovação de alguém que não seja o autor. Ao final de cada iteração, `develop` é integrado em `main`
por Pull Request e recebe uma tag (`v0.1.0`, `v0.2.0` e `v1.0.0`). Para este time, branches `release/*`
não são necessárias.

As regras detalhadas estão em [`docs/gestao-github.md`](docs/gestao-github.md).

## Issues e Milestones

Usem uma Issue por história, bug, tarefa técnica ou artefato de gestão. Toda Issue selecionada para a
iteração deve ter responsável, critérios de aceite/conclusão, estimativa e Milestone.

Milestones sugeridos:

1. `Iteração 1 — Planejamento e MVP`
2. `Iteração 2 — Evolução e qualidade`
3. `Iteração 3 — Entrega final`

No GitHub Project, usem os status `Backlog`, `Pronto para a iteração`, `Em andamento`, `Em revisão` e
`Concluído`. Os formulários em `.github/ISSUE_TEMPLATE/` já padronizam as novas Issues.

## Licença

Este projeto está sob a licença MIT — veja [`LICENSE`](LICENSE) para detalhes.
