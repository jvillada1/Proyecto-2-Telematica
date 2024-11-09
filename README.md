# TÓPICOS TELEMÁTICA - ST0263

## Estudiantes: 
- Antonio Carbonó Pedroza, hacarbonop@eafit.edu.co
- David Elias Franco Vélez, defrancov@eafit.edu.co
- Daniel Vélez Duque, dvelezd2@eafit.edu.co  
- Juan José Villada Calle, jjvilladac@eafit.edu.co

## Profesor: 
- Alvaro Enrique Ospina Sanjuan, aeospinas@eafit.edu.co

## 1. Descripción
Este proyecto implementa el despliegue de un sistema de gestión de contenidos (CMS) WordPress en un clúster de Kubernetes de alta disponibilidad utilizando la distribución MicroK8s. La configuración permite una instalación autosuficiente en IaaS, con un balanceador de cargas interno y un clúster de Kubernetes. Incluye un servidor de base de datos MySQL y un servidor de archivos NFS para almacenamiento compartido. Aunque la implementación no incluye un dominio propio ni certificado SSL, sigue principios de escalabilidad y disponibilidad para entornos de producción.

### 1.1. Aspectos Cumplidos (Requerimientos Funcionales y No Funcionales)
- **Wordpress en Kubernetes con MicroK8s:** WordPress se despliega en un clúster de Kubernetes autosuficiente, utilizando múltiples réplicas para asegurar alta disponibilidad y escalabilidad. MicroK8s gestiona las réplicas y permite el autoescalado en función de la carga.
- **Balanceo de Cargas:** Se utiliza un balanceador de cargas integrado para distribuir el tráfico entre las réplicas de WordPress, logrando un reparto equilibrado y evitando la sobrecarga de instancias individuales.
- **Base de Datos MySQL:** La base de datos se gestiona mediante un contenedor MySQL, con integración directa a WordPress y capacidad de escalado según la demanda.
- **NFS:** Implementado para almacenamiento compartido, permitiendo a las réplicas de WordPress acceder de forma unificada a archivos y datos de usuario.

### 1.2. Aspectos No Cumplidos
- **Dominio del Sitio:** No se adquirió un dominio propio, por lo que la aplicación funciona en la dirección IP asignada por AWS, pero sin afectar la operatividad.
  
## 2.  Información General de Diseño de Alto Nivel
El sistema utiliza la orquestación de contenedores de Kubernetes en un entorno IaaS, permitiendo despliegues en clústeres locales y manteniendo la alta disponibilidad y escalabilidad de la aplicación mediante MicroK8s. El servicio de base de datos y almacenamiento se externaliza para optimizar el acceso a los datos.

### Arquitectura
- **Clúster Kubernetes (Microk8s):** MicroK8s gestiona las réplicas y permite una arquitectura escalable y de alta disponibilidad adaptada al entorno de IaaS.
- **Balanceador de Cargas:** Distribuye el tráfico entre las réplicas de la aplicación, optimizando recursos y previniendo sobrecarga en instancias individuales.
- **Base de Datos y NFS:** La base de datos y el sistema de archivos son externos a la aplicación, mejorando la escalabilidad y la administración de recursos de forma independiente.

## 3. Descripción del Ambiente de Desarrollo
El proyecto se desarrolló en un entorno Kubernetes utilizando MicroK8s, integrando servicios como base de datos, balanceo de cargas y sistemas de archivos compartidos.

### 3.1 Tecnologías y Versiones:
- `Kubernetes (Microk8s)`: latest
- `NFS`: 4.2
- `Docker`: 20.1

### 3.2 Detalles Técnicos
- Archivo de Configuración: En primer lugar, `mysql-secret.yaml` y `mysql-service.yaml` son utilizados por `mysql-deployment.yaml` para preparar y conectar todo dentro de la base de datos. Asimismo , el `wordpress-deployment.yaml` configurará el servicio y el despliegue del sitio, conectandose con la BD. Finalmente, el `wordpress-service.yaml` abrirá un punto de acceso externo al cluster para poder acceder al sitio, haciendo de LoadBalancer.
  
- Estructura de Directorios:
  
  ```
  ├── mysql-deployment.yaml
  ├── mysql-secret.yaml
  ├── mysql-service.yaml
  ├── wordpress-deployment.yaml
  └── wordpress-service.yaml
  ```

## 4. Guía de Uso
Para desplegar este proyecto, se requiere acceso al clúster de MicroK8s. Las configuraciones de la base de datos y almacenamiento se encuentran en los archivos YAML.

### 4.1 Imágenes del Proyecto

![1](https://github.com/user-attachments/assets/fa992472-f9fb-40c8-b0e8-8601aa99c788)

![2](https://github.com/user-attachments/assets/69e4e62e-d421-4f19-9474-74e257f13494)

![3](https://github.com/user-attachments/assets/d3ab6b67-f7f1-428a-a21e-82fa87459ebc)


### 4.4 [Video](https://youtu.be/BUln9XlLlu8)
 
## 5. Referencias:
- WordPress Foundation. (2024). WordPress documentation. Recuperado de https://wordpress.org/support/article/installation/
- Canonical Ltd. (2024). Documentación de MicroK8s. Recuperado de https://microk8s.io/docs
- Amazon Web Services, Inc. (2024). AWS documentation. Recuperado de https://docs.aws.amazon.com/
