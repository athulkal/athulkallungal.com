+++
title = 'Cómo crear una empresa y códigos de empresa en SAP'
date = 2026-06-02T00:00:00+02:00
draft = false
categories = ["SAP"]
showReadingTime = true
ShowShareButtons = false
+++

Entonces, la primera pregunta aquí es: ¿cuál es la diferencia entre empresa y sociedad (company code)?

Una empresa (Company) es una organización que puede considerarse como una entidad legal. El detalle más importante es que una empresa puede tener múltiples sociedades.

Para entenderlo mejor, veamos un ejemplo del mundo real.

Imaginemos Volkswagen Group. Es una empresa alemana pero tiene operaciones en varios países. Aunque todas sus subsidiarias pertenecen a la misma organización, cada país debe mantener sus propios registros contables y cumplir con la normativa fiscal y legal local.

| SAP COMPANY      | SAP COMP CODE | ENTIDAD LEGAL                        |
| ---------------- | ------------- | ------------------------------------ |
| Volkswagen Group | DE01          | Volkswagen AG (Alemania)             |
| Volkswagen Group | UK01          | Volkswagen Group UK Ltd              |
| Volkswagen Group | ES01          | Volkswagen Group España Distribución |

En este ejemplo, las tres entidades pertenecen al Volkswagen Group, pero cada código de sociedad mantiene sus propios datos contables y estados financieros.

Una **Company (empresa)** se utiliza principalmente para la consolidación de informes a nivel de grupo, mientras que un **Company Code (código de sociedad)** es la unidad organizativa más pequeña en SAP para la cual se puede llevar una contabilidad completa. Todas las transacciones contables, como facturas, pagos y asientos contables, se registran a nivel de company code.

Vamos a empezar viendo cómo crear una empresa en la pantalla de SAP.

<span class="highlight">
Creación de una empresa en SAP
</span>

<span class="space">Paso 1</span>

Debes iniciar sesión en tu servidor SAP. En mi caso, tengo un servidor educativo de SAP que pagué por 3 meses. Una vez que entres, verás esta pantalla.

![SAP screen](/img/sap-1/sap-screen.png)

Aquí, en la imagen, puedes ver que he marcado el cuadro de comandos (la pequeña caja rectangular). Ahí puedes escribir T-CODES (transaction codes) que te llevarán directamente a la pantalla que necesitas. Por ejemplo, si escribes `ox15`, irás directamente a la pantalla donde se crea la empresa.

La otra forma es navegar manualmente por el menú y buscar la función que necesitas.

<span class="highlight-text">La forma manual de crear una empresa es usando el SAP Reference IMG. Para ello debes escribir el t-code `spro` en el cuadro de comandos.</span> Te aparecerá una pantalla como esta.

![SAP spro screen](/img/sap-1/spro.png)

Después debes hacer clic en el botón SAP Reference IMG (el círculo rojo en la imagen).

![SAP enterprise structure screen](/img/sap-1/es-define.png)

Llegarás a esta pantalla. Desde ahí <span class="highlight-text">debes navegar a Enterprise Structure → Definition → Financial Accounting → Define Company</span> y luego hacer clic en el botón marcado en rojo en la imagen anterior. Esto te llevará a la pantalla de creación de empresa. Este es el método manual y <span class="highlight-text">la forma más sencilla sería usar el t-code `ox15`, que te lleva directamente a esta pantalla</span>.

![SAP company creation screen](/img/sap-1/new-entries.png)

<span style=" text-decoration: underline; font-weight: bold;">Paso 2</span>

Desde esta pantalla selecciona el botón “New Entries”. Como nota, verás muchas empresas porque es un servidor educativo y, como yo, hay muchas personas utilizándolo.

Cuando hagas clic en “New Entries” llegarás a esta pantalla.

![SAP company creation screen](/img/sap-1/comp-vkw.png)

<span style=" text-decoration: underline; font-weight: bold;">Paso 3</span>

La primera línea es la empresa - <span class="highlight-text">un código alfanumérico de 6 dígitos que asignas para identificar la empresa</span>. La segunda línea es el nombre de la empresa, y “Name 2” normalmente puedes dejarlo como está.

En la segunda parte rellenamos la dirección. Un punto importante es que el país es obligatorio. El país aparece como código, como puedes ver en mi ejemplo `DE` (Alemania), y el idioma `DE` (alemán), y la moneda `EUR`. Debes seleccionar todo esto desde las opciones disponibles.

