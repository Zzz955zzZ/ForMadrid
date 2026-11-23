# Preguntas probables y respuestas · ForMadrid

Respuestas cortas (20-40 s). Primero la frase en negrita; después, si preguntan más, el detalle. Las cifras salen de `Resultados/` (ver `Resultados/trazabilidad.md`).

---

## Sobre los datos

**1. ¿Qué pasa con los afiliados «sin municipio asignado»?**
**Son el 16,7 % de los afiliados por residencia en 2025 (14,1 % en 2021); lo corregimos y lo comprobamos.**
La Seguridad Social no asigna municipio a una parte de los afiliados y esa parte crece cada año. Por eso: (1) el índice es relativo, compara municipios entre sí; (2) corregimos proporcionalmente cada año dividiendo por (1 − % sin asignar); con esa corrección el cociente empleo/residentes de la Comunidad es estable (0,99) en vez de subir artificialmente de 1,15 a 1,18; (3) repetimos el cálculo con otro denominador. En el empleo por centro de trabajo el problema es mínimo (0,8 %).

**2. ¿Por qué ese denominador? ¿No cambia el resultado si usáis otro?**
**No: con la población del INE de 15 a 64 años el ranking es prácticamente el mismo (Spearman 0,985; 0,99 en los municipios grandes).**
De los 20 municipios con mayor desajuste coinciden entre 16 y 19 según el año. Usamos 15-64 porque el INE publica grupos de cinco años; solo hay población para 2021 y 2025, por eso es una prueba de robustez y no el denominador principal.

**3. Los cursos: ¿cómo comparáis la oferta si muchos no tienen municipio?**
**Es una capa complementaria, no forma parte del índice, y lo decimos en la diapositiva.**
De 7.628 cursos, 2.954 son de teleformación (sin lugar) y, de los presenciales, el 54 % no trae municipio. Solo podemos localizar 2.156 cursos en 43 municipios. Con esos, la oferta es de 4,0 cursos por 1.000 parados en los municipios de mayor desajuste frente a 7,7 en el resto: es una señal, no una conclusión. Si la Comunidad publicara el municipio de todos los cursos, la herramienta lo incorporaría directamente.

**4. ¿Por qué paro registrado y no la EPA?**
**Porque la EPA no da datos por municipio.** El paro registrado (31 de marzo) sí, y por sector. Sabemos que no es lo mismo que el paro EPA y que marzo tiene estacionalidad; usamos siempre el mismo mes para comparar años.

**5. ¿Habéis encontrado problemas en los datos?**
**Sí, y los documentamos todos.** Además del 999: el empleo por centro de trabajo tiene valores ocultos («-») hasta 2020 y desde diciembre de 2021 viene redondeado a múltiplos de 5 por confidencialidad; los datos de paro no traen la combinación «total nacionalidades + total sectores»; el contrato temporal falta en 2014-2015. El script de limpieza comprueba todo esto y se para si algo no cuadra.

**6. ¿Los «-» los tratáis como ceros?**
**No, son valores ocultos, no ceros.** Para los totales usamos la fila Total, que está completa; el desglose sectorial de 2020 no lo usamos.

## Sobre el método

**7. ¿Cómo se calcula el índice? ¿Por qué esos pesos?**
**Tres componentes con el mismo peso: déficit de empleo local, presión de paro y desajuste sectorial.** Cada uno se estandariza entre los 179 municipios y el índice es la media. Pesos iguales porque no hay una razón objetiva para preferir uno; los componentes están poco correlacionados entre sí (miden cosas distintas). En el repositorio se pueden cambiar los pesos en una línea.

**8. ¿Qué es el «desajuste sectorial»?**
**El porcentaje de parados que tendría que cambiar de sector para que los sectores del paro se parezcan a los del empleo del municipio** (índice de disimilitud de Duncan). Usamos 4 sectores (agricultura, industria, construcción, servicios), así que es una cota inferior.

**9. Villarejo de Salvanés está en el puesto 25, ¿por qué no el 1?**
**Porque el ranking completo incluye municipios muy pequeños.** Los 74 municipios con menos de 1.000 afiliados residentes (1,5 % del paro) tienen cifras tan bajas que su índice es inestable; los mostramos con fiabilidad baja y el análisis principal se centra en los 103 municipios con fiabilidad alta, que tienen el 98,5 % del paro. Entre esos, Villarejo es de los primeros.

**10. ¿El cociente empleo/residentes mide los desplazamientos al trabajo?**
**No, es un saldo, no un flujo origen-destino.** Indica si un municipio tiene más o menos empleo que trabajadores residentes, no a dónde van. La matriz origen-destino del INE sería una ampliación natural.

**11. ¿Qué tipos de municipios salen en la tipología?**
**Cinco tipos más los municipios pequeños**: polos de empleo cualificado (Madrid, Alcobendas…), grandes municipios metropolitanos de cualificación media (Móstoles, Fuenlabrada…), residenciales cualificados, desajuste sectorial (Humanes, Algete…) y paro alto con empleo poco cualificado (Aranjuez, San Martín de Valdeiglesias…). La separación entre tipos es moderada (silueta 0,24): la tipología es orientativa.

**12. ¿Y la COVID?**
**2020 está fuera y 2021 está marcado como atípico.** Las tendencias se leen de 2021 a 2025 sabiendo que 2021 parte de un paro alto; por eso comparamos la caída entre tipos de municipio, no la cifra absoluta.

## Sobre impacto y viabilidad

**13. ¿Quién lo usaría y para qué?**
**Ayuntamientos y centros de formación.** Un ayuntamiento ve su puesto, si su problema es falta de empleo local o de sector, y qué familias de cursos tiene cerca; un centro de FP ve dónde hay parados de sectores sin empleo local y poca oferta presencial. También sirve a la Comunidad para planificar la convocatoria de cursos.

**14. ¿Es viable mantenerlo?**
**Sí: solo usa datos abiertos y la API CKAN, sin claves ni coste.** Un script descarga los datos (verificado: los ficheros descargados son idénticos byte a byte a los usados) y el resto se ejecuta en un minuto. Cada año basta con volver a ejecutarlo.

**15. ¿Qué tiene de original?**
**Cruzar empleo, residencia, paro, perfil y oferta formativa a escala municipal, y ser honestos con los límites del dato.** Detectar que el 16,7 % de afiliados sin municipio crea una tendencia falsa, corregirla y comprobarla con otra fuente cambia la lectura de los datos; y la herramienta lo convierte en una decisión concreta: dónde abrir cursos y de qué sector.

**16. ¿Habéis usado IA?**
**Sí, como asistente de programación y redacción, como permiten las bases.** Las decisiones de método, la revisión de los datos y los resultados son del equipo, y todo es reproducible desde el código.

**17. ¿Dónde está el código?**
**En GitHub: https://github.com/Zzz955zzZ/ForMadrid** (README en español, datos, scripts y la herramienta).
