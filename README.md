PS C:\Users\01009683819\projeto_react> cd .\projeto_mapa_tematico\
PS C:\Users\01009683819\projeto_react\projeto_mapa_tematico> npm run dev

> projeto_mapa_tematico@0.0.0 dev
> vite

Port 5173 is in use, trying another one...

  VITE v7.3.1  ready in 451 ms      

  ➜  Local:   http://localhost:5174/
  ➜  Network: use --host to expose  
  ➜  press h + enter to show help   





















para estudo (GEMINI)

SELECT 
    t.nm_operadora,
    tl.cd_linha,
    COUNT(tv.id_viagem) AS total_viagens_dia
FROM 
    dados_mobilidade.tab_linha tl
JOIN 
    dados_mobilidade.tab_operadora_linha tol ON tl.id_linha = tol.id_linha
JOIN 
    dados_mobilidade.tab_operadora t ON tol.id_operadora = t.id_operadora
LEFT JOIN 
    dados_mobilidade.tab_viagem tv ON tl.id_linha = tv.id_linha
GROUP BY 
    t.nm_operadora, 
    tl.cd_linha
ORDER BY 
    total_viagens_dia DESC; -- Mostra primeiro as linhas mais frequentes









/**SELECT column_name, data_type 
FROM information_schema.columns 
WHERE table_name = 'tab_itinerario' AND column_name = 'id_linha';**/


/**SELECT column_name, data_type 
FROM information_schema.columns 
WHERE table_name = 'tab_itinerario';**/


/**SELECT 
    (SELECT ST_SRID(geom_parada) FROM dados_mobilidade.tab_parada LIMIT 1) as srid_parada,
    (SELECT ST_SRID(geo_regiao_administrativa) FROM bdf.tab_regioes_administrativas LIMIT 1) as srid_ra;**/



SELECT table_name 
FROM information_schema.tables 
WHERE table_schema = 'dados_mobilidade';












select ti.geo_linhas_lin,
    tl.cd_linha,
    ti.lin_sentido,
    ti.id_itinerario
FROM 
    dados_mobilidade.tab_itinerario ti
JOIN 
    dados_mobilidade.tab_linha tl
    ON ti.id_linha = tl.id_linha
WHERE 
    tl.cd_linha = '0.170'
ORDER BY 
    ti.lin_sentido;












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









-- exercício N
select ti.geo_linhas_lin,
    tl.cd_linha,
    ti.lin_sentido,
    ti.id_itinerario
FROM 
    dados_mobilidade.tab_itinerario ti
JOIN 
    dados_mobilidade.tab_linha tl
    ON ti.id_linha = tl.id_linha
WHERE 
    tl.cd_linha = '0.170'
ORDER BY 
    ti.lin_sentido;










-- exercício O
SELECT 
    tl.cd_linha, 
    tl.tx_linha 
FROM 
    dados_mobilidade.tab_linha tl
WHERE
    tl.tx_linha ilike '%Eixo Monumental%';









-- exercício P
SELECT 
    tl.cd_linha, 
    tl.tx_linha,
    (LENGTH(tx_linha) - LENGTH(REPLACE(tx_linha, '/', '')) + 1) AS total_trechos
FROM 
    dados_mobilidade.tab_linha tl
WHERE 
    tl.cd_linha = '0.111';









-- exercício Q

















-- exercício R
select
	tl.cd_linha,
	th.hr_prevista,
	th.domingo
from
	dados_mobilidade.tab_horario th
join 
	dados_mobilidade.tab_operadora_linha tol
	on th.id_operadora_linha = tol.id_operadora_linha
join
	dados_mobilidade.tab_linha tl
	on tol.id_linha = tl.id_linha
where
	tl.cd_linha = '0.763'
	
	
	
	
	
	
	
	

-- exercício S
select 
	count(th.sabado),
	t.nm_operadora
from 
	dados_mobilidade.tab_horario th
join 
    dados_mobilidade.tab_operadora_linha tol
	on tol.id_operadora_linha = th.id_operadora_linha
