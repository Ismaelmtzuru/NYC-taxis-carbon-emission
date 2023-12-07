# NYC Taxis & Carbon Emission

![Taxis Carbon Emission, NYC](taxis.png)



## Contexto

En la ciudad de Nueva York, los servicios de taxis y de viajes compartidos en vehículos como Uber, han transformado la forma en que las personas se desplazan por las calles. Estos servicios brindan una alternativa conveniente y relativamente accesible al transporte público y al alquiler de automóviles. Además, estos servicios generan una gran cantidad de datos que pueden ser procesados y analizados por consultoras, empresas organismos públicos y también, por estudiantes de Ciencias de Datos.

Los servicios de taxis y de viajes compartidos en vehículos generan grandes cantidades de datos en tiempo real, incluyendo información sobre la ubicación del vehículo, la duración del viaje, la tarifa cobrada y la calificación del conductor. Estos datos pueden ser utilizados para identificar patrones de viaje y demanda, así como para mejorar la eficiencia y la calidad del servicio.

El cambio climático se ha acelerado a niveles sin precedentes como consecuencia de las actividades humanas, siendo una de las mayores responsables la necesidad de energía obtenida a partir de diversas fuentes de combustibles fósiles. El impacto del desarrollo energético en el ambiente y los consumos generados, atraen a las compañías a tomar acción en cómo intervenir en estas problemáticas. Lo cual lleva a mediciones de consumo y generación para intervenir o mejorar dicha generación/consumo.

## Rol a desarrollar

Una empresa de servicios de transporte de pasajeros, que actualmente se encuentra operando en el sector de micros de media y larga distancia, está interesada en invertir en el sector de transporte de pasajeros con automóviles. Con una visión de un futuro menos contaminado y ajustarse a las tendencias de mercado actuales, quieren corroborar la relación entre estos medios de transporte particulares y la calidad del aire, como también la contaminación sonora, para estudiar la posibilidad de implementar vehículos eléctricos a su flota; ya sea en su totalidad o parte de la misma.

Pero debido a que sería una unidad de negocio nueva, se pretende hacer un análisis preliminar del movimiento de los taxis en la ciudad de Nueva York, para poder obtener un marco de referencia y poder tomar decisiones bien fundamentadas.

Tu equipo es contratado por dicha empresa, con el objetivo de acompañar al negocio, en ese proceso de toma de decisión, para lo cual deberán utilizar los datos provistos de mayor calidad encontrados, y cruzarlo con otros datos, como los ofrecidos por viajes compartidos, calidad del aire, contaminación sonora y correlaciones climáticas. Nota: Pueden agregar todos los datasets que consideren pertinentes para cumplir la propuesta de trabajo, pero es obligatorio cruzar el dataset de taxis con al menos otros dos (condición necesaria de aprobación).

## Propuesta de trabajo

1. **Recopilar, depurar y disponibilizar la información:** Creación de una base de datos (DataWarehouse) de diferentes fuentes, tanto provistas por Henry como incorporadas por ustedes, corriendo en local o alojada en proveedores en la nube. La base de datos depurada deberá contemplar por lo menos dos tipos diferentes de extracción de datos, ejemplo: datos estáticos, llamadas a una API, scrapping, entre otros.

2. **Reporte y análisis significativos de la(s) línea(s) de investigación escogidas:** El análisis debe contemplar las relaciones entre variables y concluir, si es que existe, una relación entre estas, y los posibles factores que causan dicha relación en la realidad.

3. **Entrenamiento y puesta en producción de un modelo de machine learning de clasificación no supervisado o supervisado:** El modelo debe resolver un problema y conectar globalmente con los objetivos propuestos que se propongan como proyecto.

## Ideas de análisis e implementación

Algunas de las métricas e indicadores que podrían implementar son:

- Duración de viajes
- % Rates
- Viajes inter e intra boroughs
- Días, días de la semana y semanas con más viajes
- Trip distance por pasajero
- Avg tips por pasajero
- % payments types
- Borough con mayor/menor cantidad de viajes
- Viajes entre distintas Zonas
- Relación de cantidad de viajes con contaminación del aire y sonora
- Nivel sonoro autos a combustión vs autos eléctricos
- Valores y depreciación vehículos a combustión (nuevos y/o usados) vs vehículos eléctricos
- Relación precio vehículo eléctrico con velocidad de carga del mismo
- Mejoramiento de estrategias de marketing: campañas microsegmentadas
- Mapas interactivos para acompañar los análisis. Distribución de puntos de carga y los diferentes medios que hay en US: Charging Station Distribution US and Canada

Datos adicionales a cruzar: Servicios de viajes de otras plataformas, condiciones climáticas, contaminación sonora, contaminación del aire, emisión de CO2 y otros gases, análisis poblacional, ubicación de actividad comercial.

## Datasets y fuentes complementarias

Los datos son extraídos de las recolecciones hechas por NYC Taxi and Limousine Commission y otros organismos de NYC. Brinda información sobre cada viaje, los Boroughs, dónde está cada sensor de sonido / calidad del aire, emisiones de CO2 generales entre otros datos que pueden expandir y buscar datasets alternativos o más actualizados si así lo desean (siempre y cuando puedan cumplir con lo propuesto).

- Fuente data de viajes
- Datos de Transporte Público
- Historical Weather API
- API's de las condiciones climáticas
- Dataset de Kaggle sobre emisiones de CO2 por país y año, con ajustes por población
- Dataset de los sonidos recolectados en NYC
- Dataset de la calidad del aire de NYC
- ¿Qué es un Borough?
- Fuel consumption ratings
- Archivo de zonas de NYC --> taxi+_zone_lookup.csv

Ejemplos de Boroughs y sus LAT Y LONG:
- Manhattan, New York City, NY, USA (40.776676, -73.971321)
- Brooklyn, New York City, NY, USA (40.650002, -73.949997)
- Bronx, New York City, NY, USA (40.837048, -73.865433)
- Queens, New York City, NY, USA (40.742054, -73.769417)
- Staten Island, New York City, NY, USA (40.579021, -74.151535)


