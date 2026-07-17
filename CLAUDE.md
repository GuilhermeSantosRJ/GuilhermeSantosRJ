# CLAUDE.md

Instruções para o Claude Code ao trabalhar neste repositório. Este workspace reúne projetos jurídicos (automação, análise documental, integrações, scripts internos) implementados em **Python** e **Node.js**.

## Confidencialidade e dados sensíveis

Este é o ponto mais importante do repositório — trate como default, não como exceção.

- Assuma que qualquer arquivo de processo, contrato, petição, e-mail de cliente ou planilha de dados pessoais é **sigiloso** (sigilo profissional / possível segredo de justiça) e pode conter dados pessoais sob a LGPD.
- Nunca inclua nomes de partes, números de processo (CNJ), CPF/CNPJ, e-mails ou trechos de documentos reais em: commits, mensagens de commit, código de exemplo, comentários, logs ou arquivos de teste. Use dados fictícios (`Fulano da Silva`, `000.000.000-00`, `0000000-00.0000.0.00.0000`).
- Nunca envie conteúdo de processos/documentos jurídicos para serviços externos (APIs de terceiros, ferramentas de conversão online, gists, pastebins) sem confirmação explícita — mesmo que pareça anonimizado.
- Arquivos com dados reais de clientes/processos não devem ser versionados. Sempre verificar `.gitignore` antes de `git add` e usar `git status` para revisar o que está sendo staged.
- Segredos (tokens de API de tribunais/PJe, chaves OAB, credenciais de e-mail, `.env`) nunca vão para o Git.

## Estrutura do repositório

Workspace ainda em formação — múltiplos subprojetos Python e/ou Node.js podem coexistir aqui. Ao criar um novo subprojeto:

- Python: subpasta própria com `.venv/`, `pyproject.toml` (ou `requirements.txt`) e testes em `tests/`.
- Node.js: subpasta própria com `package.json` próprio; preferir TypeScript quando o projeto crescer além de scripts pontuais.
- Não misturar dependências de projetos diferentes em um único ambiente/lockfile.

## Convenções — Python

- Formatação/lint: `black` + `ruff` (ou `flake8` se já configurado no subprojeto — verificar antes de assumir).
- Usar type hints em funções novas.
- Ambiente virtual isolado por subprojeto (`.venv/`, já coberto pelo `.gitignore`).
- Ao lidar com datas de prazos processuais, sempre usar timezone explícito (`America/Sao_Paulo`) — bugs de fuso horário em prazo é o tipo de erro que não pode acontecer.

## Convenções — Node.js

- Preferir `npm` (já refletido no `.gitignore`); confirmar com o usuário antes de introduzir outro gerenciador (`pnpm`/`yarn`) em um subprojeto novo.
- Lint/format: ESLint + Prettier quando o subprojeto tiver `package.json` configurado para isso.
- Scripts que chamam MCP servers ou APIs externas (tribunais, PJe, DataJud, etc.) devem tratar timeout e rate limit explicitamente — essas integrações são notoriamente instáveis.

## Testes

- Testes de parsing de documentos jurídicos, cálculo de prazos e extração de dados devem sempre usar fixtures fictícias, nunca documentos reais mesmo que anonimizados manualmente.
- Cálculo de prazos processuais é código crítico: cobrir casos de borda (feriados forenses, suspensão de prazo, recesso forense) com testes antes de considerar pronto.

## Idioma

- Comunicação com o usuário e commits: português.
- Nomes de variáveis/funções no código: inglês, salvo quando o domínio jurídico torna o termo em português mais claro (ex.: `prazo_fatal`, `peticao`, `citacao`) — nesse caso, manter em português é aceitável e preferível a traduções forçadas.
