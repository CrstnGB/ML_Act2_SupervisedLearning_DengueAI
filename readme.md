# PRÁCTICA 2: APRENDIZAJE SUPERVISADO (DengAI)

Esta práctica tiene como objetivo final la consecución de la mejor puntuación posible evaluada con la métrica *MAE (Mean Absolute Error)* sobre la predicción de la cantidad de casos afectados por el virus del Dengue. Es requisito casi indispensable obtener una métrica *mae < 28*. Este problema es parte de una competición organizada por [DrivenData](https://www.drivendata.org/competitions/44/dengai-predicting-disease-spread/page/82/) llamada *DengAI*.

Para conseguirlo, tras un primer proceso de exploración y clusterización de la Actividad 1 donde aún no se estaba teniendo en cuenta a la variable objetivo `total_cases`, ahora se realizará una reexploración teniendo en cuenta dicha variable. Se creará un pipeline de transformaciones del dataset basado en la Actividad 1 para que este documento sea completamente autocontenido, teniendo así el dataset resultante de dichas exploraciones y clusterizaciones anteriores.

A partir de este punto, se realizarán exploraciones univariable de `total_cases` y bivariable comprando este atributo con el resto. Además, se visualizará cómo varía a lo largo de los años con una visualización temporal.

Tras esta fase, se continuará con una exploración de posibles modelos en su estado por defecto que, según el tipo de predicción, se argumenta que son adecuados para su uso en la predicción. En esta exploración preliminar se decidirá cuáles son los más aptos para seguir con su desarrollo. Para dicha evaluación se utilizará la validación cruzada (*cross validation*) en lugar de dividir el dataset simplemente en entrenamiento y validación siendo la métrica a evaluar, como se ha comentado, el *mae*.

Además, se ha experimentado combinando modelos distintos y entrenándolos con el dataset dividido según la ciudad, **sj** e **iq** debido a una clara distinción en cuanto al número de casos que se visualiza en la fase de reexploración.

Por último, se optimizarán los parámetros de aquellos que obtuvieron puntuaciones por defecto del *mae < 28* intentando conseguir el mejor modelo posible para la predicción del dataset de *test*. Esta predicción se enviará a *DrivenData* para la obtención de la métrica final.

El mejor resultado final obtenido **entrenando sin split por alguna característica** ha sido un *mae = 26.6442* con el modelo [*LGBMRegressor*](https://lightgbm.readthedocs.io/en/latest/index.html), un framework de *gradient boosting* que utiliza algoritmos de aprendizaje basado en árboles.

Sin embargo, tras realizar el experimento de distintos modelos **entrenándolos con split según ciudades** se ha obtenido un *mae = 25.9327*. Esto ha sido gracias al entrenamiento por separado, curiosamente, mediante la misma clase de modelo: *KNeighborsRegressor*.

Como curiosidad, mientras se hacían experimentaciones incontroladas, se logró alcanzar un *mae = 25.9303* con [*RandomForestRegressor*](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestRegressor.html). Sin embargo, al no haber tenido fijada la semilla en su ejecución, por desgracia, no se ha conseguido replicar el experimento.