---
nav_order: 7
---

# Postprocesamiento

> Herramientas para el postprocesamiento e interpretación de los datos.

<center><iframe max-width="400" aspect-ratio="0.5625" src="https://www.youtube.com/embed/MUQfKFzIOeU" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" 
allowfullscreen>
</iframe></center>


## Rosa de vientos:
https://mesonet.agron.iastate.edu/sites/dyn_windrose.phtml?station=SAEZ&network=AR__ASOS&bin0=2&bin1=5&bin2=7&bin3=10&bin4=15&bin5=20&units=mph&nsector=36&fmt=png&dpi=100&year1=2021&month1=12&day1=1&hour1=0&minute1=0&year2=2021&month2=12&day2=31&hour2=23&minute2=59


## aerplot



## Resumen:

### Formato de datos espaciales

+ Vectoriales:
	- ``WKT``
	- ``.gpkg ``
	- ``.shp ``

+ Matriciales (Raster)
	- ``.tiff``
	- ``.h5``
	- ``.nc``


```bash
gdal_translate -a_srs epsg:${epsg_local} ${file_out}.xyz ${file_out}XY.tif
```

### Proyección

```bash
gdaltransform -s_srs epsg:${epsg_local} -t_srs epsg:${epsg_latlon}
```


### Crop & Mask

```bash
   gdalwarp -tr ${dx} ${dx} -r cubicspline -t_srs epsg:${epsg_local} -te ${xini2} ${yini2} ${xfin2} ${yfin2} ${inp_dem} ${dem_file}
```

### Interpolación 

```bash
   gdalwarp -tr ${dx} ${dx} -r cubicspline -t_srs epsg:${epsg_local} -te ${xini2} ${yini2} ${xfin2} ${yfin2} ${inp_dem} ${dem_file}
```

### Filtros

```bash
   gdal_calc.py --format GTiff -A ${file_out}.tif --outfile "${file_out}BG.tif" --calc "A + ${BG}" 
```

### Gráficos

```bash
   gdal_contour -b 1 -a ELEV -i 10.0 -f "GPKG" -fl 0.1 1 10

```


### Herramientas para generar mapa isoconcentraciones:




### Herramientas para generar tabla de concentraciones máximas:



## Ejerecicios:



