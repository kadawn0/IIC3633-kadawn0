# Blog IIC3633 de Catalina Sarmiento
Blog para el curso Sistemas Recomendadores

![Imagen importante](https://vignette.wikia.nocookie.net/fallout/images/f/f0/Fo4-pebbles-artwork.png/revision/latest?cb=20151215234614 "Imagen importante")

## Posts

<dl>
  <dt>[??-08-2019] Collaborative filtering recommender systems. In The adaptive web</dt>
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
