FROM node:alpine as builder
WORKDIR /app
COPY ./package.json ./
RUN npm install
COPY ./ ./
RUN npm run build

FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
# copy the assets from the previous build process into nginx folder
COPY --from=builder /app/build /usr/share/nginx/html

CMD ["npm", "run", "start"]