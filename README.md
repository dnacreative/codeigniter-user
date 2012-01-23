# Codeigniter User Library V. 1.1
This library is a *very simple* but powerful user auth library for CodeIgniter. The library uses SHA1 hashing with salt to store passwords automatically.
## Quick Start
This is a quick guide to help you run your user system.

* Import the _database schema.sql_ to your database. There are 3 tables with users and permissions and the relation table.
* Copy the libraries to your application/libraries folder. If you want to see the demo login page, marge all the files (including the views and controllers).
* Change your encryption key on your application _config.php_ file and also set up your database connection config properly if you haven't yet.
* Load your database library automatically. This can be done on _autoload.php_, under _libraries_ session. Just type "database" in the array.
* *If you installed the demo*, head to http://example.com/index.php/user and try out your new user auth system.

## Usage
Here is listed some of the most common actions when managin the user auth flow on your site. Examples of:
### Logging a user in
You may put this in the "login" method.

	if($this->user->login($login, $password)){
		redirect('private_page');
	} else {
		echo "Wrong credentials!";
	}
### Validating a session (user is logged in)
You can create custom actions with this function.

	if($this->user->validate_session()) {
		echo "This is secret.";
	}

### Auto redirect on invalid session
Auto redirect function if the user isn't logged in. The first parameter tell where to redirect if theres a invalid session (controller/method). You can put this under the controller constructor if you want to lock all the controller.

	$this->user->on_invalid_session('home/login');

### Auto redirect on valid session
Auto redirect function if the user is logged in. The first parameter tell where to redirect if theres a valid session (controller/method). Ideal for login pages.

	$this->user->on_valid_session('home/login');

### Get the current logged in name/id
Simple way to retrieve the logged user name and login.

	echo $this->user->get_name();
	echo Welcome, $this->user->get_id();

### Check permission
Checks if user has the received permission. The first parameter is the permission.

	if($this->user->has_permission('editor')){
		$this->load->view('editor_menu');
	}

### Logout user
Removes all session from browser. 

	$this->user->destroy_user();


## Managing users
There is a separated library for user managing. After setting up the database config, load up the user_manager library. There are some examples of:

### Adding a new user
	$fullname = "Johnny Winter";
	$login = "john"
	$password = "123becarefulwithafool";
	$active = true;
	$permissions = array(1, 3);
	$new_user_id = $this->user_manager->save_user($fullname, $login, $password, $active, $permissions);

### Change user password or login on the fly
This function must be called after you changed the user's password in the database.

	// changing the user login and password with received data from form
	$this->user->update_pw($this->input->post('new_password'));
	$this->user->update_login($this->input->post('new_login'););


### Creating a permission
	$permission_id = $this->user_manager->save_permission('editor', 'The editors of my website.');

### Deleting a user
	if( $this->user_manager->delete_user($user_id)){
		echo "User was deleted.";
	}

## Codeigniter Sparks
[Codeigniter Sparks](http://getsparks.org/) is an amazing project. I'm on that, when I got some free time I'll read how can I put my package on Sparks!

---
# Changelog
> Version 1.1
>> Fixed some broken functions.
>> Updated doc with brief description of methods.
> Version 1.0
>> Added sha1 support.
>> Added password salting support.