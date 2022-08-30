# Terraform Executa Modulo
Github Actions para ser reutilizado nos projetos que utilizam Terraform, com a finalidade de validar a sintaxe do código e/ou criar uma infra baseada em um modulo.

## Inputs
| Nome | Descrição | Requirida | Default |
|------|-----------|-----------|---------|
| `os_version` | Versão do sistema operacional | não | ubuntu-20.04 |
| `run_apply` | Define se o step terraform apply será executado | não | false |
| `run_plan` | Define se o step terraform plan será executado | não | false |
| `tf_workspace` | Seleciona o Workspace | não | default |
| `working_directory` | Define o diretório onde a pipeline irá atuar | não | '.' |

## Secrets

Herda a secrets existentes no repositório que utiliza este workflow. A principal função é configurar as variáveis de ambientes necessárias para executar o modulo terraform.

## Utilizando 
Criar a seguintes estrutura de diretórios: 

`.github/workflows/<proposito>.yml`

Utilize o exemplo abaixo para seu pipeline de CI:

```yaml
name: "Terraform Valida e Executa Modulo"

on:
  push:
    branches:
      - main
  
jobs:
  terraform:
    uses: "mentoriaiac/cicd_centralizado/.github/workflows/terraform.yaml@v1"
    with:
      run_apply: true
      run_plan: true
      tf_workspace: "default"
    secrets: inherit
```