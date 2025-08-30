# WE Trust Registration & Admin System

## 📑 Google Sheets Setup
Create a Google Spreadsheet with these **6 tabs**:

### 1. Registrations
| Timestamp | Grade | Location | Participant Type | Mode | Name | Membership Number | Mobile | Email | Address | Pincode | Fees Paid | Seminar Dates |

### 2. Seminars
| Grade | Location | Start Date | End Date |

### 3. Admin
| Username | PasswordHash |

### 4. Logs
| Timestamp | Actor Type | Username | Action | Membership | Details |

### 5. Members
| Membership Number | Name | Status |

### 6. Deleted Members
| Deleted Timestamp | Membership Number | Name | Status | Deleted By | Reason |

---

## ⚙️ Backend (Code.gs)
1. Open **Google Apps Script** from your Sheet (`Extensions > Apps Script`).
2. Paste contents of `Code.gs` (provided in package).
3. Replace `SHEET_ID` with your Google Sheet ID.
4. Deploy as **Web App**:
   - Execute as: **Me**
   - Who has access: **Anyone with Link**
5. Copy the Web App URL.

---

## 🌐 Frontend (user.html & admin.html)
1. Replace all `WEB_APP_URL` placeholders with your Web App URL.
2. Host both files using:
   - GitHub Pages
   - Netlify
   - Your own web server

---

## 🔑 Admin Setup
- Add admin usernames & password hashes in the **Admin** sheet.
- To generate hash:  
  Run in Apps Script console:
  ```javascript
  hashString("yourpassword")
  ```
- Copy the output into **PasswordHash**.

---

## 👩‍🎓 User Portal (user.html)
- Register for eligible seminars (based on past grades).
- Auto-fetch past seminars + next eligible grade.
- Prevents duplicate **Student** registration for same grade.
- Validates Membership Number (6 digits, numeric, exists in Members sheet).
- If Member is **Inactive** → registration blocked.

---

## 🛠️ Admin Dashboard (admin.html)
### Registrations
- Search, filter (grade, mode, fees, date range, upcoming only).
- Edit inline, Save changes.
- Delete (logged).

### Auto Logout
- 5 min inactivity auto logout.
- Warning at 4 min with option to extend session.

### Exports
- Export **All Registrations** (CSV/Excel).
- Export **Filtered Registrations** (CSV/Excel).
- Export **Logs** (CSV/Excel).
- All export actions are logged.

### Members Management
- **Add Member** (Membership No, Name, Status).
- **Edit Member** (Name, Status).
- **Delete Member** → moves to **Deleted Members** (Recycle Bin).
- **Restore Member** from Deleted Members back to active list.

### Deleted Members (Recycle Bin)
- Stores deleted members with timestamp, deleted by, reason.
- Can restore back into Members.

---

## 📝 Logs
- Every action (User + Admin) recorded in **Logs** sheet:
  - Who (Username)
  - What (Action)
  - When (Timestamp)
  - Membership (if applicable)
  - Details

Example:
| Timestamp           | Actor Type | Username | Action          | Membership | Details                               |
|---------------------|------------|----------|-----------------|------------|---------------------------------------|
| 2025-09-01 18:20:45 | ADMIN      | admin1   | UPDATE MEMBER   | 123456     | Updated Name=John D., Status=Active    |
| 2025-09-01 18:40:15 | ADMIN      | admin1   | ADD MEMBER      | 456789     | Added new member: Meena (Active)       |
| 2025-09-01 18:42:55 | ADMIN      | admin2   | DELETE MEMBER   | 987654     | Moved to Deleted Members sheet         |
| 2025-09-01 18:50:12 | ADMIN      | admin2   | RESTORE MEMBER  | 987654     | Restored from Deleted Members sheet    |
| 2025-09-01 19:00:10 | USER       | -        | REGISTER (First-time) | 123456 | Registered for Grade 5 at Tirunelveli |

---

## ✅ Features Summary
- Secure **multi-admin login** (username + password hash).
- User registration with **membership validation**.
- Prevents duplicate Student registrations.
- Full **logging** of user + admin actions.
- Admin Dashboard:
  - Manage registrations
  - Manage members
  - Recycle Bin (restore deleted members)
  - Auto logout
  - CSV/Excel exports

---

## 🚀 Deployment Flow
1. Setup Google Sheet with required tabs + headers.
2. Deploy backend (`Code.gs`) as Web App.
3. Update `WEB_APP_URL` in `user.html` & `admin.html`.
4. Host frontend files.
5. Share `user.html` to participants, keep `admin.html` restricted to admins.

---
