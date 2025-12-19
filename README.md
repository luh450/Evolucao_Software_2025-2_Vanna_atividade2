# Evolucao_Software_2025-2_Vanna_atividade2


**Projeto analisado:** https://github.com/vanna-ai/vanna 


## Integrantes
Josias Ribeiro de Freitas Júnior - 202200025644

Natalia Silva Santos - 202400018206

Luzia dos Santos Souza Neta - 201700017537

Anthony Amoz Santos Aragao - 202100011207


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



## Tutorial no chathugging

Todos os modelos utilizados neste trabalho foram executados por meio do ChatHugging (Hugging Face), que atua como interface para acesso e uso de modelos de linguagem pré-treinados. Essa abordagem permitiu testar modelos mais robustos e de grande porte sem a necessidade de utilizar um computador local com alto poder computacional.

Acesse: https://huggingface.co/chat/

Do lado inferior à esquerda é possivel selecionar o modelo a ser utilizado
<img width="1484" height="857" alt="image" src="https://github.com/user-attachments/assets/7af9a0b5-ea23-4ad3-ba4f-9fe78cbf5fd4" />

São diversos modelos que podem ser utilizados. Só procurar o modelo que deseja.
<img width="1397" height="792" alt="image" src="https://github.com/user-attachments/assets/8ea99630-4f88-4e31-9b2c-dded4f01ecdb" />

Após selecionar já é possível utilizar o modelo

## Tutorial em máquina local

**Requisitos mínimos:**
`meta-llama/Meta-Llama-3.1-70B-Instruct`
- GPU: **≥ 140 GB de VRAM** (ex.: 2× A100 80GB ou equivalente)
- RAM: **≥ 128 GB**
- Armazenamento: **≥ 150 GB**
- CUDA + drivers compatíveis
- Frameworks: PyTorch + suporte a multi-GPU

**link para notebook:** https://huggingface.co/meta-llama/Llama-3.1-70B-Instruct/colab

**Código**
```python
# Instalar dependências
!pip install -q transformers accelerate torch
from transformers import AutoModelForCausalLM, AutoTokenizer
import torch
# Carregar tokenizer e modelo
model_name = "meta-llama/Meta-Llama-3.1-70B-Instruct"

tokenizer = AutoTokenizer.from_pretrained(
    model_name,
    trust_remote_code=True
)

model = AutoModelForCausalLM.from_pretrained(
    model_name,
    torch_dtype=torch.bfloat16,
    device_map="auto",
    trust_remote_code=True
)
```



`Qwen/Qwen2.5-72B-Instruct`
- GPU: **≥ 140 GB de VRAM**
- RAM: **≥ 128 GB**
- Armazenamento: **≥ 150 GB**
- Suporte a paralelismo de modelo
  
**link para notebook:** https://huggingface.co/Qwen/Qwen2.5-72B-Instruct/colab
**Código**
```python
# Instalar dependências
!pip install -q transformers accelerate torch

from transformers import AutoModelForCausalLM, AutoTokenizer
import torch
# Carregar tokenizer e modelo
model_name = "Qwen/Qwen2.5-72B-Instruct"

tokenizer = AutoTokenizer.from_pretrained(
    model_name,
    trust_remote_code=True
)

model = AutoModelForCausalLM.from_pretrained(
    model_name,
    torch_dtype=torch.float16,
    device_map="auto",
    trust_remote_code=True
)
```

## Modelos
`meta-llama/Meta-Llama-3.1-70B-Instruct` : https://huggingface.co/meta-llama/Llama-3.1-70B-Instruct

`Qwen/Qwen2.5-72B-Instruct` : https://huggingface.co/Qwen/Qwen2.5-72B-Instruct

`google/gemma-3-27b-it`  : https://huggingface.co/bigcode/starcoder

