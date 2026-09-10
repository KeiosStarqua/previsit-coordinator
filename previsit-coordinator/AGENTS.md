# PreVisit Coordinator Backend

- Spring Boot application managing the intake case lifecycle, appointment slot scheduling, emergency staff alerts, and clinic pre-visit coordination endpoints.

## Purpose

Provide REST API endpoints and business logic for:
- Creating and retrieving pre-visit intake cases.
- Recording intake submissions and detecting emergency red flags.
- Approving scheduling, proposing slots, and confirming appointments.
- Managing staff alerts and alert resolutions for halted cases.

## Ownership

- Java source code under `src/main/java/com/previsitcoordinator/` and test cases under `src/test/java/com/previsitcoordinator/`.
- Build definitions in `pom.xml`.

## Local Contracts

- Built with Spring Boot 4.x and Java 25.
- Adhere strictly to the non-diagnostic safety boundary: never attempt clinical diagnosis or triage.
- If `emergencyFlag` is `true` in an intake submission:
  - Transition intake case status to `SCHEDULING_HALTED`.
  - Create a durable `StaffAlert` record for staff visibility.
  - Halt all appointment slot proposals and confirmation.
- In non-emergency flow:
  - Case advances from `INTAKE_COMPLETE` to `SCHEDULING_APPROVED`.
  - Exactly one slot is proposed (`SLOT_PROPOSED`).
  - Appointment is created ONLY when explicit confirmation (`true`) is provided for the exact proposed slot.
- Respect domain terminology from root `AGENTS.md` and `CONTEXT.md`.

## Work Guidance

- Code structure:
  - Controller layer: handles REST request/response contracts and validation (`IntakeCaseController`, `StaffAlertController`, `HealthController`).
  - Service layer: in-memory state coordination and business constraints (`IntakeCaseService`).
  - Gateway layer: simulated provider appointment availability (`MockAppointmentGateway`, `AppointmentGateway`).
  - Domain models: request DTOs, response records, entities, and enums under `com.previsitcoordinator.intake`.
- Keep in-memory data structures thread-safe where applicable.

## Verification

- Run unit and integration tests covering the endpoint layer:
  - `HealthEndpointTest`
  - `IntakeCaseEndpointTest`
- If Maven is installed locally or in CI, verify with:
  ```bash
  mvn test
  ```

## Child DOX Index

(No child modules exist under `previsit-coordinator/`)
