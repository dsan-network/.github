# DSAN — Proteção de branches e política de integração v0.1

**Status:** PROPOSTO, ainda não aplicado no GitHub.
**Escopo:** repositórios sob dsan-network autorizados ao gestor.
**Ponto de controle:** configuração administrativa pelo mantenedor.

## Contexto e intenção

Os projetos DSAN são experimentais e contêm componentes de segurança e propriedade intelectual. A branch `main` não deve ser alterada diretamente, salvo exceção documentada e autorizada. Aprovação de CI não implica revisão de código, homologação institucional ou autorização financeira.

As configurações de proteção **não são instaladas ao mesclar este documento**. Exigem regras de branch ou rulesets configurados na interface administrativa do GitHub ou por uma integração com permissão específica de administração.

## Regras de segurança propostas

1. Target: default branch `main` de cada repositório, preferencialmente usando rulesets em modo `Evaluate` antes de `Active`, quando disponível.
2. Exigir Pull Request para alteração da `main`; desabilitar force-push e exclusão da branch.
3. Exigir resolução de conversas de revisão antes do merge.
4. Exigir CI de testes reproduzíveis **somente para checks que realmente existam e executem no PR**. Evitar listar checks de workflows opcionais ou que não rodam naquele repositório.
5. Exigir ao menos **uma revisão independente** para mudanças normativas, segurança e código, se existir um segundo revisor autorizado. O autor não deve aprovar a própria alteração. Se não houver revisor independente disponível, primeiro criar a função/política de revisão; não ativar um requisito que impeça todo merge sem mecanismo de aprovação legítimo.
6. Restringir bypass ao mínimo necessário e documentar qualquer exceção; definir política de resposta para correções emergenciais.
7. Exigir atualização do PR com a `main` antes de mesclar quando a natureza dos testes demandar compatibilidade estrita; avaliar custo/risco de bloquear por conflitos ou runs desnecessárias.

## Critérios para checks de CI em cada repositório

O gestor deverá mapear, **em documento privado**, quais workflows efetivamente rodam em PRs de cada projeto autorizado e os nomes exatos dos respectivos jobs. Não publicar nomes, cobertura ou situação operacional de repositórios privados no perfil público da organização.

- Definir como obrigatório somente um check observado executando consistentemente em todos os PRs a que a regra se aplica.
- Diferenciar workflow, job e check; confirmar o nome exibido na interface do GitHub.
- Não habilitar checks que só existem em branches experimentais, ou que rodam apenas em paths que não abrangem todos os PRs.
- Antes de criar um requisito novo, confirmar que um segundo revisor autorizado pode cumprir eventual exigência de aprovação.

## Processo manual de ativação

1. Abrir o repositório no GitHub como administrador, `Settings → Rules → Rulesets` (ou `Settings → Branches`, de acordo com plano/interface).
2. Criar ruleset de branch aplicável à `main`; usar primeiro modo Evaluate se disponível.
3. Configurar PR obrigatório, ausência de força/exclusão e conversas resolvidas.
4. Configurar revisão independente apenas com revisor realmente disponível.
5. Escolher apenas os checks já observados nas execuções de PR e com nomes únicos.
6. Salvar a regra e testar com um PR não destrutivo. Comprovar que o branch rejeita alteração não autorizada e que check falho impede merge.
7. Registrar ID/link da regra, data e responsável no inventário da governança.
8. Repetir repositório por repositório; priorizar App, Guardian e DREX antes dos demais.

## Precauções

- As regras do GitHub para repositórios privados dependem do plano e das permissões administrativas. Se a interface não exibir a funcionalidade, verificar elegibilidade sem tornar os repositórios públicos apenas para ativá-la.
- Algumas contas pessoais ou organizações com um único revisor não conseguem cumprir uma regra de aprovação independente; não habilitar um gate impossível.
- GitHub Actions em verde significa que as verificações configuradas passaram; não significa conformidade normativa, segurança de produção ou prontidão Drex.
- Não incorporar laboratórios temporários de perfis de agentes à main de produtos: mantê-los em branches privadas de teste, fora das builds de produção.
- Quando uma nova automação CI for adicionada, revisar novamente os nomes e a abrangência dos checks obrigatórios antes de ativá-los.

## Critérios de aceite

- Main protegida efetivamente segundo API/UI após configuração administrativa; o arquivo por si só **não** prova proteção.
- PR normal exige CI pertinente e política de revisão conforme os papéis autorizados.
- Exceções documentadas e controladas.
- Nenhuma mudança de licença, especificação, patente ou conteúdo privado publicada por este documento.

## Referências do GitHub

- https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/creating-rulesets-for-a-repository
- https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches
- https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets
