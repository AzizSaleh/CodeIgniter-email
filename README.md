# Codeigniter Email Library Handler

This plug and play - just copy/paste entire directory into your codeigniter directory, over writing existing files to use.

# Demo

A demo location is set for you at `application/controllers/demo.php`:

```
// Call interface
$this->load->library('ah_email', 'ah_email');

// Send email out, using demo template with following variables
$this->ah_email->send('to.email@gmail.com', 'demo', array(
    'username'  => 'Demo Handler',
    'message'   => 'Hello World',
    'mailtype'  => 'text',
));
```

# Configs Explained

Config file located at `application/configs/email.php` settings are as follows:

```
$config['settings'] = array(
    'from_email'    => 'username@gmail.com',
    'smtp_user'     => 'username@gmail.com',
    'smtp_pass'     => 'password',
    'from_name'     => 'Site Name',
    'smtp_host'     => 'smtp.googlemail.com',
    'smtp_port'     => 465,

    'protocol'      => 'smtp',
    'smtp_crypto'   => 'ssl',

    'mailtype'      => 'html',
    'charset'       => 'utf-8',
    'newline'       => "\r\n",
);
```

Those are the general connection info that you would normally use with the built in email library. I added `from_name` and `from_email` for general settings. The above settings were tested to work with Gmail, if it is not working for you, please scroll down to the debug section for some helpfull information.

```
$config['templates'] = 'emails';
```

This is the location of the templates for the emails. The way this works is that each email message is stored in a view which is loaded and sent as the body. Location starts after `application/views`.

```
$config['templates'] = array(
    // Demo
    'demo'   => array(
        'subject'    => 'Test Demo',
        'send_email' => true,
        'bcc_admin'  => false,
    ),
);
```

Those are the specific email. Each type of email you send must have a template, the template name must also match the view file name in the templates folder stated previous to this config. You can set the subject, as well as if you want to send this email or get a copy of it. On development you should have `send_email` set to false and `bcc_admin` set to true.

# Debug

If email is failing to be sent out, please try the following things:

    1) Make sure that the to email variable is set. You can hardcode an email instead of the variable to see if that is the case, another option is to output the email to variable to see it contains a valid email.

    2) If your provider is setup to require 2 step login. Create a new application password and use that. More info for how it is done on Gmail by visiting: https://support.google.com/accounts/answer/185839

    3) Gmail - Allow less secure apps: If you don't use 2-Step Verification, you might need to allow less secure apps to access your account by visiting: https://www.google.com/settings/security/lesssecureapps

    4) Gmail - If the tips above didn't help, visit: https://www.google.com/accounts/DisplayUnlockCaptcha and follow the steps on the page.

    5) Try changing your password at your provider and using the updated on.

    6) Make sure that your antivirus or other security programs are not blocking that port. Consult google for "how to open port {PORT YOU ARE USING} on {PROGRAM NAME}". For me it happened on Avast which I had to:

        1. Open Avast
    
        2. Click on 'Settings' (upper right corner of page)
    
        3. Click on 'Troubleshooting'
    
        4. Click on 'Redirect Settings'
    
        5. Remove 465 from the list.
    
        6. Click 'OK'
    
        7. Close Avast

    7) If all fails, Google is your best bet. Go to the library `application/library/Ah_Email.php` and uncomment link #100 which should hopefully give you an error message you can research on Google.
