# PET-8: malformed owner id / request body returned 500

- Signature: MethodArgumentTypeMismatchException (also PET-5/PET-6 HttpMessageNotReadableException, PET-7)
- Root cause: no handler in ExceptionControllerAdvice, catch-all returned 500 and logged ERROR
- Fix: one handler returning 400 problem details, WARN log
- Tests: OwnerRestControllerBadRequestTests (2), failed before (500), pass after; full suite green; no existing tests modified
- PR: https://github.com/hrka-demo/spring-petclinic-rest/pull/1 (merged by human, master 6296ce7)
- Closed loop: redeployed, 400 + WARN, no ERROR in Loki; PET-5..8 Done
