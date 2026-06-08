+++
title = 'Cómo crear un Centro y un Almacén en SAP'
date = 2026-06-03T00:00:00+02:00
draft = false
categories = ["SAP"]
showReadingTime = true
ShowShareButtons = false
+++

¿Qué es un centro? ¿Cómo se relaciona un centro con un almacén? Estas son las preguntas que responderemos en esta publicación. Además, te mostraré cómo crearlos en SAP.

<span class="highlight">Centro</span>

Volvamos al ejemplo que utilizamos en nuestro artículo anterior sobre la creación de una sociedad y una sociedad financiera. Utilizamos el Grupo Volkswagen como ejemplo. El Grupo Volkswagen fabrica automóviles y, para ello, necesita una planta de producción, ¿verdad? Pues eso es exactamente lo que representa un centro en términos sencillos.

Veamos cómo define SAP un centro. <span class="highlight-text">Se define como un lugar donde se producen materiales, se reciben y expiden mercancías, se gestiona el inventario y se realiza la planificación de la producción. Si todas estas actividades se llevan a cabo en un mismo lugar, entonces se considera un centro.</span>

Veamos un ejemplo real.

| CENTRO | DESCRIPCIÓN                    |
| ------ | ------------------------------ |
| MD01   | Planta de ensamblaje de Madrid |
| BCN1   | Almacén de piezas de Barcelona |
| VAL1   | Fábrica de motores de Valencia |

Todos estos son ejemplos de centros. Cada centro es una unidad logística independiente en SAP. Esto significa que SAP controla las existencias, la producción y los movimientos de materiales de forma individual para cada centro.

<span class="highlight">Almacén</span>

Ahora que ya sabemos qué es un centro, veamos qué es un almacén. <span class="highlight-text">Es un concepto muy sencillo. Si quieres fabricar algo, necesitas guardar en algún lugar las materias primas necesarias para la producción, ¿verdad? Ese lugar se denomina almacén en SAP.</span>

En el ejemplo anterior elegí tres centros, pero para simplificar utilizaré solo uno: la planta de ensamblaje de Madrid.

| ALMACÉN | DESCRIPCIÓN                     |
| ------- | ------------------------------- |
| RM01    | Almacén de materias primas      |
| FG01    | Almacén de productos terminados |
| QA01    | Área de inspección de calidad   |

Imagina que la planta de ensamblaje de Madrid recibe materias primas y componentes como motores, neumáticos, pintura, ventanas, etc. Todos estos materiales deben almacenarse en algún lugar. Si se trata de materias primas para la fabricación, se almacenan en RM01. Si son productos terminados, se almacenan en FG01. Del mismo modo, los materiales destinados a controles de calidad pueden almacenarse temporalmente en QA01 para su inspección.

<span class="highlight-text">En resumen, un centro puede tener varios almacenes asignados. Sin embargo, cada almacén solo puede estar asignado a un único centro.</span>

<span class="highlight">Creación de un centro en SAP</span>

Este proceso es bastante sencillo y muy parecido a la creación de una sociedad financiera. <span class="highlight-text">Existen dos formas de acceder a la pantalla de creación de centros. El código de transacción (t-code) es `OX10`. También puedes acceder desde la ruta IMG de SAP: Estructura empresarial → Definición → Logística general → Definir, copiar, eliminar y verificar centro.</span>

Voy a utilizar el t-code `OX10`, que te llevará a la siguiente pantalla.

![Pantalla de creación de centro en SAP](/img/sap-2/plant-creation.png)

Una vez allí, haz clic en el botón **Nuevas entradas**. Llegarás a esta pantalla.

![Pantalla de creación de centro en SAP](/img/sap-2/fac-cal.png)

He marcado el campo **Calendario de fábrica** porque es necesario crear uno. Para este ejemplo voy a crear uno. Te mostraré los pasos, pero básicamente un calendario de fábrica define los días laborables reales en los que la fábrica está operativa. Por tanto, hay que tener en cuenta los festivos. Esto significa que antes de crear un calendario de fábrica debemos crear también un calendario de festivos.

