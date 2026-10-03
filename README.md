# Ayuntamiento de Usagre · propuesta de web «Puerta abierta»

Maqueta de la web municipal del **Ayuntamiento de Usagre** (Badajoz, 1.698 habitantes), hecha con la plantilla `plantilla-ayuntamiento-puerta-abierta-web` y con su información real. **No es la web oficial**:
- lleva en todas las páginas la banda «Propuesta de diseño… no es la web oficial»;
- lleva `noindex, nofollow` en todas las páginas.

Publicada en <https://alvarotaiagu.github.io/ayuntamiento-usagre-web/> (con `?revision`, el mando de la reunión).

```bash
npm install                        # Playwright y axe-core (solo para los scripts)
node scripts/aplicar.mjs           # genera la web desde los datos
node scripts/servir.mjs 4231       # http://127.0.0.1:4231/  ·  con ?revision, el mando
node scripts/verificar.mjs         # todas las comprobaciones
```

Los datos, con su fuente y la fecha de cada consulta (3 de octubre de 2026), están en `../ayuntamiento-usagre-bocetos/DATOS.md`, fuera de esta carpeta porque esta se publica. En la misma carpeta están el inventario de su web actual (`INVENTARIO.md`), los errores encontrados (`ERRORES.md`) y las copias de cada fuente. El generador de `municipio.json` es `../ayuntamiento-usagre-bocetos/_scripts/municipio.mjs`.

---

## El concepto

Es la plantilla «Puerta abierta»: una puerta de medio punto encalada que da paso a lo que pasa hoy en el pueblo. En Usagre el arco enmarca el **puente romano de dos arcos**, el mismo que lleva su escudo bajo la cruz de Santiago.

- **Responde sin hacer buscar.** El panel «Hoy en Usagre» dice si el Ayuntamiento está abierto, qué es lo próximo de la agenda y cuál es el último aviso.
- **Se mantiene viva sin publicar a diario.** Su web lleva sin una noticia desde febrero de 2022, mientras su Facebook publica varias veces por semana. Aquí:
  - el tablón de la sede entra por script;
  - las fiestas de fecha fija llenan la agenda;
  - los avisos y la agenda se pueden escribir en una hoja de cálculo.
- **Una sola web** donde ahora hay tres sitios desconectados: la web, la de turismo y un portal de transparencia abandonado.

La receta del reskin está en [RESKIN.md](RESKIN.md) y la explicación de la plantilla, en su propio README.

El código es el de la plantilla en su commit **d297713** (3 de octubre de 2026). Verificación: `node scripts/verificar.mjs --capturas` → **88 de 88 comprobaciones**, incluida la prueba de reskin a Segura de León sin restos de Usagre.

## Qué hay en cada página

| Página | Qué tiene |
|---|---|
| Inicio | Hoy en Usagre, trámites por temas, tablón (avisos y sede), lo que viene y lo que pasó, quién se ocupa de qué, el año en Usagre |
| Trámites | Buscador sobre los **111 trámites** de su sede (comprobados uno a uno), por momentos y por temas |
| El Ayuntamiento | Alcaldía (saluda de ejemplo), pleno de 9 concejales en hemiciclo (6 PSOE, 3 PP), concejalías y quién se ocupa de qué |
| Avisos y tablón | Avisos reales de septiembre y octubre de 2026 y los anuncios de su sede sin datos personales |
| Noticias, Agenda | 7 noticias de su Facebook y de Campitur; la Agenda de Otoño 2026 |
| Teléfonos y servicios | Listín contrastado con fuentes oficiales y **las instalaciones municipales**, con el gimnasio y sus precios, la piscina, los parques, el mercado y los apartamentos rurales con tarifas y reserva |
| El pueblo | Qué ver (7 lugares con foto), «Urbs Sacra», historia, patrimonio, fiestas, gastronomía, personajes y rutas |
| Contacto, legal | Dirección, mapa bajo clic, datos de la entidad (NIF, DIR3 para FACe), aviso legal, privacidad, cookies y declaración de accesibilidad |

## Qué se añadió a la plantilla por Usagre

Su web tiene información útil y vigente que la plantilla no sabía enseñar: las **instalaciones municipales** (con dirección, horario y precio) y un **alojamiento municipal** con tarifas y reserva en línea. Se añadió como sección opcional y genérica, `instalaciones` en `municipio.json`: grupos de fichas que salen en «Teléfonos y servicios» y desaparecen si el campo está vacío. Está documentada en RESKIN.md y se prueba con datos de muestra en `pruebas/opcionales.json`.

Además usa dos secciones opcionales que la plantilla ganó el mismo día para Segura de León: `pueblo.establecimientos` («Dónde comer y dormir») y `canal_avisos`.

## Decisiones

