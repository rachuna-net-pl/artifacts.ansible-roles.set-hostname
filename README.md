# <img src="docs/linux.png" alt="linux" height="20"/> set-hostname

Rola Ansible do ustawiania hostname'u serwera, aktualizacji wpisu 127.0.1.1 w `/etc/hosts`. Obsługuje systemy Debian, Ubuntu, AlmaLinux (EL 7/8/9) oraz Alpine.

## Co robi rola
- ustawia hostname na wartość FQDN lub krótki hostname (moduł `hostname`) – można pominąć, gdy host jest już ustawiony
- aktualizuje wpis `127.0.1.1` w `/etc/hosts` dla nowej nazwy
- opcjonalnie wymusza restart maszyny po zmianie (można wyłączyć)

## Wymagania
- Ansible 2.9+
- dostęp z uprawnieniami root (np. `become: true`)

## Zmienne
| Zmienna                          | Domyślna wartość           | Opis |
|----------------------------------|----------------------------|------|
| `in_hostname_fqdn`               | `{{ inventory_hostname }}` | Docelowy hostname/FQDN. Gdy zawiera kropkę, wpis w `/etc/hosts` zawiera hostname i FQDN. |
| `in_disable_reboot`              | `false`                    | `true` wyłącza reboot po zmianie hostname'u lub wpisu w `/etc/hosts`. |


## Użycie
Podstawowy playbook ustawiający hostname i wpis w `/etc/hosts`:

```yaml
- hosts: all
  become: true
  roles:
    - role: set-hostname
      vars:
        in_hostname_fqdn: app01.example.com
        in_disable_reboot: true  # pominie restart po zmianie
```

Zmiana hostname'u i wpisu w `/etc/hosts` wywołuje handler `Reboot system`. Jeśli chcesz uniknąć restartu (np. w środowisku testowym), ustaw `in_disable_reboot: true`.

---
## Contributions
Jeśli masz pomysły na ulepszenia, zgłoś problemy, rozwidl repozytorium lub utwórz Merge Request. Wszystkie wkłady są mile widziane!
[Contributions](CONTRIBUTING.md)

---
## License
Projekt licencjonowany jest na warunkach [Licencji MIT](LICENSE).

---
# Author Information
### &emsp; Maciej Rachuna
# <img src="docs/logo.png" alt="rachuna-net.pl" height="100"/>