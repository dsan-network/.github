# DSAN Agents — Guia rápido de operação (v0.1)

**Status:** instruções para perfis propostos em PR. Os perfis não trabalham em segundo plano e não criam tickets, commits ou PRs automaticamente. A ativação depende da disponibilidade de GitHub Copilot e da integração com a organização.

## 1. O que é um agente

Um arquivo `.agent.md` determina **papel, instruções e ferramentas disponíveis** ao Copilot. Não é um servidor nem um processo que fica continuamente executando. O ambiente anfitrião (VS Code, GitHub.com/Cloud Agent ou CLI) executa o perfil quando selecionado.

Os perfis organizacionais ficam em `/agents` na raiz do repositório da organização `dsan-network/.github`. Já dentro de um repositório de projeto, a pasta correta seria `.github/agents`. Não confundir.

## 2. Agentes que existem como proposta

| Agente | Permissão | Uso |
| --- | --- | --- |
| DSAN Architect | somente `read` e `search`, seleção manual | Analisa definições normativas, interfaces e contratos; recomenda mudanças |
| DSAN Steward | somente `read` e `search`, seleção manual | Prepara inventário, prioriza issues e registra decisões pendentes |

Em ambos: `disable-model-invocation: true` e `user-invocable: true`. O usuário precisa escolher explicitamente o perfil. O agente pode não enxergar repositórios privados se a conta/integração não tiver as permissões necessárias.

## 3. Ativar depois da revisão

1. Abrir o PR organizacional: https://github.com/dsan-network/.github/pull/1
2. Revisar diferenças de arquivos e instruções; conferir que perfis estão em `agents/*.agent.md`.
3. Mesclar apenas após aprovação do mantenedor.
4. Verificar que a conta GitHub tem recurso Copilot adequado, permissões e políticas organizacionais. Copilot Cloud Agent exige disponibilidade/habilitação na conta.
5. No VS Code com GitHub Copilot Chat: autenticar no GitHub, abrir o repositório desejado e selecionar `DSAN Architect` ou `DSAN Steward` no menu de agentes. A descoberta dos agentes organizacionais pode depender de versão/configuração.
6. Alternativa: no GitHub.com, abrir https://github.com/copilot/agents e selecionar o repositório e agente personalizado, se a funcionalidade estiver habilitada.

Documentação oficial: https://docs.github.com/en/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents

## 4. Primeiros comandos seguros (um por sessão)

### DSAN Architect

> Verifique, sem editar arquivos, a coerência entre a arquitetura pública DSAN-Ecosystem e os contratos expostos pelo dsan-core. Identifique arquivos e refs/SHAs revisados, diferenças confirmadas e hipóteses. Gere até três propostas de issues, cada uma com critério de aceitação e indicação de impacto. Não proponha divulgar material privado.

### DSAN Steward

> Faça uma revisão somente leitura dos PRs em aberto no repositório atual. Separe rascunho, checks de CI concluídos, riscos e aprovações pendentes. Prepare um plano de execução com no máximo três frentes e títulos propostos de issues. Não altere nada no GitHub.

## 5. Como gerenciar (rotina sob demanda)

**Entrada:** uma tarefa concreta vinculada a repo, branch e objetivo.  
**Planejamento:** Steward propõe prioridade e critérios.  
**Avaliação:** Architect aponta impacto arquitetural e os contratos que podem quebrar.  
**Decisão:** mantenedor autoriza o escopo exato.  
**Implementação:** outro agente com permissões explicitamente concedidas, ou pessoa desenvolvedora, abre PR com testes.  
**Validação:** CI e revisão independente; resultado de teste precisa de link verificável.  
**Conclusão:** mantenedor decide sobre o merge e registra o SHA final.

### Checklist de aprovação

- [ ] Fonte, repositório e branch corretos
- [ ] Ausência de segredos, dados pessoais e conteúdo de propriedade intelectual reservado
- [ ] Mudança sem alteração inesperada da arquitetura canônica
- [ ] Testes e CI executados, não apenas previstos
- [ ] Comparação com requisitos e política de segurança
- [ ] Licenciamento e direitos de publicação conferidos
- [ ] Aprovação humana explícita para merge

## 6. Vocabulário de gestão

- **Agente:** perfil especializado executado em uma ferramenta compatível.
- **Issue:** pedido de trabalho.
- **Branch:** área de alterações separada da principal.
- **Pull Request:** proposta de inclusão de alterações que necessita de revisão.
- **GitHub Actions:** automação dos testes. Não é, por si só, um agente de desenvolvimento.
- **Merge:** incorporação da mudança na branch alvo.
- **Draft:** PR ainda em preparação.
- **CI verde:** os checks configurados passaram; isso não equivale a auditoria independente.

## 7. Três erros a evitar

1. Confundir definição do perfil com agente instalado/ativo — o arquivo só é interpretado quando um produto compatível carrega esse perfil.
2. Esperar monitoramento contínuo de um agente chamado sob demanda.
3. Dar permissão de escrita aos perfis Architect/Steward sem antes validar relatórios, limites de acesso e a política de revisão.

## 8. Escalar o modelo

Depois de aprender os dois papéis consultivos e validar visibilidade/limitações, considerar um **DSAN Implementer** isolado, que edita somente branch de trabalho e nunca mescla, e um **DSAN Sentinel**, revisor de segurança. Qualquer permissão de escrita deve ser concedida explicitamente e revisada.

Este guia é público e não contém achados específicos dos repositórios privados.
