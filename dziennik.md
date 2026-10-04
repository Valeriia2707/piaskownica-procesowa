# Dziennik laboratoryjny — Temat 1: Piaskownica procesowa w Linuksie

## Eksperyment 1: Izolacja procesów (PID namespace)
- **Polecenie:** `sudo unshare --pid --fork --mount-proc bash` oraz `ps aux`
- **Obserwacje:** Wewnątrz nowej przestrzeni nazw widoczne były tylko dwa procesy (`bash` z PID 1 oraz `ps aux` z PID 8).
- **Wnioski:** Nowy PID namespace całkowicie izoluje proces od reszty systemu. Proces wewnątrz widzi siebie jako PID 1 i nie ma dostępu do procesów działających na hoście.

## Eksperyment 2: Ograniczenie zasobów (cgroups)
- **Polecenie:** `systemd-run --user --scope -p MemoryMax=100M bash` oraz `yes | head -c 500M > /dev/shm/x`
- **Obserwacje:** Proces generowania danych został natychmiast zatrzymany komunikatem `Killed`.
- **Wnioski:** Mechanizm cgroups skutecznie pilnuje limitu pamięci 100 MB. Próba alokacji 500 MB spowodowała zabicie procesu przez OOM Killer.

## Podział ról w zespole
- **Valeriia Koval:** konfiguracja środowiska wirtualnego, implementacja mechanizmów izolacji (namespaces, cgroups).
- **Darya Drozd:** prowadzenie dokumentacji, opracowanie scenariuszy testowych, przygotowanie prezentacji wyników.

## Plan na najbliższe 2 tygodnie
1. Tydzień 1:
   - Utworzenie wspólnego repozytorium GitHub i synchronizacja środowisk.
   - Opracowanie skryptu tworzącego piaskownicę z użyciem kolejnych przestrzeni nazw (`mnt`, `net`, `uts`).
2. Tydzień 2:
   - Konfiguracja reguł cgroups v2 do limitowania CPU i pamięci.
   - Wdrożenie podstawowych filtrów `seccomp`.
   - Przygotowanie raportu z testów bezpieczeństwa.
