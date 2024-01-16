Node.js Deployment With Render
ElephantSQL
• Host for PostgreSQL databases
• Have excellent commercial options, but also a free, small instance
Getting a database
Create account at ElephantSQL using GitHub
Create a “Tiny Turtle” (free) instance
Select region: US-West-1 (even if others are closer to you)
 If you get an error selecting US-West-1, pick US-East-1
Confirm and create
Click on your new instance and copy the URL
Seeding your new database
$ pg_dump -O jobly | psql (url you copied here)
This dumps your existing jobly database and loads it in your new database. If you are deploying a different application such as your capstone, you will need to update this line of code. Please note, you will need to use a separate service to deploy your front-end site. We will detail how to use surge later in this handout.
Checking your database
$ psql (url you copied here)
Setting up your app
Create an account at Render using GitHub
From dashboard, create a new instance of “Web service”
Connect to your repository
Give it a name (this must be globally unique)
Choose advanced, and enter environmental variables:
DATABASE_URL: URL from ElephantSQL (change postgres: → postgresql:)
SECRET_KEY: anything you want (to be secure: long and random)
 Choose “Create Web Service”
Debugging your app
From the dashboard for your app, you can view the logs
Updating your app
When you push to your GitHub repo, it will automatically redeploy your site.
You can turn that off under Settings → Auto-Deploy, and then can do manual deploys.
Deploying Your Front-end (Such as a React App)
That’s all for the Jobly project in Node.js. If you are working on your Capstone or the React version of Jobly, please continue.

If you are working on a project such as your Capstone or React Jobly, you’ll need to deploy the front-end using a different tool. 
We’re going to be showing you a tool called Surge, which is a very easy way to deploy static websites!
Make sure that you have the surge command installed. You can run this command anywhere in the Terminal:
$npm install --global surge
If you are deploying React Jobly, make the following change in your JoblyApi.js. If you are working on your Capstone, make this change anywhere else you make requests to localhost:3001 make sure you have the following:
const BASE_URL = process.env.REACT_APP_BASE_URL || "http://localhost:3001";
Next, let’s make sure we define the environment variable for our frontend app. YOUR_RENDER_BACKEND_URL should be something like https://YOUR_BACKEND_APP_NAME.render.com.
Make sure you are running the following commands in the jobly-frontend folder
$REACT_APP_BASE_URL=YOUR_RENDER_BACKEND_URL npm run build
$cp build/index.html build/200.html
$surge build
