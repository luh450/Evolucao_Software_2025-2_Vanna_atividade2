# Evolucao_Software_2025-2_Vanna_atividade2


**Projeto analisado:** https://github.com/vanna-ai/vanna 

## Motivação
À medida que os sistemas de software e modelos de IA evoluem, os processos de release e fluxo de trabalho tornam-se cada vez mais complexos, distribuídos e difíceis de padronizar. Decisões relacionadas a versionamento, validação, deploy e rollback costumam depender de conhecimento tácito, revisão manual e experiência individual, o que aumenta o risco operacional, a inconsistência entre equipes e o tempo de entrega.

A adoção de uma IA especializada na análise de estratégias de release e workflows permite transformar esse conhecimento implícito em um processo estruturado, auditável e escalável. Essa IA atua como um analista técnico contínuo, capaz de avaliar pipelines existentes, identificar riscos, gargalos e pontos únicos de falha, além de recomendar melhorias alinhadas a boas práticas de engenharia, MLOps e governança.

Com isso, a organização passa a:

- Reduzir falhas em produção e retrabalho pós-release
- Aumentar a previsibilidade e a qualidade das entregas
- Padronizar decisões técnicas entre times e projetos
- Acelerar ciclos de desenvolvimento sem perder controle
- Criar rastreabilidade clara entre mudanças, versões e impactos

Mais do que automatizar tarefas, essa abordagem eleva o nível de maturidade do processo, permitindo que equipes foquem em inovação enquanto a IA apoia decisões críticas de release com análise consistente, contextual e baseada em padrões consolidados.



## Tutorial

Todos os modelos utilizados neste trabalho foram executados por meio do ChatHugging (Hugging Face), que atua como interface para acesso e uso de modelos de linguagem pré-treinados. Essa abordagem permitiu testar modelos mais robustos e de grande porte sem a necessidade de utilizar um computador local com alto poder computacional.

Acesse: https://huggingface.co/chat/

Do lado inferior à esquerda é possivel selecionar o modelo a ser utilizado
<img width="1484" height="857" alt="image" src="https://github.com/user-attachments/assets/7af9a0b5-ea23-4ad3-ba4f-9fe78cbf5fd4" />

São diversos modelos que podem ser utilizados. Só procurar o modelo que deseja.
<img width="1397" height="792" alt="image" src="https://github.com/user-attachments/assets/8ea99630-4f88-4e31-9b2c-dded4f01ecdb" />

Após selecionar já é possível utilizar o modelo


## Modelos
`meta-llama/Meta-Llama-3.1-70B-Instruct` : https://huggingface.co/meta-llama/Llama-3.1-70B-Instruct
`Qwen/Qwen2.5-72B-Instruct` : https://huggingface.co/Qwen/Qwen2.5-72B-Instruct

## Justificativa dos modelos escolhidos
1. `meta-llama/Meta-Llama-3.1-70B-Instruct` : deve-se à sua alta capacidade de compreensão semântica, raciocínio contextual e seguimento de instruções complexas. Por se tratar de um modelo de grande porte (70B parâmetros), ele apresenta desempenho superior na identificação de padrões implícitos em textos técnicos, como estratégias de release e modelos de workflow, mesmo quando essas informações não estão explicitamente estruturadas. Além disso, o modelo é otimizado para tarefas instruction-following, o que o torna especialmente adequado para analisar descrições de processos, inferir fluxos de trabalho e classificar tipos de releases a partir de documentação e código-fonte.
2. `Qwen/Qwen2.5-72B-Instruct` : justifica-se por ser um modelo de linguagem de grande escala (72.7B parâmetros) otimizado para seguir instruções (instruction-tuned), com capacidades avançadas de raciocínio, compreensão de contexto longo (até 128K tokens) e geração de texto estruturado, como JSON. Seu desempenho competitivo em benchmarks de código e raciocínio geral, aliado a um treinamento especializado em matemática e programação, o torna particularmente adequado para analisar repositórios de software, inferir fluxos de trabalho a partir de documentação técnica e identificar padrões complexos em commits, pull requests e configurações de CI/CD

## Identificação de Tipos de Releases

### Perguntas padrões:
1. **Analisando o repositório `vanna-ai/vanna`, que tipo(s) de estratégia de release o projeto aparenta utilizar  
   (ex.: *semantic versioning*, releases incrementais, release manual vs automatizado)? Justifique com evidências observáveis no repositório**


## Análise de CI/CD e Estratégia de Release

Com base nos workflows presentes no repositório (`tests.yml` e `python-publish.yaml`), é possível identificar a adoção de práticas de **Integração Contínua (CI)** e **Entrega Contínua (CD)** no projeto.

#### Integração Contínua (CI)
O arquivo `tests.yml` é responsável pela execução automática de testes a cada *push* ou *pull request*, garantindo que novas alterações no código não quebrem funcionalidades existentes. Essa prática caracteriza a integração contínua.

