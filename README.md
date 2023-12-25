# Data Science Independent Project #4 – Home Value Trends

## Descrição
Uma empresa solicita que você os ajude a tomar decisões mais informadas sobre investimentos imobiliários. Comece analisando os dados sobre os valores médios estimados de residências unifamiliares por CEP das últimas duas décadas.

Utilizei o SQLite e o DB Browser for SQLite para manupilação e consulta do banco de dados.

E agora irei responder as perguntas:

<br>

**- Quantos CEPs distintos existem neste conjunto de dados?**

```sql
select count( DISTINCT zip_code) as unique_zip_code
from home_value_data;
```

<br>
<br>

**- Quantos CEPs existem em cada estado?**

```sql
select state, count( DISTINCT zip_code) as unique_zip_code
from home_value_data
group by state;
```

<br>
<br>

**- Que intervalo de anos está representado nos dados?**


```sql
select DISTINCT substr(date, 1, 4) as year
from home_value_data
order by year asc;
```

R: De 1996 a 2018

<br>
<br>

**- Usando os dados disponíveis do mês mais recente, qual é a faixa de valores estimados de residências em todo o país?**

```sql
select round(avg(value)) as avg_value
from home_value_data
where substr(date, 1, 4) = '2018' and substr(date, 6, 2) = '11';
```

<br>
<br>

**- Usando os dados disponíveis do mês mais recente, quais estados têm os valores médios de residências mais altos? Que tal o mais baixo?**

```sql
select state, max(value) as max_value, date, substr(date, 6, 2) as month , substr(date, 1, 4) as year
from home_value_data
where year like '2018%' and month like '%11'
group by state
order by max_value desc;
```

```sql
select state, min(value) as min_value, date, substr(date, 6, 2) as month , substr(date, 1, 4) as year
from home_value_data
where year like '2018%' and month like '%11'
group by state
order by min_value asc;
```

<br>
<br>

**- Quais estados têm os valores médios residenciais mais altos/mais baixos para o ano de 2017? E para o ano de 2007? 1997?**

```sql
select state, max(value) as max_value, date, substr(date, 6, 2) as month , substr(date, 1, 4) as year
from home_value_data
where year like '2017%'
group by state
order by max_value desc;
```

```sql
select state, min(value) as min_value, date, substr(date, 6, 2) as month , substr(date, 1, 4) as year
from home_value_data
where year like '2017%'
group by state
order by min_value asc;
```

```sql
select state, max(value) as max_value, date, substr(date, 6, 2) as month , substr(date, 1, 4) as year
from home_value_data
where year like '2007%'
group by state
order by max_value desc;
```

```sql
select state, min(value) as min_value, date, substr(date, 6, 2) as month , substr(date, 1, 4) as year
from home_value_data
where year like '2007%'
group by state
order by min_value asc;
```

```sql
select state, max(value) as max_value, date, substr(date, 6, 2) as month , substr(date, 1, 4) as year
from home_value_data
where year like '1997%'
group by state
order by max_value desc;
```

```sql
select state, min(value) as min_value, date, substr(date, 6, 2) as month , substr(date, 1, 4) as year
from home_value_data
where year like '1997%'
group by state, date, month, year
having min(value) != 'null'
order by min_value asc;
```


## Considerações finais
Pude praticar mais as funções agregadas e aprendi um pouco mais sobre o comando HAVING para filtrar melhor os resultados.

Segue o link do projeto (em inglês) e do curso que estou fazendo, caso queiram dar uma olhada:

https://discuss.codecademy.com/t/data-science-independent-project-4-home-value-trends/419948

https://www.codecademy.com/career-journey/data-scientist-aly