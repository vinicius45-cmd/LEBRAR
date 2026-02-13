# LEBRAR
Lembrar de códigos que podem ser uteis no futuro
select
	tl.tx_linha,ti.geo_linhas_lin
from 
	tab_itinerario ti
join 
	tab_linha tl
  on ti.id_linha = tl.id_linha
where cd_linha = '0.305'

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


--exercício A
select
    tx_linha,
    cd_linha
from 
	dados_mobilidade.tab_linha




	
	
	
	
	
	
-- exxercício B
select
	tl.tx_linha,
	tl.id_linha, 
	ti.lin_extensao
from 
	dados_mobilidade.tab_linha tl 
join
    dados_mobilidade.tab_itinerario ti
 on ti.id_linha = tl.id_linha
where tl.cd_linha = '0.111'










-- exercício C
select 
	cd_linha, tx_linha
from 
    tab_linha li
join
    tab_itinerario ti 
  on ti.id_linha = li.id_linha
where 
	lin_extensao > 70
order by cd_linha, tx_linha DESC










-- D 
SELECT MIN (LIN_EXTENSAO)
FROM tab_itinerario ti










--exercício E
SELECT MAX (LIN_EXTENSAO)
FROM tab_itinerario ti










-- execício F
select AVG(lin_extensao)
from dados_mobilidade.tab_itinerario










-- exercício G
SELECT 
    COUNT(CASE WHEN lin_sentido ILIKE 'CIRCULAR' THEN 1 END) AS Total_Circular,
    COUNT(CASE WHEN lin_sentido ILIKE 'IDA' THEN 1 END) AS Total_Ida,
    COUNT(CASE WHEN lin_sentido ILIKE 'VOLTA' THEN 1 END) AS Total_Volta
FROM dados_mobilidade.tab_itinerario ti ;
                              --Ou
SELECT 
    COUNT(CASE WHEN tx_linha ILIKE '%Circular%' THEN 1 END) AS Total_Circular
FROM tab_linha;










-- exercício H
select 
	lin_extensao,lin_sentido
from 
    tab_itinerario ti
where ti.lin_sentido ilike 'CIRCULAR'
order by ti.lin_extensao desc
limit 1










-- exercício I
select
	tx_linha,vl_tarifa
from 
	dados_mobilidade.tab_linha
where vl_tarifa = 5.50







-- exercício J
select
    tl.cd_linha,
	tl.tx_linha,
    t.nm_operadora
from
    dados_mobilidade.tab_linha tl 
join 
	dados_mobilidade.tab_itinerario ti
   on ti.id_linha = tl.id_linha
join
	dados_mobilidade.tab_operadora_linha tol
	on tl.id_linha = tol.id_linha
join
	dados_mobilidade.tab_operadora t
	on tol.id_operadora = t.id_operadora
where t.nm_operadora like ('%PIRACICABANA%')









-- exercício K
SELECT
    AVG(ti.lin_extensao) AS media_geral_pioneira
FROM
    dados_mobilidade.tab_linha tl 
JOIN 
    dados_mobilidade.tab_itinerario ti
    ON ti.id_linha = tl.id_linha
JOIN
    dados_mobilidade.tab_operadora_linha tol
    ON tl.id_linha = tol.id_linha
JOIN
    dados_mobilidade.tab_operadora t
    ON tol.id_operadora = t.id_operadora
WHERE
    t.nm_operadora LIKE '%PIONEIRA%';










-- exercício I
SELECT 
    tx_linha
FROM 
    dados_mobilidade.tab_linha
WHERE 
    tx_linha ILIKE '%GAMA%';









-- exercício M
SELECT 
    tl.cd_linha, 
    tl.tx_linha, 
    COUNT(tol.id_operadora) AS qtd_operadoras
FROM 
    dados_mobilidade.tab_linha tl
JOIN 
    dados_mobilidade.tab_operadora_linha tol 
    ON tl.id_linha = tol.id_linha
GROUP BY 
    tl.cd_linha, 
    tl.tx_linha
HAVING 
    COUNT(tol.id_operadora) > 1;
