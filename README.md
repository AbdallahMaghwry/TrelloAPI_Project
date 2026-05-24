# Trello REST API Testing – Postman 

A structured API testing project that covers end-to-end validation of **Trello Cloud REST APIs** using **Postman** and **JavaScript** test scripts.

---

## 📌 Project Overview

This project targets the full lifecycle of core Trello entities — Boards, Lists, Cards, and Checklists — through an automated Postman collection. It goes beyond basic happy-path testing to cover data integrity across chained requests, negative scenarios, and response-time assertions.

**Collection Name:** `End-to-End Workflow`

---

##  Test Objectives

- Validate functional correctness of Trello REST APIs
- Automate full CRUD operations for Boards, Lists, Cards, and Checklists
- Ensure data consistency across chained and dependent requests
- Cover negative scenarios such as accessing deleted resources (e.g., HTTP 404 after deletion)
- Apply response-time assertions to catch performance regressions

---

##  System Under Test (SUT)

**Trello Cloud REST APIs**

 Official Docs: [https://developer.atlassian.com/cloud/trello/rest/](https://developer.atlassian.com/cloud/trello/rest/api-group-actions/)

---

##  Tools & Technologies

| Tool | Purpose |
|------|---------|
| Postman | Building, running, and managing API test collections |
| JavaScript | Writing test scripts and pre-request scripts inside Postman |
| Postman Collection Runner | Executing the full collection and reviewing results |
| Trello REST API | The system being tested |

---

##  Authentication

This project uses **Trello's API Key + Token** authentication method.

**Setup steps:**

1. Log in to [https://trello.com](https://trello.com)
2. Go to [https://trello.com/app-key](https://trello.com/app-key) to get your **API Key**
3. Generate a **Token** from the same page
4. In Postman, open the Environment and go to the **Variables** tab
5. Set the following Environment variables:

| Variable | Value |
|----------|-------|
| `apiKey` | Your Trello API Key |
| `apiToken` | Your Trello Token |

> ⚠️ Never commit your API Key or Token to a public repository.

---

##  Collection Structure

The collection is organized into multiple folders, each targeting a different testing scenario:

| Folder | Description |
|--------|-------------|
| `End-to-End Workflow` | Full CRUD operations across Boards, Lists, Cards, and Checklists |
| `Move List for Another Board Test` | Validates moving a List from one Board to another and verifies state after the move |
| `Move Card to Another List` | Validates moving Cards between two Lists within the same Board |

>  Each folder is self-contained and can be run independently via the Collection Runner.

---

### 🗂 End-to-End Workflow

### 🗂 Boards
| Request | Method | Description |
|---------|--------|-------------|
| Create Board | `POST` | Creates a new board and saves its ID to a collection variable |
| Get Board | `GET` | Retrieves board details and validates response fields |
| Update Board | `PUT` | Updates board name and verifies the change |
| Delete Board | `DELETE` | Deletes the board and verifies HTTP 200 response |

###  Lists
| Request | Method | Description |
|---------|--------|-------------|
| Create List | `POST` | Creates a list on the board created above |
| Get List | `GET` | Retrieves list details and validates its association with the board |
| Update List | `PUT` | Updates list name and verifies the change |
| Archive List | `PUT` | Sets `closed: true` and verifies the list is archived |

###  Cards
| Request | Method | Description |
|---------|--------|-------------|
| Create Card | `POST` | Creates a card inside the list created above |
| Get Card | `GET` | Retrieves card details and validates response fields |
| Update Card | `PUT` | Updates card name or description and verifies the change |
| Delete Card | `DELETE` | Deletes the card and verifies HTTP 200 response |

###  Checklists
| Request | Method | Description |
|---------|--------|-------------|
| Create Checklist | `POST` | Creates a checklist on an existing card |
| Get Checklist | `GET` | Retrieves checklist details and validates structure |
| Update Checklist | `PUT` | Updates checklist name and verifies the change |
| Delete Checklist | `DELETE` | Deletes the checklist and verifies HTTP 200 response |

---

###  Move List for another Board Test

| Request | Method | Description |
|---------|--------|-------------|
| Create First Board | `POST` | Creates the source board |
| Get Board After Create First Board | `GET` | Validates the first board was created correctly |
| Create Second Board | `POST` | Creates the destination board |
| Get Board After Create Second Board | `GET` | Validates the second board was created correctly |
| Create List in First Board | `POST` | Creates a list inside the first board |
| Get List First Board | `GET` | Validates the list exists in the first board |
| Create New Card In First Board | `POST` | Creates a card inside the list |
| Get Card in First Board | `GET` | Validates the card exists before the move |
| Move List to Second Board | `PUT` | Moves the list to the second board |
| Get Lists from Second Board | `GET` | Validates the list now exists in the second board |
| Delete First Board | `DELETE` | Cleans up the first board |
| Delete Second Board | `DELETE` | Cleans up the second board |

---

###  Move Card to another List

| Request | Method | Description |
|---------|--------|-------------|
| Create Board | `POST` | Creates a board to run the scenario on |
| Get Board After Create | `GET` | Validates the board was created correctly |
| Create First List | `POST` | Creates the source list |
| Create Second List | `POST` | Creates the destination list |
| Create First Card | `POST` | Creates the first card in the source list |
| Create Second Card | `POST` | Creates the second card in the source list |
| Move all Cards to Another List | `POST` | Moves all cards from the source list to the destination list |
| Get All Cards in List | `GET` | Validates all cards now exist in the destination list |
| Delete Board | `DELETE` | Cleans up the board after the scenario |

---

##  Key Testing Practices

- **Request Chaining** — IDs (boardId, listId, cardId, checklistId) are extracted from responses and stored as collection variables, then reused in subsequent requests automatically.
- **Negative Testing** — After deletion requests, follow-up GET requests verify the resource no longer exists (HTTP 404).
- **Response Time Assertions** — Each request includes a test asserting the response time is within an acceptable threshold.
- **DRY Principle** — A centralized pre-request script at the collection level automatically injects `apiKey` and `apiToken` into every request.

---

## 📊 Test Report

View the latest test run results here:

👉 [Open Test Report](https://abdallahmaghwry.github.io/TrelloAPI_Project/reports/Trello%20API%20%E2%80%93%20Test%20Report.html)

- **47** requests executed
- **1,428** assertions passed
- **0** failures
- **100%** pass rate

---

##  How to Run

1. Clone or download this repository
2. Open **Postman** and click **Import**
3. Select the collection `.json` file from this repo
4. Go to the collection **Variables** tab and fill in your `apiKey` and `apiToken`
5. Open **Collection Runner**, select `End-to-End Workflow`, and click **Run**

---

##  Repository Structure

```
├── Trello API.postman_collection.json   # Main Postman collection
├── Trello_Environment.postman_environment.json       # Environment variables 
└── README.md
```

---


##  License

This project is open source and available under the [MIT License](LICENSE).
