# JobHunter MX

**Español** | [English](README.md)

> **Estado: idea y planificación.** Todavía no existen integraciones funcionales ni postulaciones automatizadas.

**JobHunter MX** es un asistente de búsqueda de empleo de código abierto, diseñado para el mercado laboral mexicano y para funcionar de manera autónoma en un teléfono Android antiguo. Su objetivo es descubrir ofertas relevantes, evaluar compatibilidad, adaptar el CV con información verídica y llevar el seguimiento de las postulaciones.

El dispositivo inicial es un **LG X230H con Android 6 (API 23)**, memoria y almacenamiento limitados. Por eso priorizamos una aplicación nativa ligera, una base de datos local y el uso opcional de IA por API. Una vez configurado, el sistema no debería necesitar una computadora ni un servidor personal siempre encendido; sí necesitará Internet para consultar fuentes y servicios de IA externos.

## ¿Por qué existe?

Buscar trabajo en México suele exigir revisar Indeed, OCC, Computrabajo, publicaciones de Facebook y páginas de empresas. Comparar requisitos, adaptar un currículum y registrar solicitudes consume mucho tiempo. JobHunter MX busca reducir ese trabajo sin quitarle el control a la persona que busca empleo.

## Funciones previstas

- **Recepción de vacantes:** fuentes permitidas, alertas oficiales, enlaces compartidos por el usuario, avisos por correo y posibles APIs autorizadas. Cada plataforma tendrá un adaptador independiente; ninguna compatibilidad está garantizada.
- **Búsqueda por ubicación:** ciudad, radio configurable, modalidades remota/híbrida/presencial, salario, puesto y tecnologías. La zona se podrá introducir manualmente; usar GPS preciso será opcional.
- **Evaluación de compatibilidad:** comparar la vacante con un perfil estructurado de experiencia y habilidades, mostrando coincidencias, requisitos faltantes y condiciones excluyentes. El porcentaje es orientativo, **no** una probabilidad de contratación.
- **CV dinámico con IA:** partir de un perfil maestro verificado y generar una versión legible para ATS por cada vacante, reordenando y destacando lo relevante **sin inventar empleos, estudios, habilidades ni fechas**.
- **Documentos bilingües:** plantillas en español e inglés, exportación PDF e historial de las versiones generadas para cada oferta.
- **Gestor de postulaciones:** enlaces, contactos, borradores, estados, fechas y resultados; notificaciones cuando una solicitud esté preparada.
- **Operación autónoma:** búsquedas programadas, deduplicación, reintentos y avisos, respetando las limitaciones de batería y segundo plano de Android.
- **Privacidad:** base local, mínima recopilación de datos, permisos explícitos, protección de credenciales y opciones para exportar/eliminar información.

## Flujo propuesto

```text
Alertas / fuentes permitidas / enlaces compartidos
                        |
                        v
              Normalizar y deduplicar
                        |
                        v
              Filtrar y evaluar oferta
                        |
                        v
            Adaptar CV con datos reales
                        |
                        v
         Revisar / seguir flujo autorizado
                        |
                        v
              Registrar y notificar
```

**Importante:** descubrir vacantes y preparar borradores puede ser autónomo; el envío dependerá de los permisos y flujos de cada sitio. El proyecto **no** pretende evadir CAPTCHA, sistemas antibots ni automatizar acciones prohibidas por las plataformas. Cuando corresponda, el usuario terminará la postulación manualmente.

## Arquitectura técnica prevista (aún no implementada)

| Capa | Tecnología candidata |
| --- | --- |
| Aplicación Android | Kotlin, SDK de Android (mínimo API 23), interfaz nativa ligera |
| Tareas en segundo plano | JobScheduler compatible o una versión de WorkManager verificada para Android 6 |
| Datos locales | SQLite / Room en versión compatible |
| Fuentes | APIs oficiales/permitidas, alertas, correo y enlaces importados |
| Compatibilidad | Filtros deterministas e IA remota opcional |
| CV | Plantillas HTML/texto ligeras y generación de PDF |
| Inteligencia artificial | Proveedor remoto configurable; sin necesidad de modelos grandes locales |
| Avisos | Notificaciones Android |

Android 6 ya no recibe soporte de seguridad. Habrá que comprobar compatibilidad de bibliotecas, certificados HTTPS y tareas en segundo plano en el dispositivo real. No se deben incluir claves de API permanentes de pago sin protección dentro de la app; para producción quizá necesitemos credenciales acotadas o un intermediario opcional. No se presupone una PC dedicada.

## Estructura propuesta

```text
app/                # Aplicación Android
core/               # Planificación y orquestación
sources/            # Adaptadores de fuentes permitidas
matching/           # Filtros, geolocalización y puntuación
resume/             # Perfil maestro, adaptación y exportación
applications/       # Borradores y seguimiento de solicitudes
storage/            # Base de datos y archivos locales
docs/               # Diseño y políticas de uso de fuentes
tests/              # Pruebas unitarias y de integración
```

La estructura es una propuesta; estos directorios todavía no existen.

## Hoja de ruta

- [ ] **M0 — Viabilidad del dispositivo:** verificar compilación, instalación, HTTPS, batería y tareas programadas en el LG X230H.
- [ ] **M1 — MVP local:** configurar preferencias, importar vacantes desde enlaces/alertas, eliminar duplicados, filtrar y dar seguimiento.
- [ ] **M2 — Compatibilidad:** justificar coincidencias y requisitos faltantes con un perfil real.
- [ ] **M3 — CV dinámico:** generar, revisar y exportar CV PDF en español/inglés por oferta.
- [ ] **M4 — Notificaciones:** consultas periódicas autónomas desde fuentes admitidas y avisos de nuevas coincidencias.
- [ ] **M5 — Postulaciones:** asistencia para preparar formularios y envíos permitidos; seguimiento de respuestas.
- [ ] **M6 — Resultados:** analizar tasas de respuesta por versión de CV, con privacidad y cuidado ante muestras pequeñas.

## Automatización responsable

Respetar términos de uso, reglas de acceso, límites de frecuencia, consentimiento y seguridad de cuentas. Nunca enviar datos falsos sin revisión ni marcar una solicitud como enviada sin confirmación. Evitar la recopilación no autorizada de Facebook y otras plataformas. Mantener un historial auditable y un control para pausar o detener el agente.

## Alcance

Inicialmente orientado a vacantes de desarrollo de software en México, pero configurable para otras profesiones, ciudades, fuentes e idiomas.

## Colaboraciones

El proyecto está en fase de planificación. Se agradecen propuestas de diseño, pruebas de compatibilidad con Android antiguo, mejoras de accesibilidad, documentación e integraciones autorizadas. Las instrucciones de contribución y la licencia se definirán después.

---
*JobHunter MX es un proyecto independiente y no está afiliado a Indeed, OCC, Computrabajo, Meta ni a ningún empleador.*
