# <img src="https://github.com/Solvro/web-testownik/blob/main/public/favicon/180x180.png?raw=true" width="24"> Eventownik Mobile Legacy

> [!WARNING]
> To repozytorium zawiera starą wersję aplikacji. Nowa wersja aplikacji rozwijana jest w repozytorium [mobile-eventownik-v2](https://github.com/Solvro/mobile-eventownik-v2).

<div align="center">

![JavaScript](https://img.shields.io/badge/javascript-%23F7DF1E.svg?style=for-the-badge&logo=javascript&logoColor=black)
![Vue.js](https://img.shields.io/badge/vuejs-%2335495e.svg?style=for-the-badge&logo=vuedotjs&logoColor=%234FC08D)
![Pinia](https://img.shields.io/badge/pinia-%23ffe05d.svg?style=for-the-badge&logo=pinia&logoColor=black)
![Vite](https://img.shields.io/badge/vite-%23646CFF.svg?style=for-the-badge&logo=vite&logoColor=white)
![Cypress](https://img.shields.io/badge/-cypress-%23E9F1F7?style=for-the-badge&logo=cypress&logoColor=00BF88)
![Capacitor](https://img.shields.io/badge/capacitor-119EFF?style=for-the-badge&logo=capacitor&logoColor=white)
![Ionic](https://img.shields.io/badge/Ionic-3880FF?style=for-the-badge&logo=Ionic&logoColor=white)

</div>

## Uruchomienie lokalne

### Wymagania

- [Node.js](https://nodejs.org/)
- npm (dostarczany z Node.js)

### Instalacja

1. **Sklonuj repozytorium**

   ```bash
   git clone https://github.com/Solvro/mobile-eventownik.git
   cd mobile-eventownik
   ```

2. **Zainstaluj zależności**

   ```bash
   npm install
   ```

3. **Ustaw zmienne środowiskowe z URL do API**

   ```bash
   export VITE_API_URL='http://localhost:8000/api/'
   export VITE_WS_API_URL='ws://localhost:8000/'
   ```

4. **Uruchom serwer deweloperski** (upewnij się, że serwer API działa)

   ```bash
   ionic serve
   ```

## Testy E2E (Cypress)

1. Dodaj poniższe zmienne środowiskowe do serwera API, aby wyłączyć limity (throttling) dla testów:

   ```env
   ANON_THROTTLE_RATE = 'None'
   USER_THROTTLE_RATE = 'None'
   ```

2. W osobnym terminalu uruchom środowisko Cypress:

   ```bash
   npx cypress open
   ```

3. Upewnij się, że aplikacja kliencka działa równolegle (`ionic serve`).

## Dostępne skrypty

| Komenda            | Opis                                                  |
| ------------------ | ----------------------------------------------------- |
| `ionic serve`      | Uruchamia lokalny serwer deweloperski aplikacji       |
| `npm install`      | Instaluje wszystkie wymagane zależności projektu      |
| `npx cypress open` | Otwiera okno uruchomieniowe testów end-to-end Cypress |

## Stack technologiczny

### Frontend

- **Framework:** [Vue.js 3](https://vuejs.org/)
- **Stan globalny:** [Pinia](https://pinia.vuejs.org/)
- **Build Tool:** [Vite](https://vite.dev/)
- **Routing:** Vue Router

### UI & Mobile

- **Cross-platform Runtime:** [Capacitor](https://capacitorjs.com/)
- **UI Framework:** [Ionic](https://ionicframework.com/)

### Testy

- **E2E Testing:** [Cypress](https://www.cypress.io/)

---

## Licencja

Projekt jest udostępniany na warunkach licencji **AGPL (GNU Affero General Public License)**.

---

<div align="center">

Stworzone przez [KN Solvro](https://github.com/Solvro) dla studentów Politechniki Wrocławskiej

</div>
