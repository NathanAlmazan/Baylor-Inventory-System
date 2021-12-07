FROM node:14

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install --production

COPY . .

ENV DATABASE_URL="postgresql://bayloradmin:b4yl0rtr4d1ng@172.19.0.2:5432/baylor_company?schema=public"
ENV SECRET_KEY="wyIJ2wMLRTNw9CPSTjblem39iFa2fxScnw3L4Zzy"
ENV DATABASE_NAME="baylor_company"
ENV DATABASE_HOST="172.19.0.2"
ENV DATABASE_USER="bayloradmin"
ENV DATABASE_PASSWORD="b4yl0rtr4d1ng"
ENV DATABASE_PORT="5432"
ENV FRONTEND_SECRET="INp8IvdIyeMcoGAgFGo8IvdIyeMcoGAgFGo8IvdIyeMcoGAgFGogFGo8IvdIyeMco"

RUN npx prisma generate

EXPOSE 4000

CMD [ "npm", "start" ]

