# Sitio web · Triciclos en La Habana

Esta carpeta contiene **solo lo necesario para publicar el informe como GitHub Page**.
No incluye hojas de cálculo, documentos de entrevistas, OCR ni capturas de pantalla.

## Contenido

```text
sitio_web/
├── index.html          # informe completo
├── .nojekyll           # evita el procesamiento de Jekyll en GitHub Pages
└── assets/
    ├── css/estilos.css
    ├── js/app.js
    ├── img/            # 10 figuras en PNG
    └── data/           # 4 CSV descargables
```

El sitio es estático y funciona sin servidor, sin CDN y sin conexión a internet.

---

## 1. Publicarlo en GitHub Pages

1. Creá un repositorio en GitHub. Para usar Pages gratis, el repositorio debe ser **público**.
2. Subí **el contenido de esta carpeta** a la raíz del repositorio:
   - `index.html`
   - `.nojekyll`
   - la carpeta `assets/`

   No subas la carpeta `sitio_web` completa dentro del repositorio. GitHub Pages debe encontrar `index.html` en la raíz.
3. En el repositorio: **Settings → Pages**.
4. En **Build and deployment → Source**, elegí:
   - **Deploy from a branch**
   - Branch: **main**
   - Folder: **/ (root)**
5. Guardá y esperá uno o dos minutos.

La URL queda así:

```text
https://<tu-usuario>.github.io/<nombre-del-repositorio>/
```

Por ejemplo:

```text
https://usuario.github.io/CD/
```

Como `index.html` está en la raíz, no hace falta agregar `/informe/`.

---

## 2. Dominio propio (opcional)

El dominio `tricicloproject.com` **no resuelve y no figura registrado** en el registro `.com` al 9 de noviembre de 2026. Primero hay que registrarlo en un registrador (Namecheap, Cloudflare, Porkbun, GoDaddy, etc.).

Después, en el panel DNS del registrador:

### Dominio raíz

| Tipo | Nombre | Valor |
|---|---|---|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |

### Subdominio www

| Tipo | Nombre | Valor |
|---|---|---|
| CNAME | `www` | `<tu-usuario>.github.io` |

Luego, en **Settings → Pages → Custom domain**, escribí el dominio y guardá.
Cuando el DNS esté correcto, activá **Enforce HTTPS**.

Si GitHub pide verificación, agregá el registro **TXT** que muestra la pantalla de configuración.

> El archivo `CNAME` debe quedar en la raíz publicada, junto a `index.html`.
> No lo crees a mano hasta tener el dominio registrado y el DNS configurado.

---

## 3. Probar el sitio localmente

Desde esta carpeta:

```powershell
python -m http.server 8000
```

Y abrí:

```text
http://localhost:8000
```

También podés abrir `index.html` directamente con doble clic.

---

## 4. Problemas frecuentes

**La página principal da 404**
- Se subió la carpeta `sitio_web` en lugar de su contenido.
- `index.html` no está en la raíz del repositorio.
- Pages está configurado para publicar otra rama o carpeta.

**El sitio abre sin estilos ni figuras**
- Falta la carpeta `assets/` o no está al mismo nivel que `index.html`.
- Se renombraron o movieron archivos dentro de `assets/`.

**El dominio propio no conecta**
- El dominio no está registrado.
- Faltan los registros A o el CNAME de `www`.
- El DNS todavía está propagando (puede tardar hasta 24–48 horas).
- Quedaron registros viejos en conflicto.

**GitHub Pages no publica**
- El repositorio es privado y la cuenta no tiene Pages habilitado para repositorios privados.
- La rama elegida no es la que contiene `index.html`.

### Verificar DNS

```powershell
nslookup tricicloproject.com
nslookup www.tricicloproject.com
```

El dominio raíz debe devolver las IPs `185.199.108.153` a `185.199.111.153`.

---

## 5. Actualizar el informe

El sitio se genera desde el proyecto principal:

```powershell
cd D:\Escuela\CD
python informe/generar_informe.py
```

Después de regenerarlo, copiá de nuevo `informe/index.html` y `informe/assets/` a esta carpeta, o volvé a ejecutar el script de publicación si lo tenés automatizado.

Los números, figuras y tablas provienen de `dataset_unificado_triciclos.csv`.
