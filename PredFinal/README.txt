Problema #12 - Estabilidad del modelo frente al Undersampling
David Nicolas Torres Marin

Entrega final - competencia Kaggle utn-2026-virtual-mgr


CONTENIDO DE LA CARPETA

1. z719_David_S119993_exp7301.ipynb
   Corrida completa del workflow gerencial (FE intra-mes, algoritmo genetico,
   FE historico, undersampling al 10%, grid search, entrenamiento final,
   scoring) con semilla 119993. Experimento 7301.

2. z719_David_S299993_exp7302.ipynb
   Misma corrida, semilla 299993. Experimento 7302.

3. z719_ensemble_David_2semillas.ipynb
   Toma el prediccion.txt de las dos corridas anteriores, promedia la
   probabilidad por numero_de_cliente, y genera los cortes que se subieron
   a Kaggle (400 a 1300, de a 50). El archivo finalmente seleccionado en
   Kaggle sale de este ensemble, corte 750.


COMO CORRERLO 

Paso 1: correr z719_David_S119993_exp7301.ipynb completo (Run All).
        Genera la carpeta WF7301 con el modelo, el grid search y el
        prediccion.txt de esa semilla.

Paso 2: correr z719_David_S299993_exp7302.ipynb completo.
        Genera WF7302 de la misma forma, con la otra semilla.

Paso 3: correr z719_ensemble_David_2semillas.ipynb.
        Lee WF7301 y WF7302, promedia las probabilidades, y genera los
        CSV de cada corte en WF_ENSEMBLE_7301_7302/kaggle/.

        La ultima celda tiene un interruptor:

           submit_kaggle <- FALSE

        En FALSE solo genera los CSV, no sube nada. Para reproducir el
        submit real hay que pasarlo a TRUE y correr unicamente esa celda
        (no hace falta repetir los pasos 1 y 2).


DECISIONES APLICADAS EN EL WORKFLOW

- Undersampling (Problema #12, propio): training_pct = 0.10. Se conservan
  siempre los positivos (BAJA+1, BAJA+2); se reduce solo CONTINUA.

- FE intra-mes (Problema #03, recomendacion Grupo B): variables
  estandarizadas (Z-Score) sobre las top10 por importancia, flags de
  variables de alto riesgo, y ratios cruzados entre las variables
  estandarizadas.

- Algoritmo genetico (Problema #10, recomendacion Grupo A): gramEvol
  sobre las variables candidatas, generando hasta 20 features nuevas
  (top_features), con elitismo de 8 individuos y mutationChance 0.20,
  segun los parametros documentados por ese grupo.

- FE historico (Problema #05, recomendacion Grupo B): lag1, lag2, lag3,
  delta1, delta2, delta3 y media movil de 3 meses (ma3) sobre todas las
  variables.

- Data Drifting (Problema #02): no se implementa. El profesor indico en
  el canal de la materia que, mas alla de las recomendaciones de los
  grupos, convenia dejar el metodo en "ninguno".

- Reduccion de dimensionalidad con canaritos (Problema #06): no se
