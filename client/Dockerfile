FROM node:16 AS build_stage
#creates a workdir in /usr/src/app
WORKDIR /usr/src/app
#copies everything in my PWD to the WORKDIR/client
COPY package*.json ./      
#runs the command below
RUN npm install

COPY . .
RUN npm run build --prod

FROM nginx:latest
#copies stuff from the build context into the new nginx created
COPY --from=build_stage /usr/src/app/dist/ /usr/share/nginx/html
#this should copy the nginx.conf that now is in WORKDIR/client from line 5
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 4200
