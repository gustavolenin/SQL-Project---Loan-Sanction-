# Loan Sanction

## Projeto em Desenvolvimento

![image](https://user-images.githubusercontent.com/69591172/215238996-679635ae-600e-4c3f-bc28-6e631d1ee77c.png)

Contextualização do problema:

**Sobre a companhia**:
A empresa Dream Housing Finance lida com todos os empréstimos para habitação. Eles estão presentes em todas as áreas urbanas, semi-urbanas e rurais. O cliente aplica-se primeiro para um empréstimo à habitação depois que a empresa valida a elegibilidade do cliente para um empréstimo.

**Problema**:
A empresa deseja automatizar o processo de elegibilidade do empréstimo (em tempo real) com base nos detalhes do cliente fornecidos durante o preenchimento do formulário de inscrição on-line. Esses detalhes são sexo, estado civil, escolaridade, número de dependentes, renda, valor do empréstimo, histórico de crédito e outros. Para automatizar esse processo, eles criaram um problema para identificar os segmentos de clientes elegíveis para valores de empréstimo para atingir esses clientes especificamente. Aqui eles forneceram um conjunto de dados parcial.

Para solucionar esse problema utilizou-se o MySQL no qual foram realizadas queries SQL com o objetivo de responder as perguntas de negócio especificadas a seguir.

**Perguntas de Negócio**

**1 - O montante do empréstimo varia em função do nível educacional do requerente?**

**Solução da Primeira Pergunta de Negócio**:

```
SELECT Education, AVG(Loan_Amount_Term) AS AVG_Loan FROM inputs.loan_sanction_train
GROUP BY Education
```

Resultado: 

![image](https://user-images.githubusercontent.com/69591172/215917486-4088ffaf-de54-45e4-ba98-08733d60c95e.png)

Verifica-se que pessoas com graduação obtiveram maiores valores de empréstimos quando comparado com os valores concedidos às pessoas sem graduação.

**2 - O montante do empréstimo varia em função go gênero e estado civil?**

**Solução da Segunda Pergunta de Negócio**:

```
SELECT Gender, Married, AVG(LoanAmount) AS AVG_Loan FROM inputs.loan_sanction_train
WHERE Gender IN('Male','Female')
GROUP BY Gender, Married
```

Resultado: 

![image](https://user-images.githubusercontent.com/69591172/215919624-08f47d3e-e728-4c93-837d-f0e4b3f43b04.png)

Nota-se que pessoas casadas receberam um crédito maior do que pessoas solteiras, além disso pode-se perceber também que, dentre os solteiros, as pessoas do sexo masculino obtiveram maiores valores de crédito concedidos.
