**critical-edition**

* `critical-edition.sty` es un paquete basado en la extracción y reestructuración de fragmentos del código del paquete `reledmac.sty` de Maïeul Rouquette, que se centra en un sistema o motor "minimalista" que permite trabajar ediciones críticas que no precisen entornos como `\ledgroup` en reledmac, y para ello el paquete permite gestionar un entorno numerado y tres tipos de footnotes estáticas para gestionar tipos diferentes de información:
**1-** *Testimonium*, Testimonios/Witnesses (un tipo de apunte que indica los testimonios de los que proviene el fragmento que se está trabajando) = `\footT{}`;
**2-** *Apparatus criticus*, Aparato crítico/Critical apparatus (un tipo de apunte que indica las variantes textuales que hay entre el texto base o fijado y el resto de testimonios colacionados): `\footA{}{}`;
**3-** *Explicatio*, Explicación/Explanation (un tipo de apunto que indica diferentes tipos de información; en este caso funcionará como las convencionales `\footnote{}`): `\footE{}`.
