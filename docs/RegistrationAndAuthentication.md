#SquirrelStash Registration and Authentication
Overview of the user authentication and registration process used in SquirrelStash.

## Key Components

* Unique application name
* RSA Public/Private key pair per application
* Installation token (unique identifier)
* [Computer Profile](ComputerProfile.md) (MAC addresses, OS Version, Ram, etc.) 

## Terms

* **Application** - the application to be installed via Squirrel
* **Install** - single installation of software on a specific computer
* **User** - user of the system identified uniquely by email address
* **Organization** - a group of users either identified explicitly or implicitly by common email domain name (e.g., mdsc.com)
* **Version** - individual version of the application with full and possibly delta nuget packages
* **Branch** - release branch related to various versions of the application
* **Channel** - status for a given version (e.g., alpha, beta, production)
* **Installation Token** - token assigned for a given install to help identify different installs

## Registration and Authentication Process
The registration and authentication process is completed by the client at startup. 

### 1. Verify Server
The first step is to verify that the server is the intended server (no DNS hijacking).

1. Client sends SquirrelStash server a randomly generated number.
1. Server returns number encrypted with application private key.
1. Client verifies the number by decrypting with application public key.

### 2a. New Registration
If there is no installation token assigned, the registration check determines if a specific installation needs to be registered before use. 

1. Client prompts the user for registration information (e.g., name, email, and phone)
1. Client sends the registration and Computer Profile information to server
1. Server checks if valid user email (or organization domain). If so, server sends an email with a verification code.
1. User enters the verification code from the email in the client.
1. Client sends the verification code to the server which completes the registration process by returning the Installation Token.
1. Client stores the Installation Token for subsequent executions.

### 2b. Verifying Installation Token
If there is an installation token assigned, the installation token is checked against the Computer Profile. 

1. Client sends the Installation Token along with the Computer Profile to server.
1. Server verifies that the Computer Profile is sufficiently similar to the computer information on file for the Installation Token.
1. If valid, the server updates the computer information on file for the Installation Token.
1. If not valid, the server informs the client that registration is required and goes to 2a for new registration. 

### 3. Check for Updates
Once the installation has been registered, or validated, the client will check for any updates via Squirrel for Windows.

1. Client will generate an update url with the application name, Installation Token, and verification hash encrypted with the public key.
1. Client will use Squirrel for Windows to perform updates in the background with the generated URL.
1. Server will verify the url components and hash using the private key before serving the requested file.
1. Client will download all new configuration files from the vault.
