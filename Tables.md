Run these in MySQL Command Line
```
create database sql_college;
use sql_college;
CREATE TABLE USER (
    user_ID INT PRIMARY KEY,
    password VARCHAR(16),
    name VARCHAR(50),
    email VARCHAR(50)
);
CREATE TABLE CUSTOMER (
    c_ID INT PRIMARY KEY,
    c_homeaddr VARCHAR(255),
    c_phoneNo VARCHAR(15),
    FOREIGN KEY (c_ID) REFERENCES USER(user_ID) on DELETE CASCADE
);
CREATE TABLE PROVIDER (
    p_ID INT PRIMARY KEY,
    p_scale VARCHAR(50),
    p_officeaddr VARCHAR(255),
    p_phoneNo VARCHAR(15),
    p_multiplier FLOAT,
    p_PAN VARCHAR(20),
    p_GST VARCHAR(20),
    verified boolean,
    FOREIGN KEY (p_ID) REFERENCES USER(user_ID) on DELETE CASCADE
);
CREATE TABLE ADMIN (
    adm_ID INT PRIMARY KEY,
    adm_join_date DATE,
    FOREIGN KEY (adm_ID) REFERENCES USER(user_ID) on DELETE CASCADE
);
CREATE TABLE REQUESTS (
    req_ID INT PRIMARY KEY,
    c_ID INT,
    req_weight FLOAT,
    req_size FLOAT,
    req_speed INT,
    req_dist FLOAT,
    req_type VARCHAR(50),
    start varchar(50),
    end varchar (50),
    FOREIGN KEY (c_ID) REFERENCES CUSTOMER(c_ID) on DELETE CASCADE
);
CREATE TABLE QUOTES (
    quote_ID INT PRIMARY KEY,
    p_ID INT,
    quote_amt FLOAT,
    quote_speed INT,
    req_id INT,
    FOREIGN KEY (p_ID) REFERENCES PROVIDER(p_ID) on DELETE CASCADE,
    FOREIGN KEY (req_ID) REFERENCES requests(req_ID) on DELETE CASCADE
);
CREATE TABLE ORDERS (
    c_ID INT,
    p_ID INT,
    order_ID INT,
    weight FLOAT,
    size FLOAT,
    type VARCHAR(50),
    speed INT,
    status VARCHAR(50),
    dist FLOAT,
    bill float,
    start varchar(50),
    end varchar (50),
    PRIMARY KEY (c_ID, p_ID, order_ID),
    FOREIGN KEY (c_ID) REFERENCES CUSTOMER(c_ID) on DELETE CASCADE,
    FOREIGN KEY (p_ID) REFERENCES PROVIDER(p_ID) on DELETE CASCADE
);
CREATE TABLE EMPLOYEE (
    emp_ID INT PRIMARY KEY,
    emp_email VARCHAR(50),
    emp_salary FLOAT,
    isAssisting INT DEFAULT 0
);
CREATE TABLE EMP_PHONENO (
    emp_ID INT,
    emp_phoneNo VARCHAR(15),
    PRIMARY KEY (emp_ID, emp_phoneNo),
    FOREIGN KEY (emp_ID) REFERENCES EMPLOYEE(emp_ID) on DELETE CASCADE
);

-- INSERTS statements

INSERT INTO USER (user_ID, name, password, email) VALUES
(1000, 'Vikram', 'password123', 'vikram@gmail.com'),
(1001, 'Rohan Patel', 'securepass', 'rohan_patel@gmail.com'),
(1002, 'Vikas', 'abcdefVik', 'vikas@gmail.com'),
(1003, 'Aarav Patel', 'Aaravpass456', 'Aarav@gmail.com'),
(1004, 'Aisha Sharma', 'Aishapass123', 'Aisha@gmail.com'),
(1005, 'Arjun Singh', 'securepass', 'Arjun@gmail.com'),
(1006, 'Devika Gupta', 'devikapass', 'devika@gmail.com'),
(1007, 'Kabir Mehta', 'kabirpassMehta', 'kabir@gmail.com'),
(1008, 'Meera Reddy', 'meera123Red', 'meera@gmail.com'),
(1009, 'Rahul Khanna', 'rahulpass456', 'rahul@gmail.com'),
(1010, 'Sanya Desai', 'sanyapass789', 'sanya@gmail.com'),
(1011, 'Vikram Malhotra', 'vikrampass1011', 'vikram_malhotra@gmail.com'),
(1012, 'Zara Khan', 'zara123Khan','zara_khan@gmail.com'),
(2000, 'Yogesh Rane', 'adminpass', 'yogesh@gmail.com'),
(2001, 'Akshay K C', 'adminpass', 'akshay@gmail.com'),
(2002, 'Ashwin Mittal', 'adminpass', 'ashwin@gmail.com'),
(3000, 'APM', 'providerpass', 'aarav_mehra@live.com'),
(3001, 'Interocean', 'providerpass', 'dhruv_trivedi@live.com'),
(3002, 'RashDriven', 'absolut', 'info@kingfisher.com'),
(3003, 'Arjun Enterprises', 'ArjunEnt@789', 'arjun_enterprises@hotmail.com'),
(3004, 'Aditya Corp', 'AdityaCorp!@#', 'aditya_corp@outlook.com'),
(3005, 'InnovateX', 'InnovateX#2024', 'info@innovatex.com'),
(3006, 'Genesis Group', 'GenesisGroup$567', 'contact@genesisgroup.com'),
(3007, 'Quantum Solutions', 'QuantumSol&890', 'info@quantumsolutions.com'),
(3008, 'Vertex Ventures', 'VertexVent$123', 'contact@vertexventures.com'),
(3009, 'Fusion Innovations', 'FusionInno*456', 'info@fusioninnovations.com');

INSERT INTO ADMIN (adm_ID, adm_join_date) VALUES
(2000, '2024-01-15'),
(2001, '2024-02-20'),
(2002, '2024-03-25');

INSERT INTO CUSTOMER (c_ID, c_homeaddr, c_phoneNo) VALUES
(1000,'Udupi','8974561234'),
(1001,'Gokarna','8420453229'),
(1002, 'Ganga Nagar, Pune', '9901234567'),
(1003, 'Rajendra Nagar, Chennai', '9902345678'),
(1004, 'Krishna Colony, Durgapur', '9903456789'),
(1005, 'Nehru Street, Ajmer', '9904567890'),
(1006, 'Saraswati Vihar, Kolkata', '9905678901'),
(1007, 'Gandhi Road, Lucknow', '9906789012'),
(1008, 'Tagore Nagar, Bangalore', '9907890123'),
(1009, 'Patel Chowk, Ahmedabad', '9908901234'),
(1010, 'Vasant Vihar', '9908887777'),
(1011, 'Patlipada', '9907776666'),
(1012, 'Godhbunder', '9906665555');


INSERT INTO PROVIDER (p_ID, p_scale, p_officeaddr, p_phoneNo, p_multiplier, p_PAN, p_GST, verified) VALUES
(3000, 'Large', 'Vasant Marg', '9999909876', 1.5, 'B3JH781', '22ABC123A1Z1', True),
(3001, 'Large', 'Lajpat Lane', '9999904321', 1.2, 'C8D4F3', '22DEF456A1Z2', True),
(3002, 'Large', 'Mayur Vihar', '9999967890', 1.3, 'B3JH781', '22B3JH781A1Z1', True),
(3003, 'Large', 'Udupi', '9999987654', 1.6, 'C8D4F3', '22C8D4F3A1Z2', True),
(3004, 'Small', 'Gandhi Road', '9999972345', 1.1, 'X2Y7Z9', '22X2Y7Z9A1Z3', True),
(3005, 'Large', 'Lotus Lane', '9999954321', 1.7, 'A1B2C3', '22A1B2C3A1Z4', True),
(3006, 'Medium', 'Mango Lane', '9999978765', 1.4, 'K9L1M2', '22K9L1M2A1Z5', True),
(3007, 'Large', 'Rose Lane', '9999989012', 1.2, 'H5G3F7', '22H5G3F7A1Z6', True),
(3008, 'Medium', 'Sunflower Lane', '9999921098', 1.5, 'R6T8Y2', '22R6T8Y2A1Z7', True),
(3009, 'Large', 'Peacock Street', '9999910987', 1.8, 'S4D9F1', '22S4D9F1A1Z8', False);

INSERT INTO REQUESTS (req_ID, c_ID, req_weight, req_size, req_speed, req_dist, req_type, start, end) VALUES
(1, 1008, 113.7, 4.1, 5, 293.9, 'Large', 'Ahmedabad', 'Vadodara'),
(2, 1009, 90.2, 3.0, 3, 45.5, 'Medium', 'Chandigarh', 'Ludhiana'),
(3, 1001, 105.1, 4.8, 6, 180.2, 'Large', 'Mumbai', 'Pune'),
(4, 1003, 46.8, 2.1, 4, 32.3, 'Medium', 'Bangalore', 'Chennai'),
(5, 1002, 82.3, 3.9, 5, 225.6, 'Large', 'Kolkata', 'Durgapur'),
(6, 1002, 9.5, 2.7, 3, 47.8, 'Medium', 'Jaipur', 'Ajmer'),
(7, 1006, 99.9, 3.6, 6, 28.4, 'Medium', 'Lucknow', 'Kanpur'),
(8, 1007, 29, 2.3, 4, 7.1, 'Small', 'Hyderabad', 'Secunderabad');

INSERT INTO QUOTES (quote_ID, p_ID, quote_amt, quote_speed, req_id) VALUES
(1, 3008, 22000.0, 5, 6),
(2, 3009, 7000.0, 3, 6),
(3, 3002, 8000.0, 4, 2),
(4, 3003, 5500.0, 5, 2),
(5, 3004, 21000.0, 6, 4),
(6, 3005, 3000.0, 3, 4),
(7, 3006, 15000.0, 6, 5),
(8, 3007, 1800.0, 4, 5),
(9, 3006, 6500, 5, 1);

INSERT INTO ORDERS (c_ID, p_ID, order_ID, weight, size, type, speed, status, dist, bill, start, end) VALUES
(1002, 3002, 2, 105.1, 4.8, 'Large', 4, 'Scheduled for Pickup', 180.2, 8000, 'Mumbai', 'Pune'),
(1003, 3003, 5, 46.8, 2.1, 'Medium', 4, 'En Route', 38.3, 4500, 'Bangalore', 'Chennai'),
(1001, 3005, 3, 82.3, 3.9, 'Large', 5, 'At Origin Facility', 225.6, 21000, 'Kolkata', 'Durgapur'),
(1001, 3004, 6, 69.5, 2.7, 'Small', 3, 'Processing', 147.8, 3000, 'Jaipur', 'Ajmer'),
(1006, 3006, 8, 101.9, 3.6, 'Medium', 6, 'In Transit', 268.4, 15000, 'Lucknow', 'Kanpur'),
(1007, 3007, 9, 77.6, 2.3, 'Small', 4, 'Scheduled for Pickup', 220.1, 1800, 'Hyderabad', 'Secunderabad'),
(1008, 3007, 7, 113.7, 4.1, 'Large', 5, 'En Route', 293.9, 22000, 'Ahmedabad', 'Vadodara'),
(1009, 3001, 11, 90.2, 3.0, 'Medium', 3, 'At Destination', 216.5, 7000, 'Chandigarh', 'Ludhiana'),
(1001, 3003, 10, 85.4, 2.8, 'Medium', 4, 'Completed', 193.7, 8500, 'Pune', 'Mumbai'),
(1011, 3008, 13, 57.6, 3.5, 'Large', 5, 'Completed', 132.4, 18000, 'Chennai', 'Bangalore'),
(1012, 3000, 3, 120.8, 4.2, 'Large', 6, 'Completed', 270.5, 32000, 'Delhi', 'Jaipur');

INSERT INTO EMPLOYEE (emp_ID, emp_email, emp_salary, isAssisting) VALUES
(4001, 'akash.sharma@gmail.com', 50000.00, 1002),
(4002, 'neha.joshi@gmail.com', 60000.00, 0),
(4003, 'suresh.kumar@gmail.com', 55000.00, 0),
(4004, 'priya.mishra@outlook.com', 52000.00, 1004),
(4005, 'ananya.gupta@outlook.com', 53000.00, 0),
(4006, 'rajesh.singh@outlook.com', 58000.00, 0),
(4007, 'divya.sharma@hotmail.com', 57000.00, 0),
(4008, 'akash.verma@hotmail.com', 62000.00, 1003),
(4009, 'meera.patel@hotmail.com', 54000.00, 0);

INSERT INTO EMP_PHONENO (emp_ID, emp_phoneNo) VALUES
(4001, '9345543210'),
(4002, '9971882633'),
(4003, '9812345678'),
(4003, '9798765432'),
(4004, '9876543210'),
(4004, '9789012345'),
(4005, '9870123456'),
(4006, '9790123456'),
(4007, '9810987654'),
(4008, '9791234567'),
(4009, '9878901234');



DELIMITER //
DROP PROCEDURE IF EXISTS addrequest;
CREATE PROCEDURE addrequest(cid INT, weight FLOAT, size FLOAT, speed FLOAT, dist FLOAT, strt VARCHAR(50), endpt VARCHAR(50))
BEGIN
    DECLARE r_id INT;
    SELECT MAX(req_id) INTO r_id FROM requests;
    IF r_id IS NULL THEN
        SET r_id = 1;
    ELSE
        SET r_id = r_id + 1;
    END IF;
    
    IF weight < 50 AND dist < 15 THEN
        INSERT INTO requests (req_id, c_id, req_weight, req_size, req_speed, req_dist, req_type, `start`, `end`) 
        VALUES (r_id, cid, weight, size, speed, dist, 'Small', strt, endpt);
    ELSEIF weight < 100 AND dist < 50 THEN
        INSERT INTO requests (req_id, c_id, req_weight, req_size, req_speed, req_dist, req_type, `start`, `end`) 
        VALUES (r_id, cid, weight, size, speed, dist, 'Medium', strt, endpt);
    ELSE
        INSERT INTO requests (req_id, c_id, req_weight, req_size, req_speed, req_dist, req_type, `start`, `end`) 
        VALUES (r_id, cid, weight, size, speed, dist, 'Large', strt, endpt);
    END IF;
    COMMIT;
END//
DELIMITER ;





DELIMITER //
DROP TRIGGER IF EXISTS set_isAssisting_to_zero//
CREATE TRIGGER set_isAssisting_to_zero
AFTER DELETE ON user
FOR EACH ROW
BEGIN
    UPDATE EMPLOYEE
    SET isAssisting = 0
    WHERE isAssisting = OLD.user_ID;
END//
DELIMITER ;


```
