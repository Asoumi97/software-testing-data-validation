# Software Testing & SQL Data Validation

## Overview

This repository demonstrates software testing and data validation concepts based on experience gained while working with internal web applications.

The focus is on software verification, automated testing, and SQL-based data validation in applications using TypeScript and NestJS.

The examples in this repository are simplified and use generic data structures. Original source code and business data cannot be published due to confidentiality agreements.

> **Confidentiality Notice**
>
> This repository does not contain proprietary source code, database structures, or business data.
> All examples were recreated for demonstration purposes.

---

## Project Focus

The main focus was the verification of application functionality and data consistency across different application layers.

Key areas included:

- Unit testing
- Integration testing
- End-to-end testing
- SQL-based data validation
- Data consistency checks
- Error analysis
- Verification planning

---

## Software Testing

The application was verified using multiple testing levels:

- **Unit Tests** – Testing individual services and functions
- **Integration Tests** – Verifying interactions between application components
- **End-to-End Tests** – Testing complete application flows and API behavior
- **SQL Validation** – Verifying application results directly against stored database data

---

## End-to-End Testing

End-to-end tests were used to verify complete application flows and API behavior.

Example:

```typescript
describe('Users API (e2e)', () => {
  it('/users (GET)', () => {
    return request(app.getHttpServer())
      .get('/users')
      .expect(200)
      .expect('Content-Type', /json/);
  });
});
```

E2E testing helps ensure that multiple application components work correctly together.

---

## Unit Testing

Unit tests were used to verify individual services and application functions.

Example:

```typescript
describe('UserService', () => {
  let service: UserService;

  beforeEach(async () => {
    const module = await Test.createTestingModule({
      providers: [UserService],
    }).compile();

    service = module.get<UserService>(UserService);
  });

  it('should return a user', async () => {
    const result = await service.findOne(1);

    expect(result).toBeDefined();
  });
});
```

---

## SQL & Data Validation

SQL queries were used to validate application data and support error analysis.

Typical validation tasks included:

- Checking data consistency
- Identifying missing records
- Detecting duplicate data
- Comparing application output with database records
- Supporting root cause analysis

Example consistency check:

```sql
SELECT
    u.id,
    u.email
FROM users u
LEFT JOIN profiles p
    ON u.id = p.user_id
WHERE p.user_id IS NULL;
```

The query identifies records without corresponding related data.

Example duplicate check:

```sql
SELECT
    email,
    COUNT(*) AS duplicate_count
FROM users
GROUP BY email
HAVING COUNT(*) > 1;
```

---

## Verification Approach

The verification process followed a structured approach:

1. Analyze application requirements
2. Define relevant test scenarios
3. Create test objects and test data
4. Execute unit and integration tests
5. Perform end-to-end testing
6. Validate application results using SQL
7. Analyze inconsistencies and errors
8. Document verification results

---

## Repository Structure

```text
src/
├── testing/
│   ├── unit/
│   │   └── user.service.spec.ts
│   ├── integration/
│   │   └── user.integration.spec.ts
│   └── e2e/
│       └── application.e2e-spec.ts
│
└── sql/
    ├── data-validation.sql
    ├── consistency-check.sql
    └── error-analysis.sql
```

---

## Technologies & Skills

- TypeScript
- NestJS
- SQL
- Jest
- Unit Testing
- Integration Testing
- End-to-End Testing
- Data Validation
- Error Analysis
- Software Verification

---

## Key Skills Demonstrated

- Designing structured test scenarios
- Writing automated tests with TypeScript
- Testing NestJS application components
- Performing end-to-end API tests
- Validating application data using SQL
- Identifying data inconsistencies
- Supporting systematic error analysis
