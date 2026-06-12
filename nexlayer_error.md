# Nexlayer Build Failure Report

**Pipeline:** 19ebd8ae8e0
**Repository:** https://github.com/KatieHarris2397/-Flippy-WEb-App
**Error category:** 
**Error summary:** pipeline: image destination: app name "-Flippy-WEb-App" is not a valid registry path segment

## Build log
```

```

## Repository build artifacts

These are the actual files from the repository. Use these to understand how the project
is SUPPOSED to be built — do not rely solely on the broken Dockerfile below.

_No build artifact files were captured from the repository._


## Last attempted Dockerfile
```dockerfile
FROM mirror.gcr.io/library/nginx:alpine
COPY . /usr/share/nginx/html/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

## Last attempted nexlayer.yaml
```yaml
application:
  name: flippy-web-app
  pods:
    - name: frontend
      image: "# filled by pipeline"
      port: 80
```

## Instructions for frontier model

CRITICAL: Before writing any fix, read the repository build artifacts above and answer:
1. What language/runtime does this project use? (go.mod, package.json, pom.xml, Cargo.toml, requirements.txt)
2. What is the actual build command? (package.json scripts.build, Makefile targets, pom.xml goals, gradle tasks)
3. What is the actual start command? (package.json scripts.start, Makefile run target, Procfile)
4. What port does it serve? (EXPOSE, ENV PORT=, --port flag, framework default)
5. What dependencies does it need at runtime? (docker-compose.yml services, .env.example vars)

Then create a correct Dockerfile from scratch based on your analysis:
- All FROM base images must be standard public images (library/, gcr.io, ghcr.io, etc.)
- Use `mirror.gcr.io/library/` prefix for Docker Hub official images (node:*, python:*, golang:*, etc.)
- DO NOT copy broken steps from the "last attempted Dockerfile" — build from what the repo actually needs

Fix nexlayer.yaml if needed:
- Inter-pod service references MUST use `${podName:port}` template syntax
- Example: `DATABASE_URL: postgresql://user:pass@${postgres:5432}/db`

Create a file named `nexlayer_fix.md` on THIS branch (`nexlayer`) with this structure:

---
# Nexlayer Fix

## Fixed Dockerfile
```dockerfile
<your fixed Dockerfile>
```

## Fixed nexlayer.yaml
```yaml
<your fixed nexlayer.yaml>
```

## Notes
<explain: what build command you found, what was wrong with the previous Dockerfile, what you changed and why>
---

Nexlayer detects `nexlayer_fix.md` on the next pipeline run and applies your fixes automatically.
