# # Relatório de Testes Brasa Lembretes

## 1. Técnicas de teste utilizadas

- Partição de equivalência: aplicada aos campos do formulário de novo lembrete.
- Análise de valor limite: aplicada às validações de data, hora e campos obrigatórios.
- Teste exploratório baseado em sessão: realizado com o uso de heuristica


## 2. Artefatos utilizados

- [Casos de teste baseados na ISO 29119-3](./Casos_de_Teste_ISO_29119-3.md)
- [Casos de teste em formato Gherkin](./Casos%20de%20Teste%20em%20Gherkin.md)
- [Checklist de casos de teste](./checklist-casos-de-teste.md)
- [Condições de teste](./Condicoes%20de%20Teste.md)
- [Relatório de sessão](./Relatorio_de_Sessao.md)
- [Registro do defeito conforme a ISO 29119-3](Defeito.md)
- [Experimento com IA](./ExperimentoIA.md)


## 3. Execução dos testes

Acompanhe o status de cada caso no [Checklist de casos de teste](./checklist-casos-de-teste.md).

| Métrica | Quantidade |
| --- | ---: |
| Casos planejados | 124 |
| Casos executados | 107 |
| Passaram | 105 |
| Falharam | 2 |
| Bloqueados | 14 |
| Não executados | 3 |
| Defeitos encontrados | 3 |


## 4. Relato de defeitos

### DEF-01 — Mensagem inadequada para data inválida

- **Descrição:** ao informar a data inválida `29/02/2027`, o sistema exibe as mensagens “Precisa ser uma data e hora futura” e “Informe a data e a hora do lembrete”, sem indicar que a data informada não existe.
- **Impacto:** as mensagens não explicam o motivo da rejeição e podem confundir o usuário.
- **Prioridade / severidade:** baixa.
- **Rastreabilidade:** identificado durante o [Relatório de Sessão 1](./Relatorio_de_Sessao.md#relat%C3%B3rio-de-sess%C3%A3o-1).
- **Registro completo e evidência:** [Defeito 01](./Defeito.md#defeito-01).
  
### DEF-02 — Indicador da fila do alerta não acompanha a sequência correta

- **Descrição:** ao disparar três alertas simultâneos, o primeiro alerta não exibe o indicador da fila (esperado “1 de 3”), e ao marcar como visto o primeiro item a contagem reinicia para “1 de 2” em vez de “2 de 3”.
- **Impacto:** a navegação entre alertas fica inconsistente e a fila não reflete corretamente o estado real dos lembretes pendentes.
- **Prioridade / severidade:** média / baixa.
- **Rastreabilidade:** identificado no caso de teste [CT-055](./Casos%20de%20Teste%20em%20Gherkin.md#ct-055)
- **Registro completo e evidência:** [Defeito 02](./Defeito.md#defeito-02).

### DEF-03 — Alerta de lembrete fica travado em uma das telas em caso de mais de uma aba aberta

- **Descrição:** ao marcar lembrete de uma das abas do navegador como "lido", o alerta em outra aba segue sendo exibido, e fica travado na tela.
- **Impacto:** é necessário recarregar a página para conseguir usar novamente.
- **Prioridade / severidade:** média / média.
- **Rastreabilidade:** identificado no caso de teste [CT-097](./Casos%20de%20Teste%20em%20Gherkin.md#ct-097)
- **Registro completo e evidência:** [Defeito 03](./Defeito.md#defeito-03).


## 5. Aprendizados

1. Experiência prévia ajuda no planejamento: foi possível planejar e executar os testes com base na experiência em aplicações semelhantes, o que deu mais segurança na definição dos cenários.
2. Casos de teste formais exigem tempo e organização: escrever os casos em Gherkin e no formato ISO é um trabalho demorado, e é preciso considerar esse esforço no planejamento da atividade.
3. Testes exploratórios funcionam bem quando as regras não estão claras: combinar estratégias exploratórias com heurísticas e critérios de verificação se mostrou muito útil em entregas com regras de negócio ainda pouco definidas.
4. Priorizar os testes concentra o esforço no que importa: quando não há tempo para executar todos os cenários, priorizar ajuda a cobrir primeiro os fluxos mais importantes.
5. Revisar os casos antes de executar evita problemas: a revisão dos casos de teste pode revelar lacunas de cobertura e casos duplicados antes mesmo da execução.
6. Evidências devem ser coletadas na hora em que o bug aparece: ao identificar um bug durante a execução, é necessário coletar a evidência e registrá-lo imediatamente. Neste projeto, um dos bugs foi apenas anotado para registro posterior e não foi mais possível reproduzi-lo imediatamente, o que gerou retrabalho e perda de informação.

## 6. Experimento com IA

Como parte do experimento, foi solicitado ao Claude Code que priorizasse os 50 casos mais críticos entre os 124 casos planejados, considerando a necessidade de validar a qualidade do sistema com pouco tempo disponível.

A seleção foi organizada por módulos e priorizou os fluxos essenciais dos lembretes — cadastro, alertas, conclusão, adiamento, recorrência e persistência —, além de validações de entrada, segurança e limites de data. Casos considerados redundantes ou de menor risco ficaram de fora. A análise também indicou quais casos deveriam ser incluídos primeiro caso houvesse mais tempo.

O [Experimento com IA](./ExperimentoIA.md) contém o prompt utilizado, a justificativa completa e a lista dos casos selecionados.

**Integrantes:** Dennys, Isabella Henriques, Patrick Aguiar, Taís Santos e Yara Rodrigues
