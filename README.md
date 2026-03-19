# Python Backend Testing (flask_rds_user_api)
![Project Image](https://raw.githubusercontent.com/arumullayaswanth/Python-backend-testing/6dba8e011d7e5910079c56a772b9bffee2aac93c/flackare.jpg)

- update
```bash
sudo dnf update -y
```
- Install MySQL client
```bash
sudo dnf install mariadb105 -y
mysql --version
```
- Connect to RDS
```bash
mysql -h <your-rds-endpoint> -u <username> -p
```
example:
```bash
mysql -h mydb.xxxxxx.ap-south-1.rds.amazonaws.com -u admin -p
```
- Run the following SQL commands:
```bash
CREATE DATABASE dev;
USE dev;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE
);

SELECT * FROM dev.users;
```
#### Deploy Flask Backend on EC2

```bash
yum install python3-pip -y
pip3 install flask mysql-connector-python
yum install git -y
git clone https://github.com/arumullayaswanth/Python-backend-testing.git
python3 app.py
```

### To run Flask in background:

nohup allows your app to continue running even after terminal disconnect:

```bash
nohup python3 app.py > flask.log 2>&1 &
tail -f flask.log
```

To check if the app is running:

```bash
ps aux | grep app.py
```

To stop it:

```bash
pkill -f app.py
```

---

✅ Step 7: Reconnect to EC2 backend server once again&#x20;

Now your application is running And don't Exit your application and take the new window and connect once again your EC2 backend server and run these commands again.

Open a **new terminal window** and SSH back into EC2:

```bash
ssh -i "your-key.pem" ec2-user@<EC2 Public IP>
sudo -i
```

---

## ✅ Step 8: API Methods and Testing

### Flask API Supports:

* `GET /users` → Fetch all users
* `GET /users/<id>` → Fetch single user by ID
* `POST /users/add` → Add a new user
* `PUT /users/update/<id>` → Update user
* `DELETE /users/delete/<id>` → Delete user

### Example `curl` Commands:  Run this commands in EC2  backend server

**GET all users:**

```bash
curl -X GET http://localhost:5000/users/1
```

**GET single user:**

```bash
curl -X GET http://localhost:5000/users
```

**POST - Add user:**

```bash
curl -X POST http://localhost:5000/users/add \
     -H "Content-Type: application/json" \
     -d '{"name":"John Doe", "email":"john@example.com"}'
```

**PUT - Update user:**

```bash
curl -X PUT http://localhost:5000/users/update/1 \
     -H "Content-Type: application/json" \
     -d '{"name": "John Updated", "email": "john.updated@example.com"}'
```

**DELETE - Remove user:**

```bash
curl -X DELETE http://localhost:5000/users/delete/1
```

---
