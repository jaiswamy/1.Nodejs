FROM node:22

WORKDIR /app

# Install dependencies first (layer caching)
COPY package.json package-lock.json ./

# Clean up cache and remove node_modules for a fresh install
RUN rm -rf node_modules package-lock.json

# Reinstall dependencies (this will regenerate the package-lock.json)
RUN npm install

# Clean npm cache to avoid leftover issues
RUN npm cache clean --force

# Rebuild the app and install global tools
RUN npm rebuild
RUN npm install -g vite

# Copy the rest of the app
COPY . .

# Build the project with vite
RUN npx vite build

# Install serve locally to avoid global installation issues
RUN npm install serve

EXPOSE 3000

CMD ["npx", "serve", "-s", "dist", "-l", "3000"]