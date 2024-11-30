# Health Insurance Smart Contract

This Clarity smart contract provides functionalities for managing health insurance and automating claims processing. It enables insurers to register insurance plans, patients to submit claims, and insurers to approve claims in a decentralized manner.

---

## Features

1. **Insurance Management**  
   - Register health insurance with a specified coverage amount.
   - Verify insurance status, including coverage amount and activation status.

2. **Claims Processing**  
   - Submit claims against active insurance plans.
   - Approve submitted claims (insurer-only action).

3. **Error Handling**  
   Standardized error codes for improved clarity:
   - `u100`: Insurance not found.
   - `u101`: Claim exceeds coverage or insurance is inactive.
   - `u102`: Claim not found.
   - `u103`: Self-approval of claims is not allowed.
   - `u104`: Invalid coverage amount.
   - `u105`: Invalid claim ID.

---

## Contract Functions

### Public Functions

1. **`register-insurance (coverage-amount uint)`**  
   Registers a health insurance plan for the caller with the specified coverage amount.  
   - **Parameters**:  
     - `coverage-amount`: Positive integer representing the coverage amount.  
   - **Returns**:  
     - `"Insurance registered successfully"` on success.  
     - `ERR_INVALID_COVERAGE` if the coverage amount is invalid.  

2. **`submit-claim (claim-amount uint)`**  
   Submits a claim for processing if the caller's insurance is active and sufficient.  
   - **Parameters**:  
     - `claim-amount`: Positive integer representing the claim amount.  
   - **Returns**:  
     - Claim ID and status tuple on success.  
     - `ERR_CLAIM_EXCEEDS_COVERAGE` or `ERR_INSURANCE_NOT_FOUND` on failure.  

3. **`approve-claim (claim-id uint)`**  
   Approves a claim submitted by another user.  
   - **Parameters**:  
     - `claim-id`: Positive integer representing the claim ID.  
   - **Returns**:  
     - `"Claim approved"` on success.  
     - `ERR_INVALID_CLAIM_ID`, `ERR_CLAIM_NOT_FOUND`, or `ERR_SELF_APPROVE` on failure.  

### Read-Only Functions

1. **`get-insurance-status (user principal)`**  
   Retrieves the insurance status for the specified user.  
   - **Parameters**:  
     - `user`: The user's principal address.  
   - **Returns**:  
     - Insurance data or `ERR_INSURANCE_NOT_FOUND` if no insurance is found.  

2. **`get-claim (claim-id uint)`**  
   Retrieves claim details for the specified claim ID.  
   - **Parameters**:  
     - `claim-id`: The ID of the claim.  
   - **Returns**:  
     - Claim data or `ERR_CLAIM_NOT_FOUND` if the claim does not exist.  

---

## Data Structures

### Data Variables
- `insurance-plans-counter`: Counter for tracking insurance plan registrations.
- `claims-counter`: Counter for tracking submitted claims.

### Data Maps
- `insurance-plans`: Maps a user's principal to their insurance details:  
  - `coverage-amount`: Maximum coverage available.  
  - `is-active`: Boolean indicating whether the insurance is active.  
- `claims`: Maps claim IDs to claim details:  
  - `patient`: The claim submitter's principal address.  
  - `claim-amount`: The claim amount requested.  
  - `approved`: Boolean indicating whether the claim is approved.  

---

## Error Codes

| Code  | Description                               |
|-------|-------------------------------------------|
| `u100`| Insurance not found.                     |
| `u101`| Claim exceeds coverage or insurance inactive. |
| `u102`| Claim not found.                         |
| `u103`| Self-approval of claims is not allowed.  |
| `u104`| Invalid coverage amount.                 |
| `u105`| Invalid claim ID.                        |

---

## Setup Instructions

1. **Install Clarity Tools**  
   Ensure you have the necessary environment to deploy Clarity contracts.

2. **Deploy the Contract**  
   Use a Clarity-compatible IDE or CLI to deploy this contract.

3. **Interact with the Contract**  
   Utilize a Clarity REPL or front-end application to interact with the functions.

---

## Future Enhancements

- Add premium payment tracking.
- Automate fund allocation for approved claims.
- Include a role-based access control system for insurers.

---

This contract ensures transparency and efficiency in health insurance management through decentralized solutions.