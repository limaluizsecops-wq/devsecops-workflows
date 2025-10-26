# DevSecOps Pipeline

## 🚀 Sobre

O **DevSecOps Pipeline** é uma solução automatizada para integrar **segurança** diretamente no ciclo de desenvolvimento. Ele ajuda equipes a detectar vulnerabilidades, segredos expostos e dependências inseguras de forma rápida e eficiente, sem atrapalhar o fluxo de trabalho de desenvolvimento.

Essa ferramenta funciona como um **serviço pronto para usar** em repositórios GitHub, garantindo que cada commit e pull request seja automaticamente verificado por boas práticas de segurança.

---

## ✨ Benefícios

- **Automação completa**: roda automaticamente ao criar pull requests ou atualizar branches.
- **Multi-scan**: integra múltiplas ferramentas de segurança como Semgrep, TruffleHog e OWASP DepScan.
- **Relatórios claros**: gera artefatos de scan que podem ser revisados pela equipe.
- **Fácil integração**: pode ser usado diretamente de um repositório público, sem precisar configurar nada complexo.
- **Segurança contínua**: cada alteração de código passa por validação antes de ser mesclada, reduzindo riscos.

---

## ⚡ Como funciona

O pipeline realiza três verificações principais:

1. **Semgrep (Security Scan)**
   Detecta vulnerabilidades conhecidas, padrões inseguros de código e falhas comuns em aplicações.

2. **TruffleHog (Secret Scan)**
   Procura por chaves, tokens ou senhas acidentalmente commitadas no repositório.

3. **OWASP DepScan (Dependency Scan)**
   Verifica se alguma dependência do projeto possui vulnerabilidades conhecidas.

Todos os resultados são armazenados como artefatos do GitHub Actions para fácil acesso e análise.

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
```

3. Faça commit do arquivo `.github/workflows/devsecops-call.yml`.
4. Pronto! Toda mudança na branch será automaticamente escaneada.

---

## 📊 Relatórios

- **Semgrep**: erros são exibidos diretamente no log da ação.
- **TruffleHog**: encontra potenciais segredos e gera um relatório JSON.
- **DepScan**: gera um relatório completo de dependências vulneráveis.
- Todos os relatórios são salvos como **artefatos** do GitHub Actions, permitindo download e análise detalhada.

---

## 💡 Sugestões de uso

- Configure branches de produção para bloquear merges se algum scan falhar.
- Combine com políticas de revisão de código para garantir que vulnerabilidades sejam tratadas antes do deploy.
- Use como base para criar alertas automáticos ou integrações com chatops (Slack, Teams, etc.).

---

## 📂 Repositório público

Este pipeline é **open-source** e pode ser usado em qualquer projeto GitHub, sem necessidade de configuração extra. Basta referenciar o workflow conforme mostrado na seção de uso.
