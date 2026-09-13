# Configuração da Estação de Trabalho Fedora

Projeto Ansible para automatizar a configuração de uma estação de trabalho Fedora com ferramentas de desenvolvimento, runtime de containers, ferramentas Kubernetes e utilitários essenciais.

**Versão:** 2.0 (Modular com Roles)  
**Testado Em:** Fedora Workstation 43+  
**Última Atualização:** Janeiro 2026

## Recursos

- **Design Modular**: Organizado com roles Ansible para manutenibilidade
- **Configuração**: Segue as melhores práticas do Fedora
- **Local & Remoto**: Suporta execução local e remota
- **Idempotente**: Seguro para executar várias vezes
- **GPG Verificado**: Todos os repositórios usam verificação de assinatura
- **Customizável**: Sobrescreva padrões via variáveis
- **Execução com Tags**: Execute componentes específicos seletivamente

## Componentes Instalados

### Sistema & Desenvolvimento
- Pacotes base: vim, curl, git, make, tmux, Ghostty, ansible-lint
- Terminal: Zsh com Oh My Zsh
- Prompt do shell: Starship com tema Catppuccin Latte
- Fonte do terminal: Hack Nerd Font (v3.2.1)
- Utilitários do sistema: btop, ncdu, tree, flameshot, plocate

### IDEs & Editores
- **Visual Studio Code** (versão mais recente do repositório oficial Microsoft)

### Cloud & Infraestrutura
- **AWS CLI** (Amazon Web Services)
- **Terraform** (Infraestrutura como Código)
- **kubectl** (Cliente Kubernetes)
- **Docker Engine** (Runtime de containers)
- **Docker Compose** (Orquestração multi-container)

### Navegadores
- **Microsoft Edge** (Estável)
- **Google Chrome** (Estável)
- **Brave Browser** (Estável)

### Opcional
- **FreeLens** (IDE Kubernetes - via extra-vars)

## Instalação

### Pré-requisitos

- Fedora Workstation 43+ (verificado na inicialização)
- Acesso `sudo`
- Conexão com internet
- Ansible 2.10+

### Validação local

```bash
ansible-playbook site.yml --syntax-check
ansible-lint site.yml
```

Essas mesmas validações são executadas automaticamente pelo GitHub Actions em cada push para `main` e em pull requests.

### 1. Instale Ansible (se ainda não estiver instalado)

```bash
sudo dnf install -y ansible git
```

### 2. Clone ou baixe este projeto

```bash
git clone <url-do-repositorio> ansible-workstation
cd ansible-workstation
```

### 3. Execute o Playbook

#### **Opção A: Execução Local (Recomendado)**

```bash
ansible-playbook site.yml --ask-become-pass
```

#### **Opção B: Execução Remota**

Atualize `inventory.yml` com seu host de destino, então execute:

```bash
ansible-playbook site.yml -i inventory.yml --ask-become-pass
```

## Tags Disponíveis

Execute componentes específicos sem instalação completa:

```bash
# Componentes principais
ansible-playbook site.yml --tags base --ask-become-pass
ansible-playbook site.yml --tags shell,zsh --ask-become-pass
ansible-playbook site.yml --tags fonts --ask-become-pass
ansible-playbook site.yml --tags starship --ask-become-pass

# Ferramentas de desenvolvimento
ansible-playbook site.yml --tags development,tools --ask-become-pass
ansible-playbook site.yml --tags vscode --ask-become-pass
ansible-playbook site.yml --tags terraform --ask-become-pass
ansible-playbook site.yml --tags aws --ask-become-pass

# Containers & Orquestração
ansible-playbook site.yml --tags docker,containers --ask-become-pass
ansible-playbook site.yml --tags kubernetes,k8s --ask-become-pass

# Navegadores
ansible-playbook site.yml --tags browsers,web --ask-become-pass
ansible-playbook site.yml --tags edge,chrome --ask-become-pass

# Combinadas
ansible-playbook site.yml --tags shell,starship,fonts --ask-become-pass
ansible-playbook site.yml --tags docker,kubernetes --ask-become-pass
```

## Customização

### Sobrescreva Variáveis

Crie um `group_vars/local_workstation.yml` ou passe via linha de comando:

```bash
# Altere o tema Starship
ansible-playbook site.yml \
  -e "starship_palette=catppuccin_mocha" \
  --ask-become-pass

# Altere o tema Zsh
ansible-playbook site.yml \
  -e "zsh_theme=robbyrussell" \
  --ask-become-pass

# Instale FreeLens
ansible-playbook site.yml \
  -e "freelens_rpm_url=https://example.com/freelens.rpm" \
  --tags kubernetes \
  --ask-become-pass
```

### Crie Variáveis de Grupo Personalizadas

Crie `group_vars/local_workstation.yml`:

```yaml
---
# Variáveis personalizadas sobrescrevem padrões
zsh_theme: "agnoster"
starship_preset: "catppuccin-powerline"
starship_palette: "catppuccin_latte"
nerd_font_name: "Hack"
nerd_font_version: "3.2.1"
kubernetes_version: "1.30"
```