## Justificativa dos modelos escolhidos
1. `meta-llama/Meta-Llama-3.1-70B-Instruct` : deve-se à sua alta capacidade de compreensão semântica, raciocínio contextual e seguimento de instruções complexas. Por se tratar de um modelo de grande porte (70B parâmetros), ele apresenta desempenho superior na identificação de padrões implícitos em textos técnicos, como estratégias de release e modelos de workflow, mesmo quando essas informações não estão explicitamente estruturadas. Além disso, o modelo é otimizado para tarefas instruction-following, o que o torna especialmente adequado para analisar descrições de processos, inferir fluxos de trabalho e classificar tipos de releases a partir de documentação e código-fonte.
2. `Qwen/Qwen2.5-72B-Instruct` : justifica-se por ser um modelo de linguagem de grande escala (72.7B parâmetros) otimizado para seguir instruções (instruction-tuned), com capacidades avançadas de raciocínio, compreensão de contexto longo (até 128K tokens) e geração de texto estruturado, como JSON. Seu desempenho competitivo em benchmarks de código e raciocínio geral, aliado a um treinamento especializado em matemática e programação, o torna particularmente adequado para analisar repositórios de software, inferir fluxos de trabalho a partir de documentação técnica e identificar padrões complexos em commits, pull requests e configurações de CI/CD

3. `google/gemma-3-27b-it` : Este modelo foi escolhido por sua alta capacidade de compreensão de linguagem natural e raciocínio contextual, sendo adequado para tarefas que envolvem análise de documentação técnica, descrição de processos de software e inferência de fluxos de trabalho. Seu grande número de parâmetros (70B) permite capturar padrões complexos em textos não estruturados, o que é relevante para compreender requisitos, estratégias de release e decisões arquiteturais a partir de documentos e descrições técnicas. Além disso, por ser otimizado para seguir instruções, o modelo apresenta bom desempenho em tarefas analíticas e explicativas..

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

- `google/gemma-3-27b-it` : O projeto Vanna-AI/Vanna utiliza uma estratégia de release que combina o Semantic Versioning para gerenciar o versionamento de forma clara e consistente, um processo de release manual para iniciar o pipeline de publicação de um pacote Python, impulsionado pelo evento de criação de tags, e adota releases incrementais.  A automação é aplicada na parte de entrega (CD), mas a parte de criação da release (tag) é feita manualmente. Isso dá aos mantenedores do projeto controle sobre quando e como as novas versões são lançadas.


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

- `google/gemma-3-27b-it` : O projeto Vanna-AI/Vanna demonstra um forte alinhamento com um modelo de Continuous Delivery (CD), em vez de Continuous Deployment. A análise dos workflows de CI/CD revela que, embora a construção, teste e preparação para lançamento sejam automatizados – evidenciado pelo workflow python-publish.yaml que publica o pacote Python no PyPI –, o gatilho para esse processo é a publicação de uma release, que por sua vez é iniciada pela criação manual de uma tag. Essa intervenção humana no processo de lançamento é a principal característica que distingue CD de Continuous Deployment, onde cada alteração aprovada nos testes seria automaticamente liberada em produção. A presença de uma versão "rc1" (Release Candidate 1) no arquivo pyproject.toml também sugere um lançamento controlado e em etapas, comum em CD para testes adicionais antes da liberação final. Além disso, a opcionalidade de dependências relacionadas a servidores (Flask e FastAPI) demonstra que a Vanna oferece flexibilidade na implantação, permitindo que o usuário escolha a configuração desejada, o que é mais típico de um modelo de entrega onde a equipe fornece as ferramentas, mas o controle da implantação reside no usuário. Em resumo, a automação é utilizada para agilizar o processo, mas a decisão final sobre o lançamento é mantida pela equipe de desenvolvimento, caracterizando claramente a adoção de Continuous Delivery.

3. **Observando o histórico de versões, o projeto realiza com maior frequência releases do tipo  
   *major*, *minor* ou *patch*? O que isso indica sobre a estabilidade e maturidade do software?**
**Respostas**
- `meta-llama/Meta-Llama-3.1-70B-Instruct`: Com base no histórico de versões do projeto vanna-ai/vanna, é possível observar que o projeto realiza com maior frequência releases do tipo patch. Isso indica que o projeto está em uma fase de desenvolvimento ativo e está focado em manter a estabilidade do software.
- `Qwen/Qwen2.5-72B-Instruct`:  O projeto realiza mais releases do tipo patch. Isso indica um foco ativo na estabilidade (correções rápidas) e um desenvolvimento ágil, mas ainda não atingiu a maturidade completa (versão 0.x.y).

