# Central de Conferência da Folha de Pagamento

Projeto desenvolvido em Excel com foco em **conferência, auditoria e acompanhamento mensal da folha de pagamento**.

A proposta da solução é permitir que o RH compare os cálculos internos da empresa com a folha recebida da contabilidade, identificando automaticamente divergências em proventos, descontos e salário líquido.

O projeto foi pensado para empresas que recebem mensalmente a folha calculada pela contabilidade e precisam realizar uma conferência antes da aprovação e do pagamento.

---

## Objetivo do Projeto

Centralizar em uma única planilha os principais processos de conferência da folha de pagamento, incluindo:

* cadastro de colaboradores;
* movimentações mensais;
* faltas;
* horas extras;
* comissões;
* bônus e gratificações;
* benefícios;
* INSS;
* IRRF;
* férias;
* 13º salário;
* rescisões;
* comparação com a folha da contabilidade;
* diagnóstico automático de divergências;
* checklist mensal do RH;
* histórico por competência.

A solução funciona como uma camada de **auditoria e conferência**, e não como um sistema oficial de folha de pagamento.

---

# Visão Geral do Fluxo

O fluxo mensal foi estruturado da seguinte forma:

```text
Cadastro de Funcionários
        ↓
Movimentações do RH
        ↓
Cálculo Esperado
        ↓
Importação da Folha da Contabilidade
        ↓
Conferência
        ↓
Diagnóstico de Divergências
        ↓
Checklist Mensal
        ↓
Aprovação da Folha
```

---

# Estrutura da Planilha

## Dashboard

Visão resumida da competência atual.

Apresenta indicadores como:

* quantidade de funcionários;
* folha bruta calculada;
* folha líquida;
* total de descontos;
* quantidade de registros OK;
* quantidade de registros para revisão;
* pendências de conferência.

O objetivo é permitir uma leitura rápida do status do fechamento da folha.

---

## Cadastro

Base principal dos colaboradores.

Contém informações como:

* matrícula;
* nome;
* CPF;
* status;
* cargo;
* departamento;
* centro de custo;
* data de admissão;
* salário-base;
* jornada mensal;
* dependentes;
* vale-transporte;
* VA/VR;
* plano de saúde;
* descontos fixos;
* observações.

Essa base representa os dados permanentes ou de baixa frequência de alteração dos funcionários.

---

## Movimentações

Aba destinada aos eventos variáveis da competência.

Exemplos:

* faltas;
* horas extras 50%;
* horas extras 100%;
* comissões;
* bônus;
* gratificações;
* adicionais;
* créditos extras;
* descontos extras.

Cada movimentação é vinculada a:

```text
Competência + Matrícula
```

Dessa forma é possível manter histórico de vários meses na mesma base.

---

## Parâmetros

Centraliza valores utilizados nos cálculos.

Exemplos:

* competência ativa;
* dias úteis;
* domingos e feriados;
* base de dias do mês;
* jornada mensal;
* tolerância de divergência;
* percentuais de horas extras;
* parâmetros de VT;
* tabela de INSS;
* parâmetros de IRRF.

Essa estrutura evita que valores sejam inseridos diretamente dentro das fórmulas.

---

# Importação Contabilidade

Essa é uma das principais abas da solução.

Todos os meses, a folha recebida da contabilidade deve ser adicionada nessa tabela.

A chave utilizada para localizar os funcionários é:

```text
Competência + Matrícula
```

Exemplo:

```text
09/2026 | 1001
09/2026 | 1002
10/2026 | 1001
10/2026 | 1002
```

Os meses anteriores não precisam ser apagados.

Dessa forma a planilha mantém um histórico completo de auditoria.

Entre os valores que podem ser importados estão:

* desconto de falta;
* DSR sobre falta;
* hora extra 50%;
* hora extra 100%;
* comissão;
* bônus;
* adicionais;
* DSR sobre horas extras;
* DSR sobre comissão;
* vale-transporte;
* INSS;
* IRRF;
* VA/VR;
* plano de saúde;
* outros descontos;
* salário bruto;
* total de descontos;
* salário líquido.

---

# Conferência

A aba de Conferência é o núcleo do projeto.

Ela compara automaticamente:

```text
Valor Calculado pelo RH
x
Valor Recebido da Contabilidade
```

São analisados principalmente:

* Bruto Calculado;
* Bruto Contabilidade;
* Total de Descontos Calculado;
* Descontos Contabilidade;
* Líquido Calculado;
* Líquido Contabilidade.

