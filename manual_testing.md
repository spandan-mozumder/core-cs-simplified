# 🧪 Manual Testing — Interview Questions & Answers

> Top Manual Testing / Software Testing interview questions with answers and examples.
> Source: [Intellipaat — Manual Testing Interview Questions](https://intellipaat.com/blog/interview-question/manual-testing-interview-questions/)

---

### Q1. What is Software Testing?

The process of evaluating software to identify **defects** and ensure it meets the specified requirements. It validates that the software works as expected.

---

### Q2. Verification vs Validation

| Verification                          | Validation                         |
| ------------------------------------- | ---------------------------------- |
| "Are we building it right?"           | "Are we building the right thing?" |
| Static testing (reviews, inspections) | Dynamic testing (executing code)   |
| Done before validation                | Done after verification            |
| Checks documents, design, code        | Checks the actual product          |

---

### Q3. SDLC vs STLC

| SDLC (Software Dev Life Cycle)               | STLC (Software Testing Life Cycle)                        |
| -------------------------------------------- | --------------------------------------------------------- |
| Requirements → Design → Code → Test → Deploy | Req Analysis → Plan → Design → Execute → Report → Closure |

**STLC Phases:**

1. Requirement Analysis
2. Test Planning
3. Test Case Design
4. Environment Setup
5. Test Execution
6. Test Closure

---

### Q4. Types of Testing

| Type                    | Description                                        |
| ----------------------- | -------------------------------------------------- |
| **Unit Testing**        | Individual components/functions                    |
| **Integration Testing** | Interaction between modules                        |
| **System Testing**      | Complete system end-to-end                         |
| **Acceptance Testing**  | Business requirements validation (UAT)             |
| **Regression Testing**  | Ensure changes don't break existing functionality  |
| **Smoke Testing**       | Quick check if build is stable for further testing |
| **Sanity Testing**      | Focused check on specific functionality after fix  |

---

### Q5. Black-Box vs White-Box vs Grey-Box

| Type          | Knowledge         | Tester              | Focus         |
| ------------- | ----------------- | ------------------- | ------------- |
| **Black-Box** | No code knowledge | QA                  | Functionality |
| **White-Box** | Full code access  | Developer           | Code coverage |
| **Grey-Box**  | Partial knowledge | QA with some access | Both          |

**Black-Box Techniques:**

- Equivalence Partitioning
- Boundary Value Analysis
- Decision Table Testing
- State Transition Testing

---

### Q6. Equivalence Partitioning & Boundary Value Analysis

```
Example: Age field accepts 18-60

Equivalence Partitioning:
- Valid: 18-60 (test with 30)
- Invalid: <18 (test with 10), >60 (test with 70)

Boundary Value Analysis:
- Test: 17, 18, 19, 59, 60, 61
- Boundaries are where bugs hide!
```

---

### Q7. Test Case vs Test Scenario

| Test Scenario  | Test Case                                                |
| -------------- | -------------------------------------------------------- |
| What to test   | How to test                                              |
| High-level     | Detailed with steps                                      |
| "Verify login" | Step 1: Open login page, Step 2: Enter valid username... |

**Test Case Template:**

| Field           | Example                                                     |
| --------------- | ----------------------------------------------------------- |
| Test Case ID    | TC-001                                                      |
| Title           | Verify login with valid credentials                         |
| Precondition    | User registered, on login page                              |
| Steps           | 1. Enter valid email 2. Enter valid password 3. Click Login |
| Expected Result | User redirected to dashboard                                |
| Actual Result   | (filled during execution)                                   |
| Status          | Pass/Fail                                                   |
| Priority        | High                                                        |
| Severity        | Critical                                                    |

---

### Q8. Severity vs Priority

| Feature | Severity                  | Priority                                |
| ------- | ------------------------- | --------------------------------------- |
| Meaning | Impact on system          | Business urgency                        |
| Set by  | Tester                    | Product Manager                         |
| Example | Crash = Critical severity | Logo typo = High priority, Low severity |

**Combinations:**

- High Severity, High Priority: App crashes on login
- High Severity, Low Priority: Feature crashes but rarely used
- Low Severity, High Priority: Company logo wrong on homepage
- Low Severity, Low Priority: Minor UI misalignment on settings page

---

### Q9. Defect Life Cycle

```
New → Assigned → Open → Fixed → Retest → Verified → Closed
                   ↓                  ↓
              Rejected          Reopen (if still broken)
```

**Bug Report Fields:**

- Bug ID, Title, Description
- Steps to Reproduce
- Expected vs Actual Result
- Severity, Priority
- Environment, Screenshots
- Assigned To, Status

---

### Q10. Regression Testing vs Retesting

| Regression Testing                    | Retesting                |
| ------------------------------------- | ------------------------ |
| Test entire application after changes | Test only the fixed bug  |
| Ensures no new bugs                   | Confirms bug is resolved |
| Can be automated                      | Usually manual           |

---

### Q11. Smoke Testing vs Sanity Testing

| Smoke Testing                         | Sanity Testing                 |
| ------------------------------------- | ------------------------------ |
| Broad, shallow testing                | Narrow, deep testing           |
| "Is the build stable?"                | "Is the specific fix working?" |
| Done on new builds                    | Done after receiving a fix     |
| Also called "Build Verification Test" | Subset of regression           |

---

### Q12. Test Plan Document

**Key Components:**

1. **Objectives** — What will be tested
2. **Scope** — In-scope and out-of-scope features
3. **Test Strategy** — Approach, types of testing
4. **Resources** — Team, tools, environments
5. **Schedule** — Timeline and milestones
6. **Entry/Exit Criteria** — When to start/stop testing
7. **Risk Assessment** — Potential issues and mitigation
8. **Deliverables** — Test reports, metrics

---

### Q13. Traceability Matrix

A document that maps **requirements** to **test cases** to ensure complete test coverage.

| Requirement             | Test Case(s)           | Status       |
| ----------------------- | ---------------------- | ------------ |
| REQ-001: User Login     | TC-001, TC-002, TC-003 | Covered      |
| REQ-002: Password Reset | TC-010, TC-011         | Covered      |
| REQ-003: Profile Edit   | —                      | Not Covered! |

---

### Q14. Exploratory Testing

An informal testing approach where testers **simultaneously learn, design, and execute** tests without predefined test cases.

**When to use:** New features, limited time, experienced testers, understanding the product.

**Session-based approach:** Fixed time (60-90 min), charter (focus area), debrief (findings).

---

### Q15. 7 Principles of Software Testing

| #   | Principle                                                 |
| --- | --------------------------------------------------------- |
| 1   | Testing shows the presence of defects, not absence        |
| 2   | Exhaustive testing is impossible                          |
| 3   | Early testing saves time and cost                         |
| 4   | Defects cluster together (80/20 rule)                     |
| 5   | Pesticide paradox — same tests find fewer bugs over time  |
| 6   | Testing is context-dependent                              |
| 7   | Absence of errors fallacy — bug-free ≠ successful product |

---

### Q16. Quality Assurance vs Quality Control vs Testing

| QA                        | QC                      | Testing            |
| ------------------------- | ----------------------- | ------------------ |
| Process-oriented          | Product-oriented        | Activity within QC |
| Prevention                | Detection               | Execution          |
| Ongoing                   | At specific checkpoints | During QC          |
| Everyone's responsibility | QC team                 | Testers            |

---

### Q17. Automated vs Manual Testing

| When Manual                | When Automated       |
| -------------------------- | -------------------- |
| Exploratory/ad-hoc testing | Regression testing   |
| Usability testing          | Smoke/sanity testing |
| One-time tests             | Repetitive tests     |
| Low budget                 | Long-term projects   |
| New/changing features      | Stable features      |

---

### Q18. Performance Testing vs Monkey Testing

| Performance Testing                 | Monkey Testing                    |
| ----------------------------------- | --------------------------------- |
| Tests speed, scalability, stability | Random inputs/actions             |
| Planned with specific scenarios     | Unplanned, chaotic                |
| Tools: JMeter, LoadRunner, Gatling  | Random clicking/typing            |
| Finds bottlenecks                   | Finds crashes/unexpected behavior |

---
