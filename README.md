# Blog IIC3633 de Catalina Sarmiento
Blog para el curso Sistemas Recomendadores

![Imagen importante](https://vignette.wikia.nocookie.net/fallout/images/f/f0/Fo4-pebbles-artwork.png/revision/latest?cb=20151215234614 "Imagen importante")

## Posts

<dl>
  <dt>[03-09-2019] Performance of Recommender Algorithms on Top-N Recommendation Tasks</dt>
  <dd><em>Resumen: </em> This paper goes trough a revision of collaborative filtering methods for recommender systems. It highlights the importance of personalization over fixed recommendations based on the entirety of the user set, due to the risk of causing boredom in people.</dd> 
  <dd>For neighbourhood models such as KNN, this paper also shows a new similarity metric, which is a percentage of any other similarity coefficient that is scaled down by a "shrinkage coefficient". Its purpose is to account for credibility all over the training set, due to poor measurements of users' preferences. There is also an adjustement made to account for inherent preference in a certain kind of item across the dataset, which can be described as a residual rating based on bias.</dd>
  <dd>In the case of NNCosNgbr, the author explains how it bases its recommendations solely on user preference, without any input from similar users or the entire user base.</dd>
  <dd>Apart from what I described before, this paper compares other classical recommender systems using precision and recall. These metrics are reported for different dimensionalities of the selected training set.All the training sets come from a bigger one, and there are two of those. Namely, Netflix Prize and Movielens datasets.</dd>
  <dd>In general, the theory of precision/recall tradeoff is empirically shown to work in a graph of precision vs recall for each dataset. The recommender system which tended to yield the best results was PureSVD, or Matricial Factorization only. Overall, tests run on the Movielens dataset had better precision.</dd>
  <dd>In general, Top-N recommender systems typically overcome problems regarding as high proportion of datasets containing a single type of popular item. They can take an unpopular item for recommendation to a single usar. These systems still lack the ability of recommending relevant items to cold start users, but they are robust in all other cases.</dd>
</dl>

<dl>
  <dt>[27-08-2019] Collaborative Filtering for Implicit Feedback Datasets</dt>
  <dd><em>Implicit feedback: </em>Consiste en tomar recomendaciones del usuario cuando no las ha dado explícitamente. Esto significa que el usuario nunca hace el rating del contenido, sino que más bien da pistas de lo que le gusta por medio de un solo feedback positivo. Ahora bien, este método es inherentemente ruidoso, y no puede soportar el feedback negativo. Es ruidoso porque esto no se trata de cómo el usuario dará una preferencia, si no de cuánto puede congiar el modelo en expresiones de gusto aisladas. El modelo no puede saber el grado de preferencia específica, pero sí puede ver que el usuario da una misma pista positiva hacia un ítem de contenido e forma constante. Esto puede ser usado para expresar la confianza del modelo sobre cierta preferencia de forma numérica.</dd>
  <dd>Este método requere tomar en cuenta aspectos adicionales a lo anterior. Por ejemplo, una persona no puede dar una preferencia a dos ítems al mismo tiempo. Esto hace que no se puedan comparar dos piezas de contenido similares por una confianza sobre el usuario respecto a cada una.</dd>
  <dd><em>El modelo de implicit feedback: </em>La confianza de la que se habla en implicit feedback se puede expresar como el análisis de un conjunto de variables binarias, cada una de las cuales representa la existencia de una reacción positiva. En el caso de Facebook por ejemplo, sería un 'like'. En otras plataformas serían un 'corazón'.</dd>
  <dd>La función de costo en implicit feedback se calcula respecto a la probabilidad de observarlo, dada por el producto punto entre sets de usuarios y de ítems, tomando como coeficiente de escalamiento entre esta estimación y el rating observado a la confianza (frecuencia de los likes). También incluye el término de regularización con su propio coeficiente y distancia euclidiana al cuadrado.entre todos los usuarios e ítems.</dd>
  <dd>La confianza en sí se calcula como las observaciones de likes escaladas por un coeficiente que en su mejor test resultó ser 40, con valor mínimo uno. Mientras menos se agregue por parte de rating, más se acerca a uno.</dd>
  <dd>El algoritmo se escala con un factor exponencial para disminuir un efecto llamado 'de momento', en que una interacción s hace accidentalmente debido a razones misceláneas como dejar el sistema recomendador decidiendo sobre 'likes' del tipo continuo. Ejemplo, contar tiempo de interacción con un vídeo o sitio web es susceptible a ruido porque los usuarios pueden haberse alejado del dispositivo que utilizan para interactuar y haberlo dejado andando. Por otro lado, los resultados dados se pueden post procesar evaluándolos por similaridad entre preferencias empíricas con distancia de cosenos. Esto elimina un escalamiento en las preferencias al evaluarlas con su ángulo en el espacio de características dentro del que se ubican matricialmente.</dd>
  <dd>Los resultados se evalúan con un ranking que ubica en 0% las recomendaciones deseables. Los mayores rankings tienden a pertenecer al método que no se puede hacer tender hacia los ítems más populares. Implicit feedback cumple con esto, pues tiene que sacar sus predicciones exclusivamente desde el usuario. Por esto puede sugerir elementos que no muchos otros usuarios han consumido, pero que este usuario amaría.</dd>
  <dd>El implicit feedback logra adquirir el bias de cada usuario, se escala con la cantidad de reacciones del usuario, y saca provecho de los factores latentes de una forma que las factorizaciones matriciales explícitas no pueden. Se podría extender más alládel ranking en la etapa de evaluación al intentar adaptar los datos de confianza a ratings, y esto a su vez utilizarlo en un modelo de factorización matricial o una red neuronal. La idea de volverlo un problema explícito desde datos implícitos es atractiva porque mantendría su espacio latente y la complejidad computacional de explicit feedback ha disminuído con los años. Un caso donde sería interesante aplicar este concepto sería el sistema recomendador de Facebook, el cual es content-based. Esto requeriría una transformación adicional del usuario al contenido, y para esto el problema debería extenderse a adaptar el implicit feedback al nuevo contexto por medio de una representación adimensional, o un escalamiento respecto a vectores de ítems que pueden haberse calculado de forma implícita.
  En resumen, sería resumir el modelo implícito a un vector, como descriptor de la persona, que iría en un modelo explícito con la dimensionalidad adecuada (ejemplo, 2D).</dd>
  </dl>
<dl>
  <dt>[26-08-2019] Scalable collaborative filtering approaches for large recommender systems</dt>
   <dd>Este paper explora distintos sistemas recomendadores basados en contenido, en usuario y en modelo. Expone las distintas ventajas y desventajas de cada uno, evaluándolos en tres datasets: El dataset del Premio Netflix, el de MovieLens y el de Jester. Se enfoca principalmente en Collaborative Filtering y en técnicas de factorización matricial. Los datos son principalmente reportados en resultados de RMSE, MAE y SSE.</dd>
  <dd><em>RISMF: </em> Es un método de factorización matricial basado en los principios básicos de factorizar una matriz en dos otras utilizando descenso de gradiente. Son una matriz cuadrada y otra rectangular para pasar a la dimensionalidad original. Presenta el uso de regularización para penalizar ciertos coeficientes utilizados como pesos para el problema de optimización planteado por SSE. De esta forma, se introduce un factor de regularización que se suma con un delta a la función objetivo para que el fit se haga a una tasa más lenta y se tenga tiempo de evaluar los resultados con mejor precisión. Este método aún presenta el problema de inicializar las matrices factorizadas con valores aleatorios, o sea un cold start.</dd>
  <dd><em>Semipositive and Positive MF: </em> Se aplica un threshold a los resultados de RISMF para evitar resultados negativos. De esta forma, las factorizaciones resultan positivas o semipositivas. Se utiliza cuando un requerimiento consiste en que los usuarios y los ítems deben ser números positivos.</dd>
  <dd><em>Momentum Method: </em> Consiste en modificar ligeramente las reglas con las que se verifican las ecuaciones de RISMF dentro del algoritmo. Se introduce un factor de momento que es utilizado junto a un delta de características de usuarios y de ítems. Se calculan los nuevos gradientes utilizando el gradiente anterior y este nuevo término. Este método no da resultados más precisos, pero combina bien con otros métodos.</dd> 
  <dd><em>Retraining User Features: </em> En RISMF, las características de los usuarios cambian junto a las de los ítems, lo que causa que los datos individuales de cada ítem sean irrecuperables mientras más se desciende por el gradiente para calcular las nuevas factorizaciones. Para solucionar esto existen dos opciones: Hacer el testing por cada una de las 'épocas'o iteraciones del algoritmo, o recomputar todas las características de los usuarios luego de entrenar el modelo. El mejor método resulta ser reinicializar la matriz de usuarios en cada iteración pero mantener la matriz de ítems durante todo el proceso. Haciendo esto se gana en confiabilidad para agregar nuevos usuarios a la base de datos.</dd>
  <dd><em>Transductive MF: </em>Al método dado por la factorización de matrices normal, se le agrega un coeficiente de atenuación para lograr que la factorización de entrenamiento modere su input del set de validación en cada iteración. Por supuesto, esto supone que se ha particionado el dataset en un set de training  otro de testing, que en este caso se considera 'validación'. De esta forma se puede iterar para cada usuario pero teniendo cierto input de testing para cada uno.</dd>
  <dd><em> 2D Variant of the Matrix Factorization Algorithm: </em>Se computa la similaridad entre dos sets de datos de usuarios e ítems de dos dimensiones. Esta similaridad no es más que la distancia euclidiana entre cada dato correspondiente. Luego se aplica la versión 2D del descenso de gradiente para terminar con una matriz que por su naturaleza está compuesta de zonas con clasificaciones de preferencias distintivas, por ejemplo, características 'horroroso' y 'romántico'.</dd>
  <dd><em> Connections with Neural Networks: </em>Se utiliza RISMF junto a una red neural. Esto significa que hay un RISMF por cada rama de la red, y el error de estimación tiene back-propagation para continuar con el entrenamiento. Así se tienen múltiples pruebas de coeficientes que dan un elemento de cada matriz.</dd>
  <dd><em>Neighbor Based Correction of MF: </em>Es distinto de MF en que no se utiliza descenso de gradiente, sino que se entrena sumando la similaridad entre iteraciones. La similaridad se calcula entre un usuario y su vecino. La ventaja es que, si bien el entrenamiento es parecido a User KNN, se tiene como base la factorización matricial de los usuarios y los ítems. O sea, la similaridad se suma a la matriz que los otros métodos intentan optimizar.</dd>
  <dd>Los resultados sugieren que para los métodos anteriores es recomendable particionar para usuarios y no para ítems. Las pruebas se realizan cambiando los parámetros: Coeficiente de regularización, número de características (K) y coeficiente de atenuación. De todas las pruebas, el método que utiliza la factorización matricial junto al coeficiente de similaridad euclidiano da los mejores resultados. Esto no debería ser sorprendente, pues el coeficiente de similaridad, visto de forma matemática, es una corrección adicional al resultado del descenso de gradiente. Tiene sentido que un algoritmo con regularización y similaridad, con la ventaja de que es rápido de calcular, sea el mejor evaluado con una mejora del orden del 0.01 de disminución de error.</dd>
  <dd>Por otro lado, la selección de los sets de training y validación (o testing) juega un rol muy importante en el grado de mejora de los resultados, o si estos solo agregan a resultados reportados anteriormente por otros autores. Se observa primero que todo que aumenta el error si los datasets son pequeños.</dd>
  <dd>Contrario a lo que se esperaría, retener las características de los usuarios no mejora significativamente el error, resulta que introducir coeficientes para corregir el método básico de descenso de gradientes es preferible. Mi mejor explicación para esto consiste en que las características de los usuarios no son necesariamente lo que debe asignárseles. Los usuarios rellenan la base de datos con sus preferencias del momento y no necesariamente reflejan su personalidad, o sus preferencias al aplicarla a su toma de desiciones. Sin embargo, este método funciona muy bien para usuarios nuevos. Esto puede deberse a un efecto psicológico de que el modelo "entiende" a la persona, o que la está "escuchando" en sus opiniones expresadas sin importar lo que sean. Esto abre la puerta a que el usuario continúe interactuando.</dd>
  <dd>En definitiva, el modelo puede ser su peor enemigo al ir más allá de lo que el usuario ha ingresado explícitamente para tomarlo como su texto sagrado. Es necesario moderar cada paso que toma para extrapolar la personalidad el usuario, porque de otra forma tiene a no innovar en lo que podría querer en el futuro. Después de todo de eso se tratan los sistemas recomendadores, tienen que predecir el futuro de seres impredecibles hasta cierto grado.</dd>
</dl>

<dl>
  <dt>[07-08-2019] Ranking no personalizado (Blog de Evan Miller,
2009)</dt>
  <dd>El autor compara tres métodos de estimación del intervalo de confianza de una distribución binomial. Esto es para poder aproximar la probabilidad de que una persona dé una valoración positiva a cierto contenido. 
    Los tres métodos consisten en: Diferencia entre ratings positivos y negativos, valoraciones positivas promedio, Intervalo de Wilson. Están ordenados por robustez. </dd>
  <dd>
    <em>El método de diferencia de ratings</em> falla en que no está normalizado, o sea que no importa el tamaño de la muestra de calificaciones, siempre 'ganará' el contenido con menos valoraciones negativas, cuando debería destacar el contenido con mayor cantidad total de valoraciones positivas.</dd>
    <dd>
    <em>El método de valoraciones positivas promedio</em> no tiene la debilidad del anterior, pero discrimina en contra de ítems con una grantidad de valoraciones positivas que poseen valoraciones negativas.</dd>
      <dd>
    <em>El método del Intervalo de Wilson</em> es teóricamente robusto al basarse en métodos estadísticos en vez de funcionar como una 'rule of thumb'. Donde dice que se suma o resta un término, se selecciona la suma para ir al valor máximo del intervalo, y la resta para el valor mínimo. El intervalo de confianza asegura una coincidencia de preferencias del 95%, pero puede ser reemplazado con confianzas mayores al 'hardcodear' otros valores en el parámetro de confianza para general la distribución normal de la que se origina el intervalo.
  </dd>
    
<img src="http://www.evanmiller.org/images/average-rating/equation.png" alt="Score = Lower bound of Wilson score confidence interval">

<dd>En general, el ranking no persnalizado con el intervalo de Wilson es el estado del arte en este tipo de sistema recomendador. Resulta ser el más robusto y práctico. Sin embargo, sus predicciones fallan en casos especiales en los que los sistemas personalizados no pueden.</dd>

</dl>
