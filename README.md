# Lifelink

CREATE DATABASE lifelink;

USE lifelink;

-- Table: users

CREATE TABLE users (
    email VARCHAR(255) NOT NULL PRIMARY KEY,
    full_name VARCHAR(255) NOT NULL,
    password VARCHAR(255) NOT NULL,
    blood_type ENUM('A+', 'A-', 'B+', 'B-', 'AB+', 'AB-', 'O+', 'O-') DEFAULT NULL,
    pincode INT NOT NULL,
    role ENUM('donor', 'admin', 'manager') NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Table: donated

CREATE TABLE donated (
    email VARCHAR(255) NOT NULL,
    event_name VARCHAR(255) DEFAULT NULL,
    donation_date DATE DEFAULT NULL,
    PRIMARY KEY (email),
    FOREIGN KEY (email) REFERENCES users(email)
);

-- Table: event

CREATE TABLE event (
    event_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    date DATE NOT NULL,
    place VARCHAR(255) NOT NULL
);

-- Table: inventory

CREATE TABLE inventory (
    blood_type VARCHAR(5) NOT NULL PRIMARY KEY,
    units INT DEFAULT 0
);

-- Table: requests

CREATE TABLE requests (
    request_id INT NOT NULL PRIMARY KEY,
    pincode INT NOT NULL,
    blood_type ENUM('A+', 'A-', 'B+', 'B-', 'AB+', 'AB-', 'O+', 'O-') NOT NULL,
    quantity INT NOT NULL,
    urgency ENUM('low', 'medium', 'high') NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Table: scheduled_events

CREATE TABLE scheduled_events (
    email VARCHAR(255) NOT NULL,
    event_id INT NOT NULL,
    scheduled_date DATE DEFAULT NULL,
    PRIMARY KEY (email),
    FOREIGN KEY (email) REFERENCES users(email),
    FOREIGN KEY (event_id) REFERENCES event(event_id)
);

-- Filling up inventory to simulate real life blood storage

INSERT INTO inventory (blood_type, units) VALUES
    ('A+', 0),
    ('A-', 0),
    ('B+', 0),
    ('B-', 0),
    ('AB+', 0),
    ('AB-', 0),
    ('O+', 0),
    ('O-', 0);

-- Insert sample events into the event table

INSERT INTO event (name, date, place) VALUES 

('Blood Donation Drive - Downtown', '2024-11-10', 'Downtown Community Center'),

('University Blood Camp', '2024-12-05', 'City University Hall'),

('Corporate Blood Drive', '2025-01-20', 'Tech Park Building A'),

('Annual Charity Blood Camp', '2025-02-15', 'Central Square Park'),

('Holiday Blood Drive', '2024-12-22', 'Westside Gym'),

('Emergency Donation Event', '2024-11-15', 'City Hospital Lobby'),

('School Blood Drive', '2025-03-01', 'High School Gymnasium'),

('Neighborhood Blood Drive', '2025-03-15', 'Community Church Basement');




# Instance Commands

sudo yum update -y

sudo yum install python3 -y

sudo yum install python3-pip -y

sudo pip3 install virtualenv

python3 -m venv venv

source venv/bin/activate

sudo yum install git -y

git clone (your git repo link)

cd (your git repo)

pip install flask mysql-connector-python

python app.py
