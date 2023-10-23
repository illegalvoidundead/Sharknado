###**__Documentación del proyecto__**

##__1.Exploración de la tabla__

He comenzado por explorar la tabla con el método shape para saber por cuantas filas y columnas estaba compuesta. Después he visualizado la tabla seguido del método head para visualizar las primeras 200 filas y hacerme una idea general del contenido y estructura de la tabla. Más adelante he usado el metodo columns para obtener el nombre de las columnas. Con el método info seguido memory usage he obtenido el uso de memoria total de los elementos del DataFrame. También he visualizado las descripciones estadísticas de las columnas numéricas y no numéricas. Después he creado una variable llamada "nulos_al_inicio" en la cual he almacenado el número total de nulos de data frame para poder compararlo más adelante durante el proceso de limpieza. Seguidamente he visualizado el número de nulos por columna de las columnas que tenían al menos un valor nulo. Lo que he hecho después ha sido explorar las columnas "Unnamed: 22" y "Unnamed: 23", ya que son las que más valores nulos tenían, para ello he utilizado los métodos value counts (que me ha devuelto un solo valor para "Unnamed: 22" y dos valores para "Unnamed: 23") y .notnull().idxmax() junto .loc para localizar donde se encontraban dichos valores, con data.iloc he examinado la tabla a la altura de estos valores y no he observado nada remarcable.
Contando de nuevo los nulos por columnas y una vez he eliminado las columnas "Unnamed: 22" y "Unnamed: 23" he observado que las columnas 'href formula' y 'href' tenían un número de nulos muy parecidos y eso me ha hecho sospechar que estaban duplicadas. A través del método .index combinado con .isnull y  .tolist he descubierto que los nulos de esas dos columnas se encontraban entre las filas 6302 y 25723, así que he utilizado len() e .isnull() para comparar con len() e iloc()i y saber si la cantidad de elementos que hay en esas filas es igual al numero de elementos nulos que hay entre las filas.
He pedido  que se me muestre la tabla a la altura de las filas donde Time es nulo.
Con "data.isnull().all(axis=1).any()" he consultado si hay alguna fila en la que todos sus  valores sean nulos, no la hay.
He visualizado la tabla entera allí donde la columna 'Species' tuviera un valor nulo y lo único que consigo es aumentar mi astigmatismo y darme cuenta de que tengo una incipiente presbicia.
Utilizando el método .loc observo que en la columna 'Name' aparece en algunas ocasiones el sexo.
Consulto en qué filas están los nulos de la columna Year.
Compruebo si los valores dentro de las columnas dentro de 'Case Number', 'Case Number.1' y 'Case Number.2' están repetidos.
Pregunto cuantas filas hay con mas de tres valores Unknown, hay 159.
Creo una columna que tenga los valores de la columna Fatal (Y/N) en la cual Y=1 y N=0, hago un diagrama de caja y bigotes y no observo nada raro. Borro la columna.

##__2-Limpieza de la tabla__

Lo primero que he hecho ha sido eliminar las columnas "Unnamed: 22" y "Unnamed: 23", ya que todos sus valores excepto 1 y 2 eran nulos.
He eliminado la columna 'href formula' por redundante.
Elimino las filas comprendidas entre la 6302 y la 25723.
He sustituido los nulos de la columna Time por 0.
He corregido el nombre de la columna 'Species', el cual tenía un espacio al final.
Sustituyo por Unknown los valores nulos de la columna 'Species'.
Sustityo por 0 los valores nulos de la columna 'Age'.
Cambio el nombre de la columna 'Sex' ya que tenía un espacio al final de este.
Siempre que en la columna 'Name' aparece información acerca del sexo, cambio el valor que aparece en la columna 'Sex' por el mismo que hay en 'Name'.
Sustituyo por Unknown los nulos de la columna Activity.
Custituyo por Unknown los nulos de la columna Location.
Corrijo el nombre de la columna Fatal (Y/N) el cual tenía un espacio al final.
En la columna 'Fatal (Y/N)' sustituyo los valores por 'Y' cuando en la columna 'Injury' aparezca el valor FATAL
Por si acaso queda algún nulo en la columna 'Fatal (Y/N)' relleno con el método fillna.
He instalado geopy porque me iba a flipar averiguando, a partir de la localización, el país y el estado/provincia para rellenarlos allí donde son nulos, pero pierdo mucho tiempo intentándolo sin éxito. Se me hace tarde, ansiedad.
Sustituyo por Unknown los nulos de la columna Area.
Sustituyo por Unknown los nulos de la columna Name.
Sustituyo por Unknown los nulos de la columna Country.
Sustituyo los valores nulos de la columna Injury por el valor FATAL, siempre y cuando en la columna Fatal (Y/N) haya un valor Y.
Sustituyo por Unknown los nulos de la columna Investigator or Source.
Sustituyo por Unknown los nulos de la columna Type.
Sustituyo los nulos de la columna Year por el año que indica el valor de la columna Date.
Sustituyo por Unknown los nulos de la columna Year.
Normalizo las referencias cambiando las comas por puntos en las tres columnas 'Case Number', 'Case Number.1' y 'Case Number.2'.
Corrijo el nulo de la columna 'Case Number' basándome en el valor de la columna 'Date'
Decido no eliminar las columnas Case Number, Case Number.1 y Case Number.2 puesto que son números para clasificar los casos de uso interno y del cual desconozco si las diferencias se deben a errores o no.
Sustituyo todos los valores unknown por Unknown.
Elimino las filas donde hay mas de tres valores Unknown.
Elimino la palabra reported de las fechas, con esto me doy por satisfecho porque convertirlas a datetime es imposible.
Elimino los espacios al principio de palabra en la columna Date.
En la columna Time cambio por 0 todo los valores que no tengan el formato xxhxx y sustituyo por dos puntos las h.

##__3.Creación de una nueva columna__
Cuento las veces que cada elemento de la columna Activity coincide con una Y en la columna fatal.
Creo una columna llamada Risk en la que figuran la veces que la actividad realizada ha tenido un desenlace fatal.




















