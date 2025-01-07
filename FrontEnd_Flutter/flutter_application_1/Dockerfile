# Usar la imagen base de Flutter
FROM cirrusci/flutter:stable AS frontend

# Crear el usuario flutteruser
RUN useradd -m -s /bin/bash flutteruser && \
    mkdir -p /sdks/flutter/bin/cache && \
    chown -R flutteruser:flutteruser /sdks/flutter/bin/cache

# Establecer el directorio de trabajo
WORKDIR /home/flutteruser/app

# Cambiar permisos de todo el directorio de trabajo para evitar problemas de acceso
RUN chown -R flutteruser:flutteruser /home/flutteruser/app

# Cambiar a usuario flutteruser
USER flutteruser

# Configuración global de Git para evitar problemas de permisos y seguridad
RUN git config --global --add safe.directory /sdks/flutter

# Copiar solo los archivos esenciales para instalar dependencias
COPY pubspec.* ./

# Ejecutar flutter pub get para instalar dependencias
RUN flutter pub get

# Copiar el resto del código de la aplicación
COPY . .

# Ejecutar el build (no ejecutar flutter run en contenedor)
RUN flutter build web --release

# Exponer el puerto (si es necesario)
EXPOSE 8080

# Establecer el punto de entrada para servir la app
CMD ["flutter", "serve"]