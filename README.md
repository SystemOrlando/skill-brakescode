# skill-brakescode

El estándar de casa de **brakescode** para diseño y desarrollo web, empaquetado como plugin de Claude Code.

No es una guía de estilo para leer una vez. Es una skill que Claude carga automáticamente cuando trabajas en cualquier interfaz web, y que decide por ti tipografía, color, motion, patrones de interacción y disciplina de build según criterios medidos, no según lo que le parezca en el momento.

---

## Instalación

Necesitas acceso de lectura al repo (pídeselo a Orlando si no lo tienes) y `git` configurado con tus credenciales de GitHub.

El repo trae manifiestos para varias herramientas. **El contenido es exactamente el mismo** — lo único que cambia es el archivo que cada una lee para descubrirlo.

| Herramienta | Manifiesto | Estado |
|---|---|---|
| Claude Code | `.claude-plugin/` | Verificado |
| Cursor | `.cursor-plugin/` | Formato correcto, sin probar |
| Kimi | `.kimi-plugin/` | Formato correcto, sin probar |
| Otras | `.plugin/` | Genérico |

### Claude Code

```
/plugin marketplace add SystemOrlando/skill-brakescode
```

```
/plugin install skill-brakescode@brakescode
```

Reinicia Claude Code. Listo.

### Cursor, Kimi y otras

Instala el plugin desde el repo con el mecanismo que use tu herramienta; leerá su propio manifiesto automáticamente.

Si tu herramienta todavía no soporta plugins, **la skill funciona igual**: son archivos Markdown y nada más. Clona el repo y apunta tu herramienta a `skills/skill-brakescode/SKILL.md` como regla, contexto o instrucción de proyecto — no hay código que ejecutar, ni dependencias, ni build.

```bash
git clone https://github.com/SystemOrlando/skill-brakescode.git
```

Ese es el punto de tenerla en Markdown plano: no queda amarrada a ninguna herramienta.

### Comprobar que quedó

Corre `/plugin` y verifica que `skill-brakescode` aparece como instalado. O simplemente pídele algo de web —"hazme un hero para la landing"— y fíjate en que arranque leyendo la skill.

### Si falla la instalación

Casi siempre es acceso al repo. Comprueba que puedes clonarlo:

```bash
gh repo view SystemOrlando/skill-brakescode
```

Si eso da error, no eres colaborador todavía. Si funciona pero el plugin no instala, autentica el CLI:

```bash
gh auth login
```

---

## Qué contiene

**`skills/skill-brakescode/SKILL.md`** — el criterio y las decisiones. Es lo único que se carga siempre.

El criterio central:

> **Una idea, llevada más lejos de lo cómodo, hasta las partes que nadie diseña.**

Con cuatro tests que se aplican antes de dar algo por terminado: **spine**, **loud-once**, **8px** y **locked-out**.

Las referencias se cargan solo cuando hacen falta:

| Archivo | Cuándo se usa |
|---|---|
| `references/typography.md` | Elegir tipografías, tamaños, pesos, tracking |
| `references/color.md` | Armar paleta, fondos, tintas, contraste |
| `references/motion.md` | Cualquier animación, transición, easing, loader |
| `references/patterns.md` | 15 patrones de interacción con implementación |
| `references/casebook.md` | El registro medido, sitio por sitio |

---

## De dónde salen los valores

No están inventados ni copiados de un blog. Salen de medir cinco sitios en vivo el **2026-09-05**, leyendo el DOM real con `getComputedStyle`:

[by-kin.com](https://by-kin.com) · [species-in-pieces.com](http://species-in-pieces.com) · [iventions.com](https://iventions.com) · [minhpham.design](https://minhpham.design) · [simplychocolate.dk](https://simplychocolate.dk)

El `casebook.md` separa tres niveles de confianza y **hay que respetarlos al editar**:

- **Measured** — leído del DOM. Es un hecho.
- **Observed** — visto y cronometrado. ±20%.
- **Approximate** — estimado de un screenshot. Nunca pegar como token final sin muestrear.

Algunas de las convergencias que justifican las reglas:

- Ninguno de los cinco usa `#FFFFFF` ni `#000000`.
- Los fondos cálidos de dos estudios distintos difieren en ≤8 puntos por canal — son *el mismo color*, elegido por separado.
- El tracking es inverso al tamaño, probado en dos registros opuestos: grotesca minúscula (−0.030em → +0.020em) y condensada versalita (+0.030em → +0.200em).
- El display va en peso 500, no 700, en todos los que cargan una bold.
- Nada rebota. Cero overshoot en los cinco.

---

## Jerarquía con otras skills

Si `impeccable` u otra skill de diseño choca con esta en un valor concreto — un color, una duración, un tracking, cuántas tipografías — **manda `skill-brakescode`**, porque estos números están medidos sobre trabajo que elegimos deliberadamente.

Las otras siguen siendo útiles para craft general que esta no cubre: accesibilidad a fondo, diseño de formularios, arquitectura de información, layout de dashboards.

---

## Actualizar

Cuando Orlando publique cambios:

```
/plugin marketplace update brakescode
```

---

## Contribuir

Los cambios se proponen por PR, no editando tu copia local.

Antes de tocar un valor, lee `casebook.md`. Si el número que quieres cambiar está marcado **measured**, va contra evidencia directa: o traes una medición nueva, o el cambio no entra. Si está marcado **approximate**, muestréalo bien y mejóralo — eso siempre se agradece.
