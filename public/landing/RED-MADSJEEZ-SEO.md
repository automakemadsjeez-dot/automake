# Red Madsjeez — Backlinks legítimos entre propiedades

## Lo que ya hice en Automake
1. **Sección "Ecosistema"** en el footer con 7 cards apuntando a cada propiedad. Anchor text descriptivo, `rel="me noopener"`.
2. **JSON-LD `Organization`** en el `<head>` con `sameAs[]` listando los 7 dominios. Google interpreta esto como "todas estas URLs pertenecen a la misma entidad".
3. **JSON-LD `SoftwareApplication`** con `publisher.name = "Madsjeez"` — refuerza la propiedad.

## Lo que tenés que replicar en CADA otra propiedad

### Mínimo viable (5 minutos por sitio):
Agregá en el `<head>` de cada sitio:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "<nombre del sitio>",
  "url": "https://www.<dominio>",
  "sameAs": [
    "https://automake-production.up.railway.app/landing/",
    "https://www.madsjeez.com.ar",
    "https://www.madsjeezdesign.com",
    "https://www.appjeezpro.com",
    "https://www.appjeezpro.store",
    "https://www.trabajocerca.site",
    "https://www.marda.site",
    "https://www.mellimelos.site"
  ]
}
</script>
```

(en cada sitio, en `sameAs` poné los OTROS 6 dominios — no te listes a vos mismo)

### Recomendado (lo que mueve la aguja):
En el **footer** de cada propiedad agregá una sección similar a la de Automake con anchor text variado:

```html
<footer>
  ...
  <section>
    <h3>Otros productos Madsjeez</h3>
    <ul>
      <li><a href="https://automake-production.up.railway.app/landing/" rel="me">Automake — mensajería omnicanal con IA</a></li>
      <li><a href="https://www.madsjeez.com.ar" rel="me">Madsjeez Studio — desarrollo de software</a></li>
      <li><a href="https://www.madsjeezdesign.com" rel="me">Madsjeez Design — branding y UI</a></li>
      <li><a href="https://www.appjeezpro.com" rel="me">AppJeezPro — app pro</a></li>
      <li><a href="https://www.appjeezpro.store" rel="me">AppJeezPro Store — marketplace</a></li>
      <li><a href="https://www.trabajocerca.site" rel="me">TrabajoCerca — empleo en Salta</a></li>
      <li><a href="https://www.marda.site" rel="me">Marda</a></li>
      <li><a href="https://www.mellimelos.site" rel="me">Mellimelos — tienda online</a></li>
    </ul>
  </section>
</footer>
```

## Reglas para que Google lo considere LEGÍTIMO (no PBN)

| ✅ Hacer | ❌ NO hacer |
|---|---|
| Anchor text descriptivo y variado por sitio | "Click aquí" o keywords stuffing |
| Solo links en footer/about/contact (1 vez por sitio) | Sembrar enlaces en cada página/post |
| `rel="me"` o sin `rel` (do-follow) | `rel="sponsored"` o `nofollow` (anula el valor) |
| Mencionar al estudio Madsjeez como dueño común | Negar la relación / ocultar ownership |
| Contenido único y útil en cada sitio | Sitios calcados o sin contenido real |
| Coincidir WHOIS / contacto en todos | Esconderse detrás de WHOIS privacy en todos |

## Bonus que ayuda mucho a la E-E-A-T

1. **Misma página "Sobre nosotros"** o "Equipo" en todos los sitios, mencionando Madsjeez como estudio.
2. **Logo / mention de Madsjeez en cada sitio** ("Un producto de Madsjeez Studio").
3. **WHOIS público y consistente** (mismo registrante, email, dirección).
4. **Google Search Console**: agregá las 8 propiedades a la misma cuenta GSC. Google ya sabe que sos vos.
5. **Sitemaps cruzados**: en el `sitemap.xml` de cada sitio podés mencionar las URLs hermanas (opcional).
6. **Blog cross-linking contextual**: si en `madsjeezdesign.com` escribís un post sobre branding de SaaS, linkeá orgánicamente a Automake como caso. Eso es ORO.

## Lo que NO hace falta
- ❌ Pagar PBNs / link farms
- ❌ Intercambios masivos con sitios ajenos
- ❌ Spam de comentarios
- ❌ Guest posts forzados

Una red propia bien declarada + buen contenido en cada sitio te da más que 100 backlinks turbios.
