
 %sql
-- VENTA: aporte al total por campaña — Consumo
SELECT
  CASE WHEN ciclo_curse = '0' THEN 'GESTION ANTICIPATIVA'
       WHEN ciclo_curse IN ('1','2','3') THEN 'CARTERA IRREGULAR'
       WHEN ciclo_curse IS NOT NULL THEN 'CARTERA VENCIDA'
       ELSE 'SIN CLASIFICAR' END AS CAMPANA,
  SUM(deuda_total)/1000000 AS VENTA_MM,
  SUM(SUM(deuda_total)) OVER ()/1000000 AS TOTAL_MM,
  ROUND(100.0 * SUM(deuda_total)
        / SUM(SUM(deuda_total)) OVER (), 1) AS APORTE_VENTA_PCT
FROM practicas.practica_smartcredi.venta_prueba
WHERE cartera_sbif = 'CONSUMO'
  AND periodo = '2607'
  AND cod_subsegmento IN
   ('151','152','155','160','161','170','171','901','902','903','904','905','906','907','908','909','959','961',
    '301','302','305','310','320','330','501','505','506',
    '510','515','516','601','610','620','630','650',
    '811','812','813','814','815','816','942',
    '821','822','825','826','829','830','833','834','835','836','837','838','940','941',
    '801','823','827','831')
GROUP BY 1
ORDER BY 1
