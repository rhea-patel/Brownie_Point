# Brownie Point

Brownie Point is a full-stack course engagement app:
- **Backend:** Spring Boot API with JWT-based auth, role-aware access, course management, student enrollment, and points tracking.
- **Frontend:** React Native mobile app using Redux + Redux-Saga to call the API and render teacher/student workflows.

## Repository structure

- `backend/` — Spring Boot (Java 17) service.
- `frontend/` — React Native mobile app.
- `Dockerfile` — containerization scaffold.

## Backend architecture

- **Entrypoint:** `BpaApplication`.
- **API layer:** controllers under `backend/src/main/java/com/GRP3/BPA/controller/`.
- **Service layer:** business logic under `.../service/`.
- **Persistence layer:** JPA entities in `.../model/` and repositories in `.../repository/`.
- **Security:** JWT filter/config in `.../config/` and token helpers in `.../service/JwtService.java` and `.../utils/JWTAuthenticationUtil.java`.

### Main domain concepts

- `User` with role (`ROLE_TEACHER` / `ROLE_STUDENT`).
- `Teacher` and `Student` are role-specific models tied to users.
- `Course` belongs to a teacher.
- `CourseStudent` links a student to a course and stores points.

### API areas (high-level)

- `/api/auth/*` — login/register/reset-password.
- `/api/user` — current user details.
- `/api/teachers/courses/*` — course CRUD + roster actions.
- `/api/teachers/points/*` — point increment + points queries.

## Frontend architecture

- **App root and navigation:** `frontend/src/App.js`.
- **State management:** Redux store in `frontend/src/redux/index.js`, combined reducers in `.../reducers.js`, and root saga in `.../saga.js`.
- **Feature slices:** `redux/user`, `redux/course`, `redux/student`, `redux/points` each contain actions/reducer/saga.
- **API client:** `frontend/src/config/Axios.js` injects bearer token from async storage.
- **Screens:** role-oriented screens under `frontend/src/Screens/Teacher` and `frontend/src/Screens/Student`.

## Local development quick start

### Backend

```bash
cd backend
./mvnw spring-boot:run
```

### Frontend

```bash
cd frontend
npm install
npm run start
npm run android   # or npm run ios
```

## Tests

### Backend tests

```bash
cd backend
./mvnw test
```

### Frontend tests

```bash
cd frontend
npm test
```

## Newcomer learning path

1. Start with `frontend/src/App.js` to understand role-based navigation.
2. Trace one complete flow in frontend sagas (e.g., login or add course).
3. Follow the matching backend controller and service for that flow.
4. Review security config and JWT filter to understand auth boundaries.
5. Run tests to see expected behavior and current assumptions.

## Notes

- `backend/src/main/resources/application.properties` currently contains environment-specific credentials and should be externalized for production use.
