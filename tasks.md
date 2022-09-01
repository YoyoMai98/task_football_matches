# Football Matches - Tasks

Each of the questions/tasks below can be answered using a `SELECT` query. When you find a solution copy it into the code block under the question before pushing your solution to GitHub.

1) Find all the matches from 2017.

```sql
<!-- Copy solution here -->
SELECT * FROM public.matches WHERE season == 2007;

```

2) Find all the matches featuring Barcelona.

```sql
<!-- Copy solution here -->
SELECT * FROM public.matches WHERE hometeam = 'Barcelona' OR awayteam = 'Barcelona';

```

3) What are the names of the Scottish divisions included?

```sql
<!-- Copy solution here -->
SELECT name FROM public.divisions WHERE country = 'Scotland';

```

4) Find the division code for the Bundesliga. Use that code to find out how many matches Freiburg have played in the Bundesliga since the data started being collected.

```sql
<!-- Copy solution here -->
SELECT * FROM public.divisions WHERE name = 'Bundesliga';
SELECT COUNT(*) FROM public.matches
WHERE division_code = 'D1'
AND hometeam = 'Freiburg'
OR awayteam = 'Freiburg';
```

5) Find the unique names of the teams which include the word "City" in their name (as entered in the database)

```sql
<!-- Copy solution here -->
SELECT DISTINCT team FROM(
SELECT DISTINCT hometeam as team FROM public.matches WHERE hometeam LIKE '%City%'
UNION
SELECT DISTINCT awayteam FROM public.matches WHERE awayteam LIKE '%City%'
) as uniqueTeam;
```

6) How many different teams have played in matches recorded in a French division?

```sql
<!-- Copy solution here -->
SELECT code FROM public.divisions WHERE country = 'France';
SELECT COUNT(DISTINCT team) FROM(
SELECT DISTINCT hometeam as team FROM public.matches WHERE division_code = 'F1'
UNION
SELECT DISTINCT awayteam FROM public.matches WHERE division_code = 'F1'
) as uniqueTeam;
```

7) Have Huddersfield played Swansea in the period covered?

```sql
<!-- Copy solution here -->
SELECT CASE WHEN EXISTS(
SELECT * FROM public.matches
WHERE (hometeam = 'Swansea' AND awayteam = 'Huddersfield')
OR (hometeam = 'Huddersfield' AND awayteam = 'Swansea')
)
THEN CAST(1 AS BIT)
ELSE CAST(0 AS BIT) END;
```

8) How many draws were there in the Eredivisie between 2010 and 2015?

```sql
<!-- Copy solution here -->
SELECT * FROM public.divisions WHERE name = 'Eredivisie';
SELECT COUNT(*) FROM public.matches
WHERE season >= 2010 AND season <= 2015
AND division_code = 'N1'
AND ftr = 'D'
```

9) Select the matches played in the Premier League in order of total goals scored from highest to lowest. Where there is a tie the match with more home goals should come first.

```sql
<!-- Copy solution here -->
SELECT * FROM public.divisions WHERE name = 'Premier League';

```

10) In which division and which season were the most goals scored?

```sql
<!-- Copy solution here -->


```

### Useful Resources

- [Filtering results](https://www.w3schools.com/sql/sql_where.asp)
- [Ordering results](https://www.w3schools.com/sql/sql_orderby.asp)
- [Grouping results](https://www.w3schools.com/sql/sql_groupby.asp)