```yaml
on:
  push:
    branches:
      - main
```

#### Entrega Contínua (CD)
O workflow `python-publish.yaml` automatiza o processo de build e publicação do pacote Python, geralmente acionado por meio de *tags* ou *releases*. Isso indica a adoção de entrega contínua do pacote, permitindo que novas versões sejam disponibilizadas de forma controlada

```yaml
on:
  release:
    types: [published]
```

**Respostas**
- `meta-llama/Meta-Llama-3.1-70B-Instruct`: O projeto vanna-ai/vanna utiliza o Semantic Versioning, com base nas seguintes evidências:
Convenção de nomenclatura de tags: vX.Y.Z
Histórico de releases: mantido em CHANGELOG.md
Automatização de release: sugestão de uso de GitHub Actions
Isso indica que o projeto segue uma estratégia de release baseada no Semantic Versioning, com uma estrutura de release clara e automatizada.

- `Qwen/Qwen2.5-72B-Instruct`: O projeto vanna-ai/vanna adota o Semantic Versioning (SemVer), com um processo de release híbrido: automação nas etapas de build e teste, mas publicação manual das versões no GitHub.
Evidências-chave:
Versionamento Semântico: As tags seguem o padrão vX.Y.Z (ex.: v0.3.0).
Automação Parcial: Usa GitHub Actions para CI/CD (testes, build).


2. **O projeto `vanna-ai/vanna` está mais alinhado a um modelo de  
   *Continuous Delivery* ou *Continuous Deployment*? Explique com base no processo de publicação e integração contínua**

  Arquivo `pyproject.toml`
```
   [project]
version = "2.0.0rc1"
```

Seção `[project.optional-dependencies]`
```
[project.optional-dependencies]
flask = ["flask>=2.0.0", "flask-cors>=4.0.0"]
fastapi = ["fastapi>=0.68.0", "uvicorn>=0.15.0"]
servers = ["vanna[flask,fastapi]"]
```

**Respostas**
- `meta-llama/Meta-Llama-3.1-70B-Instruct`: Com base no processo de publicação e integração contínua, o projeto vanna-ai/vanna parece estar mais alinhado ao modelo de Continuous Delivery (CD).
Evidências que apoiam esta afirmação incluem:
GitHub Actions: O projeto utiliza GitHub Actions para automatizar o processo de build, testes e deploy. No entanto, a configuração das ações não sugere uma automação de deploy direto para produção.
Releases manuais: Embora o projeto utilize uma estratégia de release baseada no Semantic Versioning, as releases são realizadas manualmente, o que sugere que o processo de deploy ainda é controlado por humanos.
Nenhuma evidência de deploy automático: Não há nenhuma evidência de que o projeto tenha uma configuração de deploy automático para produção, o que é uma característica típica do CD.
- `Qwen/Qwen2.5-72B-Instruct`: O projeto vanna-ai/vanna está alinhado com Continuous Delivery, não com Continuous Deployment.
Por quê?
CI/CD Automatizado: Usa GitHub Actions para testes, build e geração de artefatos prontos para produção.
Deploy Manual: A implantação final em produção ou publicação pública (ex.: no PyPI) requer uma ação manual explícita de um mantenedor. Não há automação para esta etapa decisiva.

3. **Observando o histórico de versões, o projeto realiza com maior frequência releases do tipo  
   *major*, *minor* ou *patch*? O que isso indica sobre a estabilidade e maturidade do software?**
**Respostas**
- `meta-llama/Meta-Llama-3.1-70B-Instruct`: Com base no histórico de versões do projeto vanna-ai/vanna, é possível observar que o projeto realiza com maior frequência releases do tipo patch. Isso indica que o projeto está em uma fase de desenvolvimento ativo e está focado em manter a estabilidade do software.
- `Qwen/Qwen2.5-72B-Instruct`:  O projeto realiza mais releases do tipo patch. Isso indica um foco ativo na estabilidade (correções rápidas) e um desenvolvimento ágil, mas ainda não atingiu a maturidade completa (versão 0.x.y).


##  Identificação de Tipos de Workflow
### Perguntas padrões:
1. **Com base no uso de branches, pull requests e histórico de commits,  
   qual modelo de workflow o projeto mais se aproxima  
   (ex.: *GitHub Flow*, *Trunk-Based Development*, *GitFlow*)?**
   
