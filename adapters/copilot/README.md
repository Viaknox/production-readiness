# GitHub Copilot (VS Code) adapter

Copilot's agent mode loads skills from `.github/skills/` in your repository (see https://code.visualstudio.com/docs/agent-customization/agent-skills — verify the current path in the docs).

```bash
mkdir -p .github/skills
cp -r skills/production-readiness .github/skills/production-readiness
```

Then in Copilot Chat (agent mode): `run production readiness`.
