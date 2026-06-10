# Where We Are Today

<p class="doc-lead">An honest baseline of the Parttime platform before multi-tenant hardening. We support multiple organizations at the <strong>business level</strong> — not yet at the <strong>platform architecture level</strong>.</p>

<div class="doc-bridge" markdown="1">

:material-arrow-left: [Back to overview](index.md) · [Skip to proposed approach →](index.md#5-our-proposed-approach)

</div>

---

## Current architecture

```mermaid
flowchart TB
    subgraph today [Current State]
        User[User logs in]
        JWT[Custom JWT - no tenant claim]
        UI[HQ Dashboard selects Organization]
        API[API calls - org ID in URL/body]
        AuthZ[Per-endpoint AuthorizationService checks]
    end

    User --> JWT --> UI --> API --> AuthZ
```

<div class="doc-status-grid" markdown="1">

<div class="doc-status-card doc-status-card--have" markdown="1">

### What we have

- Spring Boot microservices: `common`, `job`, `notification`, `log`, `apigw`
- PostgreSQL — separate DB per service, shared schema
- **Organization → Branch → Employee** hierarchy
- Custom JWT auth (HS256, issued by `common`)
- Org selected in HQ dashboard (client-side, localStorage)
- `AuthorizationService` roles (ADMIN, OWNER, MANAGER, etc.)

</div>

<div class="doc-status-card doc-status-card--partial" markdown="1">

### Partial patterns

- `document-builder` requires `tenant_alias` header; filters templates by tenant
- `job` passes organization ID as `tenant_alias` for contract generation

</div>

<div class="doc-status-card doc-status-card--gap" markdown="1">

### Gaps

- No platform-wide tenant context in tokens
- No systematic row-level isolation across services
- Keycloak not in production (KC 20 Docker + React demo only)
- Tenant propagation beyond document-builder

</div>

</div>

!!! success "Key message for leadership"
    The org picker in HQ is good UX. The gap is making that choice **authoritative in the security token** and enforced in every service.

<div class="doc-bridge" markdown="1">

:material-arrow-right: **Next** — [Our proposed approach](index.md#5-our-proposed-approach)

</div>
