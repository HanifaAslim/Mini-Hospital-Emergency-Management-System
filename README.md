# 📖 Mini Hospital Emergency Management System — Feature & User Guide

A complete, step-by-step guide explaining all system features, custom data structure mechanics, and usage instructions for both the **Desktop GUI** and **Console CLI**.

---

## 📌 Executive System Overview

The **Mini Hospital Emergency Management System** simulates real-world emergency hospital operations across four core workflow areas. Each workflow area is powered by a custom-built data structure implemented without Java's built-in collections framework.

---

## 🛠️ Detailed System Features & Usage Guide

### 1. Patient Records Management — Binary Search Tree (BST)

#### 📘 Feature Explanation
All registered hospital patients are stored in a custom **Binary Search Tree (BST)** using the **Patient ID (integer)** as the key.
- **In-Order Traversal**: Automatically sorts and displays patients in ascending order of Patient ID ($101, 102, 103, \dots$).
- **Binary Search**: Allows $O(\log n)$ lookup speed by comparing target IDs with current tree nodes.
- **Node Deletion**: Handles 3 structural scenarios:
  1. **Leaf Node (0 Children)**: Directly removed.
  2. **Single Child (1 Child)**: Node replaced by its child.
  3. **Two Children (2 Children)**: Node replaced by its **in-order successor** (smallest node in right subtree).

#### 🖱️ How to Use in Desktop GUI (`ui.MainGUI`)
1. Open the **Patient Directory (BST)** tab.
2. **Add New Patient**:
   - Enter **Patient ID** (e.g. `116`), **Name** (e.g. `Kusal Perera`), **Age** (e.g. `28`), **Contact** (e.g. `+94-77-1234567`), and **Condition** (e.g. `Fever`).
   - Click **Add Patient to BST**.
3. **Search Patient**:
   - Enter Patient ID into the **Patient ID** search box.
   - Click **Search ID** to display a popup window with patient details.
4. **Delete Patient**:
   - Select a patient row in the table (or type their ID into the search box).
   - Click **Delete Selected / ID** to remove them from the BST.

#### 💻 How to Use in Console CLI (`ui.MainMenu`)
- Select **Option 1** to add a new patient.
- Select **Option 2** to search for a patient by ID.
- Select **Option 3** to delete a patient.
- Select **Option 4** to display all patients in ascending order.

---

### 2. Emergency Room Triage — Queue (FIFO)

#### 📘 Feature Explanation
Arriving emergency patients are managed using a custom **First-In, First-Out (FIFO) Queue**.
- **Enqueue**: Arriving patients are added to the **rear (tail)** of the waiting queue ($O(1)$ time).
- **Dequeue**: Doctors process the patient at the **front (head)** of the queue ($O(1)$ time).
- **Empty Queue Handling**: If the queue is empty, a clean alert message *"Waiting queue is empty"* is returned without throwing exceptions.

#### 🖱️ How to Use in Desktop GUI (`ui.MainGUI`)
1. Open the **Patient Directory (BST)** tab.
2. Select a patient row (or type their ID in search box) and click **Send to Emergency Queue**.
3. Switch to the **Emergency Queue (FIFO)** tab:
   - Observe the live queue length counter (e.g., *Patients Currently Waiting in Queue: 15*).
   - View patients listed in order from **Position #1 (Head)** to rear.
4. Click **Process Next Patient (Dequeue)**:
   - Removes the front patient from the waiting queue.
   - Prompts a dialog option to automatically mark treatment complete and push them to the Treatment Stack.

#### 💻 How to Use in Console CLI (`ui.MainMenu`)
- Select **Option 5** to enqueue a patient by ID.
- Select **Option 6** to dequeue and process the next emergency patient.
- Select **Option 7** to display all waiting patients.

---

### 3. Completed Treatment History — Stack (LIFO)

#### 📘 Feature Explanation
When emergency treatment is finished, the completed record is stored in a custom **Last-In, First-Out (LIFO) Stack**.
- **Push**: Newly completed treatment records are placed on the **top** of the stack ($O(1)$ time).
- **Pop / Undo**: Pops the top (most recent) treatment record off the stack ($O(1)$ time).
- **Empty Stack Handling**: Prevents errors when attempting to undo on an empty stack.

#### 🖱️ How to Use in Desktop GUI (`ui.MainGUI`)
1. Open the **Treatment History (Stack)** tab.
2. Observe the stack view: **Position #1 TOP (Most Recent)** displays the latest patient treated.
3. Click **Undo Last Treatment (Pop from Stack)**:
   - Pops the most recent treatment record off the stack.
   - Displays a confirmation alert with the undone patient's details.

#### 💻 How to Use in Console CLI (`ui.MainMenu`)
- Select **Option 8** to mark treatment complete for a patient.
- Select **Option 9** to undo the last treatment (pop from stack).
- Select **Option 10** to view treatment history.

---

### 4. Patient Visit History — Singly Linked List

#### 📘 Feature Explanation
Each `Patient` object contains an embedded custom generic **Singly Linked List (`SinglyLinkedList<Visit>`)** tracking past hospital visits.
- **Visit Fields**: `Visit ID`, `Visit Date`, `Doctor Name`, `Diagnosis`, `Treatment Prescribed`.
- **Operations**:
  - **Add Visit**: Appends a new visit node to the patient's linked list.
  - **Remove Visit**: Searches for `visitId` and unlinks the node from the list.
  - **Search Visit**: Scans list nodes to find matching visit records.

#### 🖱️ How to Use in Desktop GUI (`ui.MainGUI`)
1. Open the **Visit History (LinkedList)** tab.
2. Enter a **Patient ID** (e.g. `101`) and click **Load Patient Visit History** (Patient `101` is pre-loaded on startup).
3. **Add Visit**:
   - Fill in **Visit ID** (e.g., `V104`), **Date** (e.g., `2026-08-30`), **Doctor** (e.g., `Dr. Nihal Jayasinghe`), **Diagnosis** (e.g., `Checkup`), and **Treatment**.
   - Click **Add Visit Record**.
4. **Remove Visit**:
   - Select a visit row in the table and click **Remove Selected Visit**.

#### 💻 How to Use in Console CLI (`ui.MainMenu`)
- Select **Option 11** to add a visit record to a patient.
- Select **Option 12** to remove a visit record from a patient.
- Select **Option 13** to search for a visit record.
- Select **Option 14** to display a patient's full visit history.

---

## ⚡ How to Run the Applications

### 1. Launch Swing Desktop GUI (Recommended)
```bash
java -cp bin ui.MainGUI
```

### 2. Launch Interactive Console CLI
```bash
java -cp bin ui.MainMenu
```

### 3. Run Automated Test Suite
```bash
powershell -Command "javac -cp bin -d bin scratch/TestRunner.java; java -cp bin TestRunner"
```

---

## 📊 Summary of Data Structures & Time Complexities

| Feature Area | Custom Data Structure | Key Operations | Time Complexity |
| :--- | :--- | :--- | :---: |
| **Patient Directory** | Binary Search Tree (`BST`) | Insert, Search, Delete, In-Order Traversal | $O(\log n)$ average |
| **Emergency Triage** | FIFO Queue (`Queue`) | Enqueue, Dequeue, Peek | $O(1)$ constant |
| **Treatment History** | LIFO Stack (`Stack`) | Push, Pop (Undo), Peek | $O(1)$ constant |
| **Visit History** | Singly Linked List (`SinglyLinkedList`) | Add, Remove, Search, Traverse | $O(n)$ linear |
