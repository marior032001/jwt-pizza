# Learning notes

## JWT Pizza code study and debugging

 Action | Frontend Component | Backend Endpoints | Database SQL |
|--------|------------------|-----------------|--------------|
| View home page | home.jsx | none | none |
| Register new user (t@jwt.com, pw: test) | login.jsx | [POST] /api/auth | `INSERT INTO user (name, email, password) VALUES (?, ?, ?)` <br/> `INSERT INTO userRole (userId, role, objectId) VALUES (?, ?, ?)` |
| Login new user (t@jwt.com, pw: test) | login.jsx | [PUT] /api/auth | `INSERT INTO auth (token, userId) VALUES (?, ?)` |
| Order pizza | menu.jsx | [POST] /api/order | `INSERT INTO dinerOrder (dinerId, franchiseId, storeId, date) VALUES (?, ?, ?, NOW())` <br/> `INSERT INTO orderIt (orderId, menuId, description, price) VALUES (?, ?, ?, ?)` |
| Verify pizza | delivery.jsx | [POST] /api/order/verify | `SELECT id, franchiseld, storeld, date FROM dinerO WHERE dinerld = ? LIMIT ${offset}, ${config.db.listPerPage}` <br/> `SELECT id, menuld, description, price FROM orderl WHERE orderld = ?` |
| View profile page | dinerDashboard.jsx | [GET] /api/order | `SELECT id, franchiseld, storeld, date FROM dinerOr WHERE dinerld = ? LIMIT ${offset}, ${config.db.listPerPage}` <br/> `SELECT id, menuld, description, price FROM orderlte WHERE orderld = ?` |
| View franchise (as diner) | franchiseDashboard.jsx | [GET] /api/franchise/3 | `SELECT objectld FROM userRole WHERE role='franchisee' AND userld=?` <br/> `SELECT id, name FROM franchise WHERE id in (${franchiselds.join(.)})` |
| Logout | logout.jsx | [DELETE] /api/auth | `DELETE FROM auth WHERE token=?` |
| View About page | about.jsx | none | none |
| View History page | history.jsx | none | none |
| Login as franchisee (f@jwt.com, pw: franchisee) | franchiseDashboard.jsx | [PUT] /api/auth [GET] /api/franchise/2 | `INSERT INTO auth (token, userId) VALUES (?, ?)` <br/> `SELECT objectld FROM userRole WHERE role='franchisee' AND userld=?` <br/> `SELECT id, name FROM franchise WHERE id in (${franchiselds.join(,)})` |
| View franchise (as franchisee) | createStore.jsx | [GET] /api/franchise/2 | `SELECT objectld FROM userRole WHERE role='franchisee' AND userld=?` <br/> `SELECT id, name FROM franchise WHERE id in (${franchiselds.join(';')})` |
| Create a store | createStore.jsx | [POST] /api/franchise/1/store <br/> [GET] /api/franchise/2 | `INSERT INTO store (franchiseld, name) VALUES (?, ?)` <br/> `SELECT objectld FROM userRole WHERE role='franchisee' AND userld=?` <br/> `SELECT id, name FROM franchise WHERE id in (${franchiselds.join(';')})` |
| Close a store | closeStore.jsx | [DELETE] /api/franchise/1/store/1 | `DELETE FROM store WHERE franchiseld=? AND id=?` |
| Login as admin (a@jwt.com, pw: admin) | login.jsx | [PUT] /api/auth | `INSERT INTO auth (token, userId) VALUES (?, ?)` |
| View Admin page | adminDashboard.jsx | [GET] /api/franchise | `SELECT id, name FROM franchise` <br/> `SELECT id, name FROM store WHERE franchiseld=?` |
| Create a franchise for t@jwt.com | createFranchise.jsx | [POST] /api/franchise | `SELECT id, name FROM user WHERE email=?` <br/> `INSERT INTO franchise (name) VALUES (?)` <br/> `INSERT INTO userRole (userId, role, objectId) VALUES (?, ?, ?)` |
| Close the franchise for t@jwt.com | CloseFranchise.jsx | [DELETE] /api/franchise/3 | `DELETE FROM store WHERE franchiseld=?` <br/> `DELETE FROM userRole WHERE objectId=?` <br/> `DELETE FROM franchise WHERE id=?` |