A planilha calcula automaticamente:

```text
Diferença Bruto
Diferença Descontos
Diferença Líquido
```

---

## Status de Conferência

Cada funcionário recebe um status.

### OK

Os valores calculados estão dentro da tolerância definida.

```text
OK
```

---

### REVISAR

Existe diferença acima da tolerância permitida.

```text
REVISAR
```

Nesse caso a investigação deve continuar na aba de Diagnóstico.

---

### PENDENTE IMPORTAÇÃO

O funcionário existe no RH, mas ainda não foi localizado na folha da contabilidade para aquela competência.

```text
PENDENTE IMPORTAÇÃO
```

Isso ajuda a identificar rapidamente problemas de importação ou colaboradores ausentes no arquivo recebido.

---

# Diagnóstico de Divergências

Quando um funcionário aparece como `REVISAR`, a aba de Diagnóstico permite descobrir a provável origem da diferença.

A comparação é feita rubrica por rubrica.

Exemplo:

```text
Comissão Calculada:       R$ 4.200,00
Comissão Contabilidade:   R$ 4.100,00

Diferença:                R$ 100,00
```

Resultado:

```text
REVISAR
Provável origem: Comissão
Diferença: R$ 100,00
```

Outro exemplo:

```text
INSS Calculado:          R$ 599,08
INSS Contabilidade:      R$ 664,08

Diferença:              -R$ 65,00
```

Resultado:

```text
REVISAR
Provável origem: INSS
Diferença: R$ 65,00
```

Essa abordagem reduz significativamente o tempo necessário para investigar divergências.

---

# Férias

Controle complementar de férias contendo informações como:

* período aquisitivo;
* período concessivo;
* início das férias;
* fim das férias;
* quantidade de dias;
* abono;
* status;
* valores relacionados.

Essa aba auxilia o RH na conferência mensal e no acompanhamento de períodos próximos ao vencimento.

---

# 13º Salário

Controle histórico do décimo terceiro salário.

Permite acompanhar:

* avos;
* salário-base;
* médias variáveis;
* primeira parcela;
* segunda parcela;
* INSS;
* IRRF;
* valores líquidos.

Também ajuda na validação de admissões, afastamentos e desligamentos durante o ano.

---

# Rescisões

Base de conferência das rescisões.

Pode conter:

* data de desligamento;
* motivo;
* saldo de salário;
* aviso prévio;
* férias;
* 13º proporcional;
* FGTS;
* descontos;
* valor total da rescisão.

Essa aba funciona como histórico de desligamentos e apoio à auditoria.

---

# Checklist Mensal

Foi criado um checklist completo para acompanhar o fechamento da folha.

Atualmente o processo contempla aproximadamente 45 pontos de conferência.

Entre eles:

* competência;
* cadastro;
* admissões;
* ponto;
* faltas;
* DSR;
* horas extras;
* banco de horas;
* comissões;
* benefícios;
* INSS;
* IRRF;
* FGTS;
* férias;
* 13º;
* afastamentos;
* rescisões;
* eSocial;
* FGTS Digital;
* DCTFWeb;
* pagamento;
* aprovação.

Cada item pode receber um dos seguintes status:

```text
Pendente
Em conferência
Conferido
Revisar
Não se aplica
```

Também é possível registrar:

* responsável;
* data da conferência;
* evidência;
* observações.

---

# Processo Mensal Recomendado

## 1. Atualizar competência

Na aba `Parâmetros`, alterar a competência ativa.

Exemplo:

```text
09/2026
```

---

## 2. Atualizar cadastro

Registrar:

* admissões;
* desligamentos;
* alterações salariais;
* mudanças de cargo;
* mudanças de benefícios.

---

## 3. Inserir movimentações

Adicionar eventos da competência.

Exemplo:

```text
09/2026 | 1001 | HE 50% | 8 horas
09/2026 | 1001 | Comissão | R$ 4.200
09/2026 | 1004 | Falta | 1 dia
```

---

## 4. Importar a folha da contabilidade

Na aba:

```text
Importação Contabilidade
```

adicionar os dados recebidos.

Não apagar competências anteriores.

---

## 5. Analisar a Conferência

Filtrar principalmente:

```text
REVISAR
PENDENTE IMPORTAÇÃO
```

---

## 6. Investigar divergências

Abrir a aba:

```text
Diagnóstico
```

e verificar a verba indicada como provável origem do problema.

---

## 7. Atualizar Checklist

