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


## Modelos
`meta-llama/Meta-Llama-3.1-70B-Instruct`



## Identificação de Tipos de Releases

### Perguntas padrões:
1. Analisando o repositório `vanna-ai/vanna`, que tipo(s) de estratégia de release o projeto aparenta utilizar  
   (ex.: *semantic versioning*, releases incrementais, release manual vs automatizado)? Justifique com evidências observáveis no repositório.

**Respostas**
- `meta-llama/Meta-Llama-3.1-70B-Instruct`: O projeto vanna-ai/vanna utiliza o Semantic Versioning, com base nas seguintes evidências:
Convenção de nomenclatura de tags: vX.Y.Z
Histórico de releases: mantido em CHANGELOG.md
Automatização de release: sugestão de uso de GitHub Actions

Isso indica que o projeto segue uma estratégia de release baseada no Semantic Versioning, com uma estrutura de release clara e automatizada.

2. O projeto `vanna-ai/vanna` está mais alinhado a um modelo de  
   *Continuous Delivery* ou *Continuous Deployment*? Explique com base no processo de publicação e integração contínua
**Respostas**
- `meta-llama/Meta-Llama-3.1-70B-Instruct`: Com base no processo de publicação e integração contínua, o projeto vanna-ai/vanna parece estar mais alinhado ao modelo de Continuous Delivery (CD).
Evidências que apoiam esta afirmação incluem:
GitHub Actions: O projeto utiliza GitHub Actions para automatizar o processo de build, testes e deploy. No entanto, a configuração das ações não sugere uma automação de deploy direto para produção.
Releases manuais: Embora o projeto utilize uma estratégia de release baseada no Semantic Versioning, as releases são realizadas manualmente, o que sugere que o processo de deploy ainda é controlado por humanos.
Nenhuma evidência de deploy automático: Não há nenhuma evidência de que o projeto tenha uma configuração de deploy automático para produção, o que é uma característica típica do CD.


3. Observando o histórico de versões, o projeto realiza com maior frequência releases do tipo  
   *major*, *minor* ou *patch*? O que isso indica sobre a estabilidade e maturidade do software?
**Respostas**
- `meta-llama/Meta-Llama-3.1-70B-Instruct`: Com base no histórico de versões do projeto vanna-ai/vanna, é possível observar que o projeto realiza com maior frequência releases do tipo patch. Isso indica que o projeto está em uma fase de desenvolvimento ativo e está focado em manter a estabilidade do software.


##  Identificação de Tipos de Workflow

1. Com base no uso de branches, pull requests e histórico de commits,  
   qual modelo de workflow o projeto mais se aproxima  
   (ex.: *GitHub Flow*, *Trunk-Based Development*, *GitFlow*)? 
   
**Respostas**
- `meta-llama/Meta-Llama-3.1-70B-Instruct`: Com base no uso de branches, pull requests e histórico de commits, o projeto vanna-ai/vanna parece seguir o GitHub Flow.
Isso é apoiado pelo fato de que:
Existem apenas duas branches principais: main e develop
Os pull requests são utilizados para revisar e aprová-los antes de merge-los na branch main
O histórico de commits sugere que os desenvolvedores trabalham diretamente na branch main e criam pull requests para revisar e aprová-los antes de merge-los.


  
2. O fluxo de desenvolvimento do `vanna-ai/vanna` é predominantemente  
   orientado à automação (CI/CD) ou a validações manuais? Identifique indícios claros no repositório
   
**Respostas**
- `meta-llama/Meta-Llama-3.1-70B-Instruct`: O fluxo de desenvolvimento do vanna-ai/vanna é predominantemente orientado à automação (CI/CD).
Isso é apoiado pelo uso de GitHub Actions para automatizar a build, testes e deploy, além da presença de scripts e ferramentas de automação no repositório.

  
3. O workflow adotado favorece contribuições externas da comunidade open source?

   
**Respostas**
- `meta-llama/Meta-Llama-3.1-70B-Instruct`: O workflow adotado pelo projeto vanna-ai/vanna parece não favorecer contribuições externas da comunidade open source.
Elementos que sustentam essa resposta incluem:
Convenção de contribuição: A documentação do projeto não menciona explicitamente como contribuir, o que pode dificultar para os contribuidores externos compreender como participar.
Privacidade do repositório: O repositório é privado, o que pode limitar o acesso a contribuidores externos.
Nenhuma evidência de processos de colaboração: Não há evidências de processos de colaboração, como listas de contribuidores, contribuições de membros da comunidade, etc.


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