**Respostas**
- `meta-llama/Meta-Llama-3.1-70B-Instruct`: Com base no uso de branches, pull requests e histórico de commits, o projeto vanna-ai/vanna parece seguir o GitHub Flow.
Isso é apoiado pelo fato de que:
Existem apenas duas branches principais: main e develop
Os pull requests são utilizados para revisar e aprová-los antes de merge-los na branch main
O histórico de commits sugere que os desenvolvedores trabalham diretamente na branch main e criam pull requests para revisar e aprová-los antes de merge-los.
- `Qwen/Qwen2.5-72B-Instruct`: Com base na análise da estrutura de branches, uso de pull requests e padrões de commits, o projeto vanna-ai/vanna se aproxima mais do modelo GitHub Flow, com uma possível leve influência de Trunk-Based Development em sua simplicidade.
Evidências:
Branch Principal Única: A main é a única branch de produção permanente e estável.
Desenvolvimento em Branches de Feature: Todo novo trabalho é feito em branches descritivas criadas a partir da main (ex.: feat/..., fix/...).
Revisão via Pull Requests (PRs): As mudanças são sempre integradas à main através de Pull Requests, que servem como ponto de revisão de código, discussão e execução de checagens automáticas (CI).
Implantação a partir da Main: A versão em main está sempre em estado implantável (confirmado pela existência de CI), alinhando-se com os princípios do GitHub Flow.

  
2. **O fluxo de desenvolvimento do `vanna-ai/vanna` é predominantemente  
   orientado à automação (CI/CD) ou a validações manuais? Identifique indícios claros no repositório**
   
**Respostas**
- `meta-llama/Meta-Llama-3.1-70B-Instruct`: O fluxo de desenvolvimento do vanna-ai/vanna é predominantemente orientado à automação (CI/CD).
Isso é apoiado pelo uso de GitHub Actions para automatizar a build, testes e deploy, além da presença de scripts e ferramentas de automação no repositório.
- `Qwen/Qwen2.5-72B-Instruct`: O fluxo de desenvolvimento do vanna-ai/vanna é predominantemente orientado à automação (CI/CD).
Indícios claros:
GitHub Actions: Presença de workflows (.github/workflows/) automatizando build, testes e análise de código em cada push/pull request.
Gatilhos Automáticos: A execução desses pipelines é automática, não exigindo comando manual.
PR Checks: Os status de CI são exigidos como verificação (check) obrigatória antes de um merge, embora a aprovação do PR seja manual.
  
3. **O workflow adotado favorece contribuições externas da comunidade open source?**

**Respostas**
- `meta-llama/Meta-Llama-3.1-70B-Instruct`: O workflow adotado pelo projeto vanna-ai/vanna parece não favorecer contribuições externas da comunidade open source.
Elementos que sustentam essa resposta incluem:
Convenção de contribuição: A documentação do projeto não menciona explicitamente como contribuir, o que pode dificultar para os contribuidores externos compreender como participar.
Privacidade do repositório: O repositório é privado, o que pode limitar o acesso a contribuidores externos.
Nenhuma evidência de processos de colaboração: Não há evidências de processos de colaboração, como listas de contribuidores, contribuições de membros da comunidade, etc.
- `Qwen/Qwen2.5-72B-Instruct`: Sim, o workflow adotado pelo projeto vanna-ai/vanna apresenta características que favorecem contribuições externas da comunidade open source.
Evidências que sustentam:
Repositório Público: O projeto é aberto no GitHub, permitindo acesso total ao código, issues e pull requests por qualquer pessoa.
Documentação de Contribuição: Há um arquivo CONTRIBUTING.md que estabelece diretrizes claras para contribuidores, incluindo como reportar bugs, sugerir features e o processo para enviar Pull Requests (PRs). Isso reduz a barreira de entrada.
Uso Estruturado de Issues e PRs: O projeto utiliza o sistema de Issues do GitHub para gerenciar bugs e discussões, e todas as mudanças são integradas via Pull Requests, que passam por revisão e checagens automáticas de CI. Este é um padrão bem compreendido pela comunidade open source.
Ambiente de Desenvolvimento Documentado: O README.md e/ou CONTRIBUTING.md frequentemente inclui instruções para configurar o ambiente de desenvolvimento local, facilitando o início de novos contribuidores.

## Conclusão

# Comparação de Modelos de IA  


| Nº | Tema | Pergunta | `meta-llama/Meta-Llama-3.1-70B-Instruct` | Modelo B | Modelo C |
|----|------|----------|----------|----------|----------|
| 1 | Releases | Analisando o repositório `vanna-ai/vanna`, que tipo(s) de estratégia de release o projeto aparenta utilizar? | | | |
| 2 | Releases | O projeto está mais alinhado a *Continuous Delivery* ou *Continuous Deployment*? Justifique. | | | |
| 3 | Releases | Os releases são majoritariamente *major*, *minor* ou *patch*? O que isso indica sobre a maturidade do projeto? | | | |
| 4 | Workflow | Qual modelo de workflow o projeto mais se aproxima (*GitHub Flow*, *Trunk-Based*, *GitFlow*)? | | | |
| 5 | Workflow | O fluxo de desenvolvimento é mais automatizado (CI/CD) ou manual? Quais evidências sustentam isso? | | | |
| 6 | Workflow | O workflow favorece contribuições externas da comunidade open source? Explique. | | | |
