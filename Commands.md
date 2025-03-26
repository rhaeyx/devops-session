Commands

Do this inside the previously provided docker container.

`docker run -it -p 3000:3000 --privileged -v /var/run/docker.sock:/var/run/docker.sock devops-session`

`node --version`
`npm --version`
`docker --version`

`git --version`
`apt-get install -y git`
`git --version`

`git clone https://github.com/SAMAHAN-Systems-Development/FYLP-frontend-2024.git`

`cd FYLP-frontend-2024`
`npm i`
`npm run build`

`npm i -g pm2`
`pm2 start npm --name FYLP-frontend-2024 -- run start`
`pm2 list`

Commands for Dockerization

Do this in your local machine.

`git clone https://github.com/SAMAHAN-Systems-Development/FYLP-frontend-2024.git`

create Dockerfile and paste this

```
# Stage 1: Build
FROM node:18-alpine AS builder

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package.json package-lock.json ./

# Install dependencies
RUN npm install --frozen-lockfile

# Copy the rest of the application
COPY . .

# Build the Next.js app
RUN npm run build

# Remove dev dependencies (optional)
RUN npm prune --production

# Stage 2: Production
FROM node:18-alpine

# Set working directory
WORKDIR /app

# Copy built application from builder stage
COPY --from=builder /app/package.json ./
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/.next ./.next
COPY --from=builder /app/public ./public

# Expose the default Next.js port
EXPOSE 3000

# Start the Next.js application
CMD ["npm", "run", "start"]
```

`docker build -t fylp-2024 .`

`docker run -p 3000:3000 --name fylp-2024-app fylp-2024`
