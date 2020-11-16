<template>
    <div class="d-flex">
        <pev2 :plan-source="plan" :plan-query="query"></pev2>
    </div>
</template>

<script>
    import pev2 from "pev2";

    const plan = `[
  {
    "Plan": {
      "Node Type": "Limit",
      "Parallel Aware": false,
      "Startup Cost": 839329.82,
      "Total Cost": 847140.33,
      "Plan Rows": 100,
      "Plan Width": 447,
      "Plans": [
        {
          "Node Type": "Hash Join",
          "Parent Relationship": "Outer",
          "Parallel Aware": false,
          "Join Type": "Left",
          "Startup Cost": 839329.82,
          "Total Cost": 864635.87,
          "Plan Rows": 324,
          "Plan Width": 447,
          "Inner Unique": false,
          "Hash Cond": "(allusglobal.id_categoria_tipo_documento = categoria_tipo_documento.id)",
          "Plans": [
            {
              "Node Type": "Nested Loop",
              "Parent Relationship": "Outer",
              "Parallel Aware": false,
              "Join Type": "Left",
              "Startup Cost": 838843.85,
              "Total Cost": 864145.45,
              "Plan Rows": 324,
              "Plan Width": 433,
              "Inner Unique": true,
              "Plans": [
                {
                  "Node Type": "Nested Loop",
                  "Parent Relationship": "Outer",
                  "Parallel Aware": false,
                  "Join Type": "Inner",
                  "Startup Cost": 838843.42,
                  "Total Cost": 862759.18,
                  "Plan Rows": 324,
                  "Plan Width": 410,
                  "Inner Unique": true,
                  "Plans": [
                    {
                      "Node Type": "Aggregate",
                      "Strategy": "Sorted",
                      "Partial Mode": "Simple",
                      "Parent Relationship": "Outer",
                      "Parallel Aware": false,
                      "Startup Cost": 838843.00,
                      "Total Cost": 838922.64,
                      "Plan Rows": 4528,
                      "Plan Width": 12,
                      "Group Key": ["documento_firma.iddoc"],
                      "Plans": [
                        {
                          "Node Type": "Sort",
                          "Parent Relationship": "Outer",
                          "Parallel Aware": false,
                          "Startup Cost": 838843.00,
                          "Total Cost": 838854.45,
                          "Plan Rows": 4581,
                          "Plan Width": 12,
                          "Sort Key": ["documento_firma.iddoc"],
                          "Plans": [
                            {
                              "Node Type": "Bitmap Heap Scan",
                              "Parent Relationship": "Outer",
                              "Parallel Aware": false,
                              "Relation Name": "documento_firma",
                              "Alias": "documento_firma",
                              "Startup Cost": 9833.32,
                              "Total Cost": 838564.44,
                              "Plan Rows": 4581,
                              "Plan Width": 12,
                              "Recheck Cond": "(idaplic = 375)",
                              "Filter": "((fecha >= '2020-05-01 00:00:00'::timestamp(6) without time zone) AND (fecha <= '2020-05-05 23:59:59'::timestamp(6) without time zone))",
                              "Plans": [
                                {
                                  "Node Type": "Bitmap Index Scan",
                                  "Parent Relationship": "Outer",
                                  "Parallel Aware": false,
                                  "Index Name": "inx_documento_firma_idaplic_iddoc",
                                  "Startup Cost": 0.00,
                                  "Total Cost": 9832.17,
                                  "Plan Rows": 532231,
                                  "Plan Width": 0,
                                  "Index Cond": "(idaplic = 375)"
                                }
                              ]
                            }
                          ]
                        }
                      ]
                    },
                    {
                      "Node Type": "Index Scan",
                      "Parent Relationship": "Inner",
                      "Parallel Aware": false,
                      "Scan Direction": "Forward",
                      "Index Name": "allusglobal_pkey",
                      "Relation Name": "allusglobal",
                      "Alias": "allusglobal",
                      "Startup Cost": 0.42,
                      "Total Cost": 5.25,
                      "Plan Rows": 1,
                      "Plan Width": 402,
                      "Index Cond": "(id = documento_firma.iddoc)",
                      "Filter": "((firmado = ANY ('{\\"FIRMADO CONFORME\\",\\"FIRMADO DISCONFORME\\"}'::text[])) AND (id_categoria_tipo_documento = ANY ('{970,971,972,973,974}'::integer[])))"
                    }
                  ]
                },
                {
                  "Node Type": "Index Scan",
                  "Parent Relationship": "Inner",
                  "Parallel Aware": false,
                  "Scan Direction": "Forward",
                  "Index Name": "inx_seg_usuario_cuil",
                  "Relation Name": "seg_usuario",
                  "Alias": "seg_usuario",
                  "Startup Cost": 0.42,
                  "Total Cost": 4.28,
                  "Plan Rows": 1,
                  "Plan Width": 34,
                  "Index Cond": "((cuil)::text = (allusglobal.cuil)::text)",
                  "Filter": "(idempresa = 150)"
                }
              ]
            },
            {
              "Node Type": "Hash",
              "Parent Relationship": "Inner",
              "Parallel Aware": false,
              "Startup Cost": 294.32,
              "Total Cost": 294.32,
              "Plan Rows": 15332,
              "Plan Width": 18,
              "Plans": [
                {
                  "Node Type": "Seq Scan",
                  "Parent Relationship": "Outer",
                  "Parallel Aware": false,
                  "Relation Name": "categoria_tipo_documento",
                  "Alias": "categoria_tipo_documento",
                  "Startup Cost": 0.00,
                  "Total Cost": 294.32,
                  "Plan Rows": 15332,
                  "Plan Width": 18
                }
              ]
            }
          ]
        }
      ]
    }
  }
]`;

    const query = `select

    allusglobal.id AS "id",
    allusglobal.cuil AS "cuil",
    allusglobal.tipo AS "tipo",
    allusglobal.periodo AS "periodo",
    allusglobal.sector AS "sector",
    allusglobal.locacion AS "locacion",
    allusglobal.firmado AS "firmado",
    allusglobal.archivo AS "archivo",
    allusglobal.idcarga AS "idcarga",
    allusglobal.idkofax AS "idkofax",
    allusglobal.md5 AS "md5",
    allusglobal.bandeja AS "bandeja",
    allusglobal.id_categoria_tipo_documento AS "id_categoria_tipo_documento",
    allusglobal.nombre AS "nombre",
    allusglobal.metadata AS "metadata",
    allusglobal.id_master_eforms AS "id_master_eforms",
    allusglobal.creation_date AS "creation_date",
    allusglobal.sign_date AS "sign_date",
    seg_usuario.nombre AS "usuario_nombre",
    seg_usuario.apellido AS "usuario_apellido",
    categoria_tipo_documento.nombre AS "tipo_nombre",
    documento_firma.fecha AS "fecha_firma"
FROM
    allusglobal
    LEFT JOIN seg_usuario ON (seg_usuario.cuil = allusglobal.cuil)
        AND ((seg_usuario.idempresa = '150'))
    LEFT JOIN categoria_tipo_documento ON (categoria_tipo_documento.id = allusglobal.id_categoria_tipo_documento)
    INNER JOIN (
        SELECT
    documento_firma.iddoc AS "iddoc",
    MAX(fecha) AS "fecha"
FROM
    documento_firma
WHERE ((documento_firma.fecha BETWEEN CAST('2020-05-01 00:00:00' as timestamp(6))
        AND CAST('2020-05-05 23:59:59' as timestamp(6))))
AND ((documento_firma.idaplic = 375))
GROUP BY documento_firma.iddoc

    \t
    )
    \t
    AS documento_firma ON (documento_firma.iddoc = allusglobal.id)
WHERE ((allusglobal.id_categoria_tipo_documento IN (970, 971, 972, 973, 974))
    AND (allusglobal.firmado IN ('FIRMADO CONFORME', 'FIRMADO DISCONFORME')))
LIMIT 100 OFFSET 0;`;

    export default {
        data: function() {
            return {
                plan: plan,
                query: query
            };
        },
        components: {
            pev2
        }
    };
</script>

<style lang="scss">
    html,
    body,
    #app {
        height: 100%;
    }
</style>
