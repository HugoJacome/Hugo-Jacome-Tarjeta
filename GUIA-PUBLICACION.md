# Guía: publicar la tarjeta en GitHub Pages con dominio propio

## Datos por personalizar antes de publicar

En `index.html` y `hugo-jacome.vcf` reemplaza:

- `+593999999999` → tu número real (aparece en WhatsApp, Llamar y el vCard)
- `github.com/tuusuario` y `linkedin.com/in/tuusuario` → tus perfiles reales
- La foto: hoy el avatar muestra las iniciales "HJ". Para usar foto real, guarda `foto.jpg` en la carpeta y cambia el div del avatar por `<img src="foto.jpg" ...>` con el mismo estilo circular.

## Paso 1 — Subir a GitHub

1. Crea una cuenta u organización de GitHub para EvoWeb (ej. `evowebec`).
2. Crea un repositorio público, ej. `tarjeta-hugo`.
3. Sube los archivos de esta carpeta (`index.html`, `hugo-jacome.vcf`).

```bash
git init
git add .
git commit -m "Tarjeta digital Hugo Jácome"
git branch -M main
git remote add origin https://github.com/evowebec/tarjeta-hugo.git
git push -u origin main
```

## Paso 2 — Activar GitHub Pages

1. En el repo: **Settings → Pages**.
2. En "Source" elige **Deploy from a branch**, rama `main`, carpeta `/ (root)`.
3. En 1–2 minutos la tarjeta queda en `https://evowebec.github.io/tarjeta-hugo/`.

## Paso 3 — Dominio propio (plan Pro)

1. Compra el dominio en Cloudflare Registrar o Porkbun (~USD 10–11/año el .com).
2. En **Settings → Pages → Custom domain** escribe el dominio (ej. `hugojacome.com`) y guarda. Esto crea el archivo `CNAME` en el repo.
3. En el DNS del dominio crea:
   - Registros **A** para el dominio raíz apuntando a las IPs de GitHub Pages:
     `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - Registro **CNAME** de `www` → `evowebec.github.io`
4. Espera la verificación y marca **Enforce HTTPS** (el SSL es gratis y automático).

> En Cloudflare: pon los registros en modo "DNS only" (nube gris) hasta que GitHub emita el certificado; luego puedes activar el proxy si quieres.

## Paso 4 — QR definitivo

El QR de la página se genera solo y siempre apunta a la URL donde está publicada,
así que al activar el dominio ya queda correcto.

Para el QR imprimible en alta resolución (credenciales, firmas, material impreso):
genera un PNG/SVG del enlace final en cualquier generador (ej. Cloudflare no hace falta;
sirve `qr.io`, `goqr.me` o la librería ya incluida) a 1000×1000 px o más.

**Clave comercial:** el QR apunta al dominio, no a los datos. Si el cliente cambia
de número o cargo, se edita `index.html`, se hace push, y todos los QR ya impresos
siguen funcionando.

## Modelo por subdominio (plan Start)

Para tarjetas Start no se compra dominio: en el DNS de `evowebec.com` se crea un
CNAME por cliente (`nombre.evowebec.com` → `evowebec.github.io`) y en el repo del
cliente se configura ese subdominio como custom domain. Costo marginal: USD 0.

## Checklist de entrega al cliente

- [ ] Enlace final funcionando con HTTPS
- [ ] QR en alta resolución (PNG y SVG)
- [ ] vCard descargable probada en iPhone y Android
- [ ] Botón WhatsApp probado
- [ ] Guía de 1 página: cómo compartir su tarjeta (firma de correo, estados, redes)
- [ ] Fecha de renovación registrada en el control de dominios
