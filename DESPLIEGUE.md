## 🛠️ Informe de Despliegue: PokeDex en Azure Static Web Apps

### 1. Resumen del Proyecto

Despliegue de una aplicación web interactiva basada en Angular que consume datos de la PokeAPI.  
El objetivo principal fue configurar un flujo de integración y despliegue continuo (CI/CD) utilizando GitHub Actions y Azure Static Web Apps, cumpliendo con estándares de seguridad de nivel industrial.

---

### 2. Desafíos y Soluciones Técnicas

#### A. Fallo en la Construcción Remota (Cloud Build)

- **Problema:**  
  El flujo original en GitHub Actions fallaba por discrepancias en las versiones de Node.js y dependencias.

- **Solución:**  
  Se realizó un build local (`ng build`), generando la carpeta de producción optimizada.  
  Esto aseguró que el código desplegado fuera exactamente el probado en el entorno de desarrollo.

---

#### B. Reestructuración del Repositorio y Rutas

- **Problema:**  
  Azure no localizaba el `index.html` debido a la anidación de carpetas.  
  El pipeline utilizaba versiones obsoletas de Node.js (v20).

- **Solución:**
  - Se movieron los archivos compilados directamente a la raíz del proyecto.
  - Se actualizó el pipeline a Node.js 24 utilizando:
    - `FORCE_JAVASCRIPT_ACTIONS_TO_NODE24=true`
    - `actions/checkout@v4`

---

#### C. Conflicto de Historial (Git Push Force)

- **Problema:**  
  Errores de rechazo (`rejected / fetch first`) al sincronizar cambios locales con ediciones hechas en GitHub.

- **Solución:**  
  Uso de:
  ```bash
  git push origin main --force

para limpiar el historial y priorizar la versión de producción.

---

### 3. Configuración de Seguridad y Calificación A
Para cumplir con los estándares de PumasLab, se implementó el archivo staticwebapp.config.json, logrando una Calificación A en el Security Report Summary:

- Content-Security-Policy (CSP):
Permite conexión segura con https://pokeapi.co y carga de activos locales (assets/fonts, assets/images).

- HSTS & Anti-Clickjacking:
Implementación de:

Strict-Transport-Security

X-Frame-Options: DENY

- Manejo de rutas:
Redirección automática a index.html para evitar errores 404.

---

### 4. Parámetros Críticos del Pipeline (YAML)
El archivo .github/workflows/ fue ajustado para manejar artefactos precompilados:

app_location: "/" → Sitio ubicado en la raíz.

skip_app_build: true → Omite la compilación en la nube.

output_location: "" → Usa directamente los archivos de la app.

---

### 5. Resultados Obtenidos
Estado del pipeline: Exitoso (check verde).

Eficiencia: Tiempo de despliegue < 30 segundos.

Seguridad: Calificación A validada, mitigando riesgos de inyección y clickjacking.