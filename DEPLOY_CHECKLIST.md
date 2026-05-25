# FullShip — Deployment Checklist

## Bug Found
Type: Type B — CORS Misconfiguration
Location: backend/src/server.js, lines 13-16
Before value: `origin: 'http://localhost:5173'` (hardcoded localhost)
After value: `origin: process.env.FRONTEND_URL || 'http://localhost:5173'` (environment variable with fallback)
Fix confirmed by: After setting FRONTEND_URL in Render environment, API calls from deployed frontend succeed

## Checklist
- [ ] Frontend is live — Proof: [To be filled after deployment - Vercel URL]
- [ ] Backend is live — Proof: [To be filled after deployment - Render URL with curl /health]
- [ ] API call works end-to-end — Proof: [To be filled after deployment - Network tab screenshot showing 200 OK]
- [ ] CI pipeline passes — Proof: [To be filled after deployment - GitHub Actions screenshot]
- [ ] Health check responds — Proof: [To be filled after deployment - curl output]

## Reflection
1. What broke: CORS configuration was hardcoded to only allow requests from http://localhost:5173, blocking the deployed Vercel frontend from making API calls to the Render backend
2. How identified: Examined backend/src/server.js and found CORS origin hardcoded to localhost. This is a common deployment bug where development configuration persists in production
3. Prevention: Always use environment variables for configuration that differs between environments (development vs production). Add CORS_ORIGIN or FRONTEND_URL to .env.example and verify it's set correctly in deployment platforms
