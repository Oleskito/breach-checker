# Raport Bezpieczeństwa Projektu

## Informacje o skanie
* **Data skanu:** 19.11.2026
* **Narzędzie i wersja:** Trivy 0.76.0

## Tabela podatności obrazów

| Obraz | Rozmiar | Podatności HIGH / CRITICAL (wszystkie) | Podatności HIGH / CRITICAL (z poprawką - fixed) |
| :--- | :--- | :--- | :--- |
| `breach-checker-backend:dev` | 230 MB | 48 (48 HIGH, 0 CRITICAL) | 1 (1 HIGH, 0 CRITICAL) |
| `breach-checker-backend:prod` | 212 MB | 48 (48 HIGH, 0 CRITICAL) | 1 (1 HIGH, 0 CRITICAL) |
| `breach-checker-frontend:przed` | 225 MB | 0 | 0 |
| `breach-checker-frontend:prod` | 93.7 MB | 0 | 0 |

## Decyzja i podsumowanie
Zastosowano wieloetapowe budowanie obrazu frontendu (multi-stage build), redukując jego rozmiar z 225 MB do 93.7 MB i eliminując narzędzia Node.js/npm ze środowiska produkcyjnego, a także przebudowano oba obrazy produkcyjne z flagą `--pull` na najnowszych wersjach obrazów bazowych. W obrazie backendu (`python:3.12-slim`) zidentyfikowano 48 podatności poziomu HIGH, z czego 47 nie posiada obecnie dostępnej poprawki w oficjalnych repozytoriach Debiana (status *unfixed*). Jedyna podatność z dostępną łatką (w bibliotece `zlib1g`) oczekuje na wdrożenie w nowym wydaniu obrazu bazowego przez zespół Pythona. Następny skan bezpieczeństwa zaplanowano w cyklu miesięcznym lub po publikacji nowych wersji obrazów bazowych w rejestrze Docker Hub.
