SELECT
  SUBSTRING(CAST(d.Fecha_proceso AS STRING),3,4) AS periodo,
  v.cod_subsegmento,
  CASE WHEN v.ciclo_curse='0' THEN 'GA'
       WHEN v.ciclo_curse IN ('1','2','3') THEN 'CIRR'
       WHEN v.ciclo_curse IS NOT NULL THEN 'CVEN'
       ELSE 'SIN CLASIFICAR' END AS campana,
  'Cartera Total' AS apertura,
  SUM(v.deuda_total) AS monto
FROM practicas.practica_smartcredi.dad_prueba d
INNER JOIN practicas.practica_smartcredi.venta_prueba v
  ON d.id_numero_operac = v.operacion
WHERE d.id_concepto='COLOC'
  AND d.ESTADO_DE_DEUDA NOT IN ('3','5')
  AND SUBSTRING(CAST(d.CTA_ACTUAL AS STRING),1,4) NOT IN ('9600','1740','1735','1725','1710','1705','1120','1215','1695','1690','1820','9880','9899','1706','1730','9601','9602')
  AND d.IND_CTAS_ORDEN = 0
  AND v.cartera_sbif='CONSUMO'
  AND v.cod_subsegmento IN (...lista...)
GROUP BY 1,2,3
