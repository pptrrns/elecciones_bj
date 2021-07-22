# elecciones_bj
# Nota metodológica

Se presentan tres mapas temáticos de los *Resultados para la Jefatura Delegacional/Alcaldía Benito Juárez* de los procesos ordinarios locales de 2015, 2018 y 2021; para la elaboración de los mapas se utilizaron las Estadísticas de las elecciones de 2015 y 2018, y los resultados del Sistema de Cómputos Distritales y de Demarcación 2021 del [Instituto Electoral de la Ciudad de México](https://www.iecm.mx).

Los datos originales descargados del IECM fueron procesados para obtener los primeros lugares por sección electoral y los margenes de victoria de cada fuerza política, así como los porcentajes de votación de cada partido político y coalición. Además, se obtuvo el porcentaje de participación electoral a nivel sección.

Los datos originales y procesados se pueden descargar dándo click en el enlace de cada proceso electoral.

|              Originales              |              Procesados              |
| :----------------------------------: | :----------------------------------: |
| [Elección Ordinaria Local de 2015]() | [Elección Ordinaria Local de 2015]() |
| [Elección Ordinaria Local de 2018]() | [Elección Ordinaria Local de 2018]() |
| [Elección Ordinaria Local de 2021]() | [Elección Ordinaria Local de 2021]() |

## Productos (Mapas)

Los mapas temáticos se elaboraron utilizando la plataforma [CartdoDB](https://carto.com); en cada mapa se representa a nivel sección (unidad geográfica) el margen de victoria de la primera fuerza política y de la segunda fuerza política, así como el porcentaje de participación electoral.

* [Resultados BJ 2015](https://bit.ly/3eE16i4)
* [Resultados BJ 2018](https://bit.ly/3isn88E)
* [Resultados BJ 2021](https://bit.ly/2UXWBbc)

Los valores de estas variables estadísticas se visualizan de acuerdo a la gama cromática seleccionada para cada partido; por ejemplo, si el ganador de la primera fuerza política en la sección electoral 4272 es el Partido Acción Nacional, el color que veremos representado en el mapa será el azul. 

Es importante destacar que mientras más oscuro sea el color, mayor es el margen de victoria para la primera fuerza o mayor el procentaje de participación electoral, pero si se está analizando las segundas fuerzas políticas, mientras más oscuro sea el color, menor es el margen de victoria de la primera fuerza respecto de la segunda.

### Herramientas de análisis (Widgets)

En la parte derecha de los mapas encontramos una barra de widgets o herramientas de análisis que nos permiten filtrar información de acuerdo a las variables que deseamos aislar. Las variables disponibles en los widgets son:

- Primera Fuerza Política `_1er`
- Segunda Fuerza Política `_2ndo`
- Tercera Fuerza Política `_3er`
- Participación `part_p`
- Votación PAN `pan_p`
- Votación Morena `morena_p`
- Votación PRI `pri_p`
- Votación PRD `prd_p`
- Votación MC `mc_p`

De este modo, es posible, por ejemplo, visualizar datos de participación electoral a nivel sección `part_p` y la votación para un determiando partido en esas undiades geográficas `morena_p`.  Además, al momento de realizar la filtración por variables es posible establecer intervalos de participación y/o de votación, lo que nos representará un mapa en el que exclusivamente se visualicen las unidades geográficas que cumplan con esas condiciones,.

Como herramientas de análisis, los widgets también nos permiten:

-  *estilizar* basándonos en una variable
-  *estilizar* por categoría

### Paso a paso

Para replicar este ejercicio debe:

* Descargar los datos procesados del mapa que deseemos elaborar
* agregarlos al Dashboard de [CartoDB](https://carto.com/blog/new-dashboard/)
* crear un nuevo mapa utilizando los datos procesados

##### Layer Colonias

- Damos click en *Style tab*
- Damos click en *CartoCSS*
- Agregamos el código de la capa que estamos estilizando

```css
#layer {
  polygon-fill: #826dba;
  polygon-opacity: 0;
}

#layer::outline {
  line-width: 1;
  line-color: #ffffff;
  line-opacity: 0.5;
}
```

- Aplicamos los cambios para ver el nuevo diseño de la capa *Colonias*.

##### Layer Primera Fuerza Política

- Damos click en *Style tab*
- Estilizamos por valor
- Buscamos  `_1er`
- Establecemos el número de grupos en 7 y mantenemos la clasificación por *quantiles*
- Damos click en *CartoCSS*
- Agregamos el código de la capa que estamos estilizando

```css
#layer {
  #layer::outline {
  line-width: 1;
  line-color: #FFFFFF;
  line-opacity: 0.3;
  polygon-gamma: 0.4;
  polygon-opacity: 1;
    
     [_1er = 'PAN']{
  polygon-fill: ramp([marg_p_1_2], (#9cadd2, #8399c7, #6a85bb, #5170b0, #395ca5, #204799, #07338e), quantiles);
    }
    
    [_1er = 'MORENA']{
      polygon-fill: ramp([marg_p_1_2], (#e1a8a5, #da938f, #d37d78, #cb6762, #c4514b, #bc3c35, #b5261e), quantiles);
    }
  }
}
```

- Aplicamos los cambios para ver el nuevo diseño de la capa *Primera Fuerza Política*

##### Layer Segunda Fuerza Política

* Damos click en *Style tab*
* Estilizamos por valor
* Buscamos  `_2ndo`
* Establecemos el número de grupos en 7 y mantenemos la clasificación por *quantiles*
* Damos click en *CartoCSS*
* Agregamos el código de la capa que estamos estilizando:

```css
#layer {
  #layer::outline {
  line-width: 1;
  line-color: #FFFFFF;
  line-opacity: 0.3;
  polygon-gamma: 0.4;
  polygon-opacity: 1;
    
     [_2ndo = 'PAN']{
  polygon-fill: ramp([marg_p_1_2], (#07338e, #204799, #395ca5, #5170b0, #6a85bb, #8399c7, #9cadd2), quantiles);
    }
    
    [_2ndo = 'MORENA']{
      polygon-fill: ramp([marg_p_1_2], (#b5261e, #bc3c35, #c4514b, #cb6762, #d37d78, #da938f, #e1a8a5), quantiles);
    }
    
    [_2ndo = 'PRI']{
  polygon-fill: ramp([marg_p_1_2], (#00923f, #1a9d52, #33a865, #4db379, #66be8c, #80c99f, #99d3b2), quantiles);   
    }
    
    [_2ndo = 'MC']{
      polygon-fill: ramp([marg_p_1_2], (#fe8400, #fe901a, #fe9d33, #fea94d, #feb566, #ffc280, #ffce99), quantiles);
    }
    
    [_2ndo = "PRD"]{
    polygon-fill: ramp([marg_p_1_2], (#ffcb03, #ffd01c, #ffd535, #ffdb4f, #ffe068, #ffe581, #ffea9a), quantiles);
    }
  }
}
```

- Aplicamos los cambios para ver el nuevo diseño de la capa *Segunda Fuerza Política*

##### Layer Participación

* Damos click en *Style tab*
* Estilizamos por valor
* Buscamos  `part_p`
* Establecemos el número de grupos en 7 y mantenemos la clasificación por *quantiles*
* Damos click en *CartoCSS*
* Agregamos el código de la capa que estamos estilizando:

```CSS
#layer{
#layer::outline {
  line-width: 1;
  line-color: #FFFFFF;
  line-opacity: 0.3;
  polygon-gamma: 0.4;
  polygon-opacity: 1;
  polygon-fill: ramp([part_p], (#f3cbd3, #eaa9bd, #dd88ac, #ca699d, #b14d8e, #91357d, #6c2167), quantiles);
  }
}
```

- Aplicamos los cambios para ver el nuevo diseño de la capa *Participación*

##### Nota

La gama cromática seleccionada para cada partido es la siguiente:

* **Partido Acción Nacional**  `#07338e`
  *Gama cromática*: `#e6ebf4, #cdd6e8, #b5c2dd, #9cadd2, #8399c7, #6a85bb, #5170b0, #395ca5, #204799, #07338e`

* **Movimiento de Regeneración Nacional**  `#b5261e`
  *Gama cromática*: `#f8e9e9, #f0d4d2, #e9bebc, #e1a8a5, #da938f, #d37d78, #cb6762, #c4514b, #bc3c35, #b5261e`

* **Partido Revolucionario Institucional**  `#00923f`
  *Gama cromática*: `#e6f4ec, #cce9d9, #b3dec5, #99d3b2, #80c99f, #66be8c, #4db379, #33a865, #1a9d52, #00923f`

* **Partido de la Revoculión Democrática**  `#ffcb03`
  *Gama cromática*: `#fffae6, #fff5cd, #ffefb3, #ffea9a, #ffe581, #ffe068, #ffdb4f, #ffd535, #ffd01c, #ffcb03`

* **Movimiento Ciudadano** `#fe8400`
  *Gama cromática*: `#fff3e6, #ffe6cc, #ffdab3, #ffce99, #ffc280, #feb566, #fea94d, #fe9d33, #fe901a, #fe8400`

* **Partido Verde Ecologista de México** `#50b748`
  *Gama cromática*:`#eef8ed, #dcf1da, #cbe9c8, #b9e2b6, #a8dba4, #96d491, #85cd7f, #73c56d, #62be5a, #50b748`

* **Partido del Trabajo** `#da251d`
  *Gama cromática*: `#fbe9e8, #f8d3d2, #f4bebb, #f0a8a5, #ed928e, #e97c77, #e56661, #e1514a, #de3b34, #da251d`

* **Porcentaje de participación electoral** `#6c2167`

  *Gama cromática:* `#f3cbd3, #eaa9bd, #dd88ac, #ca699d, #b14d8e, #91357d, #6c2167`

### Descargas

Se pueden descargar los mapas  terminados dándo click aquí:

* [Resultados BJ 2015]()
* [Resultados BJ 2018]()
* [Resultados BJ 2021]()

## Autor

José Á. Torrens Hernández, 2021. [**@pptrrns**](https://twitter.com/pptrrns)

https://torrens.carto.com/me

pptrrns@gmail.com

## Licencia

© [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)

© [OpenStreetMap](http://www.openstreetmap.org/copyright)
