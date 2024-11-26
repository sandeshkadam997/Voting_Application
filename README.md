# Voting Application

The Voting Application is a backend application for a voting system where users can vote for candidates. It provides functionalities for user authentication, candidate management, and voting.

## Features

- User sign up and login with Aadhar Card Number and password
- User can view the list of candidates
- User can vote for a candidate (only once)
- Admin can manage candidates (add, update, delete)
- Admin cannot vote

## Technologies Used

- **Node.js:** Backend environment for building the application.
- **Express.js:** Framework for building RESTful APIs.
- **MongoDB:** NoSQL database for storing user and candidate data.
- **Mongoose:** ODM (Object Data Modeling) library for MongoDB.
- **JWT (JSON Web Tokens):** For secure authentication and authorization.
- **RESTful API:** For communication between frontend and backend.

# API Endpoints

## Authentication

### Sign Up
- `POST /signup`: Sign up a user

### Login
- `POST /login`: Login a user

## Candidates

### Get Candidates
- `GET /candidates`: Get the list of candidates

### Add Candidate
- `POST /candidates`: Add a new candidate (Admin only)

### Update Candidate
- `PUT /candidates/:id`: Update a candidate by ID (Admin only)

### Delete Candidate
- `DELETE /candidates/:id`: Delete a candidate by ID (Admin only)

## Voting

### Get Vote Count
- `GET /candidates/vote/count`: Get the count of votes for each candidate

### Vote for Candidate
- `POST /candidates/vote/:id`: Vote for a candidate (User only)

## User Profile

### Get Profile
- `GET /users/profile`: Get user profile information

### Change Password
- `PUT /users/profile/password`: Change user password


## Data Models

### User
The `User` data model represents the users who can vote in the voting application.

- **Fields:**
  - `name` (String): Name of the user (required).
  - `age` (Number): Age of the user (required).
  - `email` (String): Email address of the user.
  - `mobile` (String): Mobile number of the user.
  - `address` (String): Address of the user (required).
  - `aadharCardNumber` (Number): Aadhar card number (unique and required).
  - `password` (String): User's password (required).
  - `role` (String, Enum: ['voter', 'admin']): Role of the user, either "voter" or "admin"     
      (default is voter).
  - `isVoted` (Boolean): Whether the user has voted (default is false).
    
- **Example:**
  ```json
  {
    "name": "Alice Smith",
    "age": 30,
    "email": "alice.smith@example.com",
    "mobile": "987-654-3210",
    "address": "456 Elm Street",
    "aadharCardNumber": 123456789012,
    "password": "securepassword123",
    "role": "voter",
    "isVoted": false
  }


### Candidate
The `Candidate` data model represents candidates running for election.

- **Fields:**
    - `name` (String): Name of the candidate (required).
    - `party` (String): Political party of the candidate (required).
    - `age` (Number): Age of the candidate (required).
    - `votes` (Array of Objects): List of users who voted for the candidate.
    - `user` (ObjectId): Reference to the User model.
    - `votedAt` (Date): Timestamp of the vote (default is the current date).
    - `voteCount` (Number): Total votes for the candidate (default is 0).
      
- **Example:**
  ```json
  {
    "name": "John Doe",
    "party": "Democratic Party",
    "age": 45,
    "votes": [
      {
        "user": "5f8c072cb0f2b84c1a62c9bb",
        "votedAt": "2023-11-26T15:00:00Z"
      }
    ],
    "voteCount": 1
  }

## Additional Notes

- **Role Management:** The system distinguishes between two user roles: voter and admin.           Admins can manage candidates, while voters can only vote.
- **Vote Tracking:** Each vote is linked to a user, ensuring that a user can vote only once.
- **Aadhar Card Number:** Each user is uniquely identified by their Aadhar card number, 
    preventing duplicate accounts.

