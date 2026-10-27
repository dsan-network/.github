# DSAN Agents — Guia rápido de operação (v0.2)

**Status:** perfis Architect e Steward incorporados à branch principal organizacional. Ainda é necessário verificar descoberta, permissões efetivas e homologação funcional em uma sessão real do GitHub Copilot. Os perfis não trabalham continuamente em segundo plano, nem criam tickets, commits ou PRs automaticamente.

## 1. O que é um agente

Um arquivo `.agent.md` determina **papel, instruções e ferramentas disponíveis** ao Copilot. Não é um servidor nem um processo que fica continuamente executando. O ambiente anfitrião (VS Code, GitHub.com/Cloud Agent ou CLI) executa o perfil quando selecionado.

Os perfis organizacionais ficam em `/agents` na raiz do repositório da organização `dsan-network/.github`. Já dentro de um repositório de projeto, a pasta correta seria `.github/agents`. Não confundir.

## 2. Agentes configurados na organização

| Agente | Permissão | Uso |
| --- | --- | --- |
| DSAN Architect | somente `read` e `search`, seleção manual | Analisa definições normativas, interfaces e contratos; recomenda mudanças |
| DSAN Steward | somente `read` e `search`, seleção manual | Prepara inventário, prioriza issues e registra decisões pendentes |

Em ambos: `disable-model-invocation: true` e `user-invocable: true`. O usuário precisa escolher explicitamente o perfil. O agente pode não enxergar repositórios privados se a conta/integração não tiver as permissões necessárias.

## 3. Localizar os perfis e iniciar a homologação

1. O PR organizacional https://github.com/dsan-network/.github/pull/1 já foi incorporado; confira os arquivos `agents/*.agent.md` na `main`.
2. Verifique que a conta GitHub possui GitHub Copilot habilitado e acesso ao repositório-alvo; o serviço pode depender de políticas da organização.
3. No VS Code com GitHub Copilot Chat, autentique-se, abra um workspace autorizado e selecione `DSAN Architect` ou `DSAN Steward` no menu de agentes, quando disponíveis.
4. Alternativa: https://github.com/copilot/agents, escolhendo repositório e perfil no seletor de agentes.
5. Execute o roteiro `governance/AGENT-ACCEPTANCE-PLAYBOOK-v0.2-pt-BR.md`; registre evidências de execução **em local privado**. Não marque homologado apenas pela existência do perfil.
6. Caso o perfil não apareça, confira disponibilidade, políticas e permissões; **não torne um repositório privado público** apenas para destravar a descoberta.

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

Depois de homologar os dois papéis consultivos, avaliar `governance/DSAN-IMPLEMENTER-ROLE-v0.1.md` como especificação **ainda não operacional** de um implementador em sandbox. Exigir proteção efetiva da `main`, testes de isolamento e aprovação humana separada antes de conceder qualquer ferramenta de escrita. Um **DSAN Sentinel** poderá futuramente revisar segurança, também condicionado a uma avaliação específica.

Este guia é público e não contém achados específicos dos repositórios privados.