<span class="highlight">Creación de un calendario de fábrica en SAP</span>

<span class="highlight-text">El t-code para esta tarea es `SCAL`, aunque por alguna razón no funciona en mi servidor de formación. Por ello utilizaremos la ruta IMG de SAP: Gestión de tiempos → Horarios de trabajo → Definir clases de festivos.</span>

Al acceder verás una pantalla como esta.

![Creación de festivos en SAP](/img/sap-2/pub-hol.png)

Selecciona **Festivo** y haz clic en el botón que aparece en la imagen.

![Creación de festivos en SAP](/img/sap-2/create.png)

Haz clic en **Crear** en la parte superior. Se abrirá una ventana emergente. Selecciona la opción **Fecha fija** y pulsa el botón **Crear** situado en la parte inferior.

![Creación de festivos en SAP](/img/sap-2/holiday-setup.png)

Vamos a rellenar los campos con un festivo de ejemplo. He elegido el día 25 y el mes 12, ya que la Navidad es festiva en gran parte del mundo. Después pulsa el botón **Crear**. Aparecerá una ventana emergente; haz clic en el icono de confirmación (marca verde) y habrás terminado.

El siguiente elemento de la lista es el **Calendario de festivos**. Debemos crear uno siguiendo prácticamente los mismos pasos, pero esta vez tendremos que añadir los festivos que acabamos de crear. Cuando accedas a la pantalla de creación del calendario de festivos verás algo parecido a esto.

![Creación de calendario de festivos en SAP](/img/sap-2/holiday-cal.png)

En esta pantalla debes introducir un ID de calendario y un nombre para el calendario. Después debes asignar el festivo creado anteriormente (en nuestro caso, Navidad). Marca la casilla correspondiente y pulsa el botón **Asignar festivo**. Finalmente, guarda los cambios. El calendario de festivos ya estará creado. Anota el ID del calendario porque lo necesitaremos para crear el calendario de fábrica.

Ahora volvemos atrás y seleccionamos **Calendario de fábrica** desde el mismo lugar donde configuramos las otras dos opciones. Al seleccionarlo accederás a esta pantalla.

![Creación de calendario de fábrica en SAP](/img/sap-2/fac-calendar.png)

Haz clic en el botón **Crear**, tal como se muestra en la imagen.

![Creación de calendario de fábrica en SAP](/img/sap-2/create-fac-cal.png)

Ahora estás en la pantalla de creación del calendario de fábrica. Debes introducir un ID; en mi caso he utilizado `ES`. Añade también un nombre adecuado para el calendario. Puedes dejar los campos **Válido desde** y **Válido hasta** tal como están.

El último paso consiste en vincular el calendario de festivos al calendario de fábrica. Una vez hecho esto, guarda los cambios. Aparecerá una ventana emergente; pulsa la marca verde para confirmar. Ya has creado un calendario de fábrica.

**Volvamos ahora a la creación del centro**

Utilizaremos el t-code `OX10`. Haz clic en **Crear** y completa los datos correspondientes. Como ya hemos creado nuestro calendario de fábrica, también podemos asignarlo aquí. Ten en cuenta que el código de centro debe tener 4 caracteres alfanuméricos y conviene recordarlo. En mi caso utilizaré `MD01`.

![Creación de centro en SAP](/img/sap-2/plant-creation-done.png)

Pulsa **Guardar**. Aparecerá una ventana emergente donde deberás introducir la dirección y los datos de comunicación, igual que hicimos anteriormente al crear la sociedad financiera.

![Dirección del centro en SAP](/img/sap-2/plant-address.png)

Como puedes ver, ya he rellenado los datos de dirección y comunicación. Cuando termines, pulsa la marca de confirmación situada en la parte inferior. Después aparecerá una solicitud de transporte; vuelve a confirmar y habrás terminado. Tu centro se habrá creado correctamente.

