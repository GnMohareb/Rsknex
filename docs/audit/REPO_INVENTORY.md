# Rsknex Repo Inventory (G0)

- Commit: 531b23972f98789d6c64a6e42521b5a826f35eb8
- Branch: assessment/canadian-cu-foundation
- Date: 2026-11-01
- Foundation: SimpleRisk release mirror (MPL 2.0), commit adeccbe41

## Stack
- PHP 8.4.20 (CLI verified). Web server: Apache via Laragon (available).
- Database: MySQL/MariaDB expected by SimpleRisk; Laragon mysql dir present but no mysqld binary installed (BLOCKER: install MySQL).
- No composer.json detected at root. Dependencies vendored under simplerisk/vendor and simplerisk/includes.

## Top-level
- simplerisk/ : application root (index.php, header/footer, sidebar)
- docs/: assessment + (new) audit/architecture/...
- .github/: workflows
- KILO_MASTER_IMPLEMENTATION_DIRECTIVE.md

## Key application areas (simplerisk/)
- account, admin, api, artificial_intelligence, assessments, compliance, cron, governance, incidents, management, reports, resources, search, vulnerabilities, vendor.

## Counts
- Total files: 25655
- PHP files: 10844

## Verified/unverified
- Local PHP runtime: VERIFIED
- DB server: NOT VERIFIED (no mysqld) — BLOCKER
- Clean install: NOT YET (pending DB)
- License: MPL 2.0 (simplerisk/LICENSE) — VERIFIED
- Vendor dependency licenses: NOT YET INVENTORIED
