# DevSecOps Pipeline

## 🚀 Sobre

O **DevSecOps Pipeline** é uma solução automatizada para integrar **segurança** e **qualidade de código** diretamente no ciclo de desenvolvimento. Ele ajuda equipes a detectar vulnerabilidades, segredos expostos, dependências inseguras e métricas de código de forma rápida e eficiente, sem atrapalhar o fluxo de trabalho de desenvolvimento.

Essa ferramenta funciona como um **serviço pronto para usar** em repositórios GitHub, garantindo que cada commit e pull request seja automaticamente verificado por boas práticas de segurança e qualidade.

---

## ✨ Benefícios

- **Automação completa**: roda automaticamente ao criar pull requests ou atualizar branches.
- **Multi-scan**: integra múltiplas ferramentas de segurança como Semgrep, TruffleHog, OWASP DepScan e SCC.
- **Relatórios claros**: gera artefatos de scan que podem ser revisados pela equipe.
- **Fácil integração**: pode ser usado diretamente de um repositório público, sem precisar configurar nada complexo.
- **Segurança e qualidade contínua**: cada alteração de código passa por validação antes de ser mesclada, reduzindo riscos e mantendo boas práticas.

---

## ⚡ Como funciona

O pipeline realiza quatro verificações principais:

1. **Semgrep (Security Scan)**
   Detecta vulnerabilidades conhecidas, padrões inseguros de código e falhas comuns em aplicações.

2. **TruffleHog (Secret Scan)**
   Procura por chaves, tokens ou senhas acidentalmente commitadas no repositório.

3. **OWASP DepScan (Dependency Scan)**
   Verifica se alguma dependência do projeto possui vulnerabilidades conhecidas.

4. **SCC (Source Code Metrics Scan)**
   Analisa a **qualidade do código** mostrando métricas como:

   - Linhas de código por linguagem
   - Comentários e linhas em branco
   - Número de arquivos por linguagem
   - Complexidade do código (opcional)

Todos os resultados são exibidos diretamente nos logs do GitHub Actions, e os relatórios das ferramentas que geram artefatos são armazenados para download e análise detalhada.

---

## 🛠 Como usar

Para integrar o DevSecOps Pipeline no seu projeto:

1. Abra o seu repositório no GitHub.
2. Crie um workflow que **chame o pipeline reutilizável**:

```yaml
name: DevSecOps Check

on:
  push:
    branches: ["main"]
  pull_request:
    branches: ["main"]

jobs:
  devsecops:
    uses: usuario/devsecops-workflows/.github/workflows/devsecops.yml@main
    with:
      run_semgrep: true
      run_trufflehog: true
      run_depscan: true
      run_scc: true
```

3. Faça commit do arquivo `.github/workflows/devsecops-call.yml`.
4. Pronto! Toda mudança na branch será automaticamente escaneada e analisada.

---

## 📊 Relatórios

- **Semgrep**: erros são exibidos diretamente no log da ação.
- **TruffleHog**: encontra potenciais segredos e gera um relatório JSON.
- **DepScan**: gera um relatório completo de dependências vulneráveis.
- **SCC**: imprime métricas de código diretamente no console do CI.

Todos os relatórios podem ser baixados como **artefatos** do GitHub Actions para análise detalhada, exceto SCC que é exibido no log.

---

## 💡 Sugestões de uso

- Configure branches de produção para bloquear merges se algum scan falhar.
- Combine com políticas de revisão de código para garantir que vulnerabilidades sejam tratadas antes do deploy.
- Use SCC para acompanhar métricas de crescimento do código, qualidade e manutenção.
- Integre alertas automáticos ou chatops (Slack, Teams, etc.) para notificações imediatas de falhas.

---

## 📂 Repositório público

Este pipeline é **open-source** e pode ser usado em qualquer projeto GitHub, sem necessidade de configuração extra. Basta referenciar o workflow conforme mostrado na seção de uso.
