# frontend/Dockerfile
FROM node:16

WORKDIR /app

# Копируем файлы проекта
COPY package*.json ./

# Установка зависимостей
RUN npm install

COPY . .

# Сборка приложения
RUN npm run build

EXPOSE 8080
CMD ["npm", "run", "serve"]
