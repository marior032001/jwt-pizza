# Learning notes

## JWT Pizza code study and debugging

As part of `Deliverable ⓵ Development deployment: JWT Pizza`, start up the application and debug through the code until you understand how it works. During the learning process fill out the following required pieces of information in order to demonstrate that you have successfully completed the deliverable.

View home page
home.jsx <br/>
none <br/>
none

Register new user (t@jwt.com
, pw: test)
login.jsx <br/>
[POST] /api/auth <br/>
INSERT INTO user (name, email, password) VALUES (?, ?, ?) <br/>
INSERT INTO userRole (userId, role, objectId) VALUES (?, ?, ?)

Login new user (t@jwt.com
, pw: test)
login.jsx <br/>
[PUT] /api/auth <br/>
INSERT INTO auth (token, userId) VALUES (?, ?)

Order pizza
menu.jsx <br/>
[POST] /api/order <br/>
INSERT INTO dinerOrder (dinerId, franchiseId, storeId, date) VALUES (?, ?, ?, NOW()) <br/>
INSERT INTO orderIt (orderId, menuId, description, price) VALUES (?, ?, ?, ?)

Verify pizza
delivery.jsx <br/>
[POST] /api/order/verify <br/>
SELECT id, franchiseld, storeld, date FROM dinerO WHERE dinerld = ? LIMIT ${offset}, ${config.db.listPerPage} <br/>
SELECT id, menuld, description, price FROM orderl WHERE orderld = ?

View profile page
dinerDashboard.jsx <br/>
[GET] /api/order <br/>
SELECT id, franchiseld, storeld, date FROM dinerOr WHERE dinerld = ? LIMIT ${offset}, ${config.db.listPerPage} <br/>
SELECT id, menuld, description, price FROM orderlte WHERE orderld = ?

View franchise (as diner)
franchiseDashboard.jsx <br/>
[GET] /api/franchise/3 <br/>
SELECT objectld FROM userRole WHERE role='franchisee' AND userld=? <br/>
SELECT id, name FROM franchise WHERE id in (${franchiselds.join(.)})

Logout
logout.jsx <br/>
[DELETE] /api/auth <br/>
DELETE FROM auth WHERE token=?

View About page
about.jsx <br/>
none <br/>
none

View History page
history.jsx <br/>
none <br/>
none

Login as franchisee (f@jwt.com
, pw: franchisee)
franchiseDashboard.jsx <br/>
[PUT] /api/auth [GET] /api/franchise/2 <br/>
INSERT INTO auth (token, userId) VALUES (?, ?) <br/>
SELECT objectld FROM userRole WHERE role='franchisee' AND userld=? <br/>
SELECT id, name FROM franchise WHERE id in (${franchiselds.join(,)})

View franchise (as franchisee)
createStore.jsx <br/>
[GET] /api/franchise/2 <br/>
SELECT objectld FROM userRole WHERE role='franchisee' AND userld=? <br/>
SELECT id, name FROM franchise WHERE id in (${franchiselds.join(';')})

Create a store
createStore.jsx <br/>
[POST] /api/franchise/1/store <br/>
[GET] /api/franchise/2 <br/>
INSERT INTO store (franchiseld, name) VALUES (?, ?) <br/>
SELECT objectld FROM userRole WHERE role='franchisee' AND userld=? <br/>
SELECT id, name FROM franchise WHERE id in (${franchiselds.join(';')})

Close a store
closeStore.jsx <br/>
[DELETE] /api/franchise/1/store/1 <br/>
DELETE FROM store WHERE franchiseld=? AND id=?

Login as admin (a@jwt.com
, pw: admin)
login.jsx <br/>
[PUT] /api/auth <br/>
INSERT INTO auth (token, userId) VALUES (?, ?)

View Admin page
adminDashboard.jsx <br/>
[GET] /api/franchise <br/>
SELECT id, name FROM franchise <br/>
SELECT id, name FROM store WHERE franchiseld=?

Create a franchise for t@jwt.com

createFranchise.jsx <br/>
[POST] /api/franchise <br/>
SELECT id, name FROM user WHERE email=? <br/>
INSERT INTO franchise (name) VALUES (?) <br/>
INSERT INTO userRole (userId, role, objectId) VALUES (?, ?, ?)

Close the franchise for t@jwt.com

CloseFranchise.jsx <br/>
[DELETE] /api/franchise/3 <br/>
DELETE FROM store WHERE franchiseld=? <br/>
DELETE FROM userRole WHERE objectId=? <br/>
DELETE FROM franchise WHERE id=?