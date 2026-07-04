# Module 22 — Plugin Ecosystem

## Goal
Learn how to manage IntelliJ plugins safely and productively.

You will learn what plugins are, bundled vs Marketplace plugins, install/disable/uninstall/update, required plugins, performance/security impact, recommended plugins, and what to avoid.

## What Is a Plugin?

A plugin adds functionality to IntelliJ IDEA.

Examples:

```text
Docker support
Database tools
Markdown support
YAML support
Spring support
Kubernetes support
Security scanning
AI assistance
Themes
Language support
```

## Bundled vs Marketplace Plugins

| Type | Meaning |
|---|---|
| Bundled | Comes with IntelliJ |
| Marketplace | Installed separately |

Useful plugin areas:

```text
Git
Maven
Gradle
Terminal
HTTP Client
Docker
Database Tools and SQL
Package Checker
Markdown
YAML
```

## Open Plugin Settings

```text
Settings / Preferences → Plugins
```

Shortcuts:

```text
Mac: Cmd + ,
Windows/Linux: Ctrl + Alt + S
```

Tabs:

```text
Marketplace
Installed
Updates
```

## Marketplace Practice

Search:

```text
Markdown
Docker
Database Tools and SQL
Package Checker
CSV
YAML
Snyk
```

Check:

```text
Plugin name
Vendor
Downloads
Rating
Last updated
Compatibility
Description
Permissions/behavior
```

## Installed Tab

Search:

```text
Maven
Gradle
Git
Docker
Database
Package Checker
Markdown
YAML
HTTP Client
Spring
```

Do not disable core plugins randomly.

## Enable/Disable Practice

Only use a non-critical plugin.

```text
Settings → Plugins → Installed → Disable/Enable → Restart if requested
```

Avoid disabling:

```text
Java
Maven
Gradle
Git
Spring
Database Tools
Docker
Terminal
HTTP Client
```

## Updates

Open:

```text
Settings → Plugins → Updates
```

Good habit:

```text
Update regularly, but avoid mass updates during urgent work.
```

## Required Plugins

Open:

```text
Settings → Build, Execution, Deployment → Required Plugins
```

Useful for team projects.

## Recommended Plugins/Features

| Plugin/Feature | Why |
|---|---|
| Maven | Dependencies/build |
| Gradle | Dependencies/build |
| Git | Version control |
| Docker | Containers |
| Database Tools and SQL | DB browsing/query |
| Package Checker | Vulnerable dependency review |
| Markdown | Docs |
| YAML | Docker/config |
| HTTP Client | API testing |
| Spring | Spring Boot productivity |

## Security Plugins

Explore later:

```text
Package Checker
Snyk Security
Qodana
Black Duck Code Sight
```

Rule:

```text
Do not install security plugins into company projects without approval.
```

## Plugin Security Checklist

```text
1. Trusted vendor?
2. Known company/JetBrains?
3. Actively maintained?
4. Compatible with IDE?
5. Needs project file access?
6. Sends data externally?
7. Allowed by company policy?
8. Built-in feature already exists?
9. Really needed?
10. Easy to remove?
```

## Performance

Too many plugins can cause:

```text
Slow startup
Slow indexing
High memory
Slow completion
IDE freezes
```

## Practice Files

Create `README-practice.md`:

```markdown
# IntelliJ Plugin Practice

## Useful Plugins
- Maven
- Gradle
- Git
- Docker
- Database Tools and SQL
- Package Checker
- Markdown
- YAML
- HTTP Client

## Security Rule
Install only trusted plugins and avoid unnecessary plugins in company projects.
```

Open `docker-compose.yml` and check YAML support.

Open Database and Vulnerable Dependencies windows if available.

## Assignment

```text
1. Open Settings → Plugins
2. Review Marketplace
3. Review Installed
4. Search major plugins
5. Confirm important plugins enabled
6. Open Updates
7. Review Required Plugins
8. Create README-practice.md
9. Test Markdown preview
10. Check YAML support
11. Open Database tool window
12. Open Vulnerable Dependencies
13. Review one Marketplace plugin vendor/downloads/rating
14. Disable/re-enable non-critical plugin
15. Remove test plugin
16. Write plugin safety checklist
```

When done, reply:

```text
Module 22 completed
```
