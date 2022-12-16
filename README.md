# PP5 Social Media Site

Brief intro to project here..
pinterest type site, photo sharing etc 
value it brings to a user
target audience 
goal of the site 
brief overview of features 
eg create post, pin, comment, sign up 

- Am I responsive image here 

# Current Features 

- How do features contribute to better user exerience ??

## Home Page 

- Nav Link image 
- Welcome page image 
- Most recent posts image (hopefully like pinterest)

## Full Post Page

- Full size post image 
- Any comments image 

## Upload Post Page

Explanation of the functionality of the form.
Explain caption, image upload, any extra fields you include.

- Create post form image 

## Edit Post Page

- Screenshot of pre-populated form with the post you navigated from.

# React Components

- Outline the details of all the components you make here..
- Outline functionality, purpose, relation to user stories etc

- Infinite Scroll 
- Search Bar 

# Future Features To Implement 

- Add features you didn't include here..

# The Agile Approach

On my Github repository "pp5 frontend", you can find all of my user stories listed under the issues tab. While in the planning stage of this project, I wrote out all of the stories first. I listed the acceptance criteria for each, along with attaching a label with the amount of story points each one represents. Throughout the development, I adjusted the amount of points for certain user stories as some functionality took me longer than previously anticipated.
I have found that using the kanban board feature on Github has been very helpful for me to keep track of which story I am focusing on at any given time. Also as this project is quite substantial in its requirements, I found that moving over stories from "In-progress" to "Done" helped me to break down the work into smaller bite size chunks. This really helped to prevent me from getting overwhelmed with the amount of functionality I still had left to implement at times.

Throughout each iteration, the project has been manually tested for any issues and bugs. Upon encountering any problems during development, a fix will be applied if possible and a follow up commit detailing the problem and the steps taken to resolve it. All of my fixed and any unfixed bugs can be found further down this read-me with more in depth explanations.

??Sprints?? have been run once a week thoughout development of this project and user stories have been assigned to each one ensuring depending on the length of time and complexity required to implement the features. Stories have been ordered by importance, and any incompleted ones will be added to the backlog and hopefully be implemented in a future iteration.

List some "Epics" here maybe and link them to the corresponding user stories completed to implement the feature..
eg   Epic = User Authentication | User stories = login/logout/signup/signin using socials 
If you have time, maybe make flowchart thingy showing the relationships between them.

Any other Agile info to include?

# Languages/Libraries Used 

### Django Rest Framework 

- Check if i need a seperate readme for the backend?
- If not, outline details of it here

### React JS

- Built using hooks, fucntional components etc etc 
- Anything else to add?

### React-Bootstrap

- used some standard components here 
- Added your own custom CSS to customise further and make your application more unique 

### CSS

- To add my own custom styles alongside bootstrap classes

### Cloudinary 

- Used for image file storage 
- Using an ephemeral file system would result in my image files being deleted after two weeks. To prevent this from happening, I used cloudinary for my image files storage. It keeps the project cleaner by storing the files this way.

### Django Authentication or is it something else?

- More info here..

### Any Text Editors?

Any other libraries you installed add here ..
Why did you use them?

# Design 

## Color Scheme 

- Screenshot of color scheme here
- Why did you use these colors? what effect on ux? 

## Wireframes/Mockups 

- Try to throw one together to post here 
- even if its last minute..

# Deployment 

## Local Deployment



## Live Deployment

## For Your API

The points outlined below, document the steps taken to connect to the ElephantSQL database and then deploy my live API to Heroku

- On GitHub, I forked my repository so it is not deleted after inactivity
- The database used in production is only accessible within Gitpod, so you first nned to create a new database
- Navigate to ElephantSQL.com and navigate to your dashboard or create an account if you do not have one
- Click on the link "Create New Instance"
- Fill in the details required - Your name, select the tiny turtle(free plan) and leave the tags field blank.
- Select the region thats closest to where you are living
- Click "review", ensure all of the information you have given is correct and then select "Create Instance"
- Return to your dashboard and navigate to the database instance name for the project
- Next you will need to copy the database URL that is present, as you will need that for Heroku
- Navigate to heroku.com and go to your dashboard or create an account if you haven't already 
- Click on "New" and then "Create new app"
- select the region that applies to you, give the app a unique name and press create app
- Navigate to the settings tab, and open the config vars
- Add a config var named "DATABASE_URL" and paste in the value that you copied from ElephantSQL
- Use the below command to install the necessary items to connect to your external database
 pip3 install dj_database_url==0.5.0 psycopg2
- In the settings.py file import dj_database_url
- Navigate down to the databases section and update it with the below code
  if 'DEV' in os.environ:
     DATABASES = {
         'default': {
             'ENGINE': 'django.db.backends.sqlite3',
             'NAME': BASE_DIR / 'db.sqlite3',
         }
     }
 else:
     DATABASES = {
         'default': dj_database_url.parse(os.environ.get("DATABASE_URL"))
     }
- Next, go to your env.py file and add a new environment variable as shown below
os.environ.setdefault("DATABASE_URL", "<your PostgreSQL URL here>")
- Temporarily comment out the below code so Gitpod can connect to the new database
os.environ['DEV'] = '1'
- The next step is to use the below code to migrate your changes to the database
 python3 manage.py migrate
- In the terminal of gitpod, install gunicorn and update your requirements.txt file using the two below commands
 pip3 install gunicorn django-cors-headers
  pip freeze --local > requirements.txt
-  You now need to create a Procfile and add the below code to it 
release: python manage.py makemigrations && python manage.py migrate
 web: gunicorn <your project name here>.wsgi
- Next you need to update the value of ALLOWED_HOSTS in your settings.py file to the below code 
 ALLOWED_HOSTS = ['localhost', '<your_app_name>.herokuapp.com']
- Add 'corsheaders' to your list of INSTALLED_APPS in settings.py
- Add corsheaders middleware to the top of the MIDDLEWARE as shown below
MIDDLEWARE = [
     'corsheaders.middleware.CorsMiddleware',
- Under the middleware list, set the ALLOWED_ORIGINS for the network requests made to the server with the below code
if 'CLIENT_ORIGIN' in os.environ:
     CORS_ALLOWED_ORIGINS = [
         os.environ.get('CLIENT_ORIGIN')
     ]
 else:
     CORS_ALLOWED_ORIGIN_REGEXES = [
         r"^https://.*\.gitpod\.io$",
     ]
- Remove the value for the secret key and replace it with the below code instead
SECRET_KEY = os.getenv('SECRET_KEY')
- Now set a new value for your secret key in the env.py file as outlined below
os.environ.setdefault("SECRET_KEY", "CreateANEWRandomValueHere")
- Set the debug value to the below code to ensure its only true in development mode
 DEBUG = 'DEV' in os.environ
- Comment the DEV variable back in, in the env.py file that we commented out earlier
- Lastly, commit and push your changes to github
- Back on the Heroku dashboard, we now just need to add two final config vars
- Add a SECRET_KEY and a value of your choice 
- Copy and paste the CLOUDINARY_URL from cloudinary.com and add that value to your config vars also 
- Navigate to Deploy tab on heroku
- Connect to your GitHub account and type your repository name 
- Click deploy and your project should now be live
