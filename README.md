# Dequest-legacy-vault-services:
  - type: web
    name: legacy-vault-backend
    runtime: node
    buildCommand: cd backend && npm install
    startCommand: cd backend && npm start
    envVars:
      - key: NODE_ENV
        value: production
      - key: PORT
        value: 10000
      - key: JWT_SECRET
        generateValue: true
      - key: DATABASE_URL
        fromDatabase:
          name: legacy-vault-db
          property: connectionString

  - type: web
    name: legacy-vault-frontend
    runtime: static
    buildCommand: cd frontend && npm install && npm run build
    staticPublishPath: ./frontend/build
    envVars:
      - key: REACT_APP_API_URL
        value: https://legacy-vault-backend.onrender.com

databases:
  - name: legacy-vault-db
    databaseName: legacyvault
    user: legacyvault
    plan: free
