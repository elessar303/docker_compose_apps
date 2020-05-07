FROM node:14-alpine

ENV NODE_ENV=${NODE_ENV}

#Editor nano para consola
RUN apk update && \
	apk add nano

# Crear directorio de trabajo
RUN mkdir -p /opt/app

# Se estable el directorio de trabajo
WORKDIR /opt/app/

# Instala los paquetes existentes en el package.json
COPY ./config/node/package.json .
RUN npm init -y
RUN npm install --quiet

COPY ${NODE_PROJECT_DIR} .
# Instalación de Nodemon en forma Global
# Al realizarse cambios reiniciar el servidor
RUN npm install nodemon -g --quiet

# Expone la aplicación en el puerto configurado en el .env
EXPOSE ${PORT_NODE}

# Inicia la aplicación al iniciar al contenedor
CMD nodemon -L --watch . app.js