join
    dados_mobilidade.tab_operadora t
    on t.id_operadora = tol.id_operadora
where 
    th.sabado ilike 'S'
group by
    th.sabado,
    t.nm_operadora
	
	
	
	
	
	
	
	

    
    -- exercício T
   select
	tvr.linha,
	COUNT(tvr.viagem) as qtd
from 
	dados_mobilidade.tab_viagens_realizada tvr 
group by
	tvr.linha,
	tvr.viagem
order by qtd desc
limit 
	1
    
    
    
    
    
    
    
    
    
    
    
-- exercício U
select
	tl.cd_linha,
	max(th.tempo_percurso) as viagem_mais_longa
from
	dados_mobilidade.tab_horario th
join
	dados_mobilidade.tab_operadora_linha tol
	on tol.id_operadora_linha = th.id_operadora_linha
join
	dados_mobilidade.tab_linha tl
	on tl.id_linha =  tol.id_linha
group by
    tl.cd_linha
order by
	viagem_mais_longa desc
limit
	1;










-- exercício V
select
	tl.cd_linha,
	tl.tx_linha,
	th.hr_prevista
from 
    dados_mobilidade.tab_horario th
join 
    dados_mobilidade.tab_operadora_linha t
    on th.id_operadora_linha = t.id_operadora_linha 
join
	dados_mobilidade.tab_linha tl
	on t.id_linha = tl.id_linha
where
	th.hr_prevista between 0 and 4
group by
	tl.cd_linha,
	tl.tx_linha,
	th.hr_prevista
order by
    th.hr_prevista desc








Consultas Espaciais e Georeferenciamento (SQL/Postgis)



-- exercício B
select 
    p.id AS parada_id, 
    p.cod_dftrans, 
    i.lin_sentido,
    p.geom_parada
FROM 
    dados_mobilidade.tab_parada p
JOIN 
    dados_mobilidade.tab_itinerario i 
    ON ST_DWithin(p.geom_parada, i.geo_linhas_lin, 0.0005)
JOIN 
    dados_mobilidade.tab_linha l 
    ON i.id_linha = l.id_linha
WHERE 
    l.cd_linha = '0.763'
ORDER BY 
    i.lin_sentido, 
    ST_LineLocatePoint(i.geo_linhas_lin, p.geom_parada);











-- exercício C
WITH ra_preparada AS (
    SELECT 
        dsc_regiao_administrativa,
        ST_Transform(geo_regiao_administrativa, (SELECT ST_SRID(geom_parada) FROM dados_mobilidade.tab_parada LIMIT 1)) AS geom_ajustada
    FROM 
        bdf.tab_regioes_administrativas
)
SELECT 
    COALESCE(ra.dsc_regiao_administrativa, 'TOTAL GERAL') AS regiao_administrativa, 
    COUNT(p.id) AS total_paradas
FROM 
    ra_preparada ra
LEFT JOIN 
    dados_mobilidade.tab_parada p 
    ON ST_Intersects(p.geom_parada, ra.geom_ajustada)
GROUP BY 
    ROLLUP(ra.dsc_regiao_administrativa)
ORDER BY 
    total_paradas ASC;

                       OU
                       
WITH ra_preparada AS (
    SELECT 
        dsc_regiao_administrativa,
        ST_Transform(geo_regiao_administrativa, (SELECT ST_SRID(geom_parada) FROM dados_mobilidade.tab_parada LIMIT 1)) AS geom_ajustada
    FROM 
        bdf.tab_regioes_administrativas
)
SELECT 
    ra.dsc_regiao_administrativa AS regiao_administrativa, 
    COUNT(p.id) AS total_paradas
FROM 
    ra_preparada ra
LEFT JOIN 
    dados_mobilidade.tab_parada p 
    ON ST_Intersects(p.geom_parada, ra.geom_ajustada)
GROUP BY 
    ra.dsc_regiao_administrativa
ORDER BY 
    total_paradas DESC;
