# Auditor de Seguranca para Servidores e Ferramentas MCP

[![Live Demo](https://img.shields.io/badge/GitHub%20Pages-Live%20Demo-06b6d4?style=for-the-badge)](https://tavardt-brasil.github.io/mcp-security-auditor-br/)
[![Standard](https://img.shields.io/badge/Standard-Least%20Privilege-3b82f6?style=for-the-badge)](https://tavardt-brasil.github.io/mcp-security-auditor-br/)
[![Privacy](https://img.shields.io/badge/Privacy-100%25%20Client--Side-10b981?style=for-the-badge)](https://tavardt-brasil.github.io/mcp-security-auditor-br/)
[![License](https://img.shields.io/badge/License-MIT-slate?style=for-the-badge)](LICENSE)

Auditor e verificador de seguranca para servidores e ferramentas MCP (Model Context Protocol). Aplicacao web client-side e CLI.

Desenvolvido para organizacoes e desenvolvedores em **Brasil**, este repositorio fornece uma solucao integrada para auditoria de manifestos e configuracoes do **Model Context Protocol (MCP)**, prevenindo brechas de seguranca em ecossistemas de agentes de Inteligencia Artificial autonoma.

---

## Modos de Operacao

### 1. Aplicacao Web no Navegador (GitHub Pages)
Acesse a versao interativa com interface grafica diretamente pelo navegador:
- **Endereco Oficial**: [https://tavardt-brasil.github.io/mcp-security-auditor-br/](https://tavardt-brasil.github.io/mcp-security-auditor-br/)
- **Privacidade por Design**: Execucao 100% estatica no motor JavaScript do seu navegador. Nenhuma configuracao, chave ou dado e transmitido para servidores remotos.

### 2. Utilitario de Linha de Comando (CLI)
Para auditorias automatizadas em pipelines de integracao continua (CI/CD) ou execucao local:

```bash
# Execucao basica apontando para o arquivo de configuracao
python mcp_security_scanner.py --file mcp.json

# Modo estrito para pipeline de validacao (interrompe com codigo 1 perante qualquer desvio)
python mcp_security_scanner.py --file mcp.json --strict

# Geracao automatica de configuracao corrigida e blindada (Hardened)
python mcp_security_scanner.py --file mcp.json --harden mcp-hardened.json

# Exportacao de resultado estruturado em JSON
python mcp_security_scanner.py --file mcp.json --json
```

---

## Vetores de Seguranca Auditados

1. **Escopo e Montagem de Sistema de Arquivos**: Deteccao de montagens na raiz (`/`, `C:\`) ou pastas de sistema sensiveis (`/etc`, `~/.ssh`, `System32`).
2. **Execucao Arbitraria de Comandos e Shells**: Bloqueio de interpretadores de comando desprotegidos (`bash`, `sh`, `powershell`, `cmd`) e passagem de flags dinamicas (`-c`, `eval`).
3. **Exposicao de Segredos e Credenciais**: Inspecao de variaveis em texto simples (chaves de API, senhas, tokens de servico e strings de conexao de banco de dados).
4. **Seguranca de Cadeia de Suprimentos (Supply Chain)**: Verificacao de imutabilidade e fixacao estrita de versoes para ferramentas executadas via `npx` ou `uvx`.
5. **Prevencao de SSRF e Acesso a Metadados Cloud**: Deteccao de parametros direcionados a interfaces locais ou servicos de metadados internos (`169.254.169.254`).

---

## Exemplo de Integracao com GitHub Actions

Incorpore a verificacao de seguranca MCP diretamente nas rotinas de validacao de commits da sua organizacao:

```yaml
name: MCP Security Gate
on: [push, pull_request]

jobs:
  audit-mcp:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Configurar Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.11'
      - name: Executar Auditoria MCP
        run: |
          python mcp_security_scanner.py --file config/mcp.json --strict
```

---

## Padroes Institucionais e Conformidade

- **Jurisdicao**: Brasil
- **Referencial Tecnico**: Diretrizes de Menor Privilegio para Agentes de IA e OWASP LLM
- **Organizacao Mantenedora**: [TAVARDT-Brasil](https://github.com/TAVARDT-Brasil)

## Ecossistema e Portais TAVARDT

- **Portal Institucional**: [https://ag.tavardt.com/br/](https://ag.tavardt.com/br/)
- **Central de Ferramentas de Ciberseguranca**: [https://tools.tavardt.com/br/](https://tools.tavardt.com/br/)
- **Canal de Atendimento e Suporte Tecnico**: [https://ag.tavardt.com/br/contato/](https://ag.tavardt.com/br/contato/)

---

### Licenca
Distribuido sob os termos da licenca MIT. Consulte o arquivo [LICENSE](LICENSE) para maiores informacoes.
