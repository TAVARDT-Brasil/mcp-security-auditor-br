# Auditor de Segurança para Servidores e Ferramentas MCP

[![Live Demo](https://img.shields.io/badge/GitHub%20Pages-Live%20Demo-06b6d4?style=for-the-badge)](https://tavardt-brasil.github.io/mcp-security-auditor-br/)
[![Standard](https://img.shields.io/badge/Standard-Least%20Privilege-3b82f6?style=for-the-badge)](https://tavardt-brasil.github.io/mcp-security-auditor-br/)
[![Privacy](https://img.shields.io/badge/Privacy-100%25%20Client-Side-10b981?style=for-the-badge)](https://tavardt-brasil.github.io/mcp-security-auditor-br/)
[![License](https://img.shields.io/badge/License-MIT-slate?style=for-the-badge)](LICENSE)

Auditor e verificador de segurança para servidores e ferramentas MCP (Model Context Protocol). Aplicação web client-side e CLI.

Desenvolvido para organizações e desenvolvedores em **Brasil**, este repositório fornece uma solução integrada para auditoria de manifestos e configurações do **Model Context Protocol (MCP)**, prevenindo brechas de segurança em ecossistemas de agentes de Inteligência Artificial autônoma.

***

## Modos de Operação

### 1. Aplicação Web no Navegador (GitHub Pages)
Acesse a versão interativa com interface gráfica diretamente pelo navegador:
- **Endereço Oficial**: [https://tavardt-brasil.github.io/mcp-security-auditor-br/](https://tavardt-brasil.github.io/mcp-security-auditor-br/)
- **Privacidade por Design**: Execução 100% estática no motor JavaScript do seu navegador. Nenhuma configuração, chave ou dado é transmitido para servidores remotos.

### 2. Utilitário de Linha de Comando (CLI)
Para auditorias automatizadas em pipelines de integração contínua (CI/CD) ou execução local:

```bash
# Execução básica apontando para o arquivo de configuração
python mcp_security_scanner.py -file mcp.json

# Modo estrito para pipeline de validação (interrompe com código 1 perante qualquer desvio)
python mcp_security_scanner.py -file mcp.json -strict

# Geração automática de configuração corrigida e blindada (Hardened)
python mcp_security_scanner.py -file mcp.json -harden mcp-hardened.json

# Exportação de resultado estruturado em JSON
python mcp_security_scanner.py -file mcp.json -json
```

***

## Vetores de Segurança Auditados

1. **Escopo e Montagem de Sistema de Arquivos**: Detecção de montagens na raiz (`/`, `C:\`) ou pastas de sistema sensíveis (`/etc`, `~/.ssh`, `System32`).
2. **Execução Arbitrária de Comandos e Shells**: Bloqueio de interpretadores de comando desprotegidos (`bash`, `sh`, `powershell`, `cmd`) e passagem de flags dinâmicas (`-c`, `eval`).
3. **Exposição de Segredos e Credenciais**: Inspeção de variáveis em texto simples (chaves de API, senhas, tokens de serviço e strings de conexão de banco de dados).
4. **Segurança de Cadeia de Suprimentos (Supply Chain)**: Verificação de imutabilidade e fixação estrita de versões para ferramentas executadas via `npx` ou `uvx`.
5. **Prevenção de SSRF e Acesso a Serviços Internos**: Detecção de parâmetros direcionados a interfaces locais ou hosts internos não autorizados.

***

## Exemplo de Integração com GitHub Actions

Incorpore a verificação de segurança MCP diretamente nas rotinas de validação de commits da sua organização:

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
          python mcp_security_scanner.py -file config/mcp.json -strict
```

***

## Padrões Institucionais e Conformidade

- **Referencial Técnico**: Diretrizes de Menor Privilégio para Agentes de IA e OWASP LLM


## Ecossistema e Portais TAVARDT

- **Portal Institucional**: [Portal Institucional](https://ag.tavardt.com/br/)
- **Central de Ferramentas**: [Central de Ferramentas](https://tools.tavardt.com/br/)
- **Canal de Atendimento e Suporte Técnico**: [https://ag.tavardt.com/br/contato/](https://ag.tavardt.com/br/contato/)

***

### Licença
Distribuído sob os termos da licença MIT. Consulte o arquivo [LICENSE](LICENSE) para maiores informações.

***

© 2026 TAVARDT. Todos os direitos reservados.
