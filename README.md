
%sql
-- GESTION ANTICIPATIVA — Oferta prom., Venta prom. y Efectividad por mes
WITH oferta AS (
  SELECT PERIODO AS periodo,
         SUM(MONTO_OFERTA) AS oferta_suma,
         ROUND(AVG(MONTO_OFERTA)/1000000, 2) AS OFERTA_PROMEDIO_MM,
         COUNT(*) AS N_OFERTAS
  FROM practicas.practica_smartcredi.oferta_prueba
  WHERE TIPO_OFERTA = 'CONSUMO'
    AND CICLO_OFERTA = 0
    AND PERIODO >= '2501'
  GROUP BY PERIODO
),
venta AS (
  SELECT periodo,
         SUM(CASE WHEN ind_oferta_pa IS NOT NULL
                  THEN deuda_total ELSE 0 END) AS venta_con_oferta_suma,
         ROUND(AVG(deuda_total)/1000000, 2) AS VENTA_PROMEDIO_MM,
         COUNT(*) AS N_VENTAS
  FROM practicas.practica_smartcredi.venta_prueba
  WHERE cartera_sbif = 'CONSUMO'
    AND ciclo_curse = '0'
    AND periodo >= '2501'
    AND cod_subsegmento IN
     ('151','152','155','160','161','170','171','901','902','903','904','905','906','907','908','909','959','961',
      '301','302','305','310','320','330','501','505','506',
      '510','515','516','601','610','620','630','650',
      '811','812','813','814','815','816','942',
      '821','822','825','826','829','830','833','834','835','836','837','838','940','941',
      '801','823','827','831')
  GROUP BY periodo
)
SELECT
  COALESCE(o.periodo, v.periodo) AS PERIODO,
  o.OFERTA_PROMEDIO_MM,
  o.N_OFERTAS,
  v.VENTA_PROMEDIO_MM,
  v.N_VENTAS,
  ROUND(100.0 * v.venta_con_oferta_suma / o.oferta_suma, 1) AS EFECTIVIDAD_PCT
FROM oferta o
FULL OUTER JOIN venta v ON o.periodo = v.periodo
ORDER BY PERIODO
