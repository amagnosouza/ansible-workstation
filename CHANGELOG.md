# Changelog - Fedora Workstation Professional Setup

Histórico de versões e mudanças do projeto.

## v2.0 - Versão Modular com Roles (Janeiro 2026)

### Novo

- **Refatoração para Arquitetura Modular**: Mudança de playbook monolítico para estrutura baseada em roles Ansible
- **8 Roles Especializadas**: 
  - `base_system` - Pacotes base e configurações do sistema
  - `shell_zsh` - Zsh com Oh My Zsh e configurações
  - `fonts_nerd` - Hack Nerd Font (v3.2.1)
  - `starship_prompt` - Starship com tema Catppuccin Latte
  - `development_tools` - VS Code, Terraform, AWS CLI
  - `containers_docker` - Docker Engine e Docker Compose
  - `kubernetes` - kubectl e FreeLens
  - `browsers` - Microsoft Edge, Google Chrome e Brave Browser

- **Configuração Profissional**: 
  - `ansible.cfg` com otimizações de performance
  - `inventory.yml` com suporte local e remoto
  - `site.yml` como orquestrador principal

- **Suporte Local e Remoto**: Possibilidade de executar localmente ou em servidores remotos

- **Sistema de Tags**: Execução seletiva de componentes

- **Documentação Completa**: README em português brasileiro com exemplos e guias

### Modificado

- **Navegadores**: Microsoft Edge, Google Chrome e Brave Browser
- **Terminal**: Ghostty no lugar do Alacritty
- **Qualidade**: ansible-lint e validações automatizadas no GitHub Actions
- **Fonte Terminal**: Hack Nerd Font v3.2.1
- **Prompt Shell**: Starship com tema Catppuccin Latte integrado ao Zsh
- **Idempotência Melhorada**: Verificações `changed_when` e handlers apropriados

### Removido

- Playbook monolítico `workstation.yml`
- Estrutura não modular

## v1.0 - Versão Inicial (Dezembro 2025)

### Novo

- **Projeto Inicial**: Ansible playbook para automatizar configuração de Fedora Workstation

- **Componentes Base**:
  - Sistema base (vim, curl, git, make, tmux, alacritty, etc)
  - Terminal Zsh com Oh My Zsh e tema Agnoster
  - JetBrainsMono Nerd Font
  - VS Code
  - Terraform
  - AWS CLI
  - Podman e podman-compose
  - kubectl
  - Navegadores (Brave, Firefox)

- **Documentação Básica**: README com instruções de uso

- **Handlers e Post-Tasks**: Suporte para operações customizadas

---

## Notas

Este projeto segue as melhores práticas de Ansible:
- Código idempotente e seguro
- GPG signature verification para repositórios
- Documentação clara e completa
- Estrutura modular e reutilizável

### Práticas Profissionais Implementadas

**Idempotência**: Script seguro para executar múltiplas vezes
**GPG Verification**: Todas as repos com verificação de assinatura
**Error Handling**: Tratamento apropriado de erros
**Documentation**: Documentação clara e profissional
**Modularidade**: Tags para execução seletiva
**User Management**: Permissões apropriadas de arquivo/usuário
**Cleanup**: Limpeza automática de temporários
**Feedback**: Mensagens claras de conclusão

### Validação

- Arquivo YAML bem formado (341 linhas)
- 61 tasks estruturadas
- Handlers configurados
- Pre/Post tasks inclusos
- README.md documentado em inglês

### Como Usar

```bash
# Instalação completa
ansible-playbook workstation.yml --ask-become-pass

# Apenas navegadores
ansible-playbook workstation.yml --tags browsers --ask-become-pass

# Apenas terminal/fonts
ansible-playbook workstation.yml --tags zsh,fonts --ask-become-pass

# Apenas desenvolvimento
ansible-playbook workstation.yml --tags terraform,vscode --ask-become-pass
```

---