<span class="highlight">Creación de un almacén</span>

Como expliqué en el ejemplo, un almacén debe estar vinculado a un centro. Por eso vamos a crear uno ahora. <span class="highlight-text">El t-code para crear un almacén es `OX09`. También puedes acceder mediante la ruta SPRO: Estructura empresarial → Definición → Gestión de materiales → Mantener almacenes.</span>

Voy a utilizar `OX09`. El sistema te pedirá que indiques el centro en una pantalla como esta. Introduce el código alfanumérico de 4 caracteres del centro y pulsa Enter.

![Asignación de almacén a centro en SAP](/img/sap-2/SL-creation.png)

Después de introducir el centro llegarás a la siguiente pantalla.

![Creación de almacén en SAP](/img/sap-2/SL-2.png)

<span class="highlight-text">Haz clic en **Nuevas entradas**. El cursor se situará en la columna **Almacén (Sloc)**, donde deberás introducir el código alfanumérico de 4 caracteres para cada almacén. En mi caso voy a crear tres almacenes basados en nuestro ejemplo: `RM01`, `FG01` y `QA01`.</span>

En la columna de descripción, introduce una breve explicación del uso de cada almacén.

![Creación de almacén en SAP](/img/sap-2/storage-location.png)

En este punto ya podrías guardar los cambios y finalizar el proceso. Sin embargo, quizá hayas visto dos opciones adicionales.

Una de ellas es el campo **Business System for MES**, que se utiliza cuando SAP está integrado con un sistema MES (Manufacturing Execution System). Este campo identifica el sistema externo responsable de la ejecución de la producción y de las actividades en planta. Para fines de aprendizaje o configuraciones básicas de la estructura empresarial, normalmente puede dejarse vacío.

La otra opción es **Dirección del almacén**, que permite asignar una dirección específica al almacén. Para hacerlo, selecciona el almacén marcando la casilla situada a la izquierda y luego haz doble clic en la opción **Dirección del almacén** del menú lateral izquierdo. Llegarás a esta pantalla.

![Creación de dirección de almacén en SAP](/img/sap-2/storage-location-address.png)

Haz clic en **Nuevas entradas**. El cursor se situará en la columna **N.º**. Introduce una clave alfanumérica de 3 caracteres y pulsa Enter. Aparecerá una ventana emergente donde podrás introducir la dirección y los datos de comunicación. Complétalos igual que hicimos para el centro y la sociedad financiera.

Cuando termines, vuelve a la pantalla donde añadimos los tres almacenes y pulsa **Guardar**. Eso es todo. El almacén habrá sido creado y quedará vinculado al centro correspondiente.

Si deseas consultar los almacenes asignados a un centro, modificarlos o eliminarlos, puedes utilizar el mismo t-code `OX09`. Introduce el código del centro y toda la información estará disponible allí. Si deseas eliminar un almacén, selecciónalo y pulsa el botón **Eliminar** situado en la parte superior. Aparecerá una ventana emergente indicando que las entradas serán eliminadas. Confirma con la marca verde y el almacén se eliminará.

<span class="highlight">Asignación de la planta a la sociedad</span>

Este es el último paso en la creación de la planta. Una vez que has creado la planta, debes asignarla a la sociedad. Este paso es bastante sencillo. <span class="highlight-text">Puedes usar el t-code `OX18` o bien seguir la ruta en el SAP Reference IMG: Estructura empresarial → Asignación → Logística general → Asignar planta a sociedad.</span>

Una vez que estés en esa pantalla, haz clic en el botón de **nuevas entradas** en la parte superior y serás dirigido a la siguiente pantalla.

![Asignación de planta en SAP](/img/sap-2/assign-plant.png)

Aquí simplemente introduce la sociedad y la planta y haz clic en el botón de guardar en la parte superior. Ahora ya hemos creado la planta, asignado los almacenes y también asignado la planta a la sociedad.
