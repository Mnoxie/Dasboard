
%sql
-- % ATRASO por campaña — Consumo
WITH base AS (
  SELECT
    CASE WHEN ciclo_curse = '0' THEN 'GESTION ANTICIPATIVA'
         WHEN ciclo_curse IN ('1','2','3') THEN 'CARTERA IRREGULAR'
         WHEN ciclo_curse IS NOT NULL THEN 'CARTERA VENCIDA'
         ELSE 'SIN CLASIFICAR' END AS CAMPANA,
    deuda_total,
    atraso_en_dias
  FROM paso_con_ciclo
)
SELECT
  COALESCE(CAMPANA, 'TOTAL CONSUMO') AS CAMPANA,
  SUM(CASE WHEN atraso_en_dias > 0 THEN deuda_total ELSE 0 END)/1000000 AS MOROSA_MM,
  SUM(deuda_total)/1000000 AS VIGENTE_MM,
  ROUND(100.0 * SUM(CASE WHEN atraso_en_dias > 0 THEN deuda_total ELSE 0 END)
        / SUM(deuda_total), 1) AS PCT_ATRASO
FROM base
GROUP BY ROLLUP(CAMPANA)
ORDER BY CAMPANA