- **El color de marca es el sinople** de la bordura del escudo, la que lleva «VRBS SACRA». Es el esmalte con más área (34,6 %; plata, 22,6 %; oro, 22,2 %; gules, 14,7 %; azur, 6 %) y el verde de su bandera, así que no hizo falta forzarlo. El oro va solo en filetes y en la marca de «hoy»; el gules, en las alertas. Sale el mismo hex que en Ribera del Fresno (#008F4C, la paleta normalizada de los escudos de Commons). Con `?revision` se pueden probar el azur de la rivera y el almagre.
- **El lema es «Suena bien»**, el que usa el Ayuntamiento desde 2021 en su web y en sus carteles. Ninguna fuente explica el «suena»; si no lo quieren, se quita con `"lema": null`.
- **La foto de la portada** es el puente romano, de Wikimedia Commons (CC BY 4.0). Se puede publicar sin pedir permiso. Las de «Qué ver» son de la sesión de 2025 de su web de turismo y solo valen para enseñárselas a ellos.
- **El horario de atención sale como «Ejemplo».** Su web da dos: «lunes a viernes, de 8:00 a 15:00» (turismo, 2022) y «de 8:30 a 3:00» (guía local, 2018). Se enseña el más reciente, con la etiqueta.
- **Correo**: ayuntamiento@usagre.es, el de la sede, la Plataforma de Contratación y su Facebook. Su web usa info@ayuntamientodeusagre.com.
- **No hay Instagram** del Ayuntamiento. Se enlazan Facebook, Usagre TV (YouTube) y Bandomóvil «Usagre Informa».
- **Tablón:** sale de una única lectura de su sede (3 de octubre), porque el `robots.txt` de la sede prohíbe leerla a los robots. Se excluyen las relaciones nominales, las listas de admitidos y el tribunal (una lista revela discapacidad). La lectura automática se activa cuando el Ayuntamiento la autorice (`"tablon_autorizado": true`).
- **Bares y alojamientos privados** salen en «El pueblo → Dónde comer y dormir» con la lista de su web de turismo de 2022 (más reciente que la guía de 2018, con la que no coincide) y la fuente a la vista. Las tiendas no salen.
- **Bandomóvil** sale como canal de avisos, arriba de «Avisos» y en «Contacto»: que lo sigan usando.

### Erratas de su web, corregidas al usar sus textos
- «danto muestra» → «dando muestra».
- «el pico Calvo (59, mts.)» → 597 m (no se publica la cifra).
- «respostería» → «repostería».
- «leos niños» → «los niños».
- «Usagre ceunta con» → «cuenta».
- «FESTIVAL MEDIVAL» → «Medieval».
- «RUTA DE LOS ORTELANOS» → «Hortelanos».
- «afluentes del Montanchez» (Diputación) → Matachel.

### Datos que se contradicen
- **Corporación**: su web enseña la de 2019. Se usa la del BOP del 16/12/2025.
- **Consultorio**: su web da «Centro de Salud de Usagre 924 280 805»; el SES, cita 924 585 309 y urgencias 924 101 243, en C/ Pepe Larrey, 26 (antes C/ Chavero). Se usa el SES.
- **Biblioteca**: 924 585 299 (web, turismo y Ministerio) o 697 973 922 (guía local). Se usa el del Ministerio.
- **Fiestas del Cristo**: «del 13 al 16 de septiembre» (web, Diputación) y «13-18» (cartel de 2022). El programa de 2026 fue del 2 al 16, con lo grande del 13 al 16. Se usa «del 13 al 16; la procesión, el 14».
- **Fiesta principal**: un texto de Turismo de la Diputación (julio de 2026) dice que es el 25 de julio. No se usa.
- **Siglo XVI**: 625 vecinos (su web) o 752 en 1552 (Diputación). Se usa su web.
- **Convento concepcionista**: fundado en 1514 (su web) o en 1509 (Diputación). No se publica el año.
- **Superficie**: 240 km² o 291,20 km², en la misma ficha de la Diputación. No se publica.
- **Blasón**: «puente de un arco» en la transcripción de Wikipedia; dos arcos en el dibujo del Ayuntamiento, en el SVG y en el puente real.

## Créditos de las fotos

| Foto | Autor | Licencia |
|---|---|---|
| El puente romano (portada y «Qué ver») | Gonzalo 11789 (Wikimedia Commons) | CC BY 4.0 |
| Pilar del Carmen, fuente de la plaza, portada mudéjar de la iglesia, ermita del Cristo, Presa Honda, La Luná | web de turismo del Ayuntamiento (2025) | **Solo para la propuesta**: hace falta su autorización |
| Escudo | Erlenmeyer (Wikimedia Commons) | CC BY-SA 4.0 |

## Pendientes para el Ayuntamiento

- [ ] **Horario de atención** al público (sale como «Ejemplo»).
- [ ] **Permiso para las fotos** de su web de turismo, o fotos propias de la plaza y las fiestas.
- [ ] El **saluda** de la alcaldesa: el texto actual es de ejemplo.
- [ ] Cómo escriben **«Jenifer/Jennifer» Calvete** y **«Pilar Jessica/Jesica» Ortiz** (las fuentes oficiales lo escriben de las dos maneras).
- [ ] Confirmar que el grupo del PP sigue igual (sus cambios no siempre salen en el BOP).
- [ ] Teléfono de la **Policía Local** y de la **farmacia**.
- [ ] **Orden definitiva del escudo** y de la bandera (el DOE de 2009 solo publica la aprobación inicial).
- [ ] Si siguen usando el lema **«Suena bien»**.
- [ ] Confirmar la lista de **bares y alojamientos** (es de 2022) y el **horario de autobuses** (el de su web es de 2018).
- [ ] **Autorización para leer su tablón** de la sede de forma automática.
- [ ] Los **plenos**: no se graban ni se publican las actas en la web. Si lo hacen, hay sitio para enlazarlos.
