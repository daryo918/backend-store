FROM node:17 as builder

WORKDIR /usr
COPY package.json ./
COPY tsconfig.json ./
COPY @types ./@types
COPY src ./src
RUN ls -a
RUN npm install
RUN npm run build


FROM node:17 
WORKDIR /usr
COPY package.json ./
RUN npm install --only=production
COPY --from=0 /usr/dist .
RUN npm install pm2 --location=global
EXPOSE 80:80
CMD ["pm2-runtime","index.js"]