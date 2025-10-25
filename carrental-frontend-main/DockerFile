# Step 1: Build the React app using Node
FROM node:18 AS build

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the frontend code
COPY . .

# Build the production-ready files
RUN npm run build


# Step 2: Run the production build using a lightweight Node.js server
FROM node:18-alpine

WORKDIR /app

# Copy build files from the previous stage
COPY --from=build /app/dist ./dist

# Install serve package globally to serve static files
RUN npm install -g serve

# Expose port (default Vite dev port is 5173)
EXPOSE 5173

# Command to run the app
CMD ["serve", "-s", "dist", "-l", "5173"]
