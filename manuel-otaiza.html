
-- ============================================================
-- Grano: PERIODO (camada de origen) x SEGMENTO x CAMPANA x CON_OFERTA x OFERTA x CLUSTER
--
-- % ATRASO POR CAMADA — SNAPSHOT ÚNICO (cada camada vs. el DDAS más reciente):
--   - La "camada" de una operación = el PRIMER periodo en que aparece en
--     t_pcr_venta_reestructurada (MIN(periodo) por operacion). Si esa tabla
--     es un snapshot recurrente (la misma operación reaparece mes a mes
--     mientras esté vigente/reestructurada), esto evita que una misma
--     operación quede contada en varias camadas a la vez.
--     -> AJUSTAR si en tu tabla cada fila ya es un evento único de venta.
--   - Todas las camadas se evalúan SIEMPRE contra el DDAS del período MÁS
--     RECIENTE disponible (no contra el DDAS de su propio mes de origen).
--   - El corte de madurez (FEC_1ER_VEC) también es FIJO: primer día del mes
--     siguiente al período más reciente (no depende de la camada).
--   - El denominador NO lleva filtro de madurez (deuda total vigente de la
--     camada, hoy).
-- ============================================================

CREATE OR REPLACE TABLE practicas.practica_smartcredi.consumo_atraso_camada AS

WITH max_per AS (
  SELECT SUBSTRING(CAST(MAX(ddas_fec_proc) AS STRING), 3, 4) AS mp
  FROM ddas
),

venta_ops AS (
  SELECT periodo, operacion, segmento, campana, con_oferta, oferta, cluster_desafiante
  FROM (
    SELECT
      periodo,
      operacion,
      CASE
        WHEN cod_subsegmento IN ('151','152','155','160','161','170','171','901','902','903','904','905','906','907','908',
                                  '909','959','961') THEN 'Classic'
        WHEN cod_subsegmento IN ('301','302','305','310','320','330','501','505','506') THEN 'Alto valor'
        WHEN cod_subsegmento IN ('510','515','516','601','610','620','630','650') THEN 'Select'
        WHEN cod_subsegmento IN ('811','812','813','814','815','816','942') THEN 'Negocios'
        WHEN cod_subsegmento IN ('821','822','825','826','829','830','833','834','835','836','837','838','940','941') THEN 'Pyme 1'
        WHEN cod_subsegmento IN ('801','823','827','831') THEN 'Pyme 2'
      END AS segmento,
      CASE
        WHEN ciclo_curse = '0' THEN 'GESTION ANTICIPATIVA'
        WHEN ciclo_curse IN ('1','2','3') THEN 'CARTERA IRREGULAR'
        WHEN ciclo_curse IS NOT NULL THEN 'CARTERA VENCIDA'
      END AS campana,
      CASE WHEN ind_oferta_pa IS NOT NULL THEN 'SI' ELSE 'NO' END AS con_oferta,
      COALESCE(NULLIF(cluster_desafiante, 'NULL'), 'Sin clasificar') AS cluster_desafiante,
      COALESCE(NULLIF(oferta_propuesta, 'NULL'), 'Sin Oferta') AS oferta,
      -- camada = PRIMER periodo en que aparece la operación
      ROW_NUMBER() OVER (
        PARTITION BY operacion,
          CASE WHEN ind_oferta_pa IS NOT NULL THEN 'SI' ELSE 'NO' END
        ORDER BY periodo ASC
      ) AS rn
    FROM pro_business.portfcollecrecovexp.t_pcr_venta_reestructurada
    WHERE cartera_sbif = 'CONSUMO'
      AND cod_subsegmento IN (
        '151','152','155','160','161','170','171','901','902','903','904','905','906','907','908','909','959','961',
        '301','302','305','310','320','330','501','505','506',
        '510','515','516','601','610','620','630','650',
        '811','812','813','814','815','816','942',
        '821','822','825','826','829','830','833','834','835','836','837','838','940','941',
        '801','823','827','831'
      )
      AND periodo >= '2501'
  ) sub
  WHERE rn = 1
),

atraso_raw AS (
  SELECT
    v.periodo AS PERIODO,             -- camada de origen (dimensión fija)
    v.segmento AS SEGMENTO,
    v.campana AS CAMPANA,
    v.con_oferta AS CON_OFERTA,
    v.oferta AS OFERTA,
    v.cluster_desafiante AS CLUSTER_DESAFIANTE,
    SUM(
      CASE
        WHEN d.ddas_atraso_en_dias > 0
         -- corte de madurez FIJO: 1er día del mes siguiente al último periodo disponible
         AND d.ddas_FEC_1ER_VEC < CAST(DATE_FORMAT(ADD_MONTHS(TO_DATE(CONCAT('20', mp.mp, '01'), 'yyyyMMdd'), 1), 'yyyyMMdd') AS INT)
        THEN d.deuda_total ELSE 0
      END
    ) / 1000000.0 AS CARTERA_MOROSA_MM,
    SUM(d.deuda_total) / 1000000.0 AS CARTERA_VIGENTE_MM
  FROM ddas d
  CROSS JOIN max_per mp
  INNER JOIN venta_ops v
    ON d.ddas_id_numero_operac = v.operacion
   AND SUBSTRING(CAST(d.ddas_fec_proc AS STRING), 3, 4) = mp.mp   -- SIEMPRE el DDAS más reciente, sin importar la camada
  WHERE d.ddas_id_concepto = 'COLOC'
    AND d.ddas_ESTADO_DE_DEUDA NOT IN ('3','5')
    AND SUBSTRING(CAST(d.ddas_CTA_ACTUAL AS STRING), 1, 4) NOT IN
        ('9600','1740','1735','1725','1710','1705','1120','1215','1695','1690','1820','9880','9899','1706','1730','9601','9602')
    AND d.ddas_IND_CTAS_ORDEN = 0
  GROUP BY 1, 2, 3, 4, 5, 6
  HAVING SEGMENTO IS NOT NULL AND CAMPANA IS NOT NULL
)

SELECT
  PERIODO,
  SEGMENTO,
  CAMPANA,
  CON_OFERTA,
  OFERTA,
  CLUSTER_DESAFIANTE,
  SUM(CARTERA_MOROSA_MM) AS CARTERA_MOROSA_MM,
  SUM(CARTERA_VIGENTE_MM) AS CARTERA_VIGENTE_MM
FROM atraso_raw
GROUP BY 1, 2, 3, 4, 5, 6
ORDER BY PERIODO, SEGMENTO, CAMPANA, CON_OFERTA, OFERTA, CLUSTER_DESAFIANTE
