# Loan Sanction

![image](https://user-images.githubusercontent.com/69591172/215238996-679635ae-600e-4c3f-bc28-6e631d1ee77c.png)

Contextualização do problema:

**Sobre a companhia**:
A empresa Dream Housing Finance lida com todos os empréstimos para habitação. Eles estão presentes em todas as áreas urbanas, semi-urbanas e rurais. O cliente aplica-se primeiro para um empréstimo à habitação depois que a empresa valida a elegibilidade do cliente para um empréstimo.

**Problema**:
A empresa deseja automatizar o processo de elegibilidade do empréstimo (em tempo real) com base nos detalhes do cliente fornecidos durante o preenchimento do formulário de inscrição on-line. Esses detalhes são sexo, estado civil, escolaridade, número de dependentes, renda, valor do empréstimo, histórico de crédito e outros. Para automatizar esse processo, eles criaram um problema para identificar os segmentos de clientes elegíveis para valores de empréstimo para atingir esses clientes especificamente. Aqui eles forneceram um conjunto de dados parcial.

Para solucionar esse problema utilizou-se o MySQL no qual foram realizadas queries SQL com o objetivo de responder as perguntas de negócio especificadas a seguir.

**Perguntas de Negócio**

**1 - O montante do empréstimo varia em função do nível educacional do requerente?**

**Solução**:

```
SELECT Education, ROUND(AVG(Loan_Amount_Term),2) AS AVG_Loan FROM inputs.loan_sanction_train
GROUP BY Education
```

Resultado: 

![image](https://user-images.githubusercontent.com/69591172/215922001-305b8b24-3f1f-48ab-90ca-9342dbce1199.png)

Verifica-se que pessoas com graduação obtiveram maiores valores de empréstimos quando comparado com os valores concedidos às pessoas sem graduação.

**2 - O montante do empréstimo varia em função do gênero e estado civil?**

**Solução**:

```
SELECT Gender, Married, ROUND(AVG(LoanAmount),2) AS AVG_Loan FROM inputs.loan_sanction_train
WHERE Gender IN('Male','Female')
GROUP BY Gender, Married
```

Resultado: 

![image](https://user-images.githubusercontent.com/69591172/215921892-752c1e56-1647-4c6a-9c80-ae1288ed3671.png)

Nota-se que pessoas casadas receberam um crédito maior do que pessoas solteiras, além disso pode-se perceber também que, dentre os solteiros, as pessoas do sexo masculino obtiveram maiores valores de crédito concedidos.

**3 - Profissionais autônomos receberam maior ou menor montante de empréstimo?**

**Solução**:

```
SELECT Self_Employed, ROUND(AVG(LoanAmount),2) AS AVG_Loan FROM inputs.loan_sanction_train
WHERE Self_Employed IN('Yes','No')
GROUP BY Self_Employed
```

Resultado: 

![image](https://user-images.githubusercontent.com/69591172/215921827-9fd54763-36aa-417b-b3db-9e37ca1b6d99.png)

É possível ver que profissionais autônomos tiveram maior crédito.

**4 - Dentre os aplicantes casados, o montante do empréstimo é maior para aqueles com bom histórico de pagamento?**

**Solução**:

```
SELECT Credit_History, ROUND(AVG(LoanAmount),2) AS AVG_Loan FROM inputs.loan_sanction_train
WHERE Married = 'Yes'
GROUP BY Credit_History
```

Resultado: 

![image](https://user-images.githubusercontent.com/69591172/215922533-316a7090-033d-488c-a15d-ec2d5e8b6980.png)

Confirma-se que esse perfil de aplicante teve um maior valor de crédito concedido comparado aos maus pagadores.

**5 - Qual foi a renda média dentre os aplicantes solteiros e classificados como maus pagadores?**

**Solução**:

```
SELECT ROUND(AVG(ApplicantIncome),2) AS AVG_Applicant_Income FROM inputs.loan_sanction_train
WHERE Married = 'No' AND Credit_History = 0
```

Resultado: 

![image](https://user-images.githubusercontent.com/69591172/215926309-5ffb5413-b643-4222-b2aa-5f1571865034.png)