## Estrutura do Projeto

```
ansible-workstation/
├── ansible.cfg              # Configuração Ansible
├── inventory.yml            # Hosts e variáveis
├── site.yml                 # Playbook orquestrador principal
├── README.md                # Este arquivo
├── CHANGELOG.md             # Histórico de versões
├── logs/                    # Logs do playbook (criado automaticamente)
└── roles/
    ├── base_system/         # Pacotes base, configuração do sistema
    ├── shell_zsh/           # Configuração Zsh
    ├── fonts_nerd/          # Instalação de fonte Nerd
    ├── starship_prompt/     # Configuração do prompt Starship
    ├── development_tools/   # VS Code, Terraform, AWS CLI
    ├── containers_docker/    # Docker Engine e Docker Compose
    ├── kubernetes/          # kubectl e FreeLens
    └── browsers/            # Edge e Chrome
```

## Passos Pós-Instalação

### 1. Ative o Novo Shell

```bash
exec zsh
```

### 2. Configure a Fonte do Terminal

1. Abra as preferências do seu terminal
2. Defina a fonte como **"Hack Nerd Font"** (ou "Hack NerdFont")
3. Salve e reinicie o terminal

### 3. Verifique Instalações

```bash
# Verifique versões
zsh --version
starship --version
docker --version
docker compose version
kubectl version --client
terraform version
code --version
aws --version

# Teste Docker
docker run --rm hello-world

# Teste Starship
starship config
```

### 4. Configure kubectl

```bash
# Configure kubeconfig
mkdir -p ~/.kube
# Copie seu arquivo kubeconfig ou:
kubectl config view
```

### 5. Configuração do VS Code

1. Instale extensões recomendadas:
   - Terraform
   - Docker
   - Kubernetes
   - Python
   - Remote Development

```bash
# Ou via linha de comando
code --install-extension hashicorp.terraform
code --install-extension ms-azuretools.vscode-docker
code --install-extension ms-kubernetes-tools.vscode-kubernetes-tools
```

## Comandos Úteis

### Execução do Playbook

```bash
# Configuração completa
ansible-playbook site.yml --ask-become-pass

# Verifique o que seria alterado (dry-run)
ansible-playbook site.yml --check --ask-become-pass

# Saída detalhada
ansible-playbook site.yml -vvv --ask-become-pass

# Com cronometragem
ansible-playbook site.yml --ask-become-pass

# Liste as tags disponíveis
ansible-playbook site.yml --list-tags

# Apenas uma role específica
ansible-playbook site.yml --tags starship --ask-become-pass
```

## Considerações de Segurança

- Todos os repositórios usam verificação de assinatura GPG
- Nenhum script é executado sem verificação
- Uso mínimo do módulo `shell` (prefira módulos nativos)
- Permissões e propriedade explícitas dos arquivos
- Usuário adicionado ao grupo `docker`
- Sem credenciais ou dados sensíveis hardcoded

## Solução de Problemas

### Problemas de Permissão do Podman

```bash
# Verifique participação no grupo
groups $USER

# Certifique-se de que o grupo podman existe
getent group podman

# Saia e entre novamente, ou use:
newgrp podman
```

### Zsh Não Inicia como Padrão

```bash
# Verifique shell atual
echo $SHELL

# Defina Zsh como padrão manualmente
chsh -s /usr/bin/zsh

# Verifique
echo $SHELL
```

### Starship Não Carrega

```bash
# Verifique se Starship está instalado
which starship
starship --version

# Verifique arquivo de configuração
test -f ~/.config/starship.toml && echo "Config exists"

# Verifique inicialização no Zsh
grep starship ~/.zshrc
```

### Fonte Não Aparece

```bash
# Força atualização do cache de fontes
fc-cache -fv ~/.local/share/fonts

# Lista fontes instaladas
fc-list | grep -i hack

# Verifique diretório de fontes
ls -la ~/.local/share/fonts/ | grep -i hack
```

### Problemas com Kubernetes

```bash
# Verifique instalação do kubectl
kubectl version --client

# Verifique kubeconfig
kubectl config view

# Teste conexão com cluster
kubectl cluster-info
```

## Documentação & Recursos

- **Ansible**: https://docs.ansible.com
- **Starship**: https://starship.rs
- **Podman**: https://podman.io
- **Kubernetes**: https://kubernetes.io/docs
- **Fedora**: https://docs.fedoraproject.org
- **Oh My Zsh**: https://ohmyz.sh
- **Catppuccin**: https://catppuccin.com

## Licença

Este playbook é fornecido como está para uso pessoal e profissional.

## 🔄 Changelog

Veja [CHANGELOG.md](CHANGELOG.md) para histórico de versões e atualizações.

---

**Precisa de ajuda?** Verifique os logs:

```bash
# Visualize logs do Ansible
tail -f logs/ansible.log

# Visualize arquivos retry do Ansible
cat logs/*.retry
```