Registrar:

* status;
* responsável;
* data;
* evidência;
* justificativas.

---

## 8. Aprovar fechamento

A folha só deve ser aprovada após todas as divergências estarem:

```text
Corrigidas
ou
Justificadas
```

---

# Conceitos Utilizados

## Competência

Mês ao qual a folha se refere.

Exemplo:

```text
09/2026
```

---

## Proventos

Valores que aumentam a remuneração.

Exemplos:

* salário;
* comissão;
* hora extra;
* bônus;
* gratificação;
* adicionais.

---

## Descontos

Valores abatidos da remuneração.

Exemplos:

* INSS;
* IRRF;
* VT;
* plano de saúde;
* faltas;
* outros descontos.

---

## DSR

Descanso Semanal Remunerado.

Determinadas verbas variáveis podem gerar reflexos no DSR.

---

## HE

Hora Extra.

Neste projeto são considerados exemplos de:

```text
HE 50%
HE 100%
```

---

## INSS

Contribuição previdenciária calculada de acordo com a base e as regras vigentes da competência.

---

## IRRF

Imposto de Renda Retido na Fonte.

---

## FGTS

Fundo de Garantia do Tempo de Serviço.

É encargo do empregador e não deve ser tratado como desconto comum do salário líquido do empregado.

---

## Rubrica

Identificação de uma verba da folha.

Exemplos:

```text
Salário
Comissão
INSS
IRRF
Hora Extra
Vale Transporte
```

---

## Divergência

Diferença entre o valor esperado e o valor recebido da contabilidade.

---

## Conciliação

Processo de comparação entre duas fontes de dados para identificar inconsistências.

---

# Principais Regras de Auditoria

A solução segue alguns princípios importantes:

### Não conferir apenas o total geral

Uma diferença positiva de um funcionário pode compensar uma diferença negativa de outro.

Por isso a conferência é realizada individualmente.

---

### Sempre manter histórico

As competências anteriores não devem ser apagadas.

Isso permite:

* auditoria;
* rastreabilidade;
* comparação mensal;
* identificação de erros recorrentes.

---

### Trabalhar com tolerância

Pequenas diferenças de arredondamento podem existir.

Por isso existe um parâmetro de tolerância.

Exemplo:

```text
Tolerância = R$ 1,00
```

Diferenças inferiores ao limite podem permanecer como `OK`.

---

# Análise de Variação da Folha

Além da conferência individual, a solução pode ser utilizada para analisar variações entre competências.

Exemplo:

```text
Folha Agosto:     R$ 280.000
Folha Setembro:   R$ 315.000

Variação:         +R$ 35.000
```

A análise deve buscar explicar o aumento através de fatores como:

* novas admissões;
* reajustes;
* comissões;
* bônus;
* horas extras;
* férias;
* rescisões.

Esse processo também pode ser chamado de:

```text
Payroll Variance Analysis
```

---

# Tecnologias e Recursos Utilizados

* Microsoft Excel
* Fórmulas de Excel
* SUMIFS
* COUNTIFS
* validação de dados
* formatação condicional
* tabelas estruturadas
* lógica de conciliação
* controle histórico por competência
* conceitos de auditoria de folha
* conceitos de RH / Departamento Pessoal

---

# Possíveis Evoluções

O projeto pode evoluir futuramente para:

* importação automática por Power Query;
* leitura direta de arquivos CSV/XLSX da contabilidade;
* banco de dados histórico;
* dashboard em Power BI;
* análise de Payroll Variance;
* alerta automático de divergências;
* histórico de alterações;
* aprovação por usuário;
* controle de SLA do fechamento;
* integração com sistema de ponto;
* integração com ERP;
* integração com sistemas de RH;
* automatização através de Python.

---

# Observação Importante

Este projeto tem finalidade de **conferência, controle e auditoria**.

Ele não substitui:

* sistema oficial de folha;
* contabilidade;
* departamento pessoal;
* eSocial;
* FGTS Digital;
* DCTFWeb;
* validação jurídica ou trabalhista.

Tabelas, percentuais, incidências e regras devem sempre ser atualizados conforme a competência e a legislação vigente.

---

# Autor

Projeto desenvolvido como solução de análise e conferência de folha de pagamento, combinando conceitos de:

* análise de dados;
* auditoria;
* automação;
* Excel;
* RH;
* Departamento Pessoal.

A proposta principal é transformar um processo manual de conferência em um fluxo mais organizado, rastreável e orientado a dados.
