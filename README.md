# 🏏 IPL Auction Dashboard Automation (Google Sheets + Apps Script)

This project automates the **IPL Player Auction** process using **Google Sheets** and **Google Apps Script**.  
It simplifies player selection, updates auction results dynamically, and provides real-time notifications inside Google Sheets.

---

## 📌 Features
- 🎲 **Random Player Selection** – Picks a random unsold player from the "Player List" sheet.
- 📝 **Dynamic Status Update** – Automatically updates player sale details (team, price, etc.).
- 🔔 **Real-Time Notifications** – Displays toast messages when a player is sold.
- ⚡ **Automated Workflow** – Reduces manual tracking and speeds up the auction process.

---

## 📂 Google Sheet Setup
- **Sheet Name:** `Player List`
- **Columns Used:**
  - `Column A`: Player Names  
  - `Column E`: Player Status (e.g., *Unsold*, *Sold*)  
- **Cell C26**: Displays the currently picked random player.

---

## 💻 Code Overview

```javascript
// Pick a random unsold player from "Player List" and set in C26
function pickRandomUnsoldPlayer() {
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName("Player List");
  const players = sheet.getRange('A2:A51').getValues();
  const statuses = sheet.getRange('E2:E51').getValues();
  const unsoldPlayers = [];

  for (let i = 0; i < statuses.length; i++) {
    if (statuses[i][0].toString().toLowerCase() === "unsold") {
      unsoldPlayers.push(players[i][0]);
    }
  }

  // Logic for picking a random unsold player and updating details goes here...
  
  SpreadsheetApp.getActiveSpreadsheet().toast(
    playerName + " was sold to " + soldTo + " for Rs. " + salePrice
  );

  // Continue the process until all players are sold
  pickRandomUnsoldPlayer();
}