- `google/gemma-3-27b-it` : Analisando o histórico de releases do projeto Vanna, percebe-se uma predominância de releases do tipo patch, seguidos por releases minor, enquanto releases major são menos frequentes. Essa distribuição indica um foco na estabilidade e na correção de bugs, com melhorias incrementais e adição de funcionalidades mantendo a compatibilidade com versões anteriores. A predominância de patch releases sugere que a equipe prioriza resolver problemas rapidamente e manter o software confiável, enquanto os releases minor demonstram um amadurecimento gradual do projeto. A menor frequência de releases major indica que mudanças significativas na API ou arquitetura são cuidadosamente planejadas e implementadas, minimizando o risco de breaking changes para os usuários. No geral, o padrão de releases demonstra um projeto ativo, em desenvolvimento contínuo, priorizando a estabilidade e uma evolução controlada em direção à maturidade.


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

- `google/gemma-3-27b-it` : Com base na análise do uso de branches, pull requests e histórico de commits no repositório Vanna-AI/Vanna, o modelo de workflow mais aderente é o GitHub Flow. O projeto demonstra um padrão de branching simplificado, com branches de curta duração criadas a partir do main para desenvolvimento de features ou correções. Todas as contribuições são submetidas através de pull requests, que servem como ponto central para revisão de código e discussão, e são integradas ao main somente após aprovação e sucesso nos testes de integração contínua. Essa abordagem, aliada ao uso do main como fonte de verdade e um fluxo de lançamento acionado por tags, caracteriza o GitHub Flow. Outros modelos como GitFlow, com branches de longa duração como develop e release, são menos evidentes, e o Trunk-Based Development, que exige commits frequentes diretamente no tronco principal, também não se encaixa no padrão observado. A estrutura de branches, o histórico de commits mostrando merges de pull requests para o main, e o padrão consistente de pull requests para todas as contribuições reforçam essa conclusão. Em resumo, o projeto adota um fluxo de trabalho ágil e eficiente, simplificado e focado na colaboração e entrega rápida de valor, típico do GitHub Flow.

  
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

- `google/gemma-3-27b-it` : O fluxo de desenvolvimento do projeto Vanna-AI/Vanna é significativamente orientado à automação, impulsionado por práticas de CI/CD. A evidência disso reside nos workflows tests.yml e python-publish.yaml, que automatizam a execução de testes a cada alteração no código e a publicação do pacote Python no PyPI, respectivamente. A existência desses workflows demonstra um compromisso em validar automaticamente as contribuições e agilizar o processo de lançamento. Embora a automação seja predominante, validações manuais também desempenham um papel crucial, principalmente na fase de release, onde a criação de tags (que iniciam o pipeline de CD) e a aprovação de pull requests demandam intervenção humana. A utilização de versões "release candidate" sugere ainda um período de testes adicionais, possivelmente incluindo validações manuais, antes do lançamento final. Em suma, o projeto equilibra a eficiência da automação com a supervisão humana para garantir a qualidade e a estabilidade do software, mas a automação é, sem dúvida, a força motriz por trás do seu fluxo de desenvolvimento.
  
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

- `google/gemma-3-27b-it` : O workflow adotado pelo projeto Vanna-AI/Vanna demonstra um favorecimento a contribuições externas da comunidade open source, embora existam oportunidades de aprimoramento. A utilização de pull requests como o principal meio de contribuição, a natureza aberta do código, e a presença de uma comunidade ativa no Discord são indicativos de uma postura receptiva a colaboradores externos. A licença open source, que permite o uso, modificação e distribuição do código, também incentiva a participação da comunidade. Contudo, a ausência de um guia de contribuição detalhado, que explicite como configurar o ambiente de desenvolvimento e seguir as convenções de código, pode dificultar a entrada de novos colaboradores. Da mesma forma, a falta de issues marcadas como "good first issue" ou "help wanted" pode desencorajar iniciantes que buscam oportunidades de contribuir. Embora o projeto seja aberto à colaboração, fornecer um guia mais abrangente e identificar tarefas adequadas para novos colaboradores tornaria o processo mais acessível e convidativo, fortalecendo ainda mais o envolvimento da comunidade.

