CASE
    WHEN (id_producto_alt IN ('50','53','54','59') AND producto_sbif IN ('270','280','320','290','310','210'))
        THEN 'Hip+FG'

    WHEN (id_producto_alt IN ('10','20','52') AND producto_sbif IN ('140'))
        OR (id_producto_alt = '65' AND id_subprod_alt IN ('6587','6589','3550','6545','6547','6554','6555','6558','6613','6616','6664','6501','6568','6680','6690'))
        OR (id_producto_alt IN ('77','80') AND producto_sbif IN ('130'))
        OR (id_producto_alt IN ('0','51','70','85','86') AND producto_sbif IN ('140','342'))
        THEN 'Consumo'

    WHEN (id_producto_alt IN ('10','20','52') AND producto_sbif IN ('120'))
        OR (id_producto_alt = '42' AND id_subprod_alt IN ('4794','4796','4797','4830','4833','4834','4835','4839','4840','4976','4182','4185','4325','4447','4449','4462','4463','4465','4470','4480','4483','4485','4491','4522','4527','4530','4542','4607','4904','4906','4934','4936','4948','4201','4204','4206','4209','4211','4244','4258','4277','4280','4281','4291','4292','4294','4523','4538','4559','4626','4643','4763'))
        OR (id_producto_alt IN ('77','80') AND producto_sbif IN ('210'))
        OR (id_producto_alt IN ('0','31','32','33','36','44','51','55','81','85','86') AND producto_sbif IN ('120','160','170','180','210','240','250','340','350','360'))
        THEN 'Comercial'

    ELSE 'Sin Clasificar'
END AS macro_categoria
