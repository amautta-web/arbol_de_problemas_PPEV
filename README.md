# Árbol de problemas · PPEV Medellín

Visualización interactiva del árbol de problemas de la actualización de la
Política Pública de Envejecimiento y Vejez del Distrito de Medellín.

## Contenido

```
.
├── index.html    página completa (HTML + CSS + JS + datos en un solo archivo)
├── .nojekyll     evita que GitHub Pages procese el sitio con Jekyll
└── README.md
```

No hay dependencias que instalar ni proceso de compilación. Las tipografías
(Google Fonts) y GSAP se cargan por CDN sobre HTTPS.

## Publicar en GitHub Pages

1. Crear el repositorio y subir los tres archivos **en la raíz**:

   ```bash
   git init
   git add .
   git commit -m "Árbol de problemas PPEV"
   git branch -M main
   git remote add origin https://github.com/USUARIO/REPOSITORIO.git
   git push -u origin main
   ```

2. En GitHub: **Settings → Pages**.
3. En *Build and deployment*, elegir **Deploy from a branch**.
4. Branch: `main`, carpeta: `/ (root)`. Guardar.
5. Esperar uno o dos minutos. La URL queda en
   `https://USUARIO.github.io/REPOSITORIO/`

## Si la página sale en blanco

- El archivo **debe llamarse `index.html`** y estar en la raíz de la rama
  publicada. Con cualquier otro nombre GitHub devuelve un 404.
- Si se publica desde una subcarpeta, elegir `/docs` en *Settings → Pages* y
  mover ahí los archivos.
- El `.nojekyll` es necesario: sin él, Jekyll ignora cualquier archivo o
  carpeta que empiece por guion bajo.
- Forzar recarga sin caché (Ctrl+F5) tras cada despliegue.

## Uso

- Clic en cualquier nodo: traza la relación con su contraparte —una causa se
  enlaza con su efecto y viceversa—, atenúa el resto del árbol y muestra el
  texto completo de ambas tarjetas.
- Salir del trazado: la **✕** sobre la tarjeta, clic fuera, o `Esc`.
- Impresión: los controles se ocultan y las tarjetas no se parten entre páginas.
- Respeta `prefers-reduced-motion`: con la preferencia activa el árbol aparece
  ya montado, sin animación de entrada.

## Editar el contenido

Todo el texto vive en el arreglo `NODES` dentro de `index.html`. Cada nodo tiene:

| campo  | significado                                                        |
|--------|--------------------------------------------------------------------|
| `t`    | nivel: `i-up` / `d-up` / `d-dn` / `i-dn`                            |
| `e`    | número de eje (1–6)                                                 |
| `c`    | columna en la retícula de 8, p. ej. `"4"` o `"2 / span 2"`          |
| `code` | código del nodo (E.I.1.1, C.D.3…), del que depende el emparejamiento |
| `x`    | texto del nodo                                                      |

El enlace causa ↔ efecto se calcula con el sufijo del código: `C.I.2.1` apunta
a `E.I.2.1`. Si un nodo abarca dos columnas (`span`), se enlaza con todos los
nodos de su eje en el nivel espejo.
