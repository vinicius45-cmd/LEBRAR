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
