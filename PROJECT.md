# PROJECT.md

This file provides guidance to AI Assistant when working with code in this repository.

## IMPORTANT FILES

**STATUS.md**: CURRENT PROJECT STATUS. READ IT INITIALLY, UPDATE IT AFTER SIGNIFICANT CHANGES
**AI_INSTRUCTIONS.md**: Basic instructions for LLMs/agents. Read it and follow its instructions before work starts, after compaction, and whenever you need direction.

## Language policy

- **Control/meta files** (`PROJECT.md`, `STATUS.md`, `AI_INSTRUCTIONS.md`, `README.md`): English.
- **Product documentation** (`docs/`): Czech — it is the working language of the target audience in the bank.
- **Chat communication with the user:** Czech, unless the user requests otherwise.

## IMPORTANT: Session State

**FIRST ACTION in every new session:** Read and interpret `STATUS.md` file in the repository root.

This file contains:
- Current project state across all work streams
- Active issues and pending actions
- Next steps for continuation

**DO NOT** ask the user for context about current work - `STATUS.md` contains everything needed to continue seamlessly.

## Project Overview

**Open-WebUI (OWUI) implementation guidelines for the bank** — a unified AI platform for the bank.

This project creates documentation for Open-WebUI AI tool / workspace in the bank.

We will begin preparing the documentation for the future (already partially functional) solution. The documentation will also include a governance document for this solution.  
OWUI will be a "central AI hub" with the following objectives:
* to provide employees with access to appropriate models. Access to models will be controlled by group membership, which will be mapped to AD groups
* based on group membership (other than those used for controlling access to models), provide users with access to agents according to business domains
  * each agent will have—depending on their business domain—defined access to various sources. For example:
    * for the HR domain, this will be the HR system, 
    * for the domain of banking advisors = bankers, this will be CRM and related systems (e.g., client account balances...)
  * the complete list of domains is not yet known, but it must be assumed that it will not be "permanently" fixed—it will continuously adapt to needs. 
  * Access to sources must be secured through authorization checks 
  * We need to devise a technical solution for accessing sources; most likely an MCP server and "on behalf of" calls for users logged into OWUI... ?
* The basic functionality of OWUI—i.e., models + web search—is already available
* OWUI will access all models via LiteLLM (which is the company’s LLM proxy)
* SSO authentication—AAD / EntraID


