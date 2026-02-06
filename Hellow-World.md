# Tarea: Cliente–Servidor con ZeroC Ice y Medición de Atributos de Calidad

## Objetivo

El objetivo de esta tarea es **recordar y reforzar el uso de ZeroC Ice** para la construcción de sistemas cliente–servidor, así como **analizar y medir atributos de calidad**, particularmente relacionados con **performance y concurrencia**, en un escenario de múltiples clientes realizando solicitudes simultáneas.

La actividad también busca que los estudiantes practiquen **despliegue distribuido**, configuración de endpoints y observación del comportamiento del servidor bajo carga concurrente.

---

## Trabajo en parejas

La tarea se debe realizar **en parejas**.

Cada pareja deberá analizar, modificar y desplegar el código base proporcionado en el repositorio:

```
https://github.com/Ingesoft-IV/ICE-HelloWorld.git
```

---

## Parte 1: Familiarización con el código y despliegue inicial

1. Analicen el código del ejemplo **HelloWorld** basado en ZeroC Ice.
2. Para el despliegue inicial:

   * Un estudiante asumirá el **rol de servidor**.
   * El otro estudiante asumirá el **rol de cliente**.
3. Seleccionen **tres máquinas diferentes del laboratorio**:

   * 1 máquina para el **server**
   * 2 máquinas para **clients**
4. Cada estudiante debe modificar los archivos `.config` del cliente o servidor:

   * Configurar **host y puerto** de forma consistente entre ambos.
   * **No repetir** host/puerto con otras parejas.
5. Compilen y ejecuten:

   * El **server** en una máquina.
   * El **client** en las otras dos máquinas.
6. Ambos estudiantes deben enviar **muchos mensajes al servidor al mismo tiempo**, observando:

   * El comportamiento del servidor.
   * La atención concurrente de solicitudes.

---

## Parte 2: Modificación funcional del sistema

A partir del código base del *HelloWorld*, realicen las siguientes modificaciones.

### 1. Cliente interactivo por consola

Modificar el cliente para que:

* En lugar de enviar un solo mensaje, **lea mensajes desde la consola en un ciclo**.

* Cada mensaje debe ser prefijado con:

  ```
  username:hostname:mensaje
  ```

  Donde:

  * `username` corresponde al usuario logueado (`whoami`)
  * `hostname` corresponde al nombre de la máquina cliente

* El servidor debe retornar un resultado que será **impreso por el cliente**.

* El ciclo se repite hasta que el usuario digite:

```
exit
```

---

### 2. Comportamiento del servidor según el mensaje

El servidor debe analizar el contenido del mensaje recibido (sin contar el prefijo `username:hostname:`) y comportarse de la siguiente manera:

#### 2a. Número entero positivo

* Si el mensaje es un **número entero positivo** `n`:

  * El servidor debe imprimir en su consola:

    * La **serie de Fibonacci(n)**.
    * Precedida por el `username/hostname` del cliente que envió el mensaje.
  * El servidor debe retornar al cliente:

    * Los **factores primos** de `n`.

---

#### 2b. Comando `listifs`

* Si el mensaje inicia con:

```
listifs
```

* El servidor debe:

  * Imprimir en su consola las **interfaces lógicas de red** configuradas en el servidor.
  * Preceder la salida con el `username/hostname` del cliente.
  * Retornar dicha información al cliente.

---

#### 2c. Comando `listports <IPv4>`

* Si el mensaje inicia con:

```
listports <dirección IPv4>
```

* El servidor debe:

  * Imprimir en su consola los **puertos y servicios abiertos** en la dirección IPv4 indicada.
  * Preceder la salida con el `username/hostname` del cliente.
  * Retornar dicha información al cliente.

---

#### 2d. Comando `!<comando>`

* Si el mensaje inicia con:

```
!<string>
```

* El servidor debe:

  * Ejecutar el `<string>` como un comando del sistema operativo.
  * Imprimir en su consola el resultado, precedido por el `username/hostname` del cliente.
  * Retornar el resultado al cliente.

> ⚠️ **Nota:** Este punto es intencionalmente riesgoso y debe servir para reflexionar sobre **seguridad y confiabilidad** como atributos de calidad.

---

### 3. Terminación

* El cliente continúa enviando mensajes hasta que el usuario escriba:

```
exit
```

---

## Parte 3: Ejecución concurrente y medición de atributos de calidad

Con el código modificado:

1. Repitan el **deployment distribuido**:

   * 1 servidor
   * 2 clientes ejecutándose simultáneamente
2. Generen múltiples solicitudes concurrentes desde los clientes.
3. Realicen **mediciones de atributos de calidad relacionados con performance**, por ejemplo:

   * Tiempo de respuesta.
   * Comportamiento bajo carga concurrente.
   * Uso de CPU/memoria (si es posible).
4. Reflexionen sobre:

   * Escalabilidad.
   * Concurrencia.
   * Posibles cuellos de botella.

---

## Entrega

Deben subir un archivo con el siguiente nombre:

```
helloworld-ciclo-kbd-NNAA1-NNAA2.zip
```

Donde:

* `NNAA1` y `NNAA2` corresponden a **NombreApellido** de cada integrante de la pareja.

El archivo `.zip` debe contener:

```
helloworld-ciclo-kbd-NNAA1-NNAA2/
└── (estructura completa del código, partiendo de una copia del helloworld original)
```

---

## Organización en el laboratorio

* En el laboratorio hay **30 PCs**.
* Cada estudiante debe:

  * Crear un **subdirectorio con su nombre**.
  * **Duplicar** el folder `helloworld` dentro de ese subdirectorio.
* Si hay más de 30 estudiantes:

  * Algunas parejas compartirán máquinas.
  * Cada uno debe usar su propio subdirectorio.
  * Se deben usar **puertos distintos** en los archivos de configuración.

---

## Consideraciones finales

* La tarea acepta **únicamente archivos `.zip`**.
* El **monitor sustentará la tarea** durante la monitoría.
* Se evaluará:

  * Correcto uso de ZeroC Ice.
  * Funcionamiento concurrente.
  * Claridad del código.
  * Comprensión de los atributos de calidad involucrados.