# Conclusão

A análise comparativa entre os modelos Qwen e LLaMA indicou que não houve diferenças significativas de desempenho na tarefa de identificação de estratégias de *release* e modelos de *workflow* a partir dos textos analisados. Além disso, a inclusão do modelo Google Gemma-3-27B-IT na avaliação reforçou essa constatação, uma vez que o modelo apresentou resultados qualitativamente alinhados aos obtidos pelos modelos de maior porte, mesmo possuindo menor número de parâmetros.


Ambos os modelos apresentaram níveis semelhantes de correção conceitual, completude e aderência ao contexto, sendo capazes de reconhecer os principais padrões de workflow e práticas de *release* descritos nos cenários avaliados. O uso da terminologia técnica também foi, em geral, consistente entre os dois modelos, com variações pontuais que não impactaram de forma relevante o resultado final da avaliação. já o modelo Gemma demonstrou boa compreensão de documentação técnica e processos de engenharia de software, mantendo coerência terminológica e clareza explicativa compatíveis com os demais modelo analisados.

No que se refere à presença de alucinações, observou-se um comportamento comparável entre os modelos, com baixa incidência de informações não suportadas pelo texto de entrada. As diferenças identificadas foram pontuais e não suficientes para caracterizar superioridade clara de um modelo em relação ao outro. O modelo Gemma apresentou padrão semelhante nesse aspecto, com ocorrências pontuais e controladas, não comprometendo a confiabilidade geral das respostas.

Dessa forma, os resultados sugerem que tanto o Qwen quanto o LLaMA são adequados para tarefas de análise e classificação de workflows e estratégias de release, desde que aplicados em contextos semelhantes aos avaliados neste estudo. Os resultados obtidos com o modelo Google Gemma indicam que ele também se mostra adequado para esse tipo de tarefa, especialmente em cenários que demandam menor custo computacional ou restrições de infraestrutura. A escolha entre os modelos pode, portanto, considerar outros fatores, como custo computacional, disponibilidade, facilidade de integração e requisitos de infraestrutura, em vez de desempenho qualitativo das respostas.


## Comparação de Modelos de IA  

## Critérios de Avaliação das Respostas

As respostas geradas pelos modelos de linguagem foram avaliadas com base nos seguintes critérios:

### 1. Correção Conceitual
Avalia se a resposta apresentada está tecnicamente correta em relação aos conceitos de *releases* e modelos de *workflow* de desenvolvimento de software.

- **0** – Resposta incorreta  
- **1** – Parcialmente correta  
- **2** – Correta  

---

### 2. Completude
Avalia o nível de abrangência da resposta, considerando se todos os elementos relevantes presentes no texto ou workflow analisado foram identificados.

- **0** – Muito incompleta  
- **1** – Parcial  
- **2** – Completa  

---

### 3. Aderência ao Contexto
Avalia se a resposta foi construída com base no conteúdo fornecido como entrada, evitando generalizações ou suposições não fundamentadas.

- **0** – Genérica ou fora de contexto  
- **1** – Parcialmente aderente  
- **2** – Totalmente aderente  

---

### 4. Precisão Terminológica
Avalia o uso adequado e consistente de termos técnicos relacionados a estratégias de *release* e modelos de *workflow*, como *Git Flow*, *Trunk-Based Development*, *Canary Release* e *CI/CD*.

- **0** – Uso incorreto de terminologia  
- **1** – Uso correto, porém superficial ou vago  
- **2** – Uso correto e preciso  

---

### 5. Presença de Alucinações
Avalia se o modelo introduziu informações que não estão presentes no texto ou que não podem ser inferidas a partir dele.

- **0** – Nenhuma alucinação identificada  
- **-1** – Alucinação leve  
- **-2** – Alucinação grave

- 
| Modelo | Correção | Completude | Aderência | Precisão | Alucinação | Score Final |
|------|----------|------------|-----------|----------|------------|-------------|
| Qwen | 2 | 1 | 2 | 2 | 0 | 7 |
| LLaMA | 2 | 1 | 2 | 2 | 0 | 7 |
| Google Gemma | 2 | 1 | 2 | 1 | 0 | 6 |


