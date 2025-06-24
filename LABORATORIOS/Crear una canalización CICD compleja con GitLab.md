# Crear una canalización CI/CD compleja con GitLab CI/CD y Docusaurus

---

## Requisitos previos

1. **Cuenta en GitLab.com**
   Asegúrate de tener acceso y permisos para crear proyectos.

2. **Familiaridad con Git**
   Debes saber usar `clone`, `commit`, `branch`, `merge`, etc.

3. **Node.js instalado localmente**
   Por ejemplo, en macOS usa:

   ```bash
   brew install node
   ```

   Comprueba la instalación:

   ```bash
   node --version
   npm --version
   ```

---

## 1. Crear el proyecto de Docusaurus

### 1.1 Crear un repositorio nuevo en GitLab

* Ve a **Create new** → **New project/repository**.
* Elige **Create blank project**.
* Define:

  * **Nombre**: p. ej. `my-pipeline-tutorial`.
  * Marca **Initialize repository with a README**.
* Haz clic en **Create project**.

### 1.2 Clonar el repositorio a tu máquina

En tu terminal:

```bash
git clone git@gitlab.com:TU_USUARIO/my-pipeline-tutorial.git
cd my-pipeline-tutorial
```

Sustituye `TU_USUARIO`.

### 1.3 Inicializar Docusaurus

Ejecútalo y responde con las opciones por defecto (nombre del sitio, tagline, plantilla “classic”):

```bash
npm init docusaurus
```

Esto creará una carpeta `website/`.

### 1.4 Mover archivos al raíz

```bash
mv website/* .
rm -rf website
```

### 1.5 Configurar `docusaurus.config.js`

Abre el archivo y ajusta:

```js
url: 'https://TU_USUARIO.gitlab.io',
baseUrl: '/my-pipeline-tutorial/',
```

Reemplaza `TU_USUARIO` y `my-pipeline-tutorial`.

### 1.6 Subir cambios

```bash
git add .
git commit -m "Agregar sitio Docusaurus inicial"
git push origin
```

Comprueba que el README y la estructura se han subido.

---

## 2. Crear el archivo inicial CI/CD (`.gitlab-ci.yml`)

Este fichero define tu canalización:

```yaml
test-job:
  script:
    - echo "¡Este es mi primer job!"
    - date
```

* Crea `.gitlab-ci.yml` en el raíz.

* Sube y empuja:

  ```bash
  git add .gitlab-ci.yml
  git commit -m "Primer CI_JOB simple"
  git push origin
  ```

* En GitLab, ve a **CI/CD > Pipelines** y verifica que se ejecute `test-job`. Log: “¡Este es mi primer job!” + fecha.

---

## 3. Construir el sitio (`build-job`)

Reemplaza `test-job` por lo siguiente:

```yaml
build-job:
  image: node                # usa el contenedor oficial de Node.js
  script:
    - npm install           # instala dependencias (Docusaurus)
    - npm run build         # construye el sitio estático
  artifacts:
    paths:
      - build/              # guarda la carpeta build/
```

* `image:` define el entorno, aquí contenedor Node oficial.
* `artifacts:` permite que archivos generados sean usados por siguientes jobs.

Ejecútalo:

```bash
git add .gitlab-ci.yml
git commit -m "Agregar job de build"
git push origin
```

Verifica:

* Job `build-job` aparece.
* Revisa log: `npm install`, `npm run build`.
* Usa “Browse” para ver contenido en `build/`.

---

## 4. Desplegar el sitio (`pages` + zonas)

Amplía `.gitlab-ci.yml`:

```yaml
stages:
  - build
  - deploy

build-job:
  stage: build
  image: node
  script:
    - npm install
    - npm run build
  artifacts:
    paths:
      - build/

pages:
  stage: deploy
  script:
    - mv build/ public/     # GitLab Pages requiere carpeta public/
  artifacts:
    paths:
      - public/
```

* `stages:` define orden: primero `build`, luego `deploy`.
* Job `pages` toma artefacto de `build-job`, mueve `build/ → public/`, y lo expone como sitio publicada.

Empuja y comprueba:

```bash
git add .gitlab-ci.yml
git commit -m "Agregar deploy con pages"
git push origin
```

