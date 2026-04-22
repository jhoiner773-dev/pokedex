## PokeDex - PumasLab 2026

### Ingeniería de Sistemas - Sistemas Distribuidos

Aplicación web estática de alto rendimiento que consume la PokeAPI para visualizar los 151 Pokémon originales. Este proyecto se enfoca en la implementación de arquitecturas seguras y despliegue continuo (CI/CD) sobre Azure Static Web Apps.

---

### Características

Consumo de API: Integración fluida con PokeAPI v2.

Estética Retro: Interfaz inspirada en la GameBoy original con fuentes y activos personalizados.

Despliegue Profesional: Pipeline automatizado mediante GitHub Actions.

Seguridad Grado A: Configuración avanzada de cabeceras HTTP (HSTS, CSP, X-Frame-Options).

---

### Tecnologías

Frontend: HTML5, CSS3, JavaScript Vanilla.

Infraestructura: Azure Static Web Apps.

CI/CD: GitHub Actions (Runtime Node.js 24).

Seguridad: Content Security Policy (CSP) optimizado.

---

### Estructura de Activos

El proyecto cuenta con una gestión organizada de recursos locales:

/assets/fonts: Tipografía “Pokemon GB”.

/assets/images: Sprites y recursos visuales optimizados.

/assets/styles: Arquitectura modular de CSS.

---

### Análisis y Reflexiones Técnicas

#### 1. ¿Qué vulnerabilidades previenen los encabezados implementados?

La implementación del archivo staticwebapp.config.json no fue solo para obtener una nota, sino para mitigar riesgos críticos:

- Cross-Site Scripting (XSS):

Mediante el Content-Security-Policy (CSP), se restringe qué scripts pueden ejecutarse y desde qué dominios (como PokeAPI), evitando la inyección de código malicioso.

- Clickjacking:

Con el encabezado X-Frame-Options: DENY, se impide que la aplicación sea embebida en iframes de sitios externos no autorizados.

- MIME-Sniffing:

El encabezado X-Content-Type-Options: nosniff obliga al navegador a respetar el tipo de contenido declarado.

- Man-in-the-Middle (MitM):

El uso de HSTS garantiza que toda la comunicación se realice estrictamente por HTTPS.

#### 2. ¿Qué aprendiste sobre la relación entre despliegue y seguridad web?

- La seguridad es parte integral del despliegue, no una etapa final.

- Un despliegue exitoso implica no solo disponibilidad, sino resiliencia.

Los servicios como Azure aplican políticas por defecto que pueden interferir con la funcionalidad. El rol del ingeniero es ajustar ese equilibrio entre seguridad y operatividad, evitando bloqueos innecesarios (como el Error 500 experimentado).

#### 3. ¿Qué desafíos encontraste en el proceso?

- Configuración del CSP:

Ajustar la política para permitir recursos externos (fuentes y API) sin comprometer la calificación de seguridad.

- Ciclos de Vida del Pipeline:

Comprender los tiempos de ejecución y propagación de GitHub Actions en la infraestructura global de Azure.

- Resolución de Errores de Servidor:

Diagnóstico de errores (como HTTP 500) mediante herramientas de desarrollo y análisis del impacto de encabezados HTTP en el renderizado del cliente.

---

## 📑 Documentación Técnica

Para revisar el proceso de solución de errores, configuración de Azure y análisis de seguridad, haz clic aquí:
### 🔗 [Ver Bitácora de Despliegue](./DESPLIEGUE.md)
