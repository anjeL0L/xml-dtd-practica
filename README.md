&#x20;Práctica XML y DTD



&#x20;Objetivo

Aprender a diseñar documentos XML a partir de información no estructurada, definir DTD internos y externos, y gestionar versiones con Git.



Ejercicio 1: Pedido

\### Modelo propuesto

Se desglosó el pedido en destinatario, artículo, dirección (calle, número, interior) y fecha.

\### Decisiones de diseño

Se decidió separar la dirección en etiquetas individuales para facilitar la búsqueda específica de datos y su posterior procesamiento.



Ejercicio 2: Nota

\### DTD externo

Se definió un archivo `nota.dtd` y se vinculó en el XML con `SYSTEM`.

\### DTD interno

Se incluyeron las reglas `<!ELEMENT...>` directamente en la cabecera `<!DOCTYPE...>` del XML.

\### Pruebas realizadas

Se verificó que el DTD rechaza etiquetas no definidas (como `<telefono>`), etiquetas con nombres incorrectos (como `<destinatario>` en vez de `<para>`) y desorden en los elementos.



Ejercicio 3: Matrícula

\### Modelo

Se estructuró la información personal, incluyendo domicilios y datos de pago.

\### Cardinalidad

Se utilizó el operador `+` para asegurar que haya "uno o más" domicilios.

\### Restricción del atributo tipo

Se usó `<!ATTLIST domicilio tipo (familiar|habitual) #REQUIRED>` para restringir los valores y hacerlo obligatorio.

\### DTD externo e interno

Se crearon ambas versiones asegurando que el documento fuera válido.

\### Pruebas realizadas

Se comprobó que al quitar un domicilio o poner un tipo inválido (como `temporal`), el documento no superaba la validación.



Conclusion

1\. \*\*¿Cuál es la diferencia entre XML bien formado y XML válido?\*\*

Un XML bien formado cumple la sintaxis básica (etiquetas cerradas, un solo elemento raíz, etc.). Un XML válido, además, cumple estrictamente las reglas de estructura definidas en un DTD.

2\. \*\*¿Qué función cumple un DTD?\*\*

Define la estructura legal, los elementos, atributos y el orden que puede contener un documento XML.

3\. \*\*¿Qué diferencia existe entre DTD interno y externo?\*\*

El DTD interno va escrito dentro de la cabecera del mismo archivo XML; el externo es un archivo independiente (`.dtd`) que puede ser reutilizado por muchos XML.

4\. \*\*¿Cómo se expresa cardinalidad en DTD?\*\*

Con `?` (0 o 1 aparición), `\*` (0 o más apariciones), y `+` (1 o más apariciones).

5\. \*\*¿Cómo puede restringirse un atributo a determinados valores?\*\*

Usando la declaración `<!ATTLIST elemento atributo (valor1|valor2) #REQUIRED>`.

6\. \*\*¿Qué ventaja proporcionó Git durante las pruebas?\*\*

Permitió realizar pruebas destructivas (romper el código) y luego restaurar la versión funcional de forma segura y rápida.

7\. \*\*¿Qué utilidad tuvieron git diff y git restore?\*\*

`git diff` sirvió para ver exactamente qué cambios se habían hecho antes de guardarlos. `git restore` sirvió para deshacer los errores de las pruebas negativas y recuperar el archivo sano.

8\. \*\*¿Qué ventaja proporcionó una rama para desarrollar una solución alternativa?\*\*

Permitió trabajar en la versión del DTD interno sin alterar ni poner en riesgo el código funcional que ya existía en la rama principal.

1.¿Cuál es la diferencia entre XML bien formado y XML válido?

Un documento XML está "bien formado" cuando cumple las reglas sintácticas básicas, como tener un solo elemento raíz, etiquetas correctamente cerradas y un anidamiento correcto. Un documento XML es "válido" cuando, además de estar bien formado, cumple con todas las reglas y restricciones definidas en su DTD.  

2.¿Qué función cumple un DTD?

Cumple la función de definir la estructura esperada del documento XML para poder validarlo. Permite establecer qué elementos pueden existir, el orden de los mismos, las restricciones de los atributos y si contienen texto (#PCDATA) u otros elementos anidados. 

3.¿Qué diferencia existe entre DTD interno y externo?

Un DTD externo es un archivo adicional que se asocia al XML (usando la palabra SYSTEM) y es conveniente cuando se necesita validar muchos documentos con las mismas reglas. Un DTD interno se ubica dentro del mismo archivo XML y es conveniente cuando la validación aplica a un único documento.   

4.¿Cómo se expresa cardinalidad en DTD?

Se expresa utilizando símbolos específicos:   

\* indica que el elemento puede aparecer cero o una vez.   

\* indica que el elemento puede aparecer cero o más veces.   

\* indica que el elemento debe aparecer uno o más veces.   

5.¿Cómo puede restringirse un atributo a determinados valores?

Se restringe utilizando la instrucción <!ATTLIST ...> y definiendo una enumeración con los valores permitidos (por ejemplo, para que solo admita familiar o habitual).   

6.¿Qué ventaja proporcionó Git durante las pruebas?

Permitió realizar pruebas negativas (introducir errores de forma temporal para comprobar que la validación fallaba) con la seguridad de poder registrar los cambios y regresar al estado original fácilmente.   

7.¿Qué utilidad tuvieron git diff y git restore?

git diff: fue útil para observar los cambios exactos que se habían realizado en el archivo modificado.   

git restore: fue útil para descartar esos errores temporales y restaurar el documento válido original.   

8.¿Qué ventaja proporcionó una rama para desarrollar una solución alternativa?

Permitió crear un entorno aislado para desarrollar la variante del DTD interno sin afectar el código de la rama principal. Una vez completada y probada la alternativa, permitió integrarla de manera ordenada usando el comando merge.

