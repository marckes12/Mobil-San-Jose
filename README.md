https://github.com/user-attachments/assets/e84699fd-5456-420f-9b1d-ef6c07bb6387
# 📱 App de Gestión de Cobranza (Cobranza San José)

![Flutter Version](https://img.shields.io/badge/Flutter-SDK-02569B?style=for-the-badge&logo=flutter&logoColor=white)
![Dart](https://img.shields.io/badge/Dart-0175C2?style=for-the-badge&logo=dart&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=for-the-badge&logo=sqlite&logoColor=white)

> Una aplicación móvil integral desarrollada en Flutter para la gestión avanzada de cobranza en campo, monitoreo de créditos, geolocalización de clientes e impresión térmica Bluetooth. Diseñada para operar de manera eficiente en entornos con o sin conexión a internet.

---

## 📌 1. Introducción y Explicación del Proyecto
**Cobranza San José** es una herramienta móvil robusta diseñada para digitalizar y optimizar el flujo de trabajo de los gestores de cobranza. La aplicación permite a los agentes consultar información de clientes, registrar pagos en tiempo real, realizar investigaciones de campo, capturar evidencia fotográfica e imprimir recibos térmicos directamente en el domicilio del cliente. Su enfoque "Offline-First" garantiza que los gestores puedan seguir trabajando en zonas de baja cobertura, sincronizando los datos automáticamente cuando la conexión se restablece.

## ✨ 2. Características de Desarrollo
- **Offline-First**: Integración profunda con SQLite para garantizar la operatividad de la app sin conexión a internet.
- **Impresión Térmica Bluetooth**: Generación e impresión de recibos de pago en el sitio usando impresoras ESC/POS.
- **Geolocalización en Tiempo Real**: Rastreo de ubicaciones, captura de coordenadas en visitas y visualización de rutas con Google Maps.
- **Captura de Evidencia**: Integración con la cámara del dispositivo para adjuntar fotos de domicilios o comprobantes.
- **UI/UX Fluida y Moderna**: Navegación intuitiva con `curved_navigation_bar`, animaciones personalizadas y diseño responsivo.
- **Manejo Dinámico de Estados**: Sincronización transparente de información entre la base de datos local y el servidor.

## 🏗️ 3. Arquitectura de Servicios
El proyecto sigue una arquitectura **MVC (Model-View-Controller)** adaptada para Flutter, asegurando la separación de responsabilidades:
- **Views (`lib/views`)**: Contiene las interfaces de usuario.
- **Models (`lib/models`)**: Define la estructura de datos que se comunica entre la base de datos local y la API.
- **Providers / Services (`lib/providers`)**: Capa de acceso a datos. El archivo central `db_provider.dart` orquesta todas las transacciones SQL (CRUD) y maneja la lógica de sincronización con el backend mediante peticiones HTTP.

## 🔐 4. Sistema de Autenticación
El sistema de seguridad incluye:
- **Login Seguro**: Interfaz de autenticación (`login2.dart`) validada contra los servidores en la nube.
- **Gestión de Sesiones**: Uso de `shared_preferences` para almacenar y encriptar los tokens/datos del usuario de forma local, evitando que el usuario deba iniciar sesión cada vez que abre la app.
- **Control de Accesos (Roles)**: Diferenciación de interfaces y permisos dependiendo de si el usuario es administrador (`adminPane.dart`, `viewAdmin.dart`) o gestor de campo (`menuDashboard.dart`).

## 🗄️ 5. Estructura del Proyecto (Árbol de Directorios)
A continuación se detalla la estructura principal del código fuente (`lib/`), donde se evidencia la separación de responsabilidades:

```text
📦 cj1 (Cobranza San José)
 ┣ 📂 android/                  # Archivos nativos para compilación Android
 ┣ 📂 ios/                      # Archivos nativos para compilación iOS
 ┣ 📂 assets/                   # Recursos estáticos (imágenes, iconos)
 ┣ 📂 lib/                      # Código fuente de la aplicación Flutter
 ┃ ┣ 📂 Animations/             # Efectos y animaciones (FadeAnimation)
 ┃ ┣ 📂 models/                 # Modelos de base de datos local y API
 ┃ ┃ ┣ 📄 SociosModel.dart      # Entidad principal del cliente
 ┃ ┃ ┣ 📄 CreditosModel.dart    # Historial de créditos
 ┃ ┃ ┣ 📄 PagosModel.dart       # Registro de pagos
 ┃ ┃ ┣ 📄 AvalesModel.dart      # Relación de fiadores
 ┃ ┃ ┣ 📄 VisitaModel.dart      # Bitácora de campo
 ┃ ┃ ┗ 📄 ... (otros modelos de negocio)
 ┃ ┣ 📂 providers/              # Servicios y conexión a DB
 ┃ ┃ ┗ 📄 db_provider.dart      # Orquestador SQL transaccional y red
 ┃ ┣ 📂 routes/                 # Configuración de enrutamiento
 ┃ ┃ ┗ 📄 routes.dart
 ┃ ┣ 📂 utils/                  # Utilidades y variables globales
 ┃ ┃ ┣ 📄 db_pojos.dart
 ┃ ┃ ┗ 📄 getCredenciales.dart
 ┃ ┣ 📂 views/                  # Interfaces de Usuario (UI)
 ┃ ┃ ┣ 📄 main.dart             # Punto de entrada
 ┃ ┃ ┣ 📄 SplashScreen.dart     # Pantalla de carga
 ┃ ┃ ┣ 📄 login2.dart           # Autenticación segura
 ┃ ┃ ┣ 📄 menuDashboard.dart    # Vista de campo
 ┃ ┃ ┣ 📄 adminPane.dart        # Vista administrativa
 ┃ ┃ ┣ 📂 creditos/             # Vistas de créditos vigentes y vencidos
 ┃ ┃ ┣ 📂 datosCliente/         # Vistas de perfiles y desgloses
 ┃ ┃ ┣ 📂 headerViews/          # Vistas para evidencias fotográficas
 ┃ ┃ ┣ 📂 investigaciones/      # Formularios de campo y propiedades
 ┃ ┃ ┣ 📂 pagos/                # Pantallas transaccionales de cobro
 ┃ ┃ ┗ 📂 ubicacion/            # Integración de Mapas (Google Maps)
 ┃ ┗ 📄 main.dart               # Archivo de arranque principal
 ┣ 📄 pubspec.yaml              # Configuración de dependencias (Flutter)
 ┗ 📄 README.md                 # Documentación del proyecto
```

## 🧩 6. Módulos Implementados
El sistema se compone de los siguientes módulos principales:
1. **Módulo de Autenticación**: Splash screen de carga y validación de credenciales.
2. **Dashboard Principal**: Panel de control con métricas rápidas y navegación principal.
3. **Módulo de Clientes (Perfil)**: Expediente digital con datos generales, saldos e historial.
4. **Módulo de Créditos**: Desglose de amortizaciones, deudas vigentes y tasas de interés.
5. **Módulo de Pagos**: Captura de ingresos, validación de montos y conexión directa al módulo de impresión térmica.
6. **Módulo de Investigaciones / Visitas**: Bitácora de campo para registrar promesas de pago, evidencias fotográficas y estado de la visita.
7. **Módulo de Ubicación**: Integración de mapas para rutas y localización exacta de domicilios.

## 🛠️ 7. Tecnologías Utilizadas
### Core & UI
- **Flutter SDK** (Dart)
- `curved_navigation_bar`, `simple_animations`, `badges`, `timeline_tile` (Diseño e Interfaz)
- `intl`, `money2` (Formateo de divisas y fechas)

### Almacenamiento & Red
- **SQLite** (`sqflite`) - Base de datos local transaccional.
- `shared_preferences` - Almacenamiento persistente clave-valor para sesiones.
- `http`, `dio` - Clientes HTTP para consumo de APIs REST.

### Hardware & Dispositivo
- `google_maps_flutter`, `geolocator` - Servicios de ubicación y mapas.
- `blue_thermal_printer`, `esc_pos_printer` - Conectividad Bluetooth y comandos de impresión ESC/POS.
- `image_picker` - Acceso a la cámara y galería de fotos.
- `path_provider` - Acceso al sistema de archivos del dispositivo.

---
*Este repositorio es una muestra de mis habilidades en el desarrollo móvil multiplataforma, diseño de arquitecturas offline-first e integración de hardware externo (Bluetooth/Impresoras) utilizando el ecosistema Flutter.*


