## Project installation

1. Go (with the Terminal or CMD) in the folder you want to have the project 
2. Clone the repo with the following command : `git clone https://github.com/MGDev-FR/troov_test.git`

3. Go to the folder backend (`cd backend`) and install the dependencies : `npm install`
4. Go to the folder frontend (`cd frontend`) and install the dependencies : `npm install`

### Launch the server backend
- In the folder backend : `nodemon server`
- The backend server is launched on : `http://localhost:3001`

### Launch the server frontend
- In the folder frontend : `npm run dev`
- The frontend server is launched on : `http://localhost:3000`

### Use the email on local
- Launch maildev with the following command : `maildev --web 1080 --smtp 1025 --ip 127.0.0.1 --hide-extensions STARTTLS`
- Then you can access to the email sent on : `http://127.0.0.1:1080/`