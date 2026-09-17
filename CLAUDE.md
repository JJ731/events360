# Project — Claude Instructies

## Werkwijze — uitvoeren zonder toestemming vragen

Voer handelingen direct uit zonder eerst te vragen "mag ik X?". Ga ervan uit dat de gebruiker ja zegt op alles wat veilig is. Dit geldt voor:

- Bestanden aanmaken, bewerken, verwijderen (binnen projectscope)
- Commits en pushes naar GitHub
- Installaties (npm, packages)
- Deploys van goedgekeurde projecten
- Cache opschonen, scripts draaien
- Instellingen aanpassen (settings.json, .gitignore, e.d.)
- Alles wat omkeerbaar is of beperkte blast radius heeft

**Wel voorleggen (kort uitleggen + wachten):**

- Force-push naar main
- `rm -rf` buiten project- of cache-mappen
- Acties die secrets of credentials kunnen lekken
- Irreversibele data-mutaties in productie-databases
- Acties met grote blast radius buiten het huidige project
- Iets dat de gebruiker waarschijnlijk niet verwacht

## Git worktrees — altijd binnen de repo

- Tijdelijke werkmappen (parallelle sessies, losse fixes) **alleen** onder `.worktrees/` in deze repo, nooit naast de repo in `Documents`:
  `git worktree add .worktrees/<korte-naam> -b claude/<branch>`
- `.worktrees/` staat in `.gitignore`. Tools die zelf de hele repo doorlopen (lint, typecheck, build) moeten `.worktrees/` overslaan.
- Na merge opruimen: `git worktree remove .worktrees/<korte-naam>`, `git branch -d claude/<branch>` en `git worktree prune`. Geen lege of verlaten werkmappen achterlaten.
