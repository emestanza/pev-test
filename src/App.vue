<template>
    <div id="app" class="d-flex">
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

    const query = `
SELECT *
FROM tenk1 t1, tenk2 t2
WHERE t1.unique1 < 10 AND t1.unique2 = t2.unique2;`;

    export default {
        name: "App",
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
