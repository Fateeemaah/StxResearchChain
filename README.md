# STXResearchChain: Collaborative Research Funding Smart Contract

## Overview
STXResearchChain is a decentralized funding mechanism for research projects built on the Stacks blockchain. This smart contract allows researchers to propose projects, receive funding from the community, and mark projects as completed once fully funded.

## Features
- **Propose Research Projects**: Researchers can submit their projects, specifying title, description, and required funding.
- **Fund Research Projects**: Community members can contribute funds to proposed projects.
- **Complete Research Projects**: Researchers can mark projects as completed once fully funded.
- **Automated Funding Tracking**: The contract keeps track of funding contributions and project statuses.

## Constants
- `CONTRACT-OWNER`: The deployer of the contract.
- `ERR-UNAUTHORIZED (u100)`: Error for unauthorized actions.
- `ERR-INSUFFICIENT-FUNDS (u101)`: Error when funding exceeds required amount.
- `ERR-PROJECT-NOT-FOUND (u103)`: Error when referencing a non-existent project.
- `ERR-INVALID-INPUT (u104)`: Error for invalid input values.

## Project Status
- `PROJECT-STATUS-PROPOSED (u0)`: Initial status for new projects.
- `PROJECT-STATUS-FUNDED (u1)`: Status when a project has received full funding.
- `PROJECT-STATUS-COMPLETED (u2)`: Status when a researcher marks a project as completed.

## Data Structures
The contract uses a `projects` map to store project details:
- `project-id (uint)`: Unique identifier for the project.
- `researcher (principal)`: The creator of the project.
- `title (string-utf8 100)`: The title of the project.
- `description (string-utf8 500)`: Detailed explanation of the project.
- `total-funding-required (uint)`: The total amount needed for the project.
- `current-funding (uint)`: The amount currently funded.
- `status (uint)`: The current status of the project.

A `next-project-id` data variable is used to assign unique project IDs.

## Functions
### 1. `propose-project`
**Description**: Allows researchers to propose a new project.

**Parameters**:
- `title (string-utf8 100)`: The title of the project.
- `description (string-utf8 500)`: A description of the project.
- `total-funding-required (uint)`: The total funding needed.

**Returns**:
- `project-id (uint)`: The ID of the created project.

### 2. `fund-project`
**Description**: Allows users to fund a research project.

**Parameters**:
- `project-id (uint)`: The ID of the project to fund.
- `funding-amount (uint)`: The amount to contribute.

**Validations**:
- Funding amount must be greater than zero.
- Project must exist and be in `PROJECT-STATUS-PROPOSED`.
- Funding must not exceed the total required.
- Funds are transferred to the contract before updating funding.

**Returns**:
- `true` if funding is successful.

### 3. `complete-project`
**Description**: Allows a researcher to mark a project as completed.

**Parameters**:
- `project-id (uint)`: The ID of the project to complete.

**Validations**:
- Only the researcher can complete the project.
- Project must be in `PROJECT-STATUS-FUNDED`.

**Returns**:
- `true` if project completion is successful.

## Security Considerations
- **Access Control**: Only project researchers can complete projects.
- **Funding Limits**: Contributions cannot exceed the required amount.
- **Input Validation**: Ensures valid inputs to prevent erroneous entries.

## How to Deploy
1. Deploy the smart contract on the Stacks blockchain.
2. Interact with the contract using Clarity-compatible tools.

## How to Interact
Use Clarity language tools or blockchain explorers to call functions and interact with the contract.

## Future Enhancements
- **Milestone-Based Funding**: Release funds in stages based on progress.
- **Voting Mechanism**: Allow community voting on projects.
- **Refund Mechanism**: Handle failed or abandoned projects.

