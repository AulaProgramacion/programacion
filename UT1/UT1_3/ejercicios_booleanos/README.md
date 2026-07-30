# Ejercicios expresiones booleanas simples

**1.** Teniendo `esMayorDeEdad` y `tieneAutorizacionPadres`: "Denegaremos el acceso a quienes no sean mayores de edad ni tengan autorización de sus padres."

<details>
<summary>Solución</summary>

```java
!esMayorDeEdad && !tieneAutorizacionPadres
```
</details>

**2.** Teniendo `nota`: "Mostrar 'error' si la nota es menor que cero y si la nota es mayor que 10"

<details>
<summary>Solución</summary>

```java
nota < 0 || nota > 10
```
</details>

**3.** Teniendo `esFestivo` y `estaDeVacaciones`: "Responder correos salvo que sea festivo o esté de vacaciones."

<details>
<summary>Solución</summary>

```java
!esFestivo && !estaDeVacaciones
```
</details>

**4.** Teniendo `tarjetaCaducada` y `pinIncorrecto`: "No se permite pagar a quienes tengan la tarjeta caducada o el PIN incorrecto."

<details>
<summary>Solución</summary>

```java
tarjetaCaducada || pinIncorrecto
```
</details>

**5.** Teniendo `temperatura`: "Encender calefacción cuando la temperatura no esté entre 18 y 24 grados."

<details>
<summary>Solución</summary>

```java
temperatura < 18 || temperatura > 24
```
</details>

**6.** Teniendo `esVIP`, `esSocio` y `tieneCupon`: "Aplicar descuento a quienes sean VIP o socios, y además tengan cupón."

<details>
<summary>Solución</summary>

```java
(esVIP || esSocio) && tieneCupon
```
</details>

**7.** Teniendo `tieneLicencia` y `esEmpleado`: "Prohibir entrada a quien no tenga licencia y tampoco sea empleado."

<details>
<summary>Solución</summary>

```java
!tieneLicencia && !esEmpleado
```
</details>

**8.** Teniendo `esLunes` y `hayVacaciones`: "Abrir la oficina todos los días excepto los lunes y los días de vacaciones."

<details>
<summary>Solución</summary>

```java
!esLunes || !hayVacaciones
```
</details>

**9.** Teniendo `stock` y `pedidoUrgente`: "Rechazar pedido cuando no hay stock, salvo que sea urgente."

<details>
<summary>Solución</summary>

```java
stock <= 0 && !pedidoUrgente
```
</details>

**10.** Teniendo `edad`: "Denegar acceso a menores de 16 años y mayores de 70 años."

<details>
<summary>Solución</summary>

```java
edad < 16 || edad > 70
```
</details>