Una vez completado, haz clic en el botón guardar en la parte superior (lo he marcado con un círculo rojo). Puede aparecer una ventana emergente como esta.

![SAP transport request](/img/sap-1/tr-req.png)

Aquí debes pulsar “Create Request” y dar una breve descripción de la transacción, como por ejemplo creación de empresa. El concepto de transport request es otro tema completamente distinto. <span class="highlight-text">Básicamente es un contenedor que almacena cambios de configuración para poder moverlos de un sistema a otro, por ejemplo de desarrollo a pruebas y de pruebas a producción.</span>

Pulsa el tick verde y, si todo está correcto, verás en la barra inferior que los datos se han guardado. ¡Felicidades! Has creado una empresa en SAP.

---

### ¿Cómo localizar la empresa creada?

Sí, puede que necesitemos localizar la empresa si queremos hacer cambios.

<span class="highlight-text">Si no estás en la pantalla principal de SAP, debes usar /n junto con el t-code, por ejemplo `/nox15`. Esto te llevará a la pantalla de creación de empresa.</span>

Ahora verás un botón llamado “Position”. Al hacer clic aparecerá una ventana emergente.

![SAP company search request](/img/sap-1/comp-search.png)

En esta ventana introduces el código alfanumérico de 6 dígitos de tu empresa. En mi caso es `VKWGR1`. Al pulsar el check verde, tu empresa aparecerá en la lista. Otra opción es usar los cuadros de búsqueda para filtrar por nombre de empresa.

![SAP company search request](/img/sap-1/comp-search-fil.png)

---

### Creación de un código de sociedad en SAP

<span class="highlight">
Creación de un Company Code en SAP
</span>

<span class="space">Paso 1</span>

Al igual que en la creación de empresa, podemos usar SAP Reference IMG o el t-code. <span class="highlight-text">El t-code para crear company code es `ox02`.</span> La otra opción es usar SPRO y navegar a <span class="highlight-text">Enterprise Structure → Definition → Financial Accounting → Define, Edit, Copy, Delete Company Code</span>.

Llegarás a la misma pantalla y desde ahí haces clic en “New Entries”.

![SAP company code creation](/img/sap-1/comp-code.png)

<span style=" text-decoration: underline; font-weight: bold;">Paso 2</span>

<span class="highlight-text">Aquí el company code es un código alfanumérico de 4 dígitos</span>. Elegí `VKWE` para representar Volkswagen España Distribution. El resto de datos es sencillo: nombre de empresa, ciudad, país, idioma y moneda. Luego pulsa guardar.

![SAP company code creation](/img/sap-1/comp-address.png)

<span style=" text-decoration: underline; font-weight: bold;">Paso 3</span>

Aquí debemos completar más información del company code. La primera línea es el título, normalmente “Company”. La segunda es el nombre completo. El campo de búsqueda ayuda a encontrar el company code más fácilmente.

En la parte de dirección, <span class="highlight-text">el país es obligatorio y sin él no se puede continuar</span>.

La parte de comunicación puedes rellenarla con datos de ejemplo para aprendizaje.

Después haz clic en el tick verde y guarda la entrada. Se generará un transport request y vuelves a confirmar. Verás el mensaje de guardado en la barra de estado.

---

### ¿Cómo encontrar el company code creado?

El proceso es el mismo que con la empresa, usando el t-code `ox02`. Desde la lista usa “Position” o la búsqueda para encontrar tu company code.

---

### Asignación de Company a Company Code

Ahora puede surgir la pregunta: ¿dónde está la relación entre ambos?

Esto se hace mediante la asignación de company code a company. <span class="highlight-text">Se utiliza el t-code `ox16`</span> o la ruta:

<span class="highlight-text">Enterprise Structure → Assignment → Financial Accounting → Assign Company Code to Company</span>.

![SAP company code creation](/img/sap-1/comp-assignment.png)

Usa “Position” para localizar el company code y, en la columna de company, introduce el código de la empresa (6 dígitos). Guarda los cambios.

En mi caso apareció una advertencia indicando que la empresa y el company code tenían monedas diferentes, ya que no asigné moneda a la empresa (esto lo hice porque Volkswagen Group opera en varios países con diferentes monedas). Simplemente pulsé Enter y se guardó correctamente.

---

Y con esto hemos completado la creación de empresa y company code en SAP.