* Verás jobs separados en distintas etapas.
* Nuevas entradas: `pages:deploy`.
* En **Deploy > Pages**, copia el enlace (ej: `https://TU_USUARIO.gitlab.io/my-pipeline-tutorial/`).

---

## 5. Agregar pruebas (`lint-markdown`, `test-html`)

Añade al `.gitlab-ci.yml`:

```yaml
stages:
  - build
  - test
  - deploy

# build-job omisionada arriba...

lint-markdown:
  stage: test
  image: node
  dependencies: []         # sin artefactos
  script:
    - npm install -g markdownlint-cli2
    - markdownlint-cli2 -v
    - markdownlint-cli2 "blog/**/*.md" "docs/**/*.md"
  allow_failure: true      # permite fallar sin detener el pipeline

test-html:
  stage: test
  image: node
  dependencies:
    - build-job
  script:
    - npm install --save-dev htmlhint
    - npx htmlhint --version
    - npx htmlhint build/
```

Detalles:

* `lint-markdown` analiza sólo Markdown. Se permite fallo.
* `test-html` revisa HTML generado, depende de artefacto de `build-job`.

Empuja y revisa:

```bash
git add .gitlab-ci.yml
git commit -m "Agregar jobs de prueba"
git push origin
```

En **Pipelines**:

* Stage `test` con dos jobs.
* `lint-markdown` puede fallar sin bloquear el pipeline.
* `test-html` usa el sitio ya construido.

---

## 6. Usar canalizaciones para Merge Requests (`rules`)

Añade reglas para controlar cuándo se ejecutan:

```yaml
build-job:
  ... (como antes)
  rules:
    - if: $CI_PIPELINE_SOURCE == 'merge_request_event'
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH

lint-markdown:
  ... (como antes)
  rules:
    - if: $CI_PIPELINE_SOURCE == 'merge_request_event'
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH

test-html:
  ...
  rules:
    - if: $CI_PIPELINE_SOURCE == 'merge_request_event'
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH

pages:
  ...
  rules:
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH
```

* `rules:` define cuándo correr cada job:

  * Se ejecutan en pipelines generados por MR.
  * `pages` solo en actualizaciones de la rama predeterminada (`main` o `master`).

Flujo:

* Creas rama `feature`.
* Haces MR → pipeline se ejecuta (sin deploy).
* MR merge a `main` → se ejecuta deploy y se publica automáticamente.

---

## 7. Reducir configuración repetida con `default`, `extends` y jobs ocultos

Finaliza `.gitlab-ci.yml` así:

```yaml
stages:
  - build
  - test
  - deploy

default:
  image: node       # valor por defecto para jobs

.standard-rules:
  rules:
    - if: $CI_PIPELINE_SOURCE == 'merge_request_event'
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH

build-job:
  extends: [.standard-rules]
  stage: build
  script:
    - npm install
    - npm run build
  artifacts:
    paths:
      - build/

lint-markdown:
  extends: [.standard-rules]
  stage: test
  dependencies: []
  script:
    - npm install -g markdownlint-cli2
    - markdownlint-cli2 -v
    - markdownlint-cli2 "blog/**/*.md" "docs/**/*.md"
  allow_failure: true

test-html:
  extends: [.standard-rules]
  stage: test
  dependencies:
    - build-job
  script:
    - npm install --save-dev htmlhint
    - npx htmlhint --version
    - npx htmlhint build/

pages:
  stage: deploy
  image: busybox      # override: ligera utilidad UNIX
  dependencies:
    - build-job
  script:
    - mv build/ public/
  artifacts:
    paths:
      - public/
  rules:
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH
```

Detalles:

* `default:` define el contenedor base para todos los jobs (salvo override).
* Job oculto `.standard-rules` centraliza reglas.
* `extends:` aplica reglas comunes.
* `pages` usa `busybox`, más ligero.
* La configuración es DRY (no repetitiva) y fácil de mantener.

---

## Conclusión

* Canalización en etapas: construcción, pruebas y despliegue.
* Integración con Merge Requests: validación en ramas y despliegue solo en main.
* Gestión de artefactos entre jobs.
* Configuración modular, limpia y escalable.

