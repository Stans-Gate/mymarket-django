This is a website built with django that supports functionalities like user auth, communication between users, dashboard for displaying items you want to sell, form handling and customizations. 

How to boot up the website: 
1. git clone repo
2. use the command inside the mymarket folder: python manage.py runserver

How to play around with the website: 
1. Signup for your account 
2. Login to your account
3. Add items that you want to display with the New Item
4. Browse other users items in Browse
5. Check all the items you displayed in dashboard
6. Check inbox for messages from potential buyers

Time spent:
I don't remember how much I spent, but definitely more than 5. 

Project Structure:
The project is modular, with each app handling a specific feature. Here’s a breakdown:
core: Manages user authentication and site-wide utilities.
conversation: Handles messaging between users.
dashboard: Displays user-specific information and provides functionality for managing listings.
item: Manages item listings, including creation, editing, and deletion.

Each app follows Django's MTV architecture (Model-Template-View), with urls.py in each app routing requests to appropriate views.

The core app relies on Django's built-in User model, extended or customized via AbstractUser. Key elements:
Sign-up, login, logout:
URLs in core/urls.py route to Django's auth views or custom views.
Templates in core/templates/ provide UI for these actions.
Signals (e.g., post_save) might be used to create user profiles upon registration.

The conversation app handles private messages:

Models:
Likely includes Conversation and Message models.
Conversation links two users and tracks their messages.
Message has a ForeignKey to a Conversation and stores the message content, sender, and timestamp.
Views:
Views fetch conversations for a user (conversation_list) and individual messages (conversation_detail).
New messages are created through POST requests.
Templates:
Templates display conversations in a threaded format.
JavaScript (via Django templates or static files) may enhance real-time communication.


The dashboard app provides a user-centric view of their activity:
Views:
Fetch listings belonging to the authenticated user.
Calls the item app's models to get data.
Contains edit and delete functionalities, which are routed to specific endpoints in the item app.
URLs:
Dashboard URLs point to views that aggregate user-specific data (e.g., /dashboard/).
Templates:
Use Django's templating system with context variables for dynamic content (e.g., user’s items, statistics).

The item app is central to the project and handles all operations related to items:

Models:

Item model stores:
Title, description, price, image, category.
Relationships (ForeignKey) to the User model.
Images are managed using Django’s ImageField and Pillow library.
Views:

CRUD Operations:
CreateView: For adding new items (accessible from dashboard or a specific route).
UpdateView: For editing items.
DeleteView: To remove items.
Detail View:
Displays an individual item’s details and its seller information.
Forms:

Django forms validate input for creating/editing items.
Customizations like widgets (e.g., for image uploads) enhance the user experience.
Media Files:

Media files (e.g., images) are uploaded to a specified directory and served in templates.


Form Handling and Customization:
The project uses Django's form system for clean and robust user input handling:

Custom Forms:

Forms extend forms.ModelForm for easy integration with models.
Custom widgets (e.g., file inputs, dropdowns) enhance form fields.
Validation methods (clean_field_name) are used for custom rules.
CSRF Protection:

Django’s built-in CSRF middleware ensures secure form submissions.


Routing and Communication Between Components:
URL Dispatching:

Each app has its own urls.py file, included in the main project’s urls.py.
Example:
/items/<id>/ -> item app handles item detail.
/dashboard/ -> dashboard app aggregates user-specific data.
/conversations/<id>/ -> conversation app displays messages.
Context Processors:

Used to inject global data (e.g., user profile, notifications) into templates