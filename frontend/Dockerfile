# Build stage
FROM node:18-bullseye AS build

WORKDIR /app

# Copy package files
COPY frontend/package*.json ./

# Install dependencies
RUN npm install

# Copy source code
COPY frontend/ ./

# Build arguments for environment variables
ARG VITE_API_URL
ARG VITE_WS_URL

ENV VITE_API_URL=$VITE_API_URL
ENV VITE_WS_URL=$VITE_WS_URL

# Build for production (skipping type check for faster containerization)
RUN npx vite build

# Production stage
FROM nginx:stable-alpine

# Copy built files from build stage
COPY --from=build /app/dist /usr/share/nginx/html

# Copy nginx configuration
COPY ModelData3d/frontend/